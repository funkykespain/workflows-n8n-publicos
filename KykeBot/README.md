<p align="center"\>
<img src="profile.png" alt="KykeBot Profile" width="250"/\>
</p\>

# 1. KykeBot: Asistente Personal Multimodal con Orquestación de Agentes

Este workflow de n8n da vida a **"KykeBot"**, un asistente personal avanzado que opera a través de **WhatsApp** y actúa como un "mayordomo digital" para **Enrique Aranda**.

El bot ha evolucionado de ser un simple chatbot de texto a una **IA Multimodal Completa**. Ahora es capaz de **escuchar notas de voz, ver imágenes y leer documentos**, actuando como un filtro inteligente de primera línea. Su propósito estratégico es doble:
1.  **Descongestionar el canal:** Filtra consultas recurrentes de ex-clientes, resolviéndolas o desviándolas automáticamente.
2.  **Tarjeta de Presentación Interactiva:** Para nuevas oportunidades, actúa como un representante profesional, utilizando una arquitectura de **Agentes Orquestados** (potenciada por **OpenRouter**) para agendar citas y responder preguntas técnicas sobre el perfil de Enrique basándose en su CV (RAG).

El núcleo del sistema es un nodo `Switch` avanzado que utiliza **Expresiones Regulares (Regex)** para enrutar la intención del usuario o el tipo de archivo con precisión quirúrgica:

1.  **Gestión de Suscripciones:** Comandos directos (`alta`/`baja`) para la gestión del boletín de noticias en Google Sheets.
2.  **Filtro de Identidad:** Detecta y silencia los mensajes del propio Enrique para permitir el uso normal de WhatsApp.
3.  **Procesamiento Multimodal:** Una nueva capa de percepción que transcribe audios (Whisper), describe imágenes (Ollama Vision) y extrae texto de PDFs antes de invocar a la IA.
4.  **Gestión de Formatos:** Intercepta archivos no soportados (Office/Video) y devuelve respuestas amables solicitando formatos legibles, ahorrando costes de IA.
5.  **Agente de IA Conversacional (Orquestador):** El cerebro del sistema. Una arquitectura modular que coordina sub-agentes especialistas (Calendario, Email, Memoria) seleccionando dinámicamente el mejor LLM para cada tarea vía **OpenRouter**.

---

## 📍 2. Despliegue en Producción

Puedes interactuar con este workflow en tiempo real a través del canal principal de WhatsApp de Enrique Aranda:

  * **Canal de WhatsApp:** [**+34 665 65 64 04**](https://wa.me/34665656404)

---

## ⚙️ 3. Requisitos previos

Para que este workflow funcione con todas sus capacidades, necesitarás:

  * Una instancia de **n8n** (versión reciente para soporte de LangChain).
  * **Evolution API** como puerta de enlace de WhatsApp.
  * **Qdrant** (Base de datos vectorial para RAG).
  * **Redis** (Para memoria de chat y persistencia de estado de usuario).
  * **Google Sheets** (Gestión de suscriptores).
  * **Servicios Locales (Docker):**
    * **Whisper ASR Webservice:** Para transcripción de audio local (sin coste de API).
    * **Ollama (con DeepSeek/LLaVA):** Para análisis de visión (OCR e imágenes).
  * **Credenciales de API:**
      * **OpenRouter:** (Clave principal) Para acceder a modelos como Llama 3.3, Qwen 2.5, Gemini Flash, etc.
      * **CloudConvert:** Para renderizado de PDFs complejos (fallback).
      * **Gmail y Google Calendar:** Para las herramientas de los agentes.
      * **SerpAPI:** Para búsqueda web.

---

## 🐳 4. Despliegue de Servicios Locales (Docker)

Para garantizar la soberanía de los datos y reducir costes, los módulos de percepción (Audio y Visión) se ejecutan en contenedores locales.

### Whisper (Transcripción de Audio)
El bot utiliza una API local de Whisper para transcribir notas de voz sin coste. Debes desplegar este contenedor en tu servidor (accesible desde n8n):

```bash
docker run -d \
  --name whisper-asr \
  -p 9000:9000 \
  -e ASR_MODEL=large-v3 \
  -e ASR_ENGINE=faster_whisper \
  onerahmet/openai-whisper-asr-webservice:latest
````

  * **Configuración en n8n:** El nodo *Whisper Local* debe apuntar a `http://nombre-del-contenedor:9000/asr`.
  * **Variables:** Se recomienda `ASR_MODEL=large-v3` para máxima precisión en español y `faster_whisper` para evitar *timeouts* en audios largos.

### Ollama (Visión e Imágenes)

Para el análisis de imágenes (OCR y descripción), se requiere una instancia de Ollama con un modelo multimodal:

```bash
docker run -d \
  --name ollama \
  -p 11434:11434 \
  -v ollama:/root/.ollama \
  ollama/ollama
```

  * **Modelo recomendado:** Ejecuta `ollama run deepseek-ocr` (o `llava`) dentro del contenedor para descargar el modelo necesario.

---

## 📦 5. Archivos incluidos

  * `KykeBot.json`: El export completo del workflow de n8n.
  * `profile.png`: Imagen de perfil del bot.
  * `schema.png`: Diagrama visual actualizado del workflow.
  * `README.md`: Este documento explicativo.

---

## 🚀 6. Instalación e Importación

1.  Descarga el archivo `KykeBot.json`.
2.  En tu instancia de n8n, ve a **Import > From File**.
3.  Selecciona el archivo `KykeBot.json` y guarda el workflow.
4.  **Configuración de Credenciales:** Deberás crear y asignar las credenciales correspondientes en los nodos (ver sección 8).
5.  **Configuración de Webhook:** Apunta el nodo `Webhook` para recibir los *callbacks* de tu instancia de Evolution API.
6.  **Servicios Externos:** Asegúrate de que tus contenedores Docker de Whisper y Ollama son accesibles desde n8n.

---

## 🧩 7. Estructura del Workflow

El flujo inicia con un `Webhook` y un preprocesado (`MapeaDatos`) que gestiona la dualidad de identificadores de WhatsApp: utiliza el `sessionId` para el envío de mensajes (compatible con `@lid`) pero estandariza el `codeID` (`@s.whatsapp.net`) para guardar el histórico en Redis y permitir retomar conversaciones antiguas.
![n8n Workflow](schema.png)

El flujo se dirige a un nodo `Switch` principal (`Alta Noticias?`) que actúa como un enrutador inteligente basado en Regex, dividiendo el trabajo en las siguientes ramas lógicas:

### 1. Rama 1: Gestión del Boletín de Noticias
Gestiona comandos simples de suscripción sin necesidad de invocar a la IA.
* **Intención:** El usuario escribe `alta noticias` o `baja noticias`.
* **Acción:** El workflow interactúa directamente con **Google Sheets** (`Añadir a noticias`, `Comprobar en BBDD`, `Dar de baja`) para añadir o eliminar el `sessionId` del usuario de la lista de distribución.
* **Respuesta:** Envía una confirmación simple (`Confirma Alta`, `Confirma Baja`) al usuario.
* **Proyecto relacionado:** [Workflow de Envío de Noticias](https://github.com/funkykespain/workflows-n8n-publicos/tree/main/Noticias)

### 2. Rama 2: Filtro de Mensajes de Enrique
Esta es una rama de "no operación" (NoOp) crucial para un asistente personal.
* **Intención:** El mensaje proviene del propio Enrique Aranda (identificado por su `name` o `pushName`).
* **Acción:** El flujo se dirige a un nodo `Nada` (NoOp) y termina.
* **Propósito:** Esto evita que el bot responda a los mensajes de Enrique o intente tener una conversación consigo mismo, permitiéndole usar su WhatsApp con normalidad.

### 3. Rama 3: Procesamiento Multimodal
Es el "aparato sensorial" antes de que la IA "piense".
* **Audio:** Se envía al nodo `Whisper Local` (Docker) para transcripción STT.
* **Imagen:** Se envía a `Ollama` (Vision Model) para descripción y OCR en local.
* **PDF/Documentos:** Se intenta la extracción nativa de texto. Si falla (PDF escaneado), se procesa con **CloudConvert** para convertirlo a imagen y luego pasarlo por visión.
* **Resultado:** El contenido extraído se inyecta en el contexto del sistema mediante el nodo `Procesar Estado`, generando una nota interna: `[SYSTEM NOTE: El usuario envió un audio que dice...]`.

### 4. Rama 4: Archivos No Soportados
* **Intención:** Detección de formatos Office (Word/Excel) o Video.
* **Acción:** Devuelve una respuesta aleatoria amable solicitando el envío en PDF, imagen o texto plano.
* **Propósito:** Ahorrar recursos y evitar alucinaciones del LLM con binarios ilegibles.

### 5. Rama 5: Conversación con Agente AI (Orquestador)

Esta es la rama principal y más compleja, que se activa cuando el `messageType` es `conversation` (texto) o tras procesar un archivo en la rama anterior.

El propósito de este agente va más allá de una simple charla; está diseñado para **filtrar y cualificar al usuario**. Detecta si es un ex-cliente con una consulta recurrente (desviándolo de forma eficiente) o un nuevo contacto interesado en el perfil profesional de Enrique. En este último caso, el bot actúa como una tarjeta de presentación proactiva, utilizando RAG para ofrecer detalles del CV y gestionando el agendamiento de citas, asegurando que solo las interacciones de valor lleguen a Enrique.

El flujo de ejecución es el siguiente:

1.  **Carga de Estado y Contexto Enriquecido:**
    * El flujo primero lee **Redis** (`Leer Estado de Redis`) para obtener el perfil persistente del usuario (nombre, email, resumen de charlas anteriores).
    * **El Corazón Lógico:** Un nodo de código JavaScript (`Procesar Estado y Definir Flags`) actúa como *pre-procesador*. Combina el historial del usuario con el input actual. Si hubo un archivo adjunto (audio, imagen, PDF), inyecta la transcripción o el OCR generado en la rama anterior dentro de una nota de sistema (`[SYSTEM NOTE: ...]`). Esto permite al Agente "ver" y "escuchar" sin procesar archivos directamente.

2.  **El Agente AI (Orquestador vía OpenRouter):**
    Este es el cerebro del bot. Técnicamente, es un **Agente Orquestador (Orchestrator)** bajo una arquitectura *Plan-and-Execute*. No es un agente monolítico; su función principal es analizar la intención y delegar la tarea en especialistas.

    Gracias a la integración con **OpenRouter**, el agente no depende de un solo modelo. Puede utilizar modelos potentes (como **GPT-4o** o **Mistral Large**) para el razonamiento complejo, manteniendo la flexibilidad de cambiar de proveedor sin tocar el código.

    * **Memoria:** Utiliza `Redis Memo` para mantener el hilo de la conversación con latencia ultrabaja.
    * **RAG (Retrieval-Augmented Generation):** Conectado a `Qdrant Vector Store` para extraer información veraz sobre la trayectoria, stack técnico y proyectos de Enrique, reduciendo alucinaciones.

3.  **Ecosistema de Agentes Subordinados (Tools):**
    El agente principal invoca a otros agentes especializados para ejecutar acciones. OpenRouter permite asignar a cada uno el modelo más eficiente (coste/rendimiento) para su tarea:

    * **`Gestor Email` (Agente):** Utiliza la herramienta `Gmail` para redactar y enviar notificaciones. Se beneficia de modelos con alta capacidad de redacción (ej. **Llama 3.3 70B**).
    * **`Gestor Calendario` (Agente):** Utiliza un cliente MCP (`Calendar`) para gestionar la agenda. Usa modelos rápidos y precisos en estructuras JSON (ej. **Gemini 2.0 Flash**) para no fallar en las fechas.
        * *Proyecto relacionado:* [Servidor MCP-Calendar](https://github.com/funkykespain/workflows-n8n-publicos/tree/main/MCP-Calendar)
    * **`Gestor Redis` (Agente):** Utiliza un cliente MCP (`Redis`) para guardar silenciosamente los datos que el usuario proporciona (nombre, email) en la base de datos de estado.
        * *Proyecto relacionado:* [Resumen de Conversación](https://github.com/funkykespain/workflows-n8n-publicos/tree/main/Resumen-Conversacion)
    * **`SerpAPI`:** Herramienta de búsqueda web para datos en tiempo real.
    * **`Think`:** Herramienta de razonamiento interno para planificar pasos complejos antes de responder.

4.  **Respuesta y Contingencia:**
    * La respuesta final generada por el `AI Agent` se envía a WhatsApp mediante el nodo `Respuesta KykeBot`.
    * **Alta Disponibilidad:** Si el Agente falla (por ejemplo, por un error de "active run" o sobrecarga de API), el flujo activa automáticamente una **rama de contingencia** (`Error active run?`) que espera unos segundos y reintenta la ejecución, garantizando que el usuario nunca se quede sin respuesta.

---

## 🔧 8. Optimizaciones y Características Clave

Este workflow no es solo un chat; es una arquitectura diseñada para la eficiencia de costes, la robustez técnica y la utilidad comercial real.

### 🧠 Arquitectura de Orquestación (Multi-Agente + OpenRouter)
El sistema evoluciona el concepto de IA monolítica hacia una **orquestación modular** potenciada por **OpenRouter**:
* **Reducción de Carga Cognitiva:** En lugar de un solo LLM intentando manejar 10 herramientas (propenso a alucinaciones), el **Agente Orquestador** actúa como un gerente: solo decide *a quién* delegar.
* **Especialización de Modelos (Coste/Eficacia):** Gracias a OpenRouter, asignamos el modelo ideal para cada sub-agente, optimizando drásticamente el coste por token:
    * *Orquestador:* **GPT-4o / Mistral Large** (Razonamiento complejo).
    * *Calendario/Email:* **Llama 3 / Gemini Flash** (Rapidez y precisión en JSON).
    * *Memoria:* **Qwen 2.5** (Resumen eficiente).
* **Alta Disponibilidad (Fallback):** Si un proveedor de IA cae, OpenRouter redirige automáticamente a otro modelo equivalente, garantizando que el bot nunca se quede mudo.

### 🛡️ Filtrado Estratégico ("Tarjeta de Presentación")
El bot actúa como un **cualificador de leads** diseñado para ahorrar tiempo real a Enrique:
* **Gestión de Ex-Clientes:** Detecta consultas recurrentes de bajo valor comercial y las resuelve o desvía automáticamente.
* **Potenciación de Nuevas Oportunidades:** Identifica *networking* o nuevos proyectos y despliega todo su potencial (RAG + CV) para actuar como una tarjeta de presentación interactiva de alto nivel.
* **Enrutamiento Preventivo (Switch + Regex):** Ahorra costes de inferencia filtrando peticiones simples (`alta noticias`) o archivos no soportados (`Word/Excel`) *antes* de que lleguen a la IA, devolviendo respuestas predefinidas inmediatas.

### 👁️ Percepción Multimodal (Contexto Enriquecido)
Antes de "pensar", el bot "percibe". Al procesar audios e imágenes en una capa previa (Whisper/Ollama):
* **Humanización:** Permite responder naturalmente a *"Mira esta foto"* o *"Escucha mi audio"*, algo que un chatbot de texto tradicional no puede hacer.
* **Ahorro de Tokens:** El LLM recibe una transcripción limpia en lugar de tener que procesar binarios pesados, reduciendo la ventana de contexto necesaria y mejorando la precisión de la respuesta.

### 💾 Persistencia y Robustez Técnica
* **Estandarización de IDs (LID vs JID):** Soluciona la fragmentación de identificadores de WhatsApp. El bot fuerza el formato `@s.whatsapp.net` internamente, garantizando que el historial se mantenga unificado independientemente de si el usuario escribe desde el móvil (JID) o un dispositivo vinculado (LID).
* **Estado de Usuario en Redis:** No solo guarda el chat, sino el "perfil" del usuario (`nombre`, `email`, `preferencias`). Esto permite al bot saludar por el nombre a un usuario que vuelve meses después.
* **Contingencia de "Active Run":** Implementa un bucle de espera inteligente (`Wait` + `Retry`) que gestiona los errores de concurrencia de la API, evitando que el bot falle silenciosamente si hay picos de tráfico.

### 🛠️ Herramientas Especializadas (Docker & MCP)
* **Soberanía de Datos (Docker):** Servicios críticos como la transcripción (Whisper) o la visión (Ollama) corren en contenedores locales, reduciendo la dependencia de APIs externas y costes recurrentes.
* **Clientes MCP (Model Context Protocol):** La integración de servidores MCP para Calendario y Redis centraliza la lógica compleja fuera del flujo visual, haciendo que el mantenimiento sea más limpio y modular.

---

## ⚙️ 9. Credenciales Necesarias

Asegúrate de configurar estas credenciales en n8n:

* `evolutionApi`: Conexión con WhatsApp.
* `openRouterApi`: **(Nueva)** Para el acceso unificado a LLMs.
* `cloudConvertApi`: **(Nueva)** Para renderizado de PDFs complejos.
* `ollamaApi`: **(Nueva)** Para conexión con tu servidor local de visión.
* `qdrantApi`: Base de datos vectorial.
* `redis`: Para memoria y estado.
* `googleCalendarOAuth2Api` & `gmailOAuth2`: Herramientas de gestión.
* `serpApi`: Búsqueda web.
* `googleSheetsOAuth2Api`: Gestión de noticias.

---

## 🧾 10. Ejemplo de Ejecución

**Entrada del Usuario:**
> "Hola, te mando este audio para ver si Enrique puede reunirse mañana." (Archivo de Audio adjunto)

**Flujo Interno:**
1.  **Webhook:** Recibe el audio.
2.  **Switch:** Detecta `audioMessage` -> Rama Multimodal.
3.  **Whisper:** Transcribe el audio a texto: *"Hola, te mando este audio para ver si Enrique puede reunirse mañana."*
4.  **Procesar Estado:** Genera el prompt: `[SYSTEM NOTE: El usuario envió una nota de voz: "Hola, te mando este audio..."]`.
5.  **AI Agent (Orquestador):** Lee la nota. Decide invocar al `Gestor Calendario`.
6.  **Gestor Calendario:** Recibe: *"Revisar disponibilidad para mañana"*. Consulta la herramienta `Calendar`.
7.  **Respuesta:** El Agente responde: *"He escuchado tu audio. He consultado la agenda y Enrique tiene un hueco mañana a las 11:00. ¿Te va bien?"*.

---

## 🔧 11. Personalización

* **Cambiar la Persona:** Edita el *system prompt* del nodo **`AI Agent`** para modificar el tono o las directrices.
* **Cambiar Modelos:** Gracias a OpenRouter, puedes cambiar el modelo de cualquier agente (Principal o Subordinados) simplemente seleccionando otro ID en el nodo correspondiente, sin cambiar la lógica.
* **Base de Conocimiento:** Apunta el nodo `Qdrant Vector Store` a otra colección para cambiar el "cerebro" de datos del bot.

---

## 🧑‍💻 12. Autor

Desarrollado por [Enrique Aranda](https://www.linkedin.com/in/earanda/)
(Workflows públicos de `funkykespain`).

---

## 📄 13. Licencia

Este proyecto se distribuye bajo la licencia MIT.

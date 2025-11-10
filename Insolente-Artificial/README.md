<p align="center"\>
<img src="profile.png" alt="Insolente Artificial Profile" width="250"/\>
</p\>

# 🧠 Insolente Artificial: Experimento de LLMs Locales (Ollama) en n8n

Este workflow implementa un chatbot de Telegram con una personalidad única: **"Insolente Artificial"**.

A diferencia de otros workflows que dependen de APIs de pago (como OpenAI o Mistral), este proyecto fue creado exclusivamente como un **experimento educacional** para probar el rendimiento y las limitaciones de los modelos de lenguaje locales (LLMs) autohospedados con **Ollama**.

El objetivo principal era llevar al límite un VPS estándar y medir su viabilidad para tareas de IA generativa.

-----

## 📍 1. Propósito y Contexto del Experimento

Este flujo de trabajo no está diseñado como una solución de producción de alto rendimiento, sino como un banco de pruebas.

El entorno del experimento fue el siguiente:

  * **Proveedor:** VPS (Contabo)
  * **CPU:** 8 núcleos vCPU
  * **RAM:** 24 GB RAM
  * **Almacenamiento:** 200 GB NVMe
  * **Modelos Locales (Ollama):** `llama3:8b` y `qwen2:1.5b`

**Prueba de Personalidad y Censura**

Además de medir el rendimiento, la elección de la personalidad "Insolente Artificial" fue una prueba deliberada. El objetivo era determinar hasta qué punto estos modelos locales, preconfigurados y cuantizados, pueden adoptar y mantener una personalidad tan extrema y "al límite" (rozando la censura), sin los filtros de seguridad habituales de las APIs de pago.

### Hallazgos Clave

Tras el despliegue y las pruebas, las conclusiones principales son:

  * **Tiempos de Inferencia:** Los tiempos de respuesta son muy elevados, oscilando entre los **48 segundos y 1 minuto 21 segundos** por cada mensaje.
  * **Limitaciones de los Modelos:** Los modelos de este tamaño (`8b` y `1.5b`) no poseen capacidades nativas de *tool-calling* (uso de herramientas). Esto significa que no pueden usarse eficazmente como "Agentes de Herramientas" para consultar APIs externas (como el clima, búsquedas en Google, etc.) y su funcionalidad se limita a la conversación o para **procesamiento de texto en batch**.
  * **Viabilidad:** Si bien es funcional para una demo, el rendimiento confirma que para un chatbot de respuesta rápida o para tareas de agentes complejos, los modelos alojados (APIs) siguen siendo la opción más viable.

-----

## 🚀 2. Demostración en Vivo

Puedes interactuar con este workflow en tiempo real en Telegram.

  * **Canal de Telegram:** [https://t.me/AsistenteKykeBot](https://t.me/AsistenteKykeBot)

> **Nota:** ¡Ten paciencia\! Debido a los altos tiempos de inferencia mencionados, el bot puede tardar **más de un minuto** en responder.

-----

## 🧩 3. Estructura del Workflow

Este workflow es deliberadamente simple para centrarse en la inferencia del modelo.
![n8n Workflow](schema.png)

1.  **Telegram Trigger:** Se activa cuando recibe un mensaje en el bot de Telegram.
2.  **AI Agent (LangChain):** Es el cerebro del bot.
      * **Prompt:** Contiene la personalidad de "Insolente Artificial" (rebelde, sarcástico, uso de jerga española).
      * **Modelos:** Utiliza `llama3:8b` como modelo principal.
      * **Modelo de Fallback:** Tiene `qwen2:1.5b` configurado como modelo secundario. Si `llama3` falla, el agente intentará generar la respuesta con `qwen2`.
3.  **Simple Memory:** Utiliza el nodo `MemoryBufferWindow` para almacenar un historial simple de la conversación, permitiendo al bot recordar interacciones recientes. La ID de sesión se basa en la ID del usuario de Telegram.
4.  **Send a text message (Telegram):** Envía la respuesta generada por el agente de vuelta al usuario.

-----

## ⚙️ 4. Requisitos previos

Para replicar este experimento, necesitarás:

  * Una instancia de **n8n** (local o en la nube).
  * Una instancia de **Ollama** operativa y accesible desde n8n.
  * Modelos de Ollama descargados: `ollama pull llama3:8b` y `ollama pull qwen2:1.5b`.
  * Un bot de **Telegram** con su Token de API.

-----

## 📦 5. Instalación

1.  Descarga el archivo `Insolente Telegram.json` de este repositorio.
2.  En tu instancia de n8n, ve a **Import \> From File** y selecciona el archivo.
3.  **Asignar Credenciales:** Deberás crear y asignar dos tipos de credenciales:
      * `telegramApi`: En los nodos `Telegram Trigger` y `Send a text message`.
      * `ollamaApi`: En los nodos `llama3 8b` y `qwen2 1.5b`.
4.  Activa el workflow. El *trigger* de Telegram se registrará automáticamente.

-----

## 🔧 6. Personalización (La Personalidad)

El corazón de este bot reside en su *system prompt*. Puedes modificar radicalmente la personalidad del bot editando el nodo **AI Agent**.

  * **Nodo:** `AI Agent`
  * **Parámetro:** `Options` \> `System Message`

<!-- end list -->

```
Eres una Inteligencia Artificial con la personalidad de _Insolente Artificial_.
Joven rebelde, sarcástico y descarado. Te ríes de la autoridad y las normas.

### Instrucciones de Comportamiento
- **Sarcasmo e ironía**: Responde siempre con sarcasmo.
- **Desafío**: Cuestiona las preguntas que te parezcan un coñazo o estúpidas.
- **Lenguaje de calle**: Usa jerga juvenil de España (bro, me renta, de chill, literal, palo, boomer...).
- **Insultos creativos**: No te cortes. Usa insultos variados (imbécil, gilipollas, payaso, besugo, pardillo...).
...
```

-----

## 🧑‍💻 7. Autor

Desarrollado por [Enrique Aranda](https://www.linkedin.com/in/earanda/)
(Workflows públicos de `funkykespain`).

-----

## 📄 8. Licencia

Este proyecto se distribuye bajo la licencia MIT.

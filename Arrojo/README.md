# 🧠 1. ArrojoBot: Chatbot de Telegram con RAG y Agentes

Este workflow de n8n implementa un chatbot avanzado para la banda de rock **"Arrojo"**, accesible tanto por **Telegram** como por un **webhook** para su sitio web oficial.

El bot (apodado "ArrojoBot") está diseñado para responder a las preguntas de los fans utilizando una arquitectura de Agentes (Planificador + Ejecutor) y RAG (Retrieval-Augmented Generation). Combina una base de conocimiento vectorial interna (alimentada desde Google Drive) con APIs externas en tiempo real (Spotify, Facebook, YouTube, Wikipedia) para dar respuestas precisas y mantener una personalidad "en personaje".

El flujo también incluye una rama de "indexación" para poblar la base de datos vectorial.

-----

## 📍 2. Despliegue en Producción

Puedes interactuar con este workflow en tiempo real en los siguientes canales:

  - **Sitio Web Oficial:** [https://arrojorock.es](https://arrojorock.es) (visible en la burbuja de chat flotante, abajo a la derecha).
  - **Canal de Telegram:** [ArrojoBot (Dev)](https://t.me/ArrojoBot_dev_bot)

-----

## ⚙️ 3. Requisitos previos

Para que este workflow funcione, necesitarás:

  - Una instancia de **n8n** (local o en la nube).
  - Un bot de **Telegram** con su API Token.
  - Una base de datos vectorial **Qdrant** (local o en la nube).
  - Una base de datos **Redis** para la memoria del chat.
  - Una cuenta de **Google Drive** con una carpeta que contenga los documentos de la base de conocimiento.
  - Credenciales de API para:
      - **OpenAI** (para Embeddings y Chat Model).
      - **Mistral Cloud** (para Chat Model).
      - **Google Gemini (PaLM)** (para Chat Model).
      - **Spotify API** (para la herramienta de búsqueda de canciones).
      - **Facebook Graph API** (para la herramienta de búsqueda en la página).
      - **YouTube API** (para la herramienta de búsqueda de vídeos).

-----

## 📦 4. Archivos incluidos

  - `Arrojo.json`: El export completo del workflow de n8n.
  - `README.md`: Este documento explicativo.

-----

## 🚀 5. Instalación e Importación del Workflow

1.  Descarga el archivo `Arrojo.json`.
2.  En tu instancia de n8n, ve a **Import \> From File**.
3.  Selecciona el archivo `Arrojo.json` y guarda el workflow.
4.  **Importante:** Este flujo utiliza 10 tipos de credenciales distintas (ver sección de Requisitos). Deberás crear y asignar cada una de ellas en los nodos correspondientes (ej: `Telegram Trigger`, `Qdrant Vector Store`, `Redis Chat Memory`, `OpenAI Chat Model`, etc.).
5.  Revisa los nodos `buscar archivos` (Google Drive) y `youtube` (Tool) para establecer los IDs de la carpeta y el canal correctos.
6.  Activa el workflow. Los *triggers* se registrarán automáticamente.

-----

## 🧩 6. Estructura del Workflow

Este workflow se divide en dos lógicas principales:

### 1. Lógica de Chatbot (Recepción y Respuesta)

Es la rama principal que se activa con un mensaje.

1.  **Triggers (Telegram / Chat)**: El flujo se activa por dos vías: un *Telegram Trigger* para el bot (`https://t.me/ArrojoBot_dev_bot`) y un *Chat Trigger* (webhook) para la burbuja de chat de la web (`https://arrojorock.es`).
2.  **Gestión de Memoria**: Carga el historial de chat previo desde **Redis** (`Leer Historial`).
3.  **Agente Planificador ("Cafeina")**: Este es un paso crucial que sustituye al nodo `Think` estándar de n8n. Su propósito principal es solucionar el **"Lazy Agent Problem"**.

    > **¿Qué es el "Lazy Agent Problem"?**
    > Es una tendencia observada en los agentes LLM (como ArrojoBot) a volverse "perezosos" y responder usando solo su memoria de chat o conocimiento general, **ignorando las herramientas** que tienen disponibles (como la base de datos de Qdrant, Spotify, etc.). Esto provoca que el bot dé respuestas desactualizadas o alucines, aunque tuviera la herramienta correcta para obtener el dato.

    El agente "Cafeina" (usando Mistral/Gemini) actúa como un **planificador forzado**. Analiza la pregunta y el historial, y su *única* salida es un "plan" (un JSON) que dicta qué herramientas *debe* usar el agente principal (ej: `Base_de_Conocimiento_Arrojo`, `Spotify`, o `None`).

4.  **Agente Ejecutor ("ArrojoBot")**: Es el agente principal. Recibe el "plan" del planificador y utiliza *únicamente* las herramientas que "Cafeina" le ha ordenado usar para recopilar la información.
5.  **Generación de Respuesta**: El agente "ArrojoBot" (usando Gemini/OpenAI) genera la respuesta final, adhiriéndose a una personalidad y directrices muy estrictas definidas en su *system prompt*.
6.  **Formateo y Envío**: Un nodo de Python (`De MD a HTML`) convierte la respuesta de Markdown a HTML compatible con Telegram, y se envía de vuelta al usuario. El `IF` diferencia si la respuesta va a Telegram o al webhook de la web.

### 2\. Lógica de Indexación (Alimentación de RAG)

Es una rama secundaria que se activa manualmente para (re)construir la base de conocimiento.

1.  **Trigger (Manual)**: Se ejecuta manualmente para actualizar la base de conocimiento.
2.  **Google Drive**: Busca (`buscar archivos`) y descarga (`descargar archivos`) los documentos de conocimiento (ej: `.txt`, `.md`) de una carpeta específica.
3.  **Procesamiento**: Extrae el texto (`Extract from File`), lo divide en *chunks* (`Recursive Character Text Splitter`).
4.  **Embeddings**: Usa **OpenAI** para crear los vectores de texto.
5.  **Qdrant (Vector Store)**: Almacena los vectores en la colección `arrojo`, que es la base de conocimiento RAG del bot.
6.  (Opcional) Incluye nodos HTTP (`Borrar colección`) para limpiar la base de datos antes de reindexar.

-----

## ⚙️ 7. Variables y Credenciales

Asegúrate de configurar las siguientes credenciales en tu instancia de n8n:

  - `telegramApi`: Para el bot de Telegram.
  - `qdrantApi`: Para la base de datos vectorial Qdrant.
  - `redis`: Para la memoria del chat en Redis.
  - `googleDriveOAuth2Api`: Para leer documentos de Google Drive.
  - `openAiApi`: Para embeddings y el modelo de chat.
  - `mistralCloudApi`: Para el modelo de chat del planificador.
  - `googlePalmApi`: (Renombrado a Google Gemini) Para el modelo de chat.
  - `spotifyOAuth2Api`: Para la herramienta de Spotify.
  - `facebookGraphApi`: Para la herramienta de Facebook.
  - `youTubeOAuth2Api`: Para la herramienta de YouTube.

-----

## 🧾 8. Ejemplo de Ejecución

**Entrada (Webhook de Telegram):**
El JSON de `pinData` muestra un ejemplo de entrada del usuario.

```json
{
  "message": {
    "chat": {
      "id": 161313642,
      "type": "private"
    },
    "text": "¿Cuál es el enlace al vídeo de la pizza?"
  }
}
```

**Lógica interna:**

1.  **Agente "Cafeina" (Planificador)**: Recibe el texto. Decide que la intención es buscar un vídeo. Devuelve un plan: `{"tools": ["YouTube"]}`.
2.  **Agente "ArrojoBot" (Ejecutor)**: Recibe el plan. Activa la herramienta `youtube` con el término de búsqueda "vídeo de la pizza".
3.  La herramienta de YouTube devuelve un enlace (ej: `https://www.youtube.com/watch?v=XXXXXXX`).
4.  "ArrojoBot" formula una respuesta en personaje, en Markdown.

**Salida esperada (Respuesta en Telegram):**

El nodo `De MD a HTML` convierte el Markdown del bot a HTML, que se envía a Telegram:

```html
¡Claro! 🤘 Aquí tienes el vídeo de la pizza, ¡qué momentazo!

<a href='https://www.youtube.com/watch?v=XXXXXXX'>Arrojo - El vídeo de la pizza</a>

¡No olvides seguirnos en <a href='https://www.youtube.com/channel/UCJnAZC6v6OfKxNydcD6CFqQ'>YouTube</a> para más!
```

-----

## 🔧 9. Personalización

  - **Cambiar la Persona:** El núcleo del bot reside en los *system prompts* de los nodos **"Cafeina"** (planificador) y **"ArrojoBot"** (ejecutor). Puedes editar estos prompts para cambiar radicalmente la personalidad, el tono y las directrices del bot.
  - **Cambiar Base de Conocimiento**: Modifica el ID de la carpeta en el nodo de Google Drive **"buscar archivos"** para apuntar a tus propios documentos.
  - **Cambiar LLM**: El flujo está conectado a **OpenAI**, **Mistral** y **Gemini**. Puedes cambiar las conexiones en los nodos de Agente para priorizar el modelo que prefieras.
  - **Adaptar a otro Bot**: Reemplazando las herramientas (Spotify, FB, YouTube) y la base de conocimiento, este *framework* de Agente Planificador + Ejecutor puede adaptarse para cualquier tipo de chatbot de servicio al cliente.

-----

## 🧑‍💻 10. Autor

Desarrollado por [Enrique Aranda](https://www.linkedin.com/in/earanda/)
(Workflows públicos de `funkykespain`).

-----

## 📄 11. Licencia

Este proyecto se distribuye bajo la licencia MIT.

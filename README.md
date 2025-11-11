<p align="center"\>
<img src="https" alt="n8n Logo" width="150"/\>
<h1\>Workflows Públicos de n8n\</h1\>
</p\>

¡Bienvenido\! Este repositorio es una colección de flujos de trabajo (workflows) para la plataforma de automatización [n8n](https://n8n.io/), desarrollados por [Enrique Aranda](https://www.linkedin.com/in/earanda/).

El objetivo de este proyecto es compartir soluciones prácticas y ejemplos avanzados, con un fuerte enfoque en:

  * **Agentes de IA y LLMs**: Creación de chatbots y asistentes inteligentes.
  * **Arquitecturas Multi-Agente**: Orquestación de múltiples IAs para tareas complejas.
  * **RAG (Retrieval-Augmented Generation)**: Conexión de LLMs con bases de conocimiento vectorial (Qdrant).
  * **Integraciones Avanzadas**: Conexión con WhatsApp, Telegram, Google, Spotify, Azure y más.
  * **"Meta-Automatización"**: Workflows que gestionan otros workflows.

Cada subcarpeta contiene un workflow (`.json`), su `README.md` detallado y los assets necesarios.

## 🤖 Ecosistema de Asistente Personal (KykeBot)

Este conjunto de workflows gira en torno a **KykeBot**, un asistente personal avanzado, y los micro-servicios que le dan soporte para gestionar resúmenes y calendarios.

| Proyecto | Descripción | Esquema del Flujo |
| :--- | :--- | :--- |
| \<img src="KykeBot/profile.png?raw=true" width="100"\><br>[**KykeBot**](https://www.google.com/search?q=KykeBot/README.md) | **Asistente "Mayordomo Digital" para WhatsApp.** Actúa como un filtro inteligente en el primer punto de contacto, gestiona citas y proporciona información profesional usando RAG. | \<img src="KykeBot/schema.png?raw=true" width="300"\> |
| \<img src="Resumen-Conversacion/profile.png?raw=true" width="100"\><br>[**Resumen-Conversacion**](https://www.google.com/search?q=Resumen-Conversacion/README.md) | **Agente de Resúmenes para KykeBot.** Proceso de backend que monitoriza las bases de datos de KykeBot y envía un informe diario por email con los resúmenes de las nuevas conversaciones. | \<img src="Resumen-Conversacion/schema.jpg?raw=true" width="300"\> |
| \<img src="MCP-Calendar/profile.png?raw=true" width="100"\><br>[**MCP-Calendar**](https://www.google.com/search?q=MCP-Calendar/README.md) | **Servidor de Herramientas de Calendario.** Un micro-servicio (Tool Server) construido con MCP de n8n que expone 6 herramientas de Google Calendar para que KykeBot pueda crear, leer y modificar eventos. | \<img src="MCP-Calendar/schema.png?raw=true" width="300"\> |

## 🧠 Chatbots y Agentes de IA

Workflows diseñados como agentes conversacionales para diferentes propósitos, desde servicio al cliente hasta experimentación con modelos locales.

| Proyecto | Descripción | Esquema del Flujo |
| :--- | :--- | :--- |
| \<img src="Arrojo/profile.png?raw=true" width="100"\><br>[**ArrojoBot**](https://www.google.com/search?q=Arrojo/README.md) | **Chatbot RAG para una Banda de Rock.** Asistente para Telegram y web de la banda "Arrojo". Usa RAG (Qdrant) y herramientas en tiempo real (Spotify, YouTube, Facebook) para responder a los fans. | \<img src="Arrojo/schema.png?raw=true" width="300"\> |
| \<img src="Lyra/profile.png?raw=true" width="100"\><br>[**Lyra (Prompt Optimizer)**](https://www.google.com/search?q=Lyra/README.md) | **Agente de IA Experta en *Prompt Engineering*.** Un chatbot que analiza y optimiza prompts de usuario usando RAG y una metodología de 4-D (Deconstruir, Diagnosticar, Desarrollar, Entregar). | \<img src="Lyra/schema.png?raw=true" width="300"\> |
| \<img src="Insolente-Artificial/profile.png?raw=true" width="100"\><br>[**Insolente Artificial**](https://www.google.com/search?q=Insolente-Artificial/README.md) | **Experimento de LLM Local (Ollama).** Un chatbot de Telegram con personalidad sarcástica, diseñado para probar el rendimiento y las limitaciones de modelos locales (Ollama) en un VPS. | \<img src="Insolente-Artificial/schema.png?raw=true" width="300"\> |

## 🎙️ Automatización de Contenidos

Flujos de trabajo centrados en la curación, generación y distribución de contenido de forma automatizada.

| Proyecto | Descripción | Esquema del Flujo |
| :--- | :--- | :--- |
| \<img src="Noticias/profile.png?raw=true" width="100"\><br>[**Boletín de Audio IA**](https://www.google.com/search?q=Noticias/README.md) | **Generador de Boletín de Noticias en Audio.** Un sistema que escanea +10 fuentes de noticias tech, las procesa con una orquesta de 3 agentes de IA (Analista, Summarizer, Guionista) y distribuye un resumen de audio diario por WhatsApp. | \<img src="Noticias/schema.png?raw=true" width="300"\> |

## ⚙️ Utilidades y Meta-Workflows

Workflows diseñados para automatizar tareas de desarrollo y mantenimiento, incluyendo la gestión de este propio repositorio.

| Proyecto | Descripción | Esquema del Flujo |
| :--- | :--- | :--- |
| \<img src="Backup-GitHub/profile.png?raw=true" width="100"\><br>[**Backup-GitHub**](https://www.google.com/search?q=Backup-GitHub/README.md) | **Sincronización de n8n a GitHub.** Un workflow de "meta-automatización" que se ejecuta semanalmente, lee una lista de workflows de la API de n8n y los "pushea" a este repositorio de GitHub. | \<img src="Backup-GitHub/schema.png?raw=true" width="300"\> |

-----

## 🧑‍💻 Autor

Desarrollado por [**Enrique Aranda**](https://www.linkedin.com/in/earanda/)
(Workflows públicos de `funkykespain`).

## 📄 Licencia

Este proyecto se distribuye bajo la licencia MIT.

<p align="center">
  <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/banner.png?raw=true" alt="n8n Workflows Banner" width="90%"/>
  <h1>Workflows Públicos de n8n</h1>
</p>

¡Bienvenido! Este repositorio es una colección de flujos de trabajo (workflows) para la plataforma de automatización [n8n](https://n8n.io/), desarrollados por [Enrique Aranda](https://www.linkedin.com/in/earanda/).

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
| <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/KykeBot/profile.png?raw=true" width="100"><br/>[**KykeBot**](KykeBot/README.md) | **Asistente "Mayordomo Digital" para WhatsApp.** Actúa como un filtro inteligente en el primer punto de contacto, gestiona citas y proporciona información profesional usando RAG. | <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/KykeBot/schema.png?raw=true" width="300"> |
| <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Resumen-Conversacion/profile.png?raw=true" width="100"><br/>[**Resumen-Conversacion**](Resumen-Conversacion/README.md) | **Agente de Resúmenes para KykeBot.** Proceso de backend que monitoriza las bases de datos de KykeBot y envía un informe diario por email con los resúmenes de las nuevas conversaciones. | <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Resumen-Conversacion/schema.png?raw=true" width="300"> |
| <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/MCP-Calendar/profile.png?raw=true" width="100"><br/>[**MCP-Calendar**](MCP-Calendar/README.md) | **Servidor de Herramientas de Calendario.** Un micro-servicio (Tool Server) construido con MCP de n8n que expone 6 herramientas de Google Calendar para que KykeBot pueda crear, leer y modificar eventos. | <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/MCP-Calendar/schema.png?raw=true" width="300"> |

## 🧠 Chatbots y Agentes de IA

Workflows diseñados como agentes conversacionales para diferentes propósitos, desde servicio al cliente hasta experimentación con modelos locales.

| Proyecto | Descripción | Esquema del Flujo |
| :--- | :--- | :--- |
| <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Arrojo/profile.png?raw=true" width="100"><br/>[**ArrojoBot**](Arrojo/README.md) | **Chatbot RAG para una Banda de Rock.** Asistente para Telegram y web de la banda "Arrojo". Usa RAG (Qdrant) y herramientas en tiempo real (Spotify, YouTube, Facebook) para responder a los fans. | <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Arrojo/schema.png?raw=true" width="300"> |
| <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Lyra/profile.png?raw=true" width="100"><br/>[**Lyra (Prompt Optimizer)**](Lyra/README.md) | **Agente de IA Experta en *Prompt Engineering*.** Un chatbot que analiza y optimiza prompts de usuario usando RAG y una metodología de 4-D (Deconstruir, Diagnosticar, Desarrollar, Entregar). | <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Lyra/schema.png?raw=true" width="300"> |
| <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Insolente-Artificial/profile.png?raw=true" width="100"><br/>[**Insolente Artificial**](Insolente-Artificial/README.md) | **Experimento de LLM Local (Ollama).** Un chatbot de Telegram con personalidad sarcástica, diseñado para probar el rendimiento y las limitaciones de modelos locales (Ollama) en un VPS. | <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Insolente-Artificial/schema.png?raw=true" width="300"> |

## 🎙️ Automatización de Contenidos

Flujos de trabajo centrados en la curación, generación y distribución de contenido de forma automatizada.

| Proyecto | Descripción | Esquema del Flujo |
| :--- | :--- | :--- |
| <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Noticias/profile.png?raw=true" width="100"><br/>[**Boletín de Audio IA**](Noticias/README.md) | **Generador de Boletín de Noticias en Audio.** Un sistema que escanea +10 fuentes de noticias tech, las procesa con una orquesta de 3 agentes de IA (Analista, Summarizer, Guionista) y distribuirá un resumen de audio diario por WhatsApp. | <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Noticias/schema.png?raw=true" width="300"> |

## ⚙️ Utilidades y Meta-Workflows

Workflows diseñados para automatizar tareas de desarrollo y mantenimiento, incluyendo la gestión de este propio repositorio.

| Proyecto | Descripción | Esquema del Flujo |
| :--- | :--- | :--- |
| <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Backup-GitHub/profile.png?raw=true" width="100"><br/>[**Backup-GitHub**](Backup-GitHub/README.md) | **Sincronización de n8n a GitHub.** Un workflow de "meta-automatización" que se ejecuta semanalmente, lee una lista de workflows de la API de n8n y los "pushea" a este repositorio de GitHub. | <img src="https://github.com/funkykespain/workflows-n8n-publicos/blob/main/Backup-GitHub/schema.png?raw=true" width="300"> |

---

## ⚠️ Nota del Autor

Los *workflows* de este repositorio son una selección de proyectos personales y ejemplos educativos compartidos con la comunidad.

Existen numerosos flujos de trabajo adicionales, mucho más complejos y orientados a soluciones empresariales, que fueron desarrollados para clientes específicos. Debido a su naturaleza y a acuerdos de confidencialidad, dichos *workflows* no se divulgan públicamente.

## 🧑‍💻 Autor

Desarrollado por [**Enrique Aranda**](https://www.linkedin.com/in/earanda/)
(Workflows públicos de `funkykespain`).

## 📄 Licencia

Este proyecto se distribuye bajo la licencia MIT.

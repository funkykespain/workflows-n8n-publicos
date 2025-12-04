# Ingeniería de Prompts Avanzada y Arquitecturas Agénticas para la Redacción Científica: Un Paradigma de 2025

## Resumen Ejecutivo

La redacción científica asistida por Inteligencia Artificial ha experimentado una metamorfosis radical entre 2023 y 2025, transitando de una disciplina centrada en la "ingeniería de prompts" estática a un ecosistema complejo de **orquestación agéntica**, **arquitecturas cognitivas** y **flujos de trabajo automatizados**. El documento original objeto de análisis, que refleja un enfoque tradicional basado en instrucciones directas al modelo de lenguaje (LLM), posee un margen de mejora sustancial si se integran las metodologías actuales. El presente informe exhaustivo analiza cómo la implementación de técnicas de razonamiento avanzado -tales como _Chain of Draft_ (CoD), _Skeleton of Thought_ (SoT) y el patrón _Reflexion_-, combinadas con la infraestructura de automatización de _n8n_ y la especialización de modelos (OpenAI o1 frente a Claude 3.5 Sonnet), redefine la calidad, precisión y eficiencia de la producción académica. A lo largo de este análisis, se demuestra que la clave para la excelencia en 2025 no reside en pedirle a la IA que "escriba", sino en diseñar sistemas que "piensen, planifiquen, critiquen y verifiquen" antes de generar una sola línea de prosa científica.

## 1\. La Evolución del Paradigma: Del Prompt Estático a la Arquitectura Cognitiva

### 1.1 Limitaciones Intrínsecas de la Ingeniería de Prompts Tradicional

El enfoque reflejado en el documento de referencia (repositorio de GitHub sobre _Prompt Engineering_ para artículos científicos) representa el estado del arte de circa 2023. Esta metodología se basaba fundamentalmente en el diseño de "super-prompts": instrucciones extensas y detalladas que intentaban encapsular contexto, restricciones de estilo, formato y lógica en una única ventana de contexto. La premisa subyacente era que, con la instrucción adecuada, un modelo como GPT-4 podía generar un apartado científico finalizado en una sola inferencia.<sup>1</sup>

Sin embargo, la investigación actual y la práctica empírica han revelado que este enfoque monolítico adolece de **sobrecarga cognitiva**. Cuando se fuerza a un LLM a realizar recuperación de memoria, planificación estructural, redacción sintáctica y verificación factual simultáneamente, la calidad del razonamiento se degrada. Los modelos de lenguaje, por su naturaleza probabilística, tienden a priorizar la fluidez lingüística sobre la coherencia lógica cuando se satura su atención.<sup>3</sup> En el contexto de la escritura científica, esto se manifiesta en alucinaciones sutiles (referencias inexistentes pero plausibles), argumentos circulares y una estructura narrativa superficial.

### 1.2 El Surgimiento de los Sistemas Agénticos y Compuestos (2025)

La respuesta de la comunidad científica y tecnológica en 2025 ha sido la transición hacia **Sistemas de IA Compuestos** y flujos de trabajo agénticos. A diferencia de un prompt estático, un "agente" es una entidad de software que posee autonomía para ejecutar tareas, utilizar herramientas externas (como búsquedas en bases de datos académicas o ejecución de código Python) y mantener un estado persistente a lo largo de múltiples interacciones.<sup>5</sup>

En este nuevo paradigma, la redacción de un artículo científico no se aborda como una tarea de generación de texto, sino como un **proceso de orquestación**. Herramientas de automatización visual como **n8n** permiten descomponer la tarea titánica de "escribir un paper" en subprocesos discretos y especializados: agentes de investigación que recopilan evidencia <sup>7</sup>, agentes de síntesis que estructuran la lógica <sup>8</sup>, y agentes de redacción que convierten esa lógica en prosa académica. La superioridad de este enfoque radica en la **especialización funcional**: al asignar a cada instancia del modelo una tarea cognitiva única y acotada, se reduce drásticamente la tasa de error y se incrementa la profundidad del análisis.<sup>9</sup>

## 2\. Estrategias de Razonamiento Avanzado: Más Allá del Texto Generativo

Para elevar la calidad del documento original, es imperativo incorporar técnicas que fuercen al modelo a "pensar" antes de "hablar". Las secciones críticas de un artículo científico, como la Discusión y la Metodología, requieren una integridad lógica que los prompts estándar no pueden garantizar. A continuación, se detallan las arquitecturas de razonamiento que definen el estado del arte en 2025.

### 2.1 Chain of Thought (CoT): La Base del Razonamiento Secuencial

El _Chain of Thought_ (CoT) o Cadena de Pensamiento, introducido originalmente por Wei et al., marcó el primer gran salto cualitativo al demostrar que los LLMs podían resolver problemas complejos si se les instruía para "pensar paso a paso".<sup>10</sup> En lugar de mapear directamente una pregunta a una respuesta, CoT induce al modelo a generar una secuencia de pasos intermedios de razonamiento.

En el ámbito científico, CoT es fundamental para evitar saltos lógicos injustificados. Por ejemplo, al analizar los resultados de un experimento, un prompt estándar podría saltar directamente a una conclusión generalista. Un prompt CoT, por el contrario, obligaría al modelo a desglosar los datos estadísticos, considerar las variables de confusión y derivar la conclusión solo después de haber articulado la evidencia intermedia. No obstante, CoT presenta limitaciones significativas en 2025: su **verbosidad**. Los modelos tienden a generar explicaciones extensas y redundantes que consumen valiosos tokens de la ventana de contexto y aumentan la latencia, lo que a menudo diluye la densidad informativa necesaria en la escritura técnica de alto nivel.<sup>12</sup>

### 2.2 Tree of Thoughts (ToT): Exploración Multiversal de Hipótesis

La técnica _Tree of Thoughts_ (ToT) representa una evolución no lineal del razonamiento. Mientras que CoT sigue una línea única de pensamiento, ToT permite al modelo explorar múltiples ramas de razonamiento simultáneamente, creando un árbol de posibilidades.<sup>14</sup>

Mecanismo y Aplicación Científica:

ToT opera mediante un ciclo de generación, evaluación y poda. El modelo propone múltiples "pensamientos" (por ejemplo, tres interpretaciones diferentes de un mismo fenómeno observado), evalúa la viabilidad de cada una mediante autocrítica o criterios predefinidos, y descarta las ramas menos prometedoras antes de continuar.16 Para la sección de Discusión de un artículo científico, ToT es invaluable. Permite simular el pensamiento crítico de un investigador humano que pondera explicaciones alternativas. Un flujo de trabajo ToT podría instruir al agente para: "Generar tres hipótesis que expliquen la correlación observada. Evaluar la fortaleza de la evidencia para cada una. Seleccionar la hipótesis más robusta y redactar la argumentación basándose en ella". Esto introduce un nivel de rigor y matiz que elimina el sesgo de confirmación común en las generaciones de un solo paso.17

### 2.3 Skeleton of Thought (SoT): Optimización Estructural y Latencia

El _Skeleton of Thought_ (SoT) aborda un problema crítico en la generación de textos largos: la pérdida de coherencia estructural. Los modelos de lenguaje generan texto de manera secuencial (token a token), lo que a menudo resulta en documentos que divagan o pierden el hilo argumental hacia el final.<sup>8</sup>

La Metodología SoT:

SoT desacopla la planificación de la redacción. El proceso se divide en dos fases distintas:

- **Fase de Esqueleto:** Se solicita al modelo que genere _únicamente_ el esquema o esqueleto del documento, detallando los puntos clave de cada sección con extrema brevedad.<sup>19</sup>
- **Fase de Expansión Paralela:** Utilizando una arquitectura como n8n, cada punto del esqueleto se envía a una instancia separada del modelo para ser redactado en paralelo.

Esta técnica no solo reduce drásticamente la latencia (al procesar secciones simultáneamente), sino que garantiza una **coherencia global** superior. Al tener el esqueleto fijo antes de escribir, el modelo no puede desviarse de la estructura lógica predefinida. Para artículos de revisión (Review Papers) o introducciones extensas, SoT asegura que la narrativa fluya lógicamente desde el contexto general hasta la brecha de investigación específica, sin las digresiones habituales de la generación secuencial.<sup>20</sup>

### 2.4 Chain of Draft (CoD): La Revolución Minimalista de 2025

La innovación más reciente y disruptiva identificada en la literatura de 2025 es el **Chain of Draft (CoD)**.<sup>12</sup> Propuesta como una respuesta a la ineficiencia del CoT, CoD se inspira en cómo los expertos humanos realizan borradores mentales rápidos o anotaciones taquigráficas antes de formalizar una idea.

Mecanismo y Superioridad Técnica:

A diferencia del CoT, que exige explicaciones prolijas ("Primero, calculamos la media..."), CoD instruye al modelo para generar pasos de razonamiento minimalistas y densos en información, limitando a menudo cada paso a unas pocas palabras (e.g., "Max 5 palabras por paso").22

- _Ejemplo CoT:_ "Para determinar la significancia, debemos mirar el valor p. Dado que p < 0.05, podemos rechazar la hipótesis nula."
- _Ejemplo CoD:_ "p < 0.05 → Rechazar H0."

Esta condensación tiene implicaciones profundas para la escritura científica técnica, especialmente en la sección de **Metodología** o en la descripción de algoritmos. CoD fuerza al modelo a centrarse puramente en la lógica operativa, eliminando la retórica vacía. Los estudios demuestran que CoD mantiene o supera la precisión de CoT utilizando solo una fracción de los tokens (reducción de hasta el 90% en uso de tokens y latencia).<sup>25</sup> Esto permite realizar razonamientos mucho más largos y complejos dentro de la misma ventana de contexto, ideal para derivaciones matemáticas o lógicas complejas en papers teóricos.

## 3\. El Patrón Reflexion: Autocorrección y Perfeccionamiento Iterativo

El documento original probablemente asume que el output de la IA es el producto final. En 2025, el estándar de oro es el **Patrón Reflexion**, que trata el primer output de la IA meramente como un "borrador sucio" que debe ser sometido a crítica y revisión rigurosa.<sup>27</sup>

### 3.1 La Dinámica Actor-Evaluador

El patrón Reflexion institucionaliza el ciclo de revisión por pares dentro del propio sistema de generación de IA. Se implementa típicamente mediante dos roles distintos <sup>28</sup>:

- **El Actor (Redactor):** Genera el texto inicial basándose en los datos y el prompt.
- **El Evaluador (Crítico):** Analiza el texto generado no para continuarlo, sino para encontrar errores. Este agente recibe instrucciones específicas de calidad (e.g., "Identifica afirmaciones sin cita", "Detecta inconsistencias en la terminología", "Señala falacias lógicas").

### 3.2 El Bucle de Refuerzo Verbal

La innovación clave de Reflexion es que la crítica se convierte en **memoria a corto plazo** para la siguiente iteración. El Evaluador genera un "feedback verbal" (e.g., "El párrafo 3 es redundante y la conclusión no se sigue de los resultados"). El Actor recibe entonces su propio borrador original más este feedback y se le instruye para "Reescribir el texto abordando estas críticas".<sup>29</sup>

Este proceso iterativo, automatizable fácilmente en n8n mediante bucles lógicos, ha demostrado elevar el rendimiento en tareas de razonamiento y redacción compleja de un ~60% a más del 90%.<sup>28</sup> En la redacción científica, esto es crucial para pulir el **Abstract** (asegurando que contenga todos los elementos obligatorios) y afinar la precisión del lenguaje en los **Resultados**, eliminando ambigüedades antes de que el investigador humano intervenga.

## 4\. Estrategia de Selección de Modelos: La Bifurcación Cognitiva

Una actualización crítica para cualquier guía de 2025 es el abandono de la idea de "un modelo para todo". El ecosistema de LLMs se ha especializado, dividiéndose en **Modelos de Razonamiento** y **Modelos de Articulación**.<sup>31</sup>

### 4.1 OpenAI o1 y o3: Los Motores de Lógica

Los modelos de la serie **o1** (y sus sucesores o3) de OpenAI están diseñados con un paradigma de "razonamiento oculto" o entrenamiento por refuerzo a gran escala. Antes de emitir un solo token de respuesta, el modelo ejecuta una cadena de pensamiento interna, invisible para el usuario, donde planifica y verifica su respuesta.<sup>31</sup>

- **Rol en la Escritura Científica:** Estos modelos son insuperables para la **planificación estructural** (SoT), el **análisis de datos**, y la **crítica lógica** (rol de Evaluador en Reflexion). Son capaces de detectar errores sutiles en la interpretación de datos que modelos más rápidos pasarían por alto.<sup>33</sup>
- **Contraindicaciones:** Son lentos (latencia 30x mayor) y costosos. Su prosa tiende a ser rígida, esquemática y menos fluida, lo que los hace menos ideales para la redacción final del texto narrativo.<sup>34</sup>

### 4.2 Claude 3.5 Sonnet: El Virtuoso de la Prosa

Por otro lado, **Claude 3.5 Sonnet** de Anthropic se ha consolidado como el modelo de referencia para la generación de texto y código matizado. Su ventana de contexto masiva (200k tokens) y su "personalidad" menos robótica lo hacen superior para captar el tono académico y mantener la coherencia estilística.<sup>32</sup>

- **Rol en la Escritura Científica:** Claude 3.5 Sonnet debe ser el **Actor/Redactor**. Es el modelo que debe tomar el esqueleto lógico generado por o1 y expandirlo en prosa fluida. Su capacidad para seguir instrucciones de estilo complejas lo hace ideal para adaptar el texto a las guías de autores de revistas específicas.

### 4.3 Flujos de Trabajo Híbridos (Best-of-Breed)

La recomendación para actualizar el documento original es prescribir **Flujos Híbridos**:

- **Fase de Análisis (o1):** Ingesta de notas crudas y datos -> Generación de _Chain of Draft_ y Esqueleto detallado.
- **Fase de Redacción (Sonnet):** Ingesta del Esqueleto -> Redacción de borradores por sección.
- **Fase de Crítica (o1):** Revisión de los borradores en busca de fallos lógicos.
- **Fase de Edición Final (Sonnet):** Incorporación del feedback y pulido estilístico.

Esta orquestación aprovecha lo mejor de ambos mundos: la profundidad analítica de OpenAI y la elocuencia de Anthropic.<sup>33</sup>

## 5\. Orquestación y Automatización: La Infraestructura n8n

El salto más significativo respecto al documento original es la implementación técnica. Ya no se trata de copiar y pegar prompts en ChatGPT, sino de construir **pipelines de investigación** en herramientas como n8n.

### 5.1 Arquitectura del Agente de "Deep Research"

Los flujos de trabajo de "Investigación Profunda" automatizan la revisión de literatura, una de las tareas más tediosas. Un flujo típico en n8n para 2025 se estructura de la siguiente manera <sup>7</sup>:

**Tabla 1: Arquitectura de Nodos para un Agente de Investigación en n8n**

| **Componente (Nodo)** | **Función Técnica** | **Herramienta Sugerida** | **Propósito Científico** |
| --- | --- | --- | --- |
| **Trigger (Webhook/Form)** | Entrada del usuario | n8n Form | Recibir el tema de investigación y parámetros (e.g., años, tipo de estudio). |
| --- | --- | --- | --- |
| **Planificador (Planner)** | Descomposición de tareas | OpenAI o1 / GPT-4o | Romper la pregunta de investigación en sub-consultas de búsqueda específicas. |
| --- | --- | --- | --- |
| **Iterador (Loop)** | Ejecución recursiva | n8n Loop | Procesar cada sub-consulta de manera secuencial o paralela. |
| --- | --- | --- | --- |
| **Buscador (Search)** | Recuperación de fuentes | Tavily API / SerpAPI | Buscar papers relevantes en la web (no solo palabras clave, sino contexto semántico). |
| --- | --- | --- | --- |
| **Extractor (Scraper)** | Lectura profunda | Apify / Firecrawl | Acceder a las URL, extraer el texto completo del paper (o HTML) y limpiar el ruido. |
| --- | --- | --- | --- |
| **Analista (Context)** | Síntesis parcial | Claude 3.5 Sonnet | Leer el contenido extraído, filtrar irrelevancias y resumir hallazgos clave con citas. |
| --- | --- | --- | --- |
| **Agregador** | Fusión de conocimientos | n8n Merge | Combinar todos los resúmenes parciales en un cuerpo de conocimiento unificado. |
| --- | --- | --- | --- |
| **Redactor Final** | Generación del reporte | Claude 3.5 Sonnet | Redactar la revisión de literatura final basada _exclusivamente_ en los datos agregados. |
| --- | --- | --- | --- |

### 5.2 Implementación Práctica y Ventajas

Esta arquitectura permite una **investigación recursiva**. Si el Agente Planificador detecta que la información recuperada en la primera ronda es insuficiente o contradictoria, puede generar dinámicamente nuevas consultas de búsqueda para llenar los vacíos, un comportamiento imposible con un prompt estático.<sup>37</sup> Además, el uso de herramientas como **Apify** permite extraer contenido real de la web en tiempo real, superando la fecha de corte de conocimiento de los modelos pre-entrenados.<sup>36</sup>

## 6\. Integridad Científica: RAG, Grafos y Mitigación de Alucinaciones

La mayor preocupación en la escritura científica con IA es la **alucinación**: la invención de datos o citas. En 2025, la mitigación de alucinaciones ha pasado de ser un arte (prompts cuidadosos) a una ingeniería (sistemas de verificación).

### 6.1 RAG (Retrieval-Augmented Generation) y Long Context

El RAG conecta al LLM con una base de conocimiento externa confiable (e.g., una biblioteca de Zotero o una carpeta de PDFs).

- **Long RAG:** Con la llegada de ventanas de contexto de 1M+ tokens (Gemini 1.5 Pro), el RAG tradicional basado en "chunking" (fragmentar textos en pedazos pequeños) está siendo reemplazado por **Long RAG**. Esto implica alimentar al modelo con papers enteros o capítulos completos. Esto preserva el contexto global y la estructura argumentativa, permitiendo al modelo entender no solo un dato aislado, sino la metodología completa que llevó a ese dato.<sup>39</sup>

### 6.2 GraphRAG: Conectando Conceptos

Para revisiones de literatura complejas, el **GraphRAG** representa la vanguardia. En lugar de recuperar texto basado en similitud vectorial (palabras parecidas), GraphRAG construye un grafo de conocimiento donde los nodos son conceptos/autores y las aristas son relaciones. Esto permite responder preguntas complejas como "¿Qué autores contradicen la teoría X de Smith?" navegando por la red de citas, algo que el RAG vectorial simple a menudo falla en hacer.<sup>40</sup>

### 6.3 Ingeniería de Prompts Anti-Alucinación

Incluso dentro de un sistema RAG, los prompts deben blindarse contra la invención. Las técnicas más efectivas documentadas en 2025 incluyen <sup>41</sup>:

- **Instrucciones de Incertidumbre Explícita:** "Si la información no está presente en los documentos proporcionados, declara explícitamente 'No se encuentra información'. No intentes inferir o inventar." (Reducción del 52% en alucinaciones).
- **Verificación de Citas (Quote-to-Claim):** Obligar al modelo a extraer la cita exacta del texto fuente antes de hacer cualquier afirmación. "Para cada afirmación, proporciona el fragmento textual exacto del paper que la respalda."
- **Chain of Verification (CoVe):** Un proceso donde el modelo genera una respuesta, luego genera preguntas para verificar sus propios hechos, responde esas preguntas independientemente y finalmente corrige la respuesta original.

## 7\. Casos de Uso Específicos: Aplicando Técnicas SOTA a Secciones del Paper

Para maximizar la utilidad del documento original, se recomienda desglosar la aplicación de estas técnicas por sección del artículo científico.

**Tabla 2: Matriz de Aplicación de Técnicas por Sección**

| **Sección del Paper** | **Desafío Principal** | **Técnica SOTA Recomendada** | **Modelo Preferente** | **Mecanismo de Acción** |
| --- | --- | --- | --- | --- |
| **Título y Abstract** | Condensación y gancho | **Reflexion** | Claude 3.5 Sonnet | Generar múltiples variantes, criticar la claridad e impacto, iterar hasta la versión óptima. |
| --- | --- | --- | --- | --- |
| **Introducción** | Contexto y brecha | **Deep Research / RAG** | Híbrido (o1 + Sonnet) | Usar agentes de búsqueda para mapear el estado del arte actual y localizar la brecha de conocimiento real. |
| --- | --- | --- | --- | --- |
| **Metodología** | Precisión lógica | **Chain of Draft (CoD)** | OpenAI o1 | Usar CoD para describir procedimientos paso a paso con densidad lógica máxima, evitando ambigüedades. |
| --- | --- | --- | --- | --- |
| **Resultados** | Interpretación de datos | **Data Analysis Agents** | OpenAI o1 (Code Interpreter) | Subir datasets crudos; usar el modelo para ejecutar análisis Python y describir hallazgos estadísticos sin sesgo. |
| --- | --- | --- | --- | --- |
| **Discusión** | Argumentación compleja | **Tree of Thoughts (ToT)** | OpenAI o1 | Generar múltiples interpretaciones de los resultados, evaluar contra la literatura (RAG) y seleccionar la narrativa más robusta. |
| --- | --- | --- | --- | --- |

### 7.1 Ejemplo de Aplicación: Metodología con Chain of Draft

Para escribir una sección de metodología rigurosa, un prompt de _Chain of Draft_ sería superior a uno estándar.

- **Prompt CoD:** "Describe el protocolo de análisis estadístico. Piensa paso a paso, pero mantén cada paso como un borrador mínimo de máximo 5 palabras enfocado en la lógica operativa. Separador: ####. Luego redacta el párrafo completo."
- **Salida Esperada (Draft):**
  - _Normalidad -> Test Shapiro-Wilk._
  - _Homocedasticidad -> Test Levene._
  - _Comparación -> ANOVA un factor._
  - _Post-hoc -> Corrección Tukey._
  - _Software -> R v4.1.2._
  - _Redacción Final:_ "La normalidad de la distribución de los datos se evaluó mediante la prueba de Shapiro-Wilk, y la homogeneidad de varianzas mediante la prueba de Levene. Las comparaciones entre grupos se realizaron utilizando un ANOVA de un factor, seguido de pruebas post-hoc de Tukey para comparaciones múltiples. Todos los análisis se ejecutaron en el entorno estadístico R (v4.1.2)."

Este enfoque garantiza que no se omita ningún paso lógico crítico, algo frecuente cuando el modelo intenta escribir prosa florida directamente.<sup>24</sup>

## 8\. Hoja de Ruta para la Actualización del Documento

Para transformar el documento de GitHub referenciado en un recurso de vanguardia para 2025, se sugiere la siguiente estructura de actualización, integrando los hallazgos de este reporte.

### 8.1 Fase 1: Reingeniería de la Base (Conceptos)

- **Sustituir** la introducción sobre "cómo pedirle cosas a la IA" por "cómo diseñar flujos de trabajo con IA".
- **Añadir** explicaciones técnicas sobre _Chain of Draft_ y _Skeleton of Thought_ como herramientas esenciales para la escritura técnica, contrastándolas con el _Chain of Thought_ clásico.

### 8.2 Fase 2: Implementación Técnica (Herramientas)

- **Incluir** plantillas (blueprints) de **n8n** en lugar de solo prompts de texto. Proporcionar el JSON de un flujo básico de "Investigador Académico" que conecte Tavily con un modelo de lenguaje.<sup>36</sup>
- **Diferenciar** explícitamente entre el uso de modelos o1 (para pensar/estructurar) y modelos Claude/GPT-4o (para escribir), aconsejando al usuario cuándo cambiar de uno a otro.

### 8.3 Fase 3: Control de Calidad (Verificación)

- **Integrar** una sección obligatoria sobre "Mitigación de Alucinaciones", enseñando al usuario a usar prompts de verificación de citas y herramientas como Scite.ai dentro de sus flujos.
- **Promover** el uso del patrón _Reflexion_. En lugar de proporcionar un prompt para "Escribir la Discusión", proporcionar un par de prompts: uno para escribirla y otro para criticarla.<sup>29</sup>

## Conclusión

El documento original sobre ingeniería de prompts para artículos científicos, aunque válido en sus fundamentos, ha quedado obsoleto ante la velocidad de innovación de 2025. La mera "ingeniería de prompts" ha dado paso a la **ingeniería de sistemas cognitivos**. La incorporación de arquitecturas de razonamiento avanzadas (**Chain of Draft**, **Skeleton of Thought**), la adopción de flujos de trabajo agénticos (**n8n**, **Deep Research**) y la estrategia de modelos híbridos (**o1 + Sonnet**) no son mejoras incrementales, sino transformadoras.

Estas técnicas permiten pasar de una IA que actúa como un "asistente de escritura" pasivo a una que funciona como un "colaborador de investigación" activo, capaz de navegar la literatura, razonar sobre metodologías y autocorriger sus propios borradores. La actualización del documento con estas metodologías dotará a los investigadores de herramientas infinitamente más potentes para enfrentar los desafíos de la producción científica moderna, asegurando rigor, eficiencia y profundidad en sus publicaciones.

#### Obras citadas

- Prompt engineering - OpenAI API, fecha de acceso: diciembre 4, 2025, <https://platform.openai.com/docs/guides/prompt-engineering>
- The Complete Guide to Prompt Engineering in 2025: Master the Art of AI Communication, fecha de acceso: diciembre 4, 2025, <https://dev.to/fonyuygita/the-complete-guide-to-prompt-engineering-in-2025-master-the-art-of-ai-communication-4n30>
- The Ultimate Guide to Prompt Engineering in 2025 | Lakera - Protecting AI teams that disrupt the world., fecha de acceso: diciembre 4, 2025, <https://www.lakera.ai/blog/prompt-engineering-guide>
- Survey and analysis of hallucinations in large language models: attribution to prompting strategies or model behavior - Frontiers, fecha de acceso: diciembre 4, 2025, <https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2025.1622292/full>
- Prompt Secrets: AI Agents and Code | DS Stream Generative AI, fecha de acceso: diciembre 4, 2025, <https://www.dsstream.com/post/prompt-secrets-ai-agents-and-code>
- Multi-Agent Orchestration with n8n in 2025: From Concept to Practical AI Systems - Medium, fecha de acceso: diciembre 4, 2025, <https://medium.com/@angelosorte1/multi-agent-orchestration-with-n8n-in-2025-from-concept-to-practical-ai-systems-8fc6996468b2>
- Deep Research Agent - Automated Research & Notion Report Builder | n8n workflow template, fecha de acceso: diciembre 4, 2025, <https://n8n.io/workflows/7160-deep-research-agent-automated-research-and-notion-report-builder/>
- Accelerating LLMs with Skeleton-of-Thought Prompting - Portkey, fecha de acceso: diciembre 4, 2025, <https://portkey.ai/blog/skeleton-of-thought-prompting/>
- Build Custom AI Agents With Logic & Control | n8n Automation Platform, fecha de acceso: diciembre 4, 2025, <https://n8n.io/ai-agents/>
- What is chain of thought (CoT) prompting? - IBM, fecha de acceso: diciembre 4, 2025, <https://www.ibm.com/think/topics/chain-of-thoughts>
- Chain-of-Thought Prompting, fecha de acceso: diciembre 4, 2025, <https://learnprompting.org/docs/intermediate/chain_of_thought>
- Chain of Draft: Thinking Faster by Writing Less - arXiv, fecha de acceso: diciembre 4, 2025, <https://arxiv.org/html/2502.18600v1>
- Chain of Draft Prompting (COD): The Next Step in Efficient LLM Reasoning - WeCloudData, fecha de acceso: diciembre 4, 2025, <https://weclouddata.com/blog/chain-of-draft-prompting-cod-next-step-in-llm-reasoning/>
- Tree of Thoughts (ToT) - Prompt Engineering Guide, fecha de acceso: diciembre 4, 2025, <https://www.promptingguide.ai/techniques/tot>
- What is Tree Of Thoughts Prompting? - IBM, fecha de acceso: diciembre 4, 2025, <https://www.ibm.com/think/topics/tree-of-thoughts>
- Beginner's Guide To Tree Of Thoughts Prompting (With Examples) | Zero To Mastery, fecha de acceso: diciembre 4, 2025, <https://zerotomastery.io/blog/tree-of-thought-prompting/>
- Understanding and Implementing the Tree of Thoughts Paradigm - Hugging Face, fecha de acceso: diciembre 4, 2025, <https://huggingface.co/blog/sadhaklal/tree-of-thoughts>
- Reducing Latency with Skeleton of Thought Prompting - PromptHub, fecha de acceso: diciembre 4, 2025, <https://www.prompthub.us/blog/reducing-latency-with-skeleton-of-thought-prompting>
- Skeleton-of-Thought: Prompting LLMs for Efficient Parallel Generation - arXiv, fecha de acceso: diciembre 4, 2025, <https://arxiv.org/html/2307.15337v3>
- Skeleton-of-Thought Prompting: Faster and Efficient Response Generation, fecha de acceso: diciembre 4, 2025, <https://learnprompting.org/docs/advanced/decomposition/skeleton_of_thoughts>
- Skeleton of Thought: LLMs Can Do Parallel Decoding Paper Reading - Arize AI, fecha de acceso: diciembre 4, 2025, <https://arize.com/blog/skeleton-of-thought-llms-can-do-parallel-decoding-paper-reading/>
- How to Use Chain-of-Draft Prompting for Better LLM Responses? - ProjectPro, fecha de acceso: diciembre 4, 2025, <https://www.projectpro.io/article/chain-of-draft-prompting/1120>
- Chain of Draft: Concise Prompting Reduces LLM Costs by 90% - Ajith Vallath Prabhakar, fecha de acceso: diciembre 4, 2025, <https://ajithp.com/2025/03/02/chain-of-draft-llm-prompting/>
- Chain of Draft (CoD) - Learn Prompting, fecha de acceso: diciembre 4, 2025, <https://learnprompting.org/docs/advanced/thought_generation/chain-of-draft>
- Chain-of-Draft Prompting: A More Efficient Alternative to Chain of Thought - Helicone, fecha de acceso: diciembre 4, 2025, <https://www.helicone.ai/blog/chain-of-draft>
- Chain of Draft Prompting with Gemini and Groq - Analytics Vidhya, fecha de acceso: diciembre 4, 2025, <https://www.analyticsvidhya.com/blog/2025/03/chain-of-draft/>
- What is Agentic AI Reflection Pattern? - Analytics Vidhya, fecha de acceso: diciembre 4, 2025, <https://www.analyticsvidhya.com/blog/2024/10/agentic-ai-reflection-pattern/>
- Reflexion | Prompt Engineering Guide, fecha de acceso: diciembre 4, 2025, <https://www.promptingguide.ai/techniques/reflexion>
- Agentic Design Patterns Part 2: Reflection - DeepLearning.AI, fecha de acceso: diciembre 4, 2025, <https://www.deeplearning.ai/the-batch/agentic-design-patterns-part-2-reflection/>
- Building a Self-Correcting AI: A Deep Dive into the Reflexion Agent with LangChain and LangGraph | by Vi Q. Ha | Medium, fecha de acceso: diciembre 4, 2025, <https://medium.com/@vi.ha.engr/building-a-self-correcting-ai-a-deep-dive-into-the-reflexion-agent-with-langchain-and-langgraph-ae2b1ddb8c3b>
- Analysis: OpenAI o1 vs GPT-4o vs Claude 3.5 Sonnet - Vellum AI, fecha de acceso: diciembre 4, 2025, <https://www.vellum.ai/blog/analysis-openai-o1-vs-gpt-4o>
- Model Analysis: OpenAI o1 vs Claude 3.5 - PromptLayer Blog, fecha de acceso: diciembre 4, 2025, <https://blog.promptlayer.com/model-analysis-openai-o1-vs-claude-3-5/>
- OpenAI o1 vs Claude 3.5 Sonnet: Which One's Really Worth Your \$20? - Composio, fecha de acceso: diciembre 4, 2025, <https://composio.dev/blog/openai-o1-vs-claude-3-5-sonnet>
- Claude 3.5 Sonnet vs OpenAI o1: A Comprehensive Comparison - Helicone, fecha de acceso: diciembre 4, 2025, <https://www.helicone.ai/blog/claude-3.5-sonnet-vs-openai-o1>
- Sonnet 3.5 beats o1 in OpenAI's new \$1M coding benchmark : r/ClaudeAI - Reddit, fecha de acceso: diciembre 4, 2025, <https://www.reddit.com/r/ClaudeAI/comments/1isncwf/sonnet_35_beats_o1_in_openais_new_1m_coding/>
- Host Your Own AI Deep Research Agent with n8n, Apify and OpenAI o3, fecha de acceso: diciembre 4, 2025, <https://n8n.io/workflows/2878-host-your-own-ai-deep-research-agent-with-n8n-apify-and-openai-o3/>
- Build Your Own DeepResearch with N8N + Apify + Notion!, fecha de acceso: diciembre 4, 2025, <https://community.n8n.io/t/build-your-own-deepresearch-with-n8n-apify-notion/77766>
- Automate Research Paper Collection with Bright Data & n8n | n8n workflow template, fecha de acceso: diciembre 4, 2025, <https://n8n.io/workflows/5221-automate-research-paper-collection-with-bright-data-and-n8n/>
- The 2025 Guide to Retrieval-Augmented Generation (RAG) - Eden AI, fecha de acceso: diciembre 4, 2025, <https://www.edenai.co/post/the-2025-guide-to-retrieval-augmented-generation-rag>
- Advancing engineering research through context-aware and knowledge graph-based retrieval-augmented generation - Frontiers, fecha de acceso: diciembre 4, 2025, <https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2025.1697169/full>
- How to Stop AI from Making Up Facts - 12 Tested Techniques That Prevent ChatGPT and Claude Hallucinations (2025 Guide) : r/PromptEngineering - Reddit, fecha de acceso: diciembre 4, 2025, <https://www.reddit.com/r/PromptEngineering/comments/1o77fk0/how_to_stop_ai_from_making_up_facts_12_tested/>
- Writing Prompts That Don't Hallucinate in 2025 | by Kareim Tarek | Data Science Collective, fecha de acceso: diciembre 4, 2025, <https://medium.com/data-science-collective/writing-prompts-that-dont-hallucinate-in-2025-f3a5d2cfb1d0>
- Chain of Draft: How to Make Your LLM Reasoning More Efficient | by prateek sikdar, fecha de acceso: diciembre 4, 2025, <https://medium.com/@prateeksikdar/chain-of-draft-how-to-make-your-llm-reasoning-more-efficient-6349f8f23401>

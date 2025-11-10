# **Una Revisión Sistemática de la Ingeniería de Prompts: De los Principios Fundamentales a la Optimización Avanzada**

## **Parte I: Los Fundamentos de la Interacción con Modelos**

Esta primera parte establece los conceptos fundamentales de la ingeniería de prompts, definiendo la unidad básica de interacción —el prompt— y detallando los paradigmas centrales que gobiernan cómo los usuarios pueden guiar el comportamiento del modelo sin modificar sus parámetros.

### **Capítulo 1: La Anatomía de un Prompt: Deconstruyendo la Interfaz hacia los LLMs**

Este capítulo irá más allá de la noción simplista de un prompt como una mera pregunta. Formalizará el prompt como una entrada estructurada diseñada para dirigir el comportamiento del modelo, desglosándolo en sus componentes funcionales y constitutivos.

#### **1.1. Definiendo el Prompt**

En el nexo de la interacción humano-computadora con la inteligencia artificial generativa (GenAI), el concepto de "prompt" ha surgido como el paradigma principal. Un prompt no es simplemente una pregunta o una entrada de texto; es un conjunto de instrucciones específicas para una tarea, diseñadas para obtener comportamientos y resultados deseados de un modelo de lenguaje grande (LLM) aprovechando su conocimiento pre-entrenado, todo ello sin necesidad de modificar los parámetros centrales del modelo. Esta práctica, conocida como ingeniería de prompts, se ha convertido en una técnica indispensable para ampliar las capacidades de los LLMs y los modelos de visión-lenguaje (VLMs), permitiendo la integración fluida de modelos pre-entrenados en tareas posteriores basándose únicamente en la guía proporcionada en el prompt. Es el proceso de estructurar las entradas para maximizar la utilidad y la precisión de estos modelos, convirtiéndose en el mecanismo principal a través del cual los desarrolladores y usuarios finales interactúan con los sistemas de GenAI.

#### **1.2. Componentes Centrales de un Prompt Estructurado**

La transición de la ingeniería de prompts de un arte empírico a una disciplina de ingeniería repetible se evidencia en la identificación y formalización de sus componentes clave. Lo que antes era un proceso intuitivo de ensayo y error ahora puede ser deconstruido en un conjunto de elementos funcionales que, cuando se combinan de manera efectiva, guían al modelo hacia el resultado deseado. El análisis sistemático ha revelado varios componentes centrales que constituyen un prompt bien formado.

* **Rol/Persona:** Asignar un rol específico al modelo (por ejemplo, "Eres un analista financiero experto" o "Actúa como un clasificador experimentado de tickets de soporte técnico") es una táctica poderosa. Esta instrucción inicial enfoca el razonamiento, el tono y el estilo del modelo, ayudándolo a "pensar" como un especialista en el dominio requerido.  
  * **Ejemplo práctico:**  
    `Actúa como un chef profesional. Por favor, proporciona una receta sencilla para un plato de pasta vegetariano.`  
    Este prompt guía al modelo para que responda con la jerga y el formato esperados de un experto culinario.  
* **Directiva/Tarea:** Este es el núcleo del prompt, una instrucción clara e inequívoca que especifica la acción deseada. El uso de verbos de acción fuertes (por ejemplo, "Escribe una lista con viñetas", "Resume el informe adjunto", "Clasifica los tickets de soporte entrantes") elimina la ambigüedad y establece un objetivo concreto para el modelo.  
  * **Ejemplo práctico:**  
    `Resume el siguiente párrafo en una sola frase: [Párrafo sobre el cambio climático].`  
    La directiva "Resume... en una sola frase" es explícita y define claramente la tarea.  
* **Contexto e Información de Fondo:** Proporcionar hechos, datos o documentos fuente relevantes es crucial para anclar la respuesta del modelo en la realidad y reducir su dependencia del conocimiento interno, que puede ser estático u obsoleto. Incluir información como "Dado que las temperaturas globales han aumentado 1 grado Celsius desde la era preindustrial..." o "Basado en el informe financiero adjunto..." proporciona al modelo el terreno fáctico necesario para generar respuestas precisas y relevantes.  
  * **Ejemplo práctico:**  
    `Contexto: Nuestra empresa gestiona el soporte al cliente para varias herramientas SaaS. Los tickets de soporte a menudo involucran solución de problemas técnicos, consultas de facturación o solicitudes de funciones.`  
    `Tarea: Clasifica el siguiente ticket.`  
    `Ticket: "Me cobraron dos veces por mi suscripción este mes."`  
    El contexto ayuda al modelo a entender el entorno operativo y a realizar una clasificación más precisa.  
* **Ejemplos (Ejemplares):** Proporcionar uno o más pares de entrada-salida que demuestren el formato y la lógica de la tarea deseada es la base del Aprendizaje en Contexto (In-Context Learning, ICL). Estos ejemplares guían al modelo de manera mucho más efectiva que las instrucciones por sí solas, especialmente para tareas complejas.  
  * **Ejemplo práctico:**  
    `Ticket: "Necesito ayuda para restablecer mi contraseña; el enlace no funciona." -> Categoría: "Problema Técnico"`  
    `Ticket: "Me cobraron dos veces por mi suscripción este mes." -> Categoría: "Consulta de Facturación"`  
    Estos ejemplos muestran al modelo el formato de salida exacto esperado.  
* **Formato de Salida e Instrucciones de Estilo:** Definir explícitamente la estructura deseada de la salida (por ejemplo, JSON, tabla Markdown, ensayo de 500 palabras), la longitud y el tono es fundamental para obtener resultados utilizables. Instrucciones como "Organiza la salida en un formato JSON con cada categoría como clave" o "Compón un ensayo de 500 palabras" guían al modelo no solo en *qué* decir, sino en *cómo* decirlo.  
  * **Ejemplo práctico:**  
    `Enumera las tres causas principales del cambio climático, cada una en una viñeta separada.`  
    Este prompt especifica tanto el número de elementos (tres) como el formato (viñetas) para la respuesta.  
* **Restricciones e Instrucciones Negativas:** Especificar lo que el modelo *no* debe hacer puede ser tan importante como especificar lo que debe hacer. Incluir restricciones como "Evita incluir información personal en las respuestas" o "Solo emite la categoría del ticket" ayuda a prevenir resultados no deseados y a refinar aún más el comportamiento del modelo.  
  * **Ejemplo práctico:**  
    `Tarea: Clasifica el siguiente ticket de soporte.`  
    `Restricción: Solo emite la categoría del ticket. No añadas ninguna explicación.`  
    `Ticket: "Mi aplicación se bloquea constantemente."`  
    La restricción asegura que la salida sea concisa y se ajuste a los requisitos del sistema.

#### **1.3. La Evolución de Consulta a Programa**

La conceptualización del prompt ha experimentado una evolución significativa. Las interacciones iniciales con los LLMs se asemejaban a simples consultas en un motor de búsqueda, donde el usuario planteaba una pregunta y esperaba una respuesta directa. Sin embargo, la visión moderna considera el prompting como una forma de programación o aprendizaje por instrucción (*instruction learning*). Este cambio de paradigma no es meramente semántico; refleja una comprensión más profunda de la interacción con el modelo. En lugar de simplemente "preguntar", los usuarios están "instruyendo" o "programando" al modelo a través del lenguaje natural para que ejecute una tarea.  
Esta maduración del concepto se manifiesta en el desarrollo de lenguajes de consulta específicos para prompts, como el Lenguaje de Consulta para Modelos de Lenguaje (LMQL, por sus siglas en inglés). LMQL generaliza el prompting de texto puro a una combinación intuitiva de instrucciones de texto y scripts, permitiendo incluso la especificación de restricciones sobre la salida del modelo de lenguaje. Este enfoque trata al prompt no como una cadena de texto estática, sino como un programa que puede incluir control de flujo y restricciones, generando un procedimiento de inferencia eficiente que minimiza las costosas llamadas al LLM subyacente.  
Esta progresión desde consultas no estructuradas hacia prompts estructurados y, finalmente, a lenguajes de consulta formales, es un indicador clásico del desarrollo de principios de ingeniería en un campo: un movimiento desde la artesanía a medida hacia metodologías estandarizadas y fiables. Es probable que las futuras herramientas de interacción con LLMs se alejen de las simples cajas de chat para adoptar interfaces más estructuradas que guíen implícitamente a los usuarios a proporcionar estos componentes clave, enseñando de manera efectiva los principios de la ingeniería de prompts.

### **Capítulo 2: Paradigmas de Interacción Centrales: Prompting de Cero y Pocos Disparos (Zero-Shot y Few-Shot)**

Este capítulo ofrece un examen detallado de las dos estrategias de prompting más fundamentales, que constituyen la base para muchas de las técnicas más avanzadas. Estas estrategias definen la cantidad de información ejemplar que se proporciona al modelo dentro del propio prompt.

#### **2.1. Prompting de Cero Disparos (Zero-Shot): Aprovechando el Conocimiento Pre-entrenado**

* **Definición y Mecanismo:** El prompting de cero disparos (zero-shot) es la forma más básica y directa de interacción. Consiste en instruir a un LLM para que realice una tarea sin proporcionarle ningún ejemplo previo de entrada-salida. El modelo debe basarse únicamente en su vasto conocimiento pre-entrenado y en su capacidad para generalizar a partir de la instrucción misma. Por ejemplo, un prompt como Clasifica el texto en neutral, negativo o positivo. Texto: Creo que las vacaciones estuvieron bien. es un prompt de cero disparos, ya que el modelo debe comprender el concepto de "sentimiento" sin haber visto ejemplos de clasificación en el prompt. Esta capacidad se ve significativamente mejorada por el "ajuste de instrucciones" (*instruction tuning*), un proceso de afinado de modelos en conjuntos de datos descritos mediante instrucciones, y por el Aprendizaje por Refuerzo a partir de la Retroalimentación Humana (RLHF), que alinea aún más el modelo con las preferencias humanas.  
  * **Ejemplo práctico:**  
    `Analiza el sentimiento de la siguiente declaración: '¡La película fue fantástica y la vería de nuevo!'`  
    El modelo, sin ejemplos previos, utiliza su conocimiento general para responder "Positivo".  
* **Aplicaciones y Fortalezas:** Este paradigma es ideal para tareas de propósito general, consultas rápidas y situaciones en las que la creación de ejemplos es inviable o innecesaria. Es una estrategia flexible, eficiente en tiempo y altamente accesible para usuarios no técnicos, ya que elimina la necesidad de un ajuste fino específico para cada tarea. Su poder reside en la capacidad del modelo para aplicar el conocimiento previo a nuevos problemas, de manera similar al aprendizaje humano.  
* **Limitaciones:** A pesar de su simplicidad y poder, el rendimiento del prompting de cero disparos puede ser poco fiable para tareas complejas o con matices. Cuando la instrucción por sí sola es insuficiente para especificar completamente el formato de salida deseado o el proceso de razonamiento requerido, el modelo puede generar resultados no deseados o incorrectos. Cuando el prompting de cero disparos falla, la recomendación estándar es proporcionar demostraciones o ejemplos en el prompt, lo que nos lleva al paradigma de pocos disparos.

#### **2.2. Prompting de Pocos Disparos (Few-Shot): Guiando con Aprendizaje en Contexto (ICL)**

* **Definición y Mecanismo:** El prompting de pocos disparos (few-shot) mejora el paradigma de cero disparos al proporcionar al modelo un pequeño número de ejemplos (típicamente entre 2 y 10 "disparos" o "shots") directamente dentro del prompt. Estos ejemplos, también conocidos como ejemplares, sirven como demostraciones en contexto, permitiendo al modelo inferir el patrón subyacente y aplicarlo a una nueva entrada no vista. Esta técnica es una aplicación directa del Aprendizaje en Contexto (In-Context Learning, ICL), donde el modelo aprende de ejemplos incrustados en el prompt en lugar de requerir entrenamiento adicional.  
  * **Ejemplo práctico (Clasificación de Sentimiento):**  
    `Clasifica las siguientes frases como 'Positivo' o 'Negativo':`  
    `- '¡Me encanta esta película!' -> Positivo.`  
    `- 'Esta fue la peor experiencia de mi vida.' -> Negativo.`

    `Clasifica la siguiente frase: 'Tuve un día maravilloso en la playa.'`  
    Al ver los ejemplos, el modelo aprende el formato y la lógica, y responde correctamente "Positivo".  
* **Aplicaciones y Fortalezas:** Esta técnica mejora significativamente el rendimiento en tareas complejas en comparación con el prompting de cero disparos, ya que clarifica la estructura de salida esperada, el estilo, el tono y la lógica. Es particularmente efectivo para tareas como el análisis de sentimientos, la extracción de información, la generación de contenido creativo, la traducción automática y la generación de código.  
* **Matices Clave y Mejores Prácticas:** La efectividad del prompting de pocos disparos depende de varios factores sutiles. La calidad, la diversidad y el formato de los ejemplos son cruciales. Un hallazgo sorprendente y profundo de la investigación es que la *corrección* de las etiquetas en los ejemplos es menos importante que el *formato* de los ejemplos y la *distribución* de las etiquetas. Los estudios demuestran que proporcionar ejemplos con etiquetas aleatorias puede superar al prompting de cero disparos, lo que sugiere que el modelo está aprendiendo un patrón estructural en lugar de simplemente el contenido de la tarea. Esto indica que la presencia de una estructura como Entrada: \[texto\] // Etiqueta: \[categoría\], independientemente de la corrección de la etiqueta, le indica al modelo que la tarea es de "clasificación". Además, el orden de los ejemplos también puede influir en el resultado final.  
* **Limitaciones:** La principal desventaja del prompting de pocos disparos es el coste. Consume más tokens, lo que aumenta los costes computacionales y puede alcanzar el límite de la ventana de contexto del modelo, especialmente con entradas y salidas largas. Además, la elaboración de ejemplos efectivos puede ser un proceso laborioso que requiere un esfuerzo considerable.

La notable eficacia del prompting de pocos disparos, incluso con etiquetas incorrectas, revela una verdad fundamental sobre cómo funcionan estos modelos. No se trata simplemente de "enseñar" al modelo un hecho o una regla, como se podría enseñar a un humano. Más bien, el prompt actúa como una poderosa señal de recuperación que activa un "modo" de procesamiento específico o un vector de tarea aprendido dentro del espacio de alta dimensión del modelo. Los ejemplos ayudan al modelo a reducir la ambigüedad y a seleccionar cuál de sus muchas habilidades pre-entrenadas debe aplicar. Esta comprensión tiene profundas implicaciones: el futuro de la ingeniería de prompts puede centrarse menos en la creación de un *contenido* de ejemplo perfecto y más en el descubrimiento de las *plantillas estructurales* óptimas que activan de la manera más efectiva los comportamientos deseados del modelo. Este principio también subyace a los "prompts suaves" (*soft prompts*), que son esencialmente activadores estructurales aprendidos en forma de vectores continuos.

#### **2.3. Prompting de Un Disparo (One-Shot)**

Entre los dos paradigmas principales se encuentra el prompting de un disparo (one-shot), que proporciona un único ejemplo al modelo. Esta técnica sirve como un punto intermedio, a menudo suficiente para aclarar las expectativas en tareas de complejidad moderada sin incurrir en el coste de tokens de un enfoque de pocos disparos completo. Ayuda a aclarar las expectativas y a mejorar el rendimiento del modelo en comparación con el enfoque de cero disparos.

* **Ejemplo práctico:**  
  `Un "whatpu" es un pequeño animal peludo nativo de Tanzania. Un ejemplo de una frase que usa la palabra whatpu es:`  
  `Estábamos viajando por África y vimos estos whatpus tan monos.`

  `"Farduddle" significa saltar arriba y abajo muy rápido. Un ejemplo de una frase que usa la palabra farduddle es:`  
  El modelo, al ver un solo ejemplo, aprende el patrón y completa la frase: "Cuando ganamos el partido, todos empezamos a fardudlear de celebración".

## **Parte II: Elicitando y Estructurando el Razonamiento Complejo**

Esta parte transita desde las interacciones básicas hacia las técnicas avanzadas que han permitido a los LLMs abordar problemas que requieren un pensamiento de varios pasos, lógico y estratégico.

### **Capítulo 3: La Revolución de la Cadena de Pensamiento (Chain-of-Thought, CoT)**

Este capítulo proporcionará una inmersión profunda en el prompting de Cadena de Pensamiento (Chain-of-Thought, CoT), la técnica seminal que desbloqueó el razonamiento complejo en los LLMs.

#### **3.1. El Principio Central de CoT**

* **Definición:** La Cadena de Pensamiento (CoT) es una técnica de prompting que guía a un LLM para que descomponga un problema complejo en una serie de pasos de razonamiento intermedios y secuenciales antes de llegar a una respuesta final. En lugar de solicitar una respuesta directa, el CoT alienta al modelo a articular su proceso de pensamiento, a "pensar en voz alta".  
* **Por qué Funciona:** El CoT es efectivo porque obliga al modelo a asignar más computación al problema, descomponiéndolo en pasos más pequeños y manejables que puede resolver de manera más fiable. Este enfoque imita un proceso de pensamiento humano más deliberado. La externalización del razonamiento no solo mejora la precisión, sino que también hace que el proceso del modelo sea más transparente, interpretable y depurable. Esta capacidad no está presente en modelos más pequeños; se considera una habilidad emergente que aparece cuando los modelos alcanzan una escala masiva (generalmente alrededor de 100 mil millones de parámetros o más), ya que han aprendido patrones de razonamiento más matizados a partir de sus vastos datos de entrenamiento.

#### **3.2. Variantes e Implementaciones de CoT**

La versatilidad del principio de CoT ha llevado al desarrollo de varias implementaciones, cada una adaptada a diferentes necesidades y limitaciones de recursos.

* **CoT de Pocos Disparos (Few-Shot CoT):** Esta fue la implementación original de la técnica. En este enfoque, el prompt incluye algunos ejemplos de preguntas emparejadas no solo con sus respuestas finales, sino con cadenas de razonamiento detalladas y paso a paso que muestran cómo se llegó a esa respuesta. Estos ejemplos enseñan al modelo el formato de salida deseado.  
  * **Ejemplo práctico:**  
    `P: Los números impares en este grupo suman un número par: 4, 8, 9, 15, 12, 2, 1.`  
    `R: Los números impares son 9, 15, 1. Su suma es 25. 25 es un número impar. La respuesta es Falso.`

    `P: Los números impares en este grupo suman un número par: 15, 32, 5, 13, 82, 7, 1.`  
    `R:`  
    El modelo sigue el patrón de razonamiento y responde: "Los números impares son 15, 5, 13, 7, 1\. Su suma es 41\. 41 es un número impar. La respuesta es Falso".  
* **CoT de Cero Disparos (Zero-Shot CoT):** Una variante más simple pero sorprendentemente poderosa que no requiere la creación manual de ejemplos. En su lugar, se añade una simple frase como "Pensemos paso a paso" o "Explica tu razonamiento" al final de la pregunta. Esta simple instrucción es a menudo suficiente para activar las capacidades de razonamiento secuencial del modelo y hacer que genere su propia cadena de pensamiento.  
  * **Ejemplo práctico:**  
    `P: Fui al mercado y compré 10 manzanas. Le di 2 manzanas al vecino y 2 a la reparadora. Luego fui y compré 5 manzanas más y me comí 1. ¿Cuántas manzanas me quedan?`  
    `R: Pensemos paso a paso.`  
    El modelo generará los pasos: 1\. Empiezas con 10 manzanas. 2\. Das 2+2=4 manzanas. Te quedan 10-4=6. 3\. Compras 5 más, así que 6+5=11. 4\. Te comes 1, así que 11-1=10. La respuesta es 10\.  
* **CoT Automático (Auto-CoT):** Para superar la laboriosa tarea de crear manualmente ejemplos de CoT de pocos disparos, se desarrolló el Auto-CoT. Este método automatiza la creación de prompts de demostración. Funciona agrupando preguntas de un conjunto de datos en clústeres de similitud y luego utilizando el CoT de cero disparos para generar cadenas de razonamiento para un ejemplo representativo de cada clúster. Esto minimiza los errores humanos y mantiene la diversidad en los ejemplos de demostración, eliminando la necesidad de anotación manual.

#### **3.3. Mejora de CoT con Estrategias de Decodificación: Autoconsistencia (Self-Consistency)**

* **Mecanismo:** La autoconsistencia es una estrategia de decodificación que mejora significativamente la robustez de las respuestas de CoT. En lugar de tomar la primera y única cadena de razonamiento que el modelo genera (un enfoque de "decodificación codiciosa"), la autoconsistencia muestrea múltiples y diversas rutas de razonamiento desde el decodificador del modelo. Luego, agrega los resultados y selecciona la respuesta final más consistente a través de una votación mayoritaria.  
  * **Ejemplo práctico:** Para un problema matemático, el modelo podría generar tres rutas de razonamiento:  
    1. Ruta 1 \-\> Respuesta: 42  
    2. Ruta 2 \-\> Respuesta: 42  
    3. Ruta 3 (con un error de cálculo) \-\> Respuesta: 45 La autoconsistencia seleccionaría la respuesta "42" por ser la más frecuente.  
* **Impacto:** Esta técnica mejora drásticamente la precisión en tareas de razonamiento complejas (aritméticas, de sentido común y simbólicas). Al explorar múltiples formas de llegar a una solución, mitiga el riesgo de que una única ruta de razonamiento defectuosa conduzca a una respuesta incorrecta. Ha demostrado mejoras de precisión significativas, por ejemplo, un 17.9% en el benchmark GSM8K.

#### **3.4. Variantes Avanzadas y Especializadas de CoT**

La investigación ha continuado refinando el paradigma CoT para abordar debilidades específicas y mejorar aún más el rendimiento.

* **CoT Contrastivo (CCoT):** Este enfoque proporciona al modelo demostraciones tanto de razonamiento válido como inválido. Al mostrarle errores comunes junto con las soluciones correctas, el modelo aprende a evitar escollos comunes y a generar un razonamiento más robusto.  
* **CoT Lógico (LogiCoT):** Un marco neurosimbólico que aprovecha los principios de la lógica simbólica (como la *reductio ad absurdum*) para mejorar el razonamiento de una manera coherente y estructurada. Utiliza un bucle de pensar-verificar-revisar para reducir los errores lógicos y las alucinaciones.  
* **Cadena de Verificación (CoVe):** Esta técnica aborda directamente el problema de la alucinación. Implica un proceso sistemático de cuatro pasos: 1\) generar una respuesta de referencia, 2\) planificar preguntas de verificación para comprobar la respuesta, 3\) responder a esas preguntas de forma independiente para evitar sesgos, y 4\) producir una respuesta final revisada que incorpore los resultados de la verificación.

El éxito de CoT y sus variantes revela un principio fundamental para la interacción con los LLMs: para el razonamiento complejo, el *proceso* de llegar a una respuesta es tan importante, si no más, que la respuesta misma. Estas técnicas intercambian eficazmente un mayor coste computacional (generando respuestas más largas y detalladas) por una mayor precisión y robustez. El fracaso de un modelo en una tarea compleja a menudo se debe a que intenta resolverla en un único paso de inferencia. CoT transforma una tarea compleja en una secuencia de tareas más simples que el modelo *sí* puede realizar de manera fiable. Este principio de descomposición de tareas es el antecesor intelectual directo de técnicas más avanzadas como el Árbol de Pensamientos y el Grafo de Pensamientos, así como de los flujos de trabajo agénticos donde un LLM planifica y ejecuta una serie de subtareas.

### **Capítulo 4: Más Allá de la Linealidad: Explorando el Árbol y el Grafo de Pensamientos**

Este capítulo explora la evolución de las técnicas de razonamiento más allá de la simple secuencia lineal de CoT, abordando sus limitaciones inherentes y avanzando hacia estructuras de pensamiento más complejas y potentes.

#### **4.1. Las Limitaciones de las Cadenas Lineales**

A pesar de su poder transformador, la Cadena de Pensamiento (CoT) tiene una debilidad fundamental: su fragilidad. Dado que el razonamiento se genera como una secuencia lineal, un error en un paso temprano inevitablemente se propaga a través de toda la cadena, llevando a una conclusión final incorrecta. Este enfoque de "un solo camino" no permite la exploración de rutas de razonamiento alternativas, la corrección de errores intermedios o el retroceso una vez que se ha tomado un camino equivocado.

#### **4.2. Árbol de Pensamientos (Tree-of-Thoughts, ToT): Explorando Múltiples Rutas de Razonamiento**

* **Mecanismo:** El Árbol de Pensamientos (ToT) generaliza el CoT al estructurar el proceso de razonamiento como un árbol, en lugar de una cadena. En cada nodo del árbol (un paso en el razonamiento), el modelo puede generar múltiples "pensamientos" o continuaciones posibles, creando así diferentes ramas. Luego, el modelo puede utilizar la autoevaluación o algoritmos de búsqueda (como la búsqueda en anchura o en profundidad) para evaluar la viabilidad de estas rutas. Esto le permite "mirar hacia adelante" para anticipar el éxito de una rama y "retroceder" de las ramas que parecen poco prometedoras.  
  * **Ejemplo práctico (Juego del 24):** Dada la entrada "4 9 10 13", ToT exploraría múltiples caminos simultáneamente:  
    * Rama 1: (10 \- 4\) \* (13 \- 9\) \= 6 \* 4 \= 24\. ¡Solución encontrada\!  
    * Rama 2: 9 \* 4 \- 10 \= 26\. Callejón sin salida.  
    * Rama 3: 13 \+ 9 \+ 4 \- 10 \= 16\. Callejón sin salida. A diferencia de CoT, que podría atascarse en la Rama 2, ToT puede explorar la Rama 1 y encontrar la solución.  
* **Ventajas:** ToT mejora significativamente el rendimiento en tareas complejas que requieren exploración, planificación estratégica o donde existen múltiples rutas de solución válidas. Un ejemplo canónico es el "Juego del 24", donde ToT superó drásticamente a CoT al poder explorar sistemáticamente diferentes combinaciones de operaciones aritméticas.

#### **4.3. Grafo de Pensamientos (Graph-of-Thoughts, GoT): Razonamiento Dinámico y No Lineal**

* **Mecanismo:** El Grafo de Pensamientos (GoT) abstrae aún más el proceso de razonamiento, modelándolo como un grafo dirigido arbitrario. En esta estructura, los "pensamientos" son los vértices y sus dependencias son las aristas. Esto permite una flexibilidad mucho mayor que la de un árbol, ya que los pensamientos pueden combinarse, agregarse y refinarse de formas no lineales. Por ejemplo, un pensamiento de una rama de razonamiento puede fusionarse con un pensamiento de otra rama para generar una nueva idea que no habría sido posible en una estructura lineal o de árbol.  
  * **Ejemplo práctico (Planificación de un ensayo):** GoT podría generar una idea para la introducción (Nodo A) y una idea para el cuerpo del texto (Nodo B). Luego, podría generar una idea para la conclusión (Nodo C) que dependa de A y B. Si más tarde se genera una nueva idea (Nodo D) que refina la introducción, GoT puede fusionar D con C para crear una conclusión mejorada, algo que una estructura de árbol no podría hacer fácilmente.  
* **Ventajas:** GoT se alinea mejor con la naturaleza compleja e interconectada del pensamiento humano, donde las ideas no siempre siguen una progresión lineal o jerárquica. Admite la interacción dinámica y la síntesis de ideas de diferentes ramas de razonamiento, superando las restricciones de las estructuras anteriores.

#### **4.4. Marcos Orientados a Objetivos**

El desarrollo de ToT y GoT forma parte de un cambio más amplio hacia un "prompting orientado a objetivos", como se describe en la revisión de Li et al.. Este marco conceptualiza el proceso de resolución de problemas de la IA en etapas análogas al pensamiento lógico humano. Proporciona una taxonomía para entender estas técnicas avanzadas, organizándolas en fases como la Descomposición de Objetivos, la Selección de Acciones, la Ejecución de Acciones y la Evaluación. ToT y GoT son implementaciones sofisticadas de las etapas de evaluación y selección de sub-objetivos valiosos dentro de este marco.  
La progresión de CoT a ToT y a GoT es una recapitulación directa de la historia de los algoritmos de búsqueda en la inteligencia artificial clásica, ahora aplicada al nuevo dominio de los procesos de pensamiento generados por LLMs. CoT es análogo a una búsqueda simple de un solo camino, como una búsqueda codiciosa. Sus limitaciones (quedarse atascado en un mal camino) son bien conocidas en la IA clásica. La solución en la IA clásica fue desarrollar algoritmos que pudieran explorar múltiples caminos. ToT es el equivalente directo de introducir algoritmos de búsqueda en árbol (como BFS, DFS o búsqueda por haz) al proceso de razonamiento del LLM. GoT es análogo a algoritmos de búsqueda en grafo aún más avanzados (como A\*), donde los nodos (pensamientos) pueden interconectarse de maneras complejas.  
Esta poderosa analogía sugiere que el vasto cuerpo de conocimiento de la IA clásica sobre búsqueda, planificación y optimización puede adaptarse directamente para mejorar el razonamiento de los LLMs. Las futuras técnicas de ingeniería de prompts pueden incorporar explícitamente heurísticas de búsqueda más sofisticadas, algoritmos de planificación y métodos de optimización directamente en el propio marco de prompting.

## **Parte III: La Formalización de la Ingeniería de Prompts como Disciplina**

Esta parte examina el esfuerzo académico para transformar la ingeniería de prompts de una colección de técnicas ad-hoc a una disciplina formal y estructurada, con taxonomías establecidas y fundamentos matemáticos.

### **Capítulo 5: Marcos Sistemáticos y Taxonomías**

Este capítulo sintetizará las principales revisiones sistemáticas (surveys) para presentar una visión holística y estructurada del panorama de la ingeniería de prompts, destacando cómo diferentes investigadores han intentado organizar este campo en rápida evolución.

#### **5.1. La Necesidad de Estructura**

La rápida aparición de una multitud de técnicas de prompting ha llevado a una terminología fragmentada y a menudo conflictiva. Esta falta de un entendimiento ontológico compartido y un vocabulario común ha obstaculizado el progreso sistemático, creando la necesidad de una organización rigurosa. Las revisiones sistemáticas y las taxonomías son esfuerzos cruciales para abordar esta brecha, proporcionando marcos estructurados para comprender, comparar y desarrollar nuevas técnicas.

#### **5.2. Una Taxonomía Centrada en la Aplicación**

La revisión de Sahoo et al. ofrece una taxonomía completa y sistemática organizada por área de aplicación. Este es un marco eminentemente práctico, diseñado para ayudar a los desarrolladores a encontrar las técnicas más relevantes para resolver problemas específicos. Las categorías clave incluyen:

* **Razonamiento y Lógica:** Un grupo de técnicas diseñadas para mejorar las capacidades de razonamiento paso a paso, como Cadena de Pensamiento (CoT), Árbol de Pensamientos (ToT), Grafo de Pensamientos (GoT) y Autoconsistencia.  
* **Reducción de Alucinaciones:** Métodos enfocados en mejorar la veracidad fáctica de las respuestas, como la Generación Aumentada por Recuperación (RAG), ReAct y la Cadena de Verificación (CoVe).  
* **Generación y Ejecución de Código:** Técnicas especializadas para la síntesis de código, como el Programa de Pensamientos (PoT), la Cadena de Código (CoC) y el CoT Estructurado (SCoT).  
* Otras categorías incluyen la **Interacción con el Usuario** (por ejemplo, Active Prompting), el **Ajuste Fino y la Optimización** (por ejemplo, APE) y la **Gestión de Emociones y Tono** (por ejemplo, EmotionPrompting).

#### **5.3. Una Taxonomía Orientada a Objetivos**

La revisión de Li et al. propone una taxonomía novedosa y más abstracta, basada en las etapas del pensamiento lógico humano. Este marco se centra menos en la aplicación final y más en el proceso cognitivo que se está modelando. Sus cinco etapas interconectadas son:

1. **Descomposición de Objetivos:** Dividir un objetivo de alto nivel en sub-objetivos manejables (por ejemplo, Least-to-Most Prompting).  
2. **Selección de Acciones:** Elegir acciones efectivas para lograr los sub-objetivos (por ejemplo, restringir el espacio de salida).  
3. **Ejecución de Acciones:** Utilizar herramientas externas para ejecutar las acciones seleccionadas (por ejemplo, usar un intérprete de código).  
4. **Evaluación de Resultados de Sub-objetivos:** Obtener retroalimentación en cada paso para corregir errores (por ejemplo, Self-Refine, Autoconsistencia).  
5. **Selección Adicional de Sub-objetivos Valiosos:** Explorar múltiples secuencias de sub-objetivos y seleccionar las más prometedoras (por ejemplo, ToT, GoT).

#### **5.4. Una Taxonomía Centrada en la Eficiencia**

La revisión de Chang et al. categoriza los métodos basándose en el objetivo práctico y crítico de mejorar la eficiencia. Este enfoque aborda los costes humanos y computacionales del prompting. Sus dos ramas principales son:

* **Ingeniería de Prompts Automática:** Automatizar el diseño y la optimización de los prompts para reducir el esfuerzo humano. Esto incluye métodos basados en muestreo (por ejemplo, APE), basados en retroalimentación (por ejemplo, RLPrompt) y basados en edición.  
* **Compresión de Prompts:** Reducir la longitud de los prompts para ahorrar costes computacionales y espacio en la ventana de contexto. Esto se logra mediante técnicas de compresión de texto a vector (T2V) o de texto a texto (T2T), como la poda (por ejemplo, LLMLingua) o el resumen.

#### **5.5. "The Prompt Report": Un Vocabulario y Taxonomía Exhaustivos**

El trabajo de Schulhoff et al., titulado "The Prompt Report" , representa el esfuerzo más exhaustivo hasta la fecha para crear un entendimiento ontológico unificado. A través de una revisión sistemática de la literatura, los autores presentan un vocabulario detallado de 33 términos y una taxonomía que cataloga 58 técnicas de prompting para LLMs y 40 técnicas para otras modalidades. Su objetivo es establecer un entendimiento estructurado de los prompts, ensamblando una taxonomía de técnicas y analizando su uso para resolver la fragmentación terminológica del campo.  
La existencia de múltiples taxonomías en competencia no es un signo de confusión, sino más bien una característica de un campo científico naciente y vibrante. Cada taxonomía representa una "lente" diferente a través de la cual ver los mismos fenómenos complejos, y cada una es valiosa para diferentes propósitos. Un desarrollador que construye un asistente de codificación encontrará más útil la taxonomía centrada en la aplicación de Sahoo et al.. Un científico cognitivo encontrará más perspicaz la taxonomía orientada a objetivos de Li et al.. Un ingeniero de sistemas preocupado por los costes de despliegue se inclinará por la taxonomía centrada en la eficiencia de Chang et al.. Esta diversidad muestra que la "ingeniería de prompts" es un campo multifacético con diferentes subcomunidades y prioridades. Es probable que el campo converja hacia una taxonomía híbrida y multidimensional que incorpore aspectos de aplicación, proceso cognitivo y eficiencia del sistema. "The Prompt Report" es un paso significativo en esta dirección.  
La siguiente tabla comparativa sirve como una guía de referencia rápida, sintetizando las técnicas clave discutidas a lo largo de numerosos artículos en un formato único y estructurado.  
**Tabla 1: Una Taxonomía Comparativa de Técnicas de Prompting**

| Técnica | Principio Central | Caso de Uso Principal | Variantes Clave | Referencia(s) Seminal(es) |
| :---- | :---- | :---- | :---- | :---- |
| **Zero-Shot** | Instruir al modelo para que realice una tarea sin ejemplos. | Tareas generales, clasificación simple, resumen. | Prompting de instrucciones. |  |
| **Few-Shot (ICL)** | Proporcionar varios ejemplos (entrada-salida) en el prompt. | Tareas complejas que requieren un formato o estilo específico. | One-Shot, selección dinámica de ejemplos. |  |
| **Chain-of-Thought (CoT)** | Guiar al modelo para que genere un razonamiento paso a paso. | Razonamiento aritmético, de sentido común y simbólico. | Zero-Shot CoT, Auto-CoT, CoT Lógico. |  |
| **Self-Consistency** | Muestrear múltiples rutas de razonamiento y tomar una votación mayoritaria. | Mejorar la robustez y precisión de las tareas de razonamiento complejas. | N/A (es una estrategia de decodificación). |  |
| **Tree-of-Thoughts (ToT)** | Explorar múltiples rutas de razonamiento en una estructura de árbol. | Tareas que requieren exploración, planificación o retroceso. | Búsqueda en anchura/profundidad. |  |
| **Graph-of-Thoughts (GoT)** | Modelar el razonamiento como un grafo, permitiendo la síntesis de ideas. | Razonamiento altamente complejo y no lineal. | Agregación y refinamiento de pensamientos. |  |
| **Retrieval-Augmented Generation (RAG)** | Recuperar información externa relevante e incluirla en el prompt. | Preguntas basadas en conocimientos, reducción de alucinaciones. | RAG avanzado, RAG recursivo. |  |
| **ReAct** | Generar pensamientos y acciones de forma intercalada para interactuar con herramientas. | Tareas que requieren verificación de hechos o uso de herramientas externas. | N/A |  |
| **Program-of-Thoughts (PoT)** | Generar código ejecutable como la cadena de razonamiento. | Razonamiento numérico y simbólico preciso. | Chain-of-Code (CoC). |  |
| **Self-Refine** | Iterar generando, criticando y refinando la propia salida del modelo. | Mejorar la calidad de la salida en tareas de escritura o codificación. | N/A |  |

### **Capítulo 6: Ingeniería de Prompts Automática: Una Perspectiva de Optimización**

Este capítulo presenta la conceptualización más formal y matemática de la ingeniería de prompts, enmarcándola como un problema de optimización computacional. Este cambio de perspectiva es fundamental para la transición del campo de una práctica artesanal a una ciencia rigurosa.

#### **6.1. Los Límites de la Ingeniería Manual**

La ingeniería de prompts manual, aunque efectiva, enfrenta limitaciones fundamentales. Es un proceso laborioso que depende en gran medida de la experiencia y la intuición del experto, requiriendo un tedioso ciclo de ensayo y error. Además, los modelos son extremadamente sensibles a variaciones sintácticas menores en el prompt, donde cambios sutiles en la redacción o la puntuación pueden producir fluctuaciones significativas en el rendimiento. Este enfoque no es escalable, es difícil de adaptar a nuevas tareas o modelos y carece de la capacidad de alinearse eficazmente entre diferentes modalidades (por ejemplo, texto y visión).

#### **6.2. Formalizando la Optimización de Prompts**

Para superar estas limitaciones, la investigación ha avanzado hacia la ingeniería de prompts automática. El núcleo de este enfoque es reformular el diseño de prompts como un problema de optimización matemática. Formalmente, el problema se puede definir como la búsqueda de un prompt óptimo, p^\*, dentro de un espacio de prompts definido, P, que maximice una métrica de rendimiento, \\mathcal{F}, sobre un conjunto de datos de validación. Esto se puede expresar como :  
p^\* \= \\arg\\max\_{p \\in P} \\mathbb{E}\_{(x, y) \\sim \\mathcal{D}\_{val}} \[\\mathcal{F}(M(p, x), y)\]  
Donde M es el modelo de fundación (FM), x son las consultas de entrada, y son las salidas deseadas, y \\mathcal{F} es la función de evaluación. Esta formalización proporciona un marco unificado para organizar y comparar sistemáticamente diferentes métodos automáticos.

#### **6.3. Los Espacios de Optimización**

El problema de optimización se puede clasificar en función de la naturaleza de las variables del prompt que se están optimizando :

* **Optimización de Prompts Discretos (DPO):** Se centra en la optimización de "prompts duros" (*hard prompts*), que consisten en tokens de lenguaje natural discretos. Esto implica el uso de estrategias de búsqueda combinatoria para encontrar la secuencia óptima de instrucciones, los mejores ejemplos de pocos disparos o las cadenas de pensamiento más efectivas.  
* **Optimización de Prompts Continuos (CPO):** Se enfoca en la optimización de "prompts suaves" (*soft prompts*). Estos no son texto en lenguaje natural, sino vectores continuos y aprendibles (embeddings) que se concatenan a la entrada del modelo. Dado que estos vectores son diferenciables, este enfoque permite el uso de potentes métodos de optimización basados en gradientes, como el descenso de gradiente, para encontrar los vectores de prompt óptimos.  
* **Optimización de Prompts Híbridos (HPO):** Combina elementos discretos y continuos para lograr un efecto sinérgico, buscando optimizar simultáneamente las instrucciones en lenguaje natural y los embeddings suaves.

#### **6.4. Métodos de Optimización Automática**

Se han desarrollado varios marcos computacionales para resolver estos problemas de optimización :

* **Optimización Basada en Modelos de Fundación (FM):** Utiliza un LLM para generar y refinar prompts para otro LLM (o para sí mismo). Técnicas como Automatic Prompt Engineer (APE) y Optimization by Prompting (OPRO) entran en esta categoría. APE, por ejemplo, genera candidatas a instrucciones y las selecciona basándose en una puntuación de rendimiento, superando a menudo los prompts diseñados por humanos.  
* **Métodos Evolutivos:** Aplican algoritmos inspirados en la biología, como los algoritmos genéticos, para "evolucionar" una población de prompts. Los prompts se someten a operaciones de mutación (cambiar palabras) y cruce (combinar prompts) y se seleccionan para la siguiente generación en función de su rendimiento, imitando la "supervivencia del más apto".  
* **Optimización Basada en Gradientes:** Se utiliza principalmente para la optimización de prompts suaves continuos. Dado que los prompts son vectores en un espacio continuo, se pueden calcular gradientes con respecto a la función de pérdida de la tarea y utilizar algoritmos como el descenso de gradiente para actualizar iterativamente los vectores del prompt hasta alcanzar un rendimiento óptimo.  
* **Aprendizaje por Refuerzo (RL):** Trata el proceso de generación de prompts como una política en un entorno de RL. El "agente" (un LLM) genera un prompt (una "acción"), y recibe una "recompensa" basada en la calidad de la salida del modelo objetivo. El agente utiliza esta retroalimentación para aprender a generar prompts cada vez mejores.

La formalización de la ingeniería de prompts como un problema de optimización es el paso más significativo en su transición de un arte a una ciencia. Permite que el potente conjunto de herramientas de la optimización matemática se aplique directamente al problema de la interacción con los LLMs. En lugar de depender de la intuición humana para encontrar un buen prompt, ahora podemos utilizar métodos automatizados y basados en principios para buscar en el vasto espacio de posibles prompts de manera mucho más sistemática y eficiente. La conclusión lógica de esta tendencia es el desarrollo de sistemas totalmente autónomos capaces de diseñar sus propios prompts óptimos para cualquier tarea, lo que representa un paso crucial hacia una IA más autónoma y auto-mejorable.

## **Parte IV: Mejora de la Robustez y Capacidades Especializadas**

Esta parte final aborda dos aspectos prácticos y críticos de la ingeniería de prompts: superar las limitaciones inherentes de los LLMs (como la alucinación) y adaptar las técnicas generales para dominios especializados de alto valor, como la generación de código y fórmulas.

### **Capítulo 7: Mitigación de Alucinaciones y Mejora de la Precisión Fáctica**

Este capítulo se centra en las técnicas diseñadas para anclar las salidas de los LLMs en conocimientos externos y verificables, abordando una de sus debilidades más significativas.

#### **7.1. El Problema de la Alucinación**

Los modelos de lenguaje grandes, a pesar de sus impresionantes capacidades, son propensos a generar información que es plausible, coherente y gramaticalmente correcta, pero que es fácticamente incorrecta o completamente inventada. Este fenómeno, conocido como "alucinación", es una barrera importante para su despliegue en aplicaciones de alto riesgo. Las alucinaciones surgen porque los LLMs son fundamentalmente modelos generativos entrenados para predecir la siguiente palabra más probable en una secuencia, basándose en los patrones de sus datos de entrenamiento estáticos. No poseen un verdadero entendimiento del mundo ni acceso a información en tiempo real, lo que les impide verificar la veracidad de lo que generan.

#### **7.2. Generación Aumentada por Recuperación (Retrieval-Augmented Generation, RAG)**

* **Mecanismo:** RAG es un enfoque híbrido que aborda directamente el problema de la base de conocimientos estática. Combina el conocimiento paramétrico del LLM (aprendido durante el entrenamiento) con un conocimiento no paramétrico de una base de datos externa (por ejemplo, un corpus de documentos, una base de datos o una API web). El proceso típico de RAG implica dos pasos: primero, cuando se recibe una consulta del usuario, un componente "recuperador" busca en la base de conocimientos externa para encontrar fragmentos de información relevantes para la consulta. Segundo, estos fragmentos recuperados se incorporan al prompt que se le da al LLM, junto con la consulta original. El LLM utiliza entonces este contexto aumentado para generar una respuesta que está anclada en la información externa proporcionada.  
  * **Ejemplo práctico:**  
    * **Usuario:** "¿Cuáles fueron los hallazgos clave del informe de ganancias de la empresa XYZ para el cuarto trimestre de 2024?"  
    * **Sistema RAG:**  
      1. **Recupera:** Busca en la base de datos interna el documento "Informe de ganancias Q4 2024 de XYZ".  
      2. **Aumenta:** Crea un nuevo prompt: Contexto: \\n\\n Pregunta: ¿Cuáles fueron los hallazgos clave del informe de ganancias de la empresa XYZ para el cuarto trimestre de 2024?  
      3. **Genera:** El LLM lee el contexto proporcionado y genera un resumen preciso basado en el documento real, en lugar de inventar cifras.  
* **Ventajas:** RAG faculta a los LLMs para generar respuestas más precisas, actualizadas y factualmente correctas, especialmente para tareas intensivas en conocimiento. Reduce significativamente las alucinaciones al proporcionar al modelo la información correcta en el momento de la inferencia.

#### **7.3. Razonamiento y Actuación (ReAct)**

* **Mecanismo:** El marco ReAct (Reasoning and Acting) permite a los LLMs sinergizar el razonamiento y la acción de una manera intercalada. En lugar de simplemente generar una cadena de pensamiento pasiva, el modelo genera trazas de razonamiento (pensamientos) y acciones específicas que puede ejecutar. Estas acciones pueden incluir la consulta a una herramienta externa, como una API de búsqueda o una calculadora. El modelo luego observa el resultado de la acción y utiliza esa nueva información para informar su siguiente pensamiento y acción, creando un bucle dinámico de pensamiento-acción-observación.  
  * **Ejemplo práctico:**  
    * **Pregunta:** "¿Cuál es la población de la capital de Francia y cuál es su temperatura actual?"  
    * **Proceso ReAct:**  
      1. **Pensamiento:** Necesito encontrar la capital de Francia y luego buscar su población y temperatura.  
      2. **Acción:** search("capital de Francia") \-\> **Observación:** "París"  
      3. **Pensamiento:** Ahora necesito la población de París.  
      4. **Acción:** search("población de París") \-\> **Observación:** "2.1 millones"  
      5. **Pensamiento:** Ahora necesito la temperatura actual en París.  
      6. **Acción:** weather("París") \-\> **Observación:** "15°C"  
      7. **Respuesta Final:** La población de París es de 2.1 millones y su temperatura actual es de 15°C.  
* **Ventajas:** ReAct aborda la alucinación al permitir que el modelo busque y verifique activamente la información de herramientas externas. Si el modelo no sabe algo, puede generar una acción para buscarlo. Esto le permite actualizar dinámicamente su comprensión y manejar excepciones, superando problemas de propagación de errores en tareas como la verificación de hechos y la respuesta a preguntas.

#### **7.4. Bucles de Verificación y Refinamiento**

* **Cadena de Verificación (CoVe):** CoVe es un proceso explícito y de múltiples pasos diseñado para que el modelo verifique sus propias respuestas. El proceso implica: 1\) generar una respuesta de referencia; 2\) planificar preguntas de verificación diseñadas para comprobar la respuesta; 3\) responder a esas preguntas de forma independiente (para evitar el sesgo de autoconfirmación); y 4\) generar una respuesta final revisada que incorpore los resultados de la verificación. Este enfoque sistemático reduce las alucinaciones al mejorar las capacidades de razonamiento lógico.  
* **Auto-refinamiento (Self-Refine):** Este es un proceso iterativo que imita el ciclo humano de redacción y revisión. El modelo primero genera una salida inicial. Luego, en un segundo paso, se le pide que critique su propia salida, identificando posibles fallos o áreas de mejora. Finalmente, se le pide que refine la salida basándose en su propia crítica. Este bucle puede repetirse varias veces para mejorar incrementalmente la calidad de la salida.  
  * **Ejemplo práctico:**  
    1. **Prompt Inicial:** "Escribe un párrafo sobre los beneficios de la energía solar."  
    2. **Salida v1:** "La energía solar es buena. Usa el sol. Es renovable."  
    3. **Prompt de Crítica:** "Critica el párrafo anterior. ¿Es demasiado simple? ¿Le faltan detalles?"  
    4. **Crítica:** "El párrafo es muy básico. No explica los beneficios específicos como la reducción de la huella de carbono o el ahorro de costes."  
    5. **Prompt de Refinamiento:** "Reescribe el párrafo basándote en la crítica anterior."  
    6. **Salida v2:** "La energía solar ofrece beneficios significativos, incluyendo la reducción de las emisiones de gases de efecto invernadero y ahorros a largo plazo en las facturas de electricidad. Al aprovechar la luz solar, una fuente de energía inagotable, disminuye nuestra dependencia de los combustibles fósiles."

El auge de técnicas como RAG y ReAct significa un cambio filosófico crucial en cómo utilizamos los LLMs. En lugar de ver al LLM como un oráculo omnisciente, ahora lo tratamos como un **motor de razonamiento** que opera sobre un **contexto suministrado externamente**. La esperanza inicial de que los LLMs, con suficiente escala, se convertirían en repositorios fiables de conocimiento fáctico ha demostrado ser incorrecta. La solución no es hacer los modelos más grandes, sino cambiar su rol. En un sistema RAG/ReAct, el LLM ya no es la fuente principal de *hechos*; la base de datos externa o la API es la fuente de hechos. El nuevo rol del LLM es: 1\) comprender la intención del usuario, 2\) formular una consulta para la herramienta externa, 3\) sintetizar la información recuperada, y 4\) generar una respuesta coherente en lenguaje natural basada *únicamente* en esa información recuperada. Este paradigma híbrido, que aprovecha lo mejor de ambos mundos —el razonamiento de los LLMs y el almacenamiento de conocimiento de las bases de datos—, es probablemente el futuro de los sistemas de IA fiables.

### **Capítulo 8: Adaptación Específica del Dominio: Prompting para la Generación de Código y Fórmulas**

Este capítulo utiliza la generación de código como un ejemplo principal para ilustrar cómo los principios generales de prompting se adaptan y especializan para dominios complejos y estructurados, abordando directamente el interés del usuario en la generación de "fórmulas".

#### **8.1. Por qué el Código es un Caso Especial**

La generación de código es un dominio ideal para la ingeniería de prompts por varias razones. Requiere una lógica estricta y una consistencia sintáctica, y lo que es más importante, produce una salida que es verificable de manera determinista: el código se compila y se ejecuta correctamente, o no lo hace. Esto proporciona una métrica clara y objetiva para evaluar el rendimiento de un prompt, a diferencia de tareas más subjetivas como la escritura creativa. La calidad del código generado por los LLMs depende en gran medida de la calidad de los prompts de entrada.

#### **8.2. Descargando la Computación a Intérpretes**

Una de las estrategias más poderosas en este dominio es utilizar el LLM para generar código, pero no para ejecutar la lógica en sí. El objetivo es evitar que el modelo realice cálculos aritméticos o lógicos, tareas en las que puede cometer errores.

* **Programa de Pensamientos (Program-of-Thoughts, PoT):** En lugar de generar una cadena de pensamiento en lenguaje natural, PoT pide al LLM que genere un programa ejecutable (por ejemplo, en Python) que resuelva el problema. Este programa se ejecuta luego en un intérprete externo para obtener la respuesta final. Este enfoque descarga la computación numérica y lógica a una herramienta determinista y fiable, aprovechando el LLM para lo que mejor sabe hacer: traducir el lenguaje natural a un lenguaje formal.  
  * **Ejemplo práctico (Generación de Fórmulas):**  
    * **Prompt CoT (propenso a errores):** "Calcula el interés compuesto para un principal de $1000 a una tasa del 5% anual durante 10 años."  
    * **Prompt PoT (fiable):** "Escribe un script de Python para calcular el interés compuesto para un principal de $1000 a una tasa del 5% anual durante 10 años."  
    * **Salida PoT:**  
      `principal = 1000`  
      `rate = 0.05`  
      `time = 10`  
      `amount = principal * (1 + rate)**time`  
      `print(amount)`

El código se ejecuta externamente para obtener la respuesta correcta y fiable.

* **Cadena de Código (Chain-of-Code, CoC):** Esta es una extensión de PoT que anima al LLM a formatear incluso las subtareas semánticas como pseudocódigo flexible. Utiliza el código como el medio principal para el razonamiento, demostrando ser superior al CoT tradicional en preguntas que requieren un razonamiento numérico o simbólico intensivo.

#### **8.3. Estructurando Prompts para Código**

La estructura del prompt es especialmente crítica para la generación de código.

* **Cadena de Pensamiento Estructurada (SCoT):** Esta técnica incorpora estructuras de programación (como secuencias, ramas y bucles) en los pasos de razonamiento del prompt. Esto guía explícitamente al LLM para que considere los requisitos desde la perspectiva del código fuente, mejorando su rendimiento en la generación de código estructurado donde el CoT tradicional muestra una menor precisión.  
* **Proporcionar Guías y Ejemplos:** La investigación ha demostrado que incorporar directrices generales de codificación o ejemplos de código de alta calidad (en un enfoque de 1-shot) en el prompt mejora significativamente la calidad, corrección y fiabilidad del código generado. Un prompt puede incluir una plantilla que solicite explícitamente un docstring y un manejo de errores, lo que resulta en un código más robusto.  
  * **Ejemplo práctico:**  
    `Escribe una función de Python para calcular el factorial de un número. Asegúrate de que la función tenga un docstring y maneje correctamente las entradas no válidas (por ejemplo, números negativos).`  
    Este prompt estructurado produce un código de mayor calidad que un simple "escribe una función factorial".

#### **8.4. Optimización Automática para la Generación de Código**

Los principios de la ingeniería de prompts automática se están aplicando con gran éxito a la generación de código.

* **Prochemy:** Un enfoque novedoso que refina iterativamente los prompts para la generación de código basándose en el rendimiento del modelo en un conjunto de entrenamiento. Automatiza el proceso de optimización para encontrar un prompt final que mejore la consistencia y la fiabilidad en diversas tareas de codificación.  
* **EFFI-LEARNER:** Un marco de auto-optimización que se centra no solo en la corrección del código, sino también en su *eficiencia*. Primero, genera código, luego lo ejecuta localmente para capturar perfiles de sobrecarga de ejecución (tiempo, uso de memoria). Estos perfiles se retroalimentan al LLM, que luego revisa el código para reducir la sobrecarga. A través de esta auto-optimización iterativa, se mejora significativamente la eficiencia del código generado por el LLM.  
  * **Ejemplo práctico:**  
    1. **Prompt Inicial:** "Escribe una función para encontrar el elemento único en una lista donde todos los demás elementos aparecen dos veces."  
    2. **Salida v1:** Una función que utiliza un bucle anidado (ineficiente).  
    3. **Ejecución y Perfilado:** El sistema ejecuta el código y detecta un alto tiempo de ejecución.  
    4. **Prompt de Refinamiento:** "La función anterior es demasiado lenta. Aquí está su perfil de ejecución. Por favor, reescríbela para que tenga una complejidad de tiempo lineal y use espacio constante."  
    5. **Salida v2:** Una función optimizada que utiliza la operación XOR (eficiente).

El prompting para código y fórmulas revela un patrón generalizable y potente: **traducir, no calcular**. La principal fortaleza de un LLM no es ser una calculadora o un razonador lógico perfecto, sino ser un traductor universal entre el lenguaje natural y los sistemas formales. Los primeros intentos de resolver problemas matemáticos con LLMs a menudo fracasaban debido a errores aritméticos en sus cadenas de pensamiento. La idea clave de PoT fue dejar de pedirle al modelo que *hiciera las matemáticas* y, en su lugar, pedirle que *escribiera el código que hace las matemáticas*. La tarea del LLM pasó de ser "razonar sobre números" a "traducir un problema de palabras a código Python", una tarea para la que está excepcionalmente bien preparado. El cálculo real se descarga a un intérprete de Python, que es perfectamente determinista.  
Este mismo principio se aplica directamente a la generación de "fórmulas". La forma más eficaz de generar una fórmula correcta (para Excel, SQL o un cálculo científico) es pedir al LLM que escriba la fórmula como una cadena de texto dentro de un bloque de código, en lugar de intentar que calcule el resultado directamente. Este paradigma de "traducir, no calcular" es una piedra angular para construir sistemas fiables con LLMs, definiendo un claro límite de responsabilidad: el LLM se encarga de la tarea semántica de comprender la intención humana y traducirla a una representación formal, mientras que las herramientas deterministas se encargan de la ejecución de esa representación.  
**Tabla 2: Técnicas de Prompting Especializadas para la Generación de Código y Fórmulas**

| Técnica | Mecanismo Central | Ventaja sobre el CoT General | Aplicación de Ejemplo |
| :---- | :---- | :---- | :---- |
| **Program-of-Thoughts (PoT)** | Genera código ejecutable (por ejemplo, Python) como la cadena de razonamiento. | Descarga el cálculo a un intérprete determinista, eliminando errores aritméticos. | Resolver un problema de palabras matemáticas generando un script de Python que lo calcule. |
| **Chain-of-Code (CoC)** | Utiliza el código o pseudocódigo como el lenguaje principal para el razonamiento. | Aprovecha la estructura lógica inherente al código para tareas semánticas y simbólicas. | Descomponer una tarea de planificación en pasos lógicos representados como funciones. |
| **Structured CoT (SCoT)** | Incorpora estructuras de programación (secuencia, rama, bucle) en el prompt de CoT. | Guía explícitamente al LLM para generar código bien estructurado y sintácticamente correcto. | Generar una función que contenga un bucle y una lógica condicional a partir de una descripción. |
| **EFFI-LEARNER** | Utiliza perfiles de sobrecarga de ejecución (tiempo, memoria) como retroalimentación para la auto-optimización. | Mejora no solo la corrección, sino también la eficiencia computacional del código generado. | Refinar un algoritmo de ordenación generado para que utilice menos memoria o se ejecute más rápido. |

### **Conclusión y Direcciones Futuras**

Esta revisión sistemática ha trazado la evolución de la ingeniería de prompts desde un arte intuitivo hasta una disciplina de ingeniería estructurada, sistemática y cada vez más automatizada. La trayectoria es clara: desde simples consultas de cero disparos, pasando por la guía contextual del prompting de pocos disparos, hasta la elicitation de razonamiento explícito con la Cadena de Pensamiento. La progresión no se detuvo ahí, sino que avanzó hacia estructuras de razonamiento más complejas y no lineales como el Árbol y el Grafo de Pensamientos, que imitan de cerca los algoritmos de búsqueda de la IA clásica. Finalmente, la formalización de todo el proceso como un problema de optimización matemática ha abierto la puerta a métodos automáticos que prometen superar sistemáticamente el diseño manual. Al mismo tiempo, técnicas como RAG y ReAct han redefinido el rol del LLM, transformándolo de un oráculo de conocimiento a un motor de razonamiento que opera sobre información externa verificable, un paradigma fundamental para construir sistemas de IA fiables.  
La investigación en ingeniería de prompts es un campo vibrante con muchas fronteras abiertas. La literatura científica destaca varias direcciones futuras prometedoras que darán forma a la próxima generación de interacciones con la IA:

* **Optimización Restringida:** Un área de investigación crucial es el diseño de prompts que no solo maximicen el rendimiento, sino que también se adhieran a un conjunto de restricciones específicas. Esto incluye restricciones éticas (evitar sesgos), legales (respetar la privacidad), de seguridad (prevenir vulnerabilidades) y semánticas (mantener la coherencia lógica).  
* **Prompting Orientado a Agentes:** A medida que los LLMs se convierten en el cerebro de agentes autónomos que deben planificar, actuar y aprender en entornos complejos, se necesita una nueva clase de ingeniería de prompts. Esto implica diseñar prompts que permitan a los agentes descomponer objetivos, utilizar herramientas, procesar retroalimentación del entorno y adaptar sus planes dinámicamente.  
* **Prompting Transmodal y Multilingüe:** La mayoría de las investigaciones se han centrado en el texto en inglés. Una frontera importante es extender y adaptar estas técnicas más allá del texto a otras modalidades como imágenes, audio y vídeo, así como a una amplia gama de idiomas humanos, especialmente aquellos con pocos recursos.  
* **Prompting para Modelos Más Pequeños:** Muchas de las técnicas de razonamiento más potentes, como CoT, son habilidades emergentes de los modelos más grandes y costosos. Un desafío clave es desarrollar técnicas de prompting que puedan elicitar capacidades de razonamiento complejas en modelos más pequeños y eficientes, democratizando el acceso a la IA avanzada y reduciendo los costes computacionales y el impacto ambiental.

En resumen, la ingeniería de prompts ha pasado de ser un conjunto de "trucos" a ser el núcleo científico de cómo nos comunicamos y controlamos los modelos de lenguaje grandes. Su desarrollo continuo es fundamental para desbloquear todo el potencial de la inteligencia artificial, haciéndola más capaz, fiable, eficiente y segura.

### **Apéndice: Bibliografía Completa**

* Arora, S., et al. (2022). *Ask Me Anything: A simple strategy for prompting language models*.  
* Beurer-Kellner, L., Fischer, M., & Vechev, M. (2022). *Prompting Is Programming: A Query Language for Large Language Models*. arXiv:2212.06094.  
* Brown, T., et al. (2020). *Language Models are Few-Shot Learners*.  
* Chang, K., Xu, S., et al. (2024). *Efficient Prompting Methods for Large Language Models: A Survey*. arXiv:2404.01077.  
* Chen, B., Zhang, Z., Langrené, N., & Zhu, S. (2025). *Unleashing the potential of prompt engineering for large language models*. Patterns, 6(6), 101260\. arXiv:2310.14735.  
* Eskandari, F., & Roozbahani, Z. (2025). *A review of prompt engineering methods in large language models*. Engineering Management and Soft Computing, 10(2), 246-279.  
* Fu, Y., et al. (2023). *Active-Prompt: A Two-Stage Framework for Active Learning with Chain-of-Thought*.  
* Li, H., Leung, J., & Shen, Z. (2024). *Towards Goal-oriented Prompt Engineering for Large Language Models: A Survey*. arXiv:2401.14043.  
* Li, W., Wang, X., Li, W., & Jin, B. (2025). *A Survey of Automatic Prompt Engineering: An Optimization Perspective*. arXiv:2502.11560.  
* Min, S., et al. (2022). *Rethinking the Role of Demonstrations: What Makes In-Context Learning Work?*.  
* Sahoo, P., Singh, A. K., Saha, S., Jain, V., Mondal, S., & Chadha, A. (2024). *A Systematic Survey of Prompt Engineering in Large Language Models: Techniques and Applications*. arXiv:2402.07927.  
* Schulhoff, S., et al. (2024). *The Prompt Report: A Systematic Survey of Prompt Engineering Techniques*. arXiv:2406.06608.  
* Vatsal, S., Dubey, H., & Singh, a. (2025). *Multilingual Prompt Engineering in Large Language Models: A Survey Across NLP Tasks*. arXiv:2505.11665.  
* Wang, X., et al. (2022). *Self-Consistency Improves Chain of Thought Reasoning in Language Models*.  
* Wei, J., et al. (2022). *Chain-of-Thought Prompting Elicits Reasoning in Large Language Models*.  
* White, J., Fu, Q., Hays, S., et al. (2023). *A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT*. ArXiv.  
* Zhou, D., et al. (2022). *Least-to-Most Prompting Enables Complex Reasoning in Large Language Models*.

#### **Obras citadas**

1\. arXiv:2402.07927v2 \[cs.AI\] 16 Mar 2025, https://arxiv.org/abs/2402.07927 2\. arxiv.org, https://arxiv.org/html/2406.06608v6 3\. (PDF) Unleashing the potential of prompt engineering for large ..., https://www.researchgate.net/publication/375074387\_Unleashing\_the\_potential\_of\_prompt\_engineering\_for\_large\_language\_models 4\. Unleashing the potential of prompt engineering for large language models \- ResearchGate, https://www.researchgate.net/publication/391582389\_Unleashing\_the\_potential\_of\_prompt\_engineering\_for\_large\_language\_models 5\. Optimizing AI Results with Structured Prompting \- Hypha HubSpot Development, https://www.hyphadev.io/blog/ai-prompt-optimizer 6\. Mastering Few-Shot Prompting: A Comprehensive Guide | by Software Guide \- Medium, https://softwareguide.medium.com/mastering-few-shot-prompting-a-comprehensive-guide-6eda3761538c 7\. Prompt Engineering for AI Guide | Google Cloud, https://cloud.google.com/discover/what-is-prompt-engineering 8\. Zero-Shot Prompting: Examples, Theory, Use Cases \- DataCamp, https://www.datacamp.com/tutorial/zero-shot-prompting 9\. Shot-Based Prompting: Zero-Shot, One-Shot, and Few-Shot Prompting \- Learn Prompting, https://learnprompting.org/docs/basics/few\_shot 10\. The Few Shot Prompting Guide \- PromptHub, https://www.prompthub.us/blog/the-few-shot-prompting-guide 11\. Zero-Shot Prompting \- Prompt Engineering Guide, https://www.promptingguide.ai/techniques/zeroshot 12\. Prompt engineering and framework: implementation to increase code reliability based guideline for LLMs \- arXiv, https://arxiv.org/html/2506.10989v1 13\. Prompting Is Programming: A Query Language for Large Language Models \- Bohrium, https://www.bohrium.com/paper-details/prompting-is-programming-a-query-language-for-large-language-models/885130950881575100-52678 14\. Top Research Papers on Prompt Engineering \- Paperguide, https://paperguide.ai/papers/top/research-papers-prompt-engineering/ 15\. A Survey of Prompt Engineering for Large Language Models | by Nate Dong, Ph.D., https://natedong72.medium.com/a-survey-of-prompt-engineering-for-large-language-models-416bbed684cb 16\. A Guide to Zero-Shot, One-Shot, & Few-Shot AI Prompting | The GoSearch Blog, https://www.gosearch.ai/blog/zero-shot-one-shot-few-shot-ai-prompting/ 17\. Zero-Shot vs. Few-Shot Prompting: Key Differences \- Shelf.io, https://shelf.io/blog/zero-shot-and-few-shot-prompting/ 18\. What is zero-shot prompting? \- IBM, https://www.ibm.com/think/topics/zero-shot-prompting 19\. Few-Shot Prompting \- Prompt Engineering Guide, https://www.promptingguide.ai/techniques/fewshot 20\. Chain-of-Thought Prompting: Techniques, Tips, and Code Examples \- Helicone, https://www.helicone.ai/blog/chain-of-thought-prompting 21\. Chain Of Thought Prompting: Everything You Need To Know \- Annotation Box, https://annotationbox.com/chain-of-thought-prompting/ 22\. What is chain of thought (CoT) prompting? \- IBM, https://www.ibm.com/think/topics/chain-of-thoughts 23\. Chain-of-Thought Prompting: A Comprehensive Analysis of Reasoning Techniques in Large Language Models | by Pier-Jean Malandrino | Scub-Lab, https://lab.scub.net/chain-of-thought-prompting-a-comprehensive-analysis-of-reasoning-techniques-in-large-language-b67fdd2eb72a 24\. Chain of Thought Prompting Guide \- PromptHub, https://www.prompthub.us/blog/chain-of-thought-prompting-guide 25\. Chain of Thought Prompting: A Deep Dive into the AI Architecture Pattern \- Rahul Krishnan, https://solutionsarchitecture.medium.com/chain-of-thought-prompting-a-deep-dive-into-the-ai-architecture-pattern-d35cd8b52c53 26\. Towards Goal-oriented Prompt Engineering for Large Language ..., https://arxiv.org/abs/2401.14043 27\. The Prompt Report: A Systematic Survey of Prompt Engineering Techniques \- arXiv, https://arxiv.org/abs/2406.06608 28\. A review of prompt engineering methods in large language models, https://jemsc.qom.ac.ir/article\_3396.html?lang=en 29\. Daily Papers \- Hugging Face, https://huggingface.co/papers?q=prompting-style%20tasks 30\. Efficient Prompting Methods for Large Language Models: A ... \- arXiv, https://arxiv.org/abs/2404.01077 31\. The Prompt Report: A Systematic Survey of Prompt Engineering ..., https://deeplearn.org/arxiv/580487/the-prompt-report:-a-systematic-survey-of-prompt-engineering-techniques 32\. A Survey of Automatic Prompt Engineering: An Optimization Perspective \- arXiv, https://arxiv.org/html/2502.11560v1 33\. Wenhao Li's research works | East China Normal University and other places, https://www.researchgate.net/scientific-contributions/Wenhao-Li-2305257303 34\. (PDF) A Survey of Automatic Prompt Engineering: An Optimization ..., https://www.researchgate.net/publication/389091558\_A\_Survey\_of\_Automatic\_Prompt\_Engineering\_An\_Optimization\_Perspective 35\. \[Literature Review\] A Survey of Automatic Prompt Engineering: An Optimization Perspective, https://www.themoonlight.io/en/review/a-survey-of-automatic-prompt-engineering-an-optimization-perspective 36\. Prompting Techniques for Secure Code Generation: A Systematic Investigation \- arXiv, https://arxiv.org/html/2407.07064v1 37\. Prompt Alchemy: Automatic Prompt Refinement for Enhancing Code Generation \- arXiv, https://arxiv.org/html/2503.11085v1 38\. Enhancing Computer Programming Education with LLMs: A Study on Effective Prompt Engineering for Python Code Generation \- arXiv, https://arxiv.org/html/2407.05437v1 39\. EFFI-LEARNER: Enhancing Efficiency of Generated Code via Self-Optimization \- arXiv, https://arxiv.org/pdf/2405.15189 40\. \[2505.11665\] Multilingual Prompt Engineering in Large Language Models: A Survey Across NLP Tasks \- arXiv, https://arxiv.org/abs/2505.11665
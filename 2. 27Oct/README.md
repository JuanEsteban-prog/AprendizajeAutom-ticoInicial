Un conjunto de datos puede representarse como un subconjunto de \(\mathbb{R}^n\), donde \(n\) es el número de variables o características medidas por observación. Cada elemento del conjunto representa una observación y la cardinalidad del conjunto corresponde al número de observaciones distintas.

**Nota:** Si los datos se organizan en una matriz, las filas representan las observaciones y las columnas representan las variables. En ese caso, para una matriz de datos con \(m\) filas y \(n\) columnas, se tiene \(X \in \mathbb{R}^{m \times n}\), donde \(m\) es el número de observaciones y \(n\) el número de variables.

Los datos son un subjunto de \(\mathbb{R}^n\).

**Modelo:** Es una función. 

La distinción es importante: en \(\mathbb{R}^n\), \(n\) representa la dimensión de cada observación, no la cantidad de filas del conjunto de datos.

## Tipos de aprendizaje
- Aprendizaje supervisado
- Aprendizaje no supervisado 

### Aprendizaje Supervisado
Consiste en aprender una función a partir de un conjunto de datos etiquetados, con el objetivo de encontrar una relación entre las características de las instancias de entrada y sus etiquetas correspondientes, que permita predecir las etiquetas de nuevas instancias.

Puede duplicar el cesgo de datos. Si le damos datos basura genera basura.

### Aprendizaje No Supervisado
Consiste en encontrar patrones, estructuras o relaciones dentro de un conjunto de datos sin etiquetas predefinidas, con el objetivo de descubrir agrupaciones, identificar similitudes o extraer información relevante a partir de las características de las instancias.

## Tipos de Tareas
- Clasificación.
- Regresión.
- Agrupamiento.

### Clasificación
Es una tarea de aprendizaje supervisado donde el conjunto de etiquetas es un conjunto finito y discreto.
### Regresión
Es una tarea de aprendizaje supervisado donde el conjunto de etiquetas es un conjunto continuo.
### Agrupamiento
Es una tarea de aprendizaje no supervisado donde se busca agrupar las instancias en función de sus características. 

## Aprendizaje supervisado vs. no supervisado
1. Ejemplos prácticos
Ejemplo 1: Detección de spam en correos electrónicos

Situación:

Un sistema analiza miles de correos electrónicos que ya han sido identificados como spam o como mensajes legítimos. Después, recibe un correo nuevo y decide a cuál de los dos tipos pertenece.

Respuesta: Aprendizaje supervisado.

¿Por qué?

El sistema aprende a partir de ejemplos cuya respuesta correcta ya conoce. Luego utiliza lo aprendido para tomar decisiones sobre correos nuevos.

Ejemplo 2: Análisis del comportamiento de clientes

Situación:

Una tienda analiza las compras de sus clientes y descubre que existen distintos perfiles de comportamiento según los productos que suelen comprar, sin que nadie le haya indicado previamente cuáles existen.

Respuesta: Aprendizaje no supervisado.

¿Por qué?

El sistema descubre patrones y similitudes por sí mismo, sin contar con respuestas previamente conocidas.

Ejemplo 3: Diagnóstico médico

Situación:

Un hospital utiliza registros antiguos de pacientes, que incluyen sus síntomas y el diagnóstico confirmado por los médicos, para estimar el diagnóstico de nuevos pacientes.

Respuesta: Aprendizaje supervisado.

¿Por qué?

El sistema aprende a partir de casos anteriores que contienen información sobre los síntomas y el diagnóstico confirmado. Después utiliza esos conocimientos para evaluar nuevos casos.

Ejemplo 4: Recomendaciones musicales

Situación:

Una plataforma musical examina los hábitos de escucha de millones de usuarios y descubre similitudes entre sus preferencias, sin recibir instrucciones sobre qué tipos de oyentes debería encontrar.

Respuesta: Aprendizaje no supervisado.

¿Por qué?

El sistema encuentra similitudes y patrones en los hábitos de escucha sin disponer de respuestas predeterminadas sobre cómo debe clasificar a los usuarios.

Ejemplo 5: Predicción del precio de viviendas

Situación:

Una empresa utiliza datos históricos de viviendas, junto con sus precios de venta conocidos, para estimar cuánto podría costar una vivienda nueva.

Respuesta: Aprendizaje supervisado.

¿Por qué?

El sistema aprende a partir de ejemplos que contienen el precio real de cada vivienda. Con esa información, aprende la relación entre las características de una vivienda y su precio.

Ejemplo 6: Detección de anomalías en máquinas

Situación:

Una fábrica registra las vibraciones y temperaturas de sus máquinas y busca comportamientos inusuales que no coinciden con los patrones habituales, sin contar con ejemplos previos de cada posible anomalía.

Respuesta: Aprendizaje no supervisado.

¿Por qué?

El sistema aprende cuáles son los patrones habituales de funcionamiento y busca desviaciones sin necesitar ejemplos previamente identificados de cada anomalía.

### 2. Tips para identificar el tipo de aprendizaje
Tip 1: Pregúntate si el sistema conoce las respuestas correctas

Esta es una de las preguntas más útiles.

Supervisado: durante el entrenamiento, el sistema dispone de ejemplos con respuestas conocidas.
No supervisado: el sistema recibe datos y debe descubrir patrones o estructuras sin disponer de esas respuestas.

Ejemplo:

Si entrenas un sistema con fotografías de perros y gatos que ya han sido identificadas correctamente, es supervisado.

Si le proporcionas miles de fotografías y buscas que descubra cuáles son similares entre sí sin indicarle qué aparece en ellas, es no supervisado.

Tip 2: Observa qué intenta conseguir el sistema
Supervisado: suele predecir un resultado concreto, como un precio, un diagnóstico o si un correo es spam.
No supervisado: suele descubrir patrones, similitudes, estructuras o comportamientos inusuales en los datos.
Tip 3: Fíjate en la información disponible durante el entrenamiento

No te centres únicamente en el resultado final. Dos sistemas pueden producir resultados parecidos, pero utilizar métodos de aprendizaje diferentes.

Por ejemplo, una empresa puede identificar perfiles de clientes mediante dos métodos:

Si utiliza ejemplos anteriores en los que los perfiles ya fueron determinados, puede tratarse de aprendizaje supervisado.
Si el sistema descubre los perfiles a partir de los hábitos de compra, puede tratarse de aprendizaje no supervisado.

Lo importante es cómo aprendió el sistema, no solamente qué resultado produce.

Tip 4: No confundas predicción con aprendizaje supervisado en todos los casos

Aunque las predicciones suelen asociarse al aprendizaje supervisado, lo importante es cómo se entrenó el modelo.

Un sistema no supervisado también puede producir información útil para tomar decisiones. Por ejemplo, puede detectar que el comportamiento de una máquina se aleja de sus patrones habituales.

Tip 5: Busca la diferencia entre aprender una respuesta y descubrir una estructura

Una forma sencilla de recordarlo:

Supervisado: aprender a partir de ejemplos con respuestas conocidas.
No supervisado: descubrir patrones a partir de datos sin respuestas conocidas.
3. Tabla de referencia rápida
Característica	Supervisado	No supervisado
Información de entrenamiento	Ejemplos con respuestas conocidas	Datos sin respuestas conocidas
Propósito habitual	Predecir un resultado	Descubrir patrones o estructuras
Ejemplos típicos	Diagnóstico, precios, spam	Perfiles de clientes, similitudes, anomalías
Pregunta clave	¿Conoce las respuestas de los ejemplos de entrenamiento?	¿Debe descubrir los patrones por sí mismo?
4. Regla mental para un examen

Cuando leas un enunciado, sigue estos pasos:

Identifica qué datos recibe el sistema.
Comprueba si esos datos incluyen respuestas correctas conocidas.
Determina si el sistema aprende a predecir una respuesta o a descubrir patrones.
Decide qué tipo de aprendizaje corresponde.

Recuerda: la pista más importante no es el problema que resuelve el sistema, sino la información con la que aprende.


### ChatGPT
LLM(Large Language Models) -> Intenta predecir la siguiente palabra. Si ingresamos 3 palabras y muestra una 4ta palabra. Lo hace por medio de la ventana de contexto(en los modelos actuales estas ventanas son de miles de tokens).

La parte de pasar de palabras a tokens en un aprendizaje automático no superviasdo. 
Aprendizaje por refuerzo: Cuando nos hace elegir la mejor respuesta entre dos opciones. 


## Modelos Principales
Vamos a aprender un grupo seleccionado de modelos que son la base de la mayoría de modelos utilizados en la actualidad.
- KNN: Clasificación y regresión
- SVM: Clasificación y regresión
- Árboles de decisión: Clasificación y regresión
- Redes neuronales:
- Agrupamiento Jerárquico:
- k-means:
- DBSCAN: 

## Métricas
- Estudiar cómo se mide una distancia entre dos puntos: sqrt((x1-x2)^2+(y1-y2)^2)
En tres dimensiones: sqrt((x1-x2)^2+(y1-y2)^2+ (z1-z2)^2)

Para R^n
d(x,y)= sqrt(sumatoria desde i = 1 hasta n (xi-yi)^2)
Averiguar como se mide la distancia si no se puede ir en línea recta, por ejemplo, de un punto a a un punto b en una ciudad donde hay varios edificios(Distancia Manhattan/distancia 1).

La distancia 3 es lo mismo que la distancia 2 pero con un grado mayor de exponente. Pasa lo mismo con distancias mayores.

REVISAR EL RESUMEN DE CLASE PARA TENER LAS FÓRMULAS(Solo usaremos d1 y d2).
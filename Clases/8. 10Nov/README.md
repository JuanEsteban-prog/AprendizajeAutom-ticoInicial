## Aprendizaje no supervisado

A diferencia del aprendizaje supervisado, en el aprendizaje no supervisado trabajamos sin etiquetas(Es decir, tenemos la tabla de atributos X, pero no existe una columna respuesta y).

- Analogía de la clase(Profesor Oak): Imagina que se pierden las etiquetas de los «Tipos» de Pokémon (Fuego, Agua, Planta) y solo te quedan sus estadísticas numéricas (Ataque, Defensa, Velocidad). El objetivo del aprendizaje no supervisado es descubrir patrones ocultos por sí solo para agrupar a Charizard y Blastoise en clústeres distintos basándose únicamente en la similitud de sus atributos numéricos.

- Conceptos clave y aplicaciones: Además de agrupar datos mediante algoritmos como K-Means, Clusterización jerárquica, DBSCAN y Modelos de mezclas gaussianas, sirve para identificar ruido en los datos y realizar detección de anomalías (encontrar puntos atípicos que no encajan en ningún grupo normal, como fraudes bancarios o fallos técnicos).

### Tipos principales de agrupamiento(Clustering)

- Agrupamiento Exclusivo(Particional): Cada dato pertenece única y exclusivamente a un solo grupo, no hay puntos intermedios. Ejemplo: k-means.

- Agrupamiento con superposición(Difuso o Probabilístico): Un mismo dato puede pertenecer a múltiples grupos al mismo tiempo con diferentes grados de pertenencia o probabilidades(ej. 70% grupo A y 30% grupo B). Ejemplo: Clustering difuso o Modelos de Mezclas Gaussianas.

- Agrupamiento Jerárquico: En lugar de hacer una sola partición fija, organiza los datos en una estructura de árbol donde los grupos más pequeños se van fucionando(o dividiendo) paso a paso. Ejemplo: Dendogramas.

#### Preguntas importantes de la clase

- **¿Cuál es la diferencia entre agrupamiento jerárquico y exclusivo?:** El exclusivo divide los datos en k grupos planos y separados de una sola vez (cada dato va a una sola caja), mientras que el jerárquico crea un árbol de relaciones anidadas (dendrograma) que permite ver cómo se relacionan los datos a distintos niveles de granularidad sin obligarte a fijar un único número de grupos desde el principio.

- **¿Cuándo es preferible usar un modelo probabilístico frente a K-Means?:** Cuando las fronteras entre los grupos no están claramente separadas (hay solapamiento), cuando los clústeres tienen formas alargadas o elípticas de distinto tamaño (K-Means asume grupos esféricos), o cuando necesitas saber qué tan seguro está el modelo de que un dato pertenezca a un grupo.

- **¿Qué limitaciones tiene el agrupamiento con superposición en aplicaciones reales?:** Es computacionalmente más costoso, sus resultados pueden ser más difíciles de interpretar al tomar decisiones de negocio (donde a veces necesitas una categoría definitiva y no porcentajes), y es sensible al ruido o valores atípicos.

### Efecto de la normalización en la clusterización

- Como los algoritmos de agrupamiento miden distancias matemáticas entre puntos para saber quién se parece a quién, si un atributo tiene números grandes (ej. salario en miles) y otro números pequeños (ej. edad), el atributo más grande dominará toda la distancia y deformará los grupos.

- En clase se compararon técnicas como StandardScaler (media 0, varianza 1), MinMaxScaler (escala entre 0 y 1), Normalizer (escala cada fila a longitud unitaria) y RobustScaler (usa mediana y rango intercuartílico para resistir valores atípicos) para observar visualmente cuál separa mejor los clústeres en 2D.

## Preguntas de cierre
**Verficación de aprendizaje**
1. ¿En qué se diferencia la pertenencia exclusiva de la pertenencia con superposición? ¿Puede un método jerárquico producir grupos exclusivos?
    - Exclusiva vs. superposición: En la pertenencia exclusiva, cada dato pertenece única y exclusivamente a un solo grupo (como ocurre en k-Means). En la pertenencia con superposición, un mismo dato puede pertenecer a múltiples grupos simultáneamente con distintos grados de pertenencia o probabilidades (como en el clustering difuso).
    - ¿Puede un método jerárquico producir grupos exclusivos? Sí. Aunque el agrupamiento jerárquico organiza los datos en una estructura de árbol anidado (dendrograma), en el momento en que haces un corte horizontal a un nivel de detalle específico, cada dato queda asignado de forma exclusiva a una única rama o clúster.

2. En el ejemplo del cuaderno, ¿qué asignaciones de k-means cambian, si las hay, al transformar los datos y cómo explicarías esas diferencias?
    - Datos originales (sin escalar): Como la Característica 2 está multiplicada por 10, su escala domina por completo las distancias euclídeas y k-Means divide los datos con un corte horizontal (arriba vs. abajo), asignando mal los puntos de la frontera central.
    - Con StandardScaler y MinMaxScaler: Las asignaciones en la zona central cambian y el corte pasa a ser diagonal, separando correctamente las dos nubes reales. Esto ocurre porque ambos métodos transforman cada característica (columna) por separado, dejándolas en escalas comparables.
    - Con Normalizer: Las asignaciones cambian por completo y deforman la estructura original, porque Normalizer transforma cada observación (fila) de forma individual (proyectando los puntos sobre un círculo unitario), alterando las distancias reales entre las nubes.

**Preguntas de investigación**
1. En un caso real de agrupamiento sin etiquetas, ¿qué variables y decisiones de escalado podrían cambiar la interpretación de los grupos y por qué?
    - Selección de variables: Incluir identificadores (como un ID de cliente), códigos arbitrarios o variables irrelevantes distorsiona los clústeres, ya que los algoritmos de distancia los tratan como magnitudes numéricas reales. Asimismo, mezclar variables con unidades muy distintas (por ejemplo, ingresos anuales en miles frente a años de edad) hace que la variable de mayor magnitud defina por sí sola los grupos.
    - Decisiones de escalado:
      - No escalar provoca que los grupos se interpreten casi únicamente en función de la variable con mayor rango numérico
      - Usar StandardScaler o MinMaxScaler frente a RobustScaler: Si existen valores atípicos extremos (outliers), MinMaxScaler y StandardScaler se ven afectados por esos extremos y aplastan al resto de los datos, mientras que RobustScaler preserva mejor la separación real al basarse en la mediana y los cuartiles.
      - Usar Normalizer (por filas): Cambia por completo la interpretación de los grupos, pasando de agrupar por magnitud absoluta (cuánto gasta un cliente) a agrupar por proporción relativa (en qué porcentajes distribuye su gasto).

2. 
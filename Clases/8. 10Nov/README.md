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

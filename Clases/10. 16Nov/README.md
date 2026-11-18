## Agrupamiento K-means
El algoritmo k-Means divide un conjunto de observaciones numéricas en exactamente $k$ grupos (clústeres).
- La analogía de clase (Centros Pokémon): Imagina que eres el planificador urbano de Kanto y tienes presupuesto para construir exactamente $k = 3$ Centros Pokémon. Tu objetivo es ubicarlos en el mapa de forma que la distancia total que deben caminar todos los entrenadores hasta su Centro más cercano sea la menor posible
- Objetivo matemático (Minimizar la Inercia): Busca minimizar la suma de las distancias euclídeas al cuadrado entre cada observación y el centroide de su respectivo grupo (métrica conocida como inercia).
- Objetivo matemático (Minimizar la Inercia): Busca minimizar la suma de las distancias euclídeas al cuadrado entre cada observación y el centroide de su respectivo grupo (métrica conocida como inercia).

### Funcionamiento paso a paso
Recibe como entrada los datos $D$ y el número de clústeres $k$ que tú defines de antemano:

1. **Inicialización:** Se crean $k$ clústeres vacíos $P \leftarrow \{p_1, p_2, \dots, p_k\}$ y se ubican los $k$ centroides iniciales $\zeta_1, \zeta_2, \dots, \zeta_k$.
2. **Ciclo repetitivo (`mientras` no se cumpla la condición de parada):**
   * **Fase de asignación:** Se vacían los clústeres del turno anterior y, para cada punto $d_i \in D$, se mide su distancia a todos los centroides $d(d_i, \zeta_j)$ y se asigna el punto al clúster $p_j$ cuyo centroide le quede **más cerca** (distancia mínima).
   * **Fase de actualización:** Una vez que todos los puntos tienen grupo, se recalcula la posición de cada centroide $\zeta_i$ moviéndolo al **promedio exacto** de todos los puntos $d \in p_i$ que quedaron dentro de su grupo.
3. **Condición de parada:** Estos dos pasos (asignar puntos $\rightarrow$ mover centroides) se repiten una y otra vez hasta que los centroides dejan de moverse de forma apreciable (convergencia) o se alcanza un número máximo de iteraciones.

### Cómo elegir k
A diferencia del agrupamiento jerárquico, aquí tú debes decirle al algoritmo cuántos grupos ($k$) buscar:
- El engaño de la inercia: A medida que aumentas $k$ (por ejemplo, pasar de $k=3$ a $k=4$ o más), la inercia siempre disminuye, incluso cuando los grupos adicionales ya no tienen sentido práctico (un $k$ más alto no garantiza una mejor partición). 
- Criterios de selección: Se utiliza el método del codo (graficar la inercia para distintos valores de $k$ y buscar el punto donde la curva dobla y deja de bajar drásticamente), pero el profesor recalca que siempre debe contrastarse con el coeficiente de silueta, el tamaño de los grupos y si tienen una interpretación lógica para el problema.   


### Preguntas tipo entrevista
- Pregunta 1: «Aplicaste k-Means a datos de clientes y obtuviste 3 clústeres, pero visualmente los datos tienen formas alargadas y no circulares. ¿Por qué k-Means falla aquí y qué alternativas propondrías?»
    - Por qué falla: Porque k-Means asigna los puntos midiendo distancias euclídeas radiales desde un punto central (centroide), lo que asume implícitamente que los grupos son esféricos (circulares) y de tamaño similar. Al enfrentarse a formas alargadas o curvas, corta las formas por la mitad.
    - Alternativas: Usar algoritmos basados en densidad como DBSCAN, Agrupamiento Jerárquico o Modelos de Mezclas Gaussianas (GMM) (que permiten formas elípticas/alargadas).

- Pregunta 2: «Ejecuté k-Means 10 veces con los mismos datos y obtuve resultados ligeramente diferentes cada vez. ¿Por qué pasa y cómo lo solventas?»
    - Por qué pasa: Porque k-Means depende de dónde caigan los centroides iniciales al azar; distintas inicializaciones pueden hacer que el algoritmo converja a diferentes mínimos locales.
    - Cómo solventarlo:
        1. Fijar una semilla aleatoria (random_state en Python) para que los resultados sean reproducibles al comparar configuraciones.
        2. Probar múltiples inicializaciones automáticas (n_init en scikit-learn) para quedarse con la que logre menor inercia.
        3. Usar el método de inicialización inteligente k-means++ en lugar de random, el cual separa estratégicamente los centroides iniciales para mejorar la estabilidad y velocidad de convergencia.
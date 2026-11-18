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


## Preguntas Cierre
**Verificación De Aprendizaje**
1. ¿Cuáles son los pasos principales del algoritmo $k$-Means?

   - Inicialización: Definir el número de clústeres $k$, inicializar los grupos vacíos $P \leftarrow \{p_1, p_2, \dots, p_k\}$ y seleccionar los $k$ centroides iniciales $\zeta_1, \zeta_2, \dots, \zeta_k$.

   - Fase de asignación: Vaciar los clústeres del paso previo y asignar cada observación $d_i$ al clúster $p_j$ cuyo centroide $\zeta_j$ tenga la **distancia mínima** $d(d_i, \zeta_j)$.

   - Fase de actualización: Recalcular la posición de cada centroide $\zeta_i$ como el **promedio** exacto de todos los puntos asignados a su clúster $p_i$.

   - Condición de parada: Repetir iterativamente la asignación y la actualización hasta que los centroides dejen de cambiar de forma apreciable (convergencia) o se alcance el límite máximo de iteraciones.

2. ¿Qué significa minimizar la inercia en el contexto de $k$-Means y cómo se relaciona con la calidad del agrupamiento? 
    - Qué significa: Minimizar la suma de las distancias euclídeas al cuadrado entre cada observación y el centroide de su respectivo grupo.
    - Relación con la calidad: Una inercia baja indica que los grupos son internamente compactos (alta cohesión). Sin embargo, una menor inercia no garantiza por sí sola un mejor agrupamiento, ya que la inercia siempre disminuye al aumentar $k$, incluso cuando se fragmentan los datos en grupos artificiales que dejan de ser útiles (en el extremo, si $k = N$, la inercia es 0 pero el modelo no sirve).

3. ¿Cómo afecta la elección del valor de $k$ a los resultados del algoritmo y qué métodos existen para seleccionar un valor adecuado?
    - Efecto del valor de $k$: Un $k$ demasiado pequeño agrupa observaciones muy distintas en un mismo clúster (subajuste), mientras que un $k$ demasiado grande divide grupos naturales en fragmentos sin sentido práctico.
    - Métodos para seleccionarlo: Se utiliza el método del codo (graficar la inercia frente a $k$ y buscar el punto de inflexión donde la ganancia deja de ser fuerte) y debe contrastarse siempre con el coeficiente de silueta (que mide cohesión interna frente a separación entre grupos), el equilibrio en el tamaño de los clústeres y su interpretabilidad en el problema real. 

**Preguntas tipo entrevista**
1. Aplicaste $k$-Means a datos de clientes y obtuviste 3 clusters, pero visualmente los datos parecen tener formas alargadas y no circulares. ¿Por qué $k$-Means no funciona bien aquí y qué alternativas propondrías?
    - Por qué no funciona bien: Porque $k$-Means asigna puntos midiendo distancias euclídeas en línea recta hacia un único punto central (centroide). Esto crea fronteras de decisión lineales (diagramas de Voronoi) y asume implícitamente que los clústeres son esféricos (circulares/isotrópicos) y de varianza similar, haciendo que corte por la mitad las estructuras alargadas o curvas. 
    - Alternativas que propondría:
      - Modelos de Mezclas Gaussianas (GMM): Usan matrices de covarianza que se adaptan perfectamente a clústeres con formas elípticas o alargadas en cualquier orientación.   
      - DBSCAN: Agrupa por densidad de puntos contiguos, permitiendo descubrir clústeres de cualquier forma geométrica arbitraria o alargada e identificar ruido.   
      - Agrupamiento Jerárquico (con enlace simple o promedio) o aplicar primero una transformación (como PCA) si el alargamiento se debe a correlación lineal entre variables.   

2. Ejecuté $k$-Means 10 veces con los mismos datos y obtuve resultados ligeramente diferentes cada vez. ¿Cómo lo solventas?
Esto ocurre porque el algoritmo es sensible a la ubicación aleatoria de los centroides iniciales y puede converger a distintos mínimos locales de inercia. Lo solvento aplicando tres medidas:   
    - Usar inicialización `'k-means++'`: En lugar de elegir centroides iniciales completamente al azar (`'random'`), distribuye los centroides iniciales alejados entre sí para lograr convergencias más estables y consistentes.

    - Aumentar el número de inicializaciones (`n_init`): Ejecutar el algoritmo múltiples veces con diferentes semillas internas y conservar automáticamente la solución que obtenga la menor inercia final.

    - Fijar una semilla aleatoria (`random_state`): Garantiza resultados 100% reproducibles al comparar configuraciones o presentar el modelo.
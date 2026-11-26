# Clase 02
1. Cómo se representan los datos y qué es un modelo
    - **Los datos viven en $\mathbb{R}^n$:** Un conjunto de datos se representa como un subconjunto de $\mathbb{R}^n$, donde $n$ **es el número de variables o características** (la dimensión de cada observación, *no* la cantidad de filas).

    - **Forma matricial:** Si organizas los datos en una tabla o matriz $X \in \mathbb{R}^{m \times n}$, las $m$ **filas** son las observaciones (instancias) y las $n$ **columnas** son las variables.

    - **¿Qué es un modelo?:** Matemáticamente, un modelo es simplemente una **función** que recibe características de entrada y produce una salida.

2. Aprendizaje Supervisado vs No Supervisado

La diferencia clave no está en cómo se resuelve, sino en la información con la que aprende el modelo durante el entrenamiento.

    - Aprendizaje Supervisado:
      - Utiliza etiquetas(conoce la respuesta).
      - Ejemplos: Detección de spam, diagnóstico médico, precio de viviendas.
      - Riesgos: Replica sesgos de los datos(si entra basura, sale basura).
    - Aprendizaje No Supervisado:
      - Trabaja sin etiquetas(no conoce las respuestas).
      - Su objetivo es conocer patrones, similitudes o estructuras ocultas.
      - Ejemplos: Perfiles de clientes, recomendaciones musicales, detección de anomalías en máquinas.
      - Riesgo: No hay una respuesta correcta previa con la cúal podamos comparar.

3. Modelos principales
    - Aprendizaje supervisado: Clasificación y regresión -> k-NN, SVM y Árboles de decisión.
    - Aprendizaje No Supervisado: Agrupamiento -> Agrupamiento jerárquico, k-means, DBSCAN.
    - Aprendizaje Supervisado y Aprendizaje No Supervisado -> Redes neuronales.

4. Métricas de distancia
Para ver las fórmulas en acción, tomemos $x = (1, 2)$ y $y = (4, 6)$:

- **Manhattan ($d_1$):** Suma de diferencias absolutas (como caminar por cuadras sin atravesar edificios).

  $$d_1(x, y) = \sum_{i=1}^{n} |x_i - y_i|$$

  *Ejemplo:* $|1 - 4| + |2 - 6| = 3 + 4 = 7$.

- **Euclidiana ($d_2$):** Distancia en línea recta (Pitágoras generalizado). En forma matricial: $\sqrt{(x - y)^T(x - y)}$.

  $$d_2(x, y) = \sqrt{\sum_{i=1}^{n} (x_i - y_i)^2}$$

  *Ejemplo:* $\sqrt{(1 - 4)^2 + (2 - 6)^2} = \sqrt{9 + 16} = 5$. *(Ojo: tanto $d_1$ como $d_2$ cambian si modificas las unidades o escalas de tus variables).*

- **Minkowski ($d_p$):** Generaliza a las dos anteriores para cualquier $p \ge 1$. Con $p = 1$ obtienes Manhattan; con $p = 2$, Euclidiana. A mayor $p$, más peso se le da a la coordenada con mayor diferencia.

  $$d_p(x, y) = \left( \sum_{i=1}^{n} |x_i - y_i|^p \right)^{1/p}$$

  - **Mahalanobis ($d_M$):** Es una distancia euclidiana corregida por la inversa de la **matriz de covarianza** $S$ (simétrica y definida positiva).

  $$d_M(x, y) = \sqrt{(x - y)^T S^{-1} (x - y)}$$

  - **Utilidad:** Elimina el problema de las distintas escalas y toma en cuenta la **correlación** entre variables.
  - **Dos trampas de examen:** (1) Si $S$ es **singular** (no tiene inversa), no se puede calcular. (2) En problemas supervisados, $S$ debe estimarse **solo con los datos de entrenamiento** para evitar fuga de datos.

- **Hamming ($d_H$):** Cuenta en cuántas posiciones difieren dos vectores (útil para datos binarios o categóricos).

  $$d_H(x, y) = \sum_{i=1}^{n} \delta(x_i, y_i)$$

  *Ejemplo:* Entre $(1, 2)$ y $(4, 6)$ difieren en ambas posiciones $\implies d_H = 2$.

- **Disimilitud Coseno ($d_{\cos}$):** Mide la diferencia en **dirección (ángulo)** entre dos vectores no nulos, ignorando su magnitud.

  $$d_{\cos}(x, y) = 1 - \frac{x \cdot y}{\|x\|\|y\|}$$

  - **¡Fija de examen! NO es una métrica (ni pseudométrica):** Incumple la desigualdad triangular (contraejemplo: con $x = (1, 0)$, $y = (1, 1)$ y $z = (0, 1)$, se tiene $d(x, z) = 1 > 2 - \sqrt{2} = d(x, y) + d(y, z)$). Además, dos vectores distintos con la misma dirección dan disimilitud $0$, y no está definida para el vector nulo.

# Clase 03

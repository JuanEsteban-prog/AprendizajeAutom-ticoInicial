- ¿Cómo se puede evaluar modelos de clasificación multiclase?
Una forma es con la matriz de confusión. 
### Diametro del clúster/grupo
Mide la distancia máxima entre dos puntos dentro del mismo grupo.
### Inercia interna del clúster
Mide la cohesión interna de los clústeres, definida como la suma de las distancias cuadráticas entre cada punto y el centroide de su clúster.
La inercia es mejor que el diametro para medir la coherencia.
Cada clúster tiene su inercia.
### Cohesión de silueta
Mide la distancia promedio entre un putno y todos los demás puntos en el mismo clúster. 


Tenemos un escenario, que tipo de modelo aplicamos: supervisado o no supervisado
Tenemos este escenario, que vamos a priorizar, recall o precisión
Tengo esta matriz de confusión, cuanto vale el recall.

## Más para el exámen:
## 1. Validación Interna vs. Externa

* **Métricas de validación interna:** Evalúan la calidad de los clústeres usando **únicamente los datos y las distancias** (sin etiquetas), midiendo qué tan compactos y separados quedaron (Inercia, Silueta, Dunn, Davies-Bouldin).
* **Métricas de validación externa:** Se usan solo cuando **sí dispones de etiquetas reales de referencia** para comparar si tus clústeres coinciden con ellas (por ejemplo, el **Índice de Rand** o la **Información Mutua Ajustada**).

## 2. Bloques básicos: Cohesión y Separación

Antes de ver las métricas globales, necesitas entender las piezas que usan sus fórmulas para un clúster $C_i$ con centroide $\mu_i = \frac{1}{|C_i|} \sum_{x \in C_i} x$:

**Medidas de Cohesión (queremos que sean PEQUEÑAS):**

* **Diámetro del clúster ($\text{diam}(C_i)$):** Distancia máxima entre los dos puntos más lejanos dentro del mismo grupo:

$$\text{diam}(C_i) = \max_{x, y \in C_i} d(x, y)$$

* **Inercia ($I_i$):** Suma de distancias al cuadrado de cada punto a su centroide:

$$I_i = \sum_{x \in C_i} d(x, \mu_i)^2$$

* **Distancia promedio interna ($S_i$):** Distancia promedio de los puntos a su centroide:

$$S_i = \frac{1}{|C_i|} \sum_{x \in C_i} d(x, \mu_i)$$

* **Cohesión de Silueta ($a(x)$):** Distancia promedio de un punto $x$ hacia todos los demás puntos de **su propio clúster**:

$$a(x) = \frac{1}{|C_i| - 1} \sum_{y \in C_i} d(x, y)$$

**Medidas de Separación (queremos que sean GRANDES):**

* **Distancia entre clústeres ($d(C_i, C_j)$):** Distancia mínima entre los dos puntos más cercanos de dos grupos distintos:

$$d(C_i, C_j) = \min_{x \in C_i, y \in C_j} d(x, y)$$

* **Distancia entre centroides ($d_c(C_i, C_j)$):** Distancia directa entre los centros de dos grupos: $d(\mu_i, \mu_j)$.
* **Separación de Silueta ($b(x)$):** Distancia promedio de un punto $x$ hacia todos los puntos del **clúster vecino más cercano** al que no pertenece:

$$b(x) = \min_{j \neq i} \frac{1}{|C_j|} \sum_{y \in C_j} d(x, y)$$

## 3. Las 4 Métricas de Calidad Global

| Métrica | Fórmula | ¿Cómo leerla? | ¿Mejor alto o bajo? |
| :--- | :--- | :--- | :--- |
| **Inercia total** | $I_{\text{total}} = \sum_{i=1}^{k} I_i$ | Suma la dispersión interna de todos los grupos. Siempre disminuye al subir $k$. | **Más bajo** (buscando el codo) |
| **Índice de Davies-Bouldin ($DB$)** | $DB = \frac{1}{k} \sum_{i=1}^{k} \max_{j \neq i} \left( \frac{S_i + S_j}{d_c(C_i, C_j)} \right)$ | Divide la dispersión interna ($S_i + S_j$) entre la distancia de centroides. | **Más bajo** (cercano a $0$) |
| **Índice de Dunn** | $\text{Dunn} = \frac{\min_{i \neq j} d(C_i, C_j)}{\max_{1 \le l \le k} \text{diam}(C_l)}$ | Divide la **peor separación** (clústeres más pegados) entre el **peor diámetro** (clúster más ancho). | **Más alto** |
| **Índice de Silueta ($S$)** | $S = \frac{1}{\lvert D \rvert} \sum_{i=1}^{\lvert D \rvert} \frac{b(x_i) - a(x_i)}{\max\{a(x_i), b(x_i)\}}$ | Compara qué tan lejos está cada punto del grupo vecino ($b$) frente a su propio grupo ($a$). | **Más alto** (cercano a $1$) |

(Regla de oro del Resumen No. 5: Ninguna métrica sustituye el análisis del contexto; siempre deben interpretarse junto con el tamaño de los grupos, la escala y el significado de las variables).

## 4. Respuestas rápidas a las trampas de examen de esta clase

1. **¿Qué indica un Coeficiente de Silueta de $0.85$?**
   Indica una estructura de clústeres muy fuerte: los grupos son altamente compactos internamente ($a(x)$ es muy pequeño) y están muy bien separados entre sí ($b(x)$ es grande).

2. **¿Qué pasa con la inercia si aumentamos $K$ hasta $K = N$ (un clúster por dato)?**
   La inercia disminuye progresivamente hasta llegar exactamente a $0$, porque cada dato coincide con su propio centroide.

3. **¿Cuál es el coeficiente de silueta si solo existe un único clúster ($K = 1$)?**
   **No está definido** (no se puede calcular), porque no existe ningún clúster vecino para calcular la separación $b(x)$. La silueta media requiere estrictamente **al menos 2 grupos y menos grupos que observaciones ($2 \le k < N$)**. (Además, si un grupo individual tiene un solo elemento, su silueta se toma como $0$).

4. **En alta dimensionalidad, ¿es confiable el Coeficiente de Silueta?**
   Pierde confiabilidad debido a la *maldición de la dimensionalidad*: en espacios con muchas variables, las distancias euclídeas entre todos los puntos tienden a volverse muy similares, haciendo que $a(x)$ y $b(x)$ se parezcan y la silueta se acerque a $0$. En esos casos conviene reducir dimensionalidad primero (ej. con PCA) o usar distancias como la de coseno.
   
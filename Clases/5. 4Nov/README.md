## Modelos de clasificación
- Modelo de clasificación binario


Hay que recordar la tabla de contingencia. 
- Número de positivos: Los que realmente valen 1.

- Número de negativos: Los que realmente valen 0.

- Verdaderos positivos: La predicción vale 1 y el valor real vale 1.

- Verdaderos negativos: La predicción vale 0 y el valor real vale 0.

- Falsos positivos: La predicción vale 1 y el valor real vale 0. 

- Falsos negativos: La predicción vale 0 y el valor real vale 1. 

Palabras importantes:
**Exactitud:** Medimos que tan exacto es nuestro modelo.  

**Error:** Medimos en cuanto se equivoca. 

**Presición:** Medimos la confianza de nuestro modelo, medimos cuanto son 1/la cantida de 1 que predijo el modelo. 

**Sensibilidad(Tasa de verdaderos positivos):** Medimos cuantos 1 predice el modelo/ para cuantos 1 realmente tiene el modelo.

**Presición y sensibilidad son dos factores que siempre vamos a utilizar**

### Precisión
Es la proporción de instancias clasificadas como positivas que son realmente positivas. Se prioriza cuando el costo de un Falso Positivo es alto. Cuando es más perjudicial generar falsas alarmas, como bloquear operaciones legítimas o contactar a personas que no están interesadas en un producto.

### Sensibilidad/recall
Proporción de instancias positivas que fueron correctamente identificadas. Cuando es más grave dejar escapar un caso positivo real, como un paciente enfermo, una amenaza de seguridad o una vulnerabilidad crítica.

### Puntuación F1
Es una medida que nos ayuda a convinar la presición con la sensiblidad. 


### La curva ROC


## Modelos de regresión
Asumimos que los datos son continuos, por lo tanto la realidad y la predicción pueden ser operadas.
- Error Absoluto Medio(MAE): Es la media
- Error Cuadrático Medio(MSE): Es la misma fórmula que con MAE pero elevamos al cuadrado, esto lo hace más preciso.
- Raíz del error cuadrático medio(RMSE): 
- Coeficiente de determinación(R^2): 

Este tipo de errores siempre tienen que ser interpretados en base a nuestros datos. 


## Más para el exámen:
1. Modelos de clasificación Binaria 
2. Cuando tu modelo predice dos clases ($0$ o $1$), el punto de partida es la **Matriz de Confusión**, que cruza lo que ocurrió en la realidad contra lo que predijo tu modelo:

| | Predicción: 1 (Positivo) | Predicción: 0 (Negativo) |
| :--- | :--- | :--- |
| **Real: 1 (Positivo)** | **TP** (Verdadero Positivo) | **FN** (Falso Negativo) |
| **Real: 0 (Negativo)** | **FP** (Falso Positivo) | **TN** (Verdadero Negativo) |

### Fórmulas clave derivadas de la matriz

* **Exactitud (*Accuracy*):** Proporción total de aciertos sobre todos los datos ($|D| = TP + TN + FP + FN$):

$$\text{acc} = \frac{TP + TN}{|D|}$$

(Trampa de examen: Un Accuracy del 95% **no** garantiza un buen modelo si las clases están desbalanceadas; por ejemplo, si el 95% de los correos no son spam, un modelo que siempre diga «no spam» sacaría 95% sin detectar un solo fraude o spam).

* **Error:** Proporción de equivocaciones totales:

$$\text{err} = \frac{FP + FN}{|D|}$$

* **Precisión (*Precision*):** De todos los que el modelo marcó como positivos, ¿cuántos lo eran realmente?

$$\text{pre} = \frac{TP}{TP + FP}$$

* **Sensibilidad (*Recall* o *TPR*):** De todos los positivos reales que existen, ¿cuántos logró atrapar el modelo?

$$\text{rec} = \text{tpr} = \frac{TP}{TP + FN}$$

* **Especificidad (*TNR*):** Proporción de negativos reales bien clasificados: $\frac{TN}{TN + FP}$.
* **Tasa de Falsos Positivos (*FPR*):** Proporción de negativos reales marcados por error como positivos: $\frac{FP}{TN + FP}$.

* **Puntuación F1 (*F1-Score*):** Media armónica que equilibra precisión y sensibilidad:

$$F_1 = 2 \cdot \frac{\text{pre} \cdot \text{rec}}{\text{pre} + \text{rec}}$$

### ¿Cuándo priorizar Precisión vs. Sensibilidad?

* **Prioriza Precisión** cuando el costo de un **Falso Positivo ($FP$)** es muy alto. *Ejemplo de clase:* Un filtro de spam corporativo, donde mandar un correo importante de trabajo a spam ($FP$) es grave, aunque eso signifique dejar pasar algunos correos basura ($FN$).
* **Prioriza Sensibilidad (*Recall*)** cuando el costo de un **Falso Negativo ($FN$)** es muy alto. *Ejemplo de clase:* Diagnóstico de una enfermedad grave o detección de fraudes, donde dejar ir a un enfermo diciéndole que está sano ($FN$) puede ser fatal, aunque haya que hacer más pruebas a sanos ($FP$).

### Curva ROC y AUC

Si tu modelo devuelve probabilidades $\hat{f}(x) \in [0, 1]$, tú decides un **umbral $\theta$** (si la probabilidad es $\ge \theta$, predices $1$; si es menor, predices $0$).

* **Curva ROC:** Grafica los pares $(\text{fpr}_\theta, \text{tpr}_\theta)$ al ir moviendo el umbral $\theta$ entre $0$ y $1$.
* **AUC (*Area Under the Curve*):** Es el área bajo la curva ROC. Un **AUC = 1** es un modelo perfecto y un **AUC = 0.5** equivale a adivinar al azar.
  * **Rangos de interpretación:** $[0.97, 1.00)$ Excelente; $[0.90, 0.97)$ Muy bueno; $[0.75, 0.90)$ Bueno; $[0.60, 0.75)$ Regular; $[0.50, 0.60)$ Malo.

## 2. Modelos de Regresión

Aquí la variable objetivo es continua ($y_i = f(x_i)$) y la predicción es $\hat{f}(x_i)$:

| Métrica | Fórmula | Cómo entenderla |
| :--- | :--- | :--- |
| **MAE** (Error Absoluto Medio) | $\text{MAE} = \frac{1}{\lvert D \rvert} \sum_{i=1}^{n} \lvert \hat{f}(x_i) - f(x_i) \rvert$ | Promedio de los errores sin signo. Queda en las **mismas unidades** que $y$. |
| **MSE** (Error Cuadrático Medio) | $\text{MSE} = \frac{1}{\lvert D \rvert} \sum_{i=1}^{n} (\hat{f}(x_i) - f(x_i))^2$ | Al elevar al cuadrado, **penaliza mucho más los errores grandes** que el MAE. Queda en **unidades cuadradas**. |
| **RMSE** (Raíz del MSE) | $\text{RMSE} = \sqrt{\text{MSE}}$ | Devuelve el MSE a las **unidades originales** de la variable objetivo. |
| $R^2$ (Coeficiente de determinación) | $R^2 = 1 - \frac{\sum (\hat{f}(x_i) - f(x_i))^2}{\sum (f(x_i) - \bar{y})^2}$ | Mide qué proporción de la varianza de los datos explica tu modelo frente a predecir siempre el promedio $\bar{y}$. |

(Experimento clave de la clase: Si multiplicas tanto los valores reales como los predichos por $10$, el **MAE** y el **RMSE** se multiplican por $10$, mientras que el **MSE** se multiplica por $10^2 = 100$).

## 3. Modelos de Agrupamiento (Resumen de métricas)

El Resumen No. 5 también incluye las 4 métricas principales para evaluar clústeres sin etiquetas:

* **Inercia total ($I_{\text{total}}$):** Suma de las distancias al cuadrado de cada punto a su centroide $\mu_i$. Siempre baja al aumentar $k$.
* **Índice de Davies-Bouldin ($DB$):** Relaciona qué tan dispersos son los clústeres internamente ($S_i + S_j$) dividido para la distancia entre sus centroides $d_c(C_i, C_j)$. *(Mientras más bajo, mejor)*.
* **Índice de Dunn:** Divide la distancia mínima entre clústeres distintos para el diámetro máximo interno de cualquier clúster. *(Mientras más alto, mejor)*.
* **Índice de Silueta ($S$):** Compara para cada punto su cohesión interna $a(x_i)$ (distancia promedio a su propio grupo) contra su separación $b(x_i)$ (distancia promedio al grupo vecino más cercano): $\frac{b(x_i) - a(x_i)}{\max\{a(x_i), b(x_i)\}}$. (Mientras más cercano a $1$, mejor; si un grupo tiene un solo elemento, su silueta es $0$).
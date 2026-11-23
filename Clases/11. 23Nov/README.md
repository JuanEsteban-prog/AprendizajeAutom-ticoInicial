## Métodos Supervisado
### Overfitting (Sobreajuste)

También conocido como **sobreajuste**, ocurre cuando un modelo aprende demasiado bien los datos de entrenamiento, incluyendo el ruido y las particularidades específicas de estos.

Como consecuencia, obtiene un rendimiento muy bueno en los datos de entrenamiento, pero presenta un rendimiento considerablemente peor en los datos de prueba o en datos nuevos.

**Causa principal:** el modelo es demasiado complejo o ha aprendido demasiado de los datos de entrenamiento.

### Underfitting (Subajuste)

También conocido como **subajuste**, ocurre cuando un modelo no logra aprender adecuadamente los patrones y relaciones presentes en los datos de entrenamiento.

Como consecuencia, presenta un rendimiento deficiente tanto en los datos de entrenamiento como en los datos de prueba.

**Causa principal:** el modelo es demasiado simple o no ha sido entrenado lo suficiente.


### Generalization (Generalización)

También conocido como **capacidad de generalización**, es la capacidad de un modelo para aplicar lo aprendido durante el entrenamiento a datos nuevos que no ha visto anteriormente.

Un modelo tiene una buena capacidad de generalización cuando obtiene resultados similares en los datos de entrenamiento y en los datos de prueba.

**Objetivo principal:** conseguir que el modelo aprenda patrones relevantes y pueda realizar predicciones precisas sobre datos desconocidos.

### Comparación rápida

| Concepto | Entrenamiento | Prueba |
|---|---|---|
| Overfitting | Rendimiento muy bueno | Rendimiento malo |
| Underfitting | Rendimiento malo | Rendimiento malo |
| Buena generalización | Rendimiento bueno | Rendimiento bueno |

**En resumen:**
- **Overfitting:** el modelo memoriza demasiado.
- **Underfitting:** el modelo no aprende lo suficiente.
- **Generalization:** el modelo aprende patrones que puede aplicar a datos nuevos.

## Distintos algoritmos
1. K-Nearest-neighbors: Es un algoritmo de aprendizaje automático supervisado. Se pueden utilizar tanto para problemas de clasificación cómo de regresión. 
    - Hiperparámetros:
        - k: La disnicia que queremos que tengan los grupos entre sí.
        - Una forma de ver la medida de los valores de la distncia se podría ocupar el promedio, al igual que a moda y la mediana.
        - Para hacer que el valor que más cerca está del punto aporte más podemos hacer un promedio ponderado.


Una de las primeras cosas que tenemos que hacer es ver que tan bueno es el modelo durante el entrenamiento. Para hacerlo tenemos que comparar los predichos con las métricas de entrenamiento.


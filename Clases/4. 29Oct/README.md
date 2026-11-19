## Libreria Panda
Es utilizada para manegar dataframes. 
## Libreria Sklearn
[Documentación en Línea](https://scikit-learn.org/stable/)

- Matriz sparse: Matriz que tiene muchos 0 (En binario)

**Estudiar PCA en datos, que forma tiene que tener los daots para tener un buen/eficiente PCA?**

El modelo de aprendizaje automático más sencillo es el de regresión lineal. 

[Ejercicio Visto En Clase](https://colab.research.google.com/github/andres-merino/AprendizajeAutomaticoInicial-05-N0105/blob/main/2-Notebooks/04-Mi-primer-modelo.ipynb#scrollTo=5i0SaiFY3U1L)

[Hacer nuestro primer modelo/Actividad no evaluable](https://andres-merino.github.io/AprendizajeAutomaticoInicial-05-N0105/2-Clases/Clase04.pdf)



## Más para el exámen
1. Las 7 etapas del flujo de trabajo supervisado:
    1. Definición del problema.
    2. Elección de características (X) y variable objetivo (y)(por ejemplo, en el taller de viviendas, predecir price a partir de bedrooms, bathrooms, sqft_living, sqft_lot y floors).
    3. División de los datos: Separar en entrenamiento y prueba (y usar un conjunto de validación si vas a comparar alternativas para elegir un modelo, reservando prueba solo para la evaluación final).
    4. Preparación / Preprocesamiento (cuando sea necesaria): Ajustar siempre las transformaciones únicamente con los datos de entrenamiento.
    5. Entrenamiento: Estimar los coeficientes del modelo usando los datos de entrenamiento.
    6. Predicción: Generar las predicciones sobre los datos separados.   
    7. Evaluación: Medir el error en los datos de prueba.   
2. Métodos clave en 'scikit-learn'
- fit(): Aprende parámetros a partir de los datos de entrenamiento. Es un escalador aprende medias/desviaciones; en un modelo de regresión lineal estima sus coeficientes.
- transform(): Aplica una transformación de preprocesamiento usando los paramétros que ya se aprendieron con fit().
- predict(): Utiliza el modelo ya entrenado para calcular los valores predichos \(\hat{y}\) a partir de nuevas características (X).
3. Error cuadrático medio
Para evaluar el desempeño de la regresión lineal en los datos de prueba se calcula el **MSE** (*Mean Squared Error*):

$$\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$

* Donde $y_i$ es el valor real, $\hat{y}_i$ es el valor predicho por el modelo y $n$ es la cantidad de observaciones en el conjunto de prueba.
* **Interpretación clave:** El MSE siempre se expresa en **unidades cuadradas de la variable objetivo** (por ejemplo, si predices `price` en dólares, el MSE está en *dólares al cuadrado*).
* **Cuidado práctico:** Un valor aislado de MSE **no permite declarar por sí solo que un modelo es bueno**; siempre necesita contexto o comparación.


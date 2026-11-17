## Distancia de Hamming
Cuenta el número de posiciones en la que los elementos correspondientes son diferentes.

## Dismilitud coseno

## Verficación de Aprendizaje:
1. ¿Cúal es la diferencia fundamental entre el aprendizaje supervisado y no supervisado?

   El **aprendizaje supervisado** consiste en entrenar un modelo utilizando datos etiquetados, es decir, datos que incluyen tanto la información de entrada como la respuesta correcta. De esta manera, el modelo aprende a identificar patrones para realizar predicciones o clasificar nuevos datos.

    En cambio, el **aprendizaje no supervisado** utiliza datos sin etiquetar. El modelo analiza la información por sí mismo para encontrar patrones, similitudes, diferencias o grupos dentro de los datos, sin contar con respuestas correctas previamente definidas.

2. ¿Qué tipo de problemas se resuelven con aprendizaje supervisado y cúales con el no supervisado?

   **Aprendizaje supervisado:** se utiliza para resolver problemas de clasificación y predicción. Por ejemplo, identificar si un correo electrónico es spam o no, predecir el precio de una vivienda o determinar si un paciente tiene una enfermedad a partir de ciertos datos.

   **Aprendizaje no supervisado:** se utiliza para descubrir patrones, agrupar datos similares y encontrar relaciones que no son evidentes a simple vista. Por ejemplo, segmentar clientes según sus hábitos de compra, agrupar noticias por temas o detectar comportamientos inusuales en transacciones.

En resumen, la diferencia principal es que el aprendizaje supervisado aprende a partir de ejemplos con respuestas conocidas, mientras que el no supervisado busca patrones y estructuras en datos que no tienen etiquetas.

## Normalización/Escalado de datos
Cuando tenemos varias variables estas deberian de estar en el mismo intervalo, se puede hacer por los siguientes métodos:
- Normlaización por el máximo:

- Normalización Min-Max: Se distribuyen los datos en todo el intervalo. Va a existir el valor de 0 y también lo hará el valor de 1. 

- Estandarización(Z-score): 

## Discretización de datos(También nos sirve para transformar nuestros datos)
En algunas situaciones es más conveniente que la normalización/escalado de datos.
- Discretización por igual amplitud: Primero tenemos que elegir cuantos grupos queremos hacer(k-intervalos), para después determinar el tamaño del intervalo. 

- Discretización por igual frecuencia: 

## Datos categóricos
- Codificación One-Hot: 
Si nuestras variables predictorsa están muy correlacionadas puede afectar al modelo, por lo que no metemos la última variable y detectamos la variable faltante cuando hace falta las otras dos variables. SIEMPRE HAY QUE ELIMINAR UNA CATEGORIA(La que queramos).

## Conjunto de datos
Una matriz m x n puede representar un conjunto de datos. Cuando m(filas) y n(columnas) son muy grandes, el computador puede dar problemas procesando los datos, por lo que tendremos que sacrificar/reducir la m o n.

Lo recomendable es siempre tener que **m>>10n** Tenemos que tener 10 veces más datos que columnas. 

Para eliminar una m tenemos que hacer un submuestro(esto es permitido siempre que tengamos suficientes datos). 

Para eliminar n tenemos que determinar la correlación, eliminamos las n que estén más correlacionadas(De esta forma estamos eliminando el ruido). Otra forma de reducir n es realizar un analisis de componentes principales(Nos indica que transmformaciones podemos hacer para reducir las dimensiones de nuestros datos).

## Proceso de análsis de datos (Resolución de problemas)
1. Entendimiento del negocio(Entender el contexto)
2. Entender las variables/datos
3. Limpieza y depuración de los datos: Para hacer esto tenemos que realizar un análisis exploratorio inicial(Ir viendo la media, la varianza y los outliers de los datos) y luego se obtiene un análisis final de nuestros datos listos.
4. Preprocesado de datos
5. Separación de datos: De todo el conjunto de datos los separamos, nos quedamos con unos, le datos los otros datos al modelo cuando este nos de una salida le damos los datos que no ha visto el modelo(los datos que nos quedamos anteriormente), de esta forma nos podemos asegurar que los modelos no se memoricen las respuestas.
6. Entrenar Modelo
7. Evaluación/Validación del modelo: Logramos determinar que tan bueno o malo son las salidas de nuestro modelo. 

En análisis de datos tosdos estos procesos son iterativos(Desde el punto 4 al 7). 

### Separación de datos
Se suele tomar el 20% para la prueba y el 80% para el entrenamiento, esto se hace de forma aleatoria. 

Esto depende de varios factores ya que entre más datos tengamos para entrenar más preciso es el modelo, pero también tenemos que tener la suficiente cantidad de datos para hacer la prueba, ya que de esta forma nos aseguramos que el modelo no se está aprendiendo las respuestas.


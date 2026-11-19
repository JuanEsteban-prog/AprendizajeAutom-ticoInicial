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

## Más por el exámen
## 1. Partición de datos y la regla de oro (`fit` vs. `transform`)

Antes de tocar o transformar tus datos en un problema supervisado, debes dividirlos en tres conjuntos con roles distintos:

* **Entrenamiento (*Train*):** Sirve para ajustar el modelo y aprender los parámetros de las transformaciones.
* **Validación (*Validation*):** Sirve para tomar decisiones (como elegir modelos o hiperparámetros).
* **Prueba (*Test*):** Se guarda intacto únicamente para la evaluación final.

**Cómo evitar la fuga de información en Python:**
Debes aprender las medias, desviaciones, mínimos, máximos, categorías y límites de intervalos **únicamente con el conjunto de entrenamiento**. Luego aplicas esos mismos parámetros ya aprendidos a validación y prueba:

* `fit()` **aprende** los parámetros (se usa **solo** en entrenamiento).
* `transform()` **aplica** la transformación (se usa en entrenamiento, validación y prueba sin volver a ajustar).

*(Nota práctica: Al particionar, la **estratificación** conviene en problemas de clasificación para mantener la proporción de clases, pero no se aplica directamente sobre una variable objetivo continua como el precio de una casa).*

## 2. Normalización y Estandarización (Fórmulas y trampas)

Antes de aplicar cualquiera de estas fórmulas, debes identificar si existen **variables constantes** (donde todos los valores son iguales), ya que provocan divisiones para cero.

| Técnica | Fórmula | Qué logra y sus límites clave |
| :--- | :--- | :--- |
| **Normalización por el máximo** | $x'_i = \frac{x_i}{\max(X)}$ | Requiere $\max(X) \neq 0$. No equivale a dividir por el máximo absoluto y, si hay valores negativos, no garantiza el rango $[0, 1]$. |
| **Normalización Min-Max** | $x'_i = \frac{x_i - \min(X)}{\max(X) - \min(X)}$ | Requiere un rango no nulo ($\max \neq \min$). Lleva los datos de entrenamiento a $[0, 1]$, pero es muy sensible a valores extremos (*outliers*). |
| **Estandarización (Z-score)** | $x'_i = \frac{x_i - \mu}{\sigma}$ | Requiere desviación estándar $\sigma \neq 0$. Deja los datos de ajuste con **media** $0$ y **varianza** $1$, pero **no fija un rango cerrado** ni convierte la distribución en una curva normal. |

**Comprobación clásica de examen (Min-Max con datos nuevos):**[cite: 7]
Si en entrenamiento tienes $\min = 10$ y $\max = 20$, y luego llega un dato nuevo de prueba con valor $25$, al aplicar la fórmula aprendida en entrenamiento obtienes:[cite: 7]

$$x' = \frac{25 - 10}{20 - 10} = \frac{15}{10} = 1.5$$[cite: 7]

## 3. Discretización de datos

Consiste en transformar una variable numérica continua en $k$ intervalos (categorías) cuando eso aporta una interpretación útil, asumiendo que habrá cierta pérdida de detalle:

* **Discretización de igual amplitud:** Divide el rango total en $k$ intervalos del mismo ancho matemático:

$$\mathrm{Tamano~del~intervalo} = \frac{\max(X) - \min(X)}{k}$$


* **Discretización de igual frecuencia:** Divide los datos en $k$ intervalos de modo que cada intervalo contenga aproximadamente la **misma cantidad de observaciones**. *(Advertencia: si hay muchos valores repetidos, puede ser imposible lograr frecuencias exactas).*

Al igual que el escalado, los límites de los intervalos se aprenden solo con entrenamiento y se debe definir cómo asignar valores nuevos que caigan fuera de esos bordes.

## 4. Datos Categóricos: Codificación One-Hot

Cuando tienes una variable categórica nominal con $m$ categorías distintas (por ejemplo, `Color` = `{Rojo, Verde, Azul}`), la **codificación One-Hot** transforma cada categoría en un vector binario de longitud $m$, poniendo un `1` en la columna correspondiente a su categoría y `0` en las demás:

* `Rojo` $\rightarrow$ `(1, 0, 0)`
* `Verde` $\rightarrow$ `(0, 1, 0)`
* `Azul` $\rightarrow$ `(0, 0, 1)`

**Reglas prácticas para recordar:**

* **Por qué se usa:** Permite representar categorías nominales sin inventar un orden falso entre ellas.
* **Trampa de entrevista:** No toda columna con números debe estandarizarse; los códigos numéricos de una categoría (como un código de provincia o un ID) **no son magnitudes** y no deben escalarse con Z-score o Min-Max.
* **Flujo correcto:** Las categorías válidas se aprenden solo con entrenamiento y debes definir de antemano cómo tratará el modelo a las categorías nuevas que aparezcan en prueba.
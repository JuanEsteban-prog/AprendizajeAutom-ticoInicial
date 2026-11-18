### Reducción De Dimensionalidad

Es importante reducir la dimensionalidad de un conjunto de datos al construir un modelo de aprendizaje automático y esto permite construir modelos más eficientes. Cuando trabajas con demasiadas variables (por ejemplo, un dataset con 1000 características y solo 100 muestras), los modelos sufren de sobreajuste, alto costo computacional y redundancia. Para solucionarlo existen dos enfoques distintos:

- **Selección de atributos:** Consiste en elegir un subconjunto de las variables originales más relevantes y descartar el resto sin transformarlas.
- **Extracción de características:** Consiste en transformar y combinar las variables originales para crear un conjunto más pequeño de nuevas variables (como hace PCA o SVD).

### Análisis De Componentes Principales (PCA)

PCA es un método de extracción de características diseñado para reducir la dimensionalidad de un conjunto de datos.

- **Funcionamiento y cargas:** Transforma las características originales en nuevas variables llamadas componentes principales, donde cada variable original aporta un peso o "carga" a cada componente.
- **Aclaración conceptual clave (pregunta de entrevista de la clase):** Si usas PCA para pasar de 100 características a 10 componentes principales, no significa que las 90 características descartadas no fueran importantes. Lo que se descarta son los componentes de menor varianza, pero cada uno de los 10 componentes retenidos sigue siendo una combinación que conserva la información de las 100 variables originales.

La utilidad de un **gráfico screen plot** en PCA es identificar cúantos componentes principales conviene conservar.

### Descomposición en valores singulares (SVD)

**El Teorema:** Cualquier matriz $A \in \mathbb{R}^{m \times n}$ de rango $r$ se puede descomponer de forma única como:

$$A = U\Sigma V^T$$

- **¿Qué representa cada matriz?**
  - $U \in \mathbb{R}^{m \times m}$: Es una matriz ortogonal cuyas columnas se llaman **vectores singulares izquierdos**. En el ejemplo práctico de la clase sobre películas y usuarios, relaciona a los **usuarios** con los conceptos o géneros latentes.
  - $\Sigma \in \mathbb{R}^{m \times n}$: Es una matriz diagonal con entradas no negativas ordenadas de manera decreciente ($\sigma_{11} \geq \sigma_{22} \geq \dots \geq 0$), llamadas **valores singulares** de $A$. Representan la fuerza o importancia de cada concepto.
  - $V \in \mathbb{R}^{n \times n}$ (o $V^T$): Es una matriz ortogonal cuyas columnas son los **vectores singulares derechos**. En el ejemplo práctico de clase, relaciona a las **películas** con esos mismos conceptos latentes.

- **¿Cómo se calculan? (Resumen de la demostración del profesor):**
  1. Se construye la matriz simétrica $A^T A$, la cual es diagonalizable con valores propios no negativos ($\lambda_{ii}$) y vectores propios ortonormales ($P$) tal que $A^T A = PDP^T$.
  2. Al igualar con $A^T A = (U\Sigma V^T)^T(U\Sigma V^T) = V\Sigma^T\Sigma V^T$, se deduce directamente que $V = P$ (los vectores singulares derechos son los vectores propios de $A^T A$).
  3. Los valores singulares en $\Sigma$ se obtienen sacando la raíz cuadrada de los valores propios de $A^T A$: $\sigma_{ii} = \sqrt{\lambda_{ii}}$.
  4. Finalmente, las columnas $u_i$ de la matriz $U$ se obtienen despejando $Av_i = \sigma_{ii}u_i$, lo que nos da la fórmula:

$$u_i = \frac{1}{\sigma_{ii}}Av_i$$


## Ejercicios cierre 
**Verficación de Aprendizaje**
1. Al reducir cuatro características a dos componentes con PCA, ¿qué información revisarías para decidir si la representación es suficiente?
Revisaría la varianza explicada acumulada (explained_variance_ratio_.cumsum()) de los dos primeros componentes principales. Si la suma de ambos retiene un porcentaje alto de la varianza total (por ejemplo, sobre el 85%–95%, como el 95.8% en el dataset Iris), la representación en 2D es suficiente porque conserva casi toda la información original.

2. ¿Qué diferencia hay entre conservar dos atributos originales y construir dos componentes principales?
  - Conservar dos atributos originales (Selección de atributos): Eliges 2 columnas de tu tabla tal como están y eliminas por completo las demás, perdiendo toda la información de las columnas descartadas.
  - Construir dos componentes principales (Extracción de características con PCA): Creas 2 variables nuevas que son combinaciones lineales de todas las variables originales, logrando resumir el aporte de todas las columnas en solo dos ejes no correlacionados.

3. Si conservas menos valores singulares al reconstruir una matriz, ¿qué esperas que ocurra con la información representada?
  - Se obtiene una matriz aproximada más comprimida (de menor rango) que conserva únicamente los patrones o conceptos globales más fuertes (asociados a los valores singulares más grandes) y descarta el ruido o los detalles secundarios, aunque aumenta el error de reconstrucción respecto a la matriz original.

4. En el ejemplo de preferencias (usuarios y películas), ¿qué representan $U$, $\Sigma$ y $V^T$?

  - $U$ (Vectores singulares izquierdos): Representa la relación o afinidad de los usuarios con los conceptos o géneros latentes (ocultos).
  - $\Sigma$ (Valores singulares): Es la matriz diagonal cuyos valores indican el peso, fuerza o importancia de cada concepto latente en el conjunto de datos (ordenados de mayor a menor).
  - $V^T$ (Vectores singulares derechos): Representa la relación o pertenencia de los ítems (películas) a esos mismos conceptos o géneros latentes.

**Preguntas tipo entrevista**
1. Tienes un dataset con 1000 características y solo 100 muestras. ¿Por qué esto es problemático y cómo usarías PCA para abordarlo? ¿Cuántos componentes principales deberías retener?
  - Por qué es problemático:** Tener muchas más columnas que filas ($p \gg n$) provoca la «maldición de la dimensionalidad», alta redundancia (multicolinealidad) y un sobreajuste (*overfitting*) severo, pues el modelo memoriza el ruido en lugar de generalizar.
  - Cómo abordarlo con PCA:** Estandarizaría las 1000 variables y aplicaría PCA para comprimirlas en un conjunto pequeño de componentes incorrelacionados que concentren la mayor varianza.
  - Cuántos componentes retener:** Matemáticamente, el límite máximo de componentes con varianza no nula que puede generar PCA es $\min(n - 1, p)$, es decir, como máximo 99 o 100 componentes (nunca más que el número de muestras). En la práctica, usando el gráfico de varianza explicada acumulada, retendría muchos menos (por ejemplo, entre 10 y 30 componentes) que expliquen ~90%–95% de la varianza.

2. Si PCA reduce las dimensiones de mi dataset de 100 a 10 características, ¿significa que las 90 características descartadas no eran importantes?
  - Falso. PCA no descarta 90 características originales; lo que descarta son los 90 componentes principales de menor varianza. Las 100 características originales siguen presentes y aportando información dentro de los 10 componentes retenidos a través de sus pesos o cargas (loadings).

**Preguntas de investigación**
1. ¿Qué precaución tomarías antes de aplicar e interpretar PCA sobre variables categóricas codificadas como números?
PCA calcula varianzas y distancias numéricas asumiendo variables continuas. Si codificas una categoría nominal con números arbitrarios (ej. Rojo = 1, Azul = 2, Verde = 3), PCA asumirá erróneamente que Verde es mayor que Rojo y que existe un orden y distancia real entre ellos, distorsionando las cargas. Precaución: No usar codificación numérica simple para categorías nominales en PCA; se debe usar codificación One-Hot (con cuidado de no escalar de forma que infle categorías raras) o, mejor aún, emplear alternativas diseñadas para datos categóricos como MCA (Multiple Correspondence Analysis) o FAMD (para datos mixtos).
2. ¿Cómo cambia la aproximación de una matriz de preferencias al conservar uno, dos o más valores singulares?
   - Con 1 valor singular ($k = 1$): La matriz reconstruida solo captura la tendencia más general y dominante del sistema (por ejemplo, el género más popular o el promedio global de calificaciones), dando una aproximación muy gruesa.

  - Con 2 o más valores singulares ($k = 2, 3, \dots$): Cada valor singular adicional incorpora un nuevo concepto o gusto secundario más específico, haciendo que la matriz aproximada sea cada vez más precisa y cercana a las preferencias reales de la matriz original $A$ (hasta que, si conservas todos los $r$ valores singulares, reconstruyes $A$ de forma exacta).

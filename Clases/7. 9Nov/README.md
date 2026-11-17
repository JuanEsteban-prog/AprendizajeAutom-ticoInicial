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

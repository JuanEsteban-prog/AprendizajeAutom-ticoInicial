## Algoritmo de Soporte Vectorial
Están enfocadas en hacer clasificación binaria cuando los grupos son linealmente seperables. Plantea encontrar un hiperplano en dos dimensiones de tal forma que todos los puntos queden de un lado y los otro lado, pero además que genere un margen(distancia del hiperplano hacia los vectores de soporte o hacia los vectores que se encuentran más cerca) más grande

Tenemos que encontrar la recta que mejor separa a los grupos, ya que usaremos este modelo para hacer predicciones.

Más sobre la clase:
[PDF usado en clase](https://andres-merino.github.io/AprendizajeAutomaticoInicial-05-N0105/2-Clases/Clase11.pdf)

[Resumen de clase donde se puede ver el problema alegraico resuelto paso por paso](https://andres-merino.github.io/AprendizajeAutomaticoInicial-05-N0105/2-Resumenes/Resumen11.pdf)

Al resolver este sistemas de ecuaciones logramos encontrar el mejor plano que divide al los datos.

No nos pedirá las fórmulas en el exámen pero si nos pedirá entender la teoría. 

[Documenación SVC](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html)


# Regularización en SVC (Support Vector Classifier)

En **SVC (Support Vector Classifier)**, el parámetro de regularización `C` controla qué tanto penaliza el modelo los errores de clasificación durante el entrenamiento.

En otras palabras, determina el equilibrio entre:

- Maximizar el margen de separación entre las clases.
- Minimizar los errores de clasificación en los datos de entrenamiento.

## 1. ¿Qué pasa cuando modificamos C?

### C pequeño (mayor regularización)

- Permite más errores de clasificación.
- Busca un margen de separación más amplio.
- Produce un modelo más sencillo.
- Reduce el riesgo de sobreajuste (*overfitting*).
- Puede generar subajuste (*underfitting*) si C es demasiado pequeño.

### C grande (menor regularización)

- Penaliza fuertemente los errores de clasificación.
- Intenta clasificar correctamente más puntos de entrenamiento.
- Busca un margen más ajustado.
- Puede generar un modelo más complejo.
- Aumenta el riesgo de sobreajuste (*overfitting*).

## 2. Comparación visual

| Característica | C pequeño | C grande |
|---|---|---|
| Regularización | Alta | Baja |
| Penalización de errores | Baja | Alta |
| Margen de separación | Amplio | Más estrecho |
| Errores permitidos | Más | Menos |
| Riesgo de underfitting | Mayor | Menor |
| Riesgo de overfitting | Menor | Mayor |

## 3. Ejemplo en Python

Podemos definir el parámetro `C` al crear un modelo SVC utilizando Scikit-learn:

```python
from sklearn.svm import SVC

modelo = SVC(C=1.0, kernel='rbf')
modelo.fit(X_train, y_train)
```

Podemos experimentar con diferentes valores de `C`:

| Valor de C | Comportamiento |
|---|---|
| 0.01 | Regularización alta |
| 0.1 | Regularización alta |
| 1 | Equilibrio inicial |
| 10 | Regularización baja |
| 100 | Regularización muy baja |

## 4. ¿Cómo elegir el mejor valor de C?

No existe un valor universal de `C` que funcione para todos los conjuntos de datos.

Una buena práctica es probar diferentes valores utilizando validación cruzada (*Cross Validation*) mediante `GridSearchCV`.

Ejemplo:

```python
from sklearn.svm import SVC
from sklearn.model_selection import GridSearchCV

parametros = {
    'C': [0.01, 0.1, 1, 10, 100],
    'kernel': ['linear', 'rbf'],
    'gamma': ['scale', 'auto']
}

modelo = GridSearchCV(
    SVC(),
    parametros,
    cv=5,
    scoring='accuracy'
)

modelo.fit(X_train, y_train)

print("Mejores parámetros:", modelo.best_params_)
print("Mejor accuracy:", modelo.best_score_)
```

## 5. Conclusión

El parámetro `C` controla el equilibrio entre el margen de separación y los errores de clasificación:

- **C pequeño:** el modelo prioriza un margen amplio, aunque permita algunos errores de clasificación.
- **C grande:** el modelo prioriza clasificar correctamente los datos de entrenamiento, aunque reduzca el margen.

Por lo tanto, elegir correctamente el valor de `C` permite encontrar un equilibrio entre el sobreajuste (*overfitting*) y el subajuste (*underfitting*), mejorando la capacidad de generalización del modelo.

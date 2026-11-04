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

**Sensibilidad(Tasa de verdaderos positivos):**Medimos cuantos 1 predice el modelo/ para cuantos 1 realmente tiene el modelo.

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



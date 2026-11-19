1. Considera el algoritmo de agrupamiento *k-means*.
**a)** Explica cuál es el objetivo del algoritmo y qué representa cada centroide. 
    Su objetivo es dividir un conjunto de datos sin etiquetar en k grupos(clústeres) de forma que los puntos dentro de un mismo grupo sean lo más similares entre sí y los más distintos posibles de los otros grupos. 
        
    Cada centroide Ui representa el punto medio(promedio) de todas las observaciones a las que pertenecen a ese clúster.
 **b)** Describe las dos operaciones que se repiten durante las iteraciones del algoritmo. 
    K-means tiene dos operaciones que se iteran durante su ejecución:
      - Fase de asignación: Se calcula la distancia de cada observación hacia todos los centroides actuales y se asigna cada punto al clúster cuyo centoride esté más cercano (distancia mínima, generalmente euclidiana). 
      - Fase de actualización: Una vez que todos los puntos tienen un grupo, se recalcula la posición de cada centroide como el promedio(punto medio) de todos los datos asignados a ese clúster.
**c)** ¿Por qué dos ejecuciones de *k-means* sobre los mismos datos pueden producir resultados diferentes? Explica cómo se puede reducir este problema. 
    Porque el algoritmo de k-means depende de la ubicación aleatoria de los centroides iniciales. Según donde empiecen esos centroides, el algoritmo puede converger a distintos mínimos locales de inercia, generando agrupamientos diferentes sobre los mismos datos.

    Para reducir este problema, se puede hacer esto:
        - Usar inicialización k-means++: En lugar de elegir los centroides iniciales completamente al azar, este método los distribuye alejados entre sí, lo que mejora la estabilidad y mejora la convergencia.
        - Ejecutar el algoritmo múltiples veces(n_init): Ejecutar k-means varias veces con distintas inicializaciones y quedarse automáticamente con la solución que obtenga la menor inercia total. 
        - Fijar una semilla aleatoria(random_state): Permite controlar la aleatoridad para que los resultados sean 100% reproducibles en cada ejecución. 

2. Considera las siguientes observaciones:

$$X = \{(0, 0), (0, 2), (4, 0), (4, 2)\}.$$

Se aplica *k-means* con $k = 2$ y centroides iniciales

$$\mu_1 = (0, 0), \qquad \mu_2 = (4, 0).$$

Utiliza la distancia euclidiana.

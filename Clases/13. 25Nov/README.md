## Máquinas de soporte vectorial (SVM)
Cuando los datos no son línealmente separablas hay que regularizar el valor c. Cuando esto no funciona se tiene que aplicar transformaciones para poder ver los datos en más dimensiones. 
- Kernel lineal -> No hace ninguna transformación
- Kernel polinomial -> ingresa el hiperparámetro del grado del polinomio.
- Kernel radial. 

### Implementación
[Jypiter notebook donde se realizó la implementación](https://github.com/andres-merino/AprendizajeAutomaticoInicial-05-N0105/blob/main/2-Notebooks/11-SVM.ipynb)


- Cuando c es bajo se prioriza el márgen.
- Cuando c es alto se prioriza los errores(los penaliza). 

Investigar mejor cuando un algortimo está sobreajustado en base al gráfico del notebook visto en esta clase. También investigar cuando se tiene buenos resultados.

    - Subajustado: En entrenamiento está bajo
    - Sobreajustado: En validación está bajo. 
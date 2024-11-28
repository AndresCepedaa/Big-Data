# Challenge: Investigate the 90% Accuracy Limit

Andres Felipe Cepeda Carvajal - 20191005056

Una de las primeras cosas que identifiqué al analizar el codigo fue la función de activación de utilizada en cada una de las capas de la red, originalmente estaban en tanh, pero se cambiaron a Relu ya que la teoria estipula que esta función de activaión tiene mejor desempeño.

Luego analicé la composición de la red se realizaron ciertas modificaciones
1. se aumento el número de filtros en las capas convolucionales quedando la primera de 32 y la segunda de 64, el tamaño del kernel se modificó a (3,3), se agregaron dos capas de dropout, esto para evitar sobre ajustes, estos sobre ajustes en algunos casos puede ocacionar que el accuracy se estanque, por ello parecia una buena idea agregar capas que eliminaran conexiones inecesarias, las capas de drop out se ubicaron despues de las dos capas convolucionales y la otra antes de la capa de salida.

2. Noté también que existían capas con averagepooling, esto no está mal, sin embargo fueron reemplazadas por capas de maxpooling ya que estas tienen la capacidad de indetificar características mas importantes dentro de las imagenes lo que en teoria puede ayudar a mejorar el desempeño del accuracy.

3. A la capa densa o interconectada se le aumentó el número de neuronas que la componen a 128, esto con el objetivo de obtener un modelo mas complejo, de igual forma se le ajustó la función de activación a relu.

4. En el proceso de entrenamiento de la red se ajusta el optimizador por el optimizador ADAM Adaptive Moment Estimation, Adam ajusta la tasa de aprendizaje de forma individual para cada parámetro en función de sus gradientes, lo que permite una optimización más eficiente

5. Se aumentó el numero de epocas del algoritmo, se pasó de 5 a 15 con la esperanza de que el algoritmo al tener un mayor tiempo de entrenamiento pudiera llegar a un modelo con mejor desempeño.

6. Se re distribuyó la base de datos para tener más datos de entrenamiento y menos datos de validación, esto con el objetivo de que el modelo tuviera mas información de la cual aprender patrones. Se dejaron 1000 imagenes para testear el modelo y 64000 para entrenar el modelo.

7. Se agregó un tamaño de lote de 256 imagenes, esto porque en un principio no estaba estipulado el tamaño del lote, este parámetro es importante porque si el tamaño es muy pequeño el algoritmo modifica los pesos demasiadas veces loq eu hace que estos valores fluctuen demasiado afectando el accuracy.

Ya que nada de esto funcionó se puede validar la base de datos, observar que efectivamente la base de datos esté completa, puede que se tenga una clase de mas o de menos que generarian un error de accuracy similar al que se está experimentando. Puede que si de alguna manera los números del 0 al 8 están bien etiquetados y los 9 no, esto generaría un error aproximado del 10% que es lo que se está experiementando.





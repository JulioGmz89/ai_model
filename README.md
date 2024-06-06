# Modelo de detección de chihuahuas y muffins

## Contexto

Se creó un modelo de clasificación binaria, las clases que se tienen son:
- chihuahua
- muffin

El data set con el que se creó este modelo se encuentra en el siguiente [link](https://www.kaggle.com/datasets/samuelcortinhas/muffin-vs-chihuahua-image-classification).

Dentro del data set se encuentran 5917 imágenes, los cuales están divididos en:

### Train:
- chihuahua (2559 imágenes)
- muffin (2174 imágenes)

### Test:
- chihuahua (640 imágenes)
- muffin (544 imágenes)

Posteriormente, la carpeta de test fue dividida por la mitad para crear la carpeta que contendrá las imágenes para validación.

## Preprocesamiento de Datos

Primero los datos se organizaron en directorios separados para entrenamiento, validación y prueba. Esto permite una evaluación estructurada del modelo.

## Data Augmentation

1. **Rescale**: Esta función normaliza los valores de los píxeles a un rango de 0 a 1. Esto facilita el entrenamiento al hacer que los datos sean más manejables para la red neuronal.
2. **Rotation Range**: Esta función hace una rotación aleatoria a las imágenes. Al hacer esto, ayudamos al modelo al ampliar altamente su fuente de datos.
3. **Width Shift Range**: De forma aleatoria, en un rango, desplaza horizontalmente simulando diferentes posiciones y ayudando a la red a aprender mejor.
4. **Zoom Range**: Como su nombre lo indica, hace un zoom aleatorio entre un rango que define el usuario. Esto sirve para simular diferentes distancias de la cámara, ayudando al modelo a aprender características relevantes a diferentes escalas.
5. **Horizontal Flip**: Esta función voltea horizontalmente las imágenes.

## Modelo

### Capas Convolutivas

Se tienen 3 capas convolutivas, la primera tiene 32 filtros de 3x3 y activación ReLU. Esta capa detecta características básicas como bordes y texturas. Las siguientes capas aumentan el número de filtros (64 y 128) para aprender características más complejas y específicas.

El añadir más capas convolutivas permite al modelo aprender características de bajo, medio y alto nivel. Esto se justifica por investigaciones que demuestran que aumentar la profundidad de la red mejora significativamente el rendimiento en tareas de clasificación de imágenes​ [[1]](https://journalofbigdata.springeropen.com/articles/10.1186/s40537-021-00444-8).

### Capas MaxPooling

Cada capa convolutiva le sigue una capa de MaxPooling de 2x2, esta reduce el número de parámetros, evitando un overfitting.

### Capas Densas

Se cuenta con dos capas densas. La primera tiene 512 unidades y una activación ReLU, esta reconoce las características aprendidas y las transforma en algo más útil para la clasificación. La segunda es una función sigmoide, ideal para la clasificación binaria, ya que mapea los valores de salida entre 0 y 1, interpretándose como probabilidades.

### Optimizador

Se decidió por utilizar Adam ya que combina las ventajas de los optimizadores RMSprop y Momentum.

## Entrenamiento del modelo

El modelo se entrena durante 10 épocas utilizando los datos aumentados. Durante el entrenamiento, se monitorean las métricas de precisión y pérdida tanto en los conjuntos de train como de validation para evaluar el rendimiento y ajustar los hiperparámetros según sea necesario.

### Matriz de Confusión:

La matriz de confusión proporciona una evaluación detallada del rendimiento del modelo, mostrando la cantidad de verdaderos positivos, verdaderos negativos, falsos positivos y falsos negativos.

|                | Predicted Muffin | Predicted Chihuahua |
|----------------|------------------|---------------------|
| **Actual Muffin**    | 45               | 5                   |
| **Actual Chihuahua** | 3                | 47                  |

La matriz de confusión nos dice que el modelo tiene una alta tasa de verdaderos positivos (47) y verdaderos negativos (45), con una baja tasa de falsos positivos (5) y falsos negativos (3). Esto indica que el modelo es efectivo para clasificar correctamente las imágenes de chihuahuas y muffins.

Con el uso de esta matriz de confusión, podemos conseguir las siguientes métricas:
- **Precision**: 90.38%
- **Accuracy**: 92%
- **Recall**: 94%
- **F1 Score**: 92.16%

## Gráficas

- Las gráficas de accuracy de train y validación indican que el modelo mejora continuamente durante el entrenamiento, alcanzando una alta precisión en el conjunto de validación.
- Las gráficas de loss muestran una disminución continua, lo que indica que el modelo está aprendiendo y ajustándose bien a los datos.

## Mejora

### Aumento en las capas convolutivas

Agregar más capas convolutivas mejora la capacidad del modelo para aprender características más complejas y mejora su rendimiento en general. Los modelos más profundos pueden capturar características más abstractas y de alto nivel, lo que los hace más robustos para tareas de clasificación de imágenes. Las investigaciones han demostrado que las redes más profundas, como AlexNet y posteriores, han logrado mejoras significativas en el rendimiento en varias tareas de reconocimiento de imágenes al aumentar el número de capas​​ [[1]](https://journalofbigdata.springeropen.com/articles/10.1186/s40537-021-00444-8).

### Optimizador

Cambiar de RMSprop a Adam puede llevar a un mejor rendimiento. Adam combina los beneficios de RMSprop y momentum, proporcionando una tasa de aprendizaje adaptativa y una convergencia más rápida, lo cual es bueno para entrenar redes profundas​​ [[1]](https://journalofbigdata.springeropen.com/articles/10.1186/s40537-021-00444-8).

### Matriz de Confusión

Implementar una matriz de confusión proporciona un desglose detallado del rendimiento del modelo, mostrando no solo la precisión general, sino también dónde comete errores. Esto puede guiar mejoras y ajustes adicionales del modelo.

## Referencias

Laith Alzubaidi, Zhang, J., Humaidi, A. J., Al-Dujaili, A. Q., Duan, Y., Omran Al-Shamma, … Farhan, L. (2021). Review of deep learning: concepts, CNN architectures, challenges, applications, future directions. Journal of Big Data, 8(1). [https://journalofbigdata.springeropen.com/articles/10.1186/s40537-021-00444-8](https://journalofbigdata.springeropen.com/articles/10.1186/s40537-021-00444-8)

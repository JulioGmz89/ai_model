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

El añadir más capas convolutivas permite al modelo aprender características de bajo, medio y alto nivel. Esto se justifica por investigaciones que demuestran que aumentar la profundidad de la red mejora significativamente el rendimiento en tareas de clasificación de imágenes​ (SpringerOpen)​.

### Capas MaxPooling

Cada capa convolutiva le sigue una capa de MaxPooling de 2x2, esta reduce el número de parámetros, evitando un overfitting.

### Capas Densas

Se cuenta con dos capas densas. La primera tiene 512 unidades y una activación ReLU, esta reconoce las características aprendidas y las transforma en algo más útil para la clasificación. La segunda es una función sigmoide, ideal para la clasificación binaria, ya que mapea los valores de salida entre 0 y 1, interpretándose como probabilidades.

### Optimizador

Se decidió por utilizar Adam ya que combina las ventajas de los optimizadores RMSprop y Momentum.

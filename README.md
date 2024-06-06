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

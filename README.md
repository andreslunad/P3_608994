# P3_608994

El objetivo del proyecto es entrenar un modelo capaz de clasificar dígitos (0–9) escritos a mano y realizar predicciones en tiempo real utilizando una cámara web.

Se desarrollaron dos etapas principales:
Entrenamiento de modelos y selección del mejor
Implementación del mejor modelo para inferencia en tiempo real

1. Entrenamiento de Modelos
Dataset
El dataset final se compone de:
Dataset propio (imágenes capturadas manualmente)
MNIST, integrado y convertido a estructura tipo flow_from_directory
Todas las imágenes se normalizaron a [0, 1], convertidas a RGB y escaladas a 96×96 px para compatibilidad.

Modelos Entrenados
Se entrenaron 5 modelos base para comprender el impacto de diferentes modificaciones:
✔ Modelo 1 – CNN pequeña
1 conv + pooling
Rápido, pero rendimiento limitado
✔ Modelo 2 – CNN más profunda
Más filtros
Mejor generalización
✔ Modelo 3 – CNN con Batch Normalization
Entrenamiento más estable
Menos overfitting
✔ Modelo 4 – CNN con Dropout
Mejor regularización
Evita sobreajuste
✔ Modelo 5 – CNN con Augmentación intensa
Mayor robustez
Resultados más consistentes ante variaciones
🚀 2. MobileNetV2 con Transfer Learning
Después de los modelos base, se utilizó MobileNetV2 preentrenada en ImageNet, lo que dio un salto masivo en precisión.

Etapas:
Congelar el feature extractor
Entrenar nuevas capas densas
Fine-tuning de las últimas 20 capas
Entrenar nuevamente con todo el dataset
Este modelo (“ganador”) es el que se exportó y se usa en la webcam.

Métricas Principales
Accuracy validación (MobileNetV2): ~alto desempeño
Accuracy test: ≥ excelente generalización
Matriz de confusión generada para comprender errores entre clases


3. Clasificación en Tiempo Real
El script realtime_multiformat.py:
Accede a la cámara web
Preprocesa cada frame igual que en entrenamiento
Muestra en pantalla:
Probabilidades de cada dígito
Clase ganadora en verde
Imagen exacta enviada al modelo
Soporta .keras, .h5, arquitectura JSON y TensorFlow Lite

Ejecución:
conda activate digits
python realtime_multiformat.py

Compatibilidad y Exportación de Modelos
Se generaron múltiples formatos para garantizar ejecución en Windows:

Formato	Uso
.keras	Formato nativo Keras 3
.h5	Formato clásico, compatible con Windows
.tflite	Ligero, rápido, ideal para tiempo real
.json + .weights.h5	Arquitectura + pesos por separado

Instalación del Entorno
1. Crear entorno
conda create -n digits python=3.9
conda activate digits

2. Instalar dependencias
pip install tensorflow==2.12
pip install opencv-python
pip install numpy matplotlib

Cómo Ejecutar el Proyecto
Para tiempo real:
python realtime_multiformat.py
Presiona q para salir.

Aprendizajes Clave
Importancia de la arquitectura (profundidad, BN, Dropout, augmentación)
Transfer learning como herramienta para pequeños datasets
Fine-tuning para maximizar precisión
Integración de MNIST para mejorar generalización

Exportación multiplataforma para compatibilidad total

Construcción de un pipeline robusto desde datos → modelo → vida real

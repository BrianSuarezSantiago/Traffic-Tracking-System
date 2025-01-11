<a href="https://numpy.org">
    <img align="right" src="https://custom-icon-badges.herokuapp.com/badge/NumPy-14354C.svg?logo=numpylogo" alt="NumPy">
</a>

<a href="https://www.tensorflow.org">
    <img align="right" src="https://img.shields.io/badge/TensorFlow-FF6F00.svg?logo=TensorFlow&logoColor=white" alt="TensorFlow">
</a>

<a href="https://keras.io">
    <img align="right" src="https://img.shields.io/badge/Keras-D00000.svg?logo=Keras&logoColor=white" alt="Keras">
</a>

<a href="https://www.python.org">
    <img align="right" src="https://custom-icon-badges.herokuapp.com/badge/Python-14354C.svg?logo=pythonlogo" alt="Python">
</a>

<h1 align="center">🧠 Detección de Vehículos y Análisis de Tráfico e Infracciones 🤖</h1>

<img src="./resources/Header.jpeg" alt="City Traffic Monitoring">

El presente proyecto consiste en un sistema que ofrece una solución para una [Smart City](https://es.wikipedia.org/wiki/Ciudad_inteligente) basándose en el análisis de tráfico haciendo uso de técnicas de visión por computador para la detección de la velocidad, la dirección y el conteo de entradas y salidas de vehículos en una dirección a partir de un vídeo de entrada.

# 📖 Tabla de contenidos

1. [Motivación](#Motivación)
2. [Objetivo](#Objetivo)
3. [Guía de Instalación](#Guía-de-Instalación)
4. [Consideraciones a tener en cuenta](#Consideraciones-a-tener-en-cuenta)
5. [Descripción Técnica](#Descripción-Técnica)
6. [Fuentes y Tecnologías Utilizadas](#Fuentes-y-Tecnologías-Utilizadas)
7. [Conclusiones](#Conclusiones)
8. [Propuesta de Ampliación y Posibles Mejoras](#Propuesta-de-Ampliación-y-Posibles-Mejoras)
9. [Vídeo venta del trabajo](#Video-Venta-Trabajo)
10. [Imágenes del resultado final](#Imagenes-Resultado-Final)


# 📚 Motivación <a name="Motivación"></a>

El monitoreo y análisis del tráfico vehicular es crucial para la mejora de la seguridad vial, optimización de la gestión del tráfico urbano, y la reducción de la congestión en las ciudades. Este proyecto proporciona una solución automatizada para la detección de vehículos en movimiento, el cálculo de su velocidad y dirección, y el conteo de entradas y salidas de vehículos en un tramo de carretera utilizando técnicas avanzadas de visión por computador.

Asimismo, existe una necesidad crítica de un sistema automático que detecte infracciones por saltarse el semáforo en rojo utilizando grabaciones de [CCTV](https://es.wikipedia.org/wiki/Circuito_cerrado_de_televisión) en tiempo real, garantizando que los infractores sean identificados y sancionados.

Aunque los enfoques de emplear modelos de aprendizaje profundo suelen ser muy aceptados y utilizados actualmente para este ámbito, existen determinadas limitaciones de recursos en cuanto al procesamiento digital de las imágenes sobre todo en cuanto a las capacidades de dichos modelos tradicionales en acción en relación a la detección de imágenes en condiciones adversas como en la oscuridad o con niebla.

# 🚘 Objetivo <a name="Objetivo"></a>

El objetivo principal de este proyecto es desarrollar un sistema para una Smart City el cual a partir de un vídeo de tráfico, pueda:

- Detectar y rastrear vehículos en movimiento.

- Calcular la velocidad y la dirección de los vehículos.

- Contar el número de vehículos que cruzan una línea de conteo predefinida.

Este sistema puede ser utilizado por departamentos de tránsito como la [Dirección General de Tráfico - DGT](https://www.dgt.es/inicio/) en España o investigadores para la obtención de datos relevantes sobre el comportamiento del tráfico en diversos escenarios.

Otro objetivo del proyecto es automatizar el sistema de detección de infracciones de las señales de tráfico y facilitar al departamento de policía de tráfico la vigilancia y la adopción de medidas contra el propietario del vehículo infractor de forma rápida y eficaz. De esta manera, el sistema permite:

1. Detectar y seguir con precisión el vehículo.
2. Obtener en tiempo real la matrícula del vehículo infractor.
3. Reconocimiento de los colores del semáforo en tiempo real sin emplear modelos de inteligencia artificial.
4. Integración de una base de datos para registrar infracciones de matrículas sancionadas utilizando `MySQL`.

# ⚙️ Guía de Instalación <a name="Guía-de-Instalación"></a>

Para instalar y ejecutar el proyecto, sigue los siguientes pasos:

1. Clona este repositorio en tu máquina local:

```bash
git clone https://github.com/BrianSuarezSantiago/Traffic-Tracking.git
cd Traffic-Tracking/
```

2. Crea y activa un entorno virtual de Python:

```bash
# Usando Conda o Miniconda:
conda create --name virtual_env_name python=3.9.5
conda activate virtual_env_name

# Usando soporte nativo de Python:
python -m venv virtual_env_name
source virtual_env_name/bin/activate

# En Windows:
virtual_env_name\Scripts\activate
```

3. Instala las dependencias necesarias:

```bash
pip install opencv-python numpy ultralytics lap shapely tensorflow keras mysql-connector-python
```

4. Ejecuta el notebook `Traffic Tracking.ipynb` desde tu IDE favorito o a través del navegador web con Jupyter Notebook:

```bash
# Necesario tener instalado la librería 'notebook'
pip install notebook

# Abrir el notebook en el navegador web
jupyter notebook
```

# 👀 Consideraciones a tener en cuenta <a name="Consideraciones-a-tener-en-cuenta"></a>

- El modelo de YOLO utilizado es capaz de identificar vehículos tales como automóviles, autobuses, camiones y furgonetas, con variantes según su tamaño.

- La monitorización de las entradas y salidas se basa en un contador situado a una altura específica en píxeles.

- Añadir en la carpeta denominada `vídeos` ubicada dentro del directorio del proyecto todas aquellas muestras de tráfico que desee utilizar en la aplicación, y ajustar el nombre de cada uno de estos samples en la siguiente línea de código:

```python
# Set the path to the input video file
vídeo_path = "vídeos/Traffic_1.mp4"
```

- Dentro del cuaderno, reemplaza los valores `root` y `adminroot` en la sección de conexión a la base de datos con tus credenciales reales correspondientes a la base de datos `MySQL`.

# 👨🏻‍💻 Descripción Técnica <a name="Descripción-Técnica"></a>

El sistema hace uso de un modelo YOLO basándose en la librería YOLOv8 pre-entrenado previamente para la detección de objetos (vehículos, en este caso) en cada fotograma del vídeo de entrada. Una vez detectados los vehículos, se realiza el seguimiento de su trayectoria para calcular la velocidad y determinar la dirección del movimiento (norte o sur) utilizando puntos clave como coordenadas.

- <u>Detección y seguimiento:</u> Se emplea un modelo YOLO personalizado para la detección de vehículos en cada uno de los fotogramas del vídeo. Posteriormente, se realiza el seguimiento de cada uno de los vehículos detectados asignándoles un ID único.

- <u>Cálculo de la velocidad y dirección:</u> Para cada vehículo, se calcula la velocidad mediante la distancia recorrida entre dos fotogramas consecutivos. La dirección se determina comparando la posición vertical actual con la posición anterior.

- <u>Conteo de vehículos:</u> Se define una línea de conteo en el vídeo, y cada vez que un vehículo cruza esta línea, se incrementa el conteo correspondiente a la dirección del movimiento.

- <u>Visualización:</u> El sistema visualiza los resultados de detección y seguimiento, junto con la velocidad, la dirección y los conteos de vehículos, directamente sobre los fotogramas del vídeo.

# 🛠️ Fuentes y Tecnologías Utilizadas <a name="Fuentes-y-Tecnologías-Utilizadas"></a>

- <u>Python:</u> Lenguaje de programación utilizado para el desarrollo del proyecto.

- <u>Librerías:</u>
    - <u>OpenCV:</u> Biblioteca para procesamiento de imágenes y vídeos.
    - <u>NumPy:</u> Biblioteca para cálculos numéricos.
    - <u>Ultralytics YOLO:</u> Herramienta utilizada para la detección de objetos.
    - <u>LAP (Linear Assignment Problem Solver):</u> Utilizada para el rastreo de objetos.
    - <u>Shapely:</u> Biblioteca para cálculos geométricos (e.g., distancia a la línea de conteo).
    - <u>TensorFlow:</u> Biblioteca de código abierto para aprendizaje automático, utilizada para crear, entrenar y desplegar modelos de aprendizaje profundo y redes neuronales.
    - <u>Keras:</u> API de alto nivel construida sobre TensorFlow, que simplifica la creación y el entrenamiento de modelos de aprendizaje profundo gracias a su diseño intuitivo y modular.
    - <u>mysql-connector-python:</u> Librería que permite conectar aplicaciones desarrolladas en Python con bases de datos MySQL, ofreciendo una interfaz sencilla para realizar consultas, inserciones y actualizaciones de datos.

- <u>MySQL:</u> Sistema de gestión de bases de datos relacional (RDBMS) de código abierto, utilizado para almacenar, organizar y gestionar grandes volúmenes de datos. En este proyecto, sirve como repositorio central para registrar las infracciones detectadas, almacenando información como las placas de vehículos penalizados y los detalles de las infracciones.

# 🤔 Conclusiones <a name="Conclusiones"></a>

El proyecto demuestra cómo las técnicas de visión por computador pueden llegar a ser realmente útiles en un contexto aplicado a problemas de la vida real en un escenario como por ejemplo, el análisis del tráfico vehicular de manera automática y eficiente, pudiendo tener su implantación un impacto socio-económico. La detección de vehículos, el cálculo de la velocidad y dirección, así como el conteo de vehículos en tiempo real son útiles para la gestión y planificación del tráfico en ciudades alrededor del mundo.

# 📈 Propuesta de Ampliación y Posibles Mejoras <a name="Propuesta-de-Ampliación-y-Posibles-Mejoras"></a>

Tras analizar las capacidades ofrecidas actualmente por la aplicación, se han considerado de interés para el desarrollo posterior las siguientes ampliaciones y mejoras:

- <u>Mejora de la precisión del conteo:</u> Ajuste de la sensibilidad y precisión del modelo YOLO para minimizar los falsos positivos y negativos.
- <u>Ampliación del soporte para múltiples carriles:</u> Incorporación de lógica para el manejo del tráfico en múltiples carriles y direcciones.
- <u>Integración con sistemas de gestión de tráfico en tiempo real:</u> Permitir que los resultados se envíen directamente a plataformas oficiales de gestión de tráfico.
- <u>Implementación de un sistema de alerta:</u> Alertas automáticas para la detección de incidentes o tráfico inusualmente alto.
- <u>Ampliación del soporte para múltiples tipos de infracciones:</U> Incorporación de lógica para el manejo de múltiples infracciones más allá de saltarse el semáforo en rojo, como por ejemplo, detectar vehículos mal estacionados, uso de teléfono al volante, etc.

# 📖 Recursos Empleados <a name="Recursos-Empleados"></a>

1. [YOLOv8 Documentación Oficial](https://yolov8.org/yolov8-train-custom-dataset-train/)
2. [YOLOv8 Tutorial](https://github.com/roboflow/notebooks)
3. [Entrenamiento de un objeto YOLOv8 con un dataset personalizado](https://github.com/roboflow/notebooks?tab=readme-ov-file)
4. [Entrenamiento de un conjunto de datos personalizados con Ultralytics](https://www.ultralytics.com/es/blog/training-custom-datasets-with-ultralytics-yolov8-in-google-colab)
5. [Dataset de vídeos utilizados](https://www.pexels.com)
6. [Segundo dataset de vídeos utilizados](https://www.videvo.net/es/)
7. [vehicle\_detection\_haarcascades GitHub Repository](https://github.com/andrewssobral/vehicle_detection_haarcascades/blob/master/cars.xml)
8. [Car\_Sideview\_Detection GitHub Repository](https://github.com/ckyrkou/Car_Sideview_Detection)
9. [Need Haar Cascades For Cars StackOverflow Question](https://stackoverflow.com/questions/45074199/need-haar-cascades-for-cars)
10. [What are Vehicle XML Templates?](https://www.mods.studio/tutorials/how-to-create-a-vehicle-xml-template)
11. [ChatGPT](https://openai.com/index/chatgpt/)

# 📽️ Vídeo venta del trabajo <a name="Video-Venta-Trabajo"></a>

[Enlace al vídeo resumen de venta del trabajo](https://alumnosulpgc-my.sharepoint.com/personal/brian_suarez103_alu_ulpgc_es/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Fbrian%5Fsuarez103%5Falu%5Fulpgc%5Fes%2FDocuments%2FVisión%20por%20Computador&ga=1)

# 📸 Imágenes del resultado final <a name="Imagenes-Resultado-Final"></a>

<img src="./resources/Result 1.png" alt="Result 1">

<img src="./resources/Result 2.png" alt="Result 2">

<img src="./resources/Result 3.png" alt="Result 3">

<img src="./resources/Result 4.png" alt="Result 4">

<img src="./resources/Result 5.png" alt="Result 5">

<hr>
<p align="center">
Made with ♥️ in Spain
</p>

 PROYECTO-IA
#  Prototipo de Policiamiento Predictivo (SIDPOL)
Repositorio oficial del modelo predictivo basado en Machine Learning para la clasificación de tipologías delictivas en el Perú.

I. Contexto de la Investigación

**1. ¿Cuál es el problema?**
La limitada capacidad analítica de las instituciones de seguridad ciudadana para predecir y clasificar automáticamente las tipologías de delitos basándose en datos históricos masivos.

**2. ¿Cuál es el objetivo?**
Desarrollar, evaluar y comparar modelos de Machine Learning (Regresión Logística, KNN, Random Forest) para clasificar tipos de delitos utilizando exclusivamente coordenadas espaciotemporales estructuradas.

**10. ¿Cuáles fueron los resultados?**
El Modelo Base (Regresión Logística multinomial con pesos balanceados) obtuvo el mayor rendimiento predictivo global (F1-Score Macro: 0.1306), demostrando que la conversión nominal de variables geográficas de alta cardinalidad degrada la capacidad de algoritmos basados en distancias (KNN).


II. Fuente de Datos

**3. ¿Qué dataset se utilizó?**
Los datos abiertos oficiales del Sistema de Denuncias Policiales (SIDPOL) del Ministerio del Interior del Perú, abarcando 369,100 registros desde el año 2018 hasta julio de 2026.

**4. ¿Cómo obtener los datos?**
El archivo original puede ser descargado desde la Plataforma Nacional de Datos Abiertos del Estado Peruano (Sección Observatorio Nacional de Seguridad Ciudadana) o contactando a la entidad.


III. Guía Técnica y Reproducibilidad

**5. ¿Cómo instalar el proyecto?**
No se requiere instalación local compleja. Basta con clonar este repositorio y cargar el entorno interactivo (Google Colab / Jupyter). Las dependencias requeridas están documentadas en el archivo `requirements.txt`.

**6. ¿Cómo ejecutar el código?**
Abra el notebook principal ubicado en la carpeta `notebooks/`, monte el directorio donde se ubique el dataset y ejecute las celdas de preparación e ingeniería de datos de manera secuencial.

**7. ¿Cómo entrenar el modelo?**
Ejecutando la sección de Modelado en el notebook. El código instancia automáticamente el preprocesamiento (LabelEncoder, StandardScaler) y entrena los modelos matemáticos.

**8. ¿Cómo reproducir los experimentos?**
El experimento es determinista. El código mantiene un entorno controlado al fijar la semilla aleatoria (`random_state=42`) en la partición estratificada de datos y en los hiperparámetros de los algoritmos.

**9. ¿Cómo ejecutar el prototipo?**
Ejecutando la última celda del notebook. El sistema desplegará una interfaz gráfica interactiva construida con la librería `Gradio` que permite ingresar parámetros geográficos y temporales para obtener predicciones en tiempo real.

# Sistema Híbrido Multimodal de Seguridad Ciudadana (SIDPOL + CNN 2D)

Proyecto de Inteligencia Artificial (FIEI - UNFV) que combina **Machine Learning supervisado** sobre datos históricos de denuncias policiales del MININTER con **Deep Learning (Red Neuronal Convolucional 2D)** para la clasificación fotográfica de evidencia física (armas blancas y armas de fuego), integrados en un prototipo web interactivo con Gradio.

## Estructura del Repositorio

* `data/`: Dataset tabular histórico de denuncias policiales (`denuncias_policiales.csv`).
* `docs/`: Informe final de investigación en formato PDF.
* `notebooks/`: Cuaderno reproducible de Google Colab (`PROYECTOA_IA_v2_0 FINAL.ipynb`).
* `results/`: Gráficos de EDA, matrices de confusión, curvas de aprendizaje de la CNN y capturas del prototipo.
* `requirements.txt`: Dependencias de Python necesarias para ejecutar el proyecto.

## 1. ¿Cuál es el problema?
La limitada capacidad analítica de las instituciones de seguridad ciudadana para predecir tipologías delictivas a partir de datos históricos masivos, sumada a la clasificación manual de evidencia física incautada durante el registro de denuncias.

## 2. ¿Cuál es el objetivo?
Desarrollar y evaluar un sistema híbrido multimodal que integre modelos de Machine Learning (Regresión Logística, KNN y Random Forest) sobre coordenadas espaciotemporales del SIDPOL con una Red Neuronal Convolucional 2D (TensorFlow/Keras) para clasificar fotografías de evidencia pericial en tiempo real.

## 3. ¿Qué datasets se utilizaron?
* **Módulo Tabular (SIDPOL - MININTER):** 369,100 registros históricos de denuncias policiales en el Perú (enero 2018 – julio 2026), con 8 variables y 100% de completitud.
* **Módulo Visual (Kaggle - Guns-Knives Object Detection):** 5,807 fotografías etiquetadas y reorganizadas en dos clases balanceadas (`knife` y `pistol`), divididas en *train* (4,389), *valid* (1,036) y *test* (382).

## 4. ¿Cómo obtener los datos?
* **SIDPOL:** Disponible en la Plataforma Nacional de Datos Abiertos del Perú (Observatorio Nacional de Seguridad Ciudadana).
* **Imágenes de armas:** Descargadas automáticamente vía API oficial de Kaggle desde el repositorio público `iqmansingh/guns-knives-object-detection` (Licencia CC0).

## 5. ¿Cómo instalar y ejecutar el proyecto?
1. Subir `denuncias_policiales.csv` y el token personal `kaggle.json` a la raíz de Google Drive (`MyDrive/`).
2. Abrir `notebooks/PROYECTOA_IA_v2_0.ipynb` en **Google Colab**.
3. Activar aceleración por hardware en **Entorno de ejecución > Cambiar tipo de entorno de ejecución > GPU (T4 o L4)**.
4. Ejecutar todas las celdas secuencialmente (**Entorno de ejecución > Ejecutar todo**).

## 6. Reproducibilidad
El experimento fija semillas deterministas (`random_state=42` en Scikit-Learn; `tf.random.set_seed(42)` y `np.random.seed(42)` en TensorFlow/NumPy) y mantiene particiones estrictamente aisladas para prevenir fuga de información (*data leakage*).

## 7. Ejecución del Prototipo Multimodal
La última celda del notebook despliega automáticamente una interfaz web en **Gradio** (`share=True`). En ella se ingresan las coordenadas espaciotemporales (Año, Mes, Departamento, Provincia y Distrito) y opcionalmente una fotografía de evidencia para obtener en paralelo la predicción del delito (con UBIGEO real) y el análisis pericial de la CNN 2D con su porcentaje de confianza.

## 8. Resumen de Resultados

### Módulo 1: Predicción Espaciotemporal (SIDPOL)
| Modelo | Arquitectura | F1-Score (Macro) |
| :--- | :--- | :---: |
| Baseline | Regresión Logística (`class_weight='balanced'`) | **0.1306** |
| Avanzado 1 | K-Nearest Neighbors (`K=1`) | 0.0244 |
| Avanzado 2 | Random Forest (`n_estimators=50`, `balanced`) | 0.0371 |

### Módulo 2: Visión Artificial (CNN 2D - Conjunto Test: 382 imágenes)
| Clase / Métrica | Precision | Recall | F1-Score | Soporte |
| :--- | :---: | :---: | :---: | :---: |
| Arma Blanca (`knife`) | 0.90 | 0.89 | 0.90 | 207 |
| Arma de Fuego (`pistol`) | 0.87 | 0.89 | 0.88 | 175 |
| **Accuracy Global / Macro Avg** | **0.89** | **0.89** | **0.89 (88.74%)** | **382** |

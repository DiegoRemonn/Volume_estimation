# Volume_estimation

Estimación de volumen mediante aprendizaje profundo y regresión multivariante.  
El repositorio contiene varios notebooks de entrenamiento e inferencia pensados para ejecutarse en **Google Colab**.


## Tabla de contenidos
- [Requisitos](#requisitos)
- [Estructura del repositorio](#estructura-del-repositorio)
- [Uso rápido](#uso-rápido)
  - [Entrenamiento](#entrenamiento)
  - [Inferencia](#inferencia)
- [Resultados](#resultados)
- [Autor](#autor)

## Requisitos
- Python ≥ 3.5  
- TensorFlow 2.15 (se instala al inicio de cada notebook para asegurar compatibilidad con TFLite) :contentReference[oaicite:0]{index=0}  
- Scikit-Learn ≥ 0.20, NumPy, Pandas, Matplotlib, SciPy :contentReference[oaicite:1]{index=1}  
- Acceso a Google Drive para montar datos y almacenar modelos/figuras :contentReference[oaicite:2]{index=2}  


Instalación mínima:

```bash
pip install tensorflow==2.15 scikit-learn pandas matplotlib scipy joblib
```

## Estructura del repositorio
| Notebook | Descripción |
|----------|-------------|
| **VolumeDetection_Complete.ipynb** | Entrenamiento base con todas las muestras. |
| **VolumeDetection_CompleteOptimized.ipynb** | Búsqueda de hiperparámetros y optimización del modelo completo. |
| **VolumeDetection_CompleteOptimized2.ipynb** | Variante optimizada con *Free Space 1*. |
| **VolumeDetection_CompleteOptimized3.ipynb** | Variante optimizada con *Free Space 2* y ajustes finales. |
| **VolumeDetection_Inference{1-4}.ipynb** | Cuatro pruebas de inferencia que evalúan configuraciones de entrada específicas. |

Todos los notebooks siguen este flujo básico:

1. Montar Google Drive con `drive.mount('/content/drive')`.
2. Instalar / verificar TensorFlow 2.15.
3. Cargar `VolumeDataset.csv` desde Drive.
4. Dividir datos en *train*, *validation* y *test*.
5. Construir *pipelines* (imputación, escalado, PCA) y modelos (regresores clásicos o DNN).
6. Ajustar hiperparámetros (*RandomizedSearchCV* o equivalentes).
7. Guardar modelos y figuras en `VolumeModels` y `VolumeImages`.

## Uso rápido

### Entrenamiento
1. Abre en Colab el notebook deseado.  
2. Ejecuta la celda de montaje de Drive y verifica que `VolumeDataset.csv` esté en `/content/drive/MyDrive`.  
3. Ejecuta todas las celdas; el mejor modelo se guardará automáticamente gracias a `ModelCheckpoint`, y el entrenamiento se detendrá mediante `EarlyStopping` para evitar *overfitting*.  
4. Los modelos (`.h5`, `.tflite`) quedan en `MyDrive/VolumeModels`.

### Inferencia
1. Asegúrate de que el modelo entrenado está en la ruta indicada o súbelo manualmente.  
2. Abre uno de los notebooks `VolumeDetection_Inference*` y ejecuta las celdas para obtener predicciones sobre las muestras definidas.  

## Resultados
En cada notebook se calculan métricas como **MAE** y **RMSE** usando `mean_absolute_error` y `mean_squared_error`.  
Las versiones optimizadas reducen el MAE respecto al modelo base; consulta las últimas celdas de cada notebook para los valores concretos.  

## Autor
Creado por **Diego Remón** (2024/2025).  
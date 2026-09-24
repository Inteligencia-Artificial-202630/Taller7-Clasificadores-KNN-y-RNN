# Taller 07: Clasificación de Dígitos Escritos a Mano (KNN y RNN)

## 📋 Descripción

Se diseñan e implementan dos clasificadores basados en vecindad —**KNN (K-Nearest
Neighbors)** y **RNN (Radius Neighbors, vecinos dentro de un radio)**— para reconocer
dígitos manuscritos (0-9) del conjunto [`digits` de scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_digits.html)
(1797 imágenes de 8x8 píxeles).

> **Nota:** en este proyecto **RNN significa "vecinos dentro de un radio"**, no red
> neuronal recurrente.

El conjunto de datos se divide en **80 % entrenamiento / 20 % prueba** (estratificado),
y los hiperparámetros de cada modelo (K para KNN, R para RNN) se calibran mediante
**validación cruzada con 4 particiones (K-fold = 4)** sobre el conjunto de
entrenamiento:

- Se evalúa un **rango de valores de K** y se grafican las métricas de desempeño
  (Accuracy, F1 macro, Precisión macro, Recall macro) para elegir el mejor K.
- Se evalúa un **rango de valores de R** y se grafican las mismas métricas más la
  **cobertura** (fracción de muestras con al menos un vecino dentro del radio) para
  elegir el mejor R.
- Ambos modelos calibrados se entrenan con todo el entrenamiento y se evalúan **una
  sola vez** sobre el conjunto de prueba reservado (matriz de confusión, reporte de
  clasificación, ejemplos mal clasificados y tiempo de predicción).

El notebook cierra con una comparación cuantitativa y cualitativa entre KNN y RNN.

## 📁 Estructura del repositorio

```
.
├── Taller7_Clasificacion_Digits_KNN_RNN.ipynb   # Notebook principal
└── README.md
```

## 🗂️ Dataset

Se usa el conjunto **`digits` incluido en scikit-learn** (`sklearn.datasets.load_digits`),
por lo que **no requiere descarga**: se carga directamente al ejecutar el notebook.

## ⚙️ Requisitos

```bash
pip install numpy pandas matplotlib scikit-learn
```

## ▶️ Cómo ejecutar

1. Clone este repositorio.
2. Abra `Taller7_Clasificacion_Digits_KNN_RNN.ipynb` en Jupyter Notebook, JupyterLab,
   VS Code o Google Colab.
3. Ejecute las celdas en orden (`Run All`).

> **Nota:** el notebook ya viene ejecutado con sus salidas y figuras; no requiere
> controles interactivos (sliders, widgets).

## 📊 Resultados principales

- **KNN** alcanza su mejor desempeño con valores pequeños de K (K = 5, F1 macro ≈ 0.97
  en validación cruzada), y clasifica siempre el 100 % de las muestras de prueba.
- **RNN** alcanza un desempeño comparable (R = 6.0, F1 macro ≈ 0.97) exigiendo una
  cobertura mínima del 95 %; radios más pequeños dan métricas de calidad más altas pero
  con cobertura muy baja, mientras que radios más grandes cubren casi todo el conjunto
  a costa de mezclar vecinos de otras clases.
- Los **errores de ambos clasificadores** se concentran en dígitos con trazos
  ambiguos (por ejemplo, algunos "8" y "9" mal formados que se confunden entre sí),
  consistente con lo observado en las matrices de confusión.
- **KNN resulta más simple y robusto de operar** en este problema, al no depender de
  una escala de distancia fija y garantizar cobertura total, aunque **RNN** es útil
  cuando se quiere que el modelo "se abstenga" explícitamente en casos ambiguos.

Ver la sección de comparación final en el notebook para el análisis completo.

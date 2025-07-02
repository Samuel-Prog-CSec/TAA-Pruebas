# Predicción de la calidad del vino: clasificación vs. regresión

Este repositorio contiene el proyecto 1 de Machine Learning realizado para la asignatura de **Técnicas de Aprendizaje Automático (TAA)**. El objetivo es predecir la calidad de un vino basándose en sus características fisicoquímicas, comparando dos enfoques fundamentales: **regresión** y **clasificación**.

## Descripción del proyecto

El análisis se centra en el conjunto de datos de calidad del vino de UCI. El cuaderno de Jupyter (`TAA_Cuaderno_Entrega_1.ipynb`) documenta todo el proceso, desde el análisis exploratorio de datos (EDA) hasta el entrenamiento, optimización y evaluación de modelos.

### Objetivos principales
1.  **Explorar y preprocesar los datos:** analizar las variables del dataset, identificar correlaciones clave y preparar los datos para el modelado, incluyendo la normalización de características.
2.  **Entrenar un modelo de regresión:** predecir la puntuación de calidad (de 3 a 9) como un valor numérico continuo.
3.  **Entrenar un modelo de clasificación:** clasificar la calidad del vino en tres categorías: "Bajo", "Medio" y "Alto".
4.  **Evaluar y comparar:** utilizar métricas adecuadas (R², MAE, Accuracy, F1-Score, ROC-AUC) para comparar objetivamente el rendimiento de ambos enfoques.
5.  **Extraer conclusiones fundamentadas:** determinar qué enfoque es más adecuado para este problema y justificar la elección.

## Metodología

El proyecto sigue una metodología rigurosa para garantizar la validez de los resultados:

- **Análisis exploratorio (EDA):** se identificaron el alcohol, la acidez volátil y la densidad como las características más correlacionadas con la calidad.
- **Protocolo de validación:** se corrigió un potencial **data leakage** asegurando que el escalado de características se realiza *después* de la división en conjuntos de entrenamiento y prueba.
- **Modelos evaluados:** se compararon varios algoritmos para cada tarea:
    - **Regresión:** Regresión lineal, Random Forest Regressor, SVR y Decision Tree Regressor.
    - **Clasificación:** Regresión logística, Random Forest Classifier, SVC y Decision Tree Classifier.
- **Optimización de hiperparámetros:** se utilizó `GridSearchCV` para encontrar la mejor configuración para el `RandomForest`, el modelo con mejor rendimiento inicial en ambas tareas.

### Descubrimiento principal
Tras la corrección metodológica, se demostró que el **enfoque de clasificación supera de forma significativa al de regresión**.

- El modelo de **clasificación** (Random Forest Classifier) alcanzó una **Accuracy del 82.4%** y un **F1-Score de 0.759**, demostrando ser una herramienta robusta y fiable para aplicaciones prácticas.
- Por el contrario, el modelo de **regresión** (Random Forest Regressor) falló catastróficamente, obteniendo un **R² negativo de -1.547**, lo que indica que su rendimiento es peor que un modelo que simplemente calcula la media.

## Cómo ejecutar este notebook

### Prerrequisitos
- Python 3.x
- Jupyter Notebook o JupyterLab
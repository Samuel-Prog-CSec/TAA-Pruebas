# Búsqueda de patrones en el movimiento humano: clustering y procesamiento de señales

Este repositorio contiene el proyecto 2 para la asignatura **Técnicas de Aprendizaje Automático (TAA)**. El objetivo es analizar un conjunto de datos de captura de movimiento humano para identificar y caracterizar patrones de marcha distintos mediante técnicas de clustering no supervisado.

## Descripción del proyecto

El proyecto implementa un pipeline completo de Machine Learning que abarca desde la carga y limpieza de datos brutos hasta la extracción de características biomecánicas y la interpretación funcional de los clusters resultantes. Se utiliza un conjunto de datos público que contiene grabaciones de las posiciones de articulaciones principales de sujetos mientras caminan.

### Objetivos clave

- Cargar y preprocesar un conjunto de datos multi-archivo y de series temporales.
- Aplicar transformaciones biomecánicas (coordenadas relativas) para aislar los patrones de movimiento.
- Segmentar la señal continua en ventanas temporales de 4 segundos.
- Extraer un conjunto rico de características estadísticas y dinámicas de cada ventana.
- Evaluar y seleccionar el algoritmo de clustering más adecuado mediante métricas cuantitativas.
- Interpretar y caracterizar biomecánicamente los patrones de marcha identificados.

---

## Pipeline de análisis

El análisis sigue una metodología rigurosa estructurada en los siguientes pasos, implementados en el notebook `TAA_Cuaderno_Entrega_2.ipynb`:

1.  **Carga y consolidación de datos:** se leyeron y combinaron los múltiples archivos CSV por cada participante en un único DataFrame, manteniendo la trazabilidad del sujeto y la grabación.

2.  **Preprocesamiento biomecánico:**
    - **Coordenadas relativas:** se restó la posición de la pelvis (centro de masa aproximado) a todas las demás articulaciones para eliminar los efectos de la traslación global y analizar únicamente el movimiento relativo del cuerpo.
    - **Ventaneo:** la serie temporal se segmentó en ventanas no solapadas de 4 segundos.

3.  **Extracción de características:** para cada ventana y cada coordenada relativa de las articulaciones, se extrajeron características, incluyendo:
    - **Estadísticas básicas:** media, desviación estándar, rango, mínimo y máximo.
    - **Características dinámicas:** velocidad y aceleración promedio y su variabilidad.
    - **Distancias inter-articulares:** como el ancho de hombros, para capturar información postural.

4.  **Normalización:** se aplicó un enfoque de doble normalización para asegurar la robustez del clustering:
    - **Normalización Z-score por participante:** para eliminar sesgos antropométricos individuales.
    - **Normalización StandardScaler global:** para escalar todas las características a una media de 0 y una desviación estándar de 1.

5.  **Modelo de clustering:**
    - Se evaluaron K-Means, Clustering Jerárquico y DBSCAN.
    - K-Means con k=3 fue seleccionado como el modelo óptimo basado en un ranking ponderado de métricas (Silhouette, Calinski-Harabasz, Davies-Bouldin).

6.  **Visualización e interpretación:** se utilizaron técnicas de reducción de dimensionalidad (PCA y t-SNE) para visualizar los clusters y se realizó un análisis estadístico de las características para interpretar su significado biomecánico.

---

## Resultados Clave

El análisis identificó con éxito **tres patrones de marcha funcionalmente distintos**. El gráfico de distribución por participante demostró que estos clusters representan **estrategias motoras** y no tipos de individuos, ya que todos los participantes exhibieron los tres patrones.

-   **Cluster 0: marcha rápida y propulsiva (18.6% de las ventanas)**
    - Caracterizada por una **alta velocidad promedio** en el eje de avance (X), principalmente en las extremidades inferiores.

-   **Cluster 1: marcha estable base (60.5% de las ventanas)**
    - Representa el patrón más común, definido por una **baja variabilidad de velocidad y aceleración** en el eje vertical (Z), indicando un caminar estable y con poco rebote.

-   **Cluster 2: marcha con balanceo lateral (20.9% de las ventanas)**
    - Definida por una **alta velocidad promedio** en el eje medio-lateral (Y), sugiriendo un mayor balanceo del cuerpo, posiblemente como estrategia de equilibrio.

---

## Estructura del repositorio

```
/
├── TAA_Cuaderno_Entrega_2.ipynb  # Notebook principal con todo el análisis y la documentación
├── dataset/                      # Carpeta que contiene los datos del proyecto (omitida con .gitignore)
│   └── data/
└── README.md                     # Este archivo
```
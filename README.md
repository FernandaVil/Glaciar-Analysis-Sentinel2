# Análisis de Retroceso Glaciar mediante Imágenes Sentinel-2

Este proyecto desarrolla un pipeline automatizado en Python para cuantificar la pérdida de superficie de hielo utilizando imágenes satelitales de la misión **Sentinel-2 (ESA)**. 

## Resultados Visuales
![Comparativa Glaciar](./output/comparativa_glaciar.png)
*Visualización del índice NDSI (Normalized Difference Snow Index). El color azul intenso resalta las áreas con mayor presencia de nieve/hielo.*

## Desafíos Técnicos y Soluciones
Como estudiante de Ciencia de Datos, apliqué herramientas matemáticas y estadísticas para el procesamiento de datos raster:
* **Estandarización de Resoluciones:** Implementé un *upsampling* bilineal para igualar las bandas de 20m a la resolución de 10m de las bandas visibles.
* **Índices Espectrales:** Uso del índice NDSI para discriminar nieve de nubes y suelo desnudo.
  
  $$NDSI = \frac{Green - SWIR}{Green + SWIR}$$

* **Optimización:** Uso de `MemoryFile` para procesar recortes en memoria volátil, mejorando la eficiencia del pipeline.

## Estructura del Proyecto
* `Analisis_Glaciar_Final.ipynb`: Notebook principal con el flujo de trabajo documentado.
* `data/`: Área de interés (AOI) en formato GeoJSON.
* `output/`: Mapas comparativos generados.

---
*Proyecto realizado como exploración personal en Teledetección y Análisis Geoespacial.*

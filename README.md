# Análisis de Retroceso Glaciar mediante Imágenes Sentinel-2

Este proyecto desarrolla un pipeline automatizado en Python para cuantificar la pérdida de superficie de hielo utilizando imágenes satelitales de la misión **Sentinel-2 (ESA)**. Aunque este análisis se centra específicamente en el **Glaciar Perito Moreno (Argentina)**, el sistema está diseñado para ser replicable en cualquier otro glaciar del mundo simplemente sustituyendo el archivo GeoJSON del área de interés (AOI).
## Resultados Visuales
![Comparativa Glaciar](./output/comparativa_glaciar.png)
*Visualización del índice NDSI (Normalized Difference Snow Index). El color azul intenso resalta las áreas con mayor presencia de nieve/hielo.*

## Desafíos Técnicos y Soluciones
Como estudiante de Ciencia de Datos, apliqué herramientas matemáticas y estadísticas para el procesamiento de datos raster:
* **Estandarización de Resoluciones:** Implementé un *upsampling* bilineal para igualar las bandas de 20m a la resolución de 10m de las bandas visibles.
* **Escalabilidad:** El código es independiente de la ubicación; procesa cualquier par de imágenes Sentinel-2 siempre que cubran las coordenadas definidas en el archivo GeoJSON de entrada.
* **Índice Espectral (NDSI):** Utilizado para discriminar con precisión hielo de nubes y suelo. 

  $$NDSI = \frac{Green - SWIR}{Green + SWIR}$$

* **Optimización:** Uso de `MemoryFile` para procesar recortes en memoria volátil, mejorando la eficiencia del pipeline.
## Cómo ejecutar este proyecto localmente

### 1. Obtención de Datos 
Para ejecutar este notebook, necesitas descargar las imágenes satelitales crudas:
1. Ve a [Copernicus Browser](https://dataspace.copernicus.eu/browser/).
2. Busca la zona del **Glaciar Perito Moreno** (o la zona de tu interés).
3. Filtra por la misión **Sentinel-2** y busca fechas con **0% de nubosidad**.
4. Descarga el producto en formato **L2A** (Surface Reflectance).
5. Descomprime la carpeta `.SAFE` dentro de `data/raw/` en este proyecto.
### 2. Instalación y Ejecución
1. **Clonar el repositorio:**
   ```bash
   git clone [https://github.com/FernandaVil/Glaciar-Analysis-Sentinel2.git](https://github.com/FernandaVil/Glaciar-Analysis-Sentinel2.git)

2. **Instalar dependencias**
    ```bash
    pip install -r requirements.txt
3. **Ejecutar:** Abre `Analisis_Glaciar_Final.ipynb` en VS Code o Jupyter. Si quieres analizar otro glaciar, solo debes reemplazar `data/map.geojson` por uno nuevo generado en [geojson.io](https://geojson.io/).

## Estructura del Proyecto
* `Analisis_Glaciar_Final.ipynb`: Notebook principal con el flujo de trabajo documentado.
* `data/`: Área de interés (AOI) en formato GeoJSON.
* `output/`: Mapas comparativos generados.
* `requirements.txt`: Librerías necesarias para la ejecución.

---
*Proyecto realizado como exploración personal en Teledetección y Análisis Geoespacial.*

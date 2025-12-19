# Análisis de Retroceso Glaciar mediante Imágenes Sentinel-2

Este proyecto desarrolla un pipeline automatizado en Python para cuantificar la pérdida de superficie de hielo utilizando imágenes satelitales de la misión **Sentinel-2 (ESA)**. Aunque este análisis se centra específicamente en el **Glaciar Perito Moreno (Argentina)**, el sistema está diseñado para ser replicable en cualquier otro glaciar del mundo simplemente sustituyendo el archivo GeoJSON del área de interés (AOI).

> 🇺🇸 [English Version](./README.md)

## Resultados Visuales
![Comparativa Glaciar](./output/comparativa_glaciar.png)
*Visualización del índice NDSI (Normalized Difference Snow Index). El color azul intenso resalta las áreas con mayor presencia de nieve/hielo.*
## Impacto y Conclusiones
El análisis cuantificó una pérdida neta de **2.70 km²** de superficie de hielo en solo 5 años. Para dimensionar esta magnitud en el contexto local (Argentina):

* La superficie perdida equivale a casi el **80% de la Reserva Ecológica Costanera Sur** de Buenos Aires.
* Representa aproximadamente **378 canchas de fútbol** profesionales.
* Es una superficie mayor a la de todo el barrio de **Puerto Madero** (aprox 2.1 km²).

## Desafíos Técnicos y Soluciones
Como estudiante de Ciencia de Datos, apliqué herramientas matemáticas y estadísticas para el procesamiento de datos raster:
* **Estandarización de Resoluciones:** Implementé un *upsampling* bilineal para igualar las bandas de 20m a la resolución de 10m de las bandas visibles.
* **Escalabilidad:** El código es independiente de la ubicación; procesa cualquier par de imágenes Sentinel-2 siempre que cubran las coordenadas definidas en el archivo GeoJSON de entrada.
* **Índice Espectral (NDSI):** Utilizado para discriminar con precisión hielo de nubes y suelo. 

  $$NDSI = \frac{Green - SWIR}{Green + SWIR}$$

* **Optimización:** Uso de `MemoryFile` para procesar recortes en memoria volátil, mejorando la eficiencia del pipeline.
## Cómo ejecutar este proyecto localmente

### 1. Obtención de Datos (Criterios de Selección)
#### **Imagenes Satelitales**
Para que la comparación sea válida y no se vea afectada por variaciones estacionales o errores de medición, se deben seguir estos criterios en [Copernicus Browser](https://dataspace.copernicus.eu/browser/):

* **Consistencia Estacional:** Al trabajar con glaciares del Hemisferio Sur, es fundamental elegir imágenes del **verano austral** (Enero-Marzo) para ambas fechas. Esto asegura que estemos midiendo el hielo real y no la cobertura de nieve estacional de invierno.
* **Filtro de Nubosidad:** Lo ideal es buscar imágenes con **<10% de nubosidad**. En caso de no haber disponibilidad para las fechas deseadas, se puede extender el margen hasta un **20% máximo**, verificando que las nubes no cubran el frente del glaciar.
* **Tipo de Producto:** Descargar siempre en formato **L2A (Surface Reflectance)** para garantizar que los valores de reflectancia estén corregidos atmosféricamente.
* **Instalación:** Descomprimir la carpeta `.SAFE` .
#### **Área de Interés (GeoJSON):**
   - Entra en [geojson.io](https://geojson.io/).
   - Dibuja un polígono sobre el frente del glaciar que deseas analizar.
   - Haz clic en `Save > GeoJSON`.
   - Renombra el archivo como `map.geojson` y guárdalo.

### 2. Instalación y Ejecución
1. **Clonar el repositorio:**
   ```bash
   git clone https://github.com/FernandaVil/Glaciar-Analysis-Sentinel2.git
2. **Entrar a la carpeta:**
   ```bash
   cd Glaciar-Analysis-Sentinel2
3. **Instalar dependencias**
    ```bash
    pip install -r requirements.txt
(Se recomienda el uso de un entorno virtual).
4. **Mover Datos:** Copia tus carpetas .SAFE dentro de la carpeta `data/raw/` y el archivo map.geojson dentro de la carpeta `data` que se encuentra dentro del proyecto clonado.
5. **Ejecución:** Abrir el Notebook `Analisis_Glaciar_Final.ipynb` y ejecutar las celdas seleccionando el kernel donde se instalaron las dependencias.



## Estructura del Proyecto
    ```bash
      Glaciar-Analysis-Sentinel2/
      ├── data/
      │   ├── raw/           <-- AQUÍ van tus carpetas .SAFE
      │   └── map.geojson    <-- AQUÍ va tu archivo de geometría
      ├── Analisis_Glaciar_Final.ipynb
      ├── requirements.txt
      └── README.md

* `Analisis_Glaciar_Final.ipynb`: Notebook principal con el flujo de trabajo documentado.
* `data/`: Área de interés (AOI) en formato GeoJSON.
* `output/`: Mapas comparativos generados.
* `requirements.txt`: Librerías necesarias para la ejecución.

---
*Proyecto realizado como exploración personal en Teledetección y Análisis Geoespacial.*

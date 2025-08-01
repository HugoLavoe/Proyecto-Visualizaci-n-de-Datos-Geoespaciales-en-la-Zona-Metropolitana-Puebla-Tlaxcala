# Proyecto-Visualizaci-n-de-Datos-Geoespaciales-en-la-Zona-Metropolitana-Puebla-Tlaxcala
## Descripción del Proyecto
Este proyecto tiene como objetivo visualizar datos geoespaciales de la Zona Metropolitana Puebla-Tlaxcala (ZMPT) utilizando Python y bibliotecas como `folium`, `geopandas` y `matplotlib`. El trabajo incluye la creación de mapas interactivos y estáticos para representar información geográfica, como ubicaciones de estudiantes y límites administrativos.

## Tecnologías Utilizadas
- **Python**: Lenguaje principal para el análisis y visualización de datos.
- **Google Colab**: Entorno de ejecución para los scripts.
- **Bibliotecas**:
  - `pandas`: Manipulación de datos.
  - `folium`: Creación de mapas interactivos.
  - `geopandas`: Procesamiento de datos geoespaciales.
  - `matplotlib`: Visualización de gráficos y mapas estáticos.

## Estructura del Proyecto
1. **Carga y Limpieza de Datos**:  
   - Se utiliza un archivo CSV (`Estaura_peso_modificado1.csv`) que contiene datos de ubicación (latitud y longitud).
   - Los datos se limpian y separan en columnas individuales para su procesamiento.

2. **Mapa Interactivo con Folium**:  
   - Se crea un mapa centrado en Puebla, México, con marcadores que representan ubicaciones específicas.

3. **Mapa Estático con Geopandas**:  
   - Se carga un shapefile (`Limite_ZMPT.shp`) para visualizar los límites de la ZMPT.
   - Se personaliza el mapa con títulos, etiquetas y estilos.

## Instrucciones de Uso
1. **Requisitos Previos**:
   - Tener acceso a Google Colab o un entorno Python con las bibliotecas mencionadas instaladas.
   - Subir los archivos necesarios (`Estaura_peso_modificado1.csv` y `Limite_ZMPT.shp`) a la ubicación correcta en Google Drive o localmente.

2. **Ejecución**:
   - Abrir el notebook en Google Colab o ejecutar los scripts en un entorno local.
   - Asegurarse de que las rutas de los archivos estén correctamente configuradas.

3. **Resultados**:
   - El mapa interactivo se mostrará directamente en el notebook.
   - El mapa estático se generará y guardará según la configuración del script.

## Ejemplo de Código
```python
# Cargar y limpiar datos
import pandas as pd
data = pd.read_csv('/content/drive/My Drive/Colab Notebooks/Conchita/productos/Estaura_peso_modificado1.csv')
data[['Latitud', 'Longitud']] = data['Ubicacion'].str.split('.', expand=True)

# Crear mapa interactivo
import folium
mapa_puebla = folium.Map(location=[19.0414, -98.2063], zoom_start=10)
for idx, row in data.dropna(subset=['Latitud', 'Longitud']).iterrows():
    folium.Marker(
        location=[row['Latitud'], row['Longitud']],
        popup=f'Estudiante {idx + 1}',
        icon=folium.Icon(icon="info-sign")
    ).add_to(mapa_puebla)
mapa_puebla

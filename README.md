# puertos_paraguay
El presente repositorio contieene el archivo html para la descarga y visualización del mapa Mapa de puertos de Paraguay.

Ejemplo: archivo csv vinculado temporalmente.
A continuacion, se presenta el mapa con la localización de los puertos de Paraguay, creado mediante la libreria Folium de python. 
Para ejecutar el mismo, se empleo Google Colab (producto similar a Jupyter Notebook de Google Research. Un desarrollador de programas de Python puede usar este cuaderno para escribir y ejecutar códigos aleatorios de programas de Python simplemente usando un navegador web).

Sintaxis:

#Los archivos con datos pueden cargarse de forma temporal en la sesión de colab, para ello despliegue el icono de carpeta en el borde izquierdo de la pantalla y cargue el csv de interés.

import folium
from folium.plugins import MarkerCluster
import pandas as pd

#indico el url de los los datos
url='/content/puertos paraguay.csv'


#cargo el archivo dataframe
df=pd.read_csv(url)

#visualizo el encabezado
df.head()

#creo el mapa
mapa_puertos=folium.Map(location=[df['coord_y'].mean(), df['coord_x'].mean()], zoom_start=7)

#un cluster es una agrupacion de marcadores
cluster=MarkerCluster()

#itero sobre el dataframe agregando marcadores
for row in df.itertuples():
  row_id=str(dict(zip(df.columns,row[1:])))
  cluster.add_child(folium.Marker(location=[row.coord_y , row.coord_x], popup=row_id))

#agrego el cluster al mapa y lo guardo
mapa_puertos.add_child(cluster)
mapa_puertos.save('mapa de puertos paraguay.html')

#descargue el archivo 'mapa de puertos paraguay.html' de la carpeta temporal de la sesión y visualicelo con un navegador de internet.


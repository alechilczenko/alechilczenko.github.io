+++
title = "Escaneando el internet con Python"
date = "2022-04-05"
author = "Ale"
description = "¿Cómo podemos escanear gran parte de Internet en cuestión de horas? "
+++
 
Muchos buscadores como Google o Bing, son excelentes para indexar sitios web. Pero, ¿Y si quiero saber que países estan mas conectados? ¿O qué tecnologías web están siendo más utilizadas en una región? ¿O medir cuántos sistemas están expuestos?
 
Los buscadores web tradicionales no nos permiten responder estas preguntas, por lo que decidí implementar mi propia herramienta en Python.
 
## ¿Qué es Spidex?

Spidex es un escáner de reconocimiento continuo, que da prioridad a demostrar la exposición en la red. Realiza un escaneo orientado a puertos y recopila información de carácter público sobre cada dispositivo conectado a internet, como por ejemplo: la ubicación geográfica, tecnologías web y banners.

Para lograr una mayor eficiencia durante el escaneo, utiliza hilos y colas (Queue). De esta manera, las peticiones se envían en paralelo y se reduce notablemente el tiempo de ejecución para cada ciclo.

## ¿Qué son los banners?
 
Los banners son metadatos sobre un software que se ejecuta en un dispositivo. Puede ser información sobre el software del servidor, las opciones que admite el servicio, un mensaje de bienvenida o cualquier otra cosa que el cliente quiera saber antes de interactuar con el servidor. Por ejemplo, lo siguiente es un banner de FTP:
 
```
220 ProFTPD 1.3.5 Server
```
Esto nos indica el tipo de servidor FTP (ProFTPD) y su versión (1.3.5).
 
{{< image src="../escaner.png" position="center" style="border-radius: 8px;" >}}

## Almacenamiento de datos

El escáner envia los resultados a una API REST de Flask, que cuenta con una base de datos no relacional (MongoDB), su escalabilidad y flexibilidad nos permite manejar un gran volumen de información. Es ideal ya que los datos no son estructurados, los campos para cada documento pueden variar.

 
## Utilizando Elasticsearch y Kibana

Los documentos insertados en la base de datos se sincronizan periodicamente con Elasticsearch.
 
Elasticsearch es un motor de búsqueda que nos permite indexar de manera eficiente y en tiempo real los resultados.
 
Mientras que Kibana, es la interfaz gráfica para visualizar los datos de Elasticsearch y generar diversas estadísticas.
 
## Despliegue
El despliegue de las aplicaciones se realiza mediante Docker, por lo tanto podemos lanzar múltiples contenedores y evitar contaminar el entorno con dependencias.
 
{{< image src="../aws.png" position="center" style="border-radius: 8px;" >}}
 
## Resultados
Luego de varios dias probando, obtuve las siguientes estadísticas para Argentina
 
#### Ciudades más conectadas
{{< image src="../ciudad.png" position="center" style="border-radius: 8px;" >}}
 
#### Top organizaciones
{{< image src="../org.png" position="center" style="border-radius: 8px;" >}}
 
#### Tecnologías web más utilizadas
{{< image src="../tec.png" position="center" style="border-radius: 8px;" >}}


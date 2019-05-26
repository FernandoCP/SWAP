# Práctica 5: Replicación de bases de datos MySQL
## Fernando Calvillo Parejo

## Índice

0. ### [Objetivos](#0)
1. ### [Crear una BD e insertar datos](#1)
2. ### [Replicar una BD MySQL con mysqldump](#2)
3. ### [Replicación de BD mediante una configuración maestro-esclavo](#3)

<div id='0' />

## 0. Objetivos

En esta práctica el objetivo es configurar las máquinas virtuales para trabajar de forma que se mantenga actualizada la información en una BD entre dos servidores.Para ello, crearemos una BD con al menos una tabla y algunos datos, realizaremos la copia de seguridad de la BD completa usando mysqldump en la máquina principal y copiar el archivo de copia de seguridad a la máquina secundaria, después restauraremos dicha copia de seguridad en la segunda máquina (clonado manual
de la BD), de forma que en ambas máquinas esté esa BD de forma idéntica y finalmente, realizaremos la configuración maestro-esclavo de los servidores MySQL para que la replicación de datos se realice automáticamente.

<div id='1' />

## 1. Crear una BD e insertar datos

Para esta práctica lo primero que haremos es crear una nueva base de datos y unas pocas tablas y registros..                 

![imagen1](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/1.png)
![imagen1](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/2.png)
![imagen1](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/3.png)
       
En este caso hemos creado una base de datos y en ella una tabla "datos" con 2 columnas (nombre y telefono)

## 2. HAProxy

<div id='21' />

 #### Instalación de HAProxy
 
 Una vez creada la máquina y preparada de la misma manera que cuando [instalamos Nginx](#11) unicamente tendremos que ejecutar la siguiente orden:
 
    sudo apt-get install haproxy
 <div id='22' />

 #### Configuración de HAProxy
 Al igual que en la [configuracion de Nginx](#12) vamos a configurar HAProxy para definir balanceos alternando las peticiones entre los diferentes servidores usando el algoritmo *round-robin*.
Lo único que debemos hacer es modificar el archivo /etc/haproxy/haproxy.cfg que tendrá este aspecto:

![imagen5](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/HaproxyConfOLD.png)
Y deberemos dejarlo de la siguiente manera:

![imagen6](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/HPconfNEW.png)

Finalmente para lanzar el servicio HAProxy ejecutaremos el siguiente comando.

    sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg
 <div id='23' />
 
 #### Prueba de balanceo con HAProxy

 Para hacer la prueba de balanceo procederemos de la [misma manera que hicimos con Nginx](#13) usando la herramienta *curl* a la IP del balanceador que en este caso tiene la misma que el balanceador de Nginx *192.168.1.150*.
 
    curl http://192.168.1.150
 
![imagen7](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/BalanceoHP.png)
<div id='3' />

## 3. Prueba de la granja con alta carga

 Finalmente, vamos a probar nuestra granja web con una alta carga de peticiones. Para ello vamos a hacer uso de una nueva máquina y de la herramienta Apache Benchmark (ab) que viene instalada junto a apache. De esta forma unicamente tendremos que ejecutar la siguiente orden:

    ab -n 1000 -c 10 http://192.168.2.121/index.html
Los parámetros indicados en la orden anterior le indican al benchmark que solicite la página con dirección http://192.168.2.121/index.html 1000 veces (-n 1000 indica el número de peticiones) y hacer esas peticiones concurrentemente de 10 en 10 (-c 10 indica el nivel de concurrencia).

Y para apreciar como afectan las peticiones a las maquinas, tanto el balanceador como los servidores, ejercutaremos la orden: 

    top
 <div id='31' />
 
 #### Prueba con Nginx como balanceador
 
  Primero realizaremos la prueba con el balancedor que usa la herramienta Nginx y estos son los resultados:
 
 ![imagen8](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/nginxBenchmark.png)
 ![imagen9](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/nginxbenchamrk2.png)
 
 En la primera imagen podemos observar como el balanceador esta ejecutando Nginx con un 95% de la CPU y en la segunda las multiples llamadas a apache en uno de los servidores.
  <div id='32' />
 
 #### Prueba con HAProxy como balanceador
 
  De la misma manera haremos la misma prueba utilizando el balanceador que usa la herramienta HAProxy y los resultados son los siguientes:
  
 ![imagen10](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/BenchmarkHP.png)
 ![imagen11](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/BenchSWAP2HP.png)
  
  Nuevamente podemos observar en la primera imagen como el balanceador esta ejecutando HAProxy con un 92% de la CPU y en la segunda las multiples llamadas a apache en uno de los servidores.

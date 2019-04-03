# Práctica 3: Balanceo de carga
## Fernando Calvillo Parejo

## Índice

0. ### [Objetivos](#0)
1. ### [Nginx](#1)
    + #### [Instalación de Nginx](#11)
    + #### [Configuración de Nginx](#12)
    + #### [Prueba de balanceo con Nginx](#13)
2. ### [HAProxy](#2)
    + #### [Instalación de HAProxy](#21)
    + #### [Configuración de HAProxy](#22)
    + #### [Prueba de balanceo con HAProxy](#23)
3. ### [Prueba de la granja con alta carga](#3)
    + #### [Prueba con Nginx como balanceador](#31)
    + #### [Prueba con HAProxy como balanceador](#32)



<div id='0' />

## 0. Objetivos

En esta práctica vamos a configurar una red con varias máquinas en la que contaremos con un balanceador que reparta la carga entre 2 servidores finales. Para ello vamos a usar las 2 máquinas de las anteriores prácticas como servidores finales y ademas crearemos 3 máquinas más. 2 de esas nuevas máquinas las usaremos como blanceadores de carga entre los servidores finales, en una vamos a instalar y configurar la herramienta Nginx y en la segunda usaremos una alternativa a Nginx y en ella instalaremos y configuraremos HAProxy. Finalmente usaremos una última máquina para hacer un gran número de peticiones al balanceador y para ello usaremos la herramienta Benchmark Apache.

<div id='1' />

## 1. Nginx

<div id='11' />

 #### Instalación de Nginx
 
 En primer lugar crearemos una nueva máquina virtual, en mi caso he clonado una de las anteriores. Como esta máquina va a ser usada como balanceador de carga no podemos tener ningún software se apropie del puerto 80 para poder recibir peticiones HTTP desde fuera de la granja web. En nuestro caso al ser una máquina clonada tenemos instalado Apache2 de modo que lo desintalaremos con el comando siguiente:                        
       
    sudo apt purge apache2
Una vez hecho esto procederemos a instalar Nginx y unicamente tendremos que ejecutar los siguientes comandos:

    sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove
    sudo apt-get install nginx

<div id='12' />

 #### Configuración de Nginx
 
 Ahora que ya tenemos instalado Nginx lo siguiente es configurarlo para definir balanceos por round-robin, es decir, alternando las peticiones entre los diferentes servidores. Para ello, lo primero que vamos a hacer es modificar el fichero de
configuración */etc/nginx/conf.d/default.conf* de la siguiente manera:

![imagen1](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/nginxdefaultconf.png)

En mi caso no existía el archivo por tanto lo cree.

Y por último para iniciar el servicio haremos lo siguiente:

    sudo systemctl start nginx

 <div id='13' />
 
 #### Prueba de balanceo con Nginx
 
Con esta configuración hemos usado balanceo mediante el algoritmo de “round-robin” con la misma prioridad para todos los servidores. Para probarlo vamos a realizar peticiones con *curl* a la IP del balanceador que es *192.168.1.150* y, si todo es correcto, nos mostrara el archivo *index.html* de ambos servidores de forma alternativa. 
Pero antes vamos a realizar un cambio en los archivos *index.html* de los servidores para que se pueda ver facilmente. En mi caso, he hecho las siguientes modificaciones: 

![imagen2](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/IndexSWAP1.png)
![imagen3](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/indexSWAP2.png)

Una vez hecho esto vamos a ejecutar siguiente comando para ver que ocurre:

    curl http://192.168.1.150
Y el resultado es el siguiente:

![imagen3](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/BalanceoNGINX.png)

Como podemos ver realiza bien el balanceo y manda las peticiones de forma alternativa a los 2 servidores.
<div id='2' />

## 2. HAProxy

<div id='21' />

 #### Instalación de HAProxy
 
 Una vez creada la máquina y preparada de la misma manera que cuando [instalamos Nginx](#11) unicamente tendremos que ejecutar la siguiente orden:
 
    sudo apt-get install haproxy
 <div id='22' />

 #### Configuración de HAProxy
 
 <div id='23' />
 
 #### Prueba de balanceo con HAProxy


<div id='3' />

## 3. Prueba de la granja con alta carga

 <div id='31' />
 
 #### Prueba con Nginx como balanceador
 
  <div id='32' />
 
 #### Prueba con HAProxy como balanceador

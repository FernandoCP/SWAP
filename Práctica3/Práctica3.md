# Práctica 3: Balanceo de carga
## Fernando Calvillo Parejo

## Índice

0. ### [Objetivos](#0)
1. ### [Nginx](#1)
    + #### [Configuración e instalación de nginx](#11)
    + #### [Prueba de balanceo con Nginx](#12)
2. ### [HAProxy](#2)
    + #### [Configuración e instalación de HAProxy](#21)
    + #### [Prueba de balanceo con HAProxy](#22)
3. ### [Prueba de la granja con alta carga](#3)



<div id='0' />

## 0. Objetivos

En esta práctica vamos a configurar una red con varias máquinas en la que contaremos con un balanceador que reparta la carga entre 2 servidores finales. Para ello vamos a usar las 2 máquinas de las anteriores prácticas como servidores finales y ademas crearemos 3 máquinas más. 2 de esas nuevas máquinas las usaremos como blanceadores de carga entre los servidores finales, en una vamos a instalar y configurar la herramienta Nginx y en la segunda usaremos una alternativa a Nginx y en ella instalaremos y configuraremos HAProxy. Finalmente usaremos una última máquina para hacer un gran número de peticiones al balanceador y para ello usaremos la herramienta Benchmark Apache.

<div id='1' />

## 1. Nginx

<div id='11' />

 #### Configuración e instalación de nginx

<div id='12' />
 #### Prueba de balanceo con Nginx
 
 
<div id='2' />
## 2. HAProxy

<div id='21' />
 #### Configuración e instalación de HAProxy
 
 <div id='22' />
 #### Prueba de balanceo con HAProxy


<div id='3' />

## 3. Prueba de la granja con alta carga

![imagen1](https://github.com/FernandoCP/SWAP/blob/master/Práctica3/imagenes/Red.png)


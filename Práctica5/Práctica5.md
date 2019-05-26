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
![imagen2](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/2.png)
![imagen3](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/3.png)
![imagen4](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/4.png)
       
En este caso hemos creado una base de datos y en ella una tabla "datos" con 2 columnas (nombre y telefono)

<div id='2' />

## 2. Replicar una BD MySQL con mysqldump

Tenemos varias formas de replicar una base de datos, en nuestro caso realizaremos una copia en frío. En este tipo de copias de seguridad deberemos volcar todos los registros al disco y una vez hecho esto podremos apagar la base de datos para copiarla y así evitar perder la información de las transacciones en curso. Este tipo de copias de seguridad son las más sencillas y las más seguras, aunque es necesario apagar la base de datos, cosa que no siempre es posible.


![imagen5](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/5.png)
![imagen6](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/7.png)

Antes de recuperar la BDD deberemos crear otra con el mismo nombre en la segunda máquina.


![imagen7](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/8.png)

<div id='3' />

## 3. Replicación de BD mediante una configuración maestro-esclavo

Modificamos la configuración de MySQL en el maestro y el esclavo de forma que añadiremos las opciones para guardar el log y el bin, y para poder identificar el servidor.

![imagen8](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/9.png)

Seguidamente, creamos al usuario encargado de la replicación de la BDD en el esclavo.

![imagen9](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/10.png)

Una vez que ya tenemos la máquina 1 como esclavo, establecemos la máquina 2 como maestro que es la que tiene que replicar la base de datos.

![imagen10](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/11.png)

Finalmente, si realizamos un insert en el maestro, al consultar la tabla en el esclavo veremos reflejado el cambio.

![imagen11](https://github.com/FernandoCP/SWAP/blob/master/Práctica5/imagenes/13.png)





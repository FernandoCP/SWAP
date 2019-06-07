# Práctica 6: Servidor de disco NFS
## Fernando Calvillo Parejo

## Índice

0. ### [Objetivos.](#0)
1. ### [Configuración del servidor NFS.](#1)
2. ### [Configuración de los clientes.](#2)
3. ### [Automatización del proceso y pruebas.](#3)

<div id='0' />

## 0. Objetivos

En esta práctica el objetivo principal de esta práctica es configurar un servidor NFS para exportar un
espacio en disco a los servidores finales (que actuarán como clientes-NFS). Para ello vamos a configurar una máquina como servidor de disco NFS y exportar una carpeta a los clientes. Después de esto, montaremos en las máquinas cliente la carpeta exportada por el servidor. Y finalmente, comprobaremos que la información que se escribe en una máquina en dicha carpeta
se ve actualizada en el resto de máquinas que comparten ese espacio.

<div id='1' />

## 1. Configuración del servidor NFS
Para empezar instalaremos los paquetes necesarios con este comando:

`sudo apt-get install nfs-kernel-server nfs-common rpcbind`

Una vez hayamos instalado todo de forma correcta crearemos el directorio que vamos a compartir con los clientes, depsues cambiaremos el propietario y añadiremos todos los permisos.

![imagen1](https://github.com/FernandoCP/SWAP/blob/master/Práctica6/imagenes/crea.png)

Seguidamente editaremos el archivo de configuración _/etc/exports_ donde añadiremos las IPs que haran la función de cliente. 

![imagen1](https://github.com/FernandoCP/SWAP/blob/master/Práctica6/imagenes/arch.png)

Y por último reiniciaremos el servicio que el siguiente comando:

`sudo service nfs-kernel-server restart`

Con esto ya tendriamos configurado del servidor.

<div id='2' />

## 2. Configuración de los clientes

Ahora vamos a configurar ambos clientes, la configuración es exactamente la misma en los 2. Para empezar, lo primero que vamos a hacer es instalar los paquetes necesarios con el siguiente comando:

`sudo apt-get install nfs-common rpcbind`

Después de que se haya isntaldo todo correctamente procedemos a crear la carpeta que será nuestro punto de montaje y darle los permisos necesarios.

![imagen1](https://github.com/FernandoCP/SWAP/blob/master/Práctica6/imagenes/crea2.png)

Y con el siguiente comando montaremos la carpeta remota sobre el directorio recién creado:

`sudo mount 192.168.1.100:/dat/compartida carpetacliente`

El problema de esto es que cada vez que reiniciemos la máquina cliente tendremos que volver a monta la carpeta remota. Para solucionar esto vamos a hacer una pequeña configuración.

<div id='3' />

## 3. Automatización del proceso y pruebas.

Por último, para automatizar el proceso y evitar tener que montar todo cada vez que reiniciemos unicamente tenemos que añadir una línea al archivo de configuración _/etc/fstab_ para que la carpeta compartida se monte al iniciar el sistema.

`192.168.1.100:/dat/compartida /home/fernandocp/carpetacliente/ nfs auto,noatime,nolock,bg,nfsvers=3,intr,tcp,actimeo=1800 0 0`

![imagen1](https://github.com/FernandoCP/SWAP/blob/master/Práctica6/imagenes/ulti.png)

Finalmente, reiniciamos el sistema para comprobar que todo funciona de forma automatica.


![imagen1](https://github.com/FernandoCP/SWAP/blob/master/Práctica6/imagenes/4.png)


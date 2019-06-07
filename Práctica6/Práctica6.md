# Práctica 6: Servidor de disco NFS
## Fernando Calvillo Parejo

## Índice

0. ### [Objetivos](#0)
1. ### [Configurar el servidor NFS](#1)
2. ### [Configurar los clientes](#2)

<div id='0' />

## 0. Objetivos

En esta práctica el objetivo principal de esta práctica es configurar un servidor NFS para exportar un
espacio en disco a los servidores finales (que actuarán como clientes-NFS). Para ello vamos a configurar una máquina como servidor de disco NFS y exportar una carpeta a los clientes. Después de esto, montaremos en las máquinas cliente la carpeta exportada por el servidor. Y finalmente, comprobaremos que la información que se escribe en una máquina en dicha carpeta
se ve actualizada en el resto de máquinas que comparten ese espacio.

<div id='1' />

## 1. Configurar el servidor NFS
Para empezar instalaremos los paquetes necesarios con este comando:

`sudo apt-get install nfs-kernel-server nfs-common rpcbind`

Una vez hayamos instalado todo de forma correcta crearemos el directorio que vamos a compartir con los clientes, depsues cambiaremos el propietario y añadiremos todos los permisos.

![1](./capturas/directorio-permisos-1.PNG)

Ahora debemos editar el archivo de configuración _/etc/exports_ donde debemos añadir las IPs de las máquinas donde queremos exportar la carpeta.

![Configuración Exports](./capturas/exports-2.PNG)

Y finalmente reiniciamos el servicio:

`sudo service nfs-kernel-server restart`

![Restart](./capturas/restart-3.PNG)

### Montar en las máquinas cliente la carpeta exportada por el servidor.
Una vez configurada la máquina servidora en la máquina 1, configurare las máquinas 1 y 2 como clientes. _Se configuran las cosas paralelamente en ambas máquinas_

A la hora de montar la carpeta exportada, lo primero que debemos hacer es volver a instalar los paquetes necesarios.

`sudo apt-get install nfs-common rpcbind`

Después tenemos que crear la carpeta que será nuestro punto de montaje y darle los permisos necesarios.

![Creación de Carpeta Cliente](./capturas/directorio-permisos-4.PNG)

Y mediante la siguiente orden traspasamos la carpeta:

`sudo mount 192.168.1.100:/dat/compartida carpetacliente`

![Punto de Montaje](./capturas/traspasocarpeta-5.PNG)

### Comprobar que todas las máquinas pueden acceder a los archivos almacenados en la carpeta compartida.

Y vemos que podemos acceder a los mismos archivos desde ambas carpetas.

![Comprobación](./capturas/comprobacion-6.PNG)

### Hacer permanente la configuración en los clientes para que monten automáticamente la carpeta compartida al arrancar el sistema.

Finalmente, para poder hacer la configuración permanente y automatizar el proceso debemos añadir una línea de código al archivo de configuración _/etc/fstab_ para que la carpeta compartida se monte al iniciar el sistema.

`192.168.1.100:/dat/compartida /home/fernandocp/carpetacliente/ nfs auto,noatime,nolock,bg,nfsvers=3,intr,tcp,actimeo=1800 0 0`

![Configuración permanente](./capturas/fstab-7.PNG)

Reiniciamos el sistema que comprobamos que tenemos los mismos archivos en ambas máquinas.

![Todo en funcionamiento](./capturas/funciona-8.PNG)

Y como podemos comprobar todo funciona correctamente.

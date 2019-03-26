# Práctica 2: Replicar datos entre servidores
## Fernando Calvillo Parejo

**Los objetivos en esta práctica eran:** 

**• Aprender a copiar archivos mediante ssh.**

**• Clonar contenido entre máquinas.**

**• Configurar el ssh para acceder a máquinas remotas sin contraseña.**

**• Establecer tareas en cron.**

Siguiendo el tutorial he instalado 2 máquinas virtuales llamadas swap1 y swap2, respectivamente, con ubuntu server con una instalación por defecto. En la misma instalación instalamos LAMP y, posteriormente, ssh y curl.

Lo primero a realizar tras tener todo instalado es añadir un adaptador de red para la red interna en nuestras maquinas vistruales. 
![imagen](https://github.com/FernandoCP/SWAP/blob/master/Practica1/imagenes/Red.png)
modificar el documento /etc/network/interfaces añadiendle lo siguiente


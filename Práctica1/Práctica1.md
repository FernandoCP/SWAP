# Práctica 1
## Fernando Calvillo Parejo

**Los objetivos en esta practica eran principalmente 2:** 

**- El primero era la correcta instalacion de ambas maquinas y del LAMP.**

**- El segundo era conseguir la conectividad entre ambas maquinas tanto por curl, como por ssh.**

Siguiendo el tutorial he instalado 2 máquinas virtuales llamadas swap1 y swap2, respectivamente, con ubuntu server con una instalación por defecto. En la misma instalación instalamos LAMP y, posteriormente, ssh y curl.

Lo primero a realizar tras tener todo instalado es añadir un adaptador de red para la red interna en nuestras máquinas virtuales. 
![imagen1](https://github.com/FernandoCP/SWAP/blob/master/Práctica1/imagenes/Red.png)

Tras esto, nos vamos al documento /etc/network/interfaces y añadimos lo siguiente: 

#The secondary network interfaces

auto enp0s8

iface enp0s8 inet static

addres 192.168.1.100 <--- AÑADIMOS LA IP QUE QUERAMOS.

gateway 192.168.1.1

netmask 255.255.255.0

network 192.168.1.0

broadcast 192.168.1.255

Una vez hecho esto, hacemos un restart de la red de la máquina con el siguiente comando *"systemctl restart networking.service"* y con esto ambas máquinas quedan conectadas. En mi caso el comando anterior no me sirvío y el que yo utilicé fue *"/etc/init.d/networking restart"*.

Con el comando *ifconfig* podemos comprobar la información relativa a las interfaces de red como se muestra en la imagen.
![imagen2](https://github.com/FernandoCP/SWAP/blob/master/Práctica1/imagenes/ifconfig.png)

Y con el comando *ping + IPdelaotramáquina"* podemos comprobar que nuestras máquinas estan conectadas entre si.
![imagen3](https://github.com/FernandoCP/SWAP/blob/master/Práctica1/imagenes/conectadas.png)

Una vez llegado a aquí queremos acceder de una maquina a otra a través de *curl*. Para ello creamos un documento html en "/var/www/html/" y desde la otra máquina con el comando *"curl http://direccionIPdelservidor/hola.html"*
![imagen4](https://github.com/FernandoCP/SWAP/blob/master/Práctica1/imagenes/curl.png)

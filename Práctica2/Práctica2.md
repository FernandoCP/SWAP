# Práctica 2: Replicar datos entre servidores
## Fernando Calvillo Parejo

**Los objetivos en esta práctica eran:** 

**- Aprender a copiar archivos mediante ssh.**

**- Clonar contenido entre máquinas.**

**- Configurar el ssh para acceder a máquinas remotas sin contraseña.**

**- Establecer tareas en cron.**

### Copiar archivos mediante ssh.

En esta primera parte vamos a realizar la copia de ficheros y directorios de un equipo local a otro remoto. Para ello, vamos a hacer uso de la herramienta *"tar"* con la cual podemos comprimir y *"ssh"* que será lo que usemos para pasar los archivos.
Utilizaremos para hacerlo un único comando que realizara ambas operaciones. *"tar czf - directorio | ssh equipodestino 'cat > ~/tar.tgz'"*

![imagen](https://github.com/FernandoCP/SWAP/blob/master/Práctica2/img/TAR.png)

En la imagen podemos observar como se copia el archivo *"hola.tar.tgz"* de una máquina a la otra.


### Clonar contenido entre máquinas.

Para realizar la copia de contenidos de una máquina a otra vamos a hacer uso de la herramienta *"rsync"* la cual podemos instalar de forma sencilla con el comando *"sudo apt-get install rsync"* o bien desde su repositorio oficial.

EL uso de *rsync* para copiar carpetas de una máquina a otra remota es muy sencillo, tan solo utilizaremos el comando *"rsync -avz -e ssh ipmaquina:directorioacopiar directoriodondesecopia"*. Nos pedirá un password y tras ponerlo las carpetas de ambas máquinas quedaran idénticas. 
![imagen](https://github.com/FernandoCP/SWAP/blob/master/Práctica2/img/RSYNC.png)



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



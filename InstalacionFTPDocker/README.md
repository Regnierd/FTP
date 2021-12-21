# Instalación y administración de servidores de transferencia de archivos

![logo](https://github.com/Regnierd/FTP/blob/main/InstalacionFTPDocker/img/logo.png)

## Índice

- <a href="#1">1. Imagen Atmoz </a>
- <a href="#2">2. Verificar la imagen </a>
- <a href="#3">3. SFTP Multiusuario </a>

<a name="1"></a>

### 1. Imagen Atmoz
Para esta práctica usaremos la imagen de docker atmoz, para ello lo verificamos usando el comando <b>docker search sftp</b>, lo cual nos mostrará todas las imágenes con el nombre sftp.

![1](https://github.com/Regnierd/FTP/blob/main/InstalacionFTPDocker/img/1.PNG)

Usaremos la imagen que hemos nombrado anteriormente, atmoz, usando el comando: <b>sudo docker run –name mysftp -p 2294:22 -d atmoz/sftp admin:admin:::upload</b>

![2](https://github.com/Regnierd/FTP/blob/main/InstalacionFTPDocker/img/2.PNG)

<a name="2"></a>

### 2. Verificar la imagen
Verificamos que la imagen ha sido creada y el contenedor creado con el comando <b>sudo docker ps | grep sftp </b>

![3](https://github.com/Regnierd/FTP/blob/main/InstalacionFTPDocker/img/3.PNG)

Podemos comprobar el acceso al servidor ftp con el siguiente comando: <b>sudo docker inspect id-contenedor</b>

![4](https://github.com/Regnierd/FTP/blob/main/InstalacionFTPDocker/img/4.PNG)

<a name="3"></a>

### 3. SFTP Multiusuario
Si queremos tener varios usuarios para el uso de sftp una de las opciones es escribir en un fichero usuarios en el host y luego montarlo en el contenedor, como en el ejemplo que vemos en la imagen. 

![5](https://github.com/Regnierd/FTP/blob/main/InstalacionFTPDocker/img/5.PNG)

Luego para montarlo sería el siguiente comando que vemos en la imagen.

![6](https://github.com/Regnierd/FTP/blob/main/InstalacionFTPDocker/img/6.PNG)

# Instalación y administración de servidores de transferencia de archivos

![logo]()

## Índice

- <a href="#1">1. Instalar FTP </a>
- <a href="#2">2. Configurar el servidor FTP </a>
- <a href="#3">3. Instalación de Filezilla </a>
- <a href="#4">4. Seguridad TSL </a>

<a name="1"></a>

### 1. Instalar FTP
Para empezar la práctica necesitamos instalar el servicio de ftp, en nuestro caso usaremos vsftpd, con el comando <b>sudo apt install -y vsftpd</b> se instalará.

![1](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/1.png)

Comprobamos que el servicio está activo, con el comando <b> sudo systemctl status vsftpd</b>.

![2](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/2.PNG)

También debemos de activar el acceso a los puertos por defecto del servicio FTP, para ellos usaremos los dos siguientes comandos: <b>sudo ufw allow ftp</b> y <b>sudo ufw allow ftp-data</b>

![3](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/3.PNG)

<a name="2"></a>

### 2. Configurar el servidor FTP
Para configurar el servicio FTP, existe un fichero llamado vsftpd.conf, que lo puedes encontrar en /etc.

Por defecto FTP viene con el modo activo, lo que permitirá conexiones de clientes que no se encuentran tras un firewall. Para cambiarlo debemos de ir al fichero vsftpd.conf y activar el modo pasivo agregando 3 últimas líneas que vemos en la imagen.

![4](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/4.PNG)

Después de agregar las líneas anteriores debemos de actualizar el servicio, con el comando sudo systemctl reload vsftpd y agregar al firewall el rango de puerto que definimos anteriormente.

![5](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/5.PNG)

<a name="3"></a>

### 3. Instalación de Filezilla
Instalaremos un cliente FTP, en nuestro caso usaremos Filezilla. Cuando lo tengamos instalado, probamos a acceder al servidor, poniendo en el servidor la ip del servidor, nombre y contraseña local del servidor. Nos saldrá un mensaje diciendo que la conexión no es segura porque no tenemos activado la seguridad TSL.

![7](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/7.PNG)

Vemos como ya estamos conectados al servidor Ubuntu.

![8](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/8.PNG)

<a name="4"></a>

### 4. Seguridad TSL
Para activar la seguridad TSL debemos de usar las claves RSA con el comando openssl, para ello usaremos el siguiente comando:
<b>sudo openssl req -x509 -newkey rsa:2048 -days 3650 -nodes -out /etc/ssl/certs/daw.dpl.crt -keyout /etc/ssl/private/daw.dpl.key</b>

![9](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/9.PNG)

Ahora debemos de editar el fichero vsftpd.conf y cambiamos en la línea <b>ssl_enable</b> NO por YES para activar la seguridad SSL.

![10](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/10.PNG)

Reiniciamos el servicio.

![13](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/13.PNG)

Volvemos a Filezilla y comprobamos que ahora Filezilla se está conectando con la clave de seguridad RSA.

![11](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/11.PNG)

Y vemos que se conecta.

![12](https://github.com/Regnierd/FTP/blob/main/InstalacionFTP/img/12.PNG)

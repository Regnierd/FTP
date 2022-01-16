# Construccion de un servicio de empresa

![logo]()

## Índice

- <a href="#1">1. Requisitos previos </a>
- <a href="#2">2. Instalar PHP y Apache </a>
- <a href="#3">3. Comprobación de Apache </a>
- <a href="#4">4. Configuración del sitio web </a>
- <a href="#5">5. Añadiendo subdominio /sftp </a>
- <a href="#6">6. Creación del servicio SFTP </a>
- <a href="#7">7. Conexión al servidor SFTP Filezilla </a>
- <a href="#8">8. Añadiendo subdominio /phpmyadmin </a>

<a name="1"></a>

### 1. Requisitos previos
Para empezar esta práctica tendremos que tener un sistema operativo Linux, en nuestro caso usaremos Ubuntu 20.04. 

Instalaremos un servicio LAMP, agregando un servicio SFTP. Instalaremos Apache, PHP, MySQL, PHPMyAdmin y SFTP.

Para MySQL y PHPMyAdmin usaremos contenedores Docker, lo que quiere decir es que tendremos que tener instalado Docker y Docker-Compose.

<a name="2"></a>

### 2. Instalar PHP y Apache
Como hemos dicho anteriormente empezaremos a instalar Apache en nuestro equipo, con el comando <b>sudo apt install apache2</b>.

![1]()

Cuando acabe la instalación, procedemos a instalar PHP, usando el mismo comando anterior pero cambiando el nombre.

![2]()

Una vez acabada la instalación de PHP, comenzaremos a configurar Apache. Para ello activaremos el firewall de Apache. Usaremos los siguiente comando: <b>sudo ufw app list</b>  (para ver todos las aplicaciones que tenemos para activar), para activar Apache usaremos <b>sudo ufw allow ‘Apache’</b>.

![3]()

Para comprobar que se activó usaremos el comando <b> sudo ufw status</b>.

![4]()

<a name="3"></a>

### 3. Comprobación de Apache
Para comprobar que el servicio de Apache funciona correctamente, abrimos un navegador y escribimos en la URL <b>localhost</b>. Podemos ver que se abrió la página principal de Apache2.

![5]()

Para poder acceder con el dominio que nos pidió el cliente (www.nombresystem.com) tendremos que agregarlo al sistema como localhost. Para ello iremos al archivo<b> /etc/hosts</b> y lo agregamos.

![6]()

<a name="4"></a>

### 4. Configuración del sitio web
A continuación es la hora de configurar nuestro sitio web. Crearemos un archivo en la siguiente ruta <b>/etc/apache2/sites-available</b> donde van todos nuestros sitios web que queramos. 

![7]()

En el nuevo fichero escribimos el siguiente código que vemos en la imagen.

![8]()

Después de crear el fichero anterior tendremos que habilitar el fichero en otro directorio, para que el servicio de Apache pueda trabajar con él. Usaremos el siguiente comando: <b>sudo a2ensite nombresystem.conf</b>.

![9]()

Por último, tendremos que reiniciar el servicio de Apache, para ello usaremos el siguiente comando: <b>sudo systemctl restart apache2</b>.

![10]()

Comprobamos el estado del servicio.

![11]()

Ahora volvemos al navegador y escribimos en la URL que definimos anteriormente, para poder comprobar que ha detectado nuestro nuevo dominio.

![12]()

Para tener algo que mostrar en el navegador, crearemos un fichero .html en la ruta que pusimos en el fichero anterior: <b>/var/www/javierlpsystem</b>. Tendremos el siguiente código html.

![13]()

Una vez hecho esto volvemos al navegador y recargamos la página y nos debería de mostrar lo que pusimos en el fichero .html.

![14]()

<a name="5"></a>

### 5. Añadiendo subdominio /sftp
Como el cliente nos ha pedido un subdominio con los ficheros que tenemos en el sistema para poder verlos, tendremos que crear un nuevo alias y asignarle el directorio especificado como veremos en la siguiente imagen. En nuestro caso el alias será <b>/sftp</b> el cual apuntará al directorio <b>“/var/www/javierlpsystem/sftp”.</b>

![15]()

Volvemos a reiniciar el servicio de Apache para que se apliquen los cambios.

![16]()

Vamos al navegador y agregamos a la URL www.javierlp.com/<b>sftp</b> y podremos ver todos los ficheros que se encuentran dentro del directorio que especificamos anteriormente.

![17]()

<a name="6"></a>

### 6. Creación del servicio SFTP
Como el cliente también quiere tener un servicio para transferir archivos usaremos el servicio <b>SFTP</b>. Para ello instalaremos<b> vsftpd</b> que es el servicio seguro de <b>FTP</b>.

![18]()

Una vez instalado, comprobamos que está activo y funcionando correctamente.
Usaremos el comando: <b>sudo systemctl status vsftpd.service</b>

![19]()

Ahora ya podremos acceder al servicio SFTP con el siguiente comando: <b>sftp usuario@ip-servidor.</b>

![20]()

<a name="7"></a>

### 7. Conexión al servidor SFTP Filezilla
Ahora desde un ordenador diferente podemos comprobar si podemos acceder al servicio SFTP mediante un software específico para estos casos, usaremos Filezilla.

Para que podamos acceder directamente al directorio que solo puede acceder el usuario mediante el servicio SFTP, tendremos que configurar un archivo de ssh, asignando directamente la ruta del directorio y agregando las siguiente líneas al fichero.

![21]()

Una vez hecho esto, abrimos Filezilla y rellenamos los campos para poder acceder al servidor. En el servidor tendremos que poner sftp://ip-servidor, un nombre de usuario y la contraseña. Como podemos comprobar que se conecta al servidor y estamos en la ruta sftp, ya que abajo a la derecha nos sale el archivo index.php.

![22]()

<a name="8"></a>

### 8. Añadiendo subdominio /phpmyadmin
Por último, el cliente nos ha pedido un gestor de base de datos gráfico, el cual tendremos PHPMyAdmin y la base de datos estará corriendo en MySQL. Como hemos dicho al principio usaremos Docker-Compose, para tener dos contenedores que tengan los dos servicios requeridos. Levantamos los dos contenedores y vemos como están activos.

![23]()

Para poder acceder al gestor gráfico PHPMyAdmin, tendremos que actualizar el archivo de Apache de nuestro sitio web. Agregaremos la siguiente línea de comando.

![24]()

Volvemos a resetear el servicio.

![25]()

Volvemos a nuestro navegador y colocamos en la URL <b>www.javierlpsystem.com/phpmyadmin</b> y nos debería de salir el login para poder acceder al servicio.

![26]()




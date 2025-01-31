# Instalaci-n-de-Wordpress

WordPress es una plataforma de gestión de contenidos, representa un software de código abierto altamente versátil que permite a los usuarios crear y desarrollar sitios web personalizados de manera sencilla, adaptable y profesional, con una muy buena experiencia de usuario.

## Pre-requisitos

- Permiso sudo o root
- Instalar PHP 5.6 o superior
- Instarlar MySQL 5.7 o superior

### Nos ubicamos en la ruta publica de APACHE

`cd /var/www/html`

### Descargamos la última versión de WordPress

`wget http://wordpress.org/latest.tar.gz`

### Descomprimimos los archivos

`tar -xzvf latest.tar.gz`

### Creamos la estructura de directorios y permisos para WordPress
Para ello nos dirigimos a la carpeta WordPress

`cd /var/www/html/wordpress`

- Creamos un directorio donde subiremos archivos a WordPress

`mkdir /var/www/html/wordpress/wp-content/uploads`

- Cambiamos el propietario de los directorios de la ruta pública con el usuario APACHE de manera recursiva

`sudo chown -R apache:apache /var/www/html/*`

- Cambiamos los permisos de lectura y escritura

`chmod -R 777 /var/www/html/wordpress`

### Creamos una base de datos y usuario

`create database wordpress;`

- Ahora creamos un usuario

`CREATE USER 'user'@'localhost' IDENTIFIED BY 'passuser';`

- Damos permisos a la base de datos

`GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost';`

- Recargamos permisos de usuario

`GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost';`

- Y salimos de MySQL

`exit`

### Configuramos WordPress con los datos antes creados, nos dirigimos a este directorio

`cd /var/www/html/wordpress`

- Cambiamos el nombre del archivo de configuración y a la vez hacemos una copia

`cp wp-config-sample.php wp-config.php`

- Abrimos el archivo wp-config.php:

`sudo nano wp-config.php`

_Colocamos el nombre de la base de datos, el usuario y la contraseña_


En el mismo archivo modificamos las llaves de autentificación, para esto iremos a esta dirección:
https://api.wordpress.org/secret-key/1.1/salt/, copiamos los datos y lo cambiamos por los del archivo que tenemos abierto. Guardamos los cambios del archivo que modificamos.

### Configuramos virtual host Apache
Nos dirigimos a esta ruta:

`cd /etc/httpd/conf.d`

- En este directorio podemos encontrar todas las configuraciones de las aplicaciones que usan apache, creamos el siguiente archivo:

`sudo nano wordpress.conf`
- Agregamos estos datos en el archivo:

`<VirtualHost *:80>
ServerAdmin root@localhost 
DocumentRoot /var/www/html/wordpress 
<Directory #/var/www/html/wordpress/#> 
AllowOverride All 
Require all granted 
</Directory> 
</VirtualHost>`

- Reiniciamos

`sudo systemctl restart httpd`

- Ponemos en el navegador nuestra ip más /wordpress y nos aparecerá lo siguiente

![Captura de pantalla 2025-01-18 234107](https://github.com/user-attachments/assets/7335f3d6-322d-4d69-a0c4-43cf20683b4b)


- Ahora colocamos los datos que nos pidan, para la instalación de WordPress.

![Captura de pantalla 2025-01-18 234443](https://github.com/user-attachments/assets/6bceeeb1-8ef6-4514-9bc0-5036530afcd2)

Con estos pasos ya se tiene instalado WordPress y estará listo para empezar a configurar. [1]

### Referencias

[1]
Hostinglabs. “Como instalar WordPress desde la línea de comandos de Linux”. Hostinglabs. Accedido el 2 de enero de 2025. [En línea]. Disponible: https://hostinglabs.net/asistencia/base-de-conocimientos/como-instalar-wordpress-desde-la-linea-de-comandos-de-linux/

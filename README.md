# LAMP & Wordpress 🌐

 Guía de como instalar **LAMP y WORDPRESS**.

## INDEX
- [Linux](#LINUX)
- [Apache](#APACHE)
- [MySQL](#laMp)
- [PHP](#lamP)
- [WordPess](#WordPress)

## LINUX🐧
[Vuelve arriba 👆](#Linux)

Debes de estar utilizando Linux, yo lo he instalado en Ubuntu 24.04 y en mint 22.

## APACHE 🌐
[Vuelve arriba 👆](#Apache)

Apache es el servicio web que utilizaremos para ejecutar wordpress de manera web, para instalarlo:

```bash 
sudo apt install apache2 
```

## MySQL 📂

[Vuelve arriba 👆](#lAmp)

MySQL es el gestor de base de datos que utilizaremos, MySQL.

Para instalarlo:
```bash
sudo apt install mysql-server
```

Una vez instalado, tendremos que entrar como root para:

1. Otorgarle permisos al usuario principal.

2. Crear una BDD para cuando instalemos wordpress.


Para otorgarle los permisos al usuario root de mysql, primero entrar a root:

```bash
sudo -i
```

Una vez en root, crea un archivo, en la ruta que quieras, yo lo pondre en '/' y con tu editor favorito, escribiras en un archivo el siguiente texto:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY '1234321'; 
``` 

Lo guardaremos con el nombre que queráis y ejecutaremos el comando para activar ese script:

```bash
sudo mysqld --init-file=/mysql-init &
```

Y reiniciamos el servicio de mysql:

```bash
sudo systemctl restart mysql.service
```

Y para entrar:

```bash
mysql -p
```

Una vez dentro de mysql:
    1. Crear la base de datos para wordpress y darle los permisos al root para poder entrar.
    2. Crear al usuario local para no utilizar el de root.

Crear la base de datos para WordPress:

```mysql
CREATE DATABASE wordpress;
```

Crear el usuario:
```mysql
CREATE USER 'user'@'localhost' IDENTIFIED BY 'passwd';
```

Darle los permisos de todo:
```mysql
GRANT ALL PRIVILEGES ON *.* TO 'user'@'localhost';
```
Para salir utilizaremos:
``mysql
exit
``

Ahora si tienes algun problema o quieres crear tu propia BDD puedes entrar con el usuario que acabas de crear.

## PHP

[Vuelve arriba 👆](#lamP)

PHP es el lenguaje de programacion que utilizara Wordpress, asi que hace falta conectarlo con el [servicio web](#Lamp) y [MySQL](#laMp)

```bash
sudo apt install php php-mysql libapache2-mod-php
```

Una vez creado la BDD de wordpress, instalado LAMP y configurado MySQL para poder entrar desde un usuario propio, y el lemguaje de programacion que utiliza WordPress instalamos el comprimido de Wordpress.


## WORDPRESS

[Vuelve arriba 👆](#WordPress)
Entramos a la carpeta de publicacion de Apache2, donde esta configurado por defecto los archivos de ejecucion del servicio

```bash
cd /var/www/html/
```

E instalamos el comprimido

```bash
sudo get https://wordpress.org/latest.tar.gz
```
Descomprimimos

```bash
sudo tar -xvzf ./latest.tar.gz
```

Una vez descomprimido, entramos a la carpeta


```bash
cd wordpress/
```
copiamos el archivo **wp-config-sample.php**

```bash
sudo cp wp-config-sample.php wp-confi.php
```

Entramos con nuestro editor de texto favorito y reemplazamos las siguientes.

OJO, DONDE PONGA **HERE** si no aparece en la linea, no se toca


```php
define( 'DB_NAME', 'database_name_here' );

define( 'DB_USER', 'username_here' );

define( 'DB_PASSWORD', 'password_here' );

```
Acuerdate que son con lo datos que hemos creado antes al instalar mysql, ese user, passwd y BDD

Y mas abajo de estas lineas, estan las lineas de autenticacion, que tendremos que reemplazar los la de la api que proporciona el archivo, o si quieres entrar mas facil
[a este enlace](https://api.wordpress.org/secret-key/1.1/salt/) que dirige al mismo sitio, con ese texto borramos las lineas de debajo ("define(...)")

Wordpress en si no estaria instalado del todo, pero ya casi, reiniciamos el servicio web

```bash
sudo systemctl restart apache2
```

Y si entramos a nuestro navegador de la siguiente manera

**http://localhost/wordpress**

Continua los pasos ya podras empezar

## Y a disfrutar!! 

PD: Una vez instalado, para entrar en administrador del wordpress y no en la pagina para ver, entra en la subcarpeta "wp-admin":

**http://localhost/wordpress/wp-admin**


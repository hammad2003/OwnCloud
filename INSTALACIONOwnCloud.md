# OwnCloud

# Instalación del contenedor

Para instalar el contenedor procedemos a poner el siguiente comando junta al nombre y la versión del SO que queremos instalar.

```
lxc launch ubuntu:20.04 elmeucontenidor
```

## Encender el contenedor
Para encender nuestro contenedor procedemos a realizar el siguiente comando.

```
lxc start elmeucontenidor
```

## Ejecutar el contenedor
Una vez ya encendido, vamos a ejecutarlo con el siguiente comando.

```
lxc exec elmeucontenidor bash
```

## Instalar apache2, mysql y algunas librerías en el contenedor

Cuando ya hayamos entrado dentro vamos a proceder a actualizar el listado de paquetes y a descargar y instalar el `apache2`, `mysql` y algunas `librerías` para que todo funcione correctamente.

```
 apt update
 apt upgrade
 apt install apache2
 apt install mysql-server
 apt install php libapache2-mod-php
 apt install php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```

## Configuramos apache2

Activamos el módulo `proxy_fcgi`:

```
a2enmod proxy_fcgi
```

Activamos la configuración de `php-fpm`:

```
a2enconf php-fpm
```

Reiniciamos el servidor:

```
systemctl restart apache2
```

## Creamos una base de datos y un usuario en MySQL


Accedemos a `MySQL` con el usuario `root`

```
mysql -u root
```

Creamos la base de datos con el nombre que desee, en mi caso `mibasededades`

```
CREATE DATABASE mibasededades;
```

Creamos un usuario llamado `miusuario`, le ponemos el password `mipassword` y le damos privilegios sobre nuestra base de datos `mibasededades`

```
CREATE USER 'miusuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

```
GRANT ALL DONDE mibasededades.* to 'miusuario'@'localhost';
```

```
exit
```

Comprobamos que todo ha funcionado bien

```
mysql -u mi usuario -p
```

## Descomprimir el archivo .zip
Para poder descomprimir nuestro archivo .zip realizaremos los siguientes comandos.

```
apt update

apt install unzip

cd /var/www/html

wget https://download.owncloud.org/community/owncloud-complete-20210721.zip

unzip owncloud-complete-20210721.zip
```

## Accedemos al instalador de la aplicación mediante el navegador web
Primero averiguamos nuestra IP y después esta la ponemos en nuestro navegador.

```
ip -c a

También puedes ver la IP del contenedor haciendo `lxc list` des de fuera del contenedor.

http://10.161.122.237 (en el navegador)
```

# OwnCloud

# Instal·lació del contenidor
```console
lxc launch ubuntu:20.04 elmeucontenidor
```

## Engegar el contenidor (si està aturat)
```console
lxc start elmeucontenidor
```

## Executar el contenidor
```console
lxc exec elmeucontenidor bash
```

## Instal·lar apache2, mysql i algunes llibreries al contenidor

```console
 apt update
 apt upgrade
 apt install apache2
 apt install mysql-server
 apt install php libapache2-mod-php
 apt install php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```

## Configurem apache2

Activem el mòdul `proxy_fcgi`:
```console
a2enmod proxy_fcgi
```

Activem la configuració de `php-fpm`:
```console
a2enconf php-fpm
```
Reiniciem el servidor:
```console
systemctl restart apache2
```

## Creem una base de dades i un usuari al MySQL


Accedim al `MySQL` amb l'usuari `root`
```console
mysql -u root
```

Creem la base de dades amb el nom que volgueu, en el meu cas `lamevabasededades`
```console
CREATE DATABASE lamevabasededades;
```

Creem un usuari anomenat `elmeuusuari`, li posem el password `elmeupassword` i li donem privilegis sobre la nostra base de dades `lamevabasededades`

```console
CREATE USER 'elmeuusuari'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
```console
GRANT ALL ON lamevabasededades.* to 'elmeuusuari'@'localhost';
```
```console
exit
```

Comprovem que tot ha funcionat bé
```console
mysql -u elmeuusuari -p
```
També pots veure la IP del contenidor fent `lxc list`

## Descomprimir el archiu .zip

```
apt update

apt install unzip

cd /var/www/html

wget https://download.owncloud.org/community/owncloud-complete-20210721.zip

unzip owncloud-complete-20210721.zip
```
## Accedim a l'instal·lador de l'aplicació mitjançant el navegador web
Primer averiguem la nostra ip i despres aquesta la posem en el nostre navegador

```
ip -c a

http://10.161.122.237 (en el navegador)
```

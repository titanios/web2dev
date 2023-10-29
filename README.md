Docker Web-Dev Environment
--------------------------
This small repository is my first attempt to create my own web development environment under docker.

This setup contains the following containers:

- nginx:alpine
- php:fpm-alpine

This both containers are linked through the default configurations. Every php file which will be called via nginx will be interpreted by php-fpm

You can also directly call php-fpm with the following lines:

```
SCRIPT_NAME=your-file.php \
SCRIPT_FILENAME=./src/your-file.php \
REQUEST_METHOD=GET \
cgi-fcgi -bind -connect 172.20.0.3:9000
```
To execute this command you have to install:

```
apt-get install libfcgi0ldbl
```

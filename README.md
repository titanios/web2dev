Docker Web2Dev Environment
--------------------------
A small docker container for your local dev environment, containing latest nginx & php-fpm alpine image. It's easy to handle, so you can focus on your application.

This setup contains the following images:

- nginx:alpine
- php:fpm-alpine

This both images are linked through the default configurations. Every php file which will be called via nginx will be interpreted by php-fpm.

### Installation

Before you set up this dev environment via docker, you have to adapt the docker compose file, so the volumes match with your project path.

After this, run the following command:

```
docker compose up
```

You can also directly call php-fpm with the following lines:

```
SCRIPT_NAME=<your-script-name> \
SCRIPT_FILENAME=<./src/your-file.php> \
REQUEST_METHOD=GET \
cgi-fcgi -bind -connect <your-docker-gateway:9000>
```
To execute this command you have to install:

```
apt-get install libfcgi0ldbl
```

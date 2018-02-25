# php7-apache-symfony
Docker image tailored to run PHP application. Check https://hub.docker.com/r/touch4it/php7

## What's here?

This repository is a source code for following Docker images that allow relatively easily work with PHP frameworks. Included images:

* Debian + Apache + mod_php
  * touch4it/php7:php7-apache
  * touch4it/php7:php7.1-apache
  * touch4it/php7:php7.2-apache
* Alpine + Nginx + PHP-FPM
  * touch4it/php7:php7.2-fpm-nginx

# Usage

## Development env with docker-compose.yml

You can you this docker-compose.yml file to develop:

```
www:
  image: touch4it/php7:php7
  volumes:
    - ".:/var/www/html"
  ports:
    - "80"
```
Of course you are free to add linked containers like database, caching etc.

Use ```docker-compose up``` command to start your development environment.

## Build production image

You can build production ready image with Dockerfile like this:

```
FROM touch4it/php7:php7
ADD . /var/www/html
```

## Environment variables

This image uses several environment variables which are easy to miss. While none of the variables are required, they may significantly aid you in using the image.

### `ADMIN_EMAIL`

The ServerAdmin sets the contact address that the server includes in any error messages it returns to the client.
If the httpd doesn't recognize the supplied argument as an URL, it assumes, that it's an email-address and prepends it with `mailto:` in hyperlink targets.
However, it's recommended to actually use an email address, since there are a lot of CGI scripts that make that assumption.
If you want to use an URL, it should point to another server under your control. Otherwise users may not be able to contact you in case of errors.

Default value: `webmaster@localhost`

For Apache-based images

### `PHP_TIME_ZONE`

Defines the default timezone used by the date functions

http://php.net/date.timezone

Default value: `Europe/London`

### `PHP_MEMORY_LIMIT`

Maximum amount of memory a script may consume

http://php.net/memory-limit

Default value: `256M`

### `PHP_UPLOAD_MAX_FILESIZE`

Maximum allowed size for uploaded files.

http://php.net/upload-max-filesize

Default value: `32M`

### `PHP_POST_MAX_SIZE`

Maximum size of POST data that PHP will accept.
Its value may be 0 to disable the limit.
It is ignored if POST data reading is disabled through enable_post_data_reading.

http://php.net/post-max-size

Default value: `32M`

# FAQ

## What extensions are enabled by default?

### Apache

* mod_rewrite

For Apache-based images

* mod_http2

for Apache 2.4.26+ based images

### PHP

* exif
* gd
* intl
* mbstring
* opcache
* pgsql
* pdo
* pdo_mysql
* pdo_pgsql
* zip

## How do i install additional php extensions?
This work is based on official Docker Hub `php` images. You can use docker-php-ext-install to add new extensions. More information can be found https://hub.docker.com/_/php/

## How do I change default PHP variables?
You can add an ini file into `$PHP_INI_DIR/conf.d` directory 

## Why is my .htaccess file not working?
Check if you have not selected Nginx-based image

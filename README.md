# Docker PHP-FPM WordPress optimized

Based on Repository: https://github.com/TrafeX/docker-php-nginx

* Built on the lightweight and secure Alpine Linux distribution
* Multi-platform, supporting AMD4, ARMv6, ARMv7, ARM64
* Very small Docker image size (+/-40MB)
* The services Nginx, PHP-FPM and supervisord run under a non-privileged user (nobody) to make it more secure
* The logs of all the services are redirected to the output of the Docker container (visible with `docker logs -f <container name>`)
* Follows the KISS principle (Keep It Simple, Stupid) to make it easy to understand and adjust the image to your needs

## Usage
Build the image:

    docker build -t organization/your-image-tag .

Start the Docker container:

    docker run -p 80:8080 <your-image-tag>

See the PHP info on http://localhost, or the static html page on http://localhost/test.html

Or mount your own code to be served by PHP-FPM & Nginx

    docker run -p 80:8080 -v ~/my-codebase:/var/www/html <your-image-tag>

## Configuration
Nginx configuration:

    docker run -v "`pwd`/nginx-server.conf:/etc/nginx/conf.d/server.conf" trafex/php-nginx

PHP configuration:

    docker run -v "`pwd`/php-setting.ini:/etc/php83/conf.d/settings.ini" trafex/php-nginx

PHP-FPM configuration:

    docker run -v "`pwd`/php-fpm-settings.conf:/etc/php83/php-fpm.d/server.conf" trafex/php-nginx

_Note; Because `-v` requires an absolute path I've added `pwd` in the example to return the absolute path to the current directory_


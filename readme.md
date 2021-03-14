At this point this is just a copy of [Laravel Sail](https://laravel.com/docs/8.x/sail) but it's using nginx.

## PHinx
Simple lightweight container including nginx, php, composer & npm based on Alpine Linux

## Usage
* git clone this into your project
* move the docker-compose file to your project root
* set the environment variables (if you don't do this we will use default values)
* configure nginx 
* run docker-compose up

By default, you will get a mysql instance when you run docker-compose up. If you don't need a database you can comment this piece of code.

You can edit the dockerfile to adjust it to your needs.

## Troubleshooting
* Check the build context path in docker-compose file

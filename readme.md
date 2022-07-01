## PHinx
PHP-FPM, Nginx & MySQL

## Usage
* git clone this into your project
* copy the docker-compose file to your project root
* set the environment variables (if you don't do this we will use default values)
* configure nginx
* run ```docker-compose up```

By default, you will get a mysql instance when you run docker-compose up. If you don't need a database you can comment this piece of code.

If you need redis you can just uncomment the block in the docker-compose file.

You can edit the dockerfile to adjust it to your needs.

The php container comes pre-installed with composer, npm and yarn.

#### Want to start a new project but don't have composer installed?
```bash
docker run --rm --interactive --tty \
  --volume $PWD:/app \
  composer <command>
```

```bash
docker run --rm --interactive --tty \
  --volume $PWD:/app \
  composer create-project laravel/laravel example-project
```

## Troubleshooting
* Check the build context path in docker-compose file
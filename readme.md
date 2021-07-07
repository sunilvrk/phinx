## PHinx
PHP-FPM, Nginx & MySQL

## Usage
* git clone this into your project
* copy the docker-compose file to your project root
* set the environment variables (if you don't do this we will use default values)
* configure nginx
* run ```docker-compose up```

By default, you will get a mysql instance when you run docker-compose up. If you don't need a database you can comment this piece of code.

You can edit the dockerfile to adjust it to your needs.

#### There is no composer installed in the php container. If you need composer just use it the docker way:
```bash
docker run --rm --interactive --tty \
  --volume $PWD:/app \
  composer <command>
```

## Troubleshooting
* Check the build context path in docker-compose file
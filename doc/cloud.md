Deploying a cloud
=================

The following is an idea/attempt to deploy an cloud.

> Since `aap` is still in beta, this illustrates a `desired yet incomplete workflow`

## Usecase

    $ git clone https://github.com/username/my.aap.git && cd my.aap
    $ aap install
    Rebuilding docker 'mysql'
    Rebuilding docker 'mongodb'
    Rebuilding docker 'apache'
    $ aap start 
    Starting docker core-api    on 'https://coreapi.foobar.com' => 'http://0.0.0.0:3454'
    Starting docker crm-api     on 'https://crm.foobar.com'     => 'http://0.0.0.0:3455'
    Starting docker landingpage on 'https://www.foobar.com'     => 'http://0.0.0.0:3456'
    Starting docker backend     on 'https://manager.foobar.com' => 'http://0.0.0.0:3457'
    Starting docker workers 

## How

using docker-compose or (my favorite tool) [crowdr](https://github.com/polonskiy/crowdr).
If we assume crowdr, a possible aap.json could look like this:

    {
      "name": "foobar",
      "version": "1.0.0",
      "description": "",
      "website": "https://foobar.com",
      "repository": "https://github.com/jane-doe/small-sharp-tool",
      "logo": "https://small-sharp-tool.com/logo.svg",
      "scripts": {
        "postinstall": ["install_modules"]
        "postdeploy": ["start"],
        "start": ".crowdr/crowdr start",
        "stop": ".crowdr/crowdr stop",
        "build": ".crowdr/crowdr build",
        "backup": "zip -r data-`date +`.zip data",
        "test": "echo "Error: no test specified" && exit 0",
        "install_modules":"which npm && npm install; which composer && composer install"
      },
      "dependencies":{
        "crowdr:.crowdr":"git@github.com:polonskiy/crowdr.git",
        "docker.mysql:docker/mysql": "git@github.com:username/docker.mysql.git",
        "docker.mysql:docker/apache": "git@github.com:username/docker.apache.git"
      },
      "env": {
        "ADMIN_PASSWD": {
          "description": "A secret key for verifying the integrity of signed cookies.",
          "file": "data/.pw"
        },
        "WEB_CONCURRENCY": {
          "description": "The number of processes to run.",
          "value": "5"
        }
      },
      "devDependencies":{
      },
      "author": "",
      "license": "ISC"
    }

With a crowdr `.crowdr/config` like this:

    #!/bin/bash

    HOST="$(tr -d '-' <<< $HOSTNAME)"
    PREFIX="foo"

    echo "
    global project ${USER}_${HOST}_myproject

    mysql build docker/mysql
    mysql hostname $PREFIX-mysql
    mysql volume $PWD/mysql-data:/var/lib/mysql

    #comment

    apache build docker/apache
    apache hostname $PREFIX-apache
    apache memory 5g
    apache link mysql
    apache volume $PWD:/var/www
    apache env-file config.env
    "

> WARNING: this is obviously incomplete when looking at the Usecase, but it could be a startingpoint

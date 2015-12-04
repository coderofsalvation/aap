<img alt="" src="doc/logo.jpg"/>

> NOTE: beta

In the beginning there was bash..and bash had aap.json

![Build Status](https://travis-ci.org/coderofsalvation/aap.svg?branch=master)

## Usage

    $ git clone https://github.com/username/my.aap.git && cd my.aap
    $ aap install
    Rebuilding docker 'mysql'
    Rebuilding docker 'mongodb'
    Rebuilding docker 'apache'
    $ aap start 
    Starting core-api    on 'https://coreapi.foobar.com' => 'http://0.0.0.0:3454'
    Starting crm-api     on 'https://crm.foobar.com'     => 'http://0.0.0.0:3455'
    Starting landingpage on 'https://www.foobar.com'     => 'http://0.0.0.0:3456'
    Starting backend     on 'https://manager.foobar.com' => 'http://0.0.0.0:3457'
    Starting workers 
   
## Getting started 

If you're used to `npm` or `composer`, you will feel right at home.
Lets start a project:

    $ git init 
    $ aap init

> aap.json is now generated (click [here](doc/aap.json) 

Lets add dependencies to our project:

    $ aap install ssh+git://user@bitbucket.org/username/backend.git     --save
    $ aap install ssh+git://user@github.com/username/core-api.git       --save
    $ aap install ssh+git://user@bitbucket.org/username/landingpage.git --save
    $ aap install ssh+git://user@github.com/username/crm-api.git        --save
    $ aap install ssh+git://user@github.com/username/docker.mysql.git   --save
    $ aap install ssh+git://user@github.com/username/docker.mongodb.git --save
    $ aap install npm://css2js --save 
    $ aap install composer://myphppackage --save 
    $ mkdir python
    $ cd python && ../../aap install pip://mypythonpackage --save 

Now lets push our buildpack to the repo:

    $ git add app.json && git commit -m "added aap manifest"
    $ git push origin master

Congrats! Now other devs can easily run `aap install`.

## Installation

    npm install aap.bash

or 

    wget "https://raw.githubusercontent.com/coderofsalvation/aap/master/aap" -O aap
    chmod 755 aap

## Why

Now you can easily manage dependencies of gitrepos, npm/composer modules and dockerrepos.
All combined in one slim repo.

Basically `aap init` generates `aap.json` like [this](doc/aap.json), which allows you to run:

    $ aap install

Get any system to build a project from multiple remote sources.

> Only requirements: git + bash

## Options 

     $ aap
     Usage: aap <cmd> [options]
     
     aap.json Buildpacks for the web.
     Easily manage dependencies of gitrepos, npm/composer modules and dockerrepos.
     Combine a composable cloud in one slim repo.

     Commands:

       aap init [name] [options]          ┆ generates aap manifest, options:
                                          ┆ -f = force, overwrites json

       aap install [url] [..] [options]   ┆ no arguments installs all dependencies in aap.json
                                          ┆ -f         = force, overwrites existing dependencies
                                          ┆ --save     = save dependency to "dependencies" in aap.json
                                          ┆ --save-dev = save dependency to "devDependencies"
                                          ┆ --dev      = install from "devDependencies"
                                          ┆
                                          ┆ valid urls are:
                                          ┆   git@github.com:user/repo.git
                                          ┆   ssh+git://user@bitbucket.org/user/repo.git
                                          ┆   ssh+git://github.com/username/package.git

## Goals/Usecases 

* run/deploy a cloud using multiple Docker cloudservices in one repo using [crowdr](https://github.com/polonskiy/crowdr)
* depency management: wrap several repositories and modules in one repository
* use in and outside dockers 
* install package managers in environments where they're not installed
* avoid git submodules (gets laborous pretty easily)

## Todo 

* `aap update`
* `aap run`

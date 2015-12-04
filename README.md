<img alt="" src="doc/logo.jpg"/>

In the beginning there was bash..and bash had aap.json

![Build Status](https://travis-ci.org/coderofsalvation/aap.svg?branch=master)

## Getting started 

If you're used to `npm` or `composer`, you will feel right at home.
Lets start a project by adding dependencies to it:

    $ git init 
    $ aap init
    $ aap install ssh+git://user@bitbucket.org/username/backend.git            --save
    $ aap install ssh+git://user@github.com/username/core-api.git              --save
    $ aap install ssh+git://user@bitbucket.org/username/landingpage.git        --save
    $ aap install ssh+git://user@github.com/username/crm-api.git@1.3.4#master  --save
    $ aap install ssh+git://user@github.com/username/docker.mysql.git          --save
    $ aap install ssh+git://user@github.com/username/docker.mongodb.git        --save
    $ aap install npm://css2js@1.0.3                                           --save 
    $ aap install composer://myphppackage@1.4.3                                --save 
    $ mkdir python
    $ cd python && ../../aap install pip://mypythonpackage --save 
 
Nice! Now aap.json will look like [this](doc/aap.json)

Now lets push our buildpack to the repo:

    $ git add app.json && git commit -m "added aap manifest"
    $ git push origin master

Congrats! Now other devs can easily run or [deploy a cloud locally](doc/cloud.md):

    $ aap install

    installing 'backend'
        ├─ $ git clone ssh+git://user@bitbucket.org/username/backend.git
        ├─ Cloning into 'backend'...
        ├─ 
        ├─  ʕ•x•ʔ
        ├─ +-+-+-+  Your personal nested build & dependency monkey
        ├─ |a|a|p|  [https://github.com/coderofsalvation/aap]
        ├─ +-+-+-+
        ├─ 
        ├─   
        ├─ installing 'backend'
        ├─     ├─ $ git clone https://foo@bitbucket.org/username/backend-html-templates 
        ├─     ├─ Cloning into 'backend-html-templates'...
        ├─ 
        ...and so on..
        

> NOTE recursive installation is supported when `aap.json` occurs in gitrepo-dependencies as well.

Like npm, you can easily [trigger scripts](docs/scripts.md) using the `aap run <cmd>`, to build and configure stuff from one central place.

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
                                          ┆   ssh+git://github.com/username/package.git#master
                                          ┆   ssh+git://github.com/username/package.git#master#commit
                                          ┆   ssh+git://github.com/username/package.git#master@1.0.2
                                          ┆   npm://browserify 
                                          ┆   composer://user/packagename
       aap run <script>                   ┆ runs script defined in aap.json 
     
## Goals/Usecases 

* [run/deploy a cloud](doc/cloud.md) using multiple Docker cloudservices in one repo using [crowdr](https://github.com/polonskiy/crowdr)
* depency management: wrap several repositories and modules in one repository
* use in and outside dockers 
* install package managers in environments where they're not installed
* avoid git submodules (gets laborous pretty easily)
* readability: deploy and dependency info confined in one jsonfile (aap.json) to minimize shellscriptism

## Todo 

* `aap update`
* `aap run`

<img alt="" src="doc/logo.jpg"/>

> NOTE: very beta

In the beginning there was bash..and bash had aap.json

![Build Status](https://travis-ci.org/coderofsalvation/aap.svg?branch=master)

## Usage

    $ aap init
    $ aap install ssh+git://user@bitbucket.org/username/foo.git --save
    $ aap install ssh+git://user@github.com/username/foo.git --save
    $ aap install npm://css2js --save 
    $ aap install composer://modulename --save 
    $ cd python && aap install pip://packagename --save 

> aap.json is now generated (click [here](doc/aap.json) If you're used to `npm` or `composer`, you will feel right at home.

## Why

Now you can easily manage dependencies of gitrepos, npm/composer modules and dockerrepos.
All combined in one slim repo.

Basically `aap init` generates `aap.json` like [this](doc/aap.json), which allows you to run:

    $ aap install

Which allows any system to build a project from multiple remote sources.

## Goals/Usecases 

* run/deploy a cloud using multiple Docker cloudservices in one repo using [crowdr](https://github.com/polonskiy/crowdr)
* depency management: wrap several repositories and modules in one repository
* use in and outside dockers 
* install package managers in environments where they're not installed

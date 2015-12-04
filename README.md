<img alt="" src="doc/logo.jpg"/>

Language-agnostic buildpacks using aap.json.
A package manager aggregator & buildtool.

![Build Status](https://travis-ci.org/coderofsalvation/aap.svg?branch=master)

## Usage

    $ aap init
    $ aap install ssh+git://user@bitbucket.org/username/foo.git --save
    $ aap install ssh+git://user@github.com/username/foo.git --save
    $ aap install npm://browserify --save 
    $ aap install composer://browserify --save 
    $ aap install pip://packagename --save 

> If you're used to `npm` or `composer`, you will feel right at home.

## What happened?

Now you can easily manage dependencies of gitrepos, npm/composer modules and dockerrepos.
All combined in one slim repo.

Basically you end up with an `aap.json` like [this](doc/aap.json), which allows you to run:

    $ aap install

Which allows any system to build a project from multiple remote sources.

## Goals/Usecases 

* run/deploy a cloud using multiple Docker cloudservices in one repo using [crowdr](https://github.com/polonskiy/crowdr)
* depency management: wrap several repositories and modules in one repository

Triggering scripts 
==================

## Usage 

    $ aap run
    Usage: aap run <cmd>
    
    available commands:
    
      preinstall
      postinstall
      predeploy
      postdeploy
      start
      stop
      build
      backup
      test
      install_modules

You are totally flexible when it comes to triggers, they're defined in aap.json:

    {
      ...
      "scripts": {
        "preinstall": "",
        "postinstall": ["install_modules"],
        "predeploy": ["stop"],
        "postdeploy": ["start"],
        "start": "echo start && echo hoi; for((i=0;i<10;i++)); do echo $i; done",
        "stop": "echo stop",
        "build": "echo build",
        "backup": "zip -r data-`date +`.zip data",
        "test": "echo $qError: no test specified$q && exit 0",
        "install_modules":"which npm && npm install; which composer && composer install"
      }
      ....
    }

> Edit/add commands to your liking

## Aliases

As seen in the example above, arrays indicate aliases.
For example `"restart":["stop","start"]` would be the same as running:

    $ aap run stop
    $ aap run start

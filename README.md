shipsinker
==========

shipsinker is perhaps the simplest possible utility for automating single-server app deployments.
It's not tied to any particular language or framework, and can be used to deploy pretty much anything.
shipsinker used to be written in Node.js, but for compatibility with any kind of server it was rewritten in bash.


1. installation
------------

Get shipsinker by cloning the repository or grabbing the [tarball](https://github.com/Frustra/shipsinker/archive/master.tar.gz).
Put it anywhere, but keep note of where for the next step.


2. configuration
-------------

Global configuration is done via `/etc/shipsinker.conf`. It's self-documented [here](https://github.com/Frustra/shipsinker/blob/master/examples/shipsinker.conf).
`sink create [package name]` from anywhere to set up a package.


3. usage
-----

shipsinker supplies the `sink` command, which is used for managing packages

```
sink PACKAGE            pull and start/restart PACKAGE
sink [action]           execute an action for all packages
sink [action] PACKAGE   execute an action for PACKAGE
sink help               display this usage message

actions:
  autostart   start all packages configured for autostart
  list        list all packages and their status
  stopall     stop all running packages

package actions:
  create      set up new config files for PACKAGE
  deploy      pull and start/restart PACKAGE
  log         display the log file for PACKAGE
  pull        synchronize repository for PACKAGE
  restart     stop and restart PACKAGE
  start       start a new daemon for PACKAGE
  stop        stop any running instances of PACKAGE
```

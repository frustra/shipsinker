shipsinker
==========

shipsinker is perhaps the simplest possible utility for automating single-server app deployments.
It's not tied to any particular language or framework, and can be used to deploy pretty much anything.
shipsinker used to be written in Node.js, but for compatibility with more servers it was rewritten in bash.


1. installation
---------------

Get shipsinker by cloning the repository or grabbing the [tarball](https://github.com/frustra/shipsinker/archive/master.tar.gz).
It is recommended to place shipsinker in `/usr/local/lib/shipsinker` and symlink `bin/sink` to `/usr/local/bin/sink`.

Users running the sink command will need permission to run `sudo -u $BUILD_USER`.
The build user will also need to be able to run commands as the exec user.

For example, using `sinker` and `www-data` as the build and exec users, the following will need to be added to the sudoers file:
```
sinker  ALL=(www-data) NOPASSWD: ALL
```


2. configuration
----------------

An example configuration is documented [here](https://github.com/frustra/shipsinker/blob/master/examples/shipsinker.conf).
Place this file in `/etc/shipsinker.conf` and make any changes you see fit.

Shipsinker packages can be auto-generated with the `sink create [package name]` commmand,
documentation for the package format is available [here](https://github.com/frustra/shipsinker/blob/master/examples/package/ship.conf).

Once a package is created, it must be deployed before it can be started.
Run `sink [package name]` to deploy a package for the first time.


An init.d file is provided [here](https://github.com/frustra/shipsinker/blob/master/examples/init.d/shipsinker) that will start all
packages marked with the autostart flag, and can be run on system startup.


3. usage
--------

shipsinker supplies the `sink` command, which is used for managing packages

```
sink PACKAGE            pull and start/restart PACKAGE
sink [action]           execute an action for all packages
sink [action] PACKAGE   execute an action on PACKAGE
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

minimalplone6
=============

This is a minimal buildout configuration for installing the latest Plone 6.

Currently, I recommend to install the development version with unreleased
packages. Therefore, the buildout extends files from buildout.coredev on github.


Prerequisites
-------------
- Python 3
- Python Virtualenv
- Git


Install
-------

For the default configuration with the latest Plone 6 release::

    $ git clone git@github.com:collective/minimalplone6.git
    $ cd minimalplone6
    $ ./bootstrap.sh

If you want to install the development version of Plone based buildout.coredev::

    $ ./bootstrap.sh -c coredev.cfg

Or if you want to use the ZEO configuration::

    $ ./bootstrap.sh -c zeo.cfg

In any case you will be asked for an administrative username and password.

Fire up Zope and maybe the ZEO Server::

    $ ./bin/zeoserver start
    $ ./bin/instance start

Point your webbrowser to http://localhost:8080 (username admin, password admin)
and install a Plone instance (Volto or Classic).

That's all, folks.


Extend the config
-----------------

For your own projects, you might extend the configuration. Use a different
PORT, add some more eggs, like::

    [buildout]
    extends = zeo.cfg

    [zeoserver]
    zeo-address = 8100

    [instance]
    http-address = 8080
    zeo-address = ${zeoserver:zeo-address}
    eggs +=
        plone.app.debugtoolbar
        plone.app.widgets


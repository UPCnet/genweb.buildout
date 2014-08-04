Genweb Uber-buildout
====================

This is the ultimate-uber-maxi-definitive-awesomefull buildout for Genweb-based
projects.

Usage
-----

You should choose what project do you want to work with or the basis of your new
one. For example, if you want to use a GenwebUPC buildout you should specify the
name of the project .cfg associated:

    [path_to_your_python_bin] bootstrap.py -c genwebupc.cfg
    ./bin/buildout -c genwebupc.cfg

Check out for the available projects in the projects.cfg file.

.. note:: Before that, remember to copy the customizeme.cfg.in file into customizeme.cfg configuring the required parameters.

Available projects/builds
-------------------------

 * Genweb UPC (genwebupc.cfg)
 * uLearn (ulearn.cfg)
 * Websites in general (e.g Switch-Med) (websites.cfg)
 * Vilaix and transparency sites (vilaix.cfg)
 * Production builds:

     - Nginx only (1.6.0) (nginx-only.cfg)
     - Pre-frontends only (Varnish 4.0.1 and HAProxy 1.5.2) (prefrontend-only.cfg)
     - Frontends only (Zope Clients) (zope-only.cfg)
     - Backends only (ZEO servers) (zeo-only.cfg)
     - Debug frontend (debug.cfg)

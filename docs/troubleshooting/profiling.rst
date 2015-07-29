Profiling and monitoring
========================

There are some tools that we can use for profiling and monitoring the Zope/Plone
sites.

Products.LongRequestLogger
--------------------------

https://pypi.python.org/pypi/Products.LongRequestLogger

Add to the instance section of the buildout::

    [zc1]
    ...
    eggs = Products.LongRequestLogger
    ...

or if the Plone site is < Plone 4 (python2.4)::

    [zc1]
    ...
    eggs = Products.LongRequestLogger[python24]
    ...

And configure the environment variables::

    <environment>
      longrequestlogger_file $INSTANCE/log/longrequest.log
      longrequestlogger_timeout 4
      longrequestlogger_interval 2
    </environment>

directly in the zope configuration file (overrided when you run the buildout)::

    $INSTANCE/parts/zc1/etc/zope.conf

or in the instance section of the buildout::

    [zc1]
    ...
    environment-vars +=
      longrequestlogger_file ${buildout:directory}/log/longrequest.log
      longrequestlogger_timeout 4
      longrequestlogger_interval 2
    ...

==================
New egg generation
==================

To generate new eggs we should use the package generator mr.bob. It's installed
via buildout with the 'mrbob' recipe. If the current recipe you are using does
not include it, simply put it in the parts directive of the buildout section.

Then, to generate the package do:

.. code-block:: bash

    $ ./bin/mrbob -O ulearn.XXXX genweb.templates:plone

where we should specify the name of the new package after the -O modifier, and
lastly, the name of the egg containing the template and the name of the template
separated by a semicolon.

Sometimes we can use the official Plone package template:

.. code-block:: bash

    $ ./bin/mrbob -O ulearn.XXXX bobtemplates:plone_addon

Simple CSS customization
========================

Usually, client customizations happens in projects. A simple way of add a CSS
overriding all the existing ones are in place. The resource is initially in
blank::

    http://the_server/the_site/genwebcustom.css

This resource (in fact, a view) can be easily overrided by using z3c.jbot and
the `templates` directory::

    genweb.theme.browser.views_templates.genwebcustom.css.pt

and edit it accordingly.

Take in account that some of the colors and properties can be overriden directly
using the Genweb (and uLearn) control panel.

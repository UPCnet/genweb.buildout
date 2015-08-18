CSS and JS resources
====================

Due to scalability and performance issues and to the introduction of new JS
technologies, a new way of manage resources was conceived, abandoning the old
school Plone JS and CSS resource registry.

The config.json file
--------------------
The new model is based in an external file config.json, located in the root of a
Python package that manages the CSS or JS resources (or both) for a specific
layer (for a client or other purposes in its own package, eg:
ulearn.blanquerna).

It has this structure::

    {
      "resources": {
        "genweb": {
          "css": {
            "development": [
              "../genweb.js/genweb/js/components/select2/select2.css",
              "../genweb.core/genweb/core/static/fontello-genweb/css/fontello.css"
            ],
            "production": [
              "../genweb.cdn/genweb/cdn/dist/genweb.css"
            ]
          }
        }
      },
      "order": [
        "genweb"
      ],
      "replace_map": {
        "../genweb.js/genweb/js/components": "++components++root",
        "../genweb.core/genweb/core/static": "++genweb++static",
        "../genweb.cdn/genweb/cdn/dist": "++genweb++dist"
      },
      "revision_info": {
        "../genweb.cdn/genweb/cdn/dist/genweb.css": "../genweb.cdn/genweb/cdn/dist/genweb.8a6f25a6.css"
      }
    }

`resources`: The definition of the resources, structured by name and then by
type of the resource (css or js) and finally by mode (development or
production).

`order`: The order od the production resources at rendering time.
`replace_map`: The relative path requires to be translated to "Plone"
plone.resource paths (eg: ++genweb++dist). This defines the translation to be
done on rendering.
`revision_info`: Control automatic field informed by **Gruntfile.js**.

Viewlets on rendering
---------------------

Then, four new viewlets are defined:

    * gwCSSDevelViewlet
    * gwJSDevelViewlet
    * gwCSSProductionViewlet
    * gwJSProductionViewlet

each of one, taking care of the devel (while working in fg) or production mode
and rendered as required in the correct place (<head> or at the bottom of
<body> tag). They read the `config.json` and build the correct structure with
the references to the resources.

..note::

    They use a `forever` RAM cache, so it is required to restart the instance
    or process in order to refresh them.

For a new package that requires to override or add new JS or CSS resources, it
is required to override the required viewlet (ideally in both devel and
production) using a layer.

..note::

    In order to achieve easy CSS customizations, a resource is in place to do
    so. The resource
    /src/genweb.theme/genweb/theme/browser/views_templates/genwebcustom.css.pt
    can be easily overrided with z3c.jbot and the `templates` directory.


Creation of production resources
--------------------------------

The resources in `config.json` are concatenated and minified using a Grunt task.
The tasks are located in the root of the package (eg: genweb.js) and defined by
a `Gruntfile.js`. These files are custom tailored to meet each package
requirements and could be easily cloned and modified to meet your
extension package needs.

This revolves arround the idea of "bundles". In fact, a build of each group of
resources got saved in an unified package: `genweb.cdn`. Then, in production, we
can easily refer to this bundle in the Nginx configuration and bypass it to the
FS directly.

The command line is::

    $ grunt gwbuild

in all cases.

Customization of the Gruntfile.js
---------------------------------

In case you require to customize a Gruntfile.js you should look into the
configuration of the sections and update them accordingly with the name of the
production resources defined in `config.json`:

    * cssmin
    * filerev
    * uglify
    * clean
    * concat
    * ngAnnotate

For the last two, if the JS requires to be annotated (Angular.js) use
ngAnnotate, and concat if it doesn't.

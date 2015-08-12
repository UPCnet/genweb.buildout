ulearn.js
=========

How to extend GenwebApp Angular app
-----------------------------------

This is the concept of creating a new "bundle" in case that you want to extend
the default GenwebApp application. The way to do it is to clone the default
app and substitute the ulearnapp.deps.js file with one defining the new
dependencies and add the new code as modules.

Then create the new bundle and activate it for the layer corresponding to the
new feature package.

===================================================
Plone, TinyMCE i Plantilles (plonetemplates plugin)
===================================================
:Autor: Ariel
:Description: Com afegir plantilles a l'editor TinyMCE de Plone4.
:Date: 2011-10-31
:Revision: 1.0
:Tags: Plone, TinyMCE, templeates


Instal·lació
------------
Afegir al buildout::

    [eggs]
    ...
    collective.tinymcetemplates

Configuració
------------
Crear un directori **templates** a la carpeta arrel.

Afegir plantilles
++++++++++++++++++
Una plantilla és un element de tipus pàgina, cal afegir dins de les carpetes de plantilles tantes pàgines com plantilles.

- El *títol* de la pàgina serà l'identificador de la plantilla al desplegable.
- La *descripció* de la pàgina serà la plantilla per la descripció.
- La *descripció* de la pàgina serà la plantilla per la descripció.
- El *cos* de la pàgina serà la plantilla del contingut.

Nota pels editors de les plantilles
...................................

Es pot fer que el text que tingui selecciona l'usuari sobreescrigui una part de la plantilla. Per triar quina part s'ha de sobreescriure cal marcar-la amb la classe CSS *selcontent*, per exemple::

 <span class="selcontent">(your content here)</span>


Configuració avançada
+++++++++++++++++++++

La ubicació o les ubicacions de les carpetes que conten les plantilles està definida a `plone.app.registry` com `collective tinymcetemplates templateLocations`

Anar a::

    /portal_registry

Clicar a::

    collective tinymcetemplates templateLocations

Introduïr les rutes de les diferents carpetes, per exemple::

    /plantilles


Fonts
-----

:collective.tinymcetemplates: http://pypi.python.org/pypi/collective.tinymcetemplates




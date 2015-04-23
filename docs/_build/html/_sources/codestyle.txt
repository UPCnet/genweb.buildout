==========================
Manual de bones pràctiques
==========================

Aquest document exposa algunes de les bones pràctiques que es recomanen quan desenvolopeu el projecte Genweb.

PEP8
----

És important mantindre un codi d'estil unificat basat en l'estàndar Python PEP8. Aquest codi el podeu trobar a::

    http://www.python.org/dev/peps/pep-0008/

Hi han eines validadores de codi (linters) pels editors més comuns que validen PEP8, per exemple SublimeText2 te un plugin linter per PEP8.

Vistes
------

Genweb disposa del framework de desenvolupament Grok, que permet declarar vistes i viewlets de manera imperativa via Python sense necessitat de declarar-los via ZCML. Així es manté unificat el codi i la declaració de la vista.

En la mida de lo possible, utilitzarem Grok per totes les vistes i viewlets. En cas de haver de fer overrides, es farà via ZCML.

Editor / IDE
------------

Es recomana utilitzar l'entorn de desenvolupament (IDE) `Sublime Text 2 <http://www.sublimetext.com/>`_. En l'últim any s'ha convertit en referència de la comunitat i disposa de molts plugins que faciliten el treball diari del desenvolupador.

.. note::

    Podeu trobar més informació de com instal·lar Sublime Text 2 i els plugins més interessants a: http://upcnet-gc-docs.readthedocs.org/en/latest/

git i Github
------------

El VCS que es fa servir a Genweb és git. Es troba hostatjat en el servei de social coding `Github <http://github.com/>`_ .

Els paquets de Genweb pengen de la organització UPCnet de Github i són públics. Genweb és codi lliure sota la llicència GPL v2. Aquest és la URL::

    http://github.com/UPCnet

La manera de treballar amb git és amb branques i tags per releases finals. Aquestes branques segueixen el estàndar:

    master
        Per releases finals. Codi "ready for production"

    develop
        Versions beta i encara no publicades i probablement, codi no llest per producció. Branca que te els canvis que es publicaran en la següent release.

    <altres branques no permanents>
        Branques de alphas i de codi que encara no está acabat. Poden ser locals a cada desenvolupador o compartides en servidor.

Només els usuaris (de Github) autoritzats a la organització poden fer canvis en els repositoris. Els usuaris que vulguin contribuir amb codi a Genweb ho han de fer via "pull requests" de Github. El codi es revisarà i es farà el "merge" si és convenient.


.. note::

    Per més informació sobre git i github, podeu consultar: https://help.github.com/

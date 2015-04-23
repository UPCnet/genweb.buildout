=======
Testing
=======

El dessitjable és que Genweb tingui el màxim de codi cobert per testos automatitzats. Genweb disposa de una col·lecció de testos d'integració, funcionals i d'acceptació globals a la totalitat del codi que composa Genweb. Per lo tant, aquest codi comprova per exemple si es creen bé tipus de contingut comuns corresponents a paquets diferents i si funcionen bé en el contexte global de Genweb.

A més, cada paquet pot tindre els seus propis testos.

La forma de llençar els testos::

    <directori_buildout>/bin/tests -s genweb.core

Per altres paquets::

    <directori_buildout>/bin/tests -s genweb.controlpanel

Travis CI
---------

`Travis CI <http://travis-ci.org>`_ és un entorn en cloud de integració contínua (CI). Aquest entorn està enllaçat amb Github de manera que cada cop que un desenvolupador puja (commit) o fa una petició de pujada (pull request) s'executan els testos del paquet en concret, tenint d'aquesta manera control total sobre si el codi que s'ha pujat és correcte i no trenca el paquet.

Cada paquet te enllaçat un "hook" de Github per a que Travis sàpiga que ha de fer la seva feina quan es puja codi.

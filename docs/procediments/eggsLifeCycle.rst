Metodologia de treball amb Eggs 
===============================

En la majoria de projectes en que estem actualment, estem treballant amb eggs
per fer el pas a producció, i evitar problemes i ensurts al utilitzar
subversion/git directament als servidors de explotació. Tot i que som unes
poques persones que acavem "posant" els ous propiament, el cicle de vida dels
ous ens implica a tots. A continuació explicarem les bones pràctiques a seguir:


Elements que entren en joc 
--------------------------

En l'estructura bàsica d'un paquet trobarem, a l'arrel:

- El fitxer setup.py, on hi ha la versió del paquet que s'utilitza per fer l'egg. En aquest arxiu també hi hem d'indicar el correu/autor del paquet, és un paràmetre obligatori.

- El fitxer setup.cfg, on es poden especificar paràmetres de com es genera la versió del paquet. Si no necessitem fer res concret que necessiti cap paràmetre, hem de comprovar que aquests parametres estiguin a "false", si no hi són, no cal::  

    tag_build = false 
    tag_svn_revision = false

- El fitxer docs/HISTORY.txt on escriurem els canvis que es fagin en cada versió dels paquets, amb el següent format, on x.y.z és el numero de versió, i AAAA-MM-DD la data. Els canvis no tenen perquè coincidir amb els commits al subversion/git ni ser molt detallats, aquí hi escriurem descripcions curtes dels canvis que donguin una idea del que s'ha fet, per exemple::

    Changelog 
    =========

    x.y.z (AAA-MM-DD) -----------------

    * Afegida vista VistaGuai que fa un munt de coses [autor] 
    * Corregit Bug que ens portava pel camí de l'amargura [autor]


Procediment durant el desenvolupament 
-------------------------------------

- En el HISTORY.txt, mentres no fem l'ou i estiguem treballant en el paquet, al lloc on posariem la data, escriurem " x.y.z (unreleased)" en el seu lloc. Això ens indicarà que aquest paquet encara NO té un ou fet per a la versió x.y.z
- La versió que posarem al HISTORY.txt serà la següent que toqui per al paquet. Mentre hi estiguem treballant només editarem aquest arxiu, no modificarem la versió que hi ha al setup.py fins que no fem l'egg. Per exemple:

    * Si és un projecte nou, posarem 1.0 (unreleased)     
    * Si estem modificant/afegint funcionalitat a un projecte existent que estava a la versio 2.1, posarem  2.2 (unreleased)

- Per projectes nous, no cal escriure una llista de les funcionalitats, ho podem deixar amb el "- Initial Release" que ens posa el paster quan creem un paquet nou.


Procediment per fer l'egg 
-------------------------

- Comprovar en el HISTORY.txt, la versió nova que ha de tenir el paquet i que el desenvolupador ha fixat

- Escriure en el setup.py la versió que hem comprovat

- Canviar el (unreleased) del HISTORY.txt corresponent a la versió actual i posar-hi la data d'avui.

- Commitejar els canvis, indicant en el missatge de commit "Preparar per egg versió x.y.z". D'aquesta manera deixem una marca fàcilment identificable al log de revisions del subversion/git que ens permet saber cada versió de cada ou a quina revisió de codi correspon.

- Si fem algun canvi posterior a fer l'egg sense canviar número de versió de la release, recordar de quan commitejem els canvis indicar el nou "punt de canvi d'egg" amb el mateix missatge que avans. L'últim missatge al log serà el vàlid.

- IMPORTANT : Al fer l'egg es pujen els canvis que tenim en local al disc, per tant sempre revisar amb un "svn st" que no tinguem cap modificació local que no tinguem pujada al subversion. Això és especialment important per:

    * Si ens hem descuidat de commitejar canvis i fem l'egg, aquest egg contindrà els canvis, però en posteriors modificacions d'altres, es perdrien aquests canvis i els eggs no serien consistents amb el que hi ha al repositori

    * Si tenim un canvi local que no ha de ser pujat al repositori, i fem l'egg en aquell moment, el repositori estarà correcte, però haurem generat un ou dolent.

Mètode de numeració de versions 
-------------------------------

XXX TODO




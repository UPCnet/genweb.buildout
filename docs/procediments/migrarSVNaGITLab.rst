Migrar repositoris de svn a GitLab
==================================

Organització
-------------

Ara tenim els diferents paquets que formen un projecte organitzats en diferents repositoris, i amb la estructura de base del subversion, de manera que típicament tenim::

    + nomrepositori
    |
    +--+ trunk
    |  |
    |  +- nompaquet1
    |  +- nompaquet2
    |
    |- tags
    |
    +- branches

i a dins del trunk tots els paquets. això ens dona la estructura "fixa" nomrepositori/trunk/nompaquet, que sumat a la url base ens dona::

    https://devel.upcnet.es/svn/nomrepositori/trunk/nompaquet

Amb el git, ens oblidem de tota aquesta *palla*, ja que el tema del trunk/branches ho farem amb els mètodes natius que ja ens ofereix el sistema git. Per tant la nova estructura que donarem als projectes i paquets seguirà les següens directives:

* Tots els paquets estaran al mateix lloc, que serà l'arrel del git, per tant **tots** els paquets estaran sota el mateix patró de urls::

    https://git.upcnet.es/nompaquet

o si hi accedim amb les claus ssh::

    git@git.upcnet.es:nompaquet.git

* Per organitzar els paquets, es faran grups, però que aquests no afecten a les urls que acavem de dir, simplement es per tenir-ho ordenat, i mantenir un cert *sabor* a com estava organitzat avans. Aquests grups es poden fer i desfer que no afecten a les urls. Exemple, si avans teniem::

    https://devel.upcnet.es/svn/intranetupcnet/trunk/upcnet.intranet
    https://devel.upcnet.es/svn/intranetupcnet/trunk/upcnet.intranettheme

ara passarem a tenir::

    https://git.upcnet.es/upcnet.intranet
    https://git.upcnet.es/upcnet.intranettheme

i un grup al qual podrem accedir desde::

    https://git.upcnet.es/groups/intranetupcnet


Nomenclatura i organització pels buildouts
------------------------------------------

Ara soliem tenir un paquet de buildout per cada projecte, dins el repositori del projecte, que feiem servir com a buildout de desenvolupament, i apart, els buildouts utilitzats a produccio, els teniem en el repositori deployment, organitzats per maquines, per exemple, el buildout de la intranet upcnet es trobava a::

    https://devel.upcnet.es/svn/deployment/situla/trunk/intranetUPCnet

A partir d'ara, continuarem tenint un paquet per devel i un per produccio, però indicant en el nom si es de devel o de produccio de la seguent manera::

    intranetupcnet.buildout.devel
    intranetupcnet.buildout.deploy

i els guardarem en el grup que correspongui al projecte. Seguint amb l'exemple, el grup del projecte de la intranet upcnet, es quedaria amb els següents paquets a dins::

    https://git.upcnet.es/upcnet.intranet
    https://git.upcnet.es/upcnet.intranettheme
    https://git.upcnet.es/intranetupcnet.buildout.devel
    https://git.upcnet.es/intranetupcnet.buildout.deploy

Com que un repositori el podem tenir en més d'un grup a la vegada, els repositoris de deploy els organitzarem en grups segons la maquina on esta el projecte en producció, fent servir la nomenclatura::

    host.deploy

on ``host`` sera el nom de la maquina sense posar el ``.upc.edu`` o ``.upc.es`` D'aquesta manera sera fàcil fer un llistat de tots els grups de maquines en producció, o bé buscar una maquina concreta.

Passos per migrar
-----------------

* Desde colladaverda,  executar el migrador per cada un dels paquets que volem migrar indicant url del repositori, grup(s) on posarem el paquet importat i nom alternatiu (opcional) en cas que volguem renombrar el paquet::

    svn2gitlab https://devel.upcnet.es/svn/xxxxxxxxxxx grup1,grup2 nom_alternatiu


- Els grups estaran separats per comes, sense espais, i en cas de no voler posar cap grup, posarem un guio (-)
- Si no volem cambiar el nom del paquet, no cal que passem l'últim paràmetre

* Un exemple amb totes les opcions possibles::

    root@colladaverda:~# svn2gitlab https://devel.upcnet.es/svn/deployment/situla/trunk/intranetUPCnet intranetupcnet,situla.deploy intranetupcnet.buildout.deploy

       Subversion to GitLab Migrator 1.0
       ---------------------------------

     > Checking out https://devel.upcnet.es/svn/deployment/situla/trunk/intranetUPCnet \
     > Searching svn commiters for intranetUPCnet
        · Found 3 unique commiters
     > Cloning intranetUPCnet as local GIT repository /
     > Creating new GIT repository at https://git.upcnet.es/intranetupcnet.buildout.deploy.git
     > Pushing Repository.
     > Marking Subversion repo as MOVED
     Creating group "intranetupcnet"
     Adding intranetupcnet.buildout.deploy to group "intranetupcnet"
     Creating group "situla.deploy"
     Adding intranetupcnet.buildout.deploy to group "situla.deploy"
     > Applying security settings
        · Added victor.fernandez to intranetupcnet.buildout.deploy developers team
        · Added roberto.diaz to intranetupcnet.buildout.deploy developers team
        · Added carles.bruguera to intranetupcnet.buildout.deploy developers team

* El repositori subversion antic, un cop l'script a fet push al nou git, queda marcat amb un arxiu::

    ____MOVED____TO____GITLAB.txt

perque quedi clar que aquell subversion ja esta obsolet. A dins de l'arxiu, queda registrada la ubicació de nou repositori.

* L'ultim pas del migrador es donar permisos a tothom qui ha comitejat alguna vegada. Si algu dels que intenta donar permisos no ha entrat mai al gitlab, ens avisarà i si s'escau que és algú que encara treballa aqui, doncs li demanarem amablement que es logueigi, per poder tornar a executar la comanda exactament amb els mateixos paràmetres perque afegeixi aquestes persones.

Adaptar buildouts
-----------------

Un cop migrats els buildouts de devel, recordeu que els haureu d'adaptar per fer servir els nous repositoris:

* Instalarem el mr.developer en el nostre buildout.cfg::

    [buildout]

    extensions = mr.developer
    auto-checkout = *


* Afegirem tots els paquets que hem de incloure com a development, tant si son git com si queda algun subversion::

    [sources]

    nom.paquet = git git@git.upcnet.es:nom.paquet.git
    nom.paquet2 = svn https://xxxxxxxx

* En cas que el buildout utilitzes externals per obtenir els paquets i descarregar-los a la carpeta src, la migració ja s'haurà encarregat d'eliminar les referencies, de totes maneres, millor esborrar el arxius EXTERNALS.txt de la carpeta src en cas que hi sigui.
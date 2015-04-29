Traduccions a Plone 4 (i 3)
===========================
A partir de Plone 4.0 les traduccions dins de la carpeta **i18n està en desús**. Es recomana que les traduccions segueixin l'estructura estandar de gettext, per exemple::

    locales/ca/LC_MESSAGES/simpleTask.po

A partir de Plone 4.1 només s'accepten les traduccions a **locales**.

Estructura d'exemple

-----------------------------------------------------------------

::

    upcnet.simpleTask
    └── upcnet
        └── simpleTask
            ├── i18n @deprecated since v4.0
            │   ├── plone-simpleTask-ca.po
            │   ├── plone-simpleTask-en.po
            │   ├── plone-simpleTask-es.po
            │   ├── simpleTask-ca.po
            │   ├── simpleTask-en.po
            │   └── simpleTask-es.po
            └── locales
                ├── ca
                │   └── LC_MESSAGES               
                │       ├── plone.po
                │       └── upcnet.simpleTask.po
                ├── en
                │   └── LC_MESSAGES
                └── pot
                    └── LC_MESSAGES
                        ├── plone.pot
                        └── upcnet.simpleTask.pot

-----------------------------------------------------------------

Configuració del lloc
---------------------
Cal indicar a Plone/Zope que és multiidioma i quins idiomes té::

    manage -> Portal Languages

Triar del desplegable els idiomes que hi hauran al lloc i guardar els canvis.

configure.zcml
--------------

#. Afegir tag xmlns:i18n a l'etiqueta *configure*::

    xmlns:i18n="http://namespaces.zope.org/i18n"

#. Registrar el directori de les traduccions *locales*::

    <i18n:registerTranslations directory="locales" />

Carpeta locales
---------------

Per crear l'estructurua "locales/codi_idioma/LC_MESSAGES/", per exemple::

            └── locales
                └── ca
                    └── LC_MESSAGES               

#. Situar-se a l'arrel del paquet, per exemple::

    cd upcnet.simpleTask/upcnet/simpleTask

#. Pots crear tots el directoris amb la comanda (en aquest cas els idiomes son:espanyol, català, anglès)::

    mkdir -p locales/{"es","ca","en"}/LC_MESSAGES

Crear fitxer .POT i .PO
-----------------------

#. Anar al directori locales::
   
    cd locales

Creació .POT
++++++++++++

La creació del .pot que s'explica a continuació es per crear bé la ruta als fitxers en els comentaris.

#. Creació d'un idioma fictici *pot*::
    
    mkdir -p pot/LC_MESSAGES    

#. Creació de l'arxiu pot per a cada domini::

    cd pot/LC_MESSAGES
    touch [domini].pot
    i18ndude rebuild-pot --pot [domini].pot --create [domini] ../../../

Creació .PO
++++++++++++

#. Creació del po de cada idioma fent servir el .pot, des de *locales/pot/LC_MESSAGES*::
    
    touch ../../[idioma]/LC_MESSAGES/[domini].po
    i18ndude sync --pot [domini].pot ../../[idioma]/LC_MESSAGES/[domini].po

#. Definir idioma i comprovar domini de l'arxiu .po, per exemple espanyol::

    "Language-Code: es\n"
    "Language-Name: Spanish\n"
    "Domain: [domini]\n"

Actualitzar .POT i .PO
-----------------------

#. **Fes una copia de seguretat de les teves traduccions**

#. Actualitzar *.pot*::

        cd locales/pot/LC_MESSAGES
        i18ndude rebuild-pot --pot [domini].pot --merge [domini].pot --create [domini] ../../../

#. Sincronitzar els *.po*, des de locales ::

        cd locales
        i18ndude sync --pot pot/LC_MESSAGES/[domini].pot [idioma]/LC_MESSAGES/[domini].po

Override
--------
Override de traduccions s'han de fer dins de la carpeta *i18n*, el nom dels .po ha de ser::

    [domini]-[codi_idioma].

Templates
---------

El següent enllaç es interessant a l'hora de fer els templates: http://plone.org/documentation/kb/i18n-for-developers

Poedit
------

Instal·lació
++++++++++++

    sudo apt-get install poedit

El primer cop que s'executa cal introduir les dades del traductor (nom d'usuari i email).

Configuració Base de dades
++++++++++++++++++++++++++

Cal anar a::
    Edita -> Preferències -> Memòria de traducció

..
 TODO Explicar amb més detall com afegir directoris, treure els de sistema

Activar corrector
+++++++++++++++++


- Mode gràfic:

    1. Anar a::

        Catàleg -> Paràmetres -> Informació del projecte
    2. Seleccionar l'idioma de la traducció al desplegable.

- Mode text:
    1. Afegir a la capçalera del fitxer .po::
        
        "X-Poedit-Language: [Idioma]\n"
    

Més informació
--------------

Enllaços
++++++++

- http://maurits.vanrees.org/weblog/archive/2010/10/i18n-plone-4
- http://maurits.vanrees.org/weblog/archive/2007/09/i18n-locales-and-plone-3.0
- http://plone.org/documentation/manual/developer-manual/internationalization-i18n-and-localization-l10n/translating-text-in-code/i18ndude


Versions
++++++++

1.2 (2012-03-09)
................

- Secció templates


1.1 (2011-10-20)
................

- Bug: creació del .pot si no existeix, afegir touch [domini].pot (laura)
- Nou: configuració del lloc (laura)
- Borrador: secció Poedit


1.0 (2011-10-04)
................

- Versió inicial

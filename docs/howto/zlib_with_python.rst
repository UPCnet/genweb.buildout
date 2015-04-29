=========================================
 Problemes amb python i zlib?
=========================================
:Autor: roberto@UPcnet
:Description: Compiling python 2.4 with zlib
:Date: 2012-01-19
:Revision: 1.0
:Tags: Plone, Python, zlib


Descripció
------------
A la Ubuntu 11.10 quan descarreguem el Python2.4, i l'intentem compilar mostra un error de ZLIB::

    ImportError No module named zlib

De fet, l'error que dona es quan s'intenta baixar el distribute i el descomprimeix::

    tarfile.ReadError file could not be opened successfully


Solució
---------
Encara que tenim instal·lats els paquets de *zlib1g, zlib1g-dev i zlibc* es mostra el missatge d'error.

El problema es deu a que el sistema no trova la llibreria a la ruta de sistema que vol.
La solució consisteix en fer un link a la llibreria de sistema que ja tenim instal·lada::

    cd /lib
    sudo ln -s x86_64-linux-gnu/libz.so.1 libz.so


De fet, en el cas concret de la Ubuntu 11.10.386 cal fer directament això::

    sudo ln -s /lib/i386-linux-gnu/libz.so.1 /lib/libz.so


-----------------------------------------------------------------

Podeu trovar la informació original a:

    :Ubuntuforums: http://ubuntuforums.org/showthread.php?t=1759873






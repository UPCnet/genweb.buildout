NGINX and Mountain Lion
=======================

I’ve been experiencing some extrange behavior since I’ve updated to ML recently. NGINX stop compiling correctly throwing the following error::

    $ make -f objs/Makefile cd /opt/local/lib \ && if [ -f Makefile ]; then make distclean; fi \ && CC="gcc" CFLAGS="-O2 -fomit-frame-pointer -pipe " \ ./configure --disable-shared /bin/sh: ./configure: No such file or directory make[1]: *** [/opt/local/lib/Makefile] Error 127 make: *** [build] Error 2

It’s an error related with the PCRE library shiped with ML. We need to provide a brand new PCRE distribution::

    $ curl -O ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.21.tar.gz
    $ tar xvfz pcre-8.21.tar.gz
    $ cd pcre-8.21
    $ ./configure --enable-unicode-properties --enable-utf8
    $ make

Then, in the folder where we downloaded the nginx distribution::

    $ ./configure --with-pcre=../pcre-8.21

You should update the directory as needed to match the one you’ve downloaded the PCRE library.

NGINX will compile now without further notice.

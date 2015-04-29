Recuperació de backup de Genweb UPC 3.4
=======================================

S'utilitza la instància que es troba al directori de CAPRICORNIUS (màquina de desenvolupament del PloneTeam):

/var/plone/backoffice/genwebupc4

..note::

    Durant tota la narració d'aquest procediment utilitzarem com exemple la recuperació fictícia d'una instancia: *secretariesub*. Aquest nom s'utilitza com identificador de la instancia Plone i punt de muntatge a la ZMI (manage de Plone), directoris de blobs, així com a nom del fitxer de la base de dades que serà de la forma Data_secretariesub.fs. Necessitem saber també en quin entorn es troba aquesta intància. En aquest cas, estarà a l'entorn 11.

El procediment a seguir és el següent:

    1. Primerament, necessitem les dades originals de la instància que volem recuperar (*secretariesub*). Necessitem en concret la base de dades i els blobs associats. El backup del servei es troba enmagatzemat a Mebsuta, al directori: /backup/genwebupc/zeo11/secretariesub. En aquesta ubicació es troben els backups (diaris) corresponents a les dues setmanes anteriors, inclosa l'actual (fins divendres). El cap de setmana es genera un backup `full` en forma de *.fs i diàriament es generen `deltes` en forma de *.deltafs dels canvis diaris. En cas de necessitar recuperar dades anteriors, cal recuperar de la mateixa ubicació via Legato, el darrer fitxer *.fs (total del cap de setmana), el darrer *.dat (total del cap de setmana) i els *.deltafs des del cap de setmana fins la data del dia del que volem fer la recuperació. 

    2. Un cop identificats (o recuperats del Legato) els fitxers necessaris, a partir de la descripció de l'apartat anterior, cal executar un procediment per a generar el fitxer .fs corresponent a l'estat de la base de dades del dia en concret que volem recuperar. Per aconseguir això executar l'script *repozo* a Mebsuta::

        /var/plone/genwebupcZEO/produccio/bin/repozo -R -v -r /backup/genwebupc/zeo11/secretariesub/ -o /tmp/Data_secretariesub.fs -D 201X-XX-XX 

    on 201X-XX-XX és la data del dia en que volem fer la recuperació
    
    Exemple de resultat::

        looking for files between last full backup and 2010-05-18...
        files needed to recover state as of 2010-05-18:
        /backup/genwebupc/zeo11/secretariesub/2010-05-15-05-03-30.fs
        /backup/genwebupc/zeo11/secretariesub/2010-05-17-07-50-07.deltafs
        Recovering file to /tmp/Data_etseiat.fs
        Recovered 6635207 bytes, md5: a93ce32cebbc124d0f28a378779bc6c6
        root@mebsuta:/backup/genwebupc/zeo11/secretariesub# 

    4. Copiem la base de dades resultant que es troba a /tmp/Data_secretariesub.fs a Capricornius::

        scp root@mebsuta:/tmp/Data_secretariesub.fs /var/plone/backoffice/genwebupc4/var/filestorage/.

    5. A continuació, cal recuperar els blobs associats a la base de dades el dia que es vol recuperar. Podem trobar el backup dels blobs, separats per dies al directori: /backup/genwebupc/zeo11/blobs/ Es guarden els blobs diàriament i s'organitzen per carpetes dins del directori anterior en la forma /backup/genwebupc/zeo11/blobs/{diadelmes} Per això cal executar la següent comanda directament des de Capricornius::

        scp -r root@mebsuta:/backup/genwebupc/zeo11/secretariesub/blobs/XX /var/plone/backoffice/genwebupc4/var/blobstorage/secretariesub

    6. Actualitzar el fitxer /var/plone/backoffice/genwebupc4/buildout.cfg de Capricornius amb el nom de la BD ZODB que estem recuperant. Per exemple: secretariesub. Ha de tenir el mateix nom que té en el servidor d'explotació /var/plone/genwebupcZEO/produccio/instances/zeo11 (Mebsuta o Mebsuta2). Per fer-ho, obrim el fitxer i busquem la secció `filestorage` actualitzem la directiva `parts`::

        ...

        [filestorage]
        recipe = collective.recipe.filestorage
        parts = comunicacio
                espaitic
                serveisticalaupc
                secretariesub
        location = var/filestorage/Data_%(fs_part_name)s.fs
        blob-storage = var/blobstorage/%(fs_part_name)s
        
        ...

    7. Haurem de canviar el propietari i el grup dels fitxers que recuperem i col·loquem a Capricornius, doncs hauran de pertànyer a l'usuari i grup plone. Per lo tant::

        chown -R plone.plone /var/plone/backoffice/genwebupc4/var/blobstorage
        chown -R plone.plone /var/plone/backoffice/genwebupc4/var/filestorage

    8. Muntar el buildout per a que agafi la nova BD del fitxer instance executant l'script: /var/plone/backoffice/genwebupc/bin/buildout des del directori /var/plone/backoffice/genwebupc ::

            root@capricornius:/var/plone/backoffice/genwebupc4# ./bin/buildout
    
    9. Iniciar la instància amb el "foreground"::

        root@capricornius:/var/plone/backoffice/genwebupc4# ./bin/instance fg

    Pel fet de llençar-ho amb "fg" veurem tot el que fa, i quan s'aturi, comprovarem que no hi ha cap error i que ens diu que està tot correcte. Hem de veure una línia que posi, per exemple::

        2010-06-17 09:56:52 INFO Zope Ready to handle requests
    
    però encara no cancel·larem el procés (*).

    10. Cal accedir a : http://capricornius.upc.es:8880/manage amb l'usuari "admin" i la mateixa contrasenya, i muntar la nova ZODB des del menú Add de dalt, a la dreta: Escollir en el menú desplegable "ZODB Mount Point". En el formulari que apareix, deixar marcada la BD que volem muntar, i acceptar.

    11. Cal comprovar que tenim totes les dades que volem recuperar. Des del menú de l'esquerra (Root folder) escollirem la carpeta i/o fitxer que volem recuperar i, en l'espai central seleccionarem la caixeta (checkbox) on hi ha les dades que volem recuperar, i premerem el botó Import/Export de la part inferior de la finestra. Això ens deixarà les dades en un fitxer amb l'extensió *.zexp. i en la part superior del navegador veurem la ruta on ha deixat el fitxer. Per exemple::

        serveis_recuperats successfully exported to /var/plone/backoffice/genwebupc/var/instance/serveis_recuperats.zexp (2010-05-20 16:43)

    12. Recuperar les dades al servidor de producció (normalment Sylara o Sylarb) .
        Caldrà passar el fitxer *.zexp de Capricornius a Sylara. Ho farem amb l'scp. Per exemple::

        root@capricornius:/var/plone/backoffice/genwebupc4# scp /var/plone/backoffice/genwebupc4/var/instance/serveis_recuperats.zexp root@sylara:/root

    13. Arribats a aquest punt necessitem saber en quin entorn de Genweb està la instància que volem recuperar les dades. Tal i com hem comentat a l'inici, en l'exemple, secretariesub es troba en el entorn 11. Si desconeixem en quin entorn es troba, tenim diferents maneres de saber-ho:

        * Via la URL del site en producció, accedint a una vista especial (getZEO) que ens mostrarà l'entorn: http://www.upc.edu/secretariesub/getZEO
        * Accedint a Mebsuta i buscar en els fitxers de configuració de distribució d'instàncies: /var/plone/genwebupcZEO/produccio/instancies/

    14. Copiarem el que acabem de traspassar via scp a el directori del frontend corresponent a l'entorn dins de Sylara, en el exemple al ser l'entorn 11, hem de copiar-ho a la següent ubicació::

            root@sylara: cp /root/serveis_recuperats.zexp /var/plone/genwebupc/produccio/parts/zc11/import/.

    15. Li canviarem els permisos al fitxer per tal de poder-lo importar::

        root@sylara: chown plone.plone /var/plone/genwebupc/produccio/parts/zc11/import/*

    I comprovarem si els permisos són correctes::

        root@sylara: ls -lh /var/plone/genwebupc/produccio/parts/zc11/import/*

    16. Ara caldrà anar a la ZMI del frontend en el que volem fer la importació http://sylara.upc.es:11011/manage_main, situar-nos en el directori on volem fer la importació, escollir el fitxer zexp que acabem de deixar i prémer el botó Import/Export de la part inferior de la finestra. Un cop feta la importació, ja podrem accedir a la informació recuperada. Ho haurem de comprovar anant a la URL inicial que ens han facilitat en el tiquet.

    ..note::

        IMPORTANT: Abans de tancar la instancia de recover (*) amb un Ctrl + C, cal esborrar el punt de muntatge, seleccionant-lo des de l'arrel del Zope. I també haurem d'eliminar tots els fitxers que haviem recuperat de Mebsuta sobre Capricornius (els *.fs, *.dat, *.datafs, blobs, etc).

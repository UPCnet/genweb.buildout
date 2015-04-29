Migrar repositoris Git a GitLab
================================

Aquest és un procediment que hem de dur a terme a dins la maquina colladaverda::

    ssh root@colladaverda

Entrem a la carpeta on viuen els repositoris del gitlab a ::

    cd /var/gitlab/home/git/repositories

Fem una copia **bare** del repositori git, per exemple, si fos un repositori de github::

    git clone --bare -l https://github.com/UPCnet/unrepositori unrepositori.git

.. note::

    Recordeu de posar el .git al final!

Doneu els permisos adequats al nou repositori::

    chmod -R 770 unrepositori.git
    chown -R git.git unrepositori.git

Per últim, farem que el gitlab s'enteri de que hi ha un repositori nou, executant un procediment de migració. Si hem d'importar més d'un repositori, aquest últim pas el podem deixar pel final, per importar-los tots de cop::

     su gitlab
     cd /var/gitlab/gitlabhq
     bundle exec rake gitlab:import:repos RAILS_ENV=production

Per comprovar que el procediment ha funcionat, podem accedir al repositori a traves de https://git.upcnet.es/unrepositori.git.

Ara només ens queda donar permisos a qui pertoqui per poder accedir al repositori i afegir-lo al grup/s corresponents si s'escau.

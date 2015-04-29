Configuració del Sublime Text 2
===============================
:Url: http://www.sublimetext.com/2

Instal·lar el Sublime Package Control
-------------------------------------
Per a un millor control dels plugins, podem instal·lar una funcionalitat nova al Sublime que controla i administra els plugins:

 1. Obrir el SublimeText2.
 2. Activar la consola.
 3. Copy & paste::

	import urllib2,os; pf='Package Control.sublime-package'; ipp=sublime.installed_packages_path(); os.makedirs(ipp) if not os.path.exists(ipp) else None; urllib2.install_opener(urllib2.build_opener(urllib2.ProxyHandler())); open(os.path.join(ipp,pf),'wb').write(urllib2.urlopen('http://sublime.wbond.net/'+pf.replace(' ','%20')).read()); print 'Please restart Sublime Text to finish installation'

 4. Reiniciar el SublimeText2.
 5. Ara, podrem accedir al menú d'instal·lació de plugins nous a través del menú ràpid "super+shift+p" i escriure control. Això limitarà les comandes a les comandes del Package Control.
 6. Escollir la comanda que toqui (Install, Remove, List, ...)

Podeu trobar més informació a:

    http://wbond.net/sublime_packages/package_control/installation

Instal·lar paquets bàsics
-------------------------
Amb la comanda "super+shift+p" i amb el Package Control, instal·lar els següents plugins:

 * BracketHighlighter
 * SublimeLinter
 * SublimeCodeIntel
 * WordHighLight
 * Clipboard History
 * HTML5
 * Jquery
 * LESS
 * SCSS
 * Git
 * SidebarGit
 * Terminal

Tots són configurables des del menú d'opcions.

Plugins "a manija"
------------------
Decarregar, via Git:

 * https://github.com/buymeasoda/soda-theme/

Plugins del Dropbox
-------------------
Copiar des de la carpeta compartida del Dropbox de GC:

 * Zope
 * Buildout

Configuració d'usuari
---------------------
Configurar a partir d'aquí a gust de cadascun. Hi han configuracions base a la carpeta User del Dropbox. Podeu copiar els següents fitxers "a pèl":

 * Base File.sublime-settings
 * Python.sublime-settings
 * \*.sublime-snippets
 * Default{plataforma}.sublime-keymap

Instal·lar la command line
--------------------------
Útil per obrir fitxers en el editor des de línia de comandes.

Linux:

	.. code-block:: bash

	    ln -s "{Path en el que tinguem el sublime}/{binari del sublime}" /bin/slt

Mac OS X (http://www.sublimetext.com/docs/2/osx_command_line.html):

	.. code-block:: bash

	    	ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" /bin/slt

Altres plugins interssants
--------------------------

Disponibles al repositori de paquets (Package control):

	* **JSLint support for Sublime Text 2**
	* **Trailingspaces** - detector/eliminador d'espais en blanc

		- Un cop instal·lat afegir al fitxer `Key Bindings - User`::

				{ "keys": ["ctrl+shift+t"], "command": "delete_trailing_spaces" }

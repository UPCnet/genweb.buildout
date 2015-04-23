===================================
EGGS (paquets) que composen Genweb
===================================

genweb.core
-----------

És el paquet bàsic i principal del projecte. Dins del punt de vista de la totalitat i d'arquitectura del software del mateix, constitueix el pilar a on es sustenten tots els altres paquets i punt de partida dels mateixos. Aquest paquet és estratègic que només contingui funcionalitats i parametrització d'un hipotètic site Genweb. L'objectiu principal és que al instal·lar-lo el site resultant no contingui cap caracterítica diferenciadora en quant a "look and feel". Si per alguna raó ha de renderitzar en presentació alguna element o dependre en codi d'algun element, en cap manera aquest element ha de dependre d'altres paquets per al seu funcionament, al contrari, les dependències de paquets que declara i que instal·la són merament per afegir funcionalitats interessants al conjunt de funcionalitats de Genweb (p.e. Products.PloneFormGen).

genweb.controlpanel
-------------------

És el paquet que conté el nou panell de control de Genweb (a partir de 4.2). Es basa en plone.registry. Conté testos associats.

genweb.theme
------------

És el nou paquet que conté el tema (look and feel) i interfície de Genweb. És important que aquest paquet només contingui elements de personalització gràfica de *Genweb UPC*. No ha de contindre cap element funcional ni que aporti funcionalitat al conjunt.

genweb.stack
------------

És el paquet que conté dependències amb altres paquets que afegeixen funcionalitats interessants a Genweb.

genweb.portlets
---------------

És el paquet que conté tots els portlets personalitzats per Genweb, inclosos els overrides dels originals.

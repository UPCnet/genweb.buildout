===============================
Procés de migració a Genweb UPC
===============================

Existeix un procediment de migració des de un sistema genèric a un altre basat
en Genweb UPC. El procés consta de dues parts, l'exportació i la importació. El
procediment està concebut per a que es pugui executar 'over the wire' i
presuposa que el sistema origen i el destí estàn en màquines separades però
accessibles per xarxa. Aquest document explica en detall la part de exportació
per a que sigui compatible amb la part de importació de Genweb UPC.

Exportació
==========

L'exportació consta de dues parts: populació dels elements que es volen migrar i
l'exportació de les metadades i propietats dels elements prèviament populats.
Cadascun es materialitza en un web service de REST que retornen les dades
requerides en JSON.

En el procediment, el primer que es fa és una crida al webservice que popula els
elements a migrar. Un cop tenim la llista d'elements a migrar, per cada element,
es crida un altre web service que retorna les metadades i propietats de
l'element en qüestió.

A continuació es descriuen la forma i dades que retornen cada web service.

Populació dels elements a migrar
--------------------------------
Aquest web service torna un JSON amb una llista de recursos (elements) a migrar.
Aquests recursos serviran per forjar el web service usats de la part següent del
procediment que s'encarrega de migrar les dades de cada recurs.

La arrel de la URL del web service és configurable, però ha d'acabar en
/get_catalog_results. Per exemple: http://nom.servidor/directori/seccio/get_catalog_results

Ha de retornar en JSON una llista de recursos a migrar::

    [
        'http://nom.servidor/asd/asd',
        'http://nom.servidor/asd/asd2',
        'http://nom.servidor/asd/asd3',
    ]


Exportació de les metadades i propietats
----------------------------------------

Aquest web service ha de ser capaç de retornar, per cada element a migrar, una
representació en JSON de totes les seves metadades i propietats.

Es presuposa que si el sistema origen és diferent del de destí, s'haurà de fer
un mapeig de metadades i propietats per adaptar-les.

Com a exemple, aquesta és l'exportació d'un element base::

    {
      "_content_type_tableContents": "text/plain",
      "contributors": [],
      "_content_type_text": "text/html",
      "text": "<h4>Missi\u00f3</h4>\r\nDissenyem solucions a les necessitats de la UPC sobre la promoci\u00f3, l'aprenentatge, l'\u00fas i la qualitat de les lleng\u00fces. Treballem des del comprom\u00eds amb el catal\u00e0 com a llengua pr\u00f2pia i amb proactivitat davant dels reptes del multiling\u00fcisme i la interculturalitat. \r\n<table class=\"columnes\" summary=\"dues columnes\">\r\n<caption>Dues columnes de text<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /></caption>\r\n<tbody>\r\n<tr>\r\n<td>\r\n<h4>Valors</h4>\r\n</td>\r\n<td>\r\n<h4></h4>\r\n</td>\r\n</tr>\r\n<tr>\r\n<td>\r\n<ul>\r\n<li>Alineaci\u00f3 amb els objectius estrat\u00e8gics de la UPC</li>\r\n<li>Flexibilitat per respondre als reptes d'un entorn canviant </li>\r\n<li>Col\u00b7laboraci\u00f3 transversal amb les unitats de la UPC</li>\r\n<li>Millora cont\u00ednua com a organitzaci\u00f3 i com a professionals </li>\r\n<li>Il\u00b7lusi\u00f3 i comprom\u00eds de les persones </li>\r\n<li>Aliances i treball col\u00b7laboratiu interuniversitari</li>\r\n</ul>\r\n</td>\r\n<td class=\"separadorV\">\r\n<ul>\r\n<li>Executem l'enc\u00e0rrec de l'article 113 dels Estatuts de la UPC sobre pol\u00edtica ling\u00fc\u00edstica i serveis multiling\u00fces</li>\r\n<li>Coordinem el <a class=\"internal-link\" href=\"resolveuid/cdb9256287850fb88904883e97a249b4\" target=\"_self\">Pla de lleng\u00fces de la UPC</a></li>\r\n</ul>\r\n<ul style=\"line-height: 16px; color: rgb(0,0,0); font-size: 11px; \">\r\n<li>Sota la direcci\u00f3 del Vicerectorat de Pol\u00edtica Docent</li>\r\n</ul>\r\n<ul>\r\n<li>Dins l'\u00c0rea de Planificaci\u00f3, Qualitat i Projectes Transversals</li>\r\n</ul>\r\n<ul>\r\n</ul>\r\n</td>\r\n</tr>\r\n</tbody>\r\n</table>\r\n<br /><br /><img class=\"image-inline\" height=\"525\" src=\"resolveuid/92a9b760-ae72-4a59-a4be-3ef961390263/@@images/image/large\" width=\"702\" /><br />",
      "creation_date": "2012-06-20 12:32",
      "_uid": "9b7c9fec-b32c-4d4a-81e4-204458be6814",
      "_content_type_id": "text/plain",
      "id": "missio-valors-arees",
      "subject": [],
      "_content_type_excludeFromNav": "text/plain",
      "_content_type_subject": "text/plain",
      "modification_date": "2015-03-03 15:14",
      "title": "El Servei de Lleng\u00fces i Terminologia",
      "_local_roles_block": false,
      "_content_type_language": "text/plain",
      "_defaultpage": "document_view",
      "location": "",
      "_content_type_title": "text/plain",
      "excludeFromNav": false,
      "presentation": false,
      "_type": "Document",
      "description": "",
      "_atrefs": {
        "isReferencing": ["/slt/slt/imatges/servei-de-llengues-i-terminologia/resultats-i-missio", "/slt/slt/pla-llengues-upc"]
      },
      "_layout": "",
      "_workflow_history": {
        "genweb_simple": [{
          "action": null,
          "review_state": "visible",
          "comments": "",
          "actor": "carme.tarin",
          "time": "2012/06/20 12:32:56.354098 GMT+2"
        }, {
          "action": "publish",
          "review_state": "published",
          "actor": "carme.tarin",
          "comments": "",
          "time": "2012/06/21 09:20:14.299930 GMT+2"
        }]
      },
      "_content_type_rights": "text/plain",
      "_local_roles": {
        "carme.tarin": ["Owner"]
      },
      "allowDiscussion": false,
      "_content_type_allowDiscussion": "text/plain",
      "_classname": "ATDocument",
      "_translationOf": "/servei-llengues-terminologia/missio-valors-arees",
      "_canonicalTranslation": true,
      "_content_type_presentation": "text/plain",
      "tableContents": false,
      "_userdefined_roles": [],
      "_content_type": "text/html",
      "_zopeobject_document_src": "",
      "_id": "missio-valors-arees",
      "effectiveDate": "2012-06-21 09:20",
      "language": "ca",
      "rights": "",
      "_atbrefs": {
        "translationOf": ["/slt/slt/language-and-terminology-service/mission-values-and-areas-of-competence"]
      },
      "_translations": {
        "ca": "/servei-llengues-terminologia/missio-valors-arees",
        "en": "/language-and-terminology-service/mission-values-and-areas-of-competence"
      },
      "_content_type_creators": "text/plain",
      "_content_type_description": "text/plain",
      "_owner": "carme.tarin",
      "_content_type_location": "text/x-unknown-content-type",
      "_permissions": {
        "Modify portal content": {
          "acquire": false,
          "roles": ["Editor", "Manager", "Owner", "Site Administrator"]
        },
        "Delete objects": {
          "acquire": false,
          "roles": ["Editor", "Manager", "Owner", "Site Administrator"]
        },
        "Access contents information": {
          "acquire": false,
          "roles": ["Anonymous", "Editor", "Manager", "Owner", "Reader", "Site Administrator"]
        },
        "View": {
          "acquire": false,
          "roles": ["Anonymous", "Editor", "Manager", "Owner", "Reader", "Site Administrator"]
        }
      },
      "_properties": [
        ["title", "El Servei de Lleng\u00fces i Terminologia", "string"]
      ],
      "_content_type_contributors": "text/plain",
      "_gopip": 0,
      "creators": ["carme.tarin"],
      "_path": "/slt/slt/servei-llengues-terminologia/missio-valors-arees"
    }

Aquests són tots els camps que s'exporten d'un sistema Plone (Genweb antic) a un
Genweb UPC 4. A continuació s'exposen els imprescindibles per a realitzar una
exportació vàlida al sistema destí i quina és la seva funció.

"id": ID del element. Forma part de la URL, per lo que ha de contrindre ASCII.
"_id": ID del element. Forma part de la URL, per lo que ha de contrindre ASCII.
"title": Títol del element.
"text": HTML contingut al camp de text enriquit de l'element.
"subject": Llista de paraules clau (tags)
"description": Descripció de l'element.
"creation_date": Data de creació
"modification_date": Data de modificació
"effectiveDate": Data efectiva
"excludeFromNav": Exclou l'element de la navegació
"_type": Tipus de document, a escollir entre els disponibles en Genweb 4
(Document, Folder, News Item, Event, Link, Image, File)
"language": Idioma de l'element (ca, es, en)
"_properties": Llista de propietats Zope de l'element (important: posar al
menys l'element title, tal i com apareix al exemple.)
"_path": A on volem que jeràrquicament es migri l'element al sistema destí.

Si es volen migrar imatges, aquesta és l'esquema que hem de retornar::

  {
    "contributors": [],
    "creation_date": "2014-07-08 10:18",
    "_uid": "6d735eeb-a2f6-4d7a-9ddc-9dd51d945ce5",
    "_content_type_id": "text/plain",
    "id": "are_you_new_pla_lleng_cacopia.jpg",
    "subject": [],
    "_content_type_excludeFromNav": "text/plain",
    "_content_type_subject": "text/plain",
    "modification_date": "2014-07-08 10:18",
    "title": "Acabes d'arribar a Catalunya?",
    "_local_roles_block": false,
    "_content_type_language": "text/plain",
    "location": "",
    "_content_type_title": "text/plain",
    "excludeFromNav": false,
    "_atbrefs": {
      "isReferencing": ["/slt/slt/acollida/cursos"]
    },
    "_type": "Image",
    "description": "",
    "_atrefs": {},
    "_workflow_history": {
      "genweb_simple": [{
        "action": null,
        "review_state": "visible",
        "actor": "carme.tarin",
        "comments": "",
        "time": "2012/02/21 10:00:5.160680 GMT+1"
      }, {
        "action": "publish",
        "review_state": "published",
        "actor": "carme.tarin",
        "comments": "",
        "time": "2012/02/21 10:00:9.029522 GMT+1"
      }]
    },
    "_content_type_rights": "text/html",
    "_local_roles": {
      "carme.tarin": ["Owner"]
    },
    "_content_type_contributors": "text/plain",
    "_content_type_allowDiscussion": "text/plain",
    "_classname": "ATBlob",
    "_translationOf": "/imatges/homites/are_you_new_pla_lleng_cacopia.jpg",
    "_canonicalTranslation": true,
    "_datafield_image": {
      "size": 69303,
      "filename": "are_you_new_pla_lleng_ca copia.jpg",
      "content_type": "image/jpeg",
      "data_uri": "http://www.upc.edu/slt/imatges/homites/are_you_new_pla_lleng_cacopia.jpg/at_download/image"
    },
    "_userdefined_roles": [],
    "_content_type": "image/jpeg",
    "_zopeobject_document_src": "",
    "_id": "are_you_new_pla_lleng_cacopia.jpg",
    "_gopip": 16,
    "language": "ca",
    "rights": "",
    "_translations": {
      "ca": "/imatges/homites/are_you_new_pla_lleng_cacopia.jpg"
    },
    "_content_type_creators": "text/plain",
    "_content_type_description": "text/plain",
    "_owner": "carme.tarin",
    "_content_type_location": "text/x-unknown-content-type",
    "_permissions": {},
    "_properties": [
      ["title", "Acabes d'arribar a Catalunya?", "string"]
    ],
    "allowDiscussion": false,
    "creators": ["carme.tarin"],
    "_path": "/slt/slt/imatges/homites/are_you_new_pla_lleng_cacopia.jpg"
  }

Amb especial atenció al camp::

  "_datafield_image": {
      "size": El tamany
      "filename": El ID
      "content_type": El content type de la imatge
      "data_uri": La URL de la imatge a on descarregar-la
    },

i per fitxers::

  {
    "contributors": [],
    "creation_date": "2014-11-25 13:15",
    "_uid": "569a57e7-4f4a-4d87-85a0-5d50d1c2ab15",
    "_content_type_id": "text/plain",
    "id": "cursos-de-tardor-2014",
    "subject": [],
    "_content_type_excludeFromNav": "text/plain",
    "_content_type_subject": "text/plain",
    "modification_date": "2014-11-25 13:15",
    "title": "Cursos de tardor 2014",
    "_local_roles_block": false,
    "_content_type_language": "text/plain",
    "location": "",
    "_content_type_title": "text/plain",
    "excludeFromNav": false,
    "_atbrefs": {
      "isReferencing": ["/slt/slt/cursos/anys-anteriors"]
    },
    "_type": "File",
    "description": "",
    "_atrefs": {},
    "_workflow_history": {
      "genweb_simple": [{
        "action": null,
        "review_state": "visible",
        "actor": "carme.tarin",
        "comments": "",
        "time": "2012/11/07 12:45:56.988526 GMT+1"
      }, {
        "action": "publish",
        "review_state": "published",
        "actor": "carme.tarin",
        "comments": "",
        "time": "2012/11/07 12:46:1.391550 GMT+1"
      }]
    },
    "_content_type_rights": "text/plain",
    "_local_roles": {
      "carme.tarin": ["Owner"]
    },
    "_datafield_file": {
      "size": 2916661,
      "filename": "2014_cursos_tardor.pdf",
      "content_type": "application/pdf",
      "data_uri": "http://www.upc.edu/slt/cursos/programacio-slt/cursos-de-tardor-2014/at_download/file"
    },
    "_content_type_contributors": "text/plain",
    "_content_type_allowDiscussion": "text/plain",
    "_classname": "ATBlob",
    "_translationOf": "/cursos/programacio-slt/cursos-de-tardor-2014",
    "_canonicalTranslation": true,
    "_userdefined_roles": [],
    "_content_type": "application/pdf",
    "_zopeobject_document_src": "",
    "_id": "cursos-de-tardor-2014",
    "_gopip": 12,
    "language": "ca",
    "rights": "",
    "_translations": {
      "ca": "/cursos/programacio-slt/cursos-de-tardor-2014"
    },
    "_content_type_creators": "text/plain",
    "_content_type_description": "text/plain",
    "_owner": "carme.tarin",
    "_content_type_location": "text/x-unknown-content-type",
    "_permissions": {},
    "_properties": [
      ["title", "Cursos de tardor 2014", "string"]
    ],
    "allowDiscussion": false,
    "creators": ["carme.tarin"],
    "_path": "/slt/slt/cursos/programacio-slt/cursos-de-tardor-2014"
  }

igualment amb especial atenció al camp::

  "_datafield_file": {
      "size": El tamany
      "filename": El ID del fitxer (ASCII)
      "content_type": El content type
      "data_uri": La URL del fitxer a descarregar
    },

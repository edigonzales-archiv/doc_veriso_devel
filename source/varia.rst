Varia
=====
Das Kapitel *Varia* behandelt Themen von konkreten Umsetzungen einer Fachschale. Die vorgestellten Lösungen können selbstverständlich auch für andere Umsetzungen/Fachschalen verwendet werden. 


Topics-Table-Loader (VeriSO EE)
-------------------------------
Dabei handelt es sich um eine Funktion einer Fachschale, die es erlaubt einzelne Tabellen oder ganze Topics des Datenmodells aus der Datenbank in QGIS zu laden. Dazu muss das Interlismodell in eine Json-Datei umgewandelt werden, anhand dieser QGIS das GUI dynamisch aufbauen kann:

.. figure::  images/topicstablesloader1.png
   :align:   center

   Topics-Table-Loader

Die Json-Datei muss für jedes Datenmodell einmalig erstellt werden; jedoch **nicht** pro Bezugsrahmen. Dazu kann eine Properties-Datei eines vorangegangen Imports verwendet werden oder es kann nach folgendem Schema eine neue erstellt werden:

::

   dbhost = localhost
   dbname = veriso_test
   dbschema = test44
   dbport = 5432
   dbuser = veriso_user
   dbpwd = veriso_user
   dbadmin = veriso_admin
   dbadminpwd = veriso_admin

   epsg = 21781

   vacuum = false
   reindex = false

   importModelName = DM01AVCH24D
   importItfFile = /home/stefan/tmp/veriso/ch_254900_fehler.itf

   enumerationText = true
   renumberTid = true

   schemaOnly = false

   qgisFiles = true

   postprocessingDatabase = /home/stefan/.qgis2/python/plugins/veriso/modules/veriso_ee/postprocessing/postprocessing.db


Bis auf den Parameter *qgisFile = true* können Fantasiewerte verwendet werden, da man bei diesem Schritt nur die Json-Datei erzeugen will. Folgender Befehl erzeugt die Datei:

::

    java -jar /home/stefan/Apps/veriso/veriso.jar /tmp/1407087399.21.properties

Der Importprozess wird mit einer Fehlermeldung abgebrochen (aufgrund der Fantasiewerte oder des bereits vorhandenen Schemas etc.). Im ``/tmp/``-Verzeichnis wird aber ein neues Verzeichnis erstellt: ``veriso + Zufallszahl``. In diesem liegt die Datei ``tables.json``. Diese Datei muss in den Ordner ``modules/MODULNAME/tables/`` kopiert werden.

Die Datei muss analog den anderen JSON-Dateien einmalig für die Mehrsprachigkeit manuell bearbeit werden (siehe Kapitel :ref:`mehrsprachigkeit` resp. :ref:`complexchecks`). Zur Zeit steht für die französische Übersetzung ein Platzhalter in der JSON-Datein (Tabellenname + "_fr").

Dieser ganzer Herstellungsprozess ist natürlich noch bisschen hakelig... aber da er nur einmalig gemacht werden muss, malesh!


Baselayer (VeriSO EE)
---------------------
Zum schnellen Laden von Hintergrundkarten etc. gibt es die Funktion *Baselayer*. In einer JSON-Datei (``modules/veriso_ee/baselayer/baselayer.json``) können WMS- und Datenbankverbindungsparamater hinterlegt werden. Die JSON-Datei wird beim Start des Plugins geladen und alle eingetragenen Layer werden in einem Menu angezeigt:

.. figure::  images/baselayer_01.png
   :align:   center

   Baselayer #1

Die dazu passende JSON-Datei sieht so aus:

::
 
 {  
   "baselayer":[  
      {  
         "type":"wms",
         "title":{  
            "de":"Orthofoto (RGB)",
            "fr":"Orthophoto (RGB)"
         },                  
         "url":"http://www.catais.org/wms/orthofoto",
         "layers":"Orthofoto_RGB",
         "format":"image/jpeg"
      },
      {  
         "type":"wms",
         "title":{  
            "de":"Orthofoto (CIR)",
            "fr":"Orthophoto (CIR)"
         },                  
         "url":"http://www.catais.org/wms/orthofoto",
         "layers":"Orthofoto_CIR",
         "format":"image/jpeg"
      },
      {  
         "type":"wms",
         "title":{  
            "de":"Plan für das Grundbuch (farbig)",
            "fr":"Plan du registre foncier (coloré)"
         },         
         "url":"http://www.catais.org/wms/grundbuchplan",
         "layers":"Amtliche Vermessung (farbig)",
         "format":"image/jpeg"
      },
      {  
         "type":"wms",
         "title":{  
            "de":"Plan für das Grundbuch (grau)",
            "fr":"Plan du registre foncier (gris)"
         },         
         "url":"http://www.catais.org/wms/grundbuchplan_grau",
         "layers":"Amtliche Vermessung (grau)",
         "format":"image/jpeg"
      },
      {  
         "type":"wms",
         "title":{  
            "de":"Plan für das Grundbuch (schwarz-weiss)",
            "fr":"Plan du registre foncier (noir et blanc)"
         },         
         "url":"http://www.catais.org/wms/grundbuchplan",
         "layers":"Amtliche Vermessung (schwarz-weiss)",
         "format":"image/jpeg"
      },
      {  
         "type":"wms",
         "title":"AV-WMS (farbig)",
         "url":"http://www.catais.org/wms/avwms",
         "layers":"AVWMS_farbig",
         "format":"image/jpeg"
      },
      {  
         "type":"wms",
         "title":"AV-WMS (schwarz-weiss)",
         "url":"http://www.catais.org/wms/avwms",
         "layers":"AVWMS_sw",
         "format":"image/jpeg"
      },
      {  
         "type":"wms",
         "title":"AV-WMS V+D (farbig)",
         "url":"http://LOGINNAME:PASSWORT@geodata01.admin.ch/SWMS",
         "layers":"av_wms",
         "format":"image/jpeg"
      },
      {  
         "type":"wms",
         "title":"Basisplan 1:5000 (schwarz-weiss)",
         "url":"http://www.sogis1.so.ch/cgi-bin/sogis/sogis_bpav.wms",
         "layers":"bpav5000sw",
         "format":"image/jpeg"
      },
      {  
         "type":"wms",
         "title":{  
            "de":"Basisplan 1:5000 (grau)",
            "fr":"Plan de base 1: 5000 (gris)"
         },
         "url":"http://www.sogis1.so.ch/cgi-bin/sogis/sogis_bpav.wms",
         "layers":"bpav5000sw_grau",
         "format":"image/jpeg"
      },
      {  
         "type":"postgres",
         "title":"PostgreSQL Test (Temporaer)",
         "params":{  
            "dbhost":"localhost",
            "dbport":5432,
            "dbname":"veriso_test",
            "dbschema":"test1",
            "dbuser":"veriso_user",
            "dbpwd":"veriso_user",
            "dbadmin":"",
            "dbadminpwd":""
         },
         "featuretype":"bodenbedeckung_boflaeche",
         "geom":"geometrie",
         "key":"ogc_fid",
         "sql":"",
         "readonly":1,
         "style":"test/test_poly.qml"
      }
   ]
 } 

Die Übersetzung wird gleich gehandhabt wie bei anderen JSON-Dateien (siehe :ref:`complexchecks`).


Mängeltabelle (VeriSO EE / PNF-Homog.)
--------------------------------------
Die Mängeltabellen (neu: Punkt *und* Linie) sind als Postprocessing-Schritt (siehe :ref:`postprocessing`
) umgesetzt. Dh. in der SQlite-Datenbank ``modules/veriso_ee/postprocessing/postprocessing.db`` müssen verschieden Einträge vorgenommen werden.

1. Eintrag in der Tabelle *tables* zum Erzeugen der Mängeltabellen während des Importprozesses.
2. Eintrag in der Tabelle *inserts*. Dabei werden die Mängelgruppen (in diesem Fall die Interlistopics) in einer Tabelle gespeichert.

Insgesamt werden drei Tabellen erzeugt. Zwei zum Speichern der eigentlichen Mängel (*t_maengel_punkt*, *t_maengel_linie*) und eine mit den Mängelgruppen (*t_maengel_topcis*). In QGIS (nach dem Laden der Mängel) sieht das so aus:

.. figure::  images/maengel_01.png
   :align:   center

   Mängel #1

Der Layer *Informationsebenen* darf nicht entfernt werden, da die beiden Mängellisten-Layer mit diesem verknüpft sind. Der Grund für dieses (auf den ersten Blick) komplizierte Vorgehen ist das bessere Verhalten von QGIS beim Verändern von bereits bestehenden Mängeln im Gegensatz zur Lösung der ersten Version von VeriSO (Custom UI Datei). 

Sollen ebenfalls die Informationsebenen übersetzt werden, muss wie folgt vorgegangen werden: Die Tabellen *t_maengel_topics* ist mit weiteren *topic_name*-Spalten zu ergänzen, also zB. *topic_name_fr*:

::

 CREATE TABLE $$DBSCHEMA.t_maengel_topics
 (
  ogc_fid serial NOT NULL, 
  topic_name varchar NOT NULL,
  topic_name_fr  varchar NOT NULL,
  CONSTRAINT t_maengel_topics_pkey PRIMARY KEY (ogc_fid)
 ) 
 WITH (OIDS=FALSE); 
 GRANT SELECT ON TABLE $$DBSCHEMA.t_maengel_topics TO $$USER;

Fallbackebene (falls die in QGIS gewählte Sprache nicht vorhanden ist) ist immer die Spalte *topic_name*. Ggf sind die *inserts*-Befehle anzupassen:

::

 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('FixpunkteKategorie1', 'Points_fixesCategorie1');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('FixpunkteKategorie2', 'Points_fixesCategorie2');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('FixpunkteKategorie3', 'Points_fixesCategorie3');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Bodenbedeckung', 'Couverture_du_sol');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Einzelobjekte', 'Objets_divers');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Hoehen', 'Altimetrie');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Nomenklatur', 'Nomenclature');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Liegenschaften', 'Nomenclature');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Rohrleitungen', 'Conduites');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Nummerierungsbereiche', 'Domaines_numerotation');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Gemeindegrenzen', 'Limites_commune');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Bezirksgrenzen', 'Limites_district');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Kantonsgrenzen', 'Limites_canton');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Landesgrenzen', 'Limites_nationales');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Planeinteilungen', 'Repartitions_plans');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('TSEinteilung', 'RepartitionNT');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Rutschgebiete', 'Zones_glissement');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('PLZOrtschaft', 'NPA_Localite');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Gebaeudeadressen', 'Adresses_des_batiments');
 INSERT INTO $$DBSCHEMA.t_maengel_topics (topic_name, topic_name_fr) VALUES('Planrahmen', 'Bords_de_plan');
  




Varia
=====
Das Kapitel *Varia* behandelt Themen von konkreten Umsetzungen einer Fachschale. Die vorgestellten Lösungen können selbstverständlich auch für andere Umsetzungen/Fachschalen verwendet werden. 


Topics-Table-Loader (VeriSO EE)
----------------------------
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

Dieser ganzer Herstellungsprozess ist natürlich noch bisschen hakelig... aber da er nur einmalig gemacht werden muss, malesh!


Mängeltabelle (VeriSO EE / PNF-Homog.)
--------------------------------------
"Mängel auch als Postprocessing." erwähnen oder sep. Kapitel? hier eher. ah, aber vielleicht doch unterkapiel oder separat, da erkärt wird, dass die gejoined werden. oder egal. Verweis wieder auf Mehrsprachigkeit.

:ref:`postprocessing`


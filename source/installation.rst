Installation
============

Komponenten
-----------
Es werden verschiedene Software(-komponenten) benötigt:

* QGIS: Frontend für Benutzer zum Durchführen der Prüfungen.
* VeriSO: QGIS-Plugin. Steuert die Import- und Exportprozesse und führt den Verifikationr durch die Prüfungen.
* PostgreSQL/Postgis: Datenhaltung und Geoprozesse.
* VeriSO-Java: Importroutine (Interlis -> PostgreSQL)
* x2go: Terminalserver-Lösung

.. note:: Nachfolgend wird der Installationsprozess für Ubuntu 14.04 64bit erläutert. Es handelt sich dabei um eine (1) Möglichkeit. Die Pogrammversionen entsprechen den in den verschiedenen Repositories vorhandenen Versionen vom August 2014.

Ubuntugis Repository
--------------------
Das Ubuntugis Repository stellt aktuelle(re) Versionen von GIS-Komponenten für Ubuntu zur Verfügung. Dazu sind folgenden zwei Zeilen in der Datei ``/etc/apt/sources.list`` hinzufügen:

::

    deb http://ppa.launchpad.net/ubuntugis/ubuntugis-unstable/ubuntu trusty main
    deb-src http://ppa.launchpad.net/ubuntugis/ubuntugis-unstable/ubuntu trusty main

Anschliessend muss noch der Schlüssel hinzugefügt werden:

::
   
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 314DF160
    sudo apt-get update

Falls der Server hinter einem Proxy steht, kann mit folgendem Befehl der Port 80 verwendet werden:

::
    
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80/ --recv-key 314DF160
    sudo apt-get update


PostgreSQL 9.3 / PostGIS 2.1
----------------------------
::

    sudo apt-get install postgresql
    sudo apt-get install postgis
    sudo apt-get install postgresql-9.3-postgis-scripts
    sudo apt-get install pgadmin3



QGIS
----
Zur Zeit (August 2014) läuft VeriSO mit QGIS 2.4 und QGIS master. Wird VeriSO als Dienst angeboten und läuft aus diesem Grund auf einem Server, wird empfohlen QGIS selber zu kompilieren. Hauptvorteil ist vor allem die Möglichkeit verschiedene QGIS-Versionen parallel installiert zu haben.

.. note:: Treten Fehlermeldungen auf, bitte zuerst immer die Permission kontrollieren. Wird QGIS nicht im Home-Verzeichnis kompiliert und installiert, muss der User (der die Software kompiliert und installiert) entweder die benötigten Rechte haben oder die Aktonen müssen als *root* resp. *sudo* ausgeführt werden.

Abhängigkeiten
**************
::
   
    sudo apt-get build-dep qgis
    sudo apt-get install cmake-curses-gui cmake-qt-gui gdal-bin python-gdal python-qscintilla2 libqscintilla2-dev

Quellen herunterladen
*********************
Die Quellen werden im Verzeichnis ``/usr/local/src/qgis/qgis_master/`` resp. ``/usr/local/src/qgis/qgis_24/``  gespeichert.

Master
''''''
::

    git clone git://github.com/qgis/QGIS.git qgis_master

2.4
'''
Die Quellen für die Version 2.4 können `hier <http://qgis.org/downloads/qgis-2.4.0.tar.bz2>`_ heruntergeladen werden.


Kompilieren
***********
Im Quellverzeichnis ein Verzeichnis ``build/`` erstellen. In der Konsole in dieses Verzeichnis wechseln und den Befehl ``cmake-gui`` ausführen.





Optional
--------
linguist ist in devtools

Nicht vergesse
--------------
xlwt -> abhängigkeit veriso.

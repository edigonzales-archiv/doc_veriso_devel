# README #

### Installation (Ubuntu 14.04) ###

* `sudo apt-get install python-setuptools`
* `sudo easy_install -U Sphinx`
* `sudo easy_install pip`
* [Bootstrap-Theme](https://pypi.python.org/packages/source/s/sphinx-bootstrap-theme/sphinx-bootstrap-theme-0.4.0.tar.gz) herunterladen und entpacken.
* Im Verzeichnis: `sudo pip install sphinx_bootstrap_theme`
* `conf.py` [anpassen](https://pypi.python.org/pypi/sphinx-bootstrap-theme/)

### Dokumentieren ###

Im Root-Verzeichnis reicht der Aufruf `make html` um die HTML-Seiten neu zu erzeugen. Eventuell auch mal ein `make clean` ausführen. Das löscht das *build*-Verzeichnis.

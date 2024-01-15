# Entwicklung und Bau der DiGA-Konfiguration f�r den KoSIT Validator

Die im Repository enthaltene Apache Ant Datei l�dt Abh�ngigkeiten automatisch in ein `lib` Verzeichnis runter und erstellt eine Zip-Datei der Konfiguration.

## Anforderungen

+ Java Runtime Environment, Version 1.8 oder sp�ter. 
+ [Apache Ant](https://ant.apache.org) (Unter Version 1.10.9 erstellt, andere Versionen ungetestet)

## Bau der Konfiguration

Fertige Konfigurationen k�nnen von der GitHub Action
[XSLT CI](https://github.com/ITSGGMBH/validator-configuration-diga/actions?query=workflow%3A%22XSLT+CI%22)
bezogen werden.
Zum Selber-Bauen des aktuellen Commits ben�tigen Sie Apache Ant.
Die Konfiguration k�nnen Sie mit dem folgenden Befehl bauen:

```bat
    ant build
```

Das Ergebnis befindet sich dann im Verzeichnis `build`.

## Abh�ngigkeiten

W�hrend des Build-Vorgangs werden einige Abh�ngigkeiten heruntergeladen.

+ XRechnung 2.2 Validierung 2022-11-15
+ Saxon HE 10.6
+ KoSIT XML Validator 1.5.0 (F�r Testdurchf�hrung; andere Versionen wie 1.4.2 generell auch m�glich)
+ SchXslt 1.8.5

## Ant Targets

Es sind folgende Ant Targets definiert:

* `clean` Leert das `build` Verzeichnis.
* `lib-clean` Leert das `lib` Verzeichnis. Ruft implizit `clean` auf.
* `build` Ruft Abh�ngigkeiten ab, falls diese nicht existieren und erstellt eine Zip-Datei der Konfiguration.
* `test` F�hrt alle Tests durch. Ruft implizit `build` auf.
* `runtest` F�hrt einen einzelnen Testbereich durch. Hierf�r muss auch der Parameter `test.group` angegeben werden, der gleich eines der Unterverzeichnisse von `src/test/resources` ist. Ruft implizit `build` auf.

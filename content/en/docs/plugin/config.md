---
title: "Konfiguration"
description: "Konfigurationsparameter für das Gradle Plugin."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 20
menu:
  docs:
    parent: "plugin"
toc: true
---

## Ermittlung von Konfigurationswerten

### Umgebung

Die Umgebung wird, sofern sie vom Task benutzt wird, über den Parameter **environment**
des Tasks gesetzt (mittels `-Penvironment=<umgebung>`). Wird dieser Parameter nicht gesetzt, so wird
die Umgebung `default` verwendet.

#### Beispiel

```
./gradlew mergeScripts -Penvironment=testEnvironment
```


### Mandant

Der Mandant wird mit folgender Hierarchie ermittelt. 
Dabei wird von oben nach unten vorgegangen und der erste nicht-null Wert verwendet.

* Parameter **mandant** bei Aufruf des Tasks (mittels `-Pmandant=<mandant>`)
* der in der Konfigurationsdatei der Umgebung definierte Mandant 
* der in der Datei <a target="_blank" href="/docs/plugin/structure/#projectjson">config/project.json</a> definierte Mandant 

#### Beispiel

```
./gradlew mergeScripts -Pmandant=2034
```

### Name und Version des Prozessmodells

Name und Version des Prozessmodells werden aus der Datei <a target="_blank" href="/docs/plugin/structure/#projectjson">config/project.json</a> gelesen.

### Status der Prozessmodell-Version

Der aktive Status des Prozessmodells wird aus der Konfigurationsdatei der Umgebung gelesen. 


### Prozess-Engine für Deployment
Die ID der Prozess-Engine, auf die eine Prozessmodell-Version deployt werden soll, wird, sofern vorhanden, aus der Konfigurationsdatei der Umgebung gelesen.



---
title: "startLocalHttpServer"
description: "Startet einen lokalen Server auf einer beliebigen Serviceportal Umgebung um Formulare und Prozesse editieren zu können."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 200
menu:
  docs:
    parent: "tasks"
toc: true
---


## Beispiel

```shell
./gradlew startLocalHttpServer
```

## Parameter

| Parameter | Pflicht? | Beschreibung |
| --- | --- | --- |
| mandant | Nein | Überschreibt den im config-Verzeichnis festgelegten Mandanten. |
| environment | Nein | Definiert die Umgebung, deren Konfiguration verwendet wird. Wird dieser Parameter nicht verwendet, so wird die Umgebung "default" verwendet.|
| debug | Nein | Wenn der Wert des Parameters "true" ist, werden weitere debug-Ausgaben durch das Plugin ausgegeben. |


## Beschreibung

Startet einen lokalen Server, um auf einer beliebigen Serviceportal-Umgebung die auf dem lokalen 
Rechner des Entwickler liegenden Dateien des Entwicklungsprojektes (Formulare und Prozesse) 
editieren zu können.

In der Konsole wird ein Link zu einer Übersichtsseite angezeigt, auf welcher die zur
Bearbeitung verfügbaren Dateien verlinkt sind. Durch Klick auf den Link wird die entsprechende Seite 
der Umgebung im Browser geöffnet.

Mit dem Parameter `environment` kann (wie bei den anderen Tasks) die gewünschte Umgebung gewählt 
werden, auf welcher die Datei bearbeitet werden soll. Der Parameter `port` kann den Server auf
einem definierten lokalen Port starten (sofern dieser frei ist).

Es kann nur jeweils eine Instanz des Servers gestartet werden. Um den Server zu beenden, kann in der 
Übersichtsseite auf der entsprechende Link verwendet bzw. auf der Konsole der dazu bereitgestellte 
Task verwendet werden.

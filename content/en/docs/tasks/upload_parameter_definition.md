---
title: "Task uploadParameterDefinition"
description: "Lädt eine Prozessparameterdefinition für einen Prozess in das Admincenter hoch."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 140
menu:
  docs:
    parent: "tasks"
toc: true
---

## Beispiel

```shell
./gradlew uploadParameterDefinition
```


## Parameter

| Parameter | Pflicht? | Beschreibung |
| --- | --- | --- |
| mandant | Nein | Überschreibt den im config-Verzeichnis festgelegten Mandanten. |
| environment | Nein | Definiert die Umgebung, deren Konfiguration verwendet wird. Wird dieser Parameter nicht verwendet, so wird die Umgebung "default" verwendet.|
| debug | Nein | Wenn der Wert des Parameters "true" ist, werden weitere debug-Ausgaben durch das Plugin ausgegeben. |

## Beschreibung

Dieser Task lädt eine Prozessparameterdefinition für einen Prozess in das Admincenter hoch.
Eine eventuell bereits vorhandene Parameterdefinition wird überschrieben. 
Die Prozessparameterdefinition wird in diesem Task NICHT sofort deployt; das Deployment
findet beim Deployment des Prozesses statt. 

Mandant, Name und Version des Prozesses, für den die Parameterdefinition hochgeladen werden soll,
werden wie im Kapitel "Ermittlung von Konfigurationswerten" beschrieben
aus der Konfiguration gelesen.

Der Name der konfigurierten Umgebung bestimmt den Dateinamen der hochgeladenen Parameterdefinition.
Standardmäßig wird die Datei `parameterdefinitions/${nameDerUmgebung}.json` verwendet. 
Existiert diese Datei nicht oder wird keine Umgebung angegeben, so werden die 
Prozessparameterdefinitionen aus der Datei `parameterdefinitions/default.json` verwendet.

Wenn das angegebene Prozessmodell oder die angegebene Version im konfigurierten Mandanten 
im Admincenter nicht existiert, wird ein Fehler geworfen.

## Aufrufparameter

Alle globalen Aufrufparameter beeinflussen den Task wie angegeben.
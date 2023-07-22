---
title: "Task buildModel"
description: "Fügt mit `mergeScripts` zusammengefügte Skripte in die Prozessmodelle ein."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 130
menu:
  docs:
    parent: "tasks"
toc: true
---


## Beispiel

```shell
./gradlew buildModel
```

## Parameter

| Parameter | Pflicht? | Beschreibung |
| --- | --- | --- |
| mandant | Nein | Überschreibt den im config-Verzeichnis festgelegten Mandanten. |
| environment | Nein | Definiert die Umgebung, deren Konfiguration verwendet wird. Wird dieser Parameter nicht verwendet, so wird die Umgebung "default" verwendet.|
| debug | Nein | Wenn der Wert des Parameters "true" ist, werden weitere debug-Ausgaben durch das Plugin ausgegeben. |

## Beschreibung

Dieser Task fügt die (mit dem Task _mergeScripts_ zusammengefügten) Skripte in die Prozessmodelle ein, die im Verzeichnis `models` liegen,  und erweitert ggf. den Namen des Prozesses mit der für die angezogene Umgebung
 konfigurierten processModelNameExtension.

Die Skripte werden nach folgendem Schema 
`build/scripts/[ID des Prozesmodells]/[ID des Skript-Tasks].groovy`
den Skript-Tasks zugeordnet.  

Die gebauten Prozessmodelle werden in das Verzeichnis `build/models` geschrieben. 


## Aufrufparameter

Die globalen Aufrufparameter **environment** und **debug** beeinflussen den Task wie angegeben.

---
title: "Task uploadAndDeployFormularFiles"
description: "Sendet die Formulare im Projekt an eine Umgebung und deployed diese anschließend."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 180
menu:
  docs:
    parent: "tasks"
toc: true
---

## Beispiel

```shell
./gradlew uploadAndDeployFormularFiles
```

## Parameter

| Parameter | Pflicht? | Beschreibung |
| --- | --- | --- |
| mandant | Nein | Überschreibt den im config-Verzeichnis festgelegten Mandanten. |
| environment | Nein | Definiert die Umgebung, deren Konfiguration verwendet wird. Wird dieser Parameter nicht verwendet, so wird die Umgebung "default" verwendet.|
| debug | Nein | Wenn der Wert des Parameters "true" ist, werden weitere debug-Ausgaben durch das Plugin ausgegeben. |

## Beschreibung
   
Dieser Task dient dazu, die Formulare im Projekt an eine Umgebung zu senden 
und anschliessend zu deployen.
Ist ein Formular schon deployt, so wird es vor dem erneuten Deployment undeployt. 

Die weitere Funktion ist analog zum Task _uploadFormularFiles_.
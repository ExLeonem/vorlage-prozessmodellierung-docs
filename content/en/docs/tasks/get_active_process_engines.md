---
title: "Task getActiveProcessEngines"
description: ""
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 150
menu:
  docs:
    parent: "tasks"
toc: true
---

## Beispiel

```shell
./gradlew getActiveProcessEngines
```

## Parameter

| Parameter | Pflicht? | Beschreibung |
| --- | --- | --- |
| mandant | Nein | Überschreibt den im config-Verzeichnis festgelegten Mandanten. |
| environment | Nein | Definiert die Umgebung, deren Konfiguration verwendet wird. Wird dieser Parameter nicht verwendet, so wird die Umgebung "default" verwendet.|
| debug | Nein | Wenn der Wert des Parameters "true" ist, werden weitere debug-Ausgaben durch das Plugin ausgegeben. |

## Beschreibung

Dieser Task gibt die Liste der aktuell zur Verfügung stehenden Prozess-Engines aus. Die ID einer 
Prozess-Engine kann beim Deployment einer Prozessmodell-Version verwendet werden, um gezielt
auf die gewünschte Prozess-Engine zu deployen.
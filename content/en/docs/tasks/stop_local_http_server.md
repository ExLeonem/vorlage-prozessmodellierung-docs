---
title: "Task stopLocalHttpServer"
description: "Stoppt den lokalen Server zum bearbeiten von lokalen Dateien."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 210
menu:
  docs:
    parent: "tasks"
toc: true
---

## Beispiel

```shell
./gradlew stopLocalHttpServer
```

## Parameter

| Parameter | Pflicht? | Beschreibung |
| --- | --- | --- |
| mandant | Nein | Überschreibt den im config-Verzeichnis festgelegten Mandanten. |
| environment | Nein | Definiert die Umgebung, deren Konfiguration verwendet wird. Wird dieser Parameter nicht verwendet, so wird die Umgebung "default" verwendet.|
| debug | Nein | Wenn der Wert des Parameters "true" ist, werden weitere debug-Ausgaben durch das Plugin ausgegeben. |


## Beschreibung

Stoppt den lokalen Server zum Bearbeiten von lokalen Dateien.

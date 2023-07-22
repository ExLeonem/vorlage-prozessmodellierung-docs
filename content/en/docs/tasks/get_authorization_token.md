---
title: "getAuthorizationToken"
description: "Erzeugt einen neuen Bearer-Token für die Authentisierung in einer Serviceportal Umgebung."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 190
menu:
  docs:
    parent: "tasks"
toc: true
---

## Beispiel

```shell
./gradlew getAuthorizationToken -Penvironment=environmentName
```

## Parameter

| Parameter | Pflicht? | Beschreibung |
| --- | --- | --- |
| mandant | Nein | Überschreibt den im config-Verzeichnis festgelegten Mandanten. |
| environment | Nein | Definiert die Umgebung, deren Konfiguration verwendet wird. Wird dieser Parameter nicht verwendet, so wird die Umgebung "default" verwendet.|
| debug | Nein | Wenn der Wert des Parameters "true" ist, werden weitere debug-Ausgaben durch das Plugin ausgegeben. |

## Beschreibung
   
Mit diesem Task kann ein neues Bearer-Token für eine Umgebung 
in die Konfigurationsdatei `auth.json` geschrieben werden.
Existiert das entsprechende Token schon, so wird mit dem neu geholten Token ersetzt.

Benutzername und Passwort werden dabei aus einer der `gradle.properties` 
(in der systemeigenen Hierarchie) aus den Keys `serviceportal.username` bzw. `serviceportal.password` 
gelesen.

Mandant und Umgebung, unter der der Key abgelegt werden soll, werden wie im Kapitel 
"Ermittlung von Konfigurationswerten" beschrieben aus der Konfiguration gelesen.

## Aufrufparameter

Alle globalen Aufrufparameter beeinflussen den Task wie angegeben.
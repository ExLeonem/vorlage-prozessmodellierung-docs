---
title: "Task deployProcessModelVersion"
description: "Deployed ein im Admincenter vorhandes Prozessmodell."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 160
menu:
  docs:
    parent: "tasks"
toc: true
---


## Beispiel

```shell
./gradlew deployProcessModelVersion
```

## Parameter

| Parameter | Pflicht? | Beschreibung |
| --- | --- | --- |
| mandant | Nein | Überschreibt den im config-Verzeichnis festgelegten Mandanten. |
| environment | Nein | Definiert die Umgebung, deren Konfiguration verwendet wird. Wird dieser Parameter nicht verwendet, so wird die Umgebung "default" verwendet.|
| debug | Nein | Wenn der Wert des Parameters "true" ist, werden weitere debug-Ausgaben durch das Plugin ausgegeben. |


## Beschreibung

Dieser Task deployt ein im Admincenter vorhandenes Prozessmodell. Ist das Prozessmodell schon deployt, wird es undeployt und neu deployt. 

Mandant, Name, Version und Status des zu deployenden Prozesses und die ID der Prozess-Engine, auf die deployt werden soll, werden wie im Kapitel "Ermittlung von Konfigurationswerten" beschrieben aus 
der Konfiguration gelesen.

Die Aktion entspricht dabei dem Button "Prozessmodell deployen" im Admincenter. Ein Triggern der Aktion "Deploy (Prozess-Testumgebung)" über diesen Task ist nicht möglich.

Aus der Menge, der zur Verfügung stehenden Prozess-Engines, kann die Engine, auf die die Prozessversion deployt werden soll, ausgewählt werden. Ist keine Engine explizit angegeben, wird die Standard-Prozess-Engine verwendet.
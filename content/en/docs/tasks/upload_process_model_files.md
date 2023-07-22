---
title: "Task uploadProcessModelFiles"
description: "Lädt die mit dem Task `buildModel` gebauten Prozessmodell-Datein ins Admincenter hoch."
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
./gradlew uploadProcessModelFiles
```

## Parameter

| Parameter | Pflicht? | Beschreibung |
| --- | --- | --- |
| mandant | Nein | Überschreibt den im config-Verzeichnis festgelegten Mandanten. |
| environment | Nein | Definiert die Umgebung, deren Konfiguration verwendet wird. Wird dieser Parameter nicht verwendet, so wird die Umgebung "default" verwendet.|
| debug | Nein | Wenn der Wert des Parameters "true" ist, werden weitere debug-Ausgaben durch das Plugin ausgegeben. |

# Beschreibung

Dieser Task lädt die mit dem Task _buildModel_ gebauten Prozessmodell-Dateien ins Admincenter hoch.
Dabei wird das Prozessmodell nicht sofort deployt; das Deployment erfolgt über den separaten 
Task _deployProcessModelVersion_.

Mandant, Name, Version und aktiver Status für das Hochladen werden wie im Kapitel 
"Ermittlung von Konfigurationswerten" beschrieben aus der Konfiguration gelesen.

Beim erstmaligen Hochladen wird für den konfigurierten Mandanten im Admincenter 
ein Prozessmodell mit dem konfigurierten Namen angelegt. 
In diesem wird die konfigurierte Version angelegt. 
Anschließend werden alle Dateien im Ordner `build/models` für den konfigurierten Status importiert.

Falls für das angegebene Prozessmodell und die angegebene Version
* bereits Dateien mit dem angegebenen Status vorhanden sind, so gilt:
  * hat eine Datei mit einem Status den gleichen Namen wie eine Datei in `build/models`, wird diese
   ersetzt
  * alle anderen vorhandenen Dateien werden NICHT verändert oder gelöscht
* bereits Dateien in einem höheren als dem angegebenen Status vorhanden sind, ist ein Hochladen mit
  dem angegebenen Status nicht möglich.
 
## Aufrufparameter

Alle globalen Aufrufparameter beeinflussen den Task wie angegeben.
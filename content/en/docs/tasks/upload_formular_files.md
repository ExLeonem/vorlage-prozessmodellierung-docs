---
title: "Task uploadFormularFiles"
description: "Lädt die Formulare des Projekts in das Admincenter hoch."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 170
menu:
  docs:
    parent: "tasks"
toc: true
---

## Beispiel

```shell
./gradlew uploadFormularFiles
```

## Parameter

| Parameter | Pflicht? | Beschreibung |
| --- | --- | --- |
| mandant | Nein | Überschreibt den im config-Verzeichnis festgelegten Mandanten. |
| environment | Nein | Definiert die Umgebung, deren Konfiguration verwendet wird. Wird dieser Parameter nicht verwendet, so wird die Umgebung "default" verwendet.|
| debug | Nein | Wenn der Wert des Parameters "true" ist, werden weitere debug-Ausgaben durch das Plugin ausgegeben. |

## Beschreibung

Dieser Task lädt die Formulare des Projekts in das Admincenter hoch.

Die hochzuladenden Formulare werden im Ordner `forms` gesucht. Alle dort liegenden 
und der Namenskonvention entsprechenden Formulare werden über die Schnittstelle
an das Admincenter gesendet. Schon existierende Formulare werden überschrieben, 
nicht existierende Formulare und Versionen werden angelegt.
Falls der aktive Status für die Version des Formulars im Admincenter
höher ist als der angegebene Status in der Konfiguration, 
so ist ein Hochladen in den angegebene Status nicht möglich. 
Formulare, welche nicht dem Namensschema entsprechen, erzeugen einen Fehler.

## Benennung

Die Informationen zu den Formularen können entweder als Ordnerstruktur oder über den Dateinamen*
 dem Task übergeben werden:
* `forms/${FormularName}-${FormularVersion}-${Sprachkürzel}.json` 
* `forms/${FormularName}/${FormularVersion}/${Sprachkürzel}.json`

\* analog dem Namen beim Download eines Formulars aus dem Admincenter

Mandant und der Status für das Hochladen werden wie im Kapitel 
"Ermittlung von Konfigurationswerten" beschrieben aus der Konfiguration gelesen.

## Aufrufparameter

Alle globalen Aufrufparameter beeinflussen den Task wie angegeben.
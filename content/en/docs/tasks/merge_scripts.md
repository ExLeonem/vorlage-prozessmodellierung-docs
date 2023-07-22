---
title: "mergeScripts"
description: "Task zum zusammenfügen der Groovy-Skript-Tasks aus mehreren Dateien."
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
./gradlew mergeScripts
```

## Parameter

| Parameter | Pflicht? | Beschreibung |
| --- | --- | --- |
| mandant | Nein | Überschreibt den im config-Verzeichnis festgelegten Mandanten. |
| environment | Nein | Definiert die Umgebung, deren Konfiguration verwendet wird. Wird dieser Parameter nicht verwendet, so wird die Umgebung "default" verwendet.|
| debug | Nein | Wenn der Wert des Parameters "true" ist, werden weitere debug-Ausgaben durch das Plugin ausgegeben. |

## Beschreibung

Zweck dieses Tasks ist es, den Quellcode der Groovy-Skript-Tasks aus mehrere Dateien
zusammenzufügen.
Die Klassennamen in den import-Statements des Basis-Skripts definieren die einzubindenden Dateien, 
in denen typischerweise die importierten Klassen definiert sind. 
Diese eingebundenen Dateien enthalten ggf. weitere import-Statements, 
die wiederum aufgelöst werden usw. (d.h. die Auflösung erfolg rekursiv). 
Wird ein bereits behandelter Import erreicht, so wird dies erkannt 
und der Import wird nicht erneut eingefügt. 
Imports, die nicht mit dem root package `commons` beginnen, führen nicht zu einem Einbinden
einer Datei.

Die importierten Klassen werden an zwei Stellen gesucht:
* Im Verzeichnis <a target="_blank" href="/docs/plugin/structure/#ordner-scripts">scripts/commons</a>. Dort werden typischerweise projektinterne Klassen abgelegt. Diese Klassen müssen das package commons haben. 

```
// Beispielsweise importiert folgende Zeile
// dann die Datei scripts/commons/Example.groovy
import commons.Example;
```

* in beliebigen Unterordnern des Verzeichnisses `commons`. 
  In dem Verzeichnis `commons` werden typischerweise projektexterne Verzeichnisse (z.B. als git 
  Submodule) gemounted. Alle Unterordner werden als valide Quellverzeichnisse 
  für projektübergreifende Repositorys angesehen, die wieder dieselbe Ordnerstruktur 
  wie das eigentliche Projekt haben. Daher können beliebig viele Repositorys eingebunden werden.\
  Projektübergreifende Dateien müssen das Package `commons.[package].[subpackage].[Scriptdateiname]`
  haben, wobei subpackage optional ist oder selbst aus mehreren packagebestandteilen 
  zusammengesetzt sein kann. 
  D.h. die Zeile `import commons.[package].[subpackage].[Scriptdateiname]` führt dazu, dass
  die Datei `commons/[package]/scripts/commons/[package]/[subpackage]/[scriptdateiname].groovy`
  angezogen wird. 

Das zusammengefügte Skript wird im Verzeichnis 
`build/scripts/[ID des Prozesmodells]/[ID des Script-Tasks].groovy` abgelegt. 
Der Inhalt dieser Datei kann dann im Task _buildModel_ (s.u.) anschließend als Skript für den 
Skript-Task eingetragen werden.

Die Verwendung von `import`-Anweisungen erlaubt es der verwendeten IDE,
die entsprechenden Klassen für Codevervollständigung zu nutzen, zu kompilieren 
und schon während der Entwicklung auf Fehler hinzuweisen. Hierfür sollten in der IDE
die Verzeichnisse `scripts` und alle Unterverzeichnisse des Verzeichnisses `commons` 
als Groovy-Quellverzeichnisse konfiguriert werden.

## Parameter

Der globale Aufrufparameter **debug** beeinflusst den Task wie angegeben.
---
title: "Introduction"
description: ""
lead: ""
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "get_started"
weight: 100
toc: true
---


## Vorraussetzungen

- <a target="_blank" href="https://docs.gradle.org/7.6/release-notes.html">Gradle</a> - Version 7.6
- <a target="_blank" href="https://docs.aws.amazon.com/de_de/corretto/latest/corretto-11-ug/downloads-list.html">Java</a> - mindestens in version 11

## Workspace einrichten

1. Ein neues leeres GIT-Repository auf dem Server für das Projekt erstellen. 
2. Das neue Projekt clonen und einen initialen Commit machen.
3. Dieses Repository (also die Vorlage, in welcher Sie gerade lesen) als ein zweites remote-Repository 
(vorgeschlagener Name: `template`) zu Ihrem Projekt hinzufügen: 

```shell
git remote add template {link zu diesem repo}
```

Danach folgendes Kommando ausführen

```shell
git fetch --all
```

5. Im Anschluss alle Dateien aus der Vorlage in das Projekt mergen.

```shell
git merge template/master --allow-unrelated-histories
```

## Projektnamen setzen

Den Projektnamen "Prozessmodellierungsvorlage" in den folgenden Dateien, ersetzen durch den tatsächlichen Namen des Projektes:
   - `settings.gradle`
   - `config/project.json`

## Gradle-Plugin Version konfigurieren

Ggf. in der Datei `build.gradle` die gewünschte Version des Gradle-Plugins.
Verfügbare Versionen können in <a target="_blank" href="https://plugins.gradle.org/plugin/de.seitenbau.serviceportal.prozesspipeline">Gradle Plugin Repository</a> eingesehen werden.



## Updaten & Synchronisieren


1. Die Submodule (sofern vorhanden und benutzt) initialisieren:

```shell
git submodule update --init --recursive
```

2. Änderungen dann pushen mit 

```shell
git push
```

3. Anlegen der Formulare, Scripte, Prozessparameterdefinitionen und Scripte 

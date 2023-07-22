---
title: "Einführung"
description: "Grundlegende Informationen über das Gradle Plugin."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 10
menu:
  docs:
    parent: "plugin"
toc: true
---



## Versionen

<a target="_blank" href="https://plugins.gradle.org/plugin/de.seitenbau.serviceportal.prozesspipeline">
<img src="https://img.shields.io/badge/latest-v.2023.07.20-blue.svg?logo=LOGO"/>
</a>

<br/>
<br/>

Die aktuellen Versionen des prozesspipeline Plugins können über das <a target="_blank" href="https://plugins.gradle.org/plugin/de.seitenbau.serviceportal.prozesspipeline">Gradle Plugin Repository</a> abgerufen werden.


## Ziele des Gradle-Plugins zur Prozessmodellierung

Dieses Gradle-Plugin schafft die Möglichkeit, einzelne Prozess-Teile 
(insbesondere die im Prozess verwendeten Skripte) getrennt voneinander zu entwickeln
und so die Komplexität der Prozess-Entwicklung beherrschbar zu machen. 
Das Gradle-Plugin fügt die einzelnen Teile zu einem Modell zum Betrieb auf der Plattform zusammen
und spielt dieses Gesamtmodell zum Testen auf eine Zielplattform ein.

Dieser Ansatz ist für Entwickler gedacht, die sich eine lokale Arbeitsumgebung einrichten möchten
und nicht die Admincenter-Weboberflächen benutzen wollen. 
Die Weboberflächen sollen weiterhin als gleichwertige Alternative für weniger technisch orientierte
Entwickler erhalten bleiben und weiterentwickelt werden. 

Der Ansatz der lokalen Entwicklung ist aufgeteilt in:

* Entwicklung von Prozessmodellen ohne Skripte (z.B. mit Activiti Designer als Eclipse-Plugin)
* Entwicklung von Skripten als "Software" mit entsprechenden Möglichkeiten und Hilfen zur Entwicklung,
  z.B. Aufteilung in Klassen, Erstellen von Unittests usw.
  (via beliebiger IDE)
* Entwicklung von Formularen (wird noch entwickelt. Aktuell möglich ist z.B. textbasierte Entwicklung 
  oder Verwendung des Formulardesigners im Admincenter)
* Zusammenfügen, hochladen und deployen der Prozessmodelle und Formulare (dieses Gradle-Plugin)


## System-Anforderungen

* Das Plugin ist mit <a target="_blank" href="https://docs.gradle.org/7.6/release-notes.html">Gradle 7.6</a> getestet. Eventuell sind die Funktionen auch mit niedrigeren Gradle-Versionen verfügbar.
* Das verwendete Gradle muss minimal unter Java 11 laufen.


## Zugang

Das Plugin ist im Gradle Plugin-Repository unter der id <a target="_blank_" href="https://plugins.gradle.org/plugin/de.seitenbau.serviceportal.prozesspipeline ">https://plugins.gradle.org/plugin/de.seitenbau.serviceportal.prozesspipeline </a>zu finden.


## Grundidee

- Skripte werden nur als Rumpf-Skripte implementiert, die eigentliche Funktionalität
  wird in Groovy-Klassen implementiert, die wie andere Software auch mit Unittests geprüft werden 
  können. Die Klassen werden mit den Rumpf-Skripten über import-Anweisungen verbunden.
- Die entwickelten Skripte werden dann in Rumpf-bpmn-Dateien in den entsprechenden Skript-Task
  eingefügt. Die Verknüpfung zwischen Skript-Task un Skript erfolgt über die ID des Skript-Tasks
  bzw. dem Dateiname des Skripts.
- Die so entwickelten BPMN-Dateien sowie ebenso im Projekt abgelegte 
  Prozessparameterdefinitionen und Formulare können per Schnittstelle ins Admincenter 
  übertragen und deployt werden.
  
Das Gradle-Plugin unterstützt dieses Vorgehen und stellt Tasks bereit, die das Zusammenfügen der
Skripte, das Einfügen der Skripte in das Prozessmodell und das Hochladen ins Admincenter und
Deployen übernehmen.  



## Unterstützung von Gradle Multi-Project Builds

<a target="_blank" href="https://docs.gradle.org/current/userguide/multi_project_builds.html">Gradle Multi-Project Builds</a> werden vom Gradle-Plugin insofern unterstützt, als dass die Konfiguration des 
aktuell gebauten Projekts mit der Konfiguration des Root-Projekts ergänzt wird.
D.h. Vorrang hat die Konfiguration des aktuell gebauten Projekts, aber Einstellungen,
die im aktuell gebauten Projekt nicht vorhanden sind, werden aus der Konfiguration
des Root-Projektes geladen, wenn sie dort vorhanden sind.

Dies erlaubt es, die Konfiguration in den einzelnen Projekten minimal zu halten, indem 
wiederkehrende Konfigurationseinstellungen in ein Root-Projekt ausgelagert werden.

Authentifizierungsdaten, die vom Task _getAuthorizationToken_ geschrieben werden, werden
in die Datei config/auth.json des Root-Projektes geschrieben. Authentifizierungsdaten im Unterprojekt
werden dabei vollständig ignoriert.
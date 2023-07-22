---
title: "Erwartete Ordnerstruktur"
description: "Die Ordnerstruktur die vom Plugin erwartet wird. Um die Funktionsweise des Plugins zu gewährleisten muss diese eingehalten werden."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 15
menu:
  docs:
    parent: "plugin"
toc: true
---

<br/>

Über die erwartete Ordnerstruktur wird im Folgenden ein Überblick gegeben, 
danach werden die einzelnen Unterordner und Dateien im detailliert beschrieben.
Hierbei sind nicht für alle Gradle-Tasks alle beschriebenen Dateien und Ordner notwendig.


Es wird empfohlen, die Ordnerstruktur nicht selbst von null aus aufzubauen,
sondern die <a target="_blank" href="https://github.com/Seitenbau/Vorlage-Prozessmodellierung-Serviceportal">Vorlage Prozessmodellierung-Serviceportal</a> zu verwenden.

Die Ordnerstruktur wird vom Gradle-Plugin wie folgt erwartet:


```
├── config/
├── project.json
├── auth.json
├── default.json
├── scripts/
│   ├── ${prozessmodelId}
│   │     └── ${skriptName}.groovy
│   └── commons/
├── commons/
├── models/
│   └── ${dateiname}.bpmn
├── resources/
├── forms/
│   └── ${dateiname}.json
└── parameterdefinitions/
    ├── ${prozessmodelId}
    └── ${umgebungsname}.json
```


## Ordner: config/


Enthält die Konfigurationsdateien für das Gradle-Plugin. Die enthaltenen Dateien beeinflussen nur
das Verhalten des Gradle-Plugins.


### /project.json


Die Datei `project.json` enthält Informationen darüber, an welcher Stelle der Prozess
im Admincenter abgelegt wird. 

#### Attribute

Enthalten sind folgende Informationen:

| Attribut | Beschreibung |
| --- | --- |
| projectName | Der Name des Prozessmodells im Admincenter. |
| projectVersion | Die Version des Prozessmodells, an der gerade gearbeitet wird. |
| mandant | Die Id des Mandanten, unter dem das Prozessmodell und die Formulare im Admincenter abgelegt werden.|

#### Beispiel

Der Inhalt der Datei `project.json`  könnte folgendermaßen aussehen.

```json
{
  "projectName" : "TestInternal",
  "projectVersion": "v1.0",
  "mandant": "1"
}
```

### /auth.json

Die Informationen in dieser Datei authentifizieren den Benutzer gegen die entsprechende Umgebung.
Die Authentifizierungsinformationen sind sensitive persönliche Informationen
und entsprechen vom Stellenwert her persönlichen Passwörtern. 
Das heisst, jeder Entwickler sollte eigene Authentifizierungstokens benutzen, 
daher sollte diese Datei NICHT unter Versionskontrolle stehen und NICHT an andere Personen
weitergegeben werden. 

Die Datei hat folgende Struktur:

* eine Map der Umgebungen mit key Umgebungs-Id
  * darin je eine Map der Mandanten mit Key Mandanten-Id
    * darin folgendes Attribut:
      * **authorizationHeader**: Parameter zur Authentifizierung (`Bearer-Token`)

Damit die Token funktionieren, gelten folgende **Voraussetzungen**:

* Der entsprechende Nutzer muss auf der Umgebung angelegt sein
* dem Nutzer müssen die entsprechenden Rechte über Rollen/ Benutzergruppen gewährt werden.
* Das Token muss auf der entsprechenden Umgebung ausgestellt worden sein.
* Ein Zugriff mittels Webservice-Benutzern ist nicht möglich.
* Die Benutzertoken haben eine Gültigkeitsdauer von 24h, danach muss ein neues Token erzeugt werden.

Die Token können am bequemsten über den Task <a target="_blank" href="/docs/tasks/get_authorization_token/">getAuthorizationToken</a> geholt werden.

Manche Umgebungen schränken aus Sicherheitsgründen einzelne Funktionen ein.
So ist es beispielsweise möglich, auf die Produktivumgebungen Prozesse im Status `TEST` hochzuladen, aber nicht im Status `FINAL`. Ebenso ist es nicht möglich mittels des Plugins die Prozesse zu deployen. 

Diese Beschränkungen werden über den Betrieb in Absprache mit dem IM/SK für jede Umgebung festgelegt.


#### Beispiel

Beispiel für die Authentifizierung für den Mandant 1 in der Umgebung default:

```json
{
  "default": {
    "1": {
      "authorizationHeader": 
      [
        "Bearer XYZTokenContent"
      ]
    }
  }
}
```


### /default.json

Die Umgebungsdefinitionen dienen dazu, die Informationen für unterschiedliche Umgebungen abzulegen.
Wird beim Aufruf der Tasks keine Umgebung angegeben, so wird die Umgebung `default` gewählt.
Der Name der Umgebung ist in dem Dateinamen kodiert. So wird z.B. für die Umgebung `prozesstest`
die Umgebungsdefinitionsdatei `prozesstest.json` angezogen.

#### Attribute

Die Dateien enthalten folgende Informationen:

| Attribut | Beschreibung |
| --- | --- |
| url | Die URL des Servicegateways der Zielumgebung |
| status | Der Status in der das Prozessmodell und die Formulare auf der entsprechenden Umgebung abgelegt werden sollen. Gültige Werte sind: <br/> <ul><li>EDIT</li><li>TEST</li><li>FINAL</li></ul> Es kann jedoch sein, dass manche Werte auf manchen Umgebungen nicht zur Verfügung stehen. |
| mandant | Die Id des Mandanten für diese Umgebung. Wenn gesetzt, wird der Mandant aus der Datei project.json  überschrieben. |
| processModelNameExtension | Ein optionales Suffix, der beim Bauen der Prozessmodelle an den Prozessnamen, der in der bpmn-Datei definiert ist, angehängt wird (getrennt durch ein Leerzeichen). |
| processEngine | Die ID der Prozess-Engine, auf welche die Prozessmodell-Version deployt werden soll. Ist der Parameter nicht gesetzt, wird die Standard-Prozess-Engine verwendet. |


#### Beispiel

```json
{
  "url": "https://sgwtest.service-bw.de",
  "status": "EDIT",
  "mandant": "42",
  "processModelNameExtension": "DEV",
  "processEngine": "secondEngine"
}
```


## Ordner: scripts/


Enthält die Groovy-Skripte, die in die Prozessmodelle eingefügt werden,
und darin verwendete Klassen. 

Die Skripte für ein Prozessmodell liegen in einem Unterverzeichnis, dessen Name gleich der Id
des Prozessmodells (Attribut `id` des Elements `process` der BPMN-Datei) und haben den Namen

`${Id des Script-Tasks}.groovy.`

Sollen skript-tasksübergreifende Groovy-Klassen verwendet werden, können im Unterverzeichnis "commons" 
abgelegt werden.

Sie müssen im Package "commons" deklariert werden und können über Importanweisungen eingebungen 
werden. So wird z.B. die Klasse "commons.Example" in der Datei scripts/commons/Example.groovy 
gesucht.

Für projektübergreifende Klassen ist das Verzeichnis commons direkt im Projekt gedacht, s.u.

### Ordner: commons/

Der Ordner `commons` enthält beliebige Unterordner mit weiteren Groovy-Klassen, die in den Skripten verwendet werden können.
Jeder Unterordner muss dabei den Namen des zweiten Teils des packages haben und hat dieselbe Projektstruktur wie die hier beschriebene Projektstruktur.
D.h. die Klasse "commons.externalpackage.Example" würde in der Datei
commons/externalpackage/scripts/commons/externalpackage/Example.groovy gefunden werden.

Dieses Verzeichnis ist dafür gedacht, um externe Verzeichnisse, die z.B.
eine Bibliothek von prozessübergreifenden Klassen bereitstellen, 
in das Projekt verlinken zu können (beispielsweise mit git submodules).

### Ordner: models/

Der Ordner `models`enthält die Prozessmodell-Dateien des Prozesses mit leeren Skript-Tasks. Die Prozessmodell-Dateien enden mit .bpmn oder mit .bpmn20.xml.

### Ordner: forms/

Der Ordner `forms` enthält die Formulare, die zum Prozess gehören. Es gibt zwei Namensschemata für die Formulare:
* `forms/${FormularName}-${FormularVersion}-${Sprachkürzel}.json` 
* `forms/${FormularName}/${FormularVersion}/${Sprachkürzel}.json`

D.h. entweder können FormularName und Formularversion im Dateinamen konfiguriert werden oder in den Namen der Verzeichnisse.


## Ordner: parameterdefinitions/

Enthält die Definition der Prozessparameter für den Prozess. 
Die Standard-Konfiguration der Prozessparameter sollte in der Datei default.json abgelegt werden.
Werden für einzelne Umgebungen andere Prozessparameterdefinitionen benötigt, so können diese
in Dateien ${umgebungsname}.json abgelegt werden, die dann für die benannten Umgebungen 
automatisch statt default.json angezogen werden.

**Diese Dateien haben dasselbe Format wie die json-Dateien, 
die auch im Admincenter als Prozessparameterdefinitionen verwendet werden.**


### Attribute

In einer Parameterdefinition werden die folgenden Informationen gespeichert

| Attribut | Beschreibung |
| --- | --- |
| name | Der programmatische Name des Prozessparameters, muss unique für ein Prozessmodell sein |
| description | Die Beschreibung des Parameters für die Prozessverwalter, die den Parameter setzen wollen. |
| type | Der Typ des Prozessparameters. Erlaubt sind folgende Werte: <table><tr><th>Type</th><th>Beschreibumg</th></tr><tr><td>STRING</td><td>Der im ProcessParameter gespeicherte String wird as is verwendet</td></tr><tr><td>JSON_STRING_MAP</td><td>Der im ProcessParameter gespeicherte String wird im Prozess als JSON-Map&lt;String, String&gt geparst</td></tr><tr><td>JSON_OBJECT</td><td>Der im ProcessParameter gespeicherte String wird im Prozess als JSON-Objekt geparst</td></tr><tr><td>BINARY</td><td>Der im ProcessParameter gespeicherte String wird als Base64 kodierter Byte-Array interpretiert und als Byte-Array zurückgegeben.</td></tr></table> |
| defaultValue | Der Defaultwert des Parameters. Wird verwendet, falls der Prozessverwalter bei der Aktivierung des Prozesses nichts anderes angibt. Wenn defaultValue nicht gesetzt ist, gibt es keinen Defaultwert. |
| required | true, falls der Aktivierung des Prozesses immer ein Wert angegeben werden muss, oder false, wenn nicht. Default ist false. |
| hidden | true, wenn der Prozessparameter bei der Aktivierung nicht sichtbar sein soll, oder false, wenn der Prozessparameter bei der Aktivierung sichtbar sein soll. Default ist false. |


### Beispiel

Beispielhafter Inhalt einer Prozessparameterdefinitions-Datei:
```json
[
  {
    "name": "nameDesProzessparameters",
    "description": "Beschreibung für die Prozessverwalter, die den Parameter setzen wollen.",
    "type": "STRING",
    "defaultValue": "myDefaultValue",
    "required": false,
    "hidden": false
  },
  {
    "name": "otherProzessparameter",
    "description": "Andere Beschreibung",
    "type": "JSON_OBJECT"
  }
]
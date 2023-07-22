---
title: "Scripting-API"
description: "Dient der Typisierten Interaktion mit Objekten der Serviceplattform."
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 20
menu:
    docs:
        parent: guides
toc: true
---



## Verfügbar machen im Projekt

Um die Scripting-API in der aktuellsten Version für dieses Projekt zur verfügung zu stellen, reicht es in der `build.gradle` den entsprechenden Kommentar im Abschnitt `dependencies` wieder rein zu nehmen.

```
// Include to use latest scripting api version
// implementation 'de.seitenbau.serviceportal:prozess-scripting-api:1.+'
```

Im Anschluss muss nur diese Abhängigkeit durch Gradle bezogen werden. Hierfür kann folgender Befehl verwendet werden.

```shell
gradle --refresh-dependencies build
```

Alternativ kann auch der entsprechende Button in Intellij oder der IDE ihrer Wahl geklickt werden um ein Update der Abhängigkeiten anzustoßen.


## Version setzen

Falls nötig kann die Scripting-API auf eine bestimmte Version festgesetzt werden.

### Beispiel

Um die aktuellste Version auf die Version `1.162.8` zu ändern muss die Abhängigkeit wie folgt abgeändert werden

```
// alt
implementation 'de.seitenbau.serviceportal:prozess-scripting-api:1.+' 

// neu
implementation 'de.seitenbau.serviceportal:prozess-scripting-api:1.162.8' 
```

Die verfügbaren Versionen der Scripting-API können über <a target="_blank" href="https://central.sonatype.com/artifact/de.seitenbau.serviceportal/prozess-scripting-api/1.162.8/versions">Maven Central</a> abgerufen werden.


## Verwendung


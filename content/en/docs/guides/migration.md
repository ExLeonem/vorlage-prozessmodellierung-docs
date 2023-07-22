---
title: "Migration"
description: ""
lead: ""
date: 2022-01-25T14:40:56+01:00
lastmod: 2022-01-25T14:40:56+01:00
draft: false
images: []
weight: 40
menu:
    docs:
        parent: guides
toc: true
---

## Umstellung Projektstufen zu Statuswerten

Mit der aktuellsten version des Gradle Plugins wurden die Projektstufen entfernt und durch
Statuswerte ersetzt. 
Die Schnittstelle selbst funktioniert übergangsweise sowohl mit der Stufe, als auch dem neuen Status.
Es darf jedoch nur einer der beiden Werte an die Schnittstelle übertragen werden.

**Deprecated:** Ab einem einem Zeitpunkt X, wird die Verwendung der Projektstufen vollständig ausgebaut 
und komplett auf die neuen Statuswerte umgestellt. Daher ist nicht gewährleistet das die Endpunkte
zukunftig weiterhin mit den Projektstufen funktionieren.

Um zur aktuellsten Plugin Version zu migrieren, müssen folgende aktionen durchgeführt werden.

1. Konfigurationsdateien anpassen. Statt dem Attribut `projectStage` sollte das Attribut `status` verwendet werden 
2. Die neuen Statuswerte statt den ehemaligen Stufen verwenden. Siehe hierfür die folgenden Tabellen

Die Werte des veralteten `projectStage` Attributs können anhand der nachfolgenden Tabelle
in die neuen Statuswerte übertragen werden.

### Beispiel

#### Alte config.json

```json
{
   "url": "http://example.com:81/sgw",
   "projectStage": "TECHNICAL_IMPLEMENTATION"
}
```

#### Neue config.json

```json
{
   "url": "http://example.com:81/sgw",
   "status": "EDIT"
}
```

### Mapping Projektstufen auf Statuswerte

Die folgenden Tabellen stellen dar welcher Statuswert die selbe Funktionalität bietet wie in der
vorherigen Plugin version eine bestimmte Projektstufe.

#### Für Formulare

| Projektstufe      | Status |
|-------------------|--------|
| MODELLING         | EDIT   |
| QUALITY_ASSURANCE | TEST   |
| CERTIFIED         | FINAL  |

#### Für Prozesse

| Projektstufe             | Status |
|--------------------------|--------|
| FUNCTIONAL_ANALYSIS      | EDIT   |
| TECHNICAL_IMPLEMENTATION | EDIT   |
| QUALITY_ASSURANCE        | TEST   |
| CERTIFIED                | FINAL  |



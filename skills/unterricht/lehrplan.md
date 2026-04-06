# Lehrplan-Quellen — Übersicht und Aktualisierung

Zentrale Referenz aller lokalen Lehrplan-Dateien mit Quell-URLs und Download-Datum.
Zum Aktualisieren: URL aufrufen, Änderungen prüfen, `rahmenlehrplan.md` neu erstellen.

## Lokale Dateien (alle 16 Bundesländer)

| Bundesland | Datei | Quelle | Heruntergeladen |
|---|---|---|---|
| Baden-Württemberg | `lehrplan/baden-wuerttemberg/rahmenlehrplan.md` | [bildungsplaene-bw.de](https://www.bildungsplaene-bw.de/,Lde/BP2016BW_ALLG_SEK1) | 2026-04-03 |
| Bayern | `lehrplan/bayern/rahmenlehrplan.md` | [lehrplanplus.bayern.de](https://www.lehrplanplus.bayern.de) | 2026-04-03 |
| Berlin | `lehrplan/berlin/rahmenlehrplan.md` | [bildungsserver.berlin-brandenburg.de](https://bildungsserver.berlin-brandenburg.de/unterricht/rahmenlehrplaene/jahrgangsstufen-1-10) | 2026-04-03 |
| Brandenburg | `lehrplan/brandenburg/rahmenlehrplan.md` | [bildungsserver.berlin-brandenburg.de](https://bildungsserver.berlin-brandenburg.de/unterricht/rahmenlehrplaene/jahrgangsstufen-1-10) | 2026-04-03 |
| Bremen | `lehrplan/bremen/rahmenlehrplan.md` | [lis.bremen.de](https://www.lis.bremen.de/schulqualitaet/bildungsplaene/sekundarbereich-i-21953) | 2026-04-03 |
| Hamburg | `lehrplan/hamburg/rahmenlehrplan.md` | [bildungsplaene.hamburg.de](https://bildungsplaene.hamburg.de) | 2026-04-03 |
| Hessen | `lehrplan/hessen/rahmenlehrplan.md` | [kultus.hessen.de](https://kultus.hessen.de/unterricht/kerncurricula-und-lehrplaene/kerncurricula/sekundarstufe-i-kerncurricula) | 2026-04-03 |
| Mecklenburg-Vorpommern | `lehrplan/mecklenburg-vorpommern/rahmenlehrplan.md` | [bildung-mv.de](https://www.bildung-mv.de/lehrer/rahmenlehrplaene/) | 2026-04-03 |
| Niedersachsen | `lehrplan/niedersachsen/rahmenlehrplan.md` | [cuvo.nibis.de](https://cuvo.nibis.de/cuvo.php?p=search&k0_0=Schulbereich&v0_0=Sek+I) | 2026-04-03 |
| NRW | `lehrplan/nrw/rahmenlehrplan.md` | [lehrplannavigator.nrw.de](https://lehrplannavigator.nrw.de/sekundarstufe-i/kernlehrplaene-fuer-die-gesamtschule) | 2026-04-03 |
| Rheinland-Pfalz | `lehrplan/rheinland-pfalz/rahmenlehrplan.md` | [lehrplaene.bildung-rp.de](https://lehrplaene.bildung-rp.de) | 2026-04-03 |
| Saarland | `lehrplan/saarland/rahmenlehrplan.md` | [saarland.de](https://www.saarland.de/mbk/DE/portale/bildungsserver/lehrplaene-handreichungen/lehrplaene) | 2026-04-03 |
| Sachsen | `lehrplan/sachsen/rahmenlehrplan.md` | [bildung.sachsen.de](https://www.bildung.sachsen.de/apps/lehrplandb/) | 2026-04-03 |
| Sachsen-Anhalt | `lehrplan/sachsen-anhalt/rahmenlehrplan.md` | [bildung-lsa.de](https://www.bildung-lsa.de/lehrplaene___rahmenrichtlinien.html) | 2026-04-03 |
| Schleswig-Holstein | `lehrplan/schleswig-holstein/rahmenlehrplan.md` | [fachportal.lernnetz.de](https://fachportal.lernnetz.de/sh/fachanforderungen.html) | 2026-04-03 |
| Thüringen | `lehrplan/thueringen/rahmenlehrplan.md` | [schulportal-thueringen.de](https://www.schulportal-thueringen.de/lehrplaene/regelschule) | 2026-04-03 |

## Fächer pro Datei

Jede `rahmenlehrplan.md` enthält Kompetenzbereiche und Themenfelder/Lernbereiche für:
- **Mathematik**
- **Deutsch**
- **Englisch**
- **Physik**
- **Chemie**

## Aktualisierung

1. Portal-URL aufrufen und auf Änderungen/neue Fassungen prüfen
2. Bei Änderung: neue `rahmenlehrplan.md` erstellen (per WebFetch oder Perplexity)
3. `downloaded`-Datum im YAML-Header aktualisieren
4. Diese Datei (`lehrplan.md`) aktualisieren

**Hinweis:** Lehrpläne ändern sich selten (alle 5–10 Jahre). Ein jährlicher Check reicht.

## Schulinterner Lehrplan

Zusätzlich zum offiziellen Rahmenlehrplan hat jede Schule einen **schulinternen Lehrplan**
(Stoffverteilungsplan), der die konkrete Umsetzung festlegt:

- Reihenfolge der Themen
- Stundenumfang pro Thema
- Schwerpunkte und Vertiefungen
- Fächerverbindende Bezüge
- Eingesetzte Lehrbücher und Materialien

### Speicherort

`lehrplan/schulintern/<fach>_klasse<N>.md`

Beispiele:

- `lehrplan/schulintern/mathematik_klasse9.md`
- `lehrplan/schulintern/deutsch_klasse8.md`

### Erfassung

Der Unterricht-Skill fragt beim ersten Aufruf für ein Fach/Klassenstufe, ob ein
schulinterner Lehrplan vorhanden ist. Der Lehrer kann ihn als PDF, Bild oder Text
liefern. Der Skill konvertiert ihn in Markdown und speichert ihn für zukünftige
Stunden.

### Hierarchie

1. **Schulinterner Lehrplan** (höchste Priorität -- enthält die tatsächliche Planung)
2. **Offizieller Rahmenlehrplan** (Fallback -- enthält die Kompetenzanforderungen)
3. **Didaktik-Referenz** (immer -- enthält Methodik und Notation)

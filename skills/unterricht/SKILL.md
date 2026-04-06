---
name: unterricht
description: >
  This skill should be used when the user wants to "Unterricht vorbereiten",
  "Stunde planen", "Tafelbild erstellen", "Hefteintrag erstellen",
  "Stunde vorbereiten", or "Arbeitsblatt erstellen".
  Prepares lessons for Sekundarstufe I schools. Analyzes textbook material
  from books/ and suggests variants for Merke-Texte, examples, explanations,
  and exercises. Generates Hefteinträge as Word files (.docx).
---

# Unterrichtsvorbereitung — alle Fächer

Analysiert Buchmaterial und Zusatzmaterial zum Thema, schlägt Varianten und Optionen für die Stundengestaltung vor und generiert nach Auswahl einen Hefteintrag als Word-Datei (.docx).

## Verfügbare Scripts

| Script | Zweck |
|--------|-------|
| `scripts/omml_utils.py` | OMML-Formelfunktionen: `F(z,n)` Bruch, `T(text)` Operator, `M(g,z,n)` gemischte Zahl |
| `scripts/template.py` | Dokument-Grundgerüst + Inhalts-Hilfsfunktionen (siehe API unten) |

### template.py API

| Funktion | Zweck |
|----------|-------|
| `create_lesson_document(thema, kapitel, seiten)` | Grundgerüst: Titel, Kapitelangabe, Seitenreferenz |
| `add_merke(doc, text)` | Hervorgehobener Merke-Kasten (blauer Rahmen, hellblauer Hintergrund) |
| `add_methode(doc, title, steps)` | Nummerierte Methodenschritte (z.B. Lösungsverfahren) |
| `add_beispiel(doc, title)` | Beispiel-Überschrift mit Trennlinie |
| `add_probe(doc)` | "Probe:"-Überschrift |
| `add_aufgaben(doc, unterricht, hausaufgabe)` | Aufgaben mit Text: `[{"ref": "B.S. 92/1", "text": "Berechne..."}]` oder nur Referenz: `["B.S. 92/1"]` |
| `add_zusatzmaterial(doc, materials)` | Zusatzmaterial mit Inhalt: `[("Titel", "datei.doc", books_dir)]` |
| `add_coordinate_system(doc, x_range, y_range)` | Leeres Koordinatensystem (matplotlib-Bild) |
| `add_value_table(doc, headers, data)` | Wertetabelle |
| `add_loesungen(doc, loesungen)` | Lösungsblatt (Seitenumbruch): `[{"ref": "B.S. 92/1a", "loesung": "x = 3"}]` |
| `add_stundenkontext(doc, vorher, nachher)` | Kontext-Leiste: vorheriges/nächstes Thema |
| `save_document(doc, basename)` | Speichert als .docx |

## Buchmaterial

Alle extrahierten Bücher liegen unter `books/` im Projektverzeichnis. Jedes Buch hat einen eigenen Unterordner mit:
- `<Buchname>.txt` — Volltext des Buchs (Seiten markiert mit `--- Seite N ---`)
- `Zusatzmaterial.md` — Index aller Zusatzmaterialien (DOC + PDF) mit Titel + Dateiname
- `Zusatzmaterial/*.md` — Markdown-Konvertierungen der Arbeitsblätter, Lösungen, Zusammenfassungen

### Buch finden

1. Fach aus `$ARGUMENTS` oder Kontext bestimmen
2. In `books/` nach passendem Buch suchen (z.B. `books/Mathematik heute 9/`)
3. Falls kein Buch vorhanden: Lehrer fragen ob per `bibox` (Westermann), `klett` oder `cornelsen` extrahiert werden soll, oder ob PDF/Material manuell vorliegt
4. Falls gar kein Material: Stunde auch ohne Buchmaterial planen (mit didaktik-Referenz)

## Didaktik-Referenz

Für jedes Fach existiert eine allgemeine fachdidaktische Referenz unter `didaktik/<fach>.md` mit:
- Notation und Konventionen
- Typische Stundenstruktur
- Differenzierung A-Kurs / B-Kurs
- Visuelle Methoden und Materialien

**Immer die passende Didaktik-Referenz lesen** bevor Vorschläge gemacht werden.

Verfügbare Fächer: `mathematik.md`, `deutsch.md`, `englisch.md`, `physik.md`, `chemie.md`

### Lehrplan-Bezüge (bundeslandspezifisch)

Bundeslandspezifische Lehrplan-Inhalte (Kompetenzbereiche, Themenfelder, Niveaustufen) liegen unter `didaktik/lehrplan/<bundesland>/rahmenlehrplan.md`. Falls für das Bundesland des Lehrers vorhanden, zusätzlich laden.

Alle Quellen und Download-Daten: siehe `lehrplan.md`

Verfügbar (alle 16 Bundesländer): `baden-wuerttemberg`, `bayern`, `berlin`, `brandenburg`, `bremen`, `hamburg`, `hessen`, `mecklenburg-vorpommern`, `niedersachsen`, `nrw`, `rheinland-pfalz`, `saarland`, `sachsen`, `sachsen-anhalt`, `schleswig-holstein`, `thueringen`

### Förderschwerpunkt (optional)

Falls der Schultyp einen Förderschwerpunkt hat, existieren zusätzliche Ergänzungsdateien unter `didaktik/foerderschwerpunkt/`:

| Förderschwerpunkt | Dateipräfix | Schwerpunkte |
|---|---|---|
| Hören | `hoeren_` | Visuelle Methoden, Gebärdenunterstützung, Akustik-Anpassungen |
| Emotionale-soziale Entwicklung (ESE) | `ese_` | Strukturierung, Deeskalation, Token-Systeme, Beziehungsarbeit |
| Lernen | `lernen_` | Vereinfachung, Anschaulichkeit, reduzierte Lernziele, Lebensweltbezug |

Dateien pro Förderschwerpunkt: `<präfix>mathematik.md`, `<präfix>deutsch.md`, `<präfix>englisch.md`, `<präfix>physik.md`, `<präfix>chemie.md`

**Nur laden wenn der Schultyp einen Förderschwerpunkt hat.**

## Wichtigste Regel: FRAGEN STELLEN, NICHT FERTIG LIEFERN

Dieser Skill ist ein **Beratungsgespräch**, kein Automat. NIEMALS direkt ein fertiges Dokument erzeugen. Stattdessen:

1. **Material analysieren** — still im Hintergrund lesen und verstehen
2. **Aktiv Fragen stellen und Vorschläge machen** — dem Lehrer Optionen präsentieren, Ideen vorschlagen, Alternativen aufzeigen
3. **Erst nach Auswahl generieren** — das .docx wird erst erstellt wenn der Lehrer sich entschieden hat

Nutze `AskUserQuestion` intensiv. Stelle gezielte Fragen wie:
- "Im Buch gibt es auf S. 91 dieses Beispiel und auf S. 92 jenes — welches eignet sich besser als Einstieg?"
- "Der INFORMATION-Kasten im Buch sagt: '...'. Soll ich das 1:1 übernehmen oder kürzer/einfacher formulieren?"
- "Für dieses Thema gibt es ein Arbeitsblatt das die Verfahren vergleicht — soll das als Kopiervorlage mit rein?"
- "Aufgaben: S. 92 hat Aufgabe 1 (leicht) und Aufgabe 2 (schwerer). Was davon im Unterricht, was als HA?"

Stelle **konkrete** Fragen mit den **tatsächlichen Inhalten** aus dem Buch — nicht abstrakt.

## Workflow

### 0. Lehrer-Profil laden

1. `config/lehrer.md` lesen (falls vorhanden)
2. **Ersteinrichtung**: Falls Datei leer/nicht vorhanden, Grunddaten erfragen
   (Name, Schule, Bundesland, Fächer, Klassenstufen) und Datei anlegen
3. Gespeicherte Präferenzen für Vorschläge nutzen (z.B. bevorzugte Beispielquellen,
   Merke-Text-Länge, Hausaufgaben-Stil)
4. **Nach jeder Entscheidung**: Wenn der Lehrer eine Präferenz zeigt die noch nicht
   gespeichert ist, in `config/lehrer.md` notieren und kurz mitteilen

### 1. Fach und Thema bestimmen

1. Fach aus `$ARGUMENTS` oder Kontext ableiten
2. Passende `didaktik/<fach>.md` lesen
3. Passendes Buch in `books/` finden

### 1b. Schulinternen Lehrplan laden oder erfragen

Jede Schule hat einen **schulinternen Lehrplan** (Stoffverteilungsplan), der festlegt
welche Themen in welcher Reihenfolge, mit welchem Stundenumfang und welchen Schwerpunkten
unterrichtet werden. Dieser weicht oft vom offiziellen Rahmenlehrplan ab.

1. Prüfe ob bereits ein schulinterner Lehrplan gespeichert ist:
   `didaktik/lehrplan/schulintern/<fach>_klasse<N>.md`
   (z.B. `schulintern/mathematik_klasse9.md`)
2. **Falls nicht vorhanden**: Frage den Lehrer:
   - „Hast du einen schulinternen Lehrplan / Stoffverteilungsplan für <Fach> Klasse <N>?
     Du kannst ihn als PDF/Bild/Text einfügen oder beschreiben.
     Dann speichere ich ihn für die Zukunft."
3. **Falls der Lehrer einen liefert**: Speichere ihn als
   `didaktik/lehrplan/schulintern/<fach>_klasse<N>.md` mit YAML-Header:
   ```yaml
   ---
   title: "Schulinterner Lehrplan <Fach> Klasse <N>"
   schule: "<Schulname>"
   schuljahr: "<z.B. 2025/2026>"
   erstellt: "<Datum>"
   ---
   ```
4. **Falls der Lehrer keinen hat**: Verwende den offiziellen Rahmenlehrplan
   aus `didaktik/lehrplan/<bundesland>/rahmenlehrplan.md` als Fallback.
5. **Schulinternen Lehrplan nutzen** für: Themenreihenfolge, Stundenumfang,
   Schwerpunkte, Querverweise zu vorherigen/nachfolgenden Themen.

### 2. Material analysieren

1. Im Buchtext per Grep das Thema finden → relevante `--- Seite N ---`-Abschnitte lesen
2. Falls Stoffverteiler vorhanden: Rahmenlehrplan-Kompetenzen und Niveaustufe identifizieren
3. In `Zusatzmaterial.md` passende Einträge finden (Arbeitsblätter, Lösungen)
4. Bei Bedarf relevante `.md`-Dateien aus `Zusatzmaterial/` lesen
5. **Lösungen suchen**: Im Buchtext oder in `Zusatzmaterial/` nach Lösungen zu den relevanten Aufgaben suchen
6. **Stundenkontext bestimmen**: Aus schulinternem Lehrplan oder Buchkapitel-Reihenfolge ermitteln was die vorherige und nächste Stunde/Thema ist
7. **Buchseiten-Zusammenfassung**: Die relevanten Seiten kurz zusammenfassen und dem Lehrer präsentieren — der Lehrer soll nicht selbst im Buch blättern müssen

### 3. Vorschläge präsentieren und FRAGEN STELLEN

Basierend auf dem gelesenen Material dem Lehrer **konkrete Optionen und Varianten** vorstellen. Dabei immer mit den echten Inhalten aus dem Buch arbeiten (zitieren, Seitenangaben, Aufgabennummern).

**a) Stundentyp**
- Einführungsstunde (neues Konzept) vs. Verfahrensstunde (neues Verfahren) vs. Übungsstunde

**b) Merke-Text — Varianten**
- Text direkt aus dem Buch (INFORMATION-Kasten) zitieren
- Vereinfachte/schülergerechte Umformulierung vorschlagen
- Kürzere vs. ausführlichere Fassung

**c) Beispiel — Optionen**
- Welche Beispiele stehen im Buch? (mit Seitenangabe)
- Alternative: eigenes Beispiel mit "schöneren" Zahlen vorschlagen

**d) Erklärungsansatz**
- Schülergerechte Erklärung unter Berücksichtigung der Didaktik-Referenz
- Schultyp-spezifische Methoden aus `didaktik/<fach>.md` einbeziehen
- Vorwissen das vorausgesetzt wird

**e) Aufgabenauswahl**
- Aufgaben aus dem Buch mit Schwierigkeitsgrad
- Vorschlag für Unterricht vs. Hausaufgabe
- Differenzierungsmöglichkeit A-Kurs / B-Kurs

**f) Zusatzmaterial**
- Welche Arbeitsblätter/Kopiervorlagen gibt es?
- Empfehlung: Welches Material lohnt sich?

### 4. Auswahl durch den Lehrer

Mit `AskUserQuestion` den Lehrer **aktiv befragen**. Schrittweise:

1. Zuerst: Stundentyp und grobe Richtung klären
2. Dann: Merke-Text und Beispiel auswählen
3. Zuletzt: Aufgaben und Zusatzmaterial festlegen

**WICHTIG — Immer eine "Alles ins Dokument"-Option anbieten:**
Bei jeder Frage eine Option anbieten, alle Varianten in das .docx zu schreiben. Der Lehrer kann dann in Ruhe auf Papier entscheiden.

### 5. Hefteintrag generieren

Erst JETZT — nach der Auswahl — ein Python-Script erzeugen und ausführen.

```python
import sys, os
SKILL_DIR = "${CLAUDE_SKILL_DIR}"
sys.path.insert(0, os.path.join(SKILL_DIR, "scripts"))
from omml_utils import F, T, M, add_math, add_math_line, MINUS, MAL
from template import (
    create_lesson_document, add_merke, add_methode,
    add_beispiel, add_probe, add_aufgaben, add_zusatzmaterial,
    add_coordinate_system, add_value_table, save_document
)
# ... Dokument aufbauen basierend auf der Auswahl des Lehrers ...
```

```bash
uv run script.py
open <Dateiname>.docx
```

## Struktur des Hefteintrags

Jeder Hefteintrag folgt diesem Muster:

1. **Überschrift** — Thema mit Nummerierung falls Teil einer Reihe
2. **Merke** — Kernkonzept/Definition als hervorgehobener Kasten
3. **Methode** (bei Verfahren) — Nummerierte Schritte der Vorgehensweise
4. **Beispiel** — Vollständig durchgerechnetes/ausgearbeitetes Beispiel
5. **Probe** (bei Mathematik/Physik/Chemie) — Verifikation der Lösung
6. **Aufgaben** — Unterteilt in "Im Unterricht" und "Hausaufgabe", mit Aufgabentext aus dem Buch
7. **Zusatzmaterial** — Relevante Kopiervorlagen und Lösungen, mit eingebettetem Inhalt
8. **Stundenkontext** — Leiste am Ende: vorheriges Thema ← | → nächstes Thema
9. **Lösungen** (separate Seite) — Erwartungshorizont nur für die Lehrkraft

## Stundentypen

### A) Einführungsstunde (neuer Begriff/Konzept)
- **Merke-Kasten** mit Definition
- **1 Beispiel** vollständig ausgearbeitet
- **Probe** (bei MINT-Fächern)
- Aufgaben: wenige, einfache

### B) Verfahrensstunde (neues Lösungsverfahren)
- **Methodenschritte** als nummerierte Liste
- **1 Beispiel** Schritt für Schritt nach der Methode gelöst
- **Probe** — bei algebraischen Verfahren IMMER
- Aufgaben: Buch + AH gemischt

### C) Übungsstunde
- **Kein neuer Hefteintrag** — nur Aufgabenverweise
- Mehrere Aufgaben aus Buch + Arbeitsheft

### D) Wiederholung/Zusammenfassung
- Rückblick auf die Methoden/Konzepte
- "Was du gelernt hast"-Material nutzen falls vorhanden

## Notationskonventionen

- **Aufgabenformat**: "B.S. 89/2a-c" = Buch Seite 89, Aufgabe 2, Teile a bis c
- **AH-Format**: "AH S. 20/1,2,3" = Arbeitsheft Seite 20, Aufgaben 1, 2, 3
- **Thema-Nummerierung**: (1), (2), (3) für Konzepte; I, II, III für Verfahren
- Fachspezifische Notation: siehe `didaktik/<fach>.md`

## Regeln

- **Umlaute und ß IMMER verwenden** — ä, ö, ü, Ä, Ö, Ü, ß. Nur Dateinamen ohne Umlaute.
- python-docx + lxml + matplotlib werden von `uv` automatisch installiert
- Brüche/Formeln IMMER über `omml_utils` — NIEMALS als Text "3/4"
- Merke-Texte aus dem Buch ableiten (INFORMATION-Kästen oder vergleichbare Hervorhebungen)
- Beispiele bevorzugt aus dem Buch übernehmen, vollständig ausarbeiten
- Schultyp-spezifische Methoden aus `didaktik/<fach>.md` berücksichtigen
- Aufgabenverweise: Seiten + Nummern exakt angeben
- Zusatzmaterial: Nur wirklich relevante Dateien auflisten

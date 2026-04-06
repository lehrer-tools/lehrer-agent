---
name: leistungskontrolle
description: >
  This skill should be used when the user wants to "Klassenarbeit erstellen",
  "Test erstellen", "Arbeit erstellen", "Leistungskontrolle", "Mathe-Test",
  "Englisch-Test", "Deutsch-Test", "Physik-Test", "Chemie-Test",
  "Bruchrechnung Test", "kurze Kontrolle", "Lernzielkontrolle",
  "TÜ erstellen", or "Übungsarbeit".
  Creates tests and exams as Word files (.docx) for Sekundarstufe I with
  A-Kurs/B-Kurs differentiation, OMML formulas, Rechenkästchen, and
  Koordinatensysteme.
---

# Leistungskontrolle erstellen

Erzeugt separate .docx-Dateien pro Kurs (A-Kurs, B-Kurs, ggf. individuelle Variante) mit echten Word-Formeln, Rechenkästchen und Koordinatensystemen.

## Verfügbare Scripts

| Script | Zweck |
|--------|-------|
| `scripts/omml_utils.py` | OMML-Formelfunktionen: `F(z,n)` Bruch, `T(text)` Operator, `M(g,z,n)` gemischte Zahl |
| `scripts/template.py` | Dokument-Grundgerüst + Aufgaben-Hilfsfunktionen (siehe API unten) |

### template.py API

| Funktion | Zweck |
|----------|-------|
| `create_test_document(...)` | Grundgerüst erzeugen (Kopf, Name, Meta) -- je ein .docx pro Kurs |
| `add_aufgabe(doc, nummer, titel, punkte_a, punkte_b=None)` | Aufgaben-Überschrift mit Punkten rechtsbündig am Rand. B-Punkte optional darunter. |
| `add_b_marker(doc)` | Grünes **B**-Icon vor B-Kurs-Teilaufgaben. Gibt Paragraph zurück für `.add_run()`. |
| `add_rechenkaestchen(doc, rows, cols)` | Kariertes Kästchengitter als Antwortfläche |
| `add_answer_lines(doc, count)` | Leere Antwortzeilen für Textantworten |
| `add_value_table(doc, headers, data)` | Wertetabelle mit optionalen Leerfeldern |
| `add_coordinate_system(doc, x_range, y_range)` | Leeres Koordinatensystem (matplotlib-Bild) |
| `add_bewertungsfuss(doc, gesamtpunkte, punkte_b)` | Bewertungsfuß: Punkte / Zensur / Schulleitung / Unterschrift |
| `add_notenschluessel(doc, gesamtpunkte)` | Alternative: Notenschlüssel-Tabelle (Brandenburg) |
| `save_documents(docs, basename)` | Speichert als separate Dateien pro Kurs |

## Referenzdateien

| Datei | Inhalt |
|-------|--------|
| `reference/lehrplan.md` | Themen-Katalog alle Fächer Kl. 7-10, Niveauunterschiede A/B-Kurs |
| `reference/aufgabentypen.md` | Aufgabentypen pro Fach/Thema mit AFB-Zuordnung und A/B-Beispielen |
| `../unterricht/didaktik/englisch.md` | Fachdidaktik Englisch: Hörgeschädigte, visuelle Methoden, Stundenstruktur, Differenzierung |
| `../unterricht/didaktik/deutsch.md` | Fachdidaktik Deutsch: Hörgeschädigte, visuelle Methoden, Stundenstruktur, Differenzierung |
| `../unterricht/didaktik/physik.md` | Fachdidaktik Physik: Hörgeschädigte, Experimente, Formeln, Sicherheit, Differenzierung |
| `../unterricht/didaktik/chemie.md` | Fachdidaktik Chemie: Hörgeschädigte, Laborprotokolle, GHS-Symbole, Differenzierung |
| `../unterricht/didaktik/mathematik.md` | Fachdidaktik Mathematik: Hörgeschädigte, visuelle Methoden, Textaufgaben, Differenzierung |

Rechtliche Grundlagen (Sek I-V, VV-Leistungsbewertung):
- `../../skills/vv/quellen/brandenburg/sek_i_v.md`
- `../../skills/vv/quellen/brandenburg/vv_leistungsbewertung.md`

## Schulinformationen (aus `config/lehrer.md` oder beim Lehrer erfragen)

Beim Start immer `config/lehrer.md` lesen. Falls vorhanden, Schulinfos daraus übernehmen.
Falls leer oder nicht vorhanden: Grunddaten erfragen und in `config/lehrer.md` speichern.

- **Schule**: Schulname aus `config/lehrer.md` oder erfragen
- **Schulform**: Schultyp aus `config/lehrer.md` (Förderschule, Oberschule, Gesamtschule, Gymnasium)
- **Bundesland**: Aus `config/lehrer.md` oder `userConfig.bundesland` (Default: Berlin)
- **Sekundarstufe**: Klassenstufen 7 bis 10
- **System**: Integrativ (bildungsgangübergreifend, § 51 Abs. 1 Nr. 2 Sek I-V)
- **Differenzierung** (§ 51 Abs. 4 Sek I-V):
  - Ab 2. HJ Kl. 7: Mathematik + Englisch
  - Spätestens ab Kl. 9: Deutsch
  - Ab Kl. 9: Physik oder Chemie
- **A-Kurs**: Grundlegende Bildung (EBR-Niveau)
- **B-Kurs**: Erweiterte Bildung (FOR-Niveau)
- **Notenumrechnung** (§ 55 Abs. 5): B-Kurs-Note = eine Stufe besser als A-Kurs

## Anforderungsbereiche (AFB)

Jede Leistungskontrolle muss **mehrere Anforderungsbereiche** abdecken:

| AFB | Beschreibung | Typische Operatoren | Anteil |
|-----|-------------|---------------------|--------|
| I (Reproduzieren) | Wissen wiedergeben, Verfahren anwenden | nenne, berechne, ordne zu, ergänze | ~40% |
| II (Zusammenhänge) | Zusammenhänge erkennen, Verfahren auswählen | löse, stelle dar, vergleiche, zeichne | ~40% |
| III (Verallgemeinern) | Transfer, Begründen, Problemlösen | begründe, erkläre, modelliere | ~20% |

Konsultiere `reference/aufgabentypen.md` für konkrete Aufgabenbeispiele pro Fach und Thema.

## Differenzierung

### A-Kurs vs. B-Kurs

Zwei Muster (können kombiniert werden):

**Muster 1 -- Gemischte Aufgabe:** Gleiche Basisaufgabe, B-Kurs bekommt Zusatzteile.
```
Aufgabe 3 (A: /3 P., B: /6 P.)
a) Lies die Gleichungen ab.              ← alle
b) Bestimme den Schnittpunkt.            ← alle
B: c) Überprüfe rechnerisch (Probe).     ← nur B
```

**Muster 2 -- Getrennte Aufgaben:** Unterschiedliche Aufgaben gleichen Typs, B komplexer.

### Bonus/Zusatz

Extraaufgabe am Ende, geht NICHT in die Gesamtpunktzahl ein:
```
Zusatz: Sachaufgabe (+5 P.)
```

### Individuelle Variante (IND)

Für Schüler mit besonderem Förderbedarf -- eigene .docx-Datei:
- Gleiche Themen, weniger Aufgaben (3-4 statt 5-7)
- Mehr Struktur: Lückentexte, Zuordnung, Ankreuzen statt freier Lösung
- Einfachere Zahlen, weniger Rechenschritte
- Gleiche Punkte-Noten-Zuordnung (gleiche prozentuale Anforderung)

## Workflow

### 0. Lehrer-Profil laden

`config/lehrer.md` lesen. Bekannte Präferenzen (Fach, Klassenstufe, Kurs, Testformat)
vorausfüllen. Neue Präferenzen nach der Erstellung in `config/lehrer.md` notieren.

### 1. Abfrage (EINE Nachricht mit allen Fragen)

**Grunddaten:**

| Pflicht | Frage |
|---------|-------|
| Art | TÜ / Lernerfolgskontrolle / Klassenarbeit? |
| Fach | Mathematik, Englisch, Deutsch, Physik, Chemie? |
| Klassenstufe | 7, 8, 9, 10? |
| Kurse | Beide (A+B), nur A, nur B? |
| Modus | Getrennt (separate Dateien pro Kurs) oder integriert? |

**Inhaltliche Details:**

| Pflicht | Frage |
|---------|-------|
| Thema | Konkretes Thema + Unterthemen (z.B. "LGS: Einsetzungsverfahren und Gleichsetzungsverfahren, OHNE Additionsverfahren") |
| Buchseiten | Welche Seiten im Buch wurden behandelt? (z.B. "S. 88-95") |
| Zeitraum | Seit wann / seit welcher Arbeit? (z.B. "seit den Herbstferien" oder "Kapitel 4") |
| Geübte Aufgabentypen | Welche Aufgabentypen wurden im Unterricht geübt? (z.B. "Textaufgaben, Gleichungen aufstellen, graphisch lösen") |
| Schwächen der Klasse | Bekannte Probleme? (z.B. "Klasse hat Schwierigkeiten mit Textaufgaben" oder "Bruchrechnung sitzt noch nicht") |

**Optional:**

| Optional | Frage |
|----------|-------|
| Individuelle Variante | IND nötig? Falls ja: für welche Schüler, welche Anpassungen? |
| Hilfsmittel | Erlaubt? (Standard: keine) |
| Dauer | Wie lange? (Standard: TÜ 20min, LEK 30min, KA 45min) |
| Schwerpunkt | Soll ein bestimmtes Unterthema stärker gewichtet werden? |
| Bonus | Zusatzaufgabe gewünscht? |

### 2. Script generieren

Importiere die fertigen Module -- NICHT den OMML-Code neu schreiben.
Konsultiere `reference/aufgabentypen.md` für passende Aufgabenformate.

```python
import sys, os
sys.path.insert(0, os.path.join("${CLAUDE_SKILL_DIR}", "scripts"))
from omml_utils import F, T, M, add_math, add_math_line, MINUS, MAL
from template import (
    create_test_document, add_bewertungsfuss, save_documents,
    add_aufgabe, add_rechenkaestchen, add_answer_lines,
    add_value_table, add_coordinate_system
)

# Dokumente erzeugen (je ein .docx pro Kurs)
docs = create_test_document(
    fach="Mathematik", thema="Lineare Gleichungssysteme", klassenstufe=9,
    art="Klassenarbeit", zeit="45 Min", hilfsmittel="keine",
    punkte_a=39, punkte_b=52, punkte_ind=32,
    kurse=["A", "B", "IND"], ind_schueler="Ory und Layla"
)

# === A-Kurs ===
doc_a = docs["A"]

# AFB I: Zahlenpaare prüfen
add_aufgabe(doc_a, 1, "Zahlenpaare prüfen", 3)
doc_a.add_paragraph("Prüfe, ob die Zahlenpaare Lösungen der Gleichung 5x − 3y = −7 sind.")
doc_a.add_paragraph("Schreibe auf!")
add_rechenkaestchen(doc_a, rows=4, cols=20)

# AFB I: Wertetabelle
add_aufgabe(doc_a, 2, "Wertetabelle ergänzen", 3)
doc_a.add_paragraph("Ergänze die fehlenden Werte für 3x + 2y = 6.")
add_value_table(doc_a, ["x", "y"], [[0, ""], ["", 0], [1, ""]])
add_rechenkaestchen(doc_a, rows=3, cols=20)

# AFB II: Graphisches Lösen
add_aufgabe(doc_a, 3, "Graphisches Lösungsverfahren", 5)
doc_a.add_paragraph("Zeichne die Geraden y = 2x − 1 und y = 1,5x − 5 in das Koordinatensystem.")
doc_a.add_paragraph("Lies den Schnittpunkt S ab.")
add_coordinate_system(doc_a, x_range=(-2, 8), y_range=(-6, 6))

# AFB II: Algebraisch lösen
add_aufgabe(doc_a, 4, "Gleichsetzungsverfahren", 6)
doc_a.add_paragraph("Löse mit dem Gleichsetzungsverfahren. Mache die Probe!")
add_math_line(doc_a, T("I:  y = 3 "), T(MINUS), T(" x"))
add_math_line(doc_a, T("II: y = 2x "), T(MINUS), T(" 6"))
add_rechenkaestchen(doc_a, rows=8, cols=20)

# Bewertungsfuß (statt Notenschlüssel)
add_bewertungsfuss(doc_a, 39)

# === B-Kurs ===
doc_b = docs["B"]
# ... (gleiche Struktur, mehr/schwierigere Aufgaben, punkte_b=52)

add_bewertungsfuss(doc_b, 52)

# === Individuelle Variante ===
doc_ind = docs["IND"]
# ... (gleiche Themen, weniger Aufgaben, mehr Struktur)

add_bewertungsfuss(doc_ind, 32)

# Speichern + Öffnen
save_documents(docs, "LGS_Kl9")
```

### 3. Ausführen + Öffnen

```bash
uv run script.py
open LGS_Kl9_A-Kurs.docx
open LGS_Kl9_B-Kurs.docx
open LGS_Kl9_Individuell.docx
```

## Standardwerte

| Art | Zeit | Aufgaben A/B | Punkte A/B |
|----|------|-------------|-----------|
| TÜ | 10-15 Min | 3-4 / 3-4 | 15-20 / 10-15 |
| Lernerfolgskontrolle | 20-30 Min | 4-5 / 4-5 | 25-30 / 20-25 |
| Klassenarbeit | 45-90 Min | 5-8 / 5-7 | 35-60 / 25-50 |

IND: ~60-70% der Aufgabenanzahl des A-Kurses, gleiche Punkte-Noten-Prozente.

## Besonderheit Förderbedarf Hören

Bei JEDER Aufgabe beachten:
- Klare, eindeutige, kurze Sätze
- Fachbegriffe beim ersten Auftreten **fett**
- Visuelle Unterstützung (Tabellen, Zuordnungen, Skizzen)
- Englisch: KEIN Hörverstehen -> Leseverstehen
- Deutsch: KEIN Diktat -> Abschreibübungen/Lückentexte

### Nachteilsausgleich (§ 21 Abs. 3 Sek I-V)

- Verlängerung der Arbeitszeit
- Besondere Hilfsmittel
- Fachliche Anforderungen bleiben unberührt

## Regeln für schriftliche Arbeiten (VV-Leistungsbewertung)

- Gewichtung Sek I: **25%** der Gesamtnote
- Ankündigung: mind. **5 Unterrichtstage** vorher
- Max. **1 pro Tag**, **2 pro Woche** pro Schüler
- Korrekturzeit: max. **2 Wochen**
- Wenn >1/3 mangelhaft/ungenügend: Schulleitung prüft Wiederholung
- Aufgaben müssen **mehrere Anforderungsbereiche** umfassen

## Aufgabengestaltung

### Antwortflächen

- **Rechenkästchen** (`add_rechenkaestchen`): Standard für Mathe/Physik/Chemie. Kariertes Gitter für Rechnungen.
- **Antwortzeilen** (`add_answer_lines`): Für Textantworten (Deutsch, Englisch, Erklärungen).
- **Koordinatensystem** (`add_coordinate_system`): Für Graphen zeichnen. Achsenbereich passend zum Aufgabeninhalt wählen.
- **Wertetabelle** (`add_value_table`): Für Funktionswerte, Zuordnungen. Leere Felder = auszufüllen.

### Probe (Gegenrechnung)

Bei algebraischen Verfahren (Gleichsetzung, Einsetzung, Addition) IMMER "Mache die Probe!" als Teilaufgabe fordern. Punkte dafür einplanen.

### Bewertungsfuß

Am Ende jedes Dokuments `add_bewertungsfuss()` statt `add_notenschluessel()` verwenden:
- Punkte: ___ / Gesamt
- Optional: B-Kurs-Punkte (bei gemischten Dokumenten)
- Zensur
- Schulleitung
- Unterschrift Erziehungsberechtigte

## Common Gotchas

- **Umlaute und ß IMMER verwenden** -- im Dokumenttext korrekt Deutsch schreiben: ä, ö, ü, Ä, Ö, Ü, ß. NIEMALS "ue", "ae", "oe" oder "ss" als Ersatz. Nur Dateinamen ohne Umlaute.
- python-docx + lxml + matplotlib werden von `uv` automatisch installiert
- Brüche/Formeln IMMER über `omml_utils` -- NIEMALS als Text "3/4"
- Dateinamen ohne Umlaute (Buerger statt Bürger)
- Schulname im Dokument aus `config/lehrer.md` oder vorherigem Gespräch übernehmen
- Separate Dateien pro Kurs (nicht beide Kurse in ein Dokument)
- Rechenkästchen für Rechenaufgaben, Antwortzeilen für Textaufgaben
- Koordinatensystem: Achsenbereich passend wählen (nicht zu groß/klein)
- Probe bei algebraischen Verfahren nicht vergessen
- IND-Variante: gleiche Themen, weniger/einfachere Aufgaben, mehr Struktur

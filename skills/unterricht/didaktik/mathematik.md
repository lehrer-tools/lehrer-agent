# Didaktik Mathematik

Allgemeine fachdidaktische Referenz für den Mathematikunterricht (Sekundarstufe I).

**Hinweis**: Dieses Dokument enthält allgemeine fachdidaktische Grundlagen.
Für Lehrplaninhalte und Aufgabentypen siehe `lehrplan.md` und `aufgabentypen.md`.
Für hörgeschädigtenspezifische Ergänzungen siehe
`foerderschwerpunkt/hoeren_mathematik.md`.

## Notation und Konventionen

### Mathematische Notation
Alle Formeln und Gleichungen werden über die OMML-Funktionen (`omml_utils.py`)
dargestellt — NIEMALS als Klartext (z.B. nicht „3/4" sondern `F(3,4)`).
Siehe `leistungskontrolle/SKILL.md` für Details.

### Darstellungskonventionen
| Element | Konvention | Beispiel |
|---------|-----------|---------|
| Lösung als Zahlenpaar | S(x \| y) | S(2 \| 3) |
| Gleichungsnummerierung | Römisch I:, II: | I: y = 2x − 1 |
| Probe | Einsetzen → Rechnung → w.A. / ✓ | 3 = 2·2 − 1 = 3 ✓ w.A. |
| Aufgabenverweis Buch | B.S. Seite/Aufgabe | B.S. 89/2a-c |
| Aufgabenverweis AH | AH S. Seite/Aufgabe | AH S. 20/1,2,3 |
| Thema-Nummerierung | (1), (2), (3) | (1) Lineare Gleichungen mit 2 Variablen |
| Verfahrens-Nummerierung | I, II, III | I Gleichsetzungsverfahren |

### Formelheft
Schüler führen ein Formelheft mit:
- Formel + Name + Einheiten
- Beispielrechnung
- Ggf. Formeldreieck (für einfacheres Umstellen)

## Typische Stundenstruktur

Die Stundenstruktur ist detailliert in der `unterricht/SKILL.md` beschrieben.
Hier die fachspezifischen Ergänzungen für Mathematik:

### Einführung (ca. 10 Min)
1. **Hausaufgabenkontrolle**: Visuell (Dokumentenkamera, Tafel).
   Ergebnisse an der Tafel sammeln.
2. **Einstieg**: Problemstellung visuell (Bild, Diagramm, Alltagssituation).
   Frage an der Tafel notieren.
3. **Vorwissen**: Bekannte Begriffe/Formeln kurz wiederholen (visuell, Tafel).
4. **Vorentlastung**: Neue Fachbegriffe einführen (Wort + Symbol + Beispiel).

### Übung (ca. 25 Min)

1. **Erarbeitung**: Neuer Stoff im Lehrgespräch.
   Beispiel Schritt für Schritt an der Tafel.
2. **Merke-Kasten**: Regel/Definition ins Heft — visuell hervorgehoben.
3. **Übungsaufgaben**: Erst gemeinsam (Tafel), dann Einzelarbeit (Buch/AH).
   Bei Schwierigkeiten: Rückgriff auf Merke-Kasten und Formelheft.
4. **Partnerarbeit**: Ergebnisse vergleichen, sich gegenseitig erklären.

### Sicherung (ca. 10 Min)
1. **Ergebnisse vergleichen**: Schüler zeigen Lösungen (Dokumentenkamera, Tafel)
2. **Typische Fehler** besprechen (visuell zeigen)
3. **Hausaufgabe**: Klar an der Tafel mit Seitenangabe + Aufgabennummer

### Ablaufskizze (nummeriert)
```
1. HA-Kontrolle (AH/B.S.)     → visuell an der Tafel
2. Besprechung                  → Dokumentenkamera / Tafel
3. Mündliche Kontrolle          → Schüler erklären Lösungswege
4. Neustoff / Wiederholung      → Tafel, Beispiel, Merke
5. Übung (AH/B.S.)             → Einzelarbeit / Partner
6. Zusammenfassung              → Ergebnissicherung, HA
```

## Differenzierung A-Kurs / B-Kurs

Die Fachleistungsdifferenzierung in Mathematik beginnt je nach Bundesland
ab Klasse 7 oder 9.

### A-Kurs (grundlegende Bildung — EBR)
- **Aufgaben**: Klar, einfach, strukturiert; ein Rechenschritt;
  Grundformeln einsetzen (Werte gegeben); Zahlenwerte „passend" (ganzzahlig)
- **Textaufgaben**: Kurz, klar, eine Frage; relevante Größen hervorgehoben;
  ggf. mit Skizze/Bild als Hilfe
- **Formeln**: Einsetzen ja, Umstellen nein; Formeldreieck als Hilfe
- **Hilfestellungen**: Lückentexte, Zuordnungsaufgaben, Multiple Choice,
  vorstrukturierte Lösungswege, Zwischenschritte vorgegeben
- **Geometrie**: Grundfiguren, Flächen-/Umfangsberechnung, einfache Körper
- **Diagramme**: Werte ablesen; einfache Zuordnung
- **Niveaustufe F** (Förderstufe) im Stoffverteiler

### B-Kurs (erweiterte Bildung — FOR)
- **Aufgaben**: Komplex, mehrstufig, Transfer; mehrere Rechenschritte;
  Formeln umstellen; realitätsnahe Zahlenwerte
- **Textaufgaben**: Komplexer, mehrere Schritte; Modellierung nötig;
  relevante von irrelevanten Informationen trennen
- **Formeln**: Umstellen nach gesuchter Größe; mehrere Formeln kombinieren
- **Hilfestellungen**: Weniger; freie Formulierung, eigenständige Strukturierung,
  Begründungen gefordert
- **Geometrie**: Zusammengesetzte Körper, Pythagoras, Flächeninhalt komplexerer Figuren
- **Diagramme**: Selbst erstellen; Zusammenhänge beschreiben; interpretieren
- **Niveaustufe G** (Grundstufe / erweitert) im Stoffverteiler

### Differenzierungsbeispiel
```
Aufgabe: Prozentrechnung

A-Kurs:
  Ein Fahrrad kostet 450 €. Du bekommst 20 % Rabatt.
  a) Berechne den Rabatt.     Rabatt = 450 € · 20/100 = ___
  b) Berechne den neuen Preis. Neuer Preis = 450 € − ___ = ___

B-Kurs:
  Ein Laptop kostet nach 15 % Rabatt noch 637,50 €.
  a) Berechne den ursprünglichen Preis.
  b) Im Angebot kommt noch 3 % Skonto hinzu.
     Wie viel zahlst du insgesamt?
  c) Lohnt sich das Angebot im Vergleich zu einem anderen Laptop
     für 600 € ohne Rabatt? Begründe.
```

## Visuelle Methoden und Materialien

### Grundprinzip
Mathematik ist die „visuelle Sprache" der Naturwissenschaften.
Visuelle und handlungsorientierte Zugänge fördern das Verständnis.
Das Prinzip der **Anschaulichkeit** hat in der Mathematikdidaktik
einen hohen Stellenwert.

### Darstellungswechsel (EIS-Prinzip)
| Ebene | Beschreibung | Beispiel (Bruchrechnung) |
|-------|-------------|-------------------------|
| **E**naktiv (handelnd) | Reale Objekte manipulieren | Pizza in Teile schneiden |
| **I**konisch (bildlich) | Zeichnungen, Diagramme | Kreisdiagramm mit farbigen Teilen |
| **S**ymbolisch (formal) | Zahlen, Formeln, Terme | ¾ + ¼ = 1 |

Der Wechsel zwischen den Ebenen muss explizit begleitet und geübt werden.

### Methoden
| Methode | Beschreibung | Einsatz |
|---------|-------------|---------|
| **Merkheft / Formelheft** | Regeln, Formeln, Beispiele gesammelt | Nachschlagewerk, Prüfungsvorbereitung |
| **Koordinatensysteme (vorgedruckt)** | Leere Koordinatensysteme zum Einzeichnen | Lineare/quadratische Funktionen, LGS |
| **Wertetabellen** | Systematisch Werte einsetzen und berechnen | Funktionen, Zuordnungen |
| **Formeldreieck** | Visuelles Umstellungstool für Formeln | Physik/Chemie-Formeln in Mathe |
| **Farbcodierung** | Verschiedene Geraden in verschiedenen Farben | LGS graphisch: rot = Gleichung I, blau = Gleichung II |
| **Lösungsschritte nummerieren** | Verfahren als nummerierte Schrittliste | Gleichsetzungs-, Einsetzungs-, Additionsverfahren |
| **Realobjekte** | Gegenstände zum Anfassen | Geometrie (Pyramiden, Prismen), Prozente (Geld) |
| **Lernkartei** | Fachbegriff → Definition + Beispiel | Wortschatzarbeit Mathematik |
| **Lernposter** | Wichtige Regeln als Plakat im Klassenraum | Bruchrechenregeln, Vorzeichenregeln, Potenzgesetze |
| **Dokumentenkamera** | Schülerhefte live projizieren | Ergebnisvergleich, Fehleranalyse |
| **GeoGebra / Simulationen** | Interaktive Graphen, geometrische Konstruktionen | Funktionen, Geometrie, dynamisch verändern |
| **Spielerische Automatisierung** | Mathe-Bingo, Kopfrechenspiele (visuell) | Grundrechenarten festigen |
| **Mind-Maps** | Themenübersichten, Verfahrensvergleiche | Zusammenfassung, Wiederholung |

### Tafelarbeit
- Stundenziel + Ablauf sichtbar
- Neue Fachbegriffe: Wort — Symbol — Beispiel (drei Spalten)
- Beispielrechnungen: Schritt für Schritt, mit Nummerierung
- Merksätze: eingerahmt, klar formuliert
- Gleichungen: I: und II: deutlich markiert

### Textaufgaben visuell aufbereiten
Textaufgaben sind häufig eine Hürde. Strategien:
1. **Schlüsselwörter markieren**: Relevante Zahlen und Fragewörter farbig
2. **Skizze anfertigen**: Jede Textaufgabe als Bild/Skizze darstellen
3. **Tabelle erstellen**: Gegeben / Gesucht / Formel / Lösung
4. **Vereinfachte Sprache**: Kurze Sätze, bekannte Wörter, Fachbegriffe erklärt
5. **Stufenweise**: Erst Rechenaufgabe ohne Text → dann kurzer Text →
   dann komplexerer Text

## Lehrplan-Bezüge

Bundeslandspezifische Lehrplan-Bezüge (Kompetenzbereiche, Themenfelder, Niveaustufen)
finden sich unter `didaktik/lehrplan/<bundesland>/rahmenlehrplan.md`.

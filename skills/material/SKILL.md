---
name: material
description: >
  This skill should be used when the user wants to "Material suchen",
  "Material sammeln", "Arbeitsblätter suchen", "Unterrichtsmaterial finden",
  "Material zum Thema", "Was gibt es zu", "Ressourcen suchen",
  "Material vorbereiten", or "Quellen sammeln".
  Collects teaching material from local books (BiBox), publisher platforms
  (BiBox Online, Klett, Cornelsen), and free web sources (OER, worksheets,
  videos, simulations). Creates a structured material collection.
---

# Material sammeln

Durchsucht lokale und Online-Quellen nach Unterrichtsmaterial zu einem bestimmten Thema und erstellt eine strukturierte Übersicht.

## Quellen (Prioritätsreihenfolge)

### 1. Lokale Bücher (`books/`)

Höchste Priorität -- bereits extrahiertes Material ist sofort nutzbar.

- Buchtext durchsuchen (Grep nach Thema in `books/*/*.txt`)
- Zusatzmaterial-Index prüfen (`books/*/Zusatzmaterial.md`)
- Relevante Arbeitsblätter, Kopiervorlagen, Lösungen identifizieren
- Seitenangaben und Aufgabennummern notieren

### 2. BiBox Desktop (lokal)

Falls das Buch noch nicht extrahiert wurde:

```bash
bibox                    # Westermann: Alle verfügbaren Bücher auflisten
bibox --book <id>        # Westermann: Buch extrahieren
```

### 3. Klett Lernen (lokal)

```bash
klett                    # Klett: Alle verfügbaren Bücher auflisten
klett --book <DUA-ID>    # Klett: Buch extrahieren
```

### 4. Cornelsen Offline Lernen (lokal)

```bash
cornelsen                # Cornelsen: Alle verfügbaren Bücher auflisten
cornelsen --book <id>    # Cornelsen: Buch extrahieren
```

Prüfe ob weitere Bücher zum Fach in den Verlags-Apps vorhanden sind, die noch nicht extrahiert wurden.

### 5. Verlags-Plattformen (Online, Login-pflichtig)

Über Playwright MCP auf Login-pflichtige Plattformen zugreifen:

| Plattform | URL | Inhalte |
|-----------|-----|---------|
| **BiBox Online** | `bibox.schule` | Westermann-Bücher + digitale Zusatzmaterialien |
| **Klett** | `klett.de/digitaler-unterrichtsassistent` | Klett-Bücher + Arbeitsblätter |
| **Cornelsen** | `cornelsen.de/digital` | Cornelsen-Bücher + Materialien |

**Workflow Verlags-Plattformen:**
1. Playwright: Zur Plattform navigieren
2. Login-Status prüfen (evtl. schon eingeloggt)
3. Falls nicht eingeloggt: Lehrer fragen ob Login möglich/gewünscht
4. Nach Thema/Fach suchen
5. Relevante Materialien identifizieren und Links sammeln

### 6. Freie Web-Quellen

Per Perplexity-Suche nach freiem Unterrichtsmaterial suchen:

| Quelle | Typ | Beschreibung |
|--------|-----|-------------|
| **4teachers.de** | Arbeitsblätter | Community-Plattform, viele Fächer |
| **unterrichtsmaterial.ch** | Arbeitsblätter | Schweizer Plattform, gute Mathe-Materialien |
| **ZUM-Wiki** | OER | Zentrale für Unterrichtsmedien, freie Lizenzen |
| **Serlo** | OER | Freie Lernplattform, v.a. Mathe |
| **Planet Schule** | Videos | SWR/WDR Schulfernsehen, Filme + Arbeitsblätter |
| **Schulfernsehen** | Videos | BR alpha, Telekolleg |
| **PhET** | Simulationen | University of Colorado, interaktive Simulationen (Physik, Chemie, Mathe) |
| **GeoGebra** | Simulationen | Dynamische Mathematik-Software, Applets |
| **LearningApps** | Interaktiv | Kleine interaktive Übungen |
| **Bildungsserver** | Portal | Deutscher Bildungsserver, Landesbildungsserver |
| **YouTube** | Videos | Mathe by Daniel Jung, Lehrer Schmidt, musstewissen, Simple Club |

**Suchstrategie:**
```
Perplexity: "<Fach> <Thema> Arbeitsblatt Klasse <N> PDF"
Perplexity: "<Fach> <Thema> Unterrichtsmaterial kostenlos"
Perplexity: "<Thema> simulation interactive"
```

## Workflow

### 1. Thema und Kontext klären

Aus `$ARGUMENTS`, `config/lehrer.md` oder Nachfrage bestimmen:
- **Fach** (Mathematik, Deutsch, Englisch, Physik, Chemie)
- **Thema** (z.B. "Lineare Gleichungssysteme", "Simple Past", "Optik")
- **Klassenstufe** (7-10)
- **Kurs** (A/B oder beide)
- **Zweck** (Einführung, Übung, Wiederholung, Vertiefung, Projekt)

### 2. Lokale Quellen durchsuchen

1. `books/` nach passendem Buch durchsuchen
2. Im Buchtext per Grep das Thema finden
3. Zusatzmaterial-Index prüfen
4. Relevante Seiten und Materialien notieren

### 3. Verlags-Apps prüfen

1. `bibox`, `klett`, `cornelsen` aufrufen um verfügbare Bücher zu listen
2. Prüfen ob weitere Bücher zum Fach vorhanden aber nicht extrahiert sind
3. Falls ja: dem Lehrer anbieten, sie zu extrahieren

### 4. Online-Quellen durchsuchen

1. Perplexity-Suche nach freiem Material
2. Ergebnisse nach Relevanz und Qualität filtern
3. Direkte Links zu PDFs/Arbeitsblättern bevorzugen

### 5. Verlags-Plattformen (optional)

Nur wenn der Lehrer es wünscht oder lokales Material nicht ausreicht:
1. Playwright: BiBox Online, Klett, Cornelsen
2. Nach Thema suchen
3. Verfügbare Materialien auflisten

### 6. Ergebnis präsentieren

Strukturierte Übersicht mit:

```markdown
## Material zu <Thema> (<Fach>, Klasse <N>)

### Lokale Bücher
| Quelle | Seiten | Inhalt | Typ |
|--------|--------|--------|-----|
| Mathematik heute 9, S. 88-95 | 8 S. | Einführung LGS | Buchtext |
| Mathematik heute 9, AB 4.1 | 2 S. | Übungsblatt LGS | Arbeitsblatt |

### Freie Online-Quellen
| Quelle | Link | Typ | Bewertung |
|--------|------|-----|-----------|
| Serlo: LGS | serlo.org/... | Erkärung + Übungen | Gut für Selbstlernen |
| PhET: System of Equations | phet.colorado.edu/... | Simulation | Interaktiv, Einstieg |

### Videos
| Titel | Link | Dauer | Hinweise |
|-------|------|-------|----------|
| Mathe by Daniel Jung: LGS | youtube.com/... | 5:30 | Kompakt, gut für B-Kurs |

### Verlags-Material (Login nötig)
| Plattform | Material | Verfügbar |
|-----------|----------|-----------|
| BiBox Online | Interaktives AB | Ja (Lizenz vorhanden) |
```

## Wichtige Regeln

- **Lokale Quellen zuerst** -- bereits vorhandenes Material hat Vorrang
- **Links verifizieren** -- bei Web-Quellen prüfen ob der Link noch funktioniert
- **Urheberrecht beachten** -- bei Verlags-Material auf Lizenz hinweisen
- **Qualität vor Quantität** -- lieber 5 gute Quellen als 20 mittelmäßige
- **Förderschwerpunkt beachten** -- bei Förderschulen Material auf Eignung prüfen (z.B. visuelle Aufbereitung bei Hören, vereinfachte Sprache bei Lernen)
- **Differenzierung** -- Material für A-Kurs und B-Kurs getrennt bewerten
- **Perplexity statt Google** -- Für Web-Suchen immer `search_perplexity` MCP-Tool verwenden (da WebSearch nicht verfügbar)
- **Umlaute** -- ä, ö, ü, ß korrekt verwenden

## Lehrer-Profil nutzen

`config/lehrer.md` beim Start lesen. Daraus ableiten:

- **Fächer und Klassenstufen** -- Suche eingrenzen
- **Lehrbücher** -- bekannte Bücher bevorzugt durchsuchen
- **Förderschwerpunkt** -- Material auf Eignung filtern
- Neue Lehrbuch-Einträge in `config/lehrer.md` notieren wenn der Lehrer ein neues Buch nennt

## Integration mit anderen Skills

- **/lehrer-agent:unterricht** -- gefundenes Material wird für die Unterrichtsvorbereitung genutzt
- **/lehrer-agent:leistungskontrolle** -- Aufgaben aus gefundenem Material können in Tests einfließen
- **Verlags-Tools** — `bibox` (Westermann), `klett`, `cornelsen` zum Extrahieren neuer Bücher

## Portal-Konfiguration (`portale.md`)

Die Datei `portale.md` (im selben Verzeichnis) enthält die konfigurierbaren Verlags-Plattformen
und Lehrbuch-URLs. Der Lehrer kann dort seine Zugänge und bevorzugten Portale eintragen.

**Ablauf:**
1. Prüfe ob `books/` bereits Material zum Fach enthält
2. Falls nicht: lies `portale.md` und gehe die konfigurierten Portale der Reihe nach durch
3. Nur Portale durchsuchen, die in `portale.md` als `aktiv: ja` markiert sind
4. Bei Login-pflichtigen Portalen: Playwright nutzen, Lehrer fragen falls Login nötig

# Portal-Konfiguration für Material-Suche

Hier konfiguriert der Lehrer, welche Portale und Plattformen der Material-Skill
durchsuchen soll. Portale mit `aktiv: ja` werden automatisch durchsucht.

## Verlags-Plattformen (Login-pflichtig)

### BiBox Online (Westermann-Gruppe)
- **URL**: https://bibox.schule
- **Aktiv**: ja
- **Login**: Playwright (Browser-Session)
- **Verlag**: Westermann, Schroedel, Diesterweg, Schöningh
- **Inhalte**: Digitale Schulbücher + Zusatzmaterialien (Arbeitsblätter, Lösungen, interaktive Übungen)
- **Lehrbücher** (Beispiele, an eigene Bücher anpassen):
  - Mathematik heute (Klasse 5–10)
  - Elemente der Mathematik
  - Sekundo (Mathematik, Förderschule)
  - Camden Town (Englisch)
  - Praxis Sprache (Deutsch)
  - Erlebnis Physik / Chemie
  - Dorn Bader Physik

### Klett (Digitaler Unterrichtsassistent)
- **URL**: https://www.klett.de/digitaler-unterrichtsassistent
- **Aktiv**: nein
- **Login**: Playwright (Browser-Session)
- **Verlag**: Klett, Klett-Cotta
- **Inhalte**: Digitale Schulbücher + Kopiervorlagen + Lösungen
- **Lehrbücher** (Beispiele):
  - Lambacher Schweizer (Mathematik)
  - deutsch.kompetent (Deutsch)
  - Green Line (Englisch)
  - Impulse Physik
  - Elemente Chemie

### Cornelsen
- **URL**: https://www.cornelsen.de/digital
- **Aktiv**: nein
- **Login**: Playwright (Browser-Session)
- **Verlag**: Cornelsen, Volk und Wissen, Oldenbourg
- **Inhalte**: Digitale Schulbücher + Arbeitsblätter
- **Lehrbücher** (Beispiele):
  - Fundamente der Mathematik
  - Schlüssel zur Mathematik
  - Deutschbuch
  - English G Access / Lighthouse
  - Universum Physik
  - Fokus Chemie

## Freie Plattformen (kein Login)

### Serlo
- **URL**: https://de.serlo.org
- **Aktiv**: ja
- **Fächer**: Mathematik, Biologie, Chemie, Informatik, Nachhaltigkeit
- **Suchstrategie**: Perplexity: "site:serlo.org <Thema>"

### GeoGebra
- **URL**: https://www.geogebra.org/materials
- **Aktiv**: ja
- **Fächer**: Mathematik (Geometrie, Algebra, Analysis)
- **Suchstrategie**: WebFetch auf `https://www.geogebra.org/search/<Suchbegriff>`

### PhET Simulationen
- **URL**: https://phet.colorado.edu/de/simulations
- **Aktiv**: ja
- **Fächer**: Physik, Chemie, Mathematik
- **Suchstrategie**: Perplexity: "site:phet.colorado.edu <Thema> simulation"

### Planet Schule
- **URL**: https://www.planet-schule.de
- **Aktiv**: ja
- **Fächer**: Alle (Filme, Simulationen, Arbeitsblätter)
- **Suchstrategie**: Perplexity: "site:planet-schule.de <Thema>"

### ZUM-Wiki / ZUM-Unterrichten
- **URL**: https://unterrichten.zum.de
- **Aktiv**: ja
- **Fächer**: Alle (OER-Material, Wiki-basiert)
- **Suchstrategie**: Perplexity: "site:zum.de <Thema> Unterrichtsmaterial"

### 4teachers.de
- **URL**: https://www.4teachers.de
- **Aktiv**: ja
- **Fächer**: Alle (Community-Arbeitsblätter)
- **Suchstrategie**: Perplexity: "site:4teachers.de <Fach> <Thema>"

### YouTube Kanäle (Erklärvideos)
- **Aktiv**: ja
- **Kanäle**:
  - Mathe by Daniel Jung (Mathematik)
  - Lehrer Schmidt (Mathematik, Physik)
  - musstewissen (alle Fächer, funk/ARD/ZDF)
  - Simple Club (alle Fächer)
  - Duden Learnattack (alle Fächer)
- **Suchstrategie**: Perplexity: "youtube <Kanal> <Thema>"

### LearningApps
- **URL**: https://learningapps.org
- **Aktiv**: ja
- **Fächer**: Alle (interaktive Übungen, Quiz)
- **Suchstrategie**: WebFetch auf `https://learningapps.org/index.php?s=<Suchbegriff>`

## Konfigurationshinweise

- **`aktiv: ja/nein`** steuert ob das Portal automatisch durchsucht wird
- Lehrer kann Portale aktivieren/deaktivieren je nach vorhandenen Lizenzen
- Login-pflichtige Portale werden nur mit Playwright durchsucht (Lehrer wird gefragt)
- Bei neuen Portalen: URL, Verlag und Suchstrategie eintragen

# Pandas – Fallstudie Shark Attacks

## Lernziele

Nach Bearbeitung dieses Arbeitsblatts kannst du:

- einen komplexen, realen Datensatz selbstständig analysieren
- Datenbereinigung bei unstrukturierten Daten durchführen
- fortgeschrittene Pandas-Techniken anwenden
- aussagekräftige Erkenntnisse aus Daten ableiten

!!! note "Begleitende Infoblätter"
    - [:material-book-open-variant: Pandas Grundlagen](../infoblaetter/pandas-grundlagen.md)
    - [:material-book-open-variant: Pandas Aggregation](../infoblaetter/pandas-aggregation.md)
    - [:material-book-open-variant: Datenbereinigung](../infoblaetter/datenbereinigung.md)

---

## Einführung

Der Global Shark Attack File (GSAF) ist eine Datenbank aller dokumentierten Haiangriffe weltweit. Der Datensatz enthält viele fehlende Werte und unstrukturierte Textdaten – eine realistische Herausforderung!

!!! abstract "Datensatz herunterladen"
    [:material-download: global_shark_attacks.csv](../assets/files/global_shark_attacks.csv){ .md-button }

<div class="notebook-hint" markdown>
<span class="notebook-hint-icon">📓</span>
<div class="notebook-hint-text">
<strong>Bearbeite alle Aufgaben in einem Jupyter Notebook</strong>
<small>Öffne JupyterLite direkt im Browser – keine Installation nötig!</small>
</div>
<a href="https://berndheidemann.github.io/dpa_numpy_pandas_jupyter_site/jupyter/lab/index.html" target="_blank" class="jupyter-button">
🚀 JupyterLite öffnen
</a>
</div>

---

## Aufgaben

### Aufgabe 1 – Daten laden und ersten Überblick gewinnen

Lade den Shark-Attacks-Datensatz und verschaffe dir einen Überblick.

- [ ] Lade den Datensatz `global_shark_attacks.csv` – beachte das Encoding für Sonderzeichen
- [ ] Gib Shape und Spaltennamen aus
- [ ] Zeige die ersten Zeilen an (transponiert für bessere Lesbarkeit)
- [ ] Analysiere Datentypen und fehlende Werte – wie viele NaN-Werte hat jede Spalte?

!!! tip "Hilfe"
    - Laden mit Encoding: `pd.read_csv(pfad, encoding='latin-1')`
    - Transponierte Ansicht: `df.head().T`
    - Fehlende Werte: `df.isnull().sum().sort_values(ascending=False)`
    - Überblick: `df.info()`

!!! question "Reflexionsfrage"
    Welche Spalten haben besonders viele fehlende Werte? Woran könnte das liegen?

---

### Aufgabe 2 – Relevante Spalten auswählen

Der Datensatz hat viele Spalten. Wähle die wichtigsten für die Analyse aus.

- [ ] Liste alle Spaltennamen nummeriert auf
- [ ] Identifiziere relevante Spalten wie: Year, Country, Area, Location, Activity, Name, Sex, Age, Injury, Fatal (Y/N), Time, Species
- [ ] Erstelle einen Arbeits-DataFrame, der nur diese Spalten enthält (verwende `.copy()`)
- [ ] Prüfe, welche Spalten tatsächlich im Datensatz vorhanden sind

!!! tip "Hilfe"
    - Spalten auflisten: `df.columns.tolist()` oder mit enumerate durchlaufen
    - Spalten filtern: `df[liste_der_spalten].copy()`
    - Spalte prüfen: `'Spaltenname' in df.columns`

---

### Aufgabe 3 – Daten bereinigen

Reale Daten sind "messy" – standardisiere und bereinige die wichtigsten Spalten.

**Jahr bereinigen:**

- [ ] Prüfe den Datentyp der Jahr-Spalte
- [ ] Konvertiere zu numerisch – ungültige Werte sollen NaN werden
- [ ] Entferne unrealistische Jahre (vor 1800 oder in der Zukunft)
- [ ] Gib den gültigen Zeitraum und die Anzahl nach Filterung aus

!!! tip "Hilfe"
    - Numerisch konvertieren: `pd.to_numeric(df['Year'], errors='coerce')`
    - Aktuelles Jahr: `datetime.datetime.now().year`
    - Filter: `df[(df['Year'] >= 1800) & (df['Year'] <= aktuelles_jahr)]`

**Fatal (tödlich) bereinigen:**

- [ ] Zeige die vorhandenen Werte in der Fatal-Spalte mit `value_counts(dropna=False)`
- [ ] Standardisiere auf Großbuchstaben und entferne Leerzeichen
- [ ] Mappe 'Y' → True und 'N' → False
- [ ] Prüfe das Ergebnis

!!! tip "Hilfe"
    - Standardisieren: `df['Spalte'].str.upper().str.strip()`
    - Mapping: `df['Spalte'].map({'Y': True, 'N': False})`

**Alter bereinigen:**

- [ ] Konvertiere das Alter zu numerisch
- [ ] Setze unrealistische Werte (< 0 oder > 100) auf NaN
- [ ] Berechne deskriptive Statistiken für das bereinigte Alter

!!! tip "Hilfe"
    - Bedingte Zuweisung: `df.loc[bedingung, 'Spalte'] = np.nan`

**Geschlecht standardisieren:**

- [ ] Zeige die vorhandenen Geschlechts-Werte
- [ ] Standardisiere auf 'Male' und 'Female'
- [ ] Prüfe das Ergebnis

---

### Aufgabe 4 – Deskriptive Statistik

Berechne grundlegende Statistiken zum Datensatz.

- [ ] Ermittle: Gesamtanzahl Angriffe, Zeitraum (frühestes und spätestes Jahr), Anzahl verschiedener Länder
- [ ] Erstelle eine Top-10-Liste der Länder nach Anzahl der Angriffe
- [ ] Berechne, welchen Anteil die Top-10-Länder am Gesamtdatensatz haben
- [ ] Analysiere die häufigsten Aktivitäten (Top 10)
- [ ] Erstelle Altersgruppen (0-10, 11-20, 21-30, usw.) und zähle die Angriffe pro Gruppe

!!! tip "Hilfe"
    - Eindeutige Werte: `df['Spalte'].nunique()`
    - Häufigkeiten: `df['Spalte'].value_counts().head(10)`
    - Kategorien erstellen: `pd.cut(df['Age'], bins=[0, 10, 20, 30, 40, 50, 60, 100], labels=[...])`

---

### Aufgabe 5 – Zeitliche Trends

Analysiere, wie sich Haiangriffe über die Zeit entwickelt haben.

- [ ] Zähle Angriffe pro Jahr mit `groupby`
- [ ] Zeige die letzten 10 Jahre
- [ ] Berechne den Durchschnitt, das Maximum und Minimum für die Jahre ab 2000 – in welchem Jahr gab es die meisten Angriffe?
- [ ] Erstelle eine Dekaden-Spalte (1900, 1910, 1920, ...) 
- [ ] Berechne pro Dekade: Anzahl Angriffe und Tödlichkeitsrate in Prozent

!!! tip "Hilfe"
    - Gruppieren: `df.groupby('Year').size()`
    - Dekade berechnen: `(df['Year'] // 10) * 10`
    - Index des Maximums: `series.idxmax()`
    - Lambda für Prozentwerte: `lambda x: x.mean() * 100`

!!! question "Reflexionsfrage"
    Steigt die Anzahl der Angriffe über die Jahrzehnte? Bedeutet das, dass Haie gefährlicher werden, oder gibt es andere Erklärungen?

---

### Aufgabe 6 – Tödliche Angriffe analysieren

Untersuche die Tödlichkeit von Haiangriffen genauer.

- [ ] Berechne die Gesamt-Tödlichkeitsrate
- [ ] Berechne die Tödlichkeitsrate pro Dekade (ab 1950) – gibt es einen Trend?
- [ ] Erstelle eine Länder-Statistik (mind. 50 Angriffe): Anzahl Angriffe, Anzahl tödlich, Tödlichkeitsrate
- [ ] Sortiere nach Anzahl Angriffe und zeige die Top 10
- [ ] Erstelle eine Aktivitäts-Statistik (mind. 20 Fälle): Welche Aktivitäten sind am gefährlichsten?

!!! tip "Hilfe"
    - Rate bei boolean: `df['Fatal'].mean() * 100` (mean auf True/False gibt Anteil True)
    - Mehrere Aggregationen: `df.groupby('Spalte').agg(Name1=('Spalte1', 'count'), Name2=('Spalte2', 'mean'))`
    - Filtern nach Mindestanzahl: `stats[stats['Anzahl'] >= 50]`

---

## Vertiefende Aufgaben

!!! tip "Optionale Aufgaben zur Vertiefung"
    Die folgenden Aufgaben sind **optional** und vertiefen das Gelernte. Sie eignen sich besonders für:
    
    - **Tiefere Analysen nach Geschlecht, Alter und Ländern**
    - **Komplexe Pivot-Tabellen erstellen**
    - **Prüfungsvorbereitung** durch eigenständiges Arbeiten

---

### Aufgabe 7 – Tiefere Analysen

Führe detailliertere Untersuchungen durch.

**Geschlechtervergleich:**

- [ ] Gruppiere nach Geschlecht und berechne: Anzahl, Durchschnittsalter, Tödlichkeitsrate
- [ ] Berechne den prozentualen Anteil jedes Geschlechts

**Altersanalyse:**

- [ ] Berechne Anzahl und Tödlichkeitsrate pro Altersgruppe
- [ ] Vergleiche das Durchschnittsalter bei tödlichen vs. nicht-tödlichen Angriffen

**Länderprofile:**

- [ ] Erstelle für die Top-5-Länder jeweils ein Profil mit:
    - Anzahl Angriffe
    - Zeitraum (frühester bis spätester Angriff)
    - Tödlichkeitsrate
    - Häufigste Aktivität (Modus)
    - Durchschnittsalter

!!! tip "Hilfe"
    - Modus (häufigster Wert): `df['Spalte'].mode().iloc[0]`
    - Subset erstellen: `df[df['Country'] == land]`

---

### Aufgabe 8 – Pivot-Tabellen erstellen

Nutze Pivot-Tabellen für komplexere Kreuztabellen.

- [ ] Erstelle eine Pivot-Tabelle: Zeilen = Top-5-Länder, Spalten = Dekaden (ab 1950), Werte = Anzahl Angriffe
- [ ] Erstelle eine Pivot-Tabelle: Zeilen = Top-5-Länder, Spalten = Top-5-Aktivitäten, Werte = Tödlichkeitsrate in Prozent

!!! tip "Hilfe"
    - Pivot-Tabelle: `pd.pivot_table(df, values='Spalte', index='Zeilen', columns='Spalten', aggfunc='count', fill_value=0)`
    - Für Prozentwerte: `aggfunc='mean'` und dann `* 100`

---

### Aufgabe 9 – Erkenntnisse dokumentieren

Erstelle eine professionelle Zusammenfassung deiner Analyse.

- [ ] Erstelle einen formatierten Ergebnis-Report mit folgenden Abschnitten:
    - **Datensatz**: Anzahl Angriffe, Zeitraum, Anzahl Länder
    - **Risiko**: Gesamt-Tödlichkeitsrate, gefährlichstes Land, sicherste Aktivität
    - **Demografie**: Durchschnittsalter, Geschlechterverteilung
    - **Trends**: Vergleich der Angriffszahlen zwischen Dekaden
- [ ] Nutze f-Strings für formatierte Ausgaben mit Tausendertrennzeichen und Nachkommastellen

!!! tip "Hilfe"
    - Tausendertrennzeichen: `f"{zahl:,}"`
    - Eine Nachkommastelle: `f"{wert:.1f}"`
    - Prozent: `f"{rate:.1f}%"`

---

## Bonus-Aufgaben

!!! warning "Ohne Hilfe lösen"
    Bearbeite diese Erweiterungen selbstständig.

**A) Hai-Arten analysieren:**

- Extrahiere Hai-Arten aus der Species-Spalte (Textverarbeitung nötig)
- Welche Hai-Art ist am häufigsten dokumentiert?
- Welche Art hat die höchste Tödlichkeitsrate?

**B) Text Mining auf Verletzungen:**

- Analysiere die Injury-Beschreibungen
- Welche Körperteile werden am häufigsten verletzt?
- Nutze String-Methoden wie `str.contains()` um nach Schlüsselwörtern zu suchen

**C) Geographische Hotspots:**

- Gruppiere nach Area/Location innerhalb der Top-Länder
- Gibt es regionale Hotspots?
- Welche Regionen in den USA/Australien sind besonders betroffen?

**D) Korrelationsanalyse:**

- Gibt es einen Zusammenhang zwischen Alter und Tödlichkeit?
- Unterscheidet sich die Tödlichkeitsrate nach Geschlecht signifikant?
- Analysiere, ob bestimmte Aktivitäten bei bestimmten Altersgruppen häufiger vorkommen

---

## Zusammenfassung

!!! success "Das hast du gelernt"
    - **Reale Daten** sind messy – Bereinigung ist essentiell
    - **Encoding-Probleme** mit `encoding='latin-1'` lösen
    - **Typenkonvertierung** mit `pd.to_numeric(errors='coerce')`
    - **Aggregation** mit `groupby` und `pivot_table`
    - **Explorative Analyse** systematisch durchführen
    - **Erkenntnisse** zusammenfassen und interpretieren

---

??? question "Selbstkontrolle"
    1. Warum verwendet man `errors='coerce'` bei der Typkonvertierung?
    2. Wie berechnet man die Tödlichkeitsrate pro Gruppe?
    3. Was bedeutet `dropna=False` bei `value_counts()`?
    4. Wann ist ein Datensatz "sauber genug" für die Analyse?
    
    ??? success "Antworten"
        1. Ungültige Werte werden zu NaN statt einen Fehler zu werfen – wichtig bei unstrukturierten Daten
        2. `.groupby('Gruppe')['Fatal'].mean() * 100` – mean() auf True/False gibt den Anteil True
        3. NaN-Werte werden auch gezählt statt ignoriert – wichtig um fehlende Werte zu sehen
        4. Wenn die verbleibenden Probleme die Analyse nicht verfälschen und die Kernfragen beantwortet werden können – Perfekte Daten gibt es selten!

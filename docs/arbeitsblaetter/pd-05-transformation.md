# Pandas – Transformation & Datenbereinigung

## Lernziele

Nach Bearbeitung dieses Arbeitsblatts kannst du:

- Spalten transformieren mit `map()`, `apply()`, und `applymap()`
- Daten bereinigen: fehlende Werte, Duplikate, Ausreißer
- neue Spalten berechnen und hinzufügen
- Datentypen konvertieren und kategorische Daten erstellen

!!! note "Begleitende Infoblätter"
    - [:material-book-open-variant: Pandas Transformation](../infoblaetter/pandas-transformation.md) – map, apply, applymap
    - [:material-book-open-variant: Datenbereinigung](../infoblaetter/datenbereinigung.md) – Cleaning Pipeline
    
    Lies die Infoblätter **zuerst**, bevor du die Aufgaben bearbeitest. Dort findest du alle Syntax-Beispiele und Erklärungen.

---

## Einführung

Echte Daten sind selten perfekt. Transformation und Bereinigung sind oft die zeitaufwändigsten Schritte der Datenanalyse.

<div class="notebook-hint" markdown>
<span class="notebook-hint-icon">📓</span>
<div class="notebook-hint-text">
<strong>Bearbeite alle Aufgaben in einem Jupyter Notebook</strong>
<small>Öffne JupyterLite direkt im Browser – keine Installation nötig!</small>
</div>
<a href="../jupyter/lab/index.html" target="_blank" class="jupyter-button">
🚀 JupyterLite öffnen
</a>
</div>

**Für dieses Arbeitsblatt verwendest du den MBA-Datensatz (`mba_decisions.csv`).**

!!! abstract "Datensatz herunterladen"
    [:material-download: mba_decisions.csv](../assets/files/mba_decisions.csv){ .md-button }

!!! info "Daten-Pipeline"
    **Rohdaten** → **Bereinigung** (NaN, Duplikate, Ausreißer) → **Transformation** (berechnen, umkodieren, konvertieren) → **Saubere Daten**

---

## Aufgaben

### Aufgabe 1 – Datensatz laden und Probleme identifizieren

Lade den MBA-Datensatz und verschaffe dir einen Überblick über Datenqualitätsprobleme.

- [ ] Lade den MBA-Datensatz (`mba_decisions.csv`) und gib die Shape aus
- [ ] Zeige die Datentypen aller Spalten an
- [ ] Finde heraus, welche Spalten **fehlende Werte** haben und wie viele (absolut und in Prozent)
- [ ] Prüfe, ob der Datensatz **Duplikate** enthält und zeige diese an

!!! tip "Hilfe"
    - Datensatz laden: `pd.read_csv(pfad)`
    - Datentypen und Info: `df.info()`, `df.dtypes`
    - Fehlende Werte: `df.isnull().sum()` für absolute Anzahl
    - Prozent berechnen: `(df.isnull().sum() / len(df) * 100)`
    - Duplikate zählen: `df.duplicated().sum()`
    - Duplikate anzeigen: `df[df.duplicated(keep=False)]`

---

### Aufgabe 2 – Fehlende Werte behandeln

Lerne verschiedene Strategien kennen, um mit fehlenden Werten umzugehen.

- [ ] Erstelle eine Kopie des DataFrames mit `df.copy()`
- [ ] **Strategie 1**: Entferne alle Zeilen mit fehlenden Werten – wie viele Zeilen bleiben übrig?
- [ ] **Strategie 2**: Entferne nur Zeilen, bei denen `GPA` oder `Work_Experience` fehlt
- [ ] **Strategie 3**: Fülle fehlende GPA-Werte mit dem **Mittelwert** der Spalte
- [ ] **Strategie 4**: Fülle fehlende `Work_Experience`-Werte mit dem **Median** (robuster gegen Ausreißer)

!!! tip "Hilfe"
    - Zeilen entfernen: `df.dropna()` oder `df.dropna(subset=['Spalte1', 'Spalte2'])`
    - Mit Mittelwert füllen: `df['Spalte'].fillna(df['Spalte'].mean())`
    - Mit Median füllen: `df['Spalte'].fillna(df['Spalte'].median())`
    - Mit festem Wert füllen: `df['Spalte'].fillna(0)` oder `df['Spalte'].fillna('Unbekannt')`

!!! question "Reflexionsfrage"
    Wann ist der Median besser geeignet als der Mittelwert zum Füllen von Lücken?

---

### Aufgabe 3 – Duplikate entfernen

Lerne, wie du Duplikate erkennst und kontrolliert entfernst.

- [ ] Erstelle eine Kopie des DataFrames
- [ ] Ermittle die Anzahl der Zeilen **vor** dem Entfernen von Duplikaten
- [ ] Entferne alle **vollständigen Duplikate** (alle Spalten identisch)
- [ ] Entferne Duplikate basierend nur auf den Spalten `Gender`, `GPA` und `Work_Experience`
- [ ] Experimentiere mit dem `keep`-Parameter: Was passiert bei `keep='first'`, `keep='last'` und `keep=False`?

!!! tip "Hilfe"
    - Duplikate entfernen: `df.drop_duplicates()`
    - Nur bestimmte Spalten prüfen: `df.drop_duplicates(subset=['Spalte1', 'Spalte2'])`
    - Parameter `keep='first'` behält erstes Vorkommen, `keep='last'` das letzte, `keep=False` entfernt alle

---

### Aufgabe 4 – Neue Spalten berechnen

Erstelle neue Spalten durch Berechnungen und bedingte Logik.

- [ ] Erstelle eine Spalte `GPA_Prozent`, die den GPA als Prozent von 4.0 ausdrückt (gerundet auf 1 Dezimalstelle)
- [ ] Erstelle eine Spalte `High_GPA`, die "Ja" enthält wenn GPA ≥ 3.5, sonst "Nein"
- [ ] Erstelle eine Spalte `GPA_Rating` mit den Kategorien:
    - "Excellent" für GPA ≥ 3.8
    - "Good" für GPA ≥ 3.5
    - "Average" für GPA ≥ 3.0
    - "Below Average" sonst
- [ ] Erstelle eine Spalte `Exp_Kategorie` mit `pd.cut()`, die Work_Experience in die Gruppen "Junior" (0-2), "Mid" (2-5), "Senior" (5-10) und "Expert" (>10) einteilt
- [ ] Erstelle einen gewichteten `Score` aus GPA (60%) und Work_Experience (10%)

!!! tip "Hilfe"
    - Direkte Berechnung: `df['neu'] = df['alt'] * 2`
    - Bedingt (2 Werte): `np.where(df['x'] >= 3.5, 'Ja', 'Nein')`
    - Bedingt (mehrere): `np.select([bed1, bed2, bed3], ['A', 'B', 'C'], default='D')`
    - Kategorien mit Grenzen: `pd.cut(df['Spalte'], bins=[0, 2, 5, 10, np.inf], labels=['A', 'B', 'C', 'D'])`

---

### Aufgabe 5 – map() für Wertersetzung

Verwende `map()` um Werte systematisch zu ersetzen oder umzukodieren.

- [ ] Erstelle ein Dictionary, das die Decision-Werte ins Deutsche übersetzt: Admit→"Aufgenommen", Deny→"Abgelehnt", Waitlist→"Warteliste"
- [ ] Wende das Dictionary mit `map()` an und speichere das Ergebnis in `Decision_DE`
- [ ] Schreibe eine Funktion `gpa_to_grade()`, die einen GPA-Wert in eine Buchstabennote umwandelt (A, B, C, D)
- [ ] Wende diese Funktion mit `map()` auf die GPA-Spalte an
- [ ] Achte darauf, dass die Funktion mit NaN-Werten umgehen kann

!!! tip "Hilfe"
    - Dictionary-Mapping: `df['neu'] = df['alt'].map({'wert1': 'ersatz1', 'wert2': 'ersatz2'})`
    - Funktion-Mapping: `df['neu'] = df['alt'].map(meine_funktion)`
    - NaN prüfen: `if pd.isna(wert): return None`

!!! question "Eigenständige Transformationsübungen"
    Löse ohne Musterlösung:
    
    1. **Mapping**: Erstelle eine Spalte `Decision_Code` die Admit=1, Waitlist=0, Deny=-1 zuordnet
    2. **Berechnung**: Erstelle einen "Composite Score" = (GPA * 10) + (Work_Experience * 2)
    3. **Kategorisierung**: Teile GPA in Quartile ein (Q1, Q2, Q3, Q4) mit `pd.qcut()`
    4. **String-Transformation**: Erstelle eine Spalte mit dem Format "[Gender] Bewerber mit [GPA] GPA"
    5. **Mehrfach-Bedingung**: Erstelle eine "Risk Score" Spalte:
        - 3 wenn GPA < 3.0 UND Experience < 2
        - 2 wenn GPA < 3.2 ODER Experience < 3
        - 1 wenn GPA < 3.5
        - 0 sonst

---

### Aufgabe 6 – apply() für komplexe Transformationen

Verwende `apply()` für Transformationen, die mehrere Spalten oder komplexe Logik erfordern.

- [ ] Verwende `apply()` mit einer Lambda-Funktion, um alle GPA-Werte auf eine Dezimalstelle zu runden
- [ ] Schreibe eine Funktion `create_profile(row)`, die einen Profil-String erzeugt im Format: "Gender, GPA=X.X, Exp=Xy"
- [ ] Wende diese Funktion zeilenweise an (axis=1) und speichere das Ergebnis in einer neuen Spalte `Profile`
- [ ] Schreibe eine Funktion `predict_admission(row)`, die basierend auf GPA, Work_Experience und International einen Score berechnet und "Likely Admit", "Uncertain" oder "Unlikely" zurückgibt
- [ ] Vergleiche deine Vorhersagen mit der tatsächlichen Decision-Spalte (z.B. mit einer Kreuztabelle)

!!! tip "Hilfe"
    - apply auf Spalte: `df['Spalte'].apply(lambda x: x * 2)`
    - apply auf Zeilen: `df.apply(meine_funktion, axis=1)`
    - Auf Zeilenwerte zugreifen: `row['Spaltenname']`
    - Kreuztabelle: `pd.crosstab(df['Spalte1'], df['Spalte2'])`

---

### Aufgabe 7 – Datentypen konvertieren

Konvertiere Datentypen für effizientere Speicherung und korrekte Analysen.

- [ ] Zeige die aktuellen Datentypen aller Spalten an
- [ ] Konvertiere die Spalte `Decision` in den Typ `category`
- [ ] Vergleiche den Speicherverbrauch vor und nach der Konvertierung
- [ ] Erstelle eine **ordinale Kategorie** für Work_Experience mit den Stufen "Low", "Medium", "High" (geordnet!)
- [ ] Überprüfe, ob die Kategorie tatsächlich geordnet ist

!!! tip "Hilfe"
    - Zu Kategorie: `df['Spalte'].astype('category')`
    - Speicherverbrauch: `df['Spalte'].memory_usage()`
    - Ordinale Kategorie: `pd.Categorical(werte, categories=['A', 'B', 'C'], ordered=True)`
    - Ist geordnet? `df['Spalte'].cat.ordered`

---

## Vertiefende Aufgaben

!!! tip "Optionale Aufgaben zur Vertiefung"
    Die folgenden Aufgaben sind **optional** und vertiefen das Gelernte. Sie eignen sich besonders für:
    
    - **String-Bereinigung mit str-Methoden (strip, lower, replace)**
    - **Ausreißer-Behandlung mit der IQR-Methode**
    - **Prüfungsvorbereitung** durch eigenständiges Arbeiten

---

### Aufgabe 8 – Strings bereinigen

Bereinige Text-Daten für konsistente Analysen.

- [ ] Entferne führende und nachfolgende Leerzeichen aus allen String-Spalten
- [ ] Erstelle Varianten der `Gender`-Spalte: Kleinbuchstaben, Großbuchstaben, Title Case
- [ ] Ersetze in der `Major`-Spalte das Zeichen "&" durch "and"
- [ ] Überlege: Welche weiteren String-Bereinigungen könnten bei echten Daten nötig sein?

!!! tip "Hilfe"
    - String-Spalten finden: `df.select_dtypes(include=['object']).columns`
    - Whitespace entfernen: `df['Spalte'].str.strip()`
    - Kleinbuchstaben: `df['Spalte'].str.lower()`
    - Ersetzen: `df['Spalte'].str.replace('alt', 'neu', regex=False)`

---

### Aufgabe 9 – Ausreißer behandeln

Identifiziere und behandle Ausreißer mit verschiedenen Methoden.

- [ ] Berechne für die Spalte `GPA` die Quartile Q1 und Q3 sowie den Interquartilsabstand (IQR)
- [ ] Bestimme die Ausreißer-Grenzen nach der IQR-Methode (Q1 - 1.5×IQR und Q3 + 1.5×IQR)
- [ ] Finde alle Ausreißer und gib deren Anzahl und Werte aus
- [ ] Erstelle eine neue Spalte `GPA_clipped`, in der Ausreißer auf die Grenzen begrenzt werden (Capping)
- [ ] **Bonus**: Berechne für `Work_Experience` den Z-Score und finde Werte mit |Z| > 3

!!! tip "Hilfe"
    - Quartile: `df['Spalte'].quantile(0.25)` für Q1
    - Filter für Ausreißer: `df[(df['Spalte'] < lower) | (df['Spalte'] > upper)]`
    - Capping/Clipping: `df['Spalte'].clip(lower=grenze_unten, upper=grenze_oben)`
    - Z-Score: `(df['Spalte'] - df['Spalte'].mean()) / df['Spalte'].std()`

---

### Aufgabe 10 – Komplette Bereinigungspipeline

Kombiniere alle gelernten Techniken zu einer wiederverwendbaren Bereinigungsfunktion.

- [ ] Schreibe eine Funktion `clean_mba_data(df)`, die folgende Schritte durchführt:
    1. Kopie des DataFrames erstellen
    2. Strings in allen Textspalten trimmen
    3. Fehlende Werte in `GPA` und `Work_Experience` mit dem Median füllen
    4. Duplikate entfernen
    5. GPA-Ausreißer mit Capping behandeln
    6. Eine neue Spalte `GPA_Category` mit den Stufen "Low", "Medium", "High" hinzufügen
    7. Kategorische Spalten (`Gender`, `International`, `Major`, `Decision`) in den Typ `category` konvertieren
- [ ] Wende die Funktion auf den Original-Datensatz an
- [ ] Validiere das Ergebnis: Shape, Datentypen, fehlende Werte

!!! tip "Hilfe"
    - Funktion definieren: `def clean_mba_data(df): ...`
    - Am Ende: `return df`
    - Validierung: `df.info()`, `df.isnull().sum()`, `df.dtypes`

---

### Aufgabe 11 – Komplexe Transformationsaufgaben

!!! warning "Ohne Musterlösung"
    Diese Aufgaben erfordern Kombination mehrerer Transformationstechniken.

**Aufgabe A: Feature Engineering**

- [ ] Erstelle mindestens 5 neue, sinnvolle Features aus den bestehenden Daten:
    - Ein binäres Feature (ja/nein)
    - Ein numerisches abgeleitetes Feature
    - Ein kategorisches Feature mit mehr als 2 Kategorien
    - Ein Interaktions-Feature (Kombination aus 2 Spalten)
    - Ein Ranking-Feature (z.B. GPA-Rang in Prozent)

**Aufgabe B: Datenbereinigung ohne Vorgabe**

- [ ] Implementiere eine vollständige Bereinigungsfunktion für den MBA-Datensatz:
    1. Identifiziere alle Probleme (NaN, Duplikate, Inkonsistenzen)
    2. Dokumentiere, wie viele Datensätze jedes Problem haben
    3. Behebe die Probleme mit geeigneten Strategien
    4. Validiere, dass die Bereinigung erfolgreich war

**Aufgabe C: Transformation mit apply()**

- [ ] Schreibe eine `apply()`-Funktion, die für jeden Bewerber eine "Prediction" macht:
    - Analysiere erst: Was unterscheidet Aufgenommene von Abgelehnten?
    - Entwickle eine Logik mit mindestens 4 Kriterien
    - Wende sie auf alle Zeilen an
    - Berechne die Genauigkeit (% korrekte Vorhersagen)

**Aufgabe D: String-Manipulation**

Wenn der Datensatz Text-Spalten enthält:

- [ ] Bereinige alle Strings (Leerzeichen, Groß-/Kleinschreibung)
- [ ] Extrahiere relevante Informationen aus Text
- [ ] Erstelle Dummy-Variablen aus kategorischen Text-Spalten

**Aufgabe E: Pipeline erstellen**

- [ ] Erstelle eine wiederverwendbare Funktion `prepare_mba_data(filepath)`:
    - Lädt die Daten
    - Bereinigt sie
    - Fügt alle neuen Features hinzu
    - Konvertiert Datentypen
    - Gibt einen sauberen DataFrame zurück
- [ ] Dokumentiere jeden Schritt mit Kommentaren.

---

## Zusammenfassung

!!! success "Das hast du gelernt"
    - **Fehlende Werte**: `dropna()`, `fillna()`, `ffill()`, `bfill()`
    - **Duplikate**: `duplicated()`, `drop_duplicates()`
    - **map()**: Wertersetzung mit Dictionary oder Funktion
    - **apply()**: Komplexe Transformationen (axis=0/1)
    - **Neue Spalten**: Direkte Berechnung, `np.where()`, `np.select()`
    - **Datentypen**: `astype()`, `pd.to_numeric()`, `pd.Categorical()`
    - **Ausreißer**: IQR-Methode, Z-Score, `clip()`

---

??? question "Selbstkontrolle"
    1. Wann verwendest du `map()` vs. `apply()`?
    2. Wie füllst du NaN mit dem Median einer Spalte?
    3. Was macht `df.clip(lower=0, upper=100)`?
    4. Wie erstellst du eine ordinale (geordnete) Kategorie?
    
    ??? success "Antworten"
        1. `map()` für einfache 1:1 Ersetzungen (Dictionary, Funktion auf einzelne Werte); `apply()` für komplexere Logik oder wenn mehrere Spalten nötig sind (axis=1)
        2. `df['col'] = df['col'].fillna(df['col'].median())`
        3. Begrenzt alle Werte auf den Bereich 0-100 (Capping)
        4. `pd.Categorical(values, categories=['A', 'B', 'C'], ordered=True)`

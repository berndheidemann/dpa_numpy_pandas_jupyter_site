# Review der Lernsituation NumPy & Pandas

## Gesamtbewertung

| Kriterium | Bewertung | Kommentar |
|-----------|-----------|-----------|
| Struktur & Aufbau | ⭐⭐⭐⭐⭐ | Exzellent, logische Progression |
| Didaktik | ⭐⭐⭐⭐ | Gut, einzelne Sprünge zu groß |
| Infoblätter | ⭐⭐⭐⭐⭐ | Sehr hochwertig, gutes Nachschlagewerk |
| Praxisbezug | ⭐⭐⭐⭐⭐ | Echte Datensätze, realistische Aufgaben |
| Vollständigkeit | ⭐⭐⭐⭐ | Kernthemen abgedeckt, merge/concat fehlt |
| Konsistenz | ⭐⭐⭐ | Einige Inkonsistenzen bei Variablennamen |

**Fazit:** Die Materialien sind auf **sehr gutem Niveau** und eignen sich hervorragend für den Einstieg in Data Analysis mit Python.

---

## 1. Ablauf und Reihenfolge

### ✓ Stärken

| Bereich | Stärke |
|---------|--------|
| **NumPy-Progression** | Logisch: Grundlagen → Indexierung → Statistik → Filtern → Fallstudie |
| **Pandas-Progression** | Sinnvoll: DataFrames → Datenzugriff → Aggregation → Transformation → Fallstudie |
| **Infoblatt-Verweise** | Jedes Arbeitsblatt verweist auf die passenden Infoblätter |
| **Praxisbezug** | Durchgehend echte Datensätze (Taxi, Games, MBA, Shark Attacks) |

### ⚠ Probleme

**Problem 1: Fehlende Python-Grundlagen-Brücke**  
Die Arbeitsblätter setzen Python-Kenntnisse voraus (List Comprehensions, Funktionen, Dictionaries), ohne diese explizit zu erwähnen.

> **Empfehlung:** In `np-01-einfuehrung.md` einen Abschnitt "Voraussetzungen" ergänzen:
> ```markdown
> !!! info "Voraussetzungen"
>     - Python-Grundlagen (Variablen, Schleifen, Bedingungen)
>     - List Comprehensions (`[x*2 for x in liste]`)
>     - Funktionen und Lambda-Ausdrücke
> ```

**Problem 2: Übergang NumPy → Pandas könnte expliziter sein**  
Die Verbindung zwischen den beiden Themenblöcken ist nicht deutlich.

> **Empfehlung:** Am Ende von `np-05-fallstudie.md` eine Überleitung ergänzen:
> ```markdown
> ## Ausblick: Pandas
> NumPy ist mächtig für numerische Daten, hat aber Grenzen:
> - Keine Spaltennamen (nur Indizes)
> - Alle Daten müssen gleichen Typ haben
> - Keine einfache CSV-Handhabung mit gemischten Typen
> 
> → Pandas löst diese Probleme und nutzt NumPy als Basis!
> ```

---

## 2. Komplexitätssprünge

### Kritische Stellen

| Arbeitsblatt | Aufgabe | Problem | Empfehlung |
|--------------|---------|---------|------------|
| **np-02-indexierung.md** | Aufgabe 9C | Division durch 0 ohne `np.isinf()` Vorwissen | Hinweis zu `np.isinf()` ergänzen |
| **np-04-filtern.md** | Aufgabe 7 | Verschachteltes `np.where()` ohne Zwischenschritt | Aufteilen in 7a (2 Kategorien) und 7b (3+ Kategorien) |
| **pd-04-transformation.md** | Aufgabe 5 | `np.select()` ohne ausreichende Erklärung | Syntax-Beispiel in Hilfe-Box |

### Detaillierte Empfehlungen

**np-02, Aufgabe 9C:**
```markdown
!!! tip "Nützlich für Aufgabe C"
    Bei Division können `inf` (Infinity) Werte entstehen. 
    Prüfe mit `np.isinf(arr)` und kombiniere mit `np.isnan(arr)`.
```

**np-04, Aufgabe 7:**
```markdown
### Aufgabe 7a – Einfache Kategorisierung
- [ ] Teile Fahrten in "kurz" (<5 Meilen) und "lang" (≥5 Meilen) ein

### Aufgabe 7b – Drei Kategorien
- [ ] Erweitere auf "kurz", "mittel", "lang" mit verschachteltem np.where()
```

**pd-04, Aufgabe 5:**
```markdown
!!! tip "Hilfe für np.select()"
    Syntax: `np.select([bed1, bed2, bed3], ['A', 'B', 'C'], default='D')`
    - Liste von Bedingungen (in Reihenfolge geprüft!)
    - Liste von Werten (gleiche Länge)
    - default für alle anderen Fälle
```

---

## 3. Erklärungen und Hilfestellungen

### ✓ Stärken

- **Hilfe-Boxen** durchgehend vorhanden und hilfreich
- **Reflexionsfragen** fördern Verständnis (z.B. "Warum ist NumPy schneller?")
- **Selbstkontrollen** am Ende jedes Arbeitsblatts sind exzellent
- **Visualisierungen** (Mermaid, PlantUML) in Infoblättern sehr gut

### ⚠ Fehlende Hilfe

**np-03-statistik.md, Aufgabe 7:**
```markdown
# AKTUELL: Keine Hilfe für Quartile
# EMPFEHLUNG:
!!! tip "Hilfe"
    - Quartile: `np.nanpercentile(arr, [25, 50, 75])` gibt alle drei auf einmal
    - IQR = Q3 - Q1
```

**pd-03-aggregation.md: Named Aggregation Syntax**
```markdown
!!! warning "Häufiger Fehler bei Named Aggregation"
    ```python
    # FALSCH (Tupel ohne Klammern)
    df.groupby('A').agg(summe='B', 'sum')
    
    # RICHTIG
    df.groupby('A').agg(summe=('B', 'sum'))
    ```
```

---

## 4. Konsistenz

### ⚠ Inkonsistenzen

**Variablennamen gemischt:**

| Arbeitsblatt | Variablennamen |
|--------------|----------------|
| np-04-filtern.md | `passagiere`, `strecke`, `fahrpreis` (deutsch) |
| np-02-indexierung.md | `trip_distance`, `fare_amount` (englisch) |

> **Empfehlung:** Einheitlich entweder deutsche ODER englische Variablennamen verwenden.

**Spaltenindex-Dokumentation:**
- `payment_type` Index 17 nur in np-04 erwähnt, nicht in np-02 oder np-03

> **Empfehlung:** In allen NumPy-Arbeitsblättern die gleiche vollständige Spaltentabelle verwenden.

**NaN-Behandlung:**
- In np-02 Aufgabe 1 wird `np.isnan()` erwähnt
- Erst in np-03 werden `nanmean()` etc. eingeführt
- In np-02 wird aber schon mit den Daten gerechnet

> **Empfehlung:** In np-02 entweder NaN-Handling bereits einführen oder explizit sagen "Ignoriere NaN-Werte vorerst".

---

## 5. Vollständigkeit

### ✓ Abgedeckte Themen

| NumPy | Pandas |
|-------|--------|
| ✓ Array-Erstellung | ✓ DataFrame/Series |
| ✓ Indexierung/Slicing | ✓ loc/iloc |
| ✓ Statistik | ✓ groupby/agg |
| ✓ Broadcasting | ✓ pivot_table |
| ✓ Boolean Indexing | ✓ Transformation |
| ✓ np.where() | ✓ Datenbereinigung |

### ⚠ Fehlende wichtige Themen

**NumPy:**
- `np.concatenate()` / `np.vstack()` / `np.hstack()` – Arrays zusammenfügen
- `np.unique()` – für Kategorien

> **Empfehlung:** In `numpy-funktionen.md` ergänzen:
> ```markdown
> ## Arrays kombinieren
> | Funktion | Beschreibung |
> |----------|--------------|
> | `np.concatenate([a, b])` | Verketten entlang Achse |
> | `np.vstack([a, b])` | Vertikal stapeln |
> | `np.hstack([a, b])` | Horizontal stapeln |
> | `np.unique(arr)` | Eindeutige Werte |
> ```

**Pandas (HOCH PRIORITÄR):**
- `pd.merge()` / `pd.concat()` – DataFrames verbinden fehlt komplett
- Zeitreihen-Basics – `dt` Accessor wird nur kurz erwähnt

> **Empfehlung:** Neues Arbeitsblatt `pd-03b-verbinden.md` ODER Integration in pd-04.

---

## 6. Infoblätter-Qualität

| Infoblatt | Bewertung | Bemerkung |
|-----------|-----------|-----------|
| statistik-grundlagen.md | ⭐⭐⭐⭐⭐ | Exzellent mit Formeln, Visualisierungen, Praxisbeispielen |
| numpy-indexierung.md | ⭐⭐⭐⭐⭐ | Sehr gut mit Tabellen und View/Copy-Erklärung |
| pandas-datenzugriff.md | ⭐⭐⭐⭐ | Gute Übersicht loc/iloc |
| numpy-broadcasting.md | ⭐⭐⭐⭐ | Gute Visualisierungen |
| datenbereinigung.md | ⭐⭐⭐⭐ | Praktische Checkliste |

### Ergänzungsvorschläge

**numpy-grundlagen.md:** `np.random.choice()` fehlt
```markdown
# Zufallsauswahl
auswahl = np.random.choice(['A', 'B', 'C'], size=10)
gewichtet = np.random.choice([1, 2, 3], size=10, p=[0.5, 0.3, 0.2])
```

**pandas-aggregation.md:** `groupby.filter()` fehlt
```markdown
## Gruppen filtern
# Nur Gruppen mit mind. 3 Einträgen behalten
df.groupby('Kategorie').filter(lambda x: len(x) >= 3)
```

---

## 7. Bilder-Referenzen prüfen

Folgende Bilder werden referenziert – existieren sie?

- [ ] `../assets/images/statistik-intro.png`
- [ ] `../assets/images/warumDatenVerdichten.png`
- [ ] `../assets/images/median.png`

> **Aktion:** Prüfen und ggf. erstellen oder Referenzen entfernen.

---

## 8. Priorisierte Empfehlungen

### 🔴 Hohe Priorität

| # | Empfehlung | Betroffene Dateien |
|---|------------|-------------------|
| 1 | **pd.merge()/pd.concat() ergänzen** – wichtiges fehlendes Thema | Neues Arbeitsblatt oder pd-04 |
| 2 | **Spaltenindizes konsistent dokumentieren** – Taxi-Datensatz in allen np-Blättern gleich | np-02, np-03, np-04 |
| 3 | **Komplexitätssprünge abmildern** – np-04 Aufgabe 7, pd-04 Aufgabe 5 | np-04, pd-04 |

### 🟡 Mittlere Priorität

| # | Empfehlung | Betroffene Dateien |
|---|------------|-------------------|
| 4 | **Variablennamen vereinheitlichen** – deutsch oder englisch | Alle np-Arbeitsblätter |
| 5 | **Bilder prüfen** – gebrochene Referenzen | statistik-grundlagen.md, pandas-aggregation.md |
| 6 | **Übergang NumPy → Pandas** – Ausblick am Ende | np-05-fallstudie.md |

### 🟢 Niedrige Priorität

| # | Empfehlung | Betroffene Dateien |
|---|------------|-------------------|
| 7 | np.concatenate/vstack/hstack ins Infoblatt | numpy-funktionen.md |
| 8 | groupby.filter() ins Aggregation-Infoblatt | pandas-aggregation.md |
| 9 | Voraussetzungen-Box am Anfang | np-01-einfuehrung.md |

---

## Anhang: Student-Datensatz Spaltenindizes

Für np-05 fehlen die numerischen Spaltenindizes:

| Spalte | Index | Beschreibung |
|--------|-------|--------------|
| age | 2 | Alter |
| Medu | 4 | Bildung Mutter |
| Fedu | 5 | Bildung Vater |
| traveltime | 12 | Pendelzeit |
| studytime | 13 | Lernzeit |
| failures | 14 | Klassenwiederholungen |
| famrel | 23 | Familienbeziehung |
| freetime | 24 | Freizeit |
| goout | 25 | Ausgehen |
| Dalc | 26 | Alkohol werktags |
| Walc | 27 | Alkohol Wochenende |
| health | 28 | Gesundheit |
| absences | 29 | Fehlstunden |
| G1 | 30 | Note 1. Periode |
| G2 | 31 | Note 2. Periode |
| G3 | 32 | Abschlussnote |

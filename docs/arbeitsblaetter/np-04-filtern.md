# NumPy – Filtern & Vektorisierung

## Lernziele

Nach Bearbeitung dieses Arbeitsblatts kannst du:

- Boolean Indexing für komplexe Filter anwenden
- mehrere Bedingungen mit logischen Operatoren kombinieren
- vektorisierte Berechnungen statt Schleifen nutzen
- effiziente Datenmanipulationen durchführen

!!! note "Begleitende Infoblätter"
    - [:material-book-open-variant: NumPy Indexierung](../infoblaetter/numpy-indexierung.md) – Boolean Indexing
    - [:material-book-open-variant: NumPy Broadcasting](../infoblaetter/numpy-broadcasting.md) – Vektorisierung
    
    Lies die Infoblätter **zuerst**, bevor du die Aufgaben bearbeitest. Dort findest du alle Syntax-Beispiele und Erklärungen.

---

## Einführung

Boolean Indexing ist eine der mächtigsten Techniken in NumPy. Statt Schleifen nutzt du Bedingungen direkt auf Arrays.

```kroki-plantuml
@startuml
!theme plain
skinparam backgroundColor transparent

rectangle "Traditionelle Schleife" as loop #lightcoral {
    rectangle "for x in daten:\n    if x > 5:\n        ergebnis.append(x)" as l1
}

rectangle "Boolean Indexing" as bool #lightgreen {
    rectangle "ergebnis = daten[daten > 5]" as b1
}

loop --> bool : "Viel kürzer\nund schneller!"
@enduml
```

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

**Spaltenübersicht für den Taxi-Datensatz:**

| Spalte | Index | Beschreibung |
|--------|-------|--------------|
| VendorID | 0 | Anbieter-ID |
| lpep_pickup_datetime | 1 | Startzeit |
| lpep_dropoff_datetime | 2 | Endzeit |
| passenger_count | 7 | Anzahl Passagiere |
| trip_distance | 8 | Strecke (Meilen) |
| fare_amount | 9 | Fahrpreis ($) |
| tip_amount | 12 | Trinkgeld ($) |
| total_amount | 16 | Gesamtbetrag ($) |
| payment_type | 17 | Zahlungsart (1=Kreditkarte, 2=Bar) |

!!! abstract "Datensatz herunterladen"
    [:material-download: taxi_tripdata.csv](../assets/files/taxi_tripdata.csv){ .md-button }

---

## Aufgaben

### Aufgabe 1 – Daten vorbereiten

Lade die Taxi-Daten und extrahiere die relevanten Spalten für die Analyse.

- [ ] Lade die Datei `taxi_tripdata.csv` mit `np.genfromtxt()` und nutze `skip_header=1`
- [ ] Extrahiere die Spalten `passenger_count`, `trip_distance`, `fare_amount`, `tip_amount` und `total_amount` in separate Variablen
- [ ] Gib die Anzahl der Fahrten aus

!!! tip "Hilfe"
    - Datei laden: `np.genfromtxt(pfad, delimiter=',', skip_header=1)`
    - Spalte extrahieren: `array[:, spalten_index]`
    - Länge eines Arrays: `len(array)`

---

### Aufgabe 2 – Grundlagen Boolean Indexing

Verstehe, wie Boolean Indexing funktioniert.

- [ ] Erstelle eine Bedingung für Fahrten mit mehr als 5 Meilen und speichere sie in einer Variable `bedingung`
- [ ] Gib die ersten 10 Werte der Bedingung aus – was siehst du?
- [ ] Zähle, wie viele `True`-Werte die Bedingung enthält
- [ ] Verwende die Bedingung als Index, um alle langen Fahrten zu filtern
- [ ] Berechne die Durchschnittsstrecke der gefilterten Fahrten

!!! tip "Hilfe"
    - Bedingung erstellen: `bedingung = array > 5` → erzeugt Boolean-Array
    - True-Werte zählen: `bedingung.sum()`
    - Filtern: `array[bedingung]` oder direkt `array[array > 5]`

---

### Aufgabe 3 – Verschiedene Vergleichsoperatoren

Teste alle Vergleichsoperatoren auf den Taxi-Daten.

- [ ] Zähle Fahrten mit mehr als 10 Meilen Strecke
- [ ] Zähle Fahrten mit mindestens 10 Meilen Strecke
- [ ] Zähle Fahrten unter 1 Meile
- [ ] Zähle Fahrten mit exakt 0 Meilen
- [ ] Zähle Fahrten mit genau 1 Passagier und berechne deren Anteil an allen Fahrten

!!! tip "Hilfe"
    - Vergleichsoperatoren: `>`, `>=`, `<`, `<=`, `==`, `!=`
    - Zählen: `(array > 5).sum()`
    - Anteil berechnen: `anzahl / gesamt * 100`

---

### Aufgabe 4 – Mehrere Bedingungen kombinieren

!!! warning "Wichtig: Operatoren und Klammern"
    - Verwende `&` (und), `|` (oder), `~` (nicht)
    - **Nicht** `and`, `or`, `not`
    - Jede Bedingung muss in Klammern stehen!

Kombiniere mehrere Bedingungen für komplexe Filter.

- [ ] Finde Fahrten mit mehr als 2 Passagieren **UND** Strecke unter 2 Meilen
- [ ] Finde sehr kurze (< 0.5 Meilen) **ODER** sehr lange Fahrten (> 20 Meilen)
- [ ] Finde Fahrten mit Fahrpreis zwischen $10 und $20 (Bereichsfilter)
- [ ] Finde alle Fahrten **AUSSER** solchen mit 0 Passagieren (Negation)

!!! tip "Hilfe"
    - UND-Verknüpfung: `(bed1) & (bed2)`
    - ODER-Verknüpfung: `(bed1) | (bed2)`
    - Negation: `~(bedingung)`
    - Bereich: `(arr >= 10) & (arr <= 20)`

!!! question "Eigenständige Filteraufgaben"
    Löse diese Aufgaben ohne Musterlösung:
    
    1. **Preiskategorien**: Finde alle Fahrten mit einem Preis zwischen $20 und $50
    2. **Mehrfachbedingung**: Fahrten mit >3 Passagieren UND Strecke >5 Meilen UND Preis <$30
    3. **Ausschluss**: Alle Fahrten AUßER solchen mit 0 oder NaN Passagieren
    4. **Extreme kombinieren**: Sehr kurze (<0.5 Meilen) ODER sehr teure (>$100) Fahrten
    5. **Dreier-Kombination**: Fahrten mit (Trinkgeld >$5) ODER (Strecke >10 Meilen UND Preis <$30)
    
    Zähle jeweils die Anzahl und berechne den Durchschnittspreis der gefilterten Fahrten.

---

### Aufgabe 5 – Filter auf Datensätze anwenden

Filtere den gesamten Datensatz (alle Spalten) basierend auf einer Bedingung.

- [ ] Erstelle eine Maske für Fahrten über 5 Meilen
- [ ] Wende die Maske auf den gesamten Datensatz an (nicht nur eine Spalte)
- [ ] Gib die Shape vor und nach dem Filtern aus
- [ ] Berechne für die gefilterten langen Fahrten: Durchschnittspreis und Durchschnitt-Trinkgeld
- [ ] Vergleiche diese Werte mit dem Durchschnitt aller Fahrten
- [ ] Zähle Fahrten mit genau 0 Passagieren – was könnten das für Daten sein?

!!! tip "Hilfe"
    - Maske auf Datensatz anwenden: `daten[maske]` filtert Zeilen
    - Spalte aus gefiltertem Datensatz: `gefilterter_datensatz[:, spalten_index]`
    - Shape prüfen: `array.shape`

---

### Aufgabe 6 – Vektorisierte Berechnungen

Führe Berechnungen auf ganzen Arrays durch – ohne Schleifen!

- [ ] Berechne für jede Fahrt den **Preis pro Meile** (Division zweier Spalten)
- [ ] Entferne ungültige Werte (NaN und Infinity) aus dem Ergebnis
- [ ] Berechne Durchschnitt und Median des Preises pro Meile
- [ ] Erstelle eine Kopie der Fahrpreise und erhöhe alle Preise um 10%
- [ ] Berechne den **Trinkgeld-Anteil** in Prozent (Trinkgeld / Fahrpreis * 100)

!!! tip "Hilfe"
    - Vektorisierte Division: `spalte1 / spalte2`
    - Kopie erstellen: `array.copy()`
    - NaN prüfen: `np.isnan(arr)`
    - Infinity prüfen: `np.isinf(arr)`
    - Kombinierte Prüfung: `gueltig = ~np.isnan(arr) & ~np.isinf(arr)`

---

## Vertiefende Aufgaben

!!! tip "Optionale Aufgaben zur Vertiefung"
    Die folgenden Aufgaben sind **optional** und vertiefen das Gelernte. Sie eignen sich besonders für:
    
    - **np.where() für bedingte Wertzuweisung**
    - **Kombination von Filtern mit Berechnungen**
    - **Eigenständige Praxisaufgaben**
    - **Prüfungsvorbereitung** durch eigenständiges Arbeiten

---

### Aufgabe 7 – np.where() für bedingte Berechnungen

`np.where(bedingung, wenn_true, wenn_false)` ermöglicht bedingte Wertzuweisungen.

**7a) Einfache Kategorisierung (2 Kategorien):**

- [ ] Kategorisiere alle Fahrten nach Strecke: "kurz" (< 5 Meilen), "lang" (≥ 5 Meilen)
- [ ] Zähle, wie viele Fahrten in jeder Kategorie sind
- [ ] Berechne einen Rabatt: 10% bei Preisen über $30, sonst 5%

!!! tip "Hilfe für 7a"
    - Einfache Kategorisierung: `np.where(strecke < 5, 'kurz', 'lang')`
    - Zählen einer Kategorie: `(kategorie == 'kurz').sum()`

**7b) Erweiterte Kategorisierung (3+ Kategorien):**

- [ ] Kategorisiere Fahrten dreistufig: "kurz" (< 2), "mittel" (2-10), "lang" (> 10)
- [ ] Korrigiere Datenfehler: Ersetze alle negativen Fahrpreise durch 0

!!! tip "Hilfe"
    - Einfache Kategorisierung: `np.where(bed, 'ja', 'nein')`
    - Verschachtelt: `np.where(bed1, 'A', np.where(bed2, 'B', 'C'))`
    - Zählen einer Kategorie: `(kategorie == 'kurz').sum()`
    - Werte ersetzen: `np.where(arr < 0, 0, arr)`

---

### Aufgabe 8 – Praktische Analysen

Wende alles Gelernte für echte Analysen an.

- [ ] **Zahlungsarten-Vergleich**: Vergleiche Kreditkarten-Zahlungen (Spalte 17 == 1) mit Bar-Zahlungen (== 2) – wie unterscheidet sich das durchschnittliche Trinkgeld?
- [ ] **Ausreißer finden**: Finde Fahrpreise, die mehr als 3 Standardabweichungen vom Mittelwert entfernt sind (nach oben und unten)
- [ ] **Effizienzanalyse**: Berechne für jede Fahrt den "Umsatz pro Meile" und finde die Top 10% effizientesten Fahrten (nutze `np.nanpercentile()`)

!!! tip "Hilfe"
    - Ausreißer-Grenze: `mean + 3 * std` bzw. `mean - 3 * std`
    - Standardabweichung: `np.nanstd(arr)`
    - Perzentil berechnen: `np.nanpercentile(arr, 90)` für das 90. Perzentil
    - Infinity-Werte bei Perzentil ausschließen: erst filtern, dann Perzentil berechnen

---

### Aufgabe 9 – Komplexe Praxisaufgaben

!!! warning "Ohne Musterlösung"
    Diese Aufgaben erfordern Kombination mehrerer Techniken.

**Aufgabe A: Datenqualitätsprüfung**

Identifiziere "verdächtige" Fahrten und zähle sie:

- [ ] Strecke = 0 aber Preis > $5
- [ ] Strecke > 0 aber Preis = 0
- [ ] Trinkgeld > Fahrpreis
- [ ] Gesamtbetrag < Fahrpreis
- [ ] Negative Werte in irgendeiner Preisspalte
- [ ] Wie viel Prozent der Daten sind "verdächtig"?

**Aufgabe B: Kundensegmentierung**

Kategorisiere Fahrten in 4 Segmente und berechne für jedes Segment die Durchschnittswerte:

- [ ] **Basic**: Kurze Strecke (<2 Meilen), niedriger Preis (<$15)
- [ ] **Standard**: Mittlere Strecke (2-5 Meilen), mittlerer Preis ($15-$30)
- [ ] **Premium**: Lange Strecke (>5 Meilen) ODER hoher Preis (>$30)
- [ ] **VIP**: Lange Strecke (>5 Meilen) UND hoher Preis (>$30)

Hinweis: Nutze `np.where()` für die Kategorisierung.

**Aufgabe C: Zeitabhängige Analyse**

- [ ] Teile die Daten in 4 gleich große Teile (entspricht grob Tagesquartalen)
- [ ] Vergleiche für jeden Teil:
    - Durchschnittlicher Fahrpreis
    - Durchschnittliches Trinkgeld
    - Anteil der Fahrten mit Trinkgeld
- [ ] Gibt es Muster?

**Aufgabe D: Effizienzranking**

- [ ] Berechne für jede Fahrt den "Umsatz pro Meile"
- [ ] Filtere nur gültige Werte (keine NaN, keine Infinity, keine negativen Werte)
- [ ] Finde die Top-100 und Bottom-100 Fahrten
- [ ] Was unterscheidet diese Gruppen? (Analysiere Passagierzahl, Strecke, etc.)

**Aufgabe E: Anomalie-Erkennung**

Implementiere einen Anomalie-Detektor:

- [ ] Ein Datenpunkt ist eine Anomalie, wenn mindestens 2 seiner Werte (Strecke, Preis, Gesamt) mehr als 3 Standardabweichungen vom Mittelwert entfernt sind
- [ ] Zähle und analysiere diese Anomalien
- [ ] Sollten sie entfernt werden? Begründe!

---

## Zusammenfassung

!!! success "Das hast du gelernt"
    - **Boolean Indexing**: `arr[arr > 5]` filtert direkt
    - **Operatoren**: `&` (und), `|` (oder), `~` (nicht) + Klammern!
    - **Vektorisierung**: Operationen auf ganze Arrays statt Schleifen
    - **np.where()**: Bedingte Wertzuweisungen
    - **Komplexe Filter**: Kombiniere Bedingungen für mächtige Abfragen

---

??? question "Selbstkontrolle"
    1. Was ist falsch an `arr[arr > 5 and arr < 10]`?
    2. Wie filterst du alle Werte, die NICHT zwischen 5 und 10 liegen?
    3. Was macht `np.where(arr > 0, arr, 0)`?
    4. Warum ist `arr * 2` schneller als `[x * 2 for x in arr]`?
    
    ??? success "Antworten"
        1. Man muss `&` statt `and` verwenden und Klammern setzen: `arr[(arr > 5) & (arr < 10)]`
        2. `arr[(arr < 5) | (arr > 10)]` oder `arr[~((arr >= 5) & (arr <= 10))]`
        3. Ersetzt negative Werte durch 0, positive bleiben erhalten
        4. NumPy nutzt optimierte C-Routinen und verarbeitet alle Werte parallel

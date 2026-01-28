# Python – Listen

## Lernziele

Nach Bearbeitung dieses Arbeitsblatts kannst du:

- Listen erstellen, bearbeiten und durchsuchen
- List-Slicing für Teilbereiche anwenden
- List Comprehensions für kompakte Transformationen nutzen
- Verschachtelte Listen (2D-Daten) verarbeiten

!!! note "Begleitendes Infoblatt"
    [:material-book-open-variant: Listen](../infoblaetter/listen.md) – Methoden, Slicing, Comprehensions, Tuple

---

## Einführung

Listen sind das Arbeitstier der Datenanalyse in Python. Bevor du pandas und numpy kennenlernst, solltest du sicher mit nativen Listen umgehen können.

```python
# Grundlegende Listen-Operationen
daten = [1, 2, 3, 4, 5]
daten.append(6)        # Hinzufügen
daten.remove(3)        # Entfernen
print(daten[0])        # Zugriff: 1
print(daten[-1])       # Letztes Element: 6
print(daten[1:4])      # Slicing: [2, 4, 5]
```

---

## Aufgaben

### Aufgabe 1 – Verkaufsdaten bereinigen

Rohdaten enthalten oft ungültige Werte, die vor der Analyse entfernt werden müssen.

- [ ] **Erstelle `daten_bereinigung.py`:**

    Gegeben:
    ```python
    tagesumsaetze = [1200, 1500, -50, 1800, 99999, 1400, 1600, -100, 1750]
    ```

    Implementiere folgende Funktionen:

    1. **`remove_invalid_values(data)`**
        - Entferne negative Werte (Fehleingaben)
        - Entferne Werte > 10.000 (offensichtliche Ausreißer)
        - Gib die bereinigte Liste zurück

    2. **`get_statistics(data)`**
        - Berechne Summe, Durchschnitt, Min, Max
        - Gib ein Dictionary mit den Ergebnissen zurück

    3. **`normalize_data(data)`**
        - Skaliere alle Werte auf einen Bereich von 0–100
        - Formel: $norm = \frac{wert - min}{max - min} \times 100$

    Test:
    ```python
    sauber = remove_invalid_values(tagesumsaetze)
    print(sauber)  # [1200, 1500, 1800, 1400, 1600, 1750]
    
    stats = get_statistics(sauber)
    print(stats)  # {"summe": 9250, "durchschnitt": 1541.67, ...}
    
    normalisiert = normalize_data(sauber)
    print(normalisiert)  # [0.0, 50.0, 100.0, 33.33, 66.67, 91.67]
    ```

---

### Aufgabe 2 – Aktienkurs-Analyse

Zeitreihenanalyse ist ein Kernthema für Data Analysten.

- [ ] **Erstelle `aktienkurs.py`:**

    Gegeben sind die Schlusskurse einer Aktie über 20 Handelstage:
    ```python
    kurse = [100, 102, 101, 105, 108, 107, 110, 112, 111, 115,
             118, 116, 119, 122, 120, 125, 128, 127, 130, 133]
    ```

    Implementiere:

    1. **Tägliche Veränderung berechnen**
        - Erstelle eine Liste mit den Differenzen zum Vortag
        - Der erste Tag hat keine Veränderung (0 oder auslassen)

    2. **Beste und schlechteste Tage finden**
        - Finde den Tag mit dem größten Gewinn
        - Finde den Tag mit dem größten Verlust
        - Gib jeweils Tag-Nummer und Wert aus

    3. **Gleitender Durchschnitt (Moving Average)**
        - Berechne den 5-Tage-Moving-Average
        - Für Tag i: Durchschnitt von Tag i-4 bis i (inklusive)
        - Die ersten 4 Tage haben keinen MA

    4. **Längste Gewinnsträhne**
        - Ermittle die längste Folge von aufeinanderfolgenden positiven Tagen

    !!! tip "Slicing nutzen"
        ```python
        # Gleitender Durchschnitt
        for i in range(4, len(kurse)):
            fenster = kurse[i-4:i+1]  # 5 Werte
            ma = sum(fenster) / len(fenster)
        ```

---

### Aufgabe 3 – Sensordaten-Matrix (2D-Listen)

IoT-Sensoren liefern mehrdimensionale Daten.

- [ ] **Erstelle `sensordaten.py`:**

    Gegeben: Messwerte von 5 Sensoren über 7 Tage
    ```python
    sensordaten = [
        [22, 24, 19, 23, 25, 20, 21],  # Sensor 0
        [18, 22, 21, 25, 26, 24, 19],  # Sensor 1
        [20, 23, 22, 27, 24, 22, 18],  # Sensor 2
        [19, 21, 24, 26, 25, 23, 20],  # Sensor 3
        [23, 25, 27, 26, 22, 24, 21]   # Sensor 4
    ]
    ```

    Implementiere:

    1. **`sensor_average(data, sensor_id)`**
        - Berechne den Durchschnitt eines bestimmten Sensors

    2. **`day_maximum(data, day)`**
        - Finde den höchsten Wert aller Sensoren an einem Tag

    3. **`find_anomalies(data, threshold)`**
        - Finde alle Werte, die mehr als `threshold` vom Sensor-Durchschnitt abweichen
        - Gib Liste von Tupeln zurück: `[(sensor, tag, wert, abweichung), ...]`

    4. **`transpose_matrix(data)`**
        - Wandle Zeilen in Spalten um (Sensoren ↔ Tage)
        - Aus 5×7 wird 7×5

    Test:
    ```python
    print(sensor_average(sensordaten, 0))  # 22.0
    print(day_maximum(sensordaten, 3))     # 27 (Sensor 2, Tag 3)
    
    anomalien = find_anomalies(sensordaten, 3)
    # [(2, 3, 27, 4.29), ...] # Sensor 2, Tag 3, Wert 27, Abweichung 4.29
    ```

---

### Aufgabe 4 – Log-Daten filtern mit List Comprehensions

List Comprehensions sind mächtig und kompakt.

- [ ] **Erstelle `list_comprehensions.py`:**

    Gegeben sind Server-Response-Zeiten in Millisekunden:
    ```python
    response_times = [45, 120, 89, 234, 56, 890, 34, 167, 2100, 78, 445, 92]
    ```

    Nutze **List Comprehensions** für:

    1. **Schnelle Requests** (< 100ms)
        ```python
        schnell = [???]
        # [45, 89, 56, 34, 78, 92]
        ```

    2. **Langsame Requests** (> 500ms)
        ```python
        langsam = [???]
        # [890, 2100]
        ```

    3. **Kategorisierte Liste**
        ```python
        kategorisiert = [???]
        # [("schnell", 45), ("normal", 120), ("schnell", 89), ...]
        ```
        Kategorien: < 100 = "schnell", 100-500 = "normal", > 500 = "langsam"

    4. **Prozentuale Abweichung vom Durchschnitt**
        ```python
        durchschnitt = sum(response_times) / len(response_times)
        abweichungen = [???]
        # [("45ms", -85.2%), ("120ms", -61.3%), ...]
        ```

---

### Aufgabe 5 – Kundenanalyse mit verschachtelten Listen

CRM-Daten liegen oft als Listen von Listen vor.

- [ ] **Erstelle `kundenanalyse.py`:**

    Gegeben:
    ```python
    kunden = [
        ["K001", "Müller", 2019, 4500.00],
        ["K002", "Schmidt", 2021, 2300.00],
        ["K003", "Weber", 2018, 8900.00],
        ["K004", "Fischer", 2020, 1200.00],
        ["K005", "Meyer", 2017, 12500.00],
        # [ID, Name, Kunde_seit, Jahresumsatz]
    ]
    ```

    Implementiere:

    1. **Nach Jahresumsatz sortieren (absteigend)**
        ```python
        sortiert = sorted(kunden, key=lambda k: ???, reverse=True)
        ```

    2. **Kunden vor 2020 finden**
        ```python
        alte_kunden = [k for k in kunden if ???]
        # [["K001", ...], ["K003", ...], ["K005", ...]]
        ```

    3. **Gesamtumsatz aller Kunden**
        ```python
        gesamt = sum(???)
        ```

    4. **Neue Liste: nur ID und Umsatz**
        ```python
        id_umsatz = [[k[0], k[3]] for k in kunden]
        # [["K001", 4500.00], ["K002", 2300.00], ...]
        ```

    5. **Kundensegmentierung**
        - Bronze: Umsatz < 3000
        - Silber: 3000 ≤ Umsatz < 10000
        - Gold: Umsatz ≥ 10000

---

### Aufgabe 6 – A/B-Test Auswertung

A/B-Tests vergleichen zwei Varianten.

- [ ] **Erstelle `ab_test.py`:**

    Gegeben: Conversion-Raten (%) pro Tag für zwei Website-Varianten
    ```python
    variante_a = [3.2, 2.8, 3.5, 3.1, 2.9, 3.4, 3.0]
    variante_b = [3.5, 3.2, 3.8, 3.0, 3.6, 3.9, 3.3]
    ```

    Berechne:

    1. **Durchschnitt beider Varianten**

    2. **An wie vielen Tagen war Variante B besser?**
        ```python
        # Tipp: zip() nutzen
        for a, b in zip(variante_a, variante_b):
            ...
        ```

    3. **Standardabweichung beider Varianten**
        $$\sigma = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (x_i - \bar{x})^2}$$

    4. **Welche Variante ist konsistenter?**
        - Die Variante mit der geringeren Standardabweichung

    Ausgabe:
    ```
    === A/B-Test Ergebnis ===
    Variante A: Ø 3.13%, σ = 0.24
    Variante B: Ø 3.47%, σ = 0.31
    
    Variante B war an 5 von 7 Tagen besser.
    Empfehlung: Variante B hat höhere Conversion (+10.9%)
    Aber: Variante A ist konsistenter (geringere Streuung)
    ```

---

### Aufgabe 7 – Bonus: Daten-Pipeline (ETL)

Simuliere eine vereinfachte ETL-Pipeline (Extract, Transform, Load).

- [ ] **Erstelle `etl_pipeline.py`:**

    **Extract:** Generiere 1000 zufällige "Rohdaten"
    ```python
    import random
    
    rohdaten = []
    for _ in range(1000):
        if random.random() < 0.05:  # 5% None-Werte
            rohdaten.append(None)
        else:
            rohdaten.append(random.randint(0, 1000))
    ```

    **Transform:**
    - Entferne alle `None`-Werte
    - Identifiziere Ausreißer (> 2 Standardabweichungen vom Durchschnitt)
    - Ersetze Ausreißer durch den Median

    **Load:**
    - Teile die Daten in Batches à 100 Einträge auf
    - Gib für jeden Batch eine Zusammenfassung aus

    ```
    === ETL Pipeline ===
    Rohdaten: 1000 Einträge
    Nach Bereinigung: 952 Einträge (48 None entfernt)
    Ausreißer ersetzt: 23
    
    Batch 1: 100 Einträge, Ø 498.3
    Batch 2: 100 Einträge, Ø 512.1
    ...
    Batch 10: 52 Einträge, Ø 487.9
    ```

---

## Zusammenfassung

!!! success "Das hast du gelernt"
    - **Listen-Methoden**: `append`, `remove`, `sort`, `index`
    - **Slicing**: `liste[start:stop:step]`
    - **List Comprehensions**: `[ausdruck for x in liste if bedingung]`
    - **2D-Listen**: `matrix[zeile][spalte]`
    - **zip()**: Parallel über mehrere Listen iterieren
    - **Aggregation**: `sum()`, `min()`, `max()`, `len()`

---

??? question "Selbstkontrolle"
    1. Was ist der Unterschied zwischen `liste.sort()` und `sorted(liste)`?
    2. Was gibt `[1, 2, 3, 4, 5][1:4]` zurück?
    3. Schreibe eine List Comprehension für die Quadrate aller geraden Zahlen von 1-10.
    
    ??? success "Antworten"
        1. `sort()` ändert die Liste direkt (in-place), `sorted()` gibt eine neue sortierte Liste zurück
        2. `[2, 3, 4]` (Index 1 bis 3, da 4 exklusiv)
        3. `[x**2 for x in range(1, 11) if x % 2 == 0]` → `[4, 16, 36, 64, 100]`

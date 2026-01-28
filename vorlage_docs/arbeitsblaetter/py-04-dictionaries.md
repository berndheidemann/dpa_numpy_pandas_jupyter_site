# Python – Dictionaries & Dateiverarbeitung

## Lernziele

Nach Bearbeitung dieses Arbeitsblatts kannst du:

- Dictionaries erstellen, durchsuchen und bearbeiten
- Über Dictionaries iterieren mit `.keys()`, `.values()`, `.items()`
- CSV-Dateien mit Python lesen und verarbeiten
- Daten aggregieren und gruppieren

!!! note "Begleitende Infoblätter"
    - [:material-book-open-variant: Dictionaries](../infoblaetter/dictionaries.md) – Key-Value, Methoden, Iteration
    - [:material-book-open-variant: Funktionen](../infoblaetter/funktionen.md) – def, Parameter, Rückgabewerte

---

## Einführung

Dictionaries sind Key-Value-Speicher – perfekt für strukturierte Daten:

```python
# Dictionary-Grundlagen
spieler = {"name": "Max", "level": 42, "aktiv": True}

# Zugriff
print(spieler["name"])       # Max
print(spieler.get("team", "Kein Team"))  # Standardwert

# Iteration
for key, value in spieler.items():
    print(f"{key}: {value}")
```

---

## Aufgaben

### Aufgabe 1 – Produktkatalog

Ein einfacher Produktkatalog mit CRUD-Operationen.

- [ ] **Erstelle `produktkatalog.py`:**

    Starte mit diesem Katalog:
    ```python
    produkte = {
        "P001": {"name": "USB-Stick 64GB", "preis": 12.99, "bestand": 150},
        "P002": {"name": "Maus kabellos", "preis": 29.99, "bestand": 75},
        "P003": {"name": "Tastatur RGB", "preis": 79.99, "bestand": 30},
        "P004": {"name": "Monitor 27 Zoll", "preis": 299.99, "bestand": 20},
        "P005": {"name": "Webcam HD", "preis": 49.99, "bestand": 45}
    }
    ```

    Implementiere Funktionen für:

    1. **`show_product(produkte, produkt_id)`**
        - Zeigt alle Infos zu einem Produkt an
        - Gibt Fehlermeldung bei unbekannter ID

    2. **`update_stock(produkte, produkt_id, menge)`**
        - Erhöht/verringert den Bestand (negative Menge = Verkauf)
        - Bestand darf nicht unter 0 fallen

    3. **`find_low_stock(produkte, grenzwert)`**
        - Findet alle Produkte mit Bestand ≤ Grenzwert

    4. **`calculate_inventory_value(produkte)`**
        - Berechnet den Gesamtwert aller Bestände (Bestand × Preis)

    Ausgabe:
    ```
    === Produktkatalog ===
    P003: Tastatur RGB - 79.99€ - 30 Stück
    
    Lagerwarnung (Bestand ≤ 25):
    - P003: Tastatur RGB (30 Stück)
    - P004: Monitor 27 Zoll (20 Stück)
    
    Gesamter Inventarwert: 18.247,05€
    ```

---

### Aufgabe 2 – Server-Metriken Dashboard

Monitoring-Daten analysieren und überwachen.

- [ ] **Erstelle `server_monitoring.py`:**

    ```python
    server_metriken = {
        "web-server-01": {
            "cpu": [45, 52, 48, 61, 55, 72, 68, 59, 63, 71],
            "memory": [68, 70, 72, 75, 78, 82, 85, 80, 77, 79],
            "disk": 65
        },
        "db-server-01": {
            "cpu": [82, 85, 79, 88, 91, 87, 84, 89, 92, 86],
            "memory": [88, 90, 92, 91, 93, 94, 92, 90, 91, 93],
            "disk": 78
        },
        "cache-server-01": {
            "cpu": [15, 18, 12, 20, 22, 17, 19, 14, 16, 21],
            "memory": [45, 48, 50, 52, 49, 47, 51, 53, 50, 48],
            "disk": 30
        }
    }
    ```

    Implementiere:

    1. **`get_avg_cpu(metriken, server)`**
        - Durchschnittliche CPU-Auslastung eines Servers

    2. **`find_overloaded(metriken, cpu_limit, mem_limit)`**
        - Finde Server mit Durchschnitt über dem Limit

    3. **`generate_alert(metriken)`**
        - Generiere Warnungen für:
            - CPU-Durchschnitt > 80%
            - Memory-Durchschnitt > 90%
            - Disk > 75%

    4. **`create_summary(metriken)`**
        - Erstelle ein neues Dictionary mit Zusammenfassung pro Server

    Ausgabe:
    ```
    === Server Dashboard ===
    web-server-01: CPU Ø 59.4%, Mem Ø 76.6%, Disk 65%
    db-server-01:  CPU Ø 86.3%, Mem Ø 91.4%, Disk 78%
    cache-server-01: CPU Ø 17.4%, Mem Ø 49.3%, Disk 30%
    
    ⚠️ ALERTS:
    - db-server-01: CPU-Auslastung kritisch (86.3%)
    - db-server-01: Memory-Auslastung kritisch (91.4%)
    - db-server-01: Speicherplatz knapp (78%)
    ```

---

### Aufgabe 3 – CSV-Datei lesen (Videospiel-Analyse)

Arbeite mit echten CSV-Daten.

!!! info "Datei herunterladen"
    Lade die Datei [`games.csv`](../assets/files/games.csv) herunter und speichere sie im gleichen Ordner wie dein Skript.

- [ ] **Erstelle `games_analysis.py`:**

    1. **CSV einlesen ohne externe Bibliotheken**
        ```python
        def read_csv(filename):
            """Liest CSV und gibt Liste von Dictionaries zurück."""
            daten = []
            with open(filename, 'r', encoding='utf-8') as file:
                zeilen = file.readlines()
                header = zeilen[0].strip().split(',')
                
                for zeile in zeilen[1:]:
                    werte = zeile.strip().split(',')
                    eintrag = {}
                    for i, spalte in enumerate(header):
                        eintrag[spalte] = werte[i]
                    daten.append(eintrag)
            return daten
        ```

    2. **Datentypen konvertieren**
        - `Verkaufte_Einheiten_Mio` → `float`
        - `Bewertung` → `float`
        - `ID` → `int`

    3. **Analysen durchführen:**

        a) **Top 5 meistverkaufte Spiele**
        ```
        1. Minecraft - 238.0 Mio
        2. Grand Theft Auto V - 185.0 Mio
        3. PUBG: Battlegrounds - 75.0 Mio
        ...
        ```

        b) **Durchschnittliche Bewertung pro Genre**
        ```
        Puzzle: 9.90
        RPG: 8.76
        Adventure: 8.96
        ...
        ```

        c) **Verkaufszahlen pro Plattform**
        ```
        PC: 987.5 Mio
        Switch: 398.8 Mio
        Xbox: 386.0 Mio
        PS5: 174.7 Mio
        ```

        d) **Spiele mit Bewertung ≥ 9.5**

---

### Aufgabe 4 – Grouping und Aggregation

Gruppiere Daten nach verschiedenen Kriterien.

- [ ] **Erweitere `games_analysis.py`:**

    1. **`group_by_genre(games)`**
        ```python
        # Ergebnis:
        {
            "RPG": [{"Name": "Baldur's Gate 3", ...}, ...],
            "Shooter": [{"Name": "Counter-Strike 2", ...}, ...],
            ...
        }
        ```

    2. **`count_by_platform(games)`**
        ```python
        # Ergebnis:
        {"PC": 31, "Switch": 19, "Xbox": 22, "PS5": 18}
        ```

    3. **`average_rating_by_platform(games)`**
        - Berechne die Durchschnittsbewertung pro Plattform

    4. **`find_best_per_genre(games)`**
        - Finde das am besten bewertete Spiel pro Genre

    Ausgabe:
    ```
    === Beste Spiele pro Genre ===
    Action: God of War (2018) - 9.8
    Adventure: Red Dead Redemption 2 - 9.7
    Fighting: Super Smash Bros. Ultimate - 9.4
    MMO: World of Warcraft - 8.5
    MOBA: Dota 2 - 8.5
    Party: Among Us - 8.5
    Platformer: Super Mario Odyssey - 9.7
    Puzzle: Portal 2 - 9.9
    RPG: The Witcher 3: Wild Hunt - 9.8
    Racing: Forza Horizon 5 - 9.4
    Shooter: Half-Life 2 - 9.7
    Simulation: Minecraft - 9.5
    Sport: Ring Fit Adventure - 8.3
    Strategy: Factorio - 9.8
    Survival: Valheim - 9.0
    ```

---

### Aufgabe 5 – Nested Dictionaries

Komplexere Datenstrukturen verarbeiten.

- [ ] **Erstelle `nested_dicts.py`:**

    ```python
    unternehmensdaten = {
        "2021": {
            "Q1": {"umsatz": 125000, "kosten": 95000, "mitarbeiter": 45},
            "Q2": {"umsatz": 138000, "kosten": 102000, "mitarbeiter": 48},
            "Q3": {"umsatz": 142000, "kosten": 108000, "mitarbeiter": 52},
            "Q4": {"umsatz": 165000, "kosten": 115000, "mitarbeiter": 55}
        },
        "2022": {
            "Q1": {"umsatz": 148000, "kosten": 110000, "mitarbeiter": 58},
            "Q2": {"umsatz": 162000, "kosten": 118000, "mitarbeiter": 62},
            "Q3": {"umsatz": 175000, "kosten": 125000, "mitarbeiter": 65},
            "Q4": {"umsatz": 198000, "kosten": 138000, "mitarbeiter": 70}
        },
        "2023": {
            "Q1": {"umsatz": 185000, "kosten": 130000, "mitarbeiter": 72},
            "Q2": {"umsatz": 195000, "kosten": 140000, "mitarbeiter": 75},
            "Q3": {"umsatz": 210000, "kosten": 148000, "mitarbeiter": 78},
            "Q4": {"umsatz": 235000, "kosten": 160000, "mitarbeiter": 82}
        }
    }
    ```

    Implementiere:

    1. **Jahresumsatz berechnen**
        ```python
        def jahresumsatz(daten, jahr):
            # Summiere alle Quartalsumsätze
            pass
        ```

    2. **Jahresgewinn berechnen**
        ```python
        def jahresgewinn(daten, jahr):
            # Umsatz - Kosten pro Quartal, dann summieren
            pass
        ```

    3. **Wachstumsrate berechnen**
        ```python
        def wachstumsrate(daten, jahr1, jahr2):
            # (Umsatz_jahr2 - Umsatz_jahr1) / Umsatz_jahr1 * 100
            pass
        ```

    4. **Umsatz pro Mitarbeiter**
        ```python
        def umsatz_pro_mitarbeiter(daten, jahr, quartal):
            pass
        ```

    5. **Bestes Quartal finden**
        ```python
        def bestes_quartal(daten):
            # Finde das Quartal mit höchstem Gewinn (Jahr, Quartal, Gewinn)
            pass
        ```

    Ausgabe:
    ```
    === Unternehmensanalyse ===
    
    Jahresumsatz 2021: 570.000€
    Jahresumsatz 2022: 683.000€
    Jahresumsatz 2023: 825.000€
    
    Jahresgewinn 2021: 150.000€
    Jahresgewinn 2023: 247.000€
    
    Wachstumsrate 2021→2023: 44.7%
    
    Umsatz/Mitarbeiter Q4 2023: 2.866€
    
    Bestes Quartal: 2023 Q4 mit 75.000€ Gewinn
    ```

---

### Aufgabe 6 - Bonus – Dictionary Comprehensions

Kompakte Transformationen mit Dictionary Comprehensions.

- [ ] **Erstelle `dict_comprehensions.py`:**

    1. **Quadratzahlen-Dictionary**
        ```python
        quadrate = {x: x**2 for x in range(1, 11)}
        # {1: 1, 2: 4, 3: 9, ...}
        ```

    2. **Filtern**
        ```python
        preise = {"Apfel": 0.50, "Mango": 3.20, "Banane": 0.30, "Kiwi": 1.50}
        teuer = {k: v for k, v in preise.items() if v > 1.00}
        # {"Mango": 3.20, "Kiwi": 1.50}
        ```

    3. **Keys und Values tauschen**
        ```python
        original = {"a": 1, "b": 2, "c": 3}
        umgekehrt = ???
        # {1: "a", 2: "b", 3: "c"}
        ```

    4. **Aus zwei Listen ein Dictionary**
        ```python
        namen = ["Alice", "Bob", "Charlie"]
        punkte = [85, 92, 78]
        ergebnis = ???
        # {"Alice": 85, "Bob": 92, "Charlie": 78}
        ```

    5. **Wörter zählen**
        ```python
        text = "der die das der eine das der"
        woerter = text.split()
        haeufigkeit = ???
        # {"der": 3, "die": 1, "das": 2, "eine": 1}
        ```

---


## Zusammenfassung

!!! success "Das hast du gelernt"
    - **Dictionary-Methoden**: `.get()`, `.keys()`, `.values()`, `.items()`
    - **Iteration**: `for key, value in dict.items()`
    - **Nested Dictionaries**: `data[key1][key2]`
    - **CSV-Verarbeitung**: Zeilen lesen, splitten, in Dicts umwandeln
    - **Grouping**: Daten nach Kategorien zusammenfassen
    - **Dict Comprehensions**: `{k: v for k, v in items if condition}`

---

??? question "Selbstkontrolle"
    1. Was ist der Unterschied zwischen `dict["key"]` und `dict.get("key")`?
    2. Wie iterierst du gleichzeitig über Keys und Values?
    3. Schreibe eine Dict Comprehension: Aus `["a", "b", "c"]` erstelle `{"a": 0, "b": 1, "c": 2}`
    
    ??? success "Antworten"
        1. `dict["key"]` wirft KeyError bei fehlendem Key, `dict.get("key")` gibt `None` zurück (oder einen Standardwert)
        2. `for key, value in dict.items():`
        3. `{buchstabe: index for index, buchstabe in enumerate(["a", "b", "c"])}`

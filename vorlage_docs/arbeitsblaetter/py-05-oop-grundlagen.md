# Python – OOP Grundlagen

## Lernziele

Nach Bearbeitung dieses Arbeitsblatts kannst du:

- Klassen mit Attributen definieren
- Objekte erstellen und verwenden
- Methoden schreiben, die auf Objektdaten zugreifen
- Die `__init__`-Methode und `__str__`-Methode verstehen

!!! note "Begleitendes Infoblatt"
    [:material-book-open-variant: OOP in Python](../infoblaetter/oop-python.md) – Klassen, Vererbung, Properties

---

## Einführung

**Objektorientierte Programmierung (OOP)** hilft, zusammengehörige Daten und Funktionen zu bündeln. Statt loser Variablen und Funktionen arbeiten wir mit **Objekten**.

### Klasse vs. Objekt

- **Klasse** = Bauplan (z.B. "Produkt")
- **Objekt** = konkretes Exemplar (z.B. "Laptop mit Preis 999€")

```python
# Klasse definieren (Bauplan)
class Produkt:
    def __init__(self, name, preis):
        self.name = name      # Attribut
        self.preis = preis    # Attribut
    
    def __str__(self):
        return f"{self.name}: {self.preis}€"

# Objekte erstellen (konkrete Exemplare)
laptop = Produkt("Laptop", 999)
maus = Produkt("Maus", 29.99)

print(laptop)       # Laptop: 999€
print(maus.preis)   # 29.99
```

!!! info "Wichtige Begriffe"
    - `class`: Definiert eine neue Klasse
    - `__init__`: Wird beim Erstellen eines Objekts aufgerufen (Konstruktor)
    - `self`: Referenz auf das aktuelle Objekt
    - **Attribut**: Variable, die zu einem Objekt gehört (`self.name`)
    - **Methode**: Funktion, die zu einer Klasse gehört

---

## Aufgaben

### Aufgabe 1 – Erste Klasse: Messwert

Erstelle eine Klasse, die einen einzelnen Messwert repräsentiert.

- [ ] **Erstelle `messwert.py` mit der Klasse `Messwert`:**

    **Attribute:**
    
    | Attribut | Typ | Beschreibung |
    |----------|-----|--------------|
    | `wert` | float | Der Messwert (z.B. 23.5) |
    | `einheit` | str | Die Einheit (z.B. "°C") |

    **Methoden:**
    
    | Methode | Rückgabe | Beschreibung |
    |---------|----------|--------------|
    | `__init__(self, wert, einheit)` | - | Konstruktor, speichert die Attribute |
    | `__str__(self)` | str | Gibt "23.5 °C" zurück |
    | `ist_im_bereich(self, min, max)` | bool | True wenn min ≤ wert ≤ max |

    **Test – so soll es funktionieren:**
    ```python
    temperatur = Messwert(23.5, "°C")
    print(temperatur)                        # 23.5 °C
    print(temperatur.ist_im_bereich(10, 30)) # True
    print(temperatur.ist_im_bereich(0, 20))  # False
    
    luftdruck = Messwert(1013, "hPa")
    print(luftdruck)                         # 1013 hPa
    print(luftdruck.wert)                    # 1013
    ```

---

### Aufgabe 2 – Klasse mit Berechnungen: Verkauf

Erstelle eine Klasse für Verkaufsvorgänge, die den Umsatz berechnen kann.

- [ ] **Erstelle `verkauf.py` mit der Klasse `Verkauf`:**

    **Attribute:**
    
    | Attribut | Typ | Beschreibung |
    |----------|-----|--------------|
    | `produkt` | str | Produktname |
    | `menge` | int | Verkaufte Menge |
    | `einzelpreis` | float | Preis pro Stück |

    **Methoden:**
    
    | Methode | Rückgabe | Beschreibung |
    |---------|----------|--------------|
    | `__init__(self, produkt, menge, einzelpreis)` | - | Konstruktor |
    | `berechne_umsatz(self)` | float | Menge × Einzelpreis |
    | `berechne_mit_rabatt(self, prozent)` | float | Umsatz minus Rabatt |
    | `__str__(self)` | str | Formatierte Ausgabe |

    **Test:**
    ```python
    v1 = Verkauf("Laptop", 3, 999)
    print(v1)                       # Laptop: 3 x 999€ = 2997€
    print(v1.berechne_umsatz())     # 2997
    
    v2 = Verkauf("Monitor", 2, 300)
    print(v2.berechne_mit_rabatt(10))  # 540.0 (10% Rabatt auf 600€)
    ```

---

### Aufgabe 3 – Objekte in einer Liste

Oft arbeitet man mit mehreren Objekten. Nutze deine `Verkauf`-Klasse aus Aufgabe 2.

- [ ] **Erstelle eine Liste von Verkäufen und berechne Statistiken:**

    Erstelle diese Verkäufe:
    
    | Produkt | Menge | Einzelpreis |
    |---------|-------|-------------|
    | Laptop | 2 | 999 € |
    | Monitor | 5 | 299 € |
    | Tastatur | 10 | 49.99 € |
    | Maus | 15 | 29.99 € |

    **Aufgaben:**
    
    1. Speichere alle Verkäufe in einer Liste
    2. Gib alle Verkäufe mit einer Schleife aus
    3. Berechne den Gesamtumsatz aller Verkäufe
    4. Finde den Verkauf mit dem höchsten Umsatz

    **Erwartete Ausgabe:**
    ```
    === Verkaufsliste ===
    Laptop: 2 x 999€ = 1998€
    Monitor: 5 x 299€ = 1495€
    Tastatur: 10 x 49.99€ = 499.9€
    Maus: 15 x 29.99€ = 449.85€

    Gesamtumsatz: 4442.75€
    Höchster Einzelumsatz: Laptop mit 1998€
    ```

    !!! tip "Tipp"
        Du kannst mit einer List Comprehension alle Umsätze sammeln:
        ```python
        umsaetze = [v.berechne_umsatz() for v in verkaeufe]
        ```

---

### Aufgabe 4 – Klasse mit Liste als Attribut: Sensor

Ein Sensor sammelt mehrere Messwerte über die Zeit. Die Klasse soll Statistiken berechnen.

- [ ] **Erstelle `sensor.py` mit der Klasse `Sensor`:**

    **Attribute:**
    
    | Attribut | Typ | Beschreibung |
    |----------|-----|--------------|
    | `name` | str | Name des Sensors |
    | `einheit` | str | Messeinheit (z.B. "°C") |
    | `messwerte` | list | Liste der erfassten Werte (anfangs leer!) |

    **Methoden:**
    
    | Methode | Rückgabe | Beschreibung |
    |---------|----------|--------------|
    | `__init__(self, name, einheit)` | - | Konstruktor, `messwerte` als leere Liste |
    | `add_messwert(self, wert)` | - | Fügt einen Wert zur Liste hinzu |
    | `anzahl(self)` | int | Anzahl der Messwerte |
    | `durchschnitt(self)` | float | Durchschnitt (0 wenn keine Werte) |
    | `minimum(self)` | float/None | Kleinster Wert (None wenn leer) |
    | `maximum(self)` | float/None | Größter Wert (None wenn leer) |
    | `__str__(self)` | str | "Sensor 'Name': X Messwerte" |

    **Test:**
    ```python
    temp_sensor = Sensor("Temperatur", "°C")
    
    temp_sensor.add_messwert(22.5)
    temp_sensor.add_messwert(23.1)
    temp_sensor.add_messwert(21.8)
    temp_sensor.add_messwert(24.2)
    
    print(temp_sensor)                              # Sensor 'Temperatur': 4 Messwerte
    print(f"Durchschnitt: {temp_sensor.durchschnitt():.1f} °C")  # 22.9 °C
    print(f"Min: {temp_sensor.minimum()} °C")       # 21.8 °C
    print(f"Max: {temp_sensor.maximum()} °C")       # 24.2 °C
    print(f"Anzahl: {temp_sensor.anzahl()}")        # 4
    ```

---

### Aufgabe 5 – Komposition: Messstation

Eine Messstation enthält mehrere Sensoren. Das nennt man **Komposition** – ein Objekt enthält andere Objekte.

```kroki-plantuml
@startuml
skinparam classAttributeIconSize 0
skinparam style strictuml

class Messstation {
  - standort: str
  - sensoren: list
  + add_sensor(sensor)
  + get_sensor(name): Sensor
  + uebersicht()
}

class Sensor {
  - name: str
  - einheit: str
  - messwerte: list
  + add_messwert(wert)
  + durchschnitt(): float
  + minimum(): float
  + maximum(): float
}

Messstation o-- "*" Sensor : enthält >
@enduml
```

- [ ] **Erstelle `messstation.py` mit der Klasse `Messstation`:**

    **Attribute:**
    
    | Attribut | Typ | Beschreibung |
    |----------|-----|--------------|
    | `standort` | str | Standort der Station |
    | `sensoren` | list | Liste von Sensor-Objekten (anfangs leer) |

    **Methoden:**
    
    | Methode | Rückgabe | Beschreibung |
    |---------|----------|--------------|
    | `__init__(self, standort)` | - | Konstruktor |
    | `add_sensor(self, sensor)` | - | Fügt Sensor zur Liste hinzu |
    | `get_sensor(self, name)` | Sensor/None | Findet Sensor nach Name |
    | `uebersicht(self)` | - | Gibt alle Sensoren mit Durchschnitt aus |

    **Test:**
    ```python
    # Station erstellen
    station = Messstation("Bremen-Mitte")
    
    # Sensoren erstellen (aus Aufgabe 4)
    temp = Sensor("Temperatur", "°C")
    feuchte = Sensor("Luftfeuchtigkeit", "%")
    
    # Sensoren zur Station hinzufügen
    station.add_sensor(temp)
    station.add_sensor(feuchte)
    
    # Messwerte über die Sensoren hinzufügen
    temp.add_messwert(22.5)
    temp.add_messwert(23.1)
    feuchte.add_messwert(45)
    feuchte.add_messwert(48)
    
    # Sensor suchen
    t = station.get_sensor("Temperatur")
    print(t.durchschnitt())  # 22.8
    
    # Übersicht
    station.uebersicht()
    ```

    **Erwartete Ausgabe von `uebersicht()`:**
    ```
    === Messstation Bremen-Mitte ===
      Temperatur: Ø 22.8 °C
      Luftfeuchtigkeit: Ø 46.5 %
    ```

---

### Aufgabe 6 – Einfache Vererbung

Eine Klasse kann von einer anderen **erben** und deren Eigenschaften übernehmen.

```kroki-plantuml
@startuml
skinparam classAttributeIconSize 0
skinparam style strictuml

class Sensor {
  - name: str
  - messwerte: list
  + add_messwert(wert)
  + durchschnitt(): float
}

class TemperaturSensor {
  - einheit: str = "°C"
  + ist_frost(): bool
}

class DruckSensor {
  - einheit: str = "hPa"
  + tendenz(): str
}

Sensor <|-- TemperaturSensor
Sensor <|-- DruckSensor
@enduml
```

- [ ] **Erstelle `sensoren_erweitert.py`:**

    **Basisklasse `Sensor`:** (vereinfacht)
    
    | Attribut/Methode | Beschreibung |
    |------------------|--------------|
    | `name` | Name des Sensors |
    | `messwerte` | Liste der Messwerte |
    | `add_messwert(wert)` | Fügt Wert hinzu |
    | `durchschnitt()` | Berechnet Durchschnitt |

    **Kindklasse `TemperaturSensor(Sensor)`:**
    
    | Attribut/Methode | Beschreibung |
    |------------------|--------------|
    | `einheit` | Fest auf "°C" gesetzt |
    | `ist_frost()` | True wenn ein Wert < 0 ist |

    **Kindklasse `DruckSensor(Sensor)`:**
    
    | Attribut/Methode | Beschreibung |
    |------------------|--------------|
    | `einheit` | Fest auf "hPa" gesetzt |
    | `tendenz()` | "steigend", "fallend" oder "stabil" |

    !!! tip "Hinweis: Vererbung"
        ```python
        class Kind(Eltern):
            def __init__(self, ...):
                super().__init__(...)  # Ruft Konstruktor der Elternklasse auf
        ```

    **Test:**
    ```python
    # Temperatur-Sensor
    temp = TemperaturSensor("Außentemperatur")
    temp.add_messwert(5.2)
    temp.add_messwert(-2.1)
    temp.add_messwert(3.5)
    
    print(f"{temp.name}: Ø {temp.durchschnitt():.1f} {temp.einheit}")
    print(f"Frost: {temp.ist_frost()}")  # True (wegen -2.1)
    
    # Druck-Sensor
    druck = DruckSensor("Barometer")
    druck.add_messwert(1013)
    druck.add_messwert(1015)
    druck.add_messwert(1018)
    
    print(f"{druck.name}: Ø {druck.durchschnitt():.0f} {druck.einheit}")
    print(f"Tendenz: {druck.tendenz()}")  # steigend
    ```

    !!! info "Tendenz-Logik"
        Vergleiche die letzten beiden Messwerte:
        
        - Letzter > Vorletzter → "steigend"
        - Letzter < Vorletzter → "fallend"
        - Gleich → "stabil"
        - Weniger als 2 Werte → "keine Daten"

---

## Zusammenfassung

!!! success "Das hast du gelernt"
    - **Klassen definieren**: `class Name:`
    - **Konstruktor**: `__init__(self, ...)` initialisiert Attribute
    - **Attribute**: Daten, die zu einem Objekt gehören (`self.name`)
    - **Methoden**: Funktionen in einer Klasse
    - **`__str__`**: Bestimmt, was bei `print(objekt)` ausgegeben wird
    - **Listen von Objekten**: Mehrere Objekte verwalten
    - **Komposition**: Objekte enthalten andere Objekte
    - **Vererbung**: Klassen können von anderen erben (`class Kind(Eltern)`)

---

??? question "Selbstkontrolle"
    1. Was ist der Unterschied zwischen einer Klasse und einem Objekt?
    2. Wofür ist `self` in einer Methode?
    3. Was macht `super().__init__()`?
    
    ??? success "Antworten"
        1. Eine **Klasse** ist ein Bauplan, ein **Objekt** ist eine konkrete Instanz dieses Bauplans
        2. `self` ist eine Referenz auf das aktuelle Objekt, damit die Methode auf dessen Attribute zugreifen kann
        3. `super().__init__()` ruft den Konstruktor der Elternklasse auf, um deren Initialisierung auszuführen

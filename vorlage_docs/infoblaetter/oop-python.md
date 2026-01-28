# Objektorientierte Programmierung in Python

## Was ist OOP?

Die **Objektorientierte Programmierung** (OOP) ist ein Programmierparadigma, das auf dem Konzept von **Objekten** basiert. Objekte kombinieren:

- **Attribute** (Daten/Eigenschaften)
- **Methoden** (Funktionen/Verhalten)

!!! example "Analogie"
    Ein **Auto** als Objekt hätte:
    
    - Attribute: Marke, Farbe, Kilometerstand
    - Methoden: starten(), fahren(), bremsen()

---

## Klassen und Objekte

### Klasse definieren

Eine **Klasse** ist eine Vorlage/Bauplan für Objekte:

```python
class Auto:
    """Eine Klasse, die ein Auto repräsentiert."""
    pass
```

### Objekt erstellen (Instanziierung)

```python
mein_auto = Auto()  # Erstellt ein Auto-Objekt
dein_auto = Auto()  # Erstellt ein weiteres Auto-Objekt
```

---

## Der Konstruktor `__init__`

Der Konstruktor wird beim Erstellen eines Objekts automatisch aufgerufen:

```python
class Auto:
    def __init__(self, marke, farbe, baujahr):
        self.marke = marke
        self.farbe = farbe
        self.baujahr = baujahr
        self.kilometerstand = 0  # Standardwert

# Objekt erstellen
mein_auto = Auto("VW", "rot", 2020)
print(mein_auto.marke)   # VW
print(mein_auto.farbe)   # rot
```

### Was ist `self`?

`self` ist eine Referenz auf das aktuelle Objekt. Es muss der **erste Parameter** jeder Methode sein:

```python
class Person:
    def __init__(self, name):
        self.name = name  # self.name ist das Attribut
    
    def vorstellen(self):
        print(f"Ich bin {self.name}")

max = Person("Max")
max.vorstellen()  # Ich bin Max
```

!!! info "self wird automatisch übergeben"
    Beim Aufruf `max.vorstellen()` wird `self` automatisch auf `max` gesetzt.

---

## Attribute

Attribute speichern die Daten/Eigenschaften eines Objekts. Python unterscheidet zwei Arten:

### Instanzattribute

Gehören zu einem **bestimmten Objekt** und können für jedes Objekt unterschiedlich sein. Sie werden typischerweise im Konstruktor mit `self.attribut` definiert:

```python
class Kunde:
    def __init__(self, name, kundennummer):
        self.name = name           # Instanzattribut
        self.kundennummer = kundennummer

kunde1 = Kunde("Max", "K001")
kunde2 = Kunde("Anna", "K002")

print(kunde1.name)  # Max
print(kunde2.name)  # Anna
```

### Klassenattribute

Gehören zur **Klasse selbst** und werden von allen Objekten geteilt. Sie werden außerhalb des Konstruktors definiert und sind nützlich für Werte, die für alle Instanzen gleich sind (z.B. Zähler, Konstanten):

```python
class Kunde:
    anzahl_kunden = 0  # Klassenattribut
    
    def __init__(self, name):
        self.name = name
        Kunde.anzahl_kunden += 1  # Klassenattribut erhöhen

kunde1 = Kunde("Max")
kunde2 = Kunde("Anna")
print(Kunde.anzahl_kunden)  # 2
```

---

## Methoden

### Instanzmethoden

Arbeiten mit dem Objekt über `self`:

```python
class Konto:
    def __init__(self, inhaber, kontostand=0):
        self.inhaber = inhaber
        self.kontostand = kontostand
    
    def einzahlen(self, betrag):
        """Zahlt einen Betrag ein."""
        if betrag > 0:
            self.kontostand += betrag
    
    def abheben(self, betrag):
        """Hebt einen Betrag ab, wenn gedeckt."""
        if betrag <= self.kontostand:
            self.kontostand -= betrag
            return True
        return False
    
    def zeige_kontostand(self):
        print(f"Kontostand von {self.inhaber}: {self.kontostand} €")

# Verwendung
konto = Konto("Max", 1000)
konto.einzahlen(500)
konto.zeige_kontostand()  # Kontostand von Max: 1500 €
```

### String-Repräsentation mit `__str__`

```python
class Kunde:
    def __init__(self, name, kundennummer):
        self.name = name
        self.kundennummer = kundennummer
    
    def __str__(self):
        return f"Kunde {self.kundennummer}: {self.name}"

kunde = Kunde("Max", "K001")
print(kunde)  # Kunde K001: Max
```

### Weitere Magic Methods

| Methode | Beschreibung | Aufruf |
|---------|--------------|--------|
| `__str__` | String-Darstellung | `str(obj)`, `print(obj)` |
| `__repr__` | Debug-Darstellung | `repr(obj)` |
| `__len__` | Länge | `len(obj)` |
| `__eq__` | Gleichheit | `obj1 == obj2` |
| `__lt__` | Kleiner als | `obj1 < obj2` |
| `__add__` | Addition | `obj1 + obj2` |

---

## Kapselung

**Kapselung** (Encapsulation) bedeutet, interne Daten vor direktem Zugriff zu schützen. Stattdessen erfolgt der Zugriff über kontrollierte Methoden. So kannst du:

- Ungültige Werte verhindern (Validierung)
- Interne Implementierung ändern, ohne externen Code zu brechen
- Den Zustand des Objekts konsistent halten

Python erzwingt Kapselung nicht streng, nutzt aber Konventionen:

### Private Attribute (Konvention)

Ein Unterstrich signalisiert "privat" (nur Konvention, nicht erzwungen):

```python
class Konto:
    def __init__(self, kontostand):
        self._kontostand = kontostand  # "privat"
    
    def get_kontostand(self):
        return self._kontostand
```

### Name Mangling mit `__`

Doppelter Unterstrich macht Zugriff schwieriger:

```python
class Konto:
    def __init__(self):
        self.__pin = "1234"  # Name Mangling

konto = Konto()
# print(konto.__pin)  # AttributeError!
print(konto._Konto__pin)  # 1234 (umgehbar, aber unschön)
```

### Properties (Getter/Setter)

Properties bieten eine elegante Möglichkeit, den Zugriff auf Attribute zu kontrollieren, ohne die Syntax zu ändern. Von außen sieht es aus wie ein normales Attribut, aber intern können Validierung oder Berechnungen stattfinden:
class Temperatur:
    def __init__(self, celsius):
        self._celsius = celsius
    
    @property
    def celsius(self):
        """Getter für Celsius."""
        return self._celsius
    
    @celsius.setter
    def celsius(self, wert):
        """Setter mit Validierung."""
        if wert < -273.15:
            raise ValueError("Temperatur unter absolutem Nullpunkt!")
        self._celsius = wert
    
    @property
    def fahrenheit(self):
        """Berechnetes Property (nur lesen)."""
        return self._celsius * 9/5 + 32

temp = Temperatur(20)
print(temp.celsius)     # 20 (Getter)
print(temp.fahrenheit)  # 68.0 (berechnetes Property)
temp.celsius = 25       # Setter
```

---

## Vererbung

**Vererbung** ermöglicht es, eine neue Klasse auf Basis einer bestehenden zu erstellen. Die neue Klasse (Kindklasse) **erbt** alle Attribute und Methoden der Basisklasse (Elternklasse) und kann diese erweitern oder überschreiben.

**Vorteile:**

- Code-Wiederverwendung (DRY-Prinzip)
- Gemeinsame Logik in der Basisklasse
- Spezialisierung in Kindklassen

### Klassendiagramm: Vererbung

```kroki-plantuml
@startuml
skinparam classAttributeIconSize 0
skinparam style strictuml

class Fahrzeug {
  - marke: str
  - baujahr: int
  + info(): str
}

class Auto {
  - tueren: int
  + info(): str
}

class Motorrad {
  - hubraum: int
}

Fahrzeug <|-- Auto
Fahrzeug <|-- Motorrad

note right of Auto : überschreibt info()
@enduml
```

Eine Klasse kann von einer anderen erben:

```python
class Fahrzeug:
    """Basisklasse für alle Fahrzeuge."""
    
    def __init__(self, marke, baujahr):
        self.marke = marke
        self.baujahr = baujahr
    
    def info(self):
        return f"{self.marke} ({self.baujahr})"

class Auto(Fahrzeug):
    """Abgeleitete Klasse für Autos."""
    
    def __init__(self, marke, baujahr, tueren):
        super().__init__(marke, baujahr)  # Basisklasse aufrufen
        self.tueren = tueren
    
    def info(self):  # Methode überschreiben
        return f"{super().info()}, {self.tueren} Türen"

class Motorrad(Fahrzeug):
    """Abgeleitete Klasse für Motorräder."""
    
    def __init__(self, marke, baujahr, hubraum):
        super().__init__(marke, baujahr)
        self.hubraum = hubraum

# Verwendung
auto = Auto("VW", 2020, 4)
motorrad = Motorrad("Honda", 2019, 600)

print(auto.info())      # VW (2020), 4 Türen
print(motorrad.info())  # Honda (2019)
```

### super()

`super()` gibt eine Referenz auf die Basisklasse zurück:

```python
class Basis:
    def methode(self):
        print("Basis-Methode")

class Abgeleitet(Basis):
    def methode(self):
        super().methode()  # Ruft Basis.methode() auf
        print("Erweitert")

obj = Abgeleitet()
obj.methode()
# Ausgabe:
# Basis-Methode
# Erweitert
```

---

## Polymorphismus

**Polymorphismus** (griech. "Vielgestaltigkeit") bedeutet, dass verschiedene Klassen dieselbe Methode unterschiedlich implementieren können. Der aufrufende Code muss nicht wissen, welche konkrete Klasse er verwendet – er ruft einfach die Methode auf und jedes Objekt reagiert auf seine Weise.

Das ist besonders nützlich, wenn du mit einer Sammlung unterschiedlicher Objekte arbeiten willst:

```python
class Datenquelle:
    def lade_daten(self):
        raise NotImplementedError("Muss implementiert werden!")

class CSVQuelle(Datenquelle):
    def lade_daten(self):
        return "Daten aus CSV geladen"

class APIQuelle(Datenquelle):
    def lade_daten(self):
        return "Daten aus API geladen"

class DatenbankQuelle(Datenquelle):
    def lade_daten(self):
        return "Daten aus DB geladen"

# Polymorphe Verwendung
quellen = [CSVQuelle(), APIQuelle(), DatenbankQuelle()]

for quelle in quellen:
    print(quelle.lade_daten())
```

---

## Komposition

Neben Vererbung ("ist ein") gibt es eine weitere wichtige Beziehung zwischen Klassen: **Komposition** ("hat ein"). Ein Objekt enthält andere Objekte als Attribute und delegiert Aufgaben an sie.

### Klassendiagramm: Komposition

```kroki-plantuml
@startuml
skinparam classAttributeIconSize 0
skinparam style strictuml

class Motor {
  - ps: int
  + starten()
}

class Auto {
  - marke: str
  - motor: Motor
  + starten()
}

Auto *-- Motor : hat einen >

note bottom of Auto : Auto HAT einen Motor\n(Komposition)
@enduml
```

"Has-a"-Beziehung: Ein Objekt **enthält** andere Objekte:

```python
class Motor:
    def __init__(self, ps):
        self.ps = ps
    
    def starten(self):
        print(f"Motor mit {self.ps} PS startet")

class Auto:
    def __init__(self, marke, motor):
        self.marke = marke
        self.motor = motor  # Auto HAT einen Motor
    
    def starten(self):
        print(f"{self.marke} wird gestartet...")
        self.motor.starten()

motor = Motor(150)
auto = Auto("VW Golf", motor)
auto.starten()
# VW Golf wird gestartet...
# Motor mit 150 PS startet
```

!!! tip "Komposition vs. Vererbung"
    - **Vererbung**: "ist ein" (Auto ist ein Fahrzeug)
    - **Komposition**: "hat ein" (Auto hat einen Motor)
    
    Bevorzuge Komposition, wenn möglich – sie ist flexibler!

---

## Praxisbeispiel: Data Analyst Klassen

```python
class DataPoint:
    """Repräsentiert einen einzelnen Messwert."""
    
    def __init__(self, timestamp, value, unit=""):
        self.timestamp = timestamp
        self.value = value
        self.unit = unit
    
    def is_valid(self):
        return self.value is not None
    
    def __str__(self):
        return f"{self.timestamp}: {self.value} {self.unit}"


class Dataset:
    """Verwaltet eine Sammlung von Messwerten."""
    
    def __init__(self, name):
        self.name = name
        self.data = []
    
    def add(self, value):
        self.data.append(value)
    
    def mean(self):
        if not self.data:
            return None
        return sum(self.data) / len(self.data)
    
    def __len__(self):
        return len(self.data)
    
    def __str__(self):
        return f"Dataset '{self.name}' mit {len(self)} Werten"


# Verwendung
ds = Dataset("Temperaturen")
ds.add(23.5)
ds.add(24.1)
ds.add(22.8)

print(ds)            # Dataset 'Temperaturen' mit 3 Werten
print(ds.mean())     # 23.466...
print(len(ds))       # 3
```

---

## Zusammenfassung

!!! success "Das Wichtigste"
    - **Klasse**: Bauplan für Objekte
    - **Objekt**: Instanz einer Klasse
    - **`__init__`**: Konstruktor, wird bei Erstellung aufgerufen
    - **`self`**: Referenz auf das aktuelle Objekt
    - **Vererbung**: `class Kind(Eltern):`
    - **`super()`**: Zugriff auf Basisklasse
    - **Properties**: Kontrollierter Attributzugriff
    - **Komposition**: Objekte enthalten andere Objekte

---

??? question "Selbstkontrolle"
    1. Was ist der Unterschied zwischen Klasse und Objekt?
    2. Warum braucht jede Methode `self` als ersten Parameter?
    3. Was macht `super().__init__()`?
    
    ??? success "Antworten"
        1. Eine **Klasse** ist der Bauplan/die Vorlage, ein **Objekt** ist eine konkrete Instanz davon
        2. `self` ist die Referenz auf das aktuelle Objekt, damit die Methode auf dessen Attribute zugreifen kann
        3. Ruft den Konstruktor der Basisklasse auf, um deren Attribute zu initialisieren

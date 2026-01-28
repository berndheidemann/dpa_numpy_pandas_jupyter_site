# Funktionen

## Visualisierung: Funktionsaufruf

```kroki-mermaid
sequenceDiagram
    participant H as Hauptprogramm
    participant F as Funktion
    
    H->>F: Aufruf mit Argumenten
    Note right of F: Parameter empfangen
    F->>F: Code ausführen
    F-->>H: return Ergebnis
    Note left of H: Rückgabewert verwenden
```

## Was sind Funktionen?

Funktionen sind **wiederverwendbare Codeblöcke**, die eine bestimmte Aufgabe erledigen. Sie helfen dabei:

- Code zu **strukturieren**
- **Wiederholungen** zu vermeiden (DRY-Prinzip)
- Code **testbar** zu machen
- **Komplexität** zu reduzieren

---

## Funktionen definieren

### Grundsyntax

```python
def funktionsname(parameter1, parameter2):
    """Docstring: Beschreibung der Funktion."""
    # Funktionskörper
    anweisungen
    return ergebnis
```

### Einfaches Beispiel

```python
def begruessung(name):
    """Gibt eine Begrüßung aus."""
    print(f"Hallo, {name}!")

# Funktion aufrufen
begruessung("Max")   # Hallo, Max!
begruessung("Anna")  # Hallo, Anna!
```

---

## Parameter und Argumente

### Positionsparameter

```python
def addiere(a, b):
    return a + b

ergebnis = addiere(5, 3)  # 8
```

### Keyword-Argumente

```python
def person_info(name, alter, stadt):
    print(f"{name}, {alter} Jahre, aus {stadt}")

# Reihenfolge egal bei Keyword-Argumenten
person_info(alter=30, stadt="Berlin", name="Max")
```

### Default-Parameter

```python
def begruessung(name, anrede="Herr"):
    print(f"Guten Tag, {anrede} {name}!")

begruessung("Müller")           # Guten Tag, Herr Müller!
begruessung("Schmidt", "Frau")  # Guten Tag, Frau Schmidt!
```

!!! warning "Reihenfolge beachten"
    Parameter mit Default-Werten müssen **nach** Parametern ohne Default stehen:
    ```python
    # Richtig ✅
    def func(a, b, c=10):
    
    # Falsch ❌
    def func(a=10, b, c):  # SyntaxError
    ```

---

## Rückgabewerte

### Einfacher Rückgabewert

```python
def quadrat(x):
    return x ** 2

ergebnis = quadrat(5)  # 25
```

### Mehrere Rückgabewerte

```python
def statistik(zahlen):
    minimum = min(zahlen)
    maximum = max(zahlen)
    durchschnitt = sum(zahlen) / len(zahlen)
    return minimum, maximum, durchschnitt

# Rückgabe ist ein Tuple
mi, ma, avg = statistik([1, 2, 3, 4, 5])
print(f"Min: {mi}, Max: {ma}, Avg: {avg}")
```

### Kein Rückgabewert

```python
def ausgabe(text):
    print(text)
    # Kein return → gibt implizit None zurück

ergebnis = ausgabe("Test")
print(ergebnis)  # None
```

---

## Docstrings

Docstrings dokumentieren Funktionen und werden mit `"""` geschrieben:

```python
def berechne_bmi(gewicht, groesse):
    """
    Berechnet den Body-Mass-Index (BMI).
    
    Args:
        gewicht (float): Gewicht in Kilogramm
        groesse (float): Größe in Metern
    
    Returns:
        float: Der berechnete BMI-Wert
    
    Example:
        >>> berechne_bmi(75, 1.80)
        23.15
    """
    return gewicht / (groesse ** 2)

# Docstring abrufen
print(berechne_bmi.__doc__)
help(berechne_bmi)
```

---

## Variable Anzahl von Argumenten

### *args (beliebig viele Positionsargumente)

```python
def summe(*args):
    """Summiert beliebig viele Zahlen."""
    return sum(args)

print(summe(1, 2))           # 3
print(summe(1, 2, 3, 4, 5))  # 15
```

### **kwargs (beliebig viele Keyword-Argumente)

```python
def person_anlegen(**kwargs):
    """Erstellt ein Personen-Dictionary."""
    return kwargs

person = person_anlegen(name="Max", alter=30, stadt="Berlin")
print(person)  # {"name": "Max", "alter": 30, "stadt": "Berlin"}
```

### Kombiniert

```python
def flexible_funktion(pflicht, *args, **kwargs):
    print(f"Pflicht: {pflicht}")
    print(f"Args: {args}")
    print(f"Kwargs: {kwargs}")

flexible_funktion("A", "B", "C", x=1, y=2)
# Pflicht: A
# Args: ('B', 'C')
# Kwargs: {'x': 1, 'y': 2}
```

---

## Scope (Gültigkeitsbereich)

### Lokale und globale Variablen

```python
globale_var = "Ich bin global"

def beispiel():
    lokale_var = "Ich bin lokal"
    print(globale_var)  # Lesen geht
    print(lokale_var)   # OK

beispiel()
print(globale_var)  # OK
print(lokale_var)   # NameError! Nicht außerhalb sichtbar
```

### global-Keyword

```python
zaehler = 0

def erhoehe():
    global zaehler  # Zugriff auf globale Variable
    zaehler += 1

erhoehe()
erhoehe()
print(zaehler)  # 2
```

!!! warning "global vermeiden"
    Globale Variablen machen Code schwer nachvollziehbar. Besser: Werte als Parameter übergeben und zurückgeben.

---

## Lambda-Funktionen (Anonyme Funktionen)

Kurze, einzeilige Funktionen ohne Namen:

```python
# Normale Funktion
def quadrat(x):
    return x ** 2

# Als Lambda
quadrat = lambda x: x ** 2

print(quadrat(5))  # 25
```

### Praktischer Einsatz

```python
# Sortieren mit Lambda
personen = [
    {"name": "Max", "alter": 30},
    {"name": "Anna", "alter": 25},
    {"name": "Tom", "alter": 35}
]

# Nach Alter sortieren
sortiert = sorted(personen, key=lambda p: p["alter"])

# Nach Name sortieren
sortiert = sorted(personen, key=lambda p: p["name"])
```

### Mit map(), filter(), reduce()

```python
zahlen = [1, 2, 3, 4, 5]

# map: Funktion auf alle Elemente anwenden
quadrate = list(map(lambda x: x**2, zahlen))
# [1, 4, 9, 16, 25]

# filter: Elemente filtern
gerade = list(filter(lambda x: x % 2 == 0, zahlen))
# [2, 4]

# reduce: Auf einen Wert reduzieren
from functools import reduce
summe = reduce(lambda a, b: a + b, zahlen)
# 15
```

!!! tip "List Comprehensions oft besser"
    Statt `list(map(lambda x: x**2, zahlen))` ist `[x**2 for x in zahlen]` oft lesbarer.

---

## Funktionen als Parameter

Funktionen können an andere Funktionen übergeben werden:

```python
def ausfuehren(func, wert):
    """Führt eine Funktion mit einem Wert aus."""
    return func(wert)

def verdoppeln(x):
    return x * 2

def quadrieren(x):
    return x ** 2

print(ausfuehren(verdoppeln, 5))   # 10
print(ausfuehren(quadrieren, 5))   # 25
```

### Praxisbeispiel: Daten transformieren

```python
def transformiere_daten(daten, transform_func):
    """Wendet eine Transformation auf alle Daten an."""
    return [transform_func(d) for d in daten]

messwerte = [23.5, 19.2, 28.7, 22.1]

# Verschiedene Transformationen
gerundet = transformiere_daten(messwerte, round)
normalisiert = transformiere_daten(messwerte, lambda x: x / max(messwerte))
```

---

## Type Hints (Typhinweise)

Python 3.5+ unterstützt optionale Typhinweise:

```python
def berechne_durchschnitt(zahlen: list[float]) -> float:
    """Berechnet den Durchschnitt einer Zahlenliste."""
    return sum(zahlen) / len(zahlen)

def begruessung(name: str, alter: int = 0) -> str:
    return f"Hallo {name}, du bist {alter} Jahre alt."
```

!!! info "Type Hints sind optional"
    Python prüft die Typen **nicht** zur Laufzeit. Type Hints dienen der Dokumentation und können von IDEs und Tools wie `mypy` genutzt werden.

---

## Praxisbeispiele

### Datenvalidierung

```python
def validiere_email(email: str) -> bool:
    """Prüft ob eine E-Mail-Adresse gültig ist."""
    return "@" in email and "." in email.split("@")[-1]

def validiere_alter(alter: int) -> tuple[bool, str]:
    """Validiert ein Alter und gibt Status + Nachricht zurück."""
    if alter < 0:
        return False, "Alter kann nicht negativ sein"
    if alter > 150:
        return False, "Unplausibles Alter"
    return True, "OK"
```

### Datenbereinigung

```python
def bereinige_werte(daten: list, min_wert: float = 0, max_wert: float = float('inf')) -> list:
    """
    Entfernt Werte außerhalb des gültigen Bereichs.
    
    Args:
        daten: Liste von Zahlen
        min_wert: Minimaler gültiger Wert
        max_wert: Maximaler gültiger Wert
    
    Returns:
        Bereinigte Liste
    """
    return [x for x in daten if min_wert <= x <= max_wert]

messwerte = [23.5, -5, 28.7, 999, 22.1]
sauber = bereinige_werte(messwerte, min_wert=0, max_wert=100)
# [23.5, 28.7, 22.1]
```

---

## Zusammenfassung

!!! success "Das Wichtigste"
    - `def name(parameter): return wert`
    - Default-Parameter: `def func(a, b=10)`
    - Mehrere Rückgabewerte: `return a, b, c`
    - `*args` für variable Positionsargumente
    - `**kwargs` für variable Keyword-Argumente
    - Lambda: `lambda x: x * 2`
    - Docstrings für Dokumentation

---

??? question "Selbstkontrolle"
    1. Was ist der Unterschied zwischen Parameter und Argument?
    2. Was gibt eine Funktion ohne `return` zurück?
    3. Schreibe eine Funktion `maximum`, die beliebig viele Zahlen akzeptiert und die größte zurückgibt.
    
    ??? success "Antworten"
        1. **Parameter** sind die Variablen in der Funktionsdefinition, **Argumente** sind die Werte beim Aufruf
        2. `None`
        3. 
        ```python
        def maximum(*args):
            return max(args)
        # oder
        def maximum(*args):
            if not args:
                return None
            result = args[0]
            for x in args:
                if x > result:
                    result = x
            return result
        ```

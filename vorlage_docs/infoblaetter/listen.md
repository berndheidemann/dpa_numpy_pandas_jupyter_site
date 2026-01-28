# Listen

## Was sind Listen?

Listen sind **geordnete, veränderbare** Sammlungen von Elementen. Sie können verschiedene Datentypen enthalten.

```python
# Leere Liste
leere_liste = []

# Liste mit Zahlen
umsaetze = [1200, 1500, 1800, 1400]

# Liste mit Strings
kunden = ["Max", "Anna", "Tom"]

# Gemischte Liste (möglich, aber selten sinnvoll)
gemischt = [1, "Text", 3.14, True]
```

---

## Zugriff auf Elemente

### Visualisierung: Indizierung

| Index | 0 | 1 | 2 | 3 |
|:-----:|:---:|:---:|:---:|:---:|
| **Element** | Laptop | Mouse | Keyboard | Monitor |
| **Neg. Index** | -4 | -3 | -2 | -1 |

- **Index 0 / -4**: Erstes Element
- **Index 3 / -1**: Letztes Element

### Indizierung

Listen sind **0-indiziert** (erstes Element hat Index 0).

```python
produkte = ["Laptop", "Mouse", "Keyboard", "Monitor"]

print(produkte[0])   # Laptop (erstes Element)
print(produkte[1])   # Mouse (zweites Element)
print(produkte[-1])  # Monitor (letztes Element)
print(produkte[-2])  # Keyboard (vorletztes Element)
```

| Index | 0 | 1 | 2 | 3 |
|-------|---|---|---|---|
| Element | Laptop | Mouse | Keyboard | Monitor |
| Neg. Index | -4 | -3 | -2 | -1 |

### Element ändern

```python
produkte[1] = "Maus"  # Mouse → Maus
print(produkte)  # ["Laptop", "Maus", "Keyboard", "Monitor"]
```

---

## Slicing (Teilbereiche)

Mit Slicing können Teilbereiche einer Liste extrahiert werden.

### Syntax

```python
liste[start:stop:step]
```

- `start`: Startindex (inklusive), Standard: 0
- `stop`: Endindex (exklusive), Standard: Ende
- `step`: Schrittweite, Standard: 1

### Beispiele

```python
zahlen = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(zahlen[2:5])    # [2, 3, 4]
print(zahlen[:4])     # [0, 1, 2, 3] (vom Anfang)
print(zahlen[6:])     # [6, 7, 8, 9] (bis zum Ende)
print(zahlen[::2])    # [0, 2, 4, 6, 8] (jedes zweite)
print(zahlen[::-1])   # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0] (umgekehrt)
print(zahlen[-3:])    # [7, 8, 9] (letzte 3)
print(zahlen[1:7:2])  # [1, 3, 5] (Index 1-6, jedes zweite)
```

### Kopie einer Liste

```python
original = [1, 2, 3]
kopie = original[:]  # Flache Kopie

# ACHTUNG: Zuweisung kopiert NICHT!
referenz = original  # Zeigt auf dieselbe Liste!
referenz[0] = 999
print(original)  # [999, 2, 3] - Original auch geändert!
```

---

## Listen-Methoden

### Elemente hinzufügen

| Methode | Beschreibung | Beispiel |
|---------|--------------|----------|
| `append(x)` | Fügt x am Ende hinzu | `liste.append(4)` |
| `insert(i, x)` | Fügt x an Position i ein | `liste.insert(0, "Start")` |
| `extend(iter)` | Fügt alle Elemente hinzu | `liste.extend([4, 5, 6])` |

```python
daten = [1, 2, 3]

daten.append(4)        # [1, 2, 3, 4]
daten.insert(0, 0)     # [0, 1, 2, 3, 4]
daten.extend([5, 6])   # [0, 1, 2, 3, 4, 5, 6]

# + Operator erstellt NEUE Liste
neue_liste = daten + [7, 8]  # Original bleibt unverändert
```

### Elemente entfernen

| Methode | Beschreibung | Beispiel |
|---------|--------------|----------|
| `remove(x)` | Entfernt erstes x | `liste.remove("Max")` |
| `pop()` | Entfernt und gibt letztes Element zurück | `letztes = liste.pop()` |
| `pop(i)` | Entfernt und gibt Element an Index i zurück | `erstes = liste.pop(0)` |
| `clear()` | Entfernt alle Elemente | `liste.clear()` |

```python
namen = ["Max", "Anna", "Tom", "Anna"]

namen.remove("Anna")   # ["Max", "Tom", "Anna"] (nur erstes!)
letzter = namen.pop()  # "Anna", Namen = ["Max", "Tom"]
namen.clear()          # []
```

!!! warning "Fehler bei remove()"
    `remove()` wirft einen `ValueError`, wenn das Element nicht existiert:
    ```python
    namen = ["Max", "Anna"]
    namen.remove("Tom")  # ValueError: list.remove(x): x not in list
    ```

### Suchen und Zählen

| Methode | Beschreibung | Beispiel |
|---------|--------------|----------|
| `index(x)` | Index des ersten x | `liste.index("Max")` → 0 |
| `count(x)` | Anzahl von x | `liste.count("a")` → 2 |
| `x in liste` | Prüft ob x enthalten | `"Max" in liste` → True |

```python
werte = [3, 1, 4, 1, 5, 9, 2, 6]

print(werte.index(4))    # 2
print(werte.count(1))    # 2
print(5 in werte)        # True
print(7 not in werte)    # True
```

### Sortieren und Umkehren

```python
zahlen = [3, 1, 4, 1, 5, 9, 2, 6]

# In-place sortieren (ändert Original)
zahlen.sort()           # [1, 1, 2, 3, 4, 5, 6, 9]
zahlen.sort(reverse=True)  # [9, 6, 5, 4, 3, 2, 1, 1]

# Neue sortierte Liste (Original bleibt)
sortiert = sorted(zahlen)

# Umkehren
zahlen.reverse()        # Kehrt Liste um

# Länge
print(len(zahlen))      # 8
```

---

## List Comprehensions

Eine kompakte Syntax zum Erstellen von Listen.

### Grundsyntax

```python
neue_liste = [ausdruck for element in sequenz]
```

### Beispiele

```python
# Quadratzahlen
quadrate = [x**2 for x in range(1, 6)]
# [1, 4, 9, 16, 25]

# Strings zu Großbuchstaben
namen = ["max", "anna", "tom"]
gross = [name.upper() for name in namen]
# ["MAX", "ANNA", "TOM"]

# Mit Bedingung (Filter)
zahlen = [1, -2, 3, -4, 5]
positiv = [x for x in zahlen if x > 0]
# [1, 3, 5]

# Mit if-else (Transformation)
absolut = [x if x >= 0 else -x for x in zahlen]
# [1, 2, 3, 4, 5]
```

### Vergleich mit Schleife

```python
# Mit Schleife
ergebnis = []
for x in range(10):
    if x % 2 == 0:
        ergebnis.append(x * 2)

# Mit List Comprehension ✨
ergebnis = [x * 2 for x in range(10) if x % 2 == 0]
# [0, 4, 8, 12, 16]
```

!!! tip "Lesbarkeit beachten"
    List Comprehensions sind mächtig, aber bei komplexen Ausdrücken wird eine normale Schleife besser lesbar.

---

## Verschachtelte Listen (2D)

Listen können andere Listen enthalten:

```python
# 2D-Matrix (Liste von Listen)
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Zugriff: matrix[zeile][spalte]
print(matrix[0][0])  # 1 (oben links)
print(matrix[1][2])  # 6 (Zeile 2, Spalte 3)
print(matrix[2])     # [7, 8, 9] (ganze Zeile)

# Ändern
matrix[1][1] = 99    # 5 → 99
```

### Iteration über 2D-Listen

```python
sensordaten = [
    [22, 24, 19, 23],  # Sensor 1
    [18, 22, 21, 25],  # Sensor 2
    [20, 23, 22, 27],  # Sensor 3
]

# Alle Werte ausgeben
for zeile in sensordaten:
    for wert in zeile:
        print(wert, end=" ")
    print()

# Mit Indizes
for i in range(len(sensordaten)):
    for j in range(len(sensordaten[i])):
        print(f"[{i}][{j}] = {sensordaten[i][j]}")
```

### 2D List Comprehension

```python
# 3x4 Matrix mit Nullen
matrix = [[0 for _ in range(4)] for _ in range(3)]
# [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]

# Transponieren (Zeilen ↔ Spalten)
original = [[1, 2, 3], [4, 5, 6]]
transponiert = [[zeile[i] for zeile in original] for i in range(3)]
# [[1, 4], [2, 5], [3, 6]]
```

---

## Nützliche Funktionen

| Funktion | Beschreibung | Beispiel |
|----------|--------------|----------|
| `len(liste)` | Anzahl Elemente | `len([1,2,3])` → 3 |
| `sum(liste)` | Summe | `sum([1,2,3])` → 6 |
| `min(liste)` | Minimum | `min([3,1,4])` → 1 |
| `max(liste)` | Maximum | `max([3,1,4])` → 4 |
| `sorted(liste)` | Sortierte Kopie | `sorted([3,1,4])` → [1,3,4] |
| `list(seq)` | Sequenz → Liste | `list("abc")` → ['a','b','c'] |

### Statistik-Beispiel

```python
messwerte = [23.5, 19.2, 28.7, 22.1, 25.9, 21.3]

anzahl = len(messwerte)
summe = sum(messwerte)
durchschnitt = summe / anzahl
minimum = min(messwerte)
maximum = max(messwerte)

print(f"Anzahl: {anzahl}")
print(f"Summe: {summe:.1f}")
print(f"Durchschnitt: {durchschnitt:.2f}")
print(f"Min: {minimum}, Max: {maximum}")
```

---

## Praxisbeispiel: Datenbereinigung

```python
rohdaten = [1200, -50, 1500, 99999, 1800, None, 1400, -100]

# Ungültige Werte entfernen
def bereinige_daten(daten):
    return [x for x in daten if x is not None and 0 <= x <= 10000]

saubere_daten = bereinige_daten(rohdaten)
print(saubere_daten)  # [1200, 1500, 1800, 1400]
```

---

## Tuple – Unveränderliche Listen

Tuple sind wie Listen, aber **unveränderlich** (immutable). Nach der Erstellung können sie nicht mehr geändert werden.

```python
# Tuple erstellen
koordinate = (10, 20)
rgb_farbe = (255, 128, 0)
person = ("Max", 30, "Berlin")

# Auch ohne Klammern möglich
punkt = 5, 10

# Einelementige Tuple brauchen ein Komma!
einzel = (42,)     # Tuple
nicht_tuple = (42)  # Das ist nur eine Zahl!
```

### Zugriff (wie bei Listen)

```python
person = ("Max", 30, "Berlin")

print(person[0])   # "Max"
print(person[-1])  # "Berlin"
print(person[1:])  # (30, "Berlin")
```

### Was geht NICHT

```python
person = ("Max", 30, "Berlin")

# Ändern nicht möglich!
person[0] = "Anna"  # TypeError: 'tuple' object does not support item assignment

# Hinzufügen nicht möglich!
person.append("Entwickler")  # AttributeError: 'tuple' object has no attribute 'append'
```

### Wann Tuple statt Listen?

| Verwende **Tuple** wenn... | Verwende **Liste** wenn... |
|---------------------------|---------------------------|
| Daten nicht geändert werden sollen | Elemente hinzugefügt/entfernt werden |
| Feste Anzahl von Werten (z.B. Koordinaten) | Variable Anzahl von Elementen |
| Als Dictionary-Schlüssel | Sortieren/Ändern nötig |
| Mehrere Rückgabewerte einer Funktion | Sammlung gleichartiger Daten |

### Mehrere Rückgabewerte

```python
def min_max(werte):
    """Gibt Minimum und Maximum zurück."""
    return min(werte), max(werte)

# Tuple entpacken
daten = [3, 1, 4, 1, 5, 9, 2, 6]
kleinster, groesster = min_max(daten)

print(f"Min: {kleinster}, Max: {groesster}")
```

### Tuple-Unpacking

```python
# Mehrere Werte gleichzeitig zuweisen
x, y, z = (1, 2, 3)

# Praktisch: Werte tauschen
a, b = 10, 20
a, b = b, a  # a=20, b=10

# Rest sammeln mit *
erste, *rest = (1, 2, 3, 4, 5)
# erste = 1, rest = [2, 3, 4, 5]

erste, *mitte, letzte = (1, 2, 3, 4, 5)
# erste = 1, mitte = [2, 3, 4], letzte = 5
```

### Als Dictionary-Schlüssel

```python
# Tuple können Dict-Schlüssel sein (Listen nicht!)
positionen = {
    (0, 0): "Start",
    (10, 5): "Checkpoint A",
    (20, 10): "Ziel"
}

print(positionen[(10, 5)])  # "Checkpoint A"

# Liste als Schlüssel → Fehler
# {[0, 0]: "Start"}  # TypeError: unhashable type: 'list'
```

---

## Zusammenfassung

!!! success "Das Wichtigste"
    - Listen sind veränderbar und geordnet
    - Indizierung startet bei 0, negative Indizes vom Ende
    - Slicing: `liste[start:stop:step]`
    - `append()`, `insert()`, `extend()` zum Hinzufügen
    - `remove()`, `pop()`, `clear()` zum Entfernen
    - List Comprehensions für kompakte Erstellung
    - 2D-Listen: `matrix[zeile][spalte]`

---

??? question "Selbstkontrolle"
    1. Was ist der Unterschied zwischen `append()` und `extend()`?
    2. Was gibt `[1, 2, 3, 4, 5][1:4]` zurück?
    3. Schreibe eine List Comprehension für alle geraden Zahlen von 0-20.
    
    ??? success "Antworten"
        1. `append()` fügt ein einzelnes Element hinzu, `extend()` fügt alle Elemente einer Sequenz hinzu
        2. `[2, 3, 4]`
        3. `[x for x in range(21) if x % 2 == 0]` oder `[x for x in range(0, 21, 2)]`

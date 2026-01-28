# Schleifen

## while-Schleife

Die `while`-Schleife wiederholt einen Codeblock, **solange** eine Bedingung wahr ist.

```kroki-plantuml
@startuml
skinparam ActivityBackgroundColor #f5f5f5
skinparam ActivityBorderColor #333
skinparam DiamondBackgroundColor #ffe6f0
skinparam DiamondBorderColor #333

start
:Variable initialisieren;
while (Bedingung wahr?) is (ja)
  :Code ausführen;
  :Variable ändern;
endwhile (nein)
stop
@enduml
```

### Syntax

```python
while bedingung:
    # Code der wiederholt wird
    anweisungen
```

### Beispiele

```python
# Countdown
zaehler = 5
while zaehler > 0:
    print(zaehler)
    zaehler -= 1
print("Start!")

# Ausgabe: 5, 4, 3, 2, 1, Start!
```

```python
# Eingabevalidierung
eingabe = ""
while eingabe == "":
    eingabe = input("Bitte Namen eingeben: ")
print(f"Hallo, {eingabe}!")
```

!!! danger "Endlosschleifen vermeiden"
    Stelle sicher, dass die Bedingung irgendwann `False` wird!
    ```python
    # FEHLER - Endlosschleife!
    x = 1
    while x > 0:
        print(x)
        # x wird nie verändert → Schleife läuft ewig
    ```

---

## for-Schleife

Die `for`-Schleife iteriert über eine **Sequenz** (Liste, String, Range, etc.).

```kroki-plantuml
@startuml
skinparam ActivityBackgroundColor #f5f5f5
skinparam ActivityBorderColor #333
skinparam DiamondBackgroundColor #e6f0ff
skinparam DiamondBorderColor #333

start
:Sequenz bereitstellen;
while (Elemente übrig?) is (ja)
  :Nächstes Element holen;
  :Code ausführen;
endwhile (nein)
stop
@enduml
```

### Syntax

```python
for element in sequenz:
    # Code für jedes Element
    anweisungen
```

### Beispiele

```python
# Über eine Liste iterieren
umsaetze = [1200, 1500, 1800, 1400]
for umsatz in umsaetze:
    print(f"Umsatz: {umsatz} €")

# Über einen String iterieren
for zeichen in "Python":
    print(zeichen)

# Über ein Dictionary iterieren
person = {"name": "Max", "alter": 25}
for key in person:
    print(f"{key}: {person[key]}")
```

---

## range() - Zahlenfolgen generieren

Die `range()`-Funktion erzeugt eine Folge von Zahlen.

### Varianten

| Aufruf | Erzeugt | Beispiel |
|--------|---------|----------|
| `range(stop)` | 0 bis stop-1 | `range(5)` → 0,1,2,3,4 |
| `range(start, stop)` | start bis stop-1 | `range(2, 6)` → 2,3,4,5 |
| `range(start, stop, step)` | Mit Schrittweite | `range(0, 10, 2)` → 0,2,4,6,8 |

### Beispiele

```python
# 0 bis 4
for i in range(5):
    print(i)

# 1 bis 10
for i in range(1, 11):
    print(i)

# Gerade Zahlen von 0 bis 20
for i in range(0, 21, 2):
    print(i)

# Rückwärts zählen
for i in range(10, 0, -1):
    print(i)
```

### Praxisbeispiel: Tabelle ausgeben

```python
# Multiplikationstabelle
for i in range(1, 11):
    for j in range(1, 11):
        print(f"{i*j:4}", end="")
    print()  # Zeilenumbruch
```

---

## enumerate() - Index und Wert

Wenn du sowohl den **Index** als auch den **Wert** brauchst:

```python
produkte = ["Laptop", "Mouse", "Keyboard"]

# Ohne enumerate (umständlich)
for i in range(len(produkte)):
    print(f"{i}: {produkte[i]}")

# Mit enumerate (pythonisch) ✨
for index, produkt in enumerate(produkte):
    print(f"{index}: {produkt}")

# Mit Startindex 1
for nr, produkt in enumerate(produkte, start=1):
    print(f"{nr}. {produkt}")
```

---

## zip() - Parallel iterieren

Iteriert über mehrere Sequenzen gleichzeitig:

```python
namen = ["Max", "Anna", "Tom"]
punkte = [85, 92, 78]

for name, punkt in zip(namen, punkte):
    print(f"{name}: {punkt} Punkte")

# Ausgabe:
# Max: 85 Punkte
# Anna: 92 Punkte
# Tom: 78 Punkte
```

### Drei Listen kombinieren

```python
ids = [1, 2, 3]
namen = ["Max", "Anna", "Tom"]
gehälter = [3500, 4200, 3800]

for id, name, gehalt in zip(ids, namen, gehälter):
    print(f"ID {id}: {name} verdient {gehalt} €")
```

!!! info "Unterschiedliche Längen"
    `zip()` stoppt beim kürzesten Element. Für das längste Element nutze `itertools.zip_longest()`.

---

## Schleifensteuerung

### break - Schleife abbrechen

```python
# Suche nach einem Wert
zahlen = [4, 7, 2, 9, 1, 5]
gesucht = 9

for zahl in zahlen:
    if zahl == gesucht:
        print(f"Gefunden: {zahl}")
        break  # Schleife sofort beenden
    print(f"Prüfe: {zahl}")
```

### continue - Durchlauf überspringen

```python
# Nur positive Werte verarbeiten
werte = [5, -3, 8, -1, 4, -7, 2]

for wert in werte:
    if wert < 0:
        continue  # Negative Werte überspringen
    print(f"Verarbeite: {wert}")
```

### else bei Schleifen

Der `else`-Block wird ausgeführt, wenn die Schleife **ohne `break`** beendet wurde:

```python
# Primzahltest
n = 17

for i in range(2, n):
    if n % i == 0:
        print(f"{n} ist keine Primzahl (teilbar durch {i})")
        break
else:
    # Wird nur ausgeführt, wenn kein break
    print(f"{n} ist eine Primzahl")
```

---

## Verschachtelte Schleifen

```python
# 2D-Matrix durchlaufen
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

for zeile in matrix:
    for wert in zeile:
        print(wert, end=" ")
    print()  # Neue Zeile

# Mit Indizes
for i in range(len(matrix)):
    for j in range(len(matrix[i])):
        print(f"matrix[{i}][{j}] = {matrix[i][j]}")
```

---

## Praxisbeispiele

### Summe berechnen

```python
umsaetze = [1200, 1500, 1800, 1400, 2100]

summe = 0
for umsatz in umsaetze:
    summe += umsatz

print(f"Gesamtumsatz: {summe} €")

# Kürzer mit sum()
print(f"Gesamtumsatz: {sum(umsaetze)} €")
```

### Maximum finden

```python
messwerte = [23.5, 19.2, 28.7, 22.1, 25.9]

maximum = messwerte[0]
for wert in messwerte:
    if wert > maximum:
        maximum = wert

print(f"Maximum: {maximum}")

# Kürzer mit max()
print(f"Maximum: {max(messwerte)}")
```

### Daten filtern

```python
response_times = [45, 120, 890, 56, 234, 2100, 78, 167]
grenzwert = 500

langsame_requests = []
for zeit in response_times:
    if zeit > grenzwert:
        langsame_requests.append(zeit)

print(f"Langsame Requests: {langsame_requests}")
```

### Eingabe mit Abbruchbedingung

```python
messwerte = []

print("Geben Sie Messwerte ein (-1 zum Beenden):")
while True:
    eingabe = float(input("Wert: "))
    if eingabe == -1:
        break
    messwerte.append(eingabe)

print(f"Erfasste Werte: {messwerte}")
print(f"Durchschnitt: {sum(messwerte) / len(messwerte):.2f}")
```

---

## while vs. for

| Situation | Empfehlung |
|-----------|------------|
| Bekannte Anzahl Durchläufe | `for` mit `range()` |
| Über Sequenz iterieren | `for` |
| Unbekannte Anzahl Durchläufe | `while` |
| Benutzereingabe validieren | `while` |
| Bis Bedingung erfüllt | `while` |

---

## Zusammenfassung

!!! success "Das Wichtigste"
    - `while`: Wiederholt solange Bedingung wahr
    - `for`: Iteriert über Sequenzen
    - `range(start, stop, step)`: Zahlenfolgen generieren
    - `enumerate()`: Index + Wert
    - `zip()`: Parallel über mehrere Listen
    - `break`: Schleife abbrechen
    - `continue`: Durchlauf überspringen

---

??? question "Selbstkontrolle"
    1. Was ist der Unterschied zwischen `range(5)` und `range(1, 6)`?
    2. Wann verwendet man `while`, wann `for`?
    3. Was gibt `range(10, 0, -2)` aus?
    
    ??? success "Antworten"
        1. `range(5)` → 0,1,2,3,4 / `range(1, 6)` → 1,2,3,4,5 (gleiche Anzahl, andere Werte)
        2. `for` bei bekannter Anzahl oder Sequenzen, `while` bei unbekannter Anzahl oder Bedingungen
        3. 10, 8, 6, 4, 2 (rückwärts in 2er-Schritten)

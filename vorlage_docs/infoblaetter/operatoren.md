# Operatoren und Ausdrücke

## Arithmetische Operatoren

| Operator | Beschreibung | Beispiel | Ergebnis |
|----------|--------------|----------|----------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraktion | `5 - 3` | `2` |
| `*` | Multiplikation | `5 * 3` | `15` |
| `/` | Division (Kommazahl) | `7 / 2` | `3.5` |
| `//` | Ganzzahldivision | `7 // 2` | `3` |
| `%` | Modulo (Rest) | `7 % 2` | `1` |
| `**` | Potenz | `2 ** 3` | `8` |

### Beispiele

```python
# Division vs. Ganzzahldivision
print(7 / 2)   # 3.5 (float)
print(7 // 2)  # 3 (int)

# Modulo - praktisch für:
# - Gerade/Ungerade prüfen
print(10 % 2)  # 0 → gerade
print(11 % 2)  # 1 → ungerade

# - Zyklische Werte (z.B. Wochentage)
tag = 10 % 7  # 3 → Mittwoch (wenn 0=Sonntag)

# Potenz
print(2 ** 10)    # 1024
print(9 ** 0.5)   # 3.0 (Quadratwurzel)
```

---

## Vergleichsoperatoren

| Operator | Beschreibung | Beispiel | Ergebnis |
|----------|--------------|----------|----------|
| `==` | Gleich | `5 == 5` | `True` |
| `!=` | Ungleich | `5 != 3` | `True` |
| `<` | Kleiner als | `3 < 5` | `True` |
| `>` | Größer als | `5 > 3` | `True` |
| `<=` | Kleiner oder gleich | `5 <= 5` | `True` |
| `>=` | Größer oder gleich | `3 >= 5` | `False` |

### Beispiele

```python
alter = 25

print(alter == 25)   # True
print(alter != 30)   # True
print(alter >= 18)   # True
print(alter < 18)    # False

# Vergleiche liefern bool-Werte
ergebnis = alter >= 18  # ergebnis = True
```

!!! warning "Häufiger Fehler"
    Verwechsle nicht `=` (Zuweisung) mit `==` (Vergleich)!
    ```python
    x = 5    # Zuweisung: x bekommt den Wert 5
    x == 5   # Vergleich: Ist x gleich 5? → True
    ```

---

## Logische Operatoren

| Operator | Beschreibung | Beispiel | Ergebnis |
|----------|--------------|----------|----------|
| `and` | UND - beide wahr | `True and False` | `False` |
| `or` | ODER - mindestens eines wahr | `True or False` | `True` |
| `not` | NICHT - Negation | `not True` | `False` |

### Wahrheitstabellen

**AND (UND)**

| A | B | A and B |
|---|---|---------|
| True | True | True |
| True | False | False |
| False | True | False |
| False | False | False |

**OR (ODER)**

| A | B | A or B |
|---|---|--------|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | False |

### Praxisbeispiele

```python
alter = 25
einkommen = 3500
hat_kredit = False

# Kreditwürdigkeitsprüfung
if alter >= 18 and einkommen >= 2000:
    print("Grundvoraussetzungen erfüllt")

# Risikoprüfung
if einkommen < 1500 or hat_kredit:
    print("Erhöhtes Risiko")

# Negation
if not hat_kredit:
    print("Keine bestehenden Kredite")

# Komplexe Bedingung
if (alter >= 18 and einkommen >= 2000) and not hat_kredit:
    print("Kredit genehmigt")
```

!!! tip "Kurzschlussauswertung"
    Python wertet logische Ausdrücke von links nach rechts aus und bricht ab, sobald das Ergebnis feststeht:
    
    - `False and ...` → Rest wird nicht geprüft (Ergebnis ist `False`)
    - `True or ...` → Rest wird nicht geprüft (Ergebnis ist `True`)

---

## Zuweisungsoperatoren

| Operator | Beschreibung | Äquivalent zu |
|----------|--------------|---------------|
| `=` | Zuweisung | - |
| `+=` | Addition und Zuweisung | `x = x + 5` |
| `-=` | Subtraktion und Zuweisung | `x = x - 5` |
| `*=` | Multiplikation und Zuweisung | `x = x * 5` |
| `/=` | Division und Zuweisung | `x = x / 5` |
| `//=` | Ganzzahldivision und Zuweisung | `x = x // 5` |
| `%=` | Modulo und Zuweisung | `x = x % 5` |
| `**=` | Potenz und Zuweisung | `x = x ** 5` |

### Beispiele

```python
punkte = 100

punkte += 10   # punkte = 110
punkte -= 5    # punkte = 105
punkte *= 2    # punkte = 210
punkte //= 3   # punkte = 70

# Häufig in Schleifen
summe = 0
for wert in [10, 20, 30]:
    summe += wert  # summe = 60
```

---

## Typumwandlung (Casting)

| Funktion | Beschreibung | Beispiel | Ergebnis |
|----------|--------------|----------|----------|
| `int()` | In Ganzzahl | `int("42")` | `42` |
| `float()` | In Kommazahl | `float("3.14")` | `3.14` |
| `str()` | In String | `str(42)` | `"42"` |
| `bool()` | In Boolean | `bool(1)` | `True` |

### Beispiele

```python
# String zu Zahl
alter_text = "25"
alter = int(alter_text)     # 25
preis = float("19.99")      # 19.99

# Zahl zu String
id_nummer = 12345
id_text = str(id_nummer)    # "12345"

# Runden
wert = 3.7
print(int(wert))            # 3 (Abschneiden, nicht Runden!)
print(round(wert))          # 4 (Runden)
print(round(3.14159, 2))    # 3.14 (2 Dezimalstellen)

# Bool-Konvertierung
print(bool(0))      # False
print(bool(1))      # True
print(bool(""))     # False (leerer String)
print(bool("text")) # True (nicht-leerer String)
print(bool([]))     # False (leere Liste)
print(bool([1,2]))  # True (nicht-leere Liste)
```

!!! info "Falsy-Werte in Python"
    Folgende Werte werden als `False` interpretiert:
    
    - `0`, `0.0`
    - `""` (leerer String)
    - `[]`, `()`, `{}` (leere Collections)
    - `None`
    
    Alles andere ist `True` ("truthy").

---

## Operatorrangfolge (Priorität)

Von hoch nach niedrig:

| Priorität | Operator |
|-----------|----------|
| 1 | `**` |
| 2 | `*`, `/`, `//`, `%` |
| 3 | `+`, `-` |
| 4 | `<`, `<=`, `>`, `>=`, `==`, `!=` |
| 5 | `not` |
| 6 | `and` |
| 7 | `or` |

### Beispiele

```python
# Punkt vor Strich
print(2 + 3 * 4)      # 14 (nicht 20)
print((2 + 3) * 4)    # 20 (Klammern ändern Reihenfolge)

# Potenz vor Multiplikation
print(2 * 3 ** 2)     # 18 (= 2 * 9)

# Vergleich vor Logik
print(5 > 3 and 2 < 4)  # True (= True and True)

# Im Zweifel: Klammern setzen!
ergebnis = ((a > b) and (c < d)) or (e == f)
```

---

## Membership-Operatoren

| Operator | Beschreibung | Beispiel |
|----------|--------------|----------|
| `in` | Element enthalten | `"a" in "Hallo"` → `True` |
| `not in` | Element nicht enthalten | `5 not in [1,2,3]` → `True` |

```python
# In Strings
print("Python" in "Ich lerne Python")  # True

# In Listen
zahlen = [1, 2, 3, 4, 5]
print(3 in zahlen)      # True
print(10 not in zahlen) # True

# In Dictionaries (prüft Keys!)
person = {"name": "Max", "alter": 25}
print("name" in person)   # True
print("Max" in person)    # False (prüft Keys, nicht Values)
```

---

## Zusammenfassung

!!! success "Das Wichtigste"
    - `/` liefert immer `float`, `//` immer `int`
    - `%` ist nützlich für Teilbarkeit und zyklische Werte
    - `and`/`or`/`not` für logische Verknüpfungen
    - `+=`, `-=` etc. als Kurzformen
    - Im Zweifel: **Klammern setzen!**

---

??? question "Selbstkontrolle"
    1. Was ist das Ergebnis von `17 // 5` und `17 % 5`?
    2. Was ergibt `True and False or True`?
    3. Wie prüfst du, ob eine Zahl durch 3 teilbar ist?
    
    ??? success "Antworten"
        1. `17 // 5 = 3` (Ganzzahldivision), `17 % 5 = 2` (Rest)
        2. `True` (weil `and` vor `or` ausgewertet wird: `False or True = True`)
        3. `zahl % 3 == 0`

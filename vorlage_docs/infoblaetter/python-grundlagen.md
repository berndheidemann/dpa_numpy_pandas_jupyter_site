# Python-Grundlagen

## Installation & IDE-Setup

### Python installieren

1. **Download:** [python.org/downloads](https://www.python.org/downloads/)
2. **Installation:** Installer ausführen, dabei **"Add Python to PATH"** aktivieren
3. **Überprüfen:** Terminal öffnen und eingeben:
   ```bash
   python --version
   ```

### VS Code einrichten

1. **VS Code installieren:** [code.visualstudio.com](https://code.visualstudio.com/)
2. **Python Extension installieren:** Extensions (Ctrl+Shift+X) → "Python" suchen → Installieren
3. **Interpreter auswählen:** Ctrl+Shift+P → "Python: Select Interpreter"

---

## Erstes Programm

```python
print("Hello, World!")
```

!!! tip "Ausführen"
    - **VS Code:** Rechtsklick → "Run Python File in Terminal"
    - **Terminal:** `python dateiname.py`

---

## Syntax-Grundregeln

### Einrückung ist wichtig!

Python verwendet **Einrückung** (Indentation) statt geschweifter Klammern, um Codeblöcke zu definieren.

```python
# Richtig ✅
if x > 0:
    print("positiv")
    print("Zahl ist größer als Null")

# Falsch ❌ - führt zu IndentationError
if x > 0:
print("positiv")
```

!!! warning "Konsistenz"
    Verwende **immer 4 Leerzeichen** für eine Einrückungsebene. Mische niemals Tabs und Leerzeichen!

### Keine Semikolons nötig

```python
# Python - kein Semikolon am Zeilenende
x = 5
y = 10

# Mehrere Anweisungen in einer Zeile (selten verwendet)
x = 5; y = 10
```

### Groß-/Kleinschreibung beachten

```python
name = "Max"
Name = "Anna"  # Das sind zwei verschiedene Variablen!
```

---

## Variablen und Datentypen

### Variablen deklarieren

In Python muss der Datentyp **nicht** explizit angegeben werden:

```python
# Zuweisung ohne Typangabe
alter = 25
name = "Max Mustermann"
gehalt = 3500.50
ist_aktiv = True
```

### Grundlegende Datentypen

| Typ | Beschreibung | Beispiel |
|-----|--------------|----------|
| `int` | Ganze Zahlen | `42`, `-17`, `0` |
| `float` | Kommazahlen | `3.14`, `-0.5`, `1e10` |
| `str` | Zeichenketten | `"Hallo"`, `'Welt'` |
| `bool` | Wahrheitswerte | `True`, `False` |
| `None` | Kein Wert / Leer | `None` |

### Typ ermitteln

```python
x = 42
print(type(x))  # <class 'int'>

y = "Hallo"
print(type(y))  # <class 'str'>
```

---

## Ein- und Ausgabe

### Ausgabe mit `print()`

```python
# Einfache Ausgabe
print("Hallo Welt")

# Mehrere Werte
print("Name:", name, "Alter:", alter)

# Mit Formatierung (f-String) - empfohlen!
print(f"Name: {name}, Alter: {alter}")

# Alte Formatierung mit .format()
print("Name: {}, Alter: {}".format(name, alter))
```

### f-Strings im Detail

```python
preis = 19.99
menge = 3

# Einfache Einbettung
print(f"Preis: {preis} €")

# Mit Berechnung
print(f"Gesamt: {preis * menge} €")

# Formatierung: 2 Dezimalstellen
print(f"Gesamt: {preis * menge:.2f} €")

# Prozent-Formatierung
quote = 0.7534
print(f"Erfolgsquote: {quote:.1%}")  # Ausgabe: 75.3%
```

### Eingabe mit `input()`

```python
# Eingabe ist immer ein String!
name = input("Wie heißt du? ")
print(f"Hallo, {name}!")

# Für Zahlen: Typumwandlung erforderlich
alter_text = input("Wie alt bist du? ")
alter = int(alter_text)

# Oder direkt:
alter = int(input("Wie alt bist du? "))
gehalt = float(input("Dein Gehalt: "))
```

!!! danger "Fehlerquelle"
    `input()` gibt **immer einen String** zurück. Vergisst du die Umwandlung mit `int()` oder `float()`, führt das zu Fehlern bei Berechnungen!

---

## Kommentare

```python
# Einzeiliger Kommentar

x = 5  # Kommentar am Zeilenende

"""
Mehrzeiliger Kommentar
oder Docstring für Dokumentation
von Funktionen und Klassen
"""

'''
Alternativ mit einfachen
Anführungszeichen
'''
```

---

## Namenskonventionen

| Element | Konvention | Beispiel |
|---------|------------|----------|
| Variablen | snake_case | `kunden_anzahl`, `max_wert` |
| Konstanten | UPPER_SNAKE_CASE | `MAX_RETRIES`, `PI` |
| Funktionen | snake_case | `berechne_summe()` |
| Klassen | PascalCase | `DataAnalyzer`, `Customer` |

---

## String-Methoden

Strings haben viele nützliche Methoden:

### Groß-/Kleinschreibung

```python
text = "  Hallo Welt  "

text.upper()      # "  HALLO WELT  "
text.lower()      # "  hallo welt  "
text.title()      # "  Hallo Welt  "
text.capitalize() # "  hallo welt  " (nur 1. Zeichen groß)
```

### Leerzeichen entfernen

```python
text = "  Hallo Welt  "

text.strip()      # "Hallo Welt" (beide Seiten)
text.lstrip()     # "Hallo Welt  " (links)
text.rstrip()     # "  Hallo Welt" (rechts)
```

### Suchen und Ersetzen

```python
text = "Python ist toll"

text.find("ist")        # 7 (Index, wo gefunden)
text.find("Java")       # -1 (nicht gefunden)
text.replace("toll", "super")  # "Python ist super"
text.count("t")         # 2 (Anzahl Vorkommen)
```

### Prüfen

```python
text = "Python123"

text.startswith("Py")   # True
text.endswith("123")    # True
text.isdigit()          # False (enthält Buchstaben)
text.isalpha()          # False (enthält Zahlen)
text.isalnum()          # True (nur Buchstaben und Zahlen)

"   ".isspace()         # True (nur Leerzeichen)
```

### Aufteilen und Verbinden

```python
# String aufteilen → Liste
zeile = "Max;Mustermann;42"
teile = zeile.split(";")      # ["Max", "Mustermann", "42"]

# Mit beliebigem Trennzeichen
"a  b  c".split()             # ["a", "b", "c"] (Leerzeichen)
"2024-01-15".split("-")       # ["2024", "01", "15"]

# Liste verbinden → String
namen = ["Max", "Anna", "Tom"]
", ".join(namen)              # "Max, Anna, Tom"
"-".join(["2024", "01", "15"]) # "2024-01-15"
```

### Praktisches Beispiel

```python
# CSV-Zeile verarbeiten
zeile = "  Müller, Max; 42; Entwickler  "

# Bereinigen und aufteilen
zeile = zeile.strip()
teile = zeile.split(";")

# Einzelne Werte bereinigen
for teil in teile:
    print(teil.strip())

# Oder mit List Comprehension
werte = [t.strip() for t in zeile.split(";")]
# ["Müller, Max", "42", "Entwickler"]
```

!!! tip "Methoden-Verkettung"
    ```python
    # Mehrere Methoden kombinieren
    eingabe = "  PYTHON IST TOLL  "
    bereinigt = eingabe.strip().lower().replace(" ", "_")
    # "python_ist_toll"
    ```

---

## Zusammenfassung

!!! success "Das Wichtigste"
    - Python nutzt **Einrückung** statt Klammern
    - Variablen brauchen **keine Typdeklaration**
    - `input()` gibt immer **Strings** zurück
    - Verwende **f-Strings** für formatierte Ausgaben
    - Achte auf **Groß-/Kleinschreibung**

---

??? question "Selbstkontrolle"
    1. Was passiert, wenn du `print(5 + "3")` ausführst?
    2. Wie wandelst du den String `"42"` in eine Zahl um?
    3. Was ist der Unterschied zwischen `=` und `==`?
    
    ??? success "Antworten"
        1. Es gibt einen `TypeError`, da int und str nicht addiert werden können
        2. `int("42")` oder `float("42")`
        3. `=` ist Zuweisung, `==` ist Vergleich auf Gleichheit

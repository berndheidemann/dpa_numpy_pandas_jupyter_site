# Verzweigungen

## Grundstruktur

### Einfache if-Anweisung

```kroki-plantuml
@startuml
skinparam ActivityBackgroundColor #f5f5f5
skinparam ActivityBorderColor #333
skinparam DiamondBackgroundColor #ffe6f0
skinparam DiamondBorderColor #333

start
if (Bedingung?) then (True)
  :Block ausführen;
else (False)
endif
:Weiter;
stop
@enduml
```

```python
if bedingung:
    # Code wird ausgeführt, wenn Bedingung True ist
    anweisung1
    anweisung2
```

!!! warning "Einrückung ist Pflicht!"
    Der eingerückte Block gehört zur if-Anweisung. Falsche Einrückung führt zu Fehlern oder unerwartetem Verhalten.

### Beispiel

```python
temperatur = 35

if temperatur > 30:
    print("Warnung: Hohe Temperatur!")
    print("Kühlung einschalten")

print("Programm beendet")  # Wird immer ausgeführt
```

---

## if-else

```kroki-plantuml
@startuml
skinparam ActivityBackgroundColor #f5f5f5
skinparam ActivityBorderColor #333
skinparam DiamondBackgroundColor #ffe6f0
skinparam DiamondBorderColor #333

start
if (Bedingung?) then (True)
  #aaffaa:if-Block;
else (False)
  #ffaaaa:else-Block;
endif
:Weiter;
stop
@enduml
```

```python
if bedingung:
    # Code wenn True
else:
    # Code wenn False
```

### Beispiel

```python
alter = 17

if alter >= 18:
    print("Zugang gewährt")
else:
    print("Zugang verweigert")
```

---

## if-elif-else (Mehrfachverzweigung)

```kroki-plantuml
@startuml
skinparam ActivityBackgroundColor #f5f5f5
skinparam ActivityBorderColor #333
skinparam DiamondBackgroundColor #ffe6f0
skinparam DiamondBorderColor #333

start
if (Bedingung 1?) then (True)
  :Block 1;
elseif (Bedingung 2?) then (True)
  :Block 2;
elseif (Bedingung 3?) then (True)
  :Block 3;
else (False)
  :else-Block;
endif
:Weiter;
stop
@enduml
```

```python
if bedingung1:
    # Code wenn bedingung1 True
elif bedingung2:
    # Code wenn bedingung2 True
elif bedingung3:
    # Code wenn bedingung3 True
else:
    # Code wenn keine Bedingung True
```

!!! info "Reihenfolge beachten"
    Die Bedingungen werden von oben nach unten geprüft. Sobald eine Bedingung `True` ist, werden die restlichen **nicht mehr geprüft**.

### Beispiel: Notenberechnung

```python
punkte = 75

if punkte >= 90:
    note = "sehr gut"
elif punkte >= 75:
    note = "gut"
elif punkte >= 60:
    note = "befriedigend"
elif punkte >= 50:
    note = "ausreichend"
else:
    note = "nicht bestanden"

print(f"Note: {note}")
```

### Beispiel: KPI-Bewertung

```python
umsatz = 18500

if umsatz >= 30000:
    status = "🟢 Herausragend"
    bonus = umsatz * 0.10
elif umsatz >= 20000:
    status = "🟢 Sehr gut"
    bonus = umsatz * 0.05
elif umsatz >= 10000:
    status = "🟡 Ziel erreicht"
    bonus = 0
else:
    status = "🔴 Unter Ziel"
    bonus = 0

print(f"Status: {status}")
print(f"Bonus: {bonus:.2f} €")
```

---

## Verschachtelte Bedingungen

```python
alter = 25
hat_führerschein = True

if alter >= 18:
    if hat_führerschein:
        print("Darf Auto fahren")
    else:
        print("Volljährig, aber kein Führerschein")
else:
    print("Zu jung")
```

!!! tip "Tipp: Verschachtelung vermeiden"
    Zu tiefe Verschachtelungen machen Code schwer lesbar. Oft lassen sie sich mit `and`/`or` vereinfachen:
    
    ```python
    if alter >= 18 and hat_führerschein:
        print("Darf Auto fahren")
    ```

---

## Logische Operatoren in Bedingungen

### AND (UND)

Beide Bedingungen müssen erfüllt sein:

```python
temperatur = 22
luftfeuchtigkeit = 45

if temperatur >= 20 and temperatur <= 25 and luftfeuchtigkeit < 60:
    print("Optimales Raumklima")
```

### OR (ODER)

Mindestens eine Bedingung muss erfüllt sein:

```python
status_code = 404

if status_code == 400 or status_code == 404 or status_code == 500:
    print("Fehler aufgetreten!")
```

### NOT (NICHT)

Negiert die Bedingung:

```python
ist_wochenende = False

if not ist_wochenende:
    print("Arbeitstag")
```

### Kombiniert

```python
alter = 30
einkommen = 4000
hat_kredit = False

if (alter >= 18 and einkommen >= 2500) and not hat_kredit:
    print("Kredit genehmigt")
```

---

## Vergleiche mit mehreren Werten

### Elegante Bereichsprüfung

```python
# Umständlich
if temperatur >= 20 and temperatur <= 30:
    print("Angenehm")

# Pythonisch ✨
if 20 <= temperatur <= 30:
    print("Angenehm")
```

### Prüfen auf mehrere Werte

```python
# Umständlich
if status == "aktiv" or status == "wartend" or status == "neu":
    print("Gültiger Status")

# Pythonisch ✨
if status in ["aktiv", "wartend", "neu"]:
    print("Gültiger Status")
```

---

## Ternärer Operator (Kurzform)

Für einfache if-else-Zuweisungen:

```python
# Langform
if alter >= 18:
    status = "erwachsen"
else:
    status = "minderjährig"

# Kurzform (ternärer Operator)
status = "erwachsen" if alter >= 18 else "minderjährig"
```

### Syntax

```python
ergebnis = wert_wenn_true if bedingung else wert_wenn_false
```

### Praxisbeispiele

```python
# Absolutwert
absolut = x if x >= 0 else -x

# Maximum zweier Zahlen
maximum = a if a > b else b

# Standardwert bei None
name = eingabe if eingabe else "Unbekannt"

# In f-Strings
print(f"Status: {'OK' if fehler == 0 else 'FEHLER'}")
```

!!! warning "Lesbarkeit beachten"
    Der ternäre Operator ist praktisch für einfache Fälle. Bei komplexen Bedingungen ist die ausgeschriebene Form besser lesbar.

---

## Truthy und Falsy

Python interpretiert viele Werte als `True` oder `False`:

```python
# Falsy-Werte (werden als False interpretiert):
# 0, 0.0, "", [], {}, None, False

daten = []

# Umständlich
if len(daten) > 0:
    print("Daten vorhanden")

# Pythonisch ✨
if daten:
    print("Daten vorhanden")

# Prüfen auf "leer"
if not daten:
    print("Keine Daten")
```

### Praxisbeispiel: Standardwerte

```python
benutzername = input("Name: ")

# Wenn leer, Standardwert verwenden
if not benutzername:
    benutzername = "Gast"

# Oder kürzer mit 'or'
benutzername = input("Name: ") or "Gast"
```

---

## Praxisbeispiel: Datenvalidierung

```python
def validiere_alter(eingabe):
    """Prüft ob eine Eingabe ein gültiges Alter ist."""
    
    # Ist es eine Zahl?
    if not eingabe.isdigit():
        return "Fehler: Keine gültige Zahl"
    
    alter = int(eingabe)
    
    # Bereichsprüfung
    if alter < 0:
        return "Fehler: Alter kann nicht negativ sein"
    elif alter > 150:
        return "Fehler: Unplausibles Alter"
    elif alter < 18:
        return "Minderjährig"
    elif alter <= 67:
        return "Erwerbstätig"
    else:
        return "Rentner"

# Test
print(validiere_alter("25"))   # Erwerbstätig
print(validiere_alter("-5"))   # Keine gültige Zahl (isdigit schlägt fehl bei -)
print(validiere_alter("abc"))  # Fehler: Keine gültige Zahl
```

---

## Zusammenfassung

!!! success "Das Wichtigste"
    - `if`, `elif`, `else` für Verzweigungen
    - Einrückung definiert den Codeblock
    - `and`, `or`, `not` für logische Verknüpfungen
    - `20 <= x <= 30` für Bereichsprüfungen
    - `x in [a, b, c]` für Mehrfachvergleiche
    - Ternärer Operator für einfache Zuweisungen

---

??? question "Selbstkontrolle"
    1. Was ist der Unterschied zwischen `if-elif-else` und mehreren `if`-Anweisungen?
    2. Schreibe `maximum = a if a > b else b` als normale if-else-Anweisung.
    3. Warum ist `if daten:` besser als `if len(daten) > 0:`?
    
    ??? success "Antworten"
        1. Bei `if-elif-else` wird nur **ein** Block ausgeführt (bei der ersten wahren Bedingung). Bei mehreren `if`-Anweisungen können **mehrere** Blöcke ausgeführt werden.
        2. 
        ```python
        if a > b:
            maximum = a
        else:
            maximum = b
        ```
        3. Es ist kürzer, pythonischer und funktioniert auch bei `None` (während `len(None)` einen Fehler wirft).

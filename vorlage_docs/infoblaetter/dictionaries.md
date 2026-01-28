# Dictionaries

## Warum Dictionaries?

Bei Listen greifst du auf Elemente über einen **numerischen Index** zu: `liste[0]`, `liste[1]`, etc. Das funktioniert gut für geordnete Sammlungen, aber was wenn du einen Wert über einen **aussagekräftigen Namen** finden willst?

```kroki-plantuml
@startuml
skinparam defaultFontSize 12
left to right direction

map "Liste (Index-Zugriff)" as liste {
  0 => "Max"
  1 => "Anna"
  2 => "Tom"
}

map "Dictionary (Key-Zugriff)" as dict {
  "chef" => "Max"
  "dev" => "Anna"
  "admin" => "Tom"
}

note bottom of liste
  liste[1] → "Anna"
  Nur Zahlen als Index
end note

note bottom of dict
  dict["dev"] → "Anna"
  Beliebige Schlüssel
end note
@enduml
```

| Eigenschaft | Liste | Dictionary |
|-------------|-------|------------|
| Zugriff | Index (0, 1, 2, ...) | Schlüssel |
| Suche | O(n) - langsam | O(1) - schnell |
| Verwendung | Geordnete Sequenzen | Zuordnungen/Lookup |

**Beispiel:** Du willst die Telefonnummer von "Anna" finden.

- **Liste**: Du musst alle Einträge durchsuchen, bis du "Anna" findest
- **Dictionary**: Direkter Zugriff mit `telefon["Anna"]` → sofort gefunden!

---

## Was sind Dictionaries?

Dictionaries sind **ungeordnete** Sammlungen von **Schlüssel-Wert-Paaren** (Key-Value-Pairs). Auch bekannt als "Hash Maps" oder "Assoziative Arrays".

```kroki-plantuml
@startuml
skinparam defaultFontSize 14
skinparam map {
  BackgroundColor #f5f5f5
  BorderColor #333
}

map "person" as person {
  "name" => "Max"
  "alter" => 30
  "stadt" => "Berlin"
}

note right of person
  Schlüssel (Key) → Wert (Value)
  Zugriff: person["name"] → "Max"
end note
@enduml
```

```python
# Leeres Dictionary
leer = {}

# Dictionary mit Daten
person = {
    "name": "Max Mustermann",
    "alter": 30,
    "stadt": "Berlin"
}

# Einzeilig
farben = {"rot": "#FF0000", "grün": "#00FF00", "blau": "#0000FF"}
```

!!! info "Schlüssel-Regeln"
    - Schlüssel müssen **eindeutig** sein
    - Schlüssel müssen **unveränderbar** sein (str, int, tuple)
    - Werte können beliebige Typen haben

---

## Zugriff auf Werte

### Mit eckigen Klammern

```python
person = {"name": "Max", "alter": 30, "stadt": "Berlin"}

print(person["name"])   # Max
print(person["alter"])  # 30

# FEHLER bei nicht existierendem Schlüssel!
print(person["beruf"])  # KeyError: 'beruf'
```

### Mit get() (sicherer)

```python
person = {"name": "Max", "alter": 30}

print(person.get("name"))         # Max
print(person.get("beruf"))        # None (kein Fehler!)
print(person.get("beruf", "k.A.")) # k.A. (Standardwert)
```

!!! tip "Best Practice"
    Verwende `get()` wenn du nicht sicher bist, ob der Schlüssel existiert.

---

## Werte ändern und hinzufügen

```python
person = {"name": "Max", "alter": 30}

# Wert ändern
person["alter"] = 31

# Neuen Eintrag hinzufügen
person["stadt"] = "Berlin"
person["beruf"] = "Data Analyst"

print(person)
# {"name": "Max", "alter": 31, "stadt": "Berlin", "beruf": "Data Analyst"}
```

### Mehrere Einträge mit update()

```python
person = {"name": "Max"}

person.update({
    "alter": 30,
    "stadt": "Berlin",
    "beruf": "Data Analyst"
})

# Oder mit Keyword-Argumenten
person.update(email="max@example.com", telefon="0123456")
```

---

## Einträge entfernen

| Methode | Beschreibung | Beispiel |
|---------|--------------|----------|
| `del dict[key]` | Löscht Eintrag | `del person["alter"]` |
| `pop(key)` | Entfernt und gibt Wert zurück | `alter = person.pop("alter")` |
| `pop(key, default)` | Mit Standardwert | `person.pop("xyz", None)` |
| `clear()` | Löscht alle Einträge | `person.clear()` |

```python
person = {"name": "Max", "alter": 30, "stadt": "Berlin"}

del person["stadt"]        # Entfernt "stadt"
alter = person.pop("alter") # Entfernt und gibt 30 zurück
person.clear()             # Leeres Dictionary
```

---

## Prüfen ob Schlüssel existiert

```python
person = {"name": "Max", "alter": 30}

# Mit 'in' (prüft Schlüssel, nicht Werte!)
if "name" in person:
    print("Name vorhanden")

if "beruf" not in person:
    print("Beruf nicht angegeben")

# ACHTUNG: 'in' prüft nur Schlüssel!
print("Max" in person)   # False! (Max ist ein Wert, kein Schlüssel)
print("Max" in person.values())  # True
```

---

## Iteration über Dictionaries

### Über Schlüssel

```python
person = {"name": "Max", "alter": 30, "stadt": "Berlin"}

for key in person:
    print(key)

# Explizit mit .keys()
for key in person.keys():
    print(key)
```

### Über Werte

```python
for value in person.values():
    print(value)
```

### Über Schlüssel UND Werte

```python
for key, value in person.items():
    print(f"{key}: {value}")

# Ausgabe:
# name: Max
# alter: 30
# stadt: Berlin
```

---

## Dictionary-Methoden

| Methode | Beschreibung | Rückgabe |
|---------|--------------|----------|
| `keys()` | Alle Schlüssel | dict_keys |
| `values()` | Alle Werte | dict_values |
| `items()` | Alle Paare | dict_items |
| `get(key, default)` | Wert oder Standard | Wert |
| `pop(key, default)` | Entfernt und gibt zurück | Wert |
| `update(dict)` | Fügt Einträge hinzu | None |
| `copy()` | Flache Kopie | dict |
| `clear()` | Leert Dictionary | None |

### In Listen umwandeln

```python
person = {"name": "Max", "alter": 30}

schluessel = list(person.keys())    # ["name", "alter"]
werte = list(person.values())       # ["Max", 30]
paare = list(person.items())        # [("name", "Max"), ("alter", 30)]
```

---

## Dictionary Comprehensions

Ähnlich wie List Comprehensions:

```python
# Quadratzahlen als Dictionary
quadrate = {x: x**2 for x in range(1, 6)}
# {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Mit Bedingung
gerade_quadrate = {x: x**2 for x in range(1, 11) if x % 2 == 0}
# {2: 4, 4: 16, 6: 36, 8: 64, 10: 100}

# Aus zwei Listen
namen = ["Max", "Anna", "Tom"]
alter = [30, 25, 35]
personen = {n: a for n, a in zip(namen, alter)}
# {"Max": 30, "Anna": 25, "Tom": 35}
```

---

## Verschachtelte Dictionaries

```kroki-plantuml
@startuml
skinparam defaultFontSize 12
skinparam object {
  BackgroundColor #f5f5f5
  BorderColor #333
}

object "mitarbeiter" as root {
}

object "M001" as m1 {
  name = "Max Mustermann"
  abteilung = "IT"
  gehalt = 4500
}

object "M002" as m2 {
  name = "Anna Schmidt"
  abteilung = "HR"
  gehalt = 4200
}

root --> m1 : "M001"
root --> m2 : "M002"
@enduml
```

```python
mitarbeiter = {
    "M001": {
        "name": "Max Mustermann",
        "abteilung": "IT",
        "gehalt": 4500
    },
    "M002": {
        "name": "Anna Schmidt",
        "abteilung": "HR",
        "gehalt": 4200
    }
}

# Zugriff
print(mitarbeiter["M001"]["name"])      # Max Mustermann
print(mitarbeiter["M002"]["abteilung"]) # HR

# Ändern
mitarbeiter["M001"]["gehalt"] = 4800

# Neuen Mitarbeiter hinzufügen
mitarbeiter["M003"] = {
    "name": "Tom Weber",
    "abteilung": "Sales",
    "gehalt": 4000
}
```

### Iteration über verschachtelte Dicts

```python
for id, daten in mitarbeiter.items():
    print(f"ID: {id}")
    for key, value in daten.items():
        print(f"  {key}: {value}")
```

---

## Praxisbeispiele

### Häufigkeitszählung (Frequency Table)

```python
texte = ["Apfel", "Birne", "Apfel", "Orange", "Apfel", "Birne"]

# Zählen mit Dictionary
haeufigkeit = {}
for frucht in texte:
    if frucht in haeufigkeit:
        haeufigkeit[frucht] += 1
    else:
        haeufigkeit[frucht] = 1

print(haeufigkeit)  # {"Apfel": 3, "Birne": 2, "Orange": 1}

# Eleganter mit get()
haeufigkeit = {}
for frucht in texte:
    haeufigkeit[frucht] = haeufigkeit.get(frucht, 0) + 1
```

### Gruppierung von Daten

```python
mitarbeiter = [
    {"name": "Max", "abteilung": "IT"},
    {"name": "Anna", "abteilung": "HR"},
    {"name": "Tom", "abteilung": "IT"},
    {"name": "Lisa", "abteilung": "HR"},
]

# Nach Abteilung gruppieren
nach_abteilung = {}
for ma in mitarbeiter:
    abt = ma["abteilung"]
    if abt not in nach_abteilung:
        nach_abteilung[abt] = []
    nach_abteilung[abt].append(ma["name"])

print(nach_abteilung)
# {"IT": ["Max", "Tom"], "HR": ["Anna", "Lisa"]}
```

### Lookup-Tabelle

```python
# Status-Codes
status_codes = {
    200: "OK",
    201: "Created",
    400: "Bad Request",
    404: "Not Found",
    500: "Internal Server Error"
}

code = 404
print(f"Status {code}: {status_codes.get(code, 'Unknown')}")
```

### Konfigurationsdaten

```python
config = {
    "database": {
        "host": "localhost",
        "port": 5432,
        "name": "analytics_db"
    },
    "api": {
        "timeout": 30,
        "retries": 3
    },
    "debug": True
}

# Zugriff
db_host = config["database"]["host"]
timeout = config["api"]["timeout"]
```

---

## Zusammenfassung

!!! success "Das Wichtigste"
    - Dictionaries speichern Schlüssel-Wert-Paare
    - Zugriff mit `dict[key]` oder sicher mit `dict.get(key)`
    - `in` prüft ob **Schlüssel** existiert
    - Iteration mit `.keys()`, `.values()`, `.items()`
    - Dictionary Comprehensions: `{k: v for k, v in ...}`
    - Ideal für Lookup-Tabellen und strukturierte Daten

---

??? question "Selbstkontrolle"
    1. Was ist der Unterschied zwischen `dict["key"]` und `dict.get("key")`?
    2. Wie prüfst du, ob ein Wert (nicht Schlüssel!) im Dictionary existiert?
    3. Erstelle ein Dictionary mit den Zahlen 1-5 und ihren Quadraten.
    
    ??? success "Antworten"
        1. `dict["key"]` wirft `KeyError` wenn der Schlüssel nicht existiert, `dict.get("key")` gibt `None` zurück
        2. `wert in dict.values()`
        3. `{x: x**2 for x in range(1, 6)}` oder `{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}`

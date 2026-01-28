# Python – Exceptions (Fehlerbehandlung)

## Überblick

Exceptions sind Fehler, die während der Programmausführung auftreten. Python bietet mit `try-except` eine elegante Möglichkeit, diese Fehler abzufangen und zu behandeln.

---

## Warum Fehlerbehandlung?

Ohne Fehlerbehandlung stürzt das Programm ab:

```python
# Ohne try-except: Absturz bei ungültiger Eingabe
zahl = int(input("Gib eine Zahl ein: "))  # "abc" → ValueError
ergebnis = 100 / zahl                      # 0 → ZeroDivisionError
```

Mit Fehlerbehandlung läuft das Programm weiter:

```python
try:
    zahl = int(input("Gib eine Zahl ein: "))
    ergebnis = 100 / zahl
    print(f"Ergebnis: {ergebnis}")
except ValueError:
    print("Das war keine gültige Zahl!")
except ZeroDivisionError:
    print("Division durch Null ist nicht erlaubt!")
```

---

## Grundstruktur

### Visualisierung: try-except-else-finally Ablauf

```kroki-plantuml
@startuml
skinparam ActivityBackgroundColor #f5f5f5
skinparam ActivityBorderColor #333
skinparam DiamondBackgroundColor #ffe6f0
skinparam DiamondBorderColor #333

start
:try-Block ausführen;

if (Fehler aufgetreten?) then (ja)
  if (Passendes except?) then (ja)
    #ffaaaa:except-Block ausführen;
  else (nein)
    :Fehler weiterreichen;
    stop
  endif
else (nein)
  #aaffaa:else-Block ausführen;
endif

#aaaaff:finally-Block ausführen;
stop
@enduml
```

```python
try:
    # Code, der einen Fehler verursachen könnte
    risikoreicher_code()
except ExceptionTyp:
    # Was tun, wenn dieser Fehler auftritt
    fehlerbehandlung()
except AndererExceptionTyp:
    # Anderer Fehlertyp
    andere_behandlung()
else:
    # Wird ausgeführt, wenn KEIN Fehler aufgetreten ist
    erfolg_code()
finally:
    # Wird IMMER ausgeführt (mit oder ohne Fehler)
    aufraeumen()
```

---

## Häufige Exception-Typen

| Exception | Ursache | Beispiel |
|-----------|---------|----------|
| `ValueError` | Ungültiger Wert | `int("abc")` |
| `TypeError` | Falscher Datentyp | `"text" + 5` |
| `ZeroDivisionError` | Division durch 0 | `10 / 0` |
| `IndexError` | Index außerhalb | `liste[100]` |
| `KeyError` | Schlüssel nicht vorhanden | `dict["fehlt"]` |
| `FileNotFoundError` | Datei nicht gefunden | `open("gibt_es_nicht.txt")` |
| `AttributeError` | Attribut existiert nicht | `"text".nicht_da()` |

---

## Praktische Beispiele

### Benutzereingabe validieren

```python
def eingabe_zahl(prompt: str, min_val: float = None, max_val: float = None) -> float:
    """Liest eine Zahl ein mit Validierung."""
    while True:
        try:
            wert = float(input(prompt))
            
            if min_val is not None and wert < min_val:
                print(f"Wert muss mindestens {min_val} sein!")
                continue
            
            if max_val is not None and wert > max_val:
                print(f"Wert darf höchstens {max_val} sein!")
                continue
            
            return wert
        
        except ValueError:
            print("Bitte eine gültige Zahl eingeben!")

# Verwendung
alter = eingabe_zahl("Alter: ", min_val=0, max_val=150)
```

### Datei sicher lesen

```python
def datei_lesen(pfad: str) -> str | None:
    """Liest eine Datei und gibt den Inhalt zurück."""
    try:
        with open(pfad, 'r', encoding='utf-8') as f:
            return f.read()
    except FileNotFoundError:
        print(f"Datei nicht gefunden: {pfad}")
        return None
    except PermissionError:
        print(f"Keine Berechtigung für: {pfad}")
        return None
    except Exception as e:
        print(f"Unerwarteter Fehler: {e}")
        return None

# Verwendung
inhalt = datei_lesen("daten.txt")
if inhalt:
    print(inhalt)
```

### Dictionary mit Fallback

```python
daten = {"name": "Max", "alter": 30}

# Methode 1: try-except
try:
    stadt = daten["stadt"]
except KeyError:
    stadt = "Unbekannt"

# Methode 2: .get() mit Default (eleganter!)
stadt = daten.get("stadt", "Unbekannt")
```

### CSV-Datei verarbeiten

```python
import csv

def lade_csv(pfad: str) -> list[dict]:
    """Lädt eine CSV-Datei mit Fehlerbehandlung."""
    daten = []
    
    try:
        with open(pfad, 'r', encoding='utf-8') as f:
            reader = csv.DictReader(f)
            
            for zeile_nr, zeile in enumerate(reader, start=2):
                try:
                    # Versuche, numerische Werte zu konvertieren
                    if 'menge' in zeile:
                        zeile['menge'] = int(zeile['menge'])
                    if 'preis' in zeile:
                        zeile['preis'] = float(zeile['preis'])
                    
                    daten.append(zeile)
                
                except ValueError as e:
                    print(f"Warnung: Zeile {zeile_nr} übersprungen ({e})")
                    continue
    
    except FileNotFoundError:
        print(f"Datei nicht gefunden: {pfad}")
    except Exception as e:
        print(f"Fehler beim Lesen: {e}")
    
    return daten
```

---

## Eigene Exceptions auslösen

Mit `raise` kannst du selbst Exceptions auslösen:

```python
def berechne_rabatt(preis: float, prozent: float) -> float:
    """Berechnet rabattierten Preis."""
    if preis < 0:
        raise ValueError("Preis darf nicht negativ sein!")
    
    if not 0 <= prozent <= 100:
        raise ValueError("Rabatt muss zwischen 0 und 100 liegen!")
    
    return preis * (1 - prozent / 100)

# Verwendung
try:
    neuer_preis = berechne_rabatt(100, 150)  # Ungültiger Rabatt!
except ValueError as e:
    print(f"Fehler: {e}")
```

---

## Eigene Exception-Klassen

Für spezifische Fehler kannst du eigene Exceptions definieren:

```python
class ValidationError(Exception):
    """Fehler bei der Datenvalidierung."""
    pass

class DataNotFoundError(Exception):
    """Daten wurden nicht gefunden."""
    pass

def validiere_email(email: str) -> str:
    """Prüft eine E-Mail-Adresse."""
    if "@" not in email or "." not in email:
        raise ValidationError(f"Ungültige E-Mail: {email}")
    return email.lower().strip()

# Verwendung
try:
    email = validiere_email("ungueltig")
except ValidationError as e:
    print(f"Validierungsfehler: {e}")
```

---

## Best Practices

!!! tip "Empfehlungen"
    
    **1. Spezifische Exceptions abfangen**
    ```python
    # ❌ Schlecht: Fängt ALLES ab
    try:
        ...
    except Exception:
        pass
    
    # ✅ Gut: Nur erwartete Fehler
    try:
        ...
    except (ValueError, TypeError):
        ...
    ```
    
    **2. Fehlermeldung loggen**
    ```python
    except ValueError as e:
        print(f"Fehler aufgetreten: {e}")  # Details ausgeben
    ```
    
    **3. Nicht still ignorieren**
    ```python
    # ❌ Schlecht: Fehler verschwinden spurlos
    except:
        pass
    
    # ✅ Gut: Mindestens loggen
    except Exception as e:
        print(f"Warnung: {e}")
    ```
    
    **4. finally für Aufräumarbeiten**
    ```python
    verbindung = None
    try:
        verbindung = datenbank_verbinden()
        # ...arbeiten...
    finally:
        if verbindung:
            verbindung.schliessen()
    ```

---

## try-except vs. Prüfung vorher

Manchmal ist eine Prüfung besser als try-except:

```python
# Variante 1: EAFP (Easier to Ask for Forgiveness than Permission)
try:
    wert = daten["schluessel"]
except KeyError:
    wert = "default"

# Variante 2: LBYL (Look Before You Leap)
if "schluessel" in daten:
    wert = daten["schluessel"]
else:
    wert = "default"

# Variante 3: .get() - Oft am elegantesten!
wert = daten.get("schluessel", "default")
```

In Python ist EAFP oft idiomatischer, aber lesbarkeit geht vor.

---

## Zusammenfassung

!!! success "Wichtige Konzepte"
    - **try-except**: Fehler abfangen statt Absturz
    - **Mehrere except**: Verschiedene Fehlertypen unterscheiden
    - **else**: Code für den Erfolgsfall
    - **finally**: Code, der immer ausgeführt wird
    - **raise**: Selbst Exceptions auslösen
    - **Eigene Exceptions**: Für spezifische Fehlerfälle

---

## Schnellreferenz

```python
# Grundstruktur
try:
    risiko_code()
except ValueError as e:
    print(f"Wert-Fehler: {e}")
except (TypeError, KeyError):
    print("Typ- oder Schlüssel-Fehler")
except Exception as e:
    print(f"Anderer Fehler: {e}")
else:
    print("Alles gut!")
finally:
    print("Aufräumen...")

# Eigene Exception auslösen
raise ValueError("Ungültiger Wert!")

# Eigene Exception-Klasse
class MeinFehler(Exception):
    pass
```

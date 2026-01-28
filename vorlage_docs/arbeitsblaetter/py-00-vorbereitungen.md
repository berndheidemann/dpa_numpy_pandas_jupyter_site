# Python Einführung – Vorbereitungen & Erste Schritte

## Lernziele

Nach Bearbeitung dieses Arbeitsblatts kannst du:

- deine Python-Entwicklungsumgebung einrichten
- ein erstes Python-Programm ausführen
- Variablen anlegen und ausgeben
- Benutzereingaben verarbeiten

!!! note "Begleitendes Infoblatt"
    [:material-book-open-variant: Python Grundlagen](../infoblaetter/python-grundlagen.md) – Variablen, Datentypen, Ein-/Ausgabe, String-Methoden

---

## Aufgaben

### Aufgabe 1 – Installation überprüfen

- [ ] **Python installieren:** Falls noch nicht geschehen, lade Python von [python.org/downloads](https://www.python.org/downloads/) herunter und installiere es. **Wichtig:** Aktiviere bei der Installation "Add Python to PATH"!

- [ ] **Installation testen:** Öffne ein Terminal (Windows: `cmd` oder PowerShell, macOS/Linux: Terminal) und gib ein:
    ```bash
    python --version
    ```
    Es sollte die installierte Python-Version angezeigt werden (z.B. `Python 3.11.5`).

### Aufgabe 2 – VS Code einrichten

- [ ] **VS Code installieren:** Falls noch nicht vorhanden, lade VS Code von [code.visualstudio.com](https://code.visualstudio.com/) herunter.

- [ ] **Python Extension installieren:** Öffne VS Code, klicke auf das Extensions-Symbol (oder `Ctrl+Shift+X`) und suche nach "Python". Installiere die Extension von Microsoft.

- [ ] **Interpreter auswählen:** Drücke `Ctrl+Shift+P`, tippe "Python: Select Interpreter" und wähle deine Python-Installation aus.

### Aufgabe 3 – Hello World

- [ ] **Datei erstellen:** Erstelle in VS Code eine neue Datei `hello.py`

- [ ] **Code eingeben:**
    ```python
    print("Hello, World!")
    print("Willkommen zu Python!")
    ```

- [ ] **Programm ausführen:** Rechtsklick → "Run Python File in Terminal" oder `F5`

### Aufgabe 4 – Variablen und Ausgabe

- [ ] **Erstelle eine Datei `variablen.py`** mit folgendem Inhalt:
    ```python
    # Variablen definieren
    name = "Max Mustermann"
    alter = 25
    gehalt = 3500.50
    ist_student = False

    # Ausgabe
    print(name)
    print(alter)
    print(gehalt)
    print(ist_student)
    ```

- [ ] **Führe das Programm aus** und beobachte die Ausgabe.

- [ ] **Ändere die Werte** der Variablen und führe das Programm erneut aus.

### Aufgabe 5 – Formatierte Ausgabe mit f-Strings

- [ ] **Erweitere `variablen.py`** um formatierte Ausgaben:
    ```python
    # f-String Ausgabe
    print(f"Name: {name}")
    print(f"Alter: {alter} Jahre")
    print(f"Gehalt: {gehalt} €")
    print(f"Student: {ist_student}")
    
    # Berechnung in f-String
    print(f"In 5 Jahren: {alter + 5} Jahre")
    print(f"Jahresgehalt: {gehalt * 12} €")
    ```

### Aufgabe 6 – Benutzereingabe

- [ ] **Erstelle eine Datei `eingabe.py`:**
    ```python
    name = input("Wie heißt du? ")
    print(f"Hallo, {name}!")
    ```

- [ ] **Führe das Programm aus** und teste es mit verschiedenen Namen.

### Aufgabe 7 – Eingabe von Zahlen

Die `input()`-Funktion gibt immer einen **String** zurück. Für Berechnungen musst du den Wert umwandeln.

- [ ] **Erstelle eine Datei `zahlen_eingabe.py`:**
    ```python
    # Eingabe als String
    alter_text = input("Wie alt bist du? ")
    
    # Umwandlung in Zahl
    alter = int(alter_text)
    
    # Berechnung
    print(f"In 10 Jahren bist du {alter + 10} Jahre alt.")
    ```

- [ ] **Teste das Programm** mit verschiedenen Eingaben. Was passiert, wenn du "abc" eingibst?

### Aufgabe 8 – Einfacher Taschenrechner

- [ ] **Erstelle eine Datei `taschenrechner.py`:**

    Schreibe ein Programm, das:
    1. Zwei Zahlen vom Benutzer einliest
    2. Die vier Grundrechenarten ausführt
    3. Die Ergebnisse ausgibt

    Erwartete Ausgabe:
    ```
    Erste Zahl: 10
    Zweite Zahl: 3
    
    Addition: 10 + 3 = 13
    Subtraktion: 10 - 3 = 7
    Multiplikation: 10 * 3 = 30
    Division: 10 / 3 = 3.33
    ```

    !!! tip "Tipps"
        - Nutze `float()` statt `int()` für Kommazahlen
        - Für formatierte Dezimalstellen: `f"{ergebnis:.2f}"`

### Aufgabe 9 – Datentypen erkunden

- [ ] **Erstelle eine Datei `datentypen.py`:**
    ```python
    # Verschiedene Datentypen
    ganzzahl = 42
    kommazahl = 3.14159
    text = "Hallo"
    wahrheitswert = True
    
    # Typ ermitteln
    print(type(ganzzahl))
    print(type(kommazahl))
    print(type(text))
    print(type(wahrheitswert))
    ```

- [ ] **Experimentiere mit Typumwandlungen:**
    ```python
    # String zu Zahl
    print(int("42"))
    print(float("3.14"))
    
    # Zahl zu String
    print(str(42))
    
    # Was passiert hier?
    print("5" + "3")    # ???
    print(5 + 3)        # ???
    print(int("5") + int("3"))  # ???
    ```

### Aufgabe 10 – BMI-Rechner (Anwendung)

- [ ] **Erstelle einen BMI-Rechner** (`bmi_rechner.py`):

    Der Body-Mass-Index berechnet sich: $BMI = \frac{Gewicht}{Größe^2}$
    
    - Frage den Benutzer nach Gewicht (in kg) und Größe (in m)
    - Berechne den BMI
    - Gib das Ergebnis auf 2 Dezimalstellen gerundet aus

    Beispiel:
    ```
    Gewicht in kg: 75
    Größe in m: 1.80
    
    Dein BMI: 23.15
    ```

---

## Zusammenfassung

!!! success "Das hast du gelernt"
    - **Python-Setup:** Installation und VS Code einrichten
    - **Variablen:** Werte speichern ohne Typangabe
    - **print():** Ausgabe auf der Konsole
    - **f-Strings:** Formatierte Ausgabe mit `f"Text {variable}"`
    - **input():** Benutzereingabe (gibt String zurück!)
    - **Typumwandlung:** `int()`, `float()`, `str()`

---

??? question "Selbstkontrolle"
    1. Welchen Datentyp hat `input()` als Rückgabewert?
    2. Wie wandelst du den String `"3.14"` in eine Kommazahl um?
    3. Was ist der Unterschied zwischen `print(5 + 3)` und `print("5" + "3")`?
    
    ??? success "Antworten"
        1. Immer `str` (String)
        2. `float("3.14")`
        3. `print(5 + 3)` gibt `8` aus (Addition von Zahlen), `print("5" + "3")` gibt `53` aus (Konkatenation von Strings)

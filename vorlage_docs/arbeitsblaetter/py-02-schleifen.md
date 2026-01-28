# Python – Schleifen

## Lernziele

Nach Bearbeitung dieses Arbeitsblatts kannst du:

- `while`-Schleifen für unbestimmte Wiederholungen nutzen
- `for`-Schleifen mit `range()` einsetzen
- Schleifensteuerung mit `break` und `continue` anwenden
- Daten in Schleifen verarbeiten und aggregieren

!!! note "Begleitende Infoblätter"
    - [:material-book-open-variant: Schleifen](../infoblaetter/schleifen.md) – while, for, range(), enumerate(), zip()
    - [:material-book-open-variant: Funktionen](../infoblaetter/funktionen.md) – def, Parameter, Rückgabewerte (ab Aufgabe 4)

---

## Einführung

Schleifen sind essenziell für die Datenverarbeitung: Du wirst sie nutzen, um über Datensätze zu iterieren, Berechnungen durchzuführen und Eingaben zu validieren.

!!! info "while vs. for"
    - **`while`**: Wiederholt, solange eine Bedingung wahr ist (unbekannte Anzahl)
    - **`for`**: Iteriert über eine Sequenz oder einen Bereich (bekannte Anzahl)

---

## Aufgaben

### Aufgabe 1 – Dateneingabe mit Validierung

In der Praxis müssen Eingaben oft validiert werden, bis ein gültiger Wert vorliegt.

- [ ] **Erstelle `eingabe_validierung.py`:**

    Schreibe ein Programm, das:
    1. Den Benutzer nach einer Zahl zwischen 1 und 100 fragt
    2. Bei ungültiger Eingabe erneut fragt
    3. Die Anzahl der Fehlversuche zählt
    4. Am Ende die gültige Eingabe und die Anzahl der Versuche ausgibt

    ```
    Zahl (1-100): 150
    Ungültig! Bitte eine Zahl zwischen 1 und 100.
    Zahl (1-100): -5
    Ungültig! Bitte eine Zahl zwischen 1 und 100.
    Zahl (1-100): 42
    
    Gültige Eingabe: 42
    Versuche benötigt: 3
    ```

    !!! tip "Struktur"
        ```python
        versuche = 0
        while True:
            versuche += 1
            # Eingabe lesen
            # Prüfen
            # Bei gültiger Eingabe: break
        ```

---

### Aufgabe 2 – Batch-Verarbeitung von Messwerten

Simuliere die manuelle Erfassung von Messdaten, wie sie in Laboren oder bei Feldstudien vorkommt.

- [ ] **Erstelle `messwert_erfassung.py`:**

    Das Programm soll:
    1. Beliebig viele Temperaturwerte einlesen (Abbruch bei Eingabe von `-999`)
    2. Nach dem Abbruch berechnen und ausgeben:
        - Anzahl der erfassten Messwerte
        - Minimum und Maximum
        - Durchschnitt

    ```
    Temperatur eingeben (-999 zum Beenden): 23.5
    Temperatur eingeben (-999 zum Beenden): 24.1
    Temperatur eingeben (-999 zum Beenden): 22.8
    Temperatur eingeben (-999 zum Beenden): 25.2
    Temperatur eingeben (-999 zum Beenden): -999
    
    === Auswertung ===
    Anzahl Messwerte: 4
    Minimum: 22.8
    Maximum: 25.2
    Durchschnitt: 23.90
    ```

    !!! tip "Variablen initialisieren"
        ```python
        messwerte = []  # Oder: summe = 0, anzahl = 0
        minimum = float('inf')   # Größtmögliche Zahl
        maximum = float('-inf')  # Kleinstmögliche Zahl
        ```

---

### Aufgabe 3 – Passwort-Generator

Sichere Passwörter werden oft automatisch generiert.

- [ ] **Erstelle `passwort_generator.py`:**

    Das Programm soll:
    1. Die gewünschte Passwortlänge einlesen
    2. Ein zufälliges Passwort generieren (Buchstaben, Zahlen, Sonderzeichen)
    3. Das Passwort ausgeben

    ```
    Passwortlänge: 12
    Generiertes Passwort: aK7#mP2$xLn9
    ```

    !!! tip "Zufällige Zeichen"
        ```python
        import random
        
        zeichen = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%"
        
        # Zufälliges Zeichen
        zufallszeichen = random.choice(zeichen)
        ```

- [ ] **Erweiterung:** Generiere 10 Passwörter auf einmal mit einer verschachtelten Schleife.

---

### Aufgabe 4 – Primzahltest

Primzahlen sind nur durch 1 und sich selbst teilbar. Dieser Algorithmus ist ein Klassiker.

!!! info "Neu: Funktionen"
    Ab hier verwendest du **Funktionen** (`def`). Falls du damit noch nicht vertraut bist, lies zuerst das [:material-book-open-variant: Infoblatt Funktionen](../infoblaetter/funktionen.md).

- [ ] **Erstelle `primzahl.py`:**

    Implementiere eine Funktion `ist_primzahl(n)`, die `True` zurückgibt, wenn n eine Primzahl ist.

    ```python
    def ist_primzahl(n):
        # Dein Code hier
        pass
    
    # Test
    for i in range(2, 20):
        if ist_primzahl(i):
            print(f"{i} ist eine Primzahl")
    ```

    !!! tip "Algorithmus"
        - Zahlen < 2 sind keine Primzahlen
        - Prüfe, ob n durch eine Zahl von 2 bis n-1 teilbar ist
        - Wenn ja → keine Primzahl, wenn nein → Primzahl

- [ ] **Bonus: Optimierung**
    
    Du musst nur bis zur Wurzel von n prüfen. Warum?
    
    ```python
    import math
    grenze = int(math.sqrt(n)) + 1
    ```

---

### Aufgabe 5 – Log-Analyse Simulation

Server-Logs werden analysiert, um Anomalien zu erkennen (z.B. Brute-Force-Angriffe).

- [ ] **Erstelle `log_analyse.py`:**

    Das Programm soll:
    1. 100 Login-Versuche simulieren (zufällig erfolgreich oder fehlgeschlagen)
    2. Zählen:
        - Erfolgreiche Logins
        - Fehlgeschlagene Logins
        - Längste Serie von Fehlversuchen hintereinander (Brute-Force-Indikator)

    ```python
    import random
    
    erfolge = 0
    fehler = 0
    aktuelle_fehlserie = 0
    max_fehlserie = 0
    
    for i in range(100):
        # random.random() gibt Zahl zwischen 0 und 1 zurück
        erfolgreich = random.random() > 0.3  # 70% Erfolgsrate
        
        # Dein Code hier
    ```

    Ausgabe:
    ```
    === Login-Analyse (100 Versuche) ===
    Erfolgreiche Logins: 72
    Fehlgeschlagene Logins: 28
    Längste Fehlserie: 5
    
    ⚠️ Warnung: Fehlserie > 3 deutet auf möglichen Angriff hin!
    ```

---

### Aufgabe 6 – Balkendiagramm in der Konsole

Visualisiere Daten direkt im Terminal – ein typisches Quick-Analysis-Tool.

- [ ] **Erstelle `balkendiagramm.py`:**

    Gegeben ist eine Liste von Quartalsumsätzen:
    ```python
    umsaetze = [12000, 18500, 9200, 22000, 15800]
    quartale = ["Q1", "Q2", "Q3", "Q4", "Q5"]
    ```

    Gib ein horizontales Balkendiagramm aus, wobei jeder 1000 € einem `█` entspricht:
    
    ```
    Q1: ████████████ (12000 €)
    Q2: ██████████████████ (18500 €)
    Q3: █████████ (9200 €)
    Q4: ██████████████████████ (22000 €)
    Q5: ███████████████ (15800 €)
    ```

    !!! tip "String-Multiplikation"
        ```python
        balken = "█" * (umsatz // 1000)
        ```

---

### Aufgabe 7 – Zinseszins-Rechner

Berechne, wie sich ein Kapital über Jahre entwickelt.

- [ ] **Erstelle `zinseszins.py`:**

    Das Programm soll:
    1. Anfangskapital, Zinssatz und Laufzeit einlesen
    2. Für jedes Jahr den Kontostand berechnen und ausgeben
    3. Am Ende ausgeben, nach wie vielen Jahren sich das Kapital verdoppelt hat

    Formel: $Kapital_{neu} = Kapital_{alt} \times (1 + Zinssatz)$

    ```
    Anfangskapital (€): 10000
    Zinssatz (%): 5
    Laufzeit (Jahre): 20
    
    Jahr  1: 10500.00 €
    Jahr  2: 11025.00 €
    Jahr  3: 11576.25 €
    ...
    Jahr 15: 20789.28 € ← Verdopplung!
    ...
    Jahr 20: 26532.98 €
    
    Das Kapital hat sich nach 15 Jahren verdoppelt.
    ```

---

### Aufgabe 8 – Verschachtelte Schleifen: Multiplikationstabelle

- [ ] **Erstelle `multiplikation.py`:**

    Gib eine formatierte Multiplikationstabelle von 1×1 bis 10×10 aus:

    ```
         1    2    3    4    5    6    7    8    9   10
     1   1    2    3    4    5    6    7    8    9   10
     2   2    4    6    8   10   12   14   16   18   20
     3   3    6    9   12   15   18   21   24   27   30
    ...
    ```

    !!! tip "Formatierte Ausgabe"
        ```python
        print(f"{zahl:4}", end="")  # 4 Zeichen breit, kein Zeilenumbruch
        print()  # Zeilenumbruch
        ```

---

### Aufgabe 9 – Bonus: Fibonacci-Zahlen

Die Fibonacci-Folge ist: 0, 1, 1, 2, 3, 5, 8, 13, 21, ... (jede Zahl ist die Summe der beiden vorherigen).

- [ ] **Erstelle `fibonacci.py`:**

    Berechne und gib die ersten n Fibonacci-Zahlen aus.

    ```
    Wie viele Fibonacci-Zahlen? 10
    
    0, 1, 1, 2, 3, 5, 8, 13, 21, 34
    ```

---

## Zusammenfassung

!!! success "Das hast du gelernt"
    - **while**: Wiederholung mit Bedingung
    - **for + range()**: Zählschleife
    - **break**: Schleife vorzeitig beenden
    - **continue**: Durchlauf überspringen
    - **Verschachtelte Schleifen**: Für mehrdimensionale Daten
    - **Aggregation**: Summe, Min, Max, Durchschnitt in Schleifen

---

??? question "Selbstkontrolle"
    1. Wann verwendest du `while`, wann `for`?
    2. Was ist der Unterschied zwischen `break` und `continue`?
    3. Was gibt `range(5, 0, -1)` aus?
    
    ??? success "Antworten"
        1. `while` bei unbekannter Anzahl Durchläufe (z.B. bis Bedingung erfüllt), `for` bei bekannter Anzahl oder Iteration über Sequenz
        2. `break` beendet die Schleife komplett, `continue` überspringt nur den aktuellen Durchlauf
        3. 5, 4, 3, 2, 1 (rückwärts zählen, 0 ist nicht enthalten)

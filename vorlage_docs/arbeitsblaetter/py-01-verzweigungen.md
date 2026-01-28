# Python – Verzweigungen (if-else)

## Lernziele

Nach Bearbeitung dieses Arbeitsblatts kannst du:

- bedingte Anweisungen mit `if`, `elif`, `else` formulieren
- logische Operatoren (`and`, `or`, `not`) anwenden
- verschachtelte Bedingungen strukturieren
- praxisnahe Validierungen implementieren

!!! note "Begleitende Infoblätter"
    - [:material-book-open-variant: Verzweigungen](../infoblaetter/verzweigungen.md) – if-elif-else, Ternärer Operator
    - [:material-book-open-variant: Operatoren](../infoblaetter/operatoren.md) – Vergleichs- und logische Operatoren

---

## Einführung

Als Data Analyst arbeitest du häufig mit Daten, die validiert, kategorisiert oder gefiltert werden müssen. Verzweigungen sind das grundlegende Werkzeug dafür.

!!! info "Syntax"
    ```python
    if bedingung:
        # wird ausgeführt wenn bedingung True
    elif andere_bedingung:
        # wird ausgeführt wenn andere_bedingung True
    else:
        # wird ausgeführt wenn keine Bedingung True
    ```

---

## Aufgaben

### Aufgabe 1 – Datenqualitätsprüfung

Ein Datensatz enthält Altersangaben von Kunden. Diese müssen vor der Analyse validiert werden.

- [ ] **Erstelle `datenqualitaet.py`:**

    Schreibe ein Programm, das eine Altersangabe einliest und prüft:
    
    | Bedingung | Ausgabe |
    |-----------|---------|
    | Wert < 0 | "Ungültig: Alter kann nicht negativ sein" |
    | Wert > 120 | "Unplausibel: Bitte Eingabe prüfen" |
    | 0–17 | "Kategorie: Minderjährig" |
    | 18–65 | "Kategorie: Erwerbstätig" |
    | > 65 | "Kategorie: Rentner" |

    Beispiel:
    ```
    Alter eingeben: 45
    Kategorie: Erwerbstätig
    ```

- [ ] **Teste mit verschiedenen Werten:** -5, 0, 17, 18, 65, 66, 200

---

### Aufgabe 2 – Umsatz-KPI-Bewertung

Ein Vertriebsmitarbeiter hat einen Monatsumsatz erzielt. Das Programm soll den Umsatz bewerten und ggf. einen Bonus berechnen.

- [ ] **Erstelle `umsatz_bewertung.py`:**

    | Umsatz | Bewertung | Bonus |
    |--------|-----------|-------|
    | < 10.000 € | "Ziel nicht erreicht – Coaching empfohlen" | 0% |
    | 10.000–19.999 € | "Ziel erreicht" | 0% |
    | 20.000–29.999 € | "Gute Leistung" | 5% |
    | ≥ 30.000 € | "Herausragend" | 10% |

    Das Programm soll:
    1. Den Umsatz einlesen
    2. Die Bewertung ausgeben
    3. Den Bonus-Betrag berechnen und ausgeben

    Beispiel:
    ```
    Monatsumsatz in Euro: 25000
    Bewertung: Gute Leistung
    Bonus (5%): 1250.00 €
    ```

---

### Aufgabe 3 – Datumsprüfung für Datenimport

Beim Import von CSV-Dateien müssen Datumsangaben validiert werden.

- [ ] **Erstelle `datum_validierung.py`:**

    Schreibe ein Programm, das Tag, Monat und Jahr einliest und prüft, ob es ein gültiges Datum ist.

    Regeln:
    - Monate 1, 3, 5, 7, 8, 10, 12 haben 31 Tage
    - Monate 4, 6, 9, 11 haben 30 Tage
    - Februar hat 28 Tage (29 im Schaltjahr)
    
    **Schaltjahrregel:**
    - Durch 4 teilbar → Schaltjahr
    - ABER: Durch 100 teilbar → kein Schaltjahr
    - ABER: Durch 400 teilbar → doch Schaltjahr

    !!! tip "Tipp: Modulo-Operator"
        `jahr % 4 == 0` prüft, ob `jahr` durch 4 teilbar ist.

    Beispiele:
    ```
    Tag: 29
    Monat: 2
    Jahr: 2024
    ✓ Gültiges Datum (2024 ist Schaltjahr)
    
    Tag: 31
    Monat: 4
    Jahr: 2023
    ✗ Ungültiges Datum (April hat nur 30 Tage)
    ```

---

### Aufgabe 4 – Kreditwürdigkeitsprüfung (Mini-Scoring)

Eine Bank prüft Kreditanträge mit einem einfachen Scoring-System.

- [ ] **Erstelle `kredit_scoring.py`:**

    Lies folgende Werte ein:
    - Monatliches Einkommen (in €)
    - Beschäftigungsdauer (in Jahren)
    - Bestehende Kredite (ja/nein)

    Entscheidungslogik:
    
    | Kriterien | Entscheidung |
    |-----------|--------------|
    | Einkommen < 2000 € | Ablehnung |
    | Einkommen ≥ 2000 € UND Beschäftigung < 1 Jahr | Ablehnung |
    | Einkommen ≥ 2000 € UND Beschäftigung ≥ 1 Jahr UND keine Kredite | Genehmigung |
    | Einkommen ≥ 2000 € UND Beschäftigung ≥ 1 Jahr UND bestehende Kredite | Manuelle Prüfung |

    !!! tip "Tipp: ja/nein Eingabe"
        ```python
        eingabe = input("Bestehende Kredite (ja/nein)? ")
        hat_kredit = eingabe.lower() == "ja"
        ```

    Beispiel:
    ```
    Monatliches Einkommen: 3500
    Beschäftigungsdauer (Jahre): 2
    Bestehende Kredite (ja/nein)? nein
    
    Entscheidung: ✓ Kredit genehmigt
    ```

---

### Aufgabe 5 – Server-Monitoring

Ein Überwachungstool misst die Auslastung eines Servers und gibt Warnungen aus.

- [ ] **Erstelle `server_monitor.py`:**

    Lies ein:
    - CPU-Auslastung (%)
    - RAM-Auslastung (%)
    - Festplattenbelegung (%)

    Bewertungslogik:

    | Situation | Status |
    |-----------|--------|
    | Alle Werte < 70% | ✅ System OK |
    | Ein Wert zwischen 70–90% | ⚠️ Warnung |
    | Ein Wert > 90% | 🔴 Kritisch – Maßnahme erforderlich |
    | Zwei oder mehr Werte > 80% | 🔴 Überlastung – Skalierung prüfen |

    !!! tip "Mehrere Bedingungen zählen"
        ```python
        kritische_werte = 0
        if cpu > 80:
            kritische_werte += 1
        if ram > 80:
            kritische_werte += 1
        # usw.
        ```

    Beispiel:
    ```
    CPU-Auslastung (%): 75
    RAM-Auslastung (%): 82
    Festplatte (%): 65
    
    Status: ⚠️ Warnung
    Details: RAM-Auslastung erhöht (82%)
    ```

---

### Aufgabe 6 – HTTP-Statuscode-Interpreter

Schreibe ein Tool, das HTTP-Statuscodes erklärt.

- [ ] **Erstelle `http_status.py`:**

    | Code-Bereich | Kategorie | Beispiele |
    |--------------|-----------|-----------|
    | 100–199 | Information | 100: Continue |
    | 200–299 | Erfolg | 200: OK, 201: Created |
    | 300–399 | Weiterleitung | 301: Moved Permanently |
    | 400–499 | Client-Fehler | 400: Bad Request, 404: Not Found |
    | 500–599 | Server-Fehler | 500: Internal Server Error |

    Das Programm soll:
    1. Einen Statuscode einlesen
    2. Die Kategorie bestimmen
    3. Bei bekannten Codes die genaue Bedeutung ausgeben

    ```
    HTTP-Statuscode: 404
    Kategorie: Client-Fehler (4xx)
    Bedeutung: Not Found – Die angeforderte Ressource wurde nicht gefunden.
    ```

---

### Aufgabe 7 – Bonus: Ternärer Operator

Schreibe kompakte Bedingungen mit dem ternären Operator.

- [ ] **Erstelle `ternaer.py`:**
    ```python
    # Beispiel
    alter = int(input("Alter: "))
    status = "Erwachsen" if alter >= 18 else "Minderjährig"
    print(status)
    ```

- [ ] **Aufgaben:**
    1. `maximum = ???` → Das größere von zwei eingegebenen Zahlen
    2. `vorzeichen = ???` → "positiv", "negativ" oder "null" für eine Zahl
    3. `note_text = ???` → "bestanden" wenn Punkte >= 50, sonst "nicht bestanden"

---

## Zusammenfassung

!!! success "Das hast du gelernt"
    - **if-elif-else**: Mehrfachverzweigungen
    - **Logische Operatoren**: `and`, `or`, `not`
    - **Vergleichsoperatoren**: `==`, `!=`, `<`, `>`, `<=`, `>=`
    - **Bereichsprüfung**: `if 10 <= x <= 20`
    - **Ternärer Operator**: `a if bedingung else b`

---

??? question "Selbstkontrolle"
    1. Was ist der Unterschied zwischen `=` und `==`?
    2. Wie prüfst du, ob eine Zahl zwischen 10 und 20 liegt (inklusive)?
    3. Was gibt `True and False or True` zurück?
    
    ??? success "Antworten"
        1. `=` ist Zuweisung, `==` ist Vergleich auf Gleichheit
        2. `if 10 <= zahl <= 20:` oder `if zahl >= 10 and zahl <= 20:`
        3. `True` (weil `and` vor `or` ausgewertet wird: `False or True = True`)

# Testprotokoll – Blackbox-Test

## E2E-01: Vollständiger Flow

**Datum:** 2026-01-07  
**Tester:** Leonid Tsarov  
**System:** Go-Live

---

### Testschritte

1. Login mit Benutzer `admin@admin.com`
2. Foto hochladen
3. Direkter Abruf des Eintrags (Statusabfrage)
4. Warten 5–10 Sekunden
5. Erneuter Abruf des Eintrags
6. Ergebnis prüfen

---

### Erwartetes Ergebnis

- Score > 0
- Kalorien > 0

---

### Tatsächliches Ergebnis

- **Schritt 3:** Testabbruch aufgrund eines Fehlers (`error`)
- Die weiteren Testschritte konnten **nicht ausgeführt** werden.

---

### Abweichungen / Fehlerbeschreibung

Der Test ist in **Schritt 3** fehlgeschlagen.  
Beim direkten Abruf des Eintrags wurde ein unerwarteter Fehler zurückgegeben, wodurch der End-to-End-Flow nicht
weitergeführt werden konnte.

---

### Testergebnis

**Ergebnis:** nicht bestanden

---

## E2E-02: Refresh-Token-Flow

**Datum:** 2026-01-07  
**Tester:** Leonid Tsarov  
**System:** Go-Live

---

### Testschritte

1. Login mit `admin@admin.com`
2. Erhalt eines Access- und Refresh-Tokens
3. Erneuerung des Access-Tokens über Refresh-Token
4. Aufruf des geschützten Endpunkts `GET /meals` mit neuem Access-Token

---

### Erwartetes Ergebnis

- Neuer Access-Token wird erfolgreich ausgestellt
- Zugriff auf geschützten Endpunkt ist möglich

---

### Tatsächliches Ergebnis

- Neuer Access-Token erfolgreich erhalten
- Geschützter Endpunkt `GET /meals` liefert gültige Antwort

---

### Testergebnis

**Ergebnis:** bestanden

---

## E2E-03: Fehlerhafte Eingaben

**Datum:** 2026-01-07  
**Tester:** Leonid Tsarov  
**System:** Go-Live

---

### Testschritte

1. Login mit `admin@admin.com`
2. Upload eines leeren oder beschädigten Fotos
3. Start der Analyse

---

### Erwartetes Ergebnis

- Analyse wird nicht gestartet
- Fehlerstatus wird zurückgegeben

---

### Tatsächliches Ergebnis

- System gibt einen Fehlerstatus (`error`) zurück
- Analyse wird korrekt nicht gestartet

---

### Testergebnis

**Ergebnis:** bestanden

# Testprotokoll – Blackbox-Test

## E2E-01: Vollständiger Flow

**Datum:** 2026-01-07  
**Tester:** Leonid Tsarov  
**System:** Go-Live

### Testschritte

1. Login mit Benutzer `admin@admin.com`
2. Foto hochladen
3. Direkter Abruf des Eintrags (Statusabfrage)
4. Warten 5–10 Sekunden
5. Erneuter Abruf des Eintrags
6. Ergebnis prüfen

### Erwartetes Ergebnis

- Score > 0
- Kalorien > 0

### Tatsächliches Ergebnis

- **Schritt 3:** Testabbruch aufgrund eines Fehlers (`error`)
- Die weiteren Testschritte konnten **nicht ausgeführt** werden.

### Abweichungen / Fehlerbeschreibung

Der Test ist in **Schritt 3** fehlgeschlagen.  
Beim direkten Abruf des Eintrags wurde ein unerwarteter Fehler zurückgegeben, wodurch der End-to-End-Flow nicht
weitergeführt werden konnte.

### Tatsächliche Response (Schritt 3)

Beim direkten Abruf des Eintrags wurde folgende Response vom Backend zurückgegeben:

```json
{
  "id": "c69e5994-a0de-419d-a402-6412fcd11c01",
  "title": null,
  "notes": null,
  "context": "",
  "status": "error",
  "global_score": null,
  "created_at": "2026-01-07T13:12:56.82832Z",
  "nutrition": null,
  "photos": [
    "https://mealmind.edonssfall.com/mealmind/meals/c69e5994-a0de-419d-a402-6412fcd11c01/2511a4a1-1703-4257-a354-163a8475174c.jpg?x-id=GetObject&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=minioadmin%2F20260107%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20260107T141300Z&X-Amz-Expires=1800&X-Amz-SignedHeaders=host&X-Amz-Signature=1ece30a45d124e33fb62c5545bc9149d601a31a64ba68c01f4e2ff4695515e80"
  ]
}
```

### Testergebnis

**Ergebnis:** nicht bestanden

---

## E2E-02: Refresh-Token-Flow

**Datum:** 2026-01-07  
**Tester:** Leonid Tsarov  
**System:** Go-Live

### Testschritte

1. Login mit `admin@admin.com`
2. Erhalt eines Access- und Refresh-Tokens
3. Erneuerung des Access-Tokens über Refresh-Token
4. Aufruf des geschützten Endpunkts `GET /meals` mit neuem Access-Token

### Erwartetes Ergebnis

- Neuer Access-Token wird erfolgreich ausgestellt
- Zugriff auf geschützten Endpunkt ist möglich

### Tatsächliches Ergebnis

- Neuer Access-Token erfolgreich erhalten
- Geschützter Endpunkt `GET /meals` liefert gültige Antwort

### Testergebnis

**Ergebnis:** bestanden

---

## E2E-03: Fehlerhafte Eingaben

**Datum:** 2026-01-07  
**Tester:** Leonid Tsarov  
**System:** Go-Live

### Testschritte

1. Login mit `admin@admin.com`
2. Upload eines leeren oder beschädigten Fotos
3. Start der Analyse

### Erwartetes Ergebnis

- Analyse wird nicht gestartet
- Fehlerstatus wird zurückgegeben

### Tatsächliches Ergebnis

- System gibt einen Fehlerstatus (`error`) zurück
- Analyse wird korrekt nicht gestartet

### Testergebnis

**Ergebnis:** bestanden

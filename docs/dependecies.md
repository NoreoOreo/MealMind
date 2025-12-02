# [Home](../README.md)

## Abhängigkeiten und Integrationsrisiken

Die Anwendung besteht aus mehreren gekoppelten Komponenten (Frontend, Backend, PostgreSQL, MinIO, OpenAI-API). Diese
Abhängigkeiten werden bewusst dokumentiert und bei der Planung von Deployments und Tests berücksichtigt.

### Übersicht der wichtigsten Abhängigkeiten

| Komponente     | Abhängigkeit             | Mögliche Probleme                                       | Strategie zur Minimierung                                                  |
|----------------|--------------------------|---------------------------------------------------------|----------------------------------------------------------------------------|
| Backend (Rust) | PostgreSQL               | DB nicht erreichbar, Migrationsfehler, Schema-Konflikte | Klare Migrationsstrategie, lokale Test-DB, Health-Checks                   |
| Backend (Rust) | MinIO                    | Bucket/Keys falsch, Upload schlägt fehl                 | Konfig via ENV, Start-Checks, Logging bei Fehlern                          |
| Backend (Rust) | OpenAI Vision API        | Rate-Limits, Timeout, API-Änderungen                    | Timeouts, Retries, Mock-Service für Tests, Feature-Flag                    |
| Frontend (RN)  | Backend-API              | API nicht erreichbar oder Response-Format geändert      | Versionierte Endpunkte, Fehler-Handling im Client, Container Versionierung |
| CI/CD (GitHub) | Docker / Registry (GHCR) | Build schlägt fehl, Image nicht pushbar                 | Fixe Basis-Images, Lint + Tests vor Build                                  |

### Umgang mit Abhängigkeitsproblemen

- **Versionierung:** Wichtige Libraries und Docker-Images werden mit fixen Versionen verwendet (keine „latest“-Tags).
- **Mocks & Staging:** Für Tests wird die OpenAI-Integration teilweise gemockt, um Ausfälle oder Kosten zu vermeiden.
- **Fehler-Handling:** Das Backend behandelt Netzwerkfehler (DB, MinIO, OpenAI) mit Timeouts, sinnvollen Fehlermeldungen
  und Logging.
- **Monitoring:** Logfiles und (optional) Metrics helfen, Integrationsprobleme früh zu erkennen (z. B. häufige
  Timeouts).


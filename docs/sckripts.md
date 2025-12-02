# [Home](../README.md)

## Automatisierung & Umgebungskonfiguration

Zur Vereinfachung wiederkehrender Aufgaben (Build, Test, Deployment) werden Automatisierungs­skripte und definierte
Umgebungsvariablen eingesetzt.

### Automatisierungs-Skripte

- Für die Backend-Authentifizierung wurde ein **E2E-Skript** erstellt, das den gesamten Flow automatisiert ausführt:
    - Registrierung
    - Login
    - Token-Refresh
      Dies ermöglicht wiederholbare Release-Tests ohne manuelles Durchklicken.

- Weitere automatisierte Abläufe:
    - `cargo fmt`, `cargo clippy` und `cargo test` über GitHub Actions
    - automatischer Docker-Build und Push bei Tags
    - lokales Starten von Backend/DB/MinIO mit `docker compose`

### Umgebungsvariablen

Es werden zwei Kategorien unterschieden:

1. **Build-/Test-Variablen**  
   Werden für Linting, Builds und Tests benötigt (z. B. `POSTGRES_DB`, `MINIO_ENDPOINT` im Testmodus).

2. **Runtime-Variablen (Betrieb)**  
   Notwendig für den täglichen Betrieb der Anwendung:
    - `JWT_SECRET`
    - `DATABASE_URL`
    - `MINIO_ACCESS_KEY`, `MINIO_SECRET_KEY`
    - `OPENAI_API_KEY`
    - Backend-Port/Konfiguration  
      Diese werden auf dem Server als sicher

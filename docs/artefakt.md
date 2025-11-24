# [Home](../README.md)

## Artefakt-Verwaltung und Versionierung

### Auswahl des Artefakt-Repositoriums (Evaluierung & Begründung)

Für die Verwaltung der Build-Artefakte wurden folgende Optionen betrachtet:  
- **Nexus / Artifactory**: mächtige, aber relativ schwere Lösungen mit zusätzlichem Betriebsaufwand.  
- **GitLab Package Registry**: sinnvoll bei GitLab als Hauptplattform.  
- **GitHub (Actions + Releases + GHCR)**: nahtlos integriert in das bestehende Repository, kein zusätzlicher Server nötig.

Da das Projekt bereits vollständig auf **GitHub** basiert, wurde entschieden, die Artefakt-Verwaltung ebenfalls dort zu integrieren:

- **GitHub Actions Artefakte** für temporäre Build-Artefakte (z. B. der Rust-Binary für Tests und Release).
- **GitHub Container Registry (GHCR)** für veröffentlichte Docker-Images des Backends.

Externe Lösungen wie Nexus oder Artifactory wären für den Projektumfang überdimensioniert.

### Versionierung der Artefakte

Es wird eine **SemVer-Strategie** verwendet:

- Git-Tags im Format `vMAJOR.MINOR.PATCH` (z. B. `v1.0.0`).
- Der Tag-Name wird:
  - als Version des Backends verwendet,
  - als Docker-Tag im GHCR genutzt (z. B. `ghcr.io/org/mealmind-backend:v1.0.0`),
  - in GitHub Releases und Artefaktnamen übernommen.

Damit ist nachvollziehbar, welche Artefakte zu welchem Release gehören.

### Nutzung der Artefakte im Build-/Testprozess

Zur Vermeidung doppelter Builds und unnötiger Download-Zeiten wird folgender Prozess eingesetzt:

1. **Build-Job**
   - Rust-Dependencies werden per **Cache** wiederverwendet (schnellere Builds).
   - Es wird genau **ein Backend-Binary** gebaut.
   - Dieses Binary wird als **GitHub Actions Artefakt** gespeichert.

2. **Test-Job**
   - Lädt dasselbe Binary-Artefakt herunter.
   - Führt darauf basierend Integrationstests und E2E-Tests aus (z. B. kompletter Auth-Flow).
   - Dadurch wird sichergestellt, dass genau der getestete Stand später ausgeliefert wird.

3. **Release-/Image-Job (bei Tag)**
   - Nutzt erneut dasselbe Binary-Artefakt.
   - Verpackt es in ein Docker-Image und pusht es in **GHCR**.
   - Kein erneuter Build nötig → weniger Fehlerquellen, identischer Stand wie im Test.

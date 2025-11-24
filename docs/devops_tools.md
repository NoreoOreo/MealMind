# [Home](../README.md)

Für die Entwicklung wird eine einheitliche Umgebung verwendet, die für alle Teammitglieder reproduzierbar ist. Die
folgende Tabelle zeigt die eingesetzten Tools entlang des DevOps-Lifecycles:

| DevOps-Phase | Tool                  |
|--------------|-----------------------|
| Plan         | Git                   |
| Code         | VS Code / RustRover   |
| Build        | Docker                |
| Test         | GitHub Actions        |
| Release      | GitHub Actions (Tags) |
| Deploy       | Docker Compose        |
| Operate      | Logfiles / Monitoring |
| Monitor      | Grafana (optional)    |

### Kurzbeschreibung der Einrichtung

- Git, Docker und die Rust-Toolchain installieren
- Repository klonen
- Backend per `docker compose up` starten
- Frontend per `npm install` und `expo start` ausführen

Diese Schritte reichen aus, damit Teammitglieder die Entwicklungsumgebung schnell und konsistent aufsetzen können.

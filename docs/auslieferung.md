# [Home](../README.md)

## Services für die Auslieferung

### Architekturübersicht

Das System besteht aus folgenden Kernkomponenten:

- nginx als Reverse Proxy und TLS-Termination
- Docker Compose zur Verwaltung aller Services (Backend, DB, MinIO usw.)
- Let's Encrypt / certbot für automatische SSL-Zertifikate
- rsync für täglichen Datenabgleich von Produktion → Entwicklung
- Cron-Jobs für Automatisierungsaufgaben

Die Produktionsdaten liegen in `./data`, die Entwicklungsdaten in `./dev-data`.

### TLS und Reverse Proxy

- Für die Domains

    - `mealmind.edonssfall.com`

    - `dev.mealmind.edonssfall.com`

      werden per certbot automatisch Let's-Encrypt-Zertifikate erstellt.

- nginx nutzt diese Zertifikate und wird bei Änderungen automatisch neu geladen.

- Ein täglicher Cron-Job führt

    ```
    certbot renew --deploy-hook "systemctl reload nginx"
    ```

    aus.

Damit bleibt das System dauerhaft verschlüsselt und wartungsarm.

### Datenverwaltung und Sync

- Produktionsservices speichern Daten unter `./data`.

- Entwicklungsservices nutzen `./dev-data`.

- Ein Cron-Job synchronisiert täglich um 02:00 Uhr:

    ```
    rsync -a --delete data/ dev-data/
    ```

So wird eine realistische Testumgebung gewährleistet, ohne Produktionssysteme zu beeinflussen.

### Service-Betrieb (Docker Compose)

Die Umgebung ist vollständig containerisiert:

- Start Produktion:

    ```
    docker compose -f compose.yaml up -d
    ```

- Start Entwicklung:

    ```
  docker compose -f dev-compose.yaml up -d
    ```

- Images werden automatisch aktualisiert (CI/CD), danach wird auf dem Server ausgeführt:
    ```
    docker compose pull
    docker compose up -d
    docker system prune -f
    ```

Docker ermöglicht einfache Updates, Rollbacks und horizontale Skalierung (mehrere Containerinstanzen möglich).

### Wartbarkeit

Das System ist wartbar durch:

- Automatisiertes Setup (nginx, SSL, Cron)

- Trennung von Prod- und Dev-Umgebungen

- Versionierte Konfiguration (docker-compose + Templates)

- Automatische Zertifikats- und Datenpflege

- Minimaler manueller Aufwand im Betrieb

### Skalierbarkeit

- Durch Docker kann das Backend später horizontal skaliert werden.

- nginx kann als Load Balancer erweitert werden.

- Die Containerarchitektur unterstützt Migration zu Kubernetes ohne strukturelle Änderungen.

- Prod und Dev sind sauber getrennt und unterstützen parallele Entwicklung.

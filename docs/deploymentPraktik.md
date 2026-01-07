# Evaluierung der Deployment-Strategie und Dokumentation des Deployment-Prozesses  

## 1. Ziel des Dokuments

Dieses Dokument beschreibt die **Evaluierung und Auswahl einer geeigneten Deployment-Strategie** für das Projekt *MealMind*.  
Zusätzlich wird der **gesamte Deployment-Prozess** inklusive aller notwendigen Schritte, Werkzeuge und Abhängigkeiten dokumentiert.

Ziel ist es, Deployments **sicher, nachvollziehbar und reproduzierbar** durchführen zu können und das Risiko von Ausfällen oder fehlerhaften Releases zu minimieren.

---

## 2. Ausgangslage im Projekt

MealMind ist eine containerisierte Anwendung mit folgenden Eigenschaften:

- Mobile App (React Native)
- Backend (Rust / Axum)
- PostgreSQL-Datenbank
- MinIO (S3-kompatibler Objektspeicher)
- Deployment via Docker auf einem Server
- CI/CD über GitHub Actions
- Images in GitHub Container Registry (GHCR)

Das Deployment erfolgt **serverseitig** und wird bewusst einfach gehalten, da es sich um ein MVP- bzw. Schulprojekt handelt.

---

## 3. Evaluierung möglicher Deployment-Strategien

### 3.1 Blue-Green-Deployment

**Beschreibung:**  
Beim Blue-Green-Deployment existieren zwei identische Produktionsumgebungen:
- *Blue* (aktuell aktiv)
- *Green* (neue Version)

Nach erfolgreichem Test der neuen Version wird der Traffic auf die neue Umgebung umgeschaltet.

**Vorteile**
- Nahezu keine Downtime
- Einfaches Rollback durch Umschalten
- Sehr stabile Releases

**Nachteile**
- Doppelter Ressourcenbedarf
- Höherer Infrastruktur- und Konfigurationsaufwand
- Für kleine Projekte oft überdimensioniert

---

### 3.2 Rolling Updates

**Beschreibung:**  
Bei Rolling Updates werden bestehende Services schrittweise durch neue Versionen ersetzt, während das System weiterläuft.

**Vorteile**
- Geringerer Ressourcenbedarf
- Einfache Umsetzung
- Gut geeignet für containerisierte Anwendungen

**Nachteile**
- Kurzzeitig können unterschiedliche Versionen parallel laufen
- Rollback etwas aufwendiger als bei Blue-Green

---

## 4. Auswahl der Deployment-Strategie

### 4.1 Entscheidung

Für das Projekt wurde **kein vollständiges Blue-Green-Deployment**, sondern ein **vereinfachtes Rolling-Update-ähnliches Verfahren** gewählt.

### Begründung:
- MVP-Charakter des Projekts
- Begrenzte Server-Ressourcen
- Fokus auf Einfachheit und Nachvollziehbarkeit
- Docker-basierte Infrastruktur ohne Orchestrator (z. B. Kubernetes)

Das Deployment erfolgt durch:
- Austausch des Docker-Images
- Neustart des entsprechenden Containers

Diese Strategie bietet einen **guten Kompromiss zwischen Stabilität und Aufwand**.

---

## 5. Verwendete Tools im Deployment-Prozess

| Bereich        | Tool / Technologie              |
|---------------|----------------------------------|
| Versionskontrolle | Git / GitHub                 |
| CI/CD         | GitHub Actions                   |
| Containerisierung | Docker                       |
| Registry      | GitHub Container Registry (GHCR) |
| Deployment    | Docker Compose                   |

---

## 6. Dokumentation des Deployment-Prozesses

### 6.1 Voraussetzungen

- Zugriff auf den Server (SSH)
- Docker und Docker Compose installiert
- Zugriff auf GitHub Container Registry
- Gültige Environment-Variablen (Secrets)

---

### 6.2 Schritt-für-Schritt Deployment

#### 1. Code-Änderung
- Entwicklung in Feature-Branch
- Merge in `main` nach Review

#### 2. CI-Phase
- Automatische Tests und Linter über GitHub Actions
- Build-Überprüfung

#### 3. Release-Erstellung
- Erstellung eines Git-Tags (`vX.Y.Z`)
- Trigger für CD-Pipeline

#### 4. Build & Push
- Docker-Image wird gebaut
- Image wird mit Versionstag in GHCR veröffentlicht

#### 5. Deployment auf dem Server
- Server zieht neues Image (`docker compose pull`)
- Container werden neu gestartet (`docker compose up -d`)
- Alte Container werden ersetzt

#### 6. Post-Deployment-Check
- Kurzer Funktionstest
- Prüfung der Logs
- Kontrolle der wichtigsten Endpunkte

---

## 7. Rollback-Strategie

Falls ein Fehler nach dem Deployment auftritt:

1. Rückkehr zur vorherigen Version:
   - Anpassung des Image-Tags im `compose.yml`
2. Neustart der Container
3. Überprüfung der Funktionalität

Dank versionierter Docker-Images ist ein Rollback **schnell und zuverlässig** möglich.

---

## 8. Sicherheit und Stabilität beim Deployment

- Secrets werden **nicht im Code** gespeichert
- Deployment erfolgt nur mit getesteten Images
- Keine direkten Änderungen auf dem Live-System
- Logs werden nach jedem Release überprüft

---

## 9. Bewertung der gewählten Strategie

**Vorteile**
- Einfacher Deployment-Prozess
- Geringes Fehlerrisiko
- Gut geeignet für kleine Teams
- Klare Nachvollziehbarkeit

**Einschränkungen**
- Kurze Downtime beim Neustart möglich
- Keine parallelen Produktionsumgebungen

Für den aktuellen Projektumfang ist die gewählte Strategie **zweckmässig und effizient**.

---

## 10. Zusammenfassung

Die Evaluierung hat gezeigt, dass ein **vereinfachtes Rolling-Update-Verfahren** für das MealMind-Projekt die beste Lösung darstellt.

Durch:
- Docker-basierte Deployments
- CI/CD mit GitHub Actions
- Versionierte Images
- Klare Dokumentation  

wird ein stabiler, wartbarer und transparenter Deployment-Prozess gewährleistet.

Die gewählte Deployment-Strategie unterstützt die Projektziele optimal und kann bei Bedarf in Zukunft erweitert werden (z. B. Blue-Green oder Orchestrierung).

---

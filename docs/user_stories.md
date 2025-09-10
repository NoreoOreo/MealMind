# [Home](../README.md)
# User Stories
## 1. Registrieren und anmelden
**Als Nutzer**
möchte ich mich bei der App registrieren und anmelden können,
**um** meine persönlichen Daten, Ernährungshistorie und Einstellungen jederzeit abrufen zu können.
### Akzeptanzkriterien:
1. Registrierung mit E-Mail und Passwort möglich.
2. Optionale Anmeldung via Social Login (z. B. Google, Apple).
3. Sichere Passwortverschlüsselung im Backend.
4. Nach Anmeldung Zugriff auf persönliche Ernährungs- und Menü-Daten.
5. Fehlermeldungen bei falschen Login-Daten.

## 2. Lebensmittel erfassen
**Als Nutzer**
möchte ich Lebensmittel per Barcode oder Foto scannen können,
**um** diese schnell und bequem meiner Ernährungsliste hinzuzufügen.
### Akzeptanzkriterien:
6. Barcode-Scanner erkennt gängige Lebensmittel.
7. Foto-Erkennung funktioniert für Standardprodukte.
8. Automatisches Hinzufügen zur Lebensmitteldatenbank des Nutzers.

## 3. Kalorien- und Nährwerte berechnen
**Als Nutzer**
möchte ich die Kalorien und Nährwerte meiner erfassten Lebensmittel sehen,
**um** einen Überblick über meine tägliche Ernährung zu behalten.
### Akzeptanzkriterien:
9. Kalorien, Makros (Eiweiß, Fett, Kohlenhydrate) und ggf. Mikronährstoffe werden angezeigt.
10. Tages- und Wochenübersicht verfügbar.
11. Möglichkeit, eigene Portionsgrößen einzutragen.

## 4. Personalisierte Menüvorschläge
**Als Nutzer**
möchte ich KI-gestützte Menüvorschläge basierend auf meinen Vorlieben und Zielen erhalten, 
**um** gesünder und abwechslungsreicher zu essen.
### Akzeptanzkriterien:
12. Berücksichtigung von Allergien, Diätformen und Kalorienziel.
13. Menüvorschläge variieren nach Saison und Vorräten.
14. Nutzer kann Vorschläge anpassen oder ablehnen.

## 5. Sichere und benutzerfreundliche Nutzung
**Als Nutzer**
möchte ich meine Daten sicher gespeichert wissen und die App intuitiv bedienen können,
**um** ohne Bedenken und mit wenig Aufwand meine Ernährung zu tracken.
### Akzeptanzkriterien:
15. Datenverschlüsselung im Backend.
16. Anmeldung per E-Mail/Passwort oder Social Login.
17. Klare Navigation und einfache Benutzeroberfläche.
 
## 6. Aufbau der Grundstruktur mit modernem Framework
**Als Entwickler**
möchte ich die Grundstruktur der App mit einem modernen Framework (z. B. React Native mit Backend-API) aufsetzen,
**um** eine saubere, erweiterbare und wartbare Basis für die weitere Entwicklung zu schaffen.
### Akzeptanzkriterien:
18. Projektstruktur ist klar definiert (Frontend, Backend, API).
19. Basisfunktionen (Navigation, State-Management, Authentifizierung) sind vorbereitet.
20. Code ist nach Best Practices organisiert (z. B. modulare Architektur, Linter/Formatter).
21. Kompatibilität mit iOS und Android ist getestet.

## 7. Einrichtung von CI/CD-Pipeline und Deployment-Infrastruktur
**Als Entwickler**
möchte ich eine CI/CD-Pipeline und Deployment-Infrastruktur einrichten,
**um** automatisierte Builds, Tests und Deployments sicherzustellen.
### Akzeptanzkriterien:
22. Code wird automatisch bei jedem Commit getestet und gebaut.
23. Automatisches Deployment auf Test- oder Staging-Umgebungen.
24. Rollback-Möglichkeit bei fehlerhaften Releases.
25. Dokumentation der Pipeline ist vorhanden.

## 8. Erstellung Mockups
**Als Entwickler**
möchte ich Mockups der App-Oberfläche erstellen,
**um** das Layout, die Farbwelt und die Benutzerführung frühzeitig visualisieren zu können.
### Akzeptanzkriterien:
26. Mockups zeigen die zentralen Screens (Startseite, Lebensmittelerfassung, Kalorienübersicht, Menüvorschläge, Einkaufslisten).
27. Design folgt modernen UI/UX-Prinzipien (klar, konsistent, mobilfreundlich).
28. Farb- und Typografie-Konzept ist definiert.
29. Mockups sind als Referenz für die spätere Entwicklung dokumentiert.

# Product Requirements Document (PRD)
## Smart-Plant-Monitor - IoT-Lernprojekt

**Version:** 1.0  
**Datum:** 24. Juli 2025  
**Autor:** Jana Maire  

---

## Inhaltsverzeichnis
1. [Vision & Projektziele](#1-vision--projektziele)
2. [Stakeholder & User Stories](#2-stakeholder--user-stories)
3. [Funktionale Anforderungen](#3-funktionale-anforderungen)
4. [Nicht-funktionale Anforderungen](#4-nicht-funktionale-anforderungen)
5. [Systemgrenzen & Scope](#5-systemgrenzen--scope)
6. [Akzeptanzkriterien](#6-akzeptanzkriterien)
7. [Risiken & Abhängigkeiten](#7-risiken--abhängigkeiten)
8. [Erfolgs-Metriken](#8-erfolgs-metriken)
9. [Nice-to-Have Features](#9-nice-to-have-features-optional)

---

### 1. Vision & Projektziele

**Vision:**
Ein intelligentes Pflanzenüberwachungssystem, das mittels IoT-Technologien das Wohlbefinden von Zimmerpflanzen kontinuierlich überwacht, visuell darstellt und bei kritischen Zuständen warnt.

**Primäres Ziel:**
Praktisches Erlernen moderner IoT-Architekturprinzipien durch Entwicklung eines End-to-End-Systems mit realistischem Anwendungsfall.

**Sekundäre Ziele:**
- Vertiefung von MicroPython, Docker, MQTT, BLE-Kommunikation
- Implementierung einer 3-Tier IoT-Architektur
- Vorbereitung für spätere Cloud-Migration
- Aufbau eines wiederverwendbaren IoT-Frameworks

### 2. Stakeholder & User Stories

**Primärer Nutzer:** Pflanzenliebhaberin mit technischem Interesse

**User Stories:**

*Als Pflanzenbesitzerin möchte ich...*
- **US1:** die aktuelle Temperatur und Luftfeuchtigkeit meiner Pflanzenumgebung sehen
- **US2:** den Feuchtigkeitsgrad der Erde meiner Pflanze überwachen
- **US3:** die Lichtverhältnisse meiner Pflanze verfolgen
- **US4:** sofort visuell erkennen, wenn meine Pflanze Aufmerksamkeit braucht (Ampel)
- **US5:** aktuelle Werte direkt am Gerät ablesen können (LED-Display)
- **US6:** historische Daten in ansprechenden Diagrammen visualisieren
- **US7:** Trends und Muster im Pflanzenwachstum erkennen
- **US8:** automatische Benachrichtigungen bei kritischen Zuständen erhalten

### 3. Funktionale Anforderungen

#### 3.1 Datenerfassung (ESP32)
- **FR1:** DHT22-Sensor erfasst Temperatur (±0.5°C) und Luftfeuchtigkeit (±2-5%)
- **FR2:** Bodenfeuchtigkeitssensor misst Substratfeuchtigkeit (0-100% relativ)
- **FR3:** Lichtsensor erfasst Beleuchtungsstärke (Lux-Werte)
- **FR4:** Messintervalle: Klima 5min, Bodenfeuchtigkeit 30min, Licht 10min
- **FR5:** Lokale Anzeige aktueller Werte auf LED-Display
- **FR6:** Status-Ampel zeigt Gesamtzustand (Grün/Gelb/Rot)

#### 3.2 Datenübertragung & -verarbeitung
- **FR7:** BLE-Kommunikation zwischen ESP32 und Raspberry Pi
- **FR8:** MQTT-Messaging für Datenweiterleitung Gateway → Cloud
- **FR9:** Node-RED Edge-Processing für Filterung und lokale Logik
- **FR10:** Node-RED Cloud-Processing für komplexe Datenanalyse

#### 3.3 Datenspeicherung & Visualisierung
- **FR11:** InfluxDB speichert Zeitreihendaten mit 1-Jahr Retention
- **FR12:** Grafana Dashboard mit Real-time und historischen Views
- **FR13:** Alerting bei Grenzwertüberschreitung

### 4. Nicht-funktionale Anforderungen

#### 4.1 Performance
- **NFR1:** Maximale Latenz Gateway → Cloud: 10 Sekunden
- **NFR2:** ESP32 Batterielebensdauer: mindestens 48h (bei USB-Versorgung optional)
- **NFR3:** System Verfügbarkeit: 95% (Lernprojekt-Standard)

#### 4.2 Skalierbarkeit & Wartbarkeit
- **NFR4:** Architektur unterstützt mehrere ESP32-Geräte
- **NFR5:** Docker-Container für einfache Deployment-Migration
- **NFR6:** Konfiguration über Config-Files, kein Hard-Coding

#### 4.3 Technische Constraints
- **NFR7:** MicroPython auf ESP32 für Rapid Prototyping
- **NFR8:** Docker für alle Service-Container
- **NFR9:** Git-Versionierung aller Code-Komponenten
- **NFR10:** Dokumentation in Markdown für GitHub

### 5. Systemgrenzen & Scope

#### Im Scope:
- Ein ESP32 mit einem Sensorset pro Pflanze
- Lokales Gateway (Raspberry Pi) für eine Wohnung
- Lokale "Cloud"-Simulation auf MacBook
- Basic Web-UI über Grafana
- Dokumentierte Migration-Vorbereitung

#### Explizit außerhalb des Scope:
- Mobile App-Entwicklung
- Produktives Cloud-Deployment
- Mehrbenutzersystem
- Automatische Bewässerung/Aktoren
- Maschinelles Lernen/KI-Features
- Kommerzielle Sicherheitsanforderungen

### 6. Akzeptanzkriterien

#### Minimum Viable Product (MVP):
- **AC1:** ESP32 sammelt alle 3 Sensorwerte und zeigt sie lokal an
- **AC2:** Daten werden via BLE zum Raspberry Pi übertragen
- **AC3:** Raspberry Pi leitet Daten via MQTT zum MacBook weiter
- **AC4:** Daten werden in InfluxDB gespeichert
- **AC5:** Grafana zeigt Live-Dashboard mit aktuellen Werten
- **AC6:** Ampel funktioniert basierend auf konfigurierbaren Schwellenwerten

#### Definition of Done:
- Code ist kommentiert und in Git versioniert
- Docker-Setup funktioniert mit einem Befehl
- README enthält vollständige Setup-Anleitung
- Mindestens ein Grafana-Dashboard ist konfiguriert
- System läuft 24h stabil durch

### 7. Risiken & Abhängigkeiten

#### Technische Risiken:
- **R1:** BLE-Reichweite könnte für gewünschte Aufstellung unzureichend sein
- **R2:** ESP32-Stromverbrauch höher als erwartet
- **R3:** Docker-Container auf Raspberry Pi 5 mit Performance-Problemen

#### Lernkurve Risiken:
- **R4:** MicroPython BLE-Implementierung komplexer als erwartet
- **R5:** Node-RED Flow-Programmierung benötigt Einarbeitung

#### Abhängigkeiten:
- **D1:** Funktionierendes WiFi-Netzwerk für MQTT-Kommunikation
- **D2:** Raspberry Pi 5-Setup und -Konfiguration
- **D3:** Verfügbarkeit aller Hardware-Komponenten

### 8. Erfolgs-Metriken

**Technische Metriken:**
- Datenübertragung funktioniert ohne Verluste über 24h
- Setup-Zeit für Neuinstallation < 30 Minuten
- Alle Container starten erfolgreich mit `docker-compose up`

**Lern-Metriken:**
- Verständnis für 3-Tier IoT-Architektur entwickelt
- BLE- und MQTT-Protokolle praktisch implementiert
- Docker-Multi-Container-Setup gemeistert
- Grafana-Dashboard-Erstellung erlernt

**Anwendungs-Metriken:**
- System erkennt zuverlässig, wenn Pflanze Wasser braucht
- Historische Trends sind in Grafana sichtbar
- Ampel-Status entspricht tatsächlichem Pflanzenzustand

### 9. Nice-to-Have Features (Optional)

#### 9.1 Sicherheitsfeatures
- **NTH1:** Basis-Firewall Konfiguration auf Raspberry Pi
- **NTH2:** MQTT-Broker mit Authentifizierung (Username/Password)
- **NTH3:** SSL/TLS-Verschlüsselung für MQTT-Kommunikation
- **NTH4:** Grafana mit Login-Schutz
- **NTH5:** SSH-Schlüssel statt Passwort-Authentication
- **NTH6:** Regelmäßige automatische System-Updates

#### 9.2 ESP32-Cam Integration
- **NTH7:** ESP32-Cam erfasst Pflanzenbilder (1x täglich)
- **NTH8:** Bilder werden via HTTP/FTP zum Gateway übertragen
- **NTH9:** Grafana zeigt neuestes Pflanzenbild im Dashboard
- **NTH10:** Zeitraffer-Funktionalität für Pflanzenwachstum
- **NTH11:** Bildarchivierung mit Datum/Zeit-Stempel

---

**Änderungshistorie:**
- v1.0 (24.07.2025): Initiale Version mit Nice-to-Have Features

**Nächste Schritte:**
- Detaillierter Projektplan mit Meilensteinen
- GitHub-Repository-Setup
- "Hello World"-Test-Definition
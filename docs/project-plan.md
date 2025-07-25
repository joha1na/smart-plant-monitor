# Projektplan - Smart-Plant-Monitor
## IoT-Lernprojekt-Roadmap

**Version:** 1.2  
**Datum:** 25. Juli 2025  
**Projektdauer:** 5 Tage (à 6 Stunden) + 1 optionaler Tag  
**Gesamtaufwand:** ~30 Stunden  

---

## Inhaltsverzeichnis
1. [Projektübersicht](#1-projektübersicht)
2. [Sprint-Planung & Meilensteine](#2-sprint-planung--meilensteine)
3. [Abhängigkeiten & Kritischer Pfad](#3-abhängigkeiten--kritischer-pfad)
4. [Risikoanalyse & Mitigation](#4-risikoanalyse--mitigation)
5. [Ressourcenplanung](#5-ressourcenplanung)
6. [Sprint-Tracking](#6-sprint-tracking)

---

## 1. Projektübersicht

**Gesamtaufwand:** ~30 Stunden (5 Tage à 6h + 1 optionaler Tag)  
**Anzahl Sprints:** 5 Sprints à 1 Tag + 1 optionaler Sprint  
**Team:** 1 Entwicklerin (Lernprojekt)  
**Technologie-Stack:** ESP32, Raspberry Pi 5, Docker, Python, Node-RED, MQTT, BLE  

---

## 2. Sprint-Planung & Meilensteine

### 🚀 **Sprint 1: Foundation & Setup** (Tag 1 - 6h)
**Sprint Goal:** Entwicklungsumgebung und "Hello World"-System

#### Vormittag (3h):
- [ ] **PROJ-001** GitHub-Repository mit kompletter Struktur erstellen (45min)
- [ ] **PROJ-002** README.md und PRD ins Repository (30min)
- [ ] **PROJ-003** Docker-Compose für MacBook (InfluxDB, Grafana, Node-RED) (60min)
- [ ] **PROJ-004** Docker-Compose für Raspberry Pi (Mosquitto, Node-RED) (45min) 

#### Nachmittag (3h):
- [ ] **PROJ-005** Raspberry Pi 5-OS-Installation und Docker-Setup (120min)
- [ ] **PROJ-006** SSH-Zugang und Basis-Konfiguration (30min)
- [ ] **TEST-001** Alle Docker-Container erfolgreich starten (30min)

**Definition of Done:**
- Repository ist vollständig auf GitHub
- Alle Docker-Container laufen ohne Fehler
- Raspberry Pi ist entwicklungsbereit

**🔥 Prioritäten:**
- GitHub-Repository-Setup
- Docker-Environments
- Raspberry Pi-Konfiguration

---

### 🔗 **Sprint 2: BLE-Communication** (Tag 2 - 6h)
**Sprint Goal:** ESP32 ↔ Raspberry Pi BLE-Kommunikation etablieren

#### Vormittag (3h):
- [ ] **ESP-001** MicroPython auf ESP32 installieren (Thonny-Setup) (45min)
- [ ] **ESP-002** BLE-Server "Hello World" implementieren (90min)
- [ ] **ESP-003** Basis-LED-Test für Status-Anzeige (45min)

#### Nachmittag (3h):
- [ ] **RPI-001** Python-BLE-Client-Service entwickeln (90min)
- [ ] **RPI-002** MQTT-Bridge-Service implementieren (60min)
- [ ] **TEST-002** End-to-End BLE → MQTT → InfluxDB-Test (30min)

**Testkriterien:**
- ESP32 sendet zuverlässig BLE-Nachrichten
- Raspberry Pi empfängt und leitet via MQTT weiter
- Daten erscheinen in InfluxDB

**⚡ Prioritäten:**
- ESP32 MicroPython-Setup
- BLE-Kommunikation
- End-to-End Test

---

### 📊 **Sprint 3: Sensor-Integration** (Tag 3 - 6h)
**Sprint Goal:** Vollständige Sensordatenerfassung und lokale Anzeige

#### Vormittag (3h):
- [ ] **ESP-004** DHT22-Sensor-Integration und Kalibrierung (75min)
- [ ] **ESP-005** Bodenfeuchtigkeitssensor-Integration (60min)
- [ ] **ESP-006** Lichtsensor-Integration (45min)

#### Nachmittag (3h):
- [ ] **ESP-007** LED-Display für aktuelle Messwerte programmieren (90min)
- [ ] **ESP-008** Ampel-Logic mit konfigurierbaren Schwellenwerten (60min)
- [ ] **TEST-003** Alle Sensoren + Anzeigen funktional testen (30min)

**Testkriterien:**
- Alle 3 Sensoren liefern plausible, kalibrierte Werte
- LED-Display zeigt rotierend alle aktuellen Messwerte
- Ampel reagiert korrekt auf definierte Schwellenwerte

**📊 Prioritäten:**
- Sensor-Integration
- LED-Display
- Ampel-Logik

---

### 🎯 **Sprint 4: Cloud-Pipeline & Dashboards** (Tag 4 - 6h)
**Sprint Goal:** Vollständige Datenvisualisierung und -analyse

#### Vormittag (3h):
- [ ] **RPI-003** Node-RED-Edge-Flows für Datenvalidierung (75min)
- [ ] **CLOUD-001** InfluxDB-Datenbank-Schema optimieren (45min)
- [ ] **CLOUD-002** Node-RED-Cloud-Flows für Datenanalyse (60min)

#### Nachmittag (3h):
- [ ] **CLOUD-003** Grafana-Dashboard: Real-time Sensor Values (75min)
- [ ] **CLOUD-004** Grafana-Dashboard: Historical Trends (60min)
- [ ] **CLOUD-005** Grafana-Alerting-Rules konfigurieren (45min)

**Testkriterien:**
- Node-RED verarbeitet Daten ohne Fehler
- Grafana zeigt Live-Daten aller Sensoren
- Alerts werden bei Grenzwertüberschreitung ausgelöst

**🎯 Prioritäten:**
- Node-RED-Flows
- Grafana-Dashboards
- Alerting-System

---

### 📚 **Sprint 5: Stabilization & Documentation** (Tag 5 - 6h)
**Sprint Goal:** Production-Ready-System mit kompletter Dokumentation

#### Vormittag (3h):
- [ ] **SYS-001** Error-Handling und Retry-Logic in allen Services (90min)
- [ ] **SYS-002** Configuration Files für einfaches Deployment (60min)
- [ ] **SYS-003** Systemd-Services für Auto-Start (30min)

#### Nachmittag (3h):
- [ ] **DOC-001** Kompletter Setup-Guide mit Screenshots (90min)
- [ ] **DOC-002** Troubleshooting-Guide und FAQ (45min)
- [ ] **DOC-003** Architektur-Diagramme und Code-Dokumentation (45min)
- [ ] **TEST-004** 24h-Stabilitätstest-Setup und -Start (30min)

**Definition of Done:**
- System startet vollständig automatisch nach Reboot
- Komplette Neuinstallation dauert < 45min
- 24h-Test läuft ohne Ausfälle

**📚 Prioritäten:**
- Error-Handling
- Dokumentation
- Stabilitätstest

---

### 🎁 **Sprint 6: Nice-to-Haves** (Tag 6 - 6h) - Optional
**Sprint Goal:** Sicherheitsfeatures und ESP32-Cam Integration

#### Vormittag (3h):
- [ ] **SEC-001** UFW-Firewall auf Raspberry Pi (45min)
- [ ] **SEC-002** MQTT-Broker mit Username/Password-Auth (60min)
- [ ] **SEC-003** Grafana mit Login-Protection (45min)
- [ ] **SEC-004** SSH-Key-based Authentication (30min)

#### Nachmittag (3h):
- [ ] **CAM-001** ESP32-Cam Hardware-Integration (60min)
- [ ] **CAM-002** Bild-Capture und Upload-Service (90min)
- [ ] **CAM-003** Grafana-Image-Panel-Integration (30min)

**🎁 Prioritäten:**
- Sicherheitsfeatures
- ESP32-Cam-Integration

---

## 3. Abhängigkeiten & Kritischer Pfad

### Kritischer Pfad (keine Parallelisierung möglich):
Tag 1: PROJ-005 (RPi Setup) →
Tag 2: ESP-002 (BLE Server) → RPI-001 (BLE Client) →
Tag 3: ESP-004/005/006 (Sensoren) →
Tag 4: CLOUD-003/004 (Dashboards) →
Tag 5: TEST-004 (Stabilitätstest)

### Parallelisierbare Arbeiten:
- **Tag 1:** Docker-Setup auf MacBook parallel zu RPi-Installation
- **Tag 3:** LED-Display parallel zu Sensor-Integration
- **Tag 4:** InfluxDB-Optimierung parallel zu Node-RED-Entwicklung
- **Tag 5:** Dokumentation während Stabilitätstest-Laufzeit

## 4. Risikoanalyse & Mitigation

| Risiko | Wahrscheinlichkeit | Impact | Mitigation | Backup-Plan |
|--------|-------------------|---------|------------|-------------|
| BLE-Implementierung zu komplex | Hoch | Mittel | 4h für BLE eingeplant | WiFi-MQTT als Alternative |
| Sensor-Kalibrierung schwierig | Mittel | Niedrig | Relative Werte nutzen | Mock-Daten für Tests |
| Docker Performance-Probleme | Niedrig | Hoch | Lite-Images verwenden | Native Installation |
| Zeitüberschreitung einzelner Tasks | Mittel | Niedrig | Buffer-Zeit eingeplant | Nice-to-Haves streichen |

## 5. Ressourcenplanung

### Hardware Checklist:
- ✅ ESP32-Development-Board mit USB-Kabel
- ✅ DHT22-Temperatur/Feuchtigkeitssensor
- ✅ Bodenfeuchtigkeitssensor
- ✅ Lichtsensor
- ✅ LED-Display-Module
- ✅ Ampel-LED (Rot/Gelb/Grün)
- ✅ Breadboard und Jumper-Kabel
- ✅ Raspberry Pi 5 mit SD-Karte (32GB+)
- ✅ MacBook für Development

### Software Preparation:
- [ ] Thonny-IDE für ESP32-Entwicklung installieren
- [ ] Docker-Desktop auf MacBook installieren
- [ ] SSH-Client (Terminal) konfigurieren
- [ ] Git für Repository-Management

## 6. Sprint-Tracking

Siehe [Sprint-Tracking](../docs/sprints/README.md)

---

**Daily Commitment:** 6 Stunden fokussierte Arbeit + 30min Planung/Review  
**Goal:** Funktionsfähiges Smart-Plant-Monitor-System
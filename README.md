# Smart-Plant-Monitor 🌱
## IoT-Lernprojekt - Intelligentes Pflanzenüberwachungssystem

Ein End-to-End IoT-System zur Überwachung von Zimmerpflanzen mit ESP32, Raspberry Pi 5 und Cloud-Analytics.

<!-- TEMPORÄR AUSGEBLENDET BIS SPRINT 5 
![Architektur Overview](docs/architecture-overview.png)
-->

**Status:** 🔄 In Development | **Version:** 1.0.0 | **Letztes Update:** 25. Juli 2025

## 🎯 Projektziel

Praktisches Erlernen moderner IoT-Architekturprinzipien durch Entwicklung eines funktionsfähigen Pflanzenüberwachungssystems mit 3-Tier-Architektur.

## ⭐ Key Features

- 🌡️ **Real-time Monitoring:** Live-Sensordaten (Temperatur, Feuchtigkeit, Licht, Bodenfeuchtigkeit)
- 📈 **Historical Analytics:** Langzeit-Trends und Muster-Erkennung
- 🚨 **Smart Alerts:** Ampel-System + Grafana-Benachrichtigungen
- 🖥️ **Local Display:** Aktuelle Werte direkt am ESP32-Display
- ☁️ **Cloud-Ready:** Einfache Migration zu echter Cloud-Infrastruktur
- 🐳 **Containerized:** Docker für alle Services

## 🏗️ Systemarchitektur

```
┌─────────────────────────────┐
│        CLOUD TIER           │  📊 MacBook (Cloud Simulation)
│  ┌─────────────────────┐    │  • InfluxDB (Datenspeicherung)
│  │    Docker Stack     │    │  • Grafana (Dashboards)
│  │  ┌───────────────┐  │    │  • Node-RED (Datenanalyse)
│  │  │ InfluxDB      │  │    │
│  │  │ Grafana       │  │    │
│  │  │ Node-RED      │  │    │
│  │  └───────────────┘  │    │
│  └─────────────────────┘    │
└─────────────────────────────┘
        ↑ MQTT over WiFi
┌─────────────────────────────┐
│       GATEWAY TIER          │  🖥️ Raspberry Pi 5
│  ┌─────────────────────┐    │  • MQTT-Broker (Mosquitto)
│  │   Local Services    │    │  • Node-RED-Edge
│  │  ┌───────────────┐  │    │  • BLE-Client-Service
│  │  │ Mosquitto     │  │    │  • Datenvorverarbeitung
│  │  │ Node-RED Edge │  │    │
│  │  │ BLE Service   │  │    │
│  │  └───────────────┘  │    │
│  └─────────────────────┘    │
└─────────────────────────────┘
        ↑ BLE
┌─────────────────────────────┐
│      CONSTRAINED TIER       │  📡 ESP32
│  ┌─────────────────────┐    │  • DHT22 (Temp/Humidity)
│  │      Sensors        │    │  • Bodenfeuchtigkeitssensor
│  │   ┌─────────────┐   │    │  • Lichtsensor
│  │   │ DHT22       │   │    │  • LED-Display
│  │   │ Soil        │   │    │  • Status-LED (Ampel)
│  │   │ Light       │   │    │  • BLE-Server
│  │   │ LED Display │   │    │
│  │   │ Ampel       │   │    │
│  │   └─────────────┘   │    │
│  └─────────────────────┘    │
└─────────────────────────────┘
```

## 🛠️ Hardware Requirements

### ESP32 Setup
- ✅ ESP32-Development-Board mit USB-Kabel
- ✅ DHT22-Temperatur/Feuchtigkeitssensor  
- ✅ Bodenfeuchtigkeitssensor
- ✅ Lichtsensor (LDR)
- ✅ LED-Display-Modul
- ✅ Ampel-LED (Rot/Gelb/Grün)
- ✅ Breadboard und Jumper-Kabel

### Gateway & Cloud
- ✅ Raspberry Pi 5 (4GB+ empfohlen)
- ✅ SD-Karte (32GB+ Class 10)
- ✅ MacBook für Cloud-Simulation

<!-- TEMPORÄR AUSGEBLENDET BIS FERTIGSTELLUNG
## 🚀 Quick Start

### Voraussetzungen
```bash
# Docker installieren (falls nicht vorhanden)
# Für macOS:
brew install --cask docker

# Für Raspberry Pi:
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```

### 1. Repository klonen
```bash
git clone https://github.com/jmaire/smart-plant-monitor.git
cd smart-plant-monitor
```

### 2. Cloud Setup (MacBook)
```bash
cd cloud/
docker-compose up -d

# Services prüfen
docker-compose ps
```

**Zugriff auf Services:**
- Grafana: http://localhost:3000 (admin/admin)
- InfluxDB: http://localhost:8086
- Node-RED: http://localhost:1881

### 3. Gateway Setup (Raspberry Pi)
```bash
cd raspberry-pi/
docker-compose up -d

# Logs verfolgen
docker-compose logs -f
```

### 4. ESP32 Setup
1. **Thonny IDE installieren:** [Download](https://thonny.org/)
2. **MicroPython flashen:** ESP32 mit USB verbinden
3. **Code uploaden:** Dateien aus `esp32/` Ordner

```bash
# ESP32 Code-Struktur
esp32/
├── main.py          # Hauptprogramm
├── sensors.py       # Sensor-Integration  
├── ble_server.py    # BLE Server
├── display.py       # LED Display
└── config.py        # Konfiguration
``` 
-->

<!-- TEMPORÄR AUSGEBLENDET BIS FERTIGSTELLUNG
## 📁 Projektstruktur

```
smart-plant-monitor/
├── README.md                    # Diese Datei
├── docs/                        # Projektdokumentation
│   ├── product-requirements.md  # PRD
│   ├── project-plan.md         # Detaillierter Projektplan
│   ├── architecture.md         # Technische Architektur
│   ├── setup-guide.md          # Setup-Anleitung
│   └── troubleshooting.md      # Problemlösungen
├── esp32/                       # ESP32 MicroPython Code
│   ├── main.py                 # Hauptprogramm
│   ├── sensors.py              # Sensor-Integration
│   ├── ble_server.py           # BLE Server
│   ├── display.py              # LED Display
│   └── config.py               # Konfiguration
├── raspberry-pi/                # Raspberry Pi Services
│   ├── docker-compose.yml      # Docker Setup
│   ├── services/               # Python Services
│   │   ├── ble_client.py       # BLE Client
│   │   └── mqtt_bridge.py      # MQTT Bridge
│   ├── node-red/               # Node-RED Flows
│   └── mosquitto/              # MQTT Broker Config
├── cloud/                       # MacBook Cloud Stack
│   ├── docker-compose.yml      # Docker Setup
│   ├── influxdb/               # Datenbank Config
│   ├── grafana/                # Dashboards
│   └── node-red-cloud/         # Cloud Datenanalyse
└── scripts/                     # Automatisierung
    ├── setup.sh                # Automatisches Setup
    └── deploy.sh               # Deployment
``` 
-->

## 🎓 Lernziele

- **IoT-Architektur:** 3-Tier-Design-Pattern verstehen
- **Protokolle:** BLE, MQTT, HTTP praktisch implementieren
- **Containerization:** Docker-Multi-ServiceSetup
- **Datenvisualisierung:** Grafana-Dashboard-Entwicklung
- **Edge Computing:** Raspberry Pi als IoT-Gateway
- **Embedded Programming:** ESP32-MicroPython

## 📈 Projektfortschritt

**Aktueller Sprint:** Foundation & Setup  
**Nächste Schritte:** Docker-Container Setup

- [ ] **Tag 1:** Foundation & Setup
- [ ] **Tag 2:** BLE-Communication
- [ ] **Tag 3:** Sensor-Integration
- [ ] **Tag 4:** Cloud-Pipeline & Dashboards
- [ ] **Tag 5:** Stabilization & Documentation
- [ ] **Tag 6:** Nice-to-Haves (Security, ESP32-Cam)

Detaillierter Projektplan: [docs/project-plan.md](docs/project-plan.md)

<!-- TEMPORÄR AUSGEBLENDET BIS FERTIGSTELLUNG
## 🔧 Development Commands

```bash
# Cloud Stack starten
cd cloud && docker-compose up -d

# Gateway Stack starten  
cd raspberry-pi && docker-compose up -d

# Logs anzeigen
docker-compose logs -f

# Container stoppen
docker-compose down

# System komplett zurücksetzen
docker-compose down -v
docker system prune -f
``` 
-->

<!-- TEMPORÄR AUSGEBLENDET BIS FERTIGSTELLUNG
## 🐛 Troubleshooting

**Häufige Probleme:**

| Problem | Lösung |
|---------|---------|
| Docker-Container starten nicht | `docker system prune -f` und erneut versuchen |
| BLE-Verbindung fehlgeschlagen | Raspberry Pi neustarten, BLE-Dienste prüfen |
| ESP32 nicht erkannt | USB-Kabel prüfen, Treiber installieren |
| Grafana zeigt keine Daten | InfluxDB-Verbindung in Datasource prüfen |

Vollständiges Troubleshooting: [docs/troubleshooting.md](docs/troubleshooting.md) 
-->

## 📝 Dokumentation

- 📋 [Product Requirements](docs/product-requirements.md)
- 📅 [Projektplan](docs/project-plan.md)
<!-- TEMPORÄR AUSGEBLENDET BIS ERSTELLUNG
- 🔧 [Setup Guide](docs/setup-guide.md)
- 🏗️ [Architecture Details](docs/architecture.md)  
-->
- 📊 [Sprint-Tracking](docs/sprints/README.md)

## 🤝 Contributing

Dies ist ein Lernprojekt. Feedback und Verbesserungsvorschläge sind herzlich willkommen!

1. Fork des Repositories
2. Feature-Branch erstellen (`git checkout -b feature/amazing-feature`)
3. Änderungen committen (`git commit -m 'Add amazing feature'`)
4. Branch pushen (`git push origin feature/amazing-feature`)
5. Pull Request erstellen

## 📄 License

tbd.
<!-- TEMPORÄR AUSGEBLENDET BIS ENTSCHEIDUNG
MIT License - Siehe [LICENSE](LICENSE) Datei für Details. 
-->

---

**Daily Commitment:** 6 Stunden fokussierte Arbeit + 30min Planung/Review  
**Projekt-Goal:** Funktionsfähiges Smart-Plant-Monitor-System mit vollständiger Dokumentation
# Raspberry Pi 5 Setup Guide
## Smart Plant Monitor - Komplette Installationsanleitung

**Version:** 1.0  
**Datum:** 25. Juli 2025  
**Getestet mit:** Raspberry Pi 5, macOS, Debian 12 (Bookworm)

---

## Inhaltsverzeichnis
1. [Hardware-Vorbereitung](#1-hardware-vorbereitung)
2. [OS-Installation](#2-os-installation)
3. [Erstkonfiguration](#3-erstkonfiguration)
4. [SSH-Verbindung](#4-ssh-verbindung)
5. [System-Update](#5-system-update)
6. [Docker-Installation](#6-docker-installation)
7. [Bluetooth-Setup](#7-bluetooth-setup)
8. [Repository-Setup](#8-repository-setup)
9. [Troubleshooting](#9-troubleshooting)
10. [Erfolgskriterien](#10-erfolgskriterien)

---

## 1. Hardware-Vorbereitung

### **Benötigte Hardware:**
- [ ] Raspberry Pi 5 (4GB+ empfohlen)
- [ ] MicroSD-Karte (32GB+, Class 10)
- [ ] SD-Karten-Adapter für MacBook
- [ ] USB-C Stromkabel für Pi 5
- [ ] Ethernet-Kabel (optional, als Backup)

### **Software-Vorbereitung:**
- [ ] Raspberry Pi Imager auf MacBook installieren
- [ ] WiFi-Zugangsdaten bereithalten
- [ ] Router-Interface-Zugang (für IP-Ermittlung)

---

## 2. OS-Installation

### **2.1 Raspberry Pi Imager Setup (5min)**

1. **Download:** https://www.raspberrypi.com/software/
2. **Installation:** DMG-Datei öffnen und in Applications ziehen
3. **Starten:** Raspberry Pi Imager öffnen

### **2.2 OS auswählen (2min)**

1. **"CHOOSE OS"** klicken
2. **"Raspberry Pi OS (other)"** auswählen  
3. **"Raspberry Pi OS Lite (64-bit)"** wählen
   - ✅ Lite = ohne Desktop (bessere Performance)
   - ✅ 64-bit = optimal für Pi 5

### **2.3 SD-Karte auswählen (1min)**

1. **SD-Karte** in MacBook einlegen
2. **"CHOOSE STORAGE"** klicken
3. **Ihre SD-Karte** auswählen
   - ⚠️ **Warnung:** Alle Daten gehen verloren!

### **2.4 Erweiterte Konfiguration (5min)**

**⚙️ Zahnrad-Symbol** klicken für erweiterte Optionen:

```
✅ Enable SSH
○ Use password authentication
✅ Set username and password
Username: pi
Password: [IHR SICHERES PASSWORT]
⚠️ WICHTIG: Passwort notieren!

✅ Configure wireless LAN
SSID: [IHR WIFI-NAME]
Password: [IHR WIFI-PASSWORT]
Wireless LAN country: DE

✅ Set locale settings
Time zone: Europe/Berlin
Keyboard layout: de
```

### **2.5 Image schreiben (10min)**

1. **"SAVE"** klicken
2. **"WRITE"** klicken
3. **Warnung bestätigen**
4. **Warten** bis "Write Successful" erscheint
5. **SD-Karte auswerfen**

---

## 3. Erstkonfiguration

### **3.1 Hardware aufbauen (2min)**

1. **SD-Karte** in Raspberry Pi einlegen (Kontakte nach unten)
2. **Stromkabel anschließen** - Pi startet automatisch
3. **Boot-Vorgang abwarten** (2-3 Minuten)
   - Rote LED = Strom vorhanden
   - Grüne LED blinkt = Boot läuft
   - Grüne LED konstant/aus = Boot fertig

### **3.2 WiFi-Troubleshooting (falls nötig)**

**Problem:** Pi erscheint nicht im Netzwerk

**Lösung: WiFi-Konfiguration manuell erstellen**

```bash
# SD-Karte wieder in MacBook einlegen
# Terminal öffnen und ausführen:

cd /Volumes/bootfs
# oder: cd /Volumes/boot

# WiFi-Konfiguration erstellen
nano wpa_supplicant.conf
```

**Inhalt der Datei:**
```
country=DE
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="IHR_WIFI_NAME"
    psk="IHR_WIFI_PASSWORT"
    key_mgmt=WPA-PSK
}
```

**SSH-Datei erstellen:**
```bash
touch ssh
# SD-Karte auswerfen und wieder in Pi einlegen
```

---

## 4. SSH-Verbindung

### **4.1 IP-Adresse ermitteln**

#### **Methode 1: Router-Interface (empfohlen)**

1. Browser öffnen: `http://192.168.1.1` oder `http://192.168.2.1`
2. Im Router anmelden
3. "Connected Devices" oder "DHCP Clients" suchen
4. Nach "raspberry" oder "pi" suchen

#### **Methode 2: Netzwerk-Scan**
```bash
# Für 192.168.1.x Netze:
nmap -sn 192.168.1.0/24 | grep -A1 -i raspberry

# Für 192.168.2.x Netze:  
nmap -sn 192.168.2.0/24 | grep -A1 -i raspberry

# Falls nmap Probleme macht:
arp -a | grep 192.168.1
```

#### **Methode 3: Manual Ping**
```bash
# Häufige Pi-IPs testen:
ping -c 1 192.168.1.100
ping -c 1 192.168.1.101
ping -c 1 192.168.2.100
ping -c 1 192.168.2.101
```

### **4.2 SSH-Verbindung aufbauen**

```bash
# SSH zum Pi (IP durch Ihre echte ersetzen)
ssh pi@192.168.1.100
```

**Beim ersten Verbindungsaufbau:**
```
The authenticity of host '192.168.1.100' can't be established.
ECDSA key fingerprint is SHA256:...
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```
**Antworten:** `yes`  
**Passwort eingeben:** Das Passwort aus der Konfiguration

**Erfolgreich verbunden:**
```
pi@raspberrypi:~ $
```

---

## 5. System-Update

### **5.1 System-Info prüfen**

```bash
# Systeminfo anzeigen
uname -a
cat /etc/os-release
```

**Erwartete Ausgabe:**
```
Linux raspberrypi 6.12.25+rpt-rpi-2712 #1 SMP PREEMPT Debian...
PRETTY_NAME="Debian GNU/Linux 12 (bookworm)"
```

### **5.2 Vollständiges System-Update (10min)**

```bash
# Paketlisten aktualisieren und System upgraden
sudo apt update && sudo apt upgrade -y
```

**Bei Konfigurationsdateien-Abfragen:**
```
Configuration file '/etc/...' 
==> Modified (by you or by a script) since installation.
==> Package distributor has shipped an updated version.
   What would you like to do about it ?
*** initramfs.conf (Y/I/N/O/D/Z) [default=N] ?
```
**Antworten:** `Y` (neue Version verwenden)

### **5.3 Basis-Tools installieren**

```bash
# Wichtige Entwicklungstools
sudo apt install -y git curl wget nano htop python3-pip

# Versionen prüfen
python3 --version  # Sollte Python 3.11.x zeigen
git --version      # Sollte Git 2.39.x zeigen
pip3 --version     # Sollte pip 23.x zeigen
```

### **5.4 Python IoT-Libraries**

```bash
# BLE und MQTT Libraries für IoT
pip3 install bleak paho-mqtt --break-system-packages
```

**Erfolgreiche Installation:**
```
Successfully installed bleak-1.0.1 paho-mqtt-2.1.0 ...
```

---

## 6. Docker-Installation

### **6.1 Docker installieren (5min)**

```bash
# Offizielles Docker-Installationsskript
curl -fsSL https://get.docker.com -o get-docker.sh

# Docker installieren
sudo sh get-docker.sh
```

**Output (normal):**
```
# Executing docker install script, commit: ...
+ sh -c apt-get update -qq >/dev/null
+ sh -c DEBIAN_FRONTEND=noninteractive apt-get install -y -qq docker-ce...
```

### **6.2 Docker-Berechtigungen konfigurieren**

```bash
# Pi User zur Docker-Gruppe hinzufügen
sudo usermod -aG docker pi

# Docker Compose installieren
sudo apt install -y docker-compose

# System neustarten (für Gruppenmitgliedschaft)
sudo reboot
```

### **6.3 Docker-Test (nach Neustart)**

```bash
# Nach ~2 Minuten neu verbinden
ssh pi@[IP-ADRESSE]

# Docker ohne sudo testen
docker --version        # Docker version 20.10.x
docker-compose --version # docker-compose version 1.29.x

# Test-Container laufen lassen
docker run hello-world
```

**Erfolgreiche Docker-Installation:**
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

---

## 7. Bluetooth-Setup

### **7.1 Bluetooth-Tools installieren**

```bash
# Bluetooth-Pakete installieren
sudo apt install -y bluetooth bluez bluez-tools

# Bluetooth-Service aktivieren
sudo systemctl enable bluetooth
sudo systemctl start bluetooth
```

### **7.2 Bluetooth-Status prüfen**

```bash
# Service-Status anzeigen
sudo systemctl status bluetooth
```

**Erwartete Ausgabe:**
```
● bluetooth.service - Bluetooth service
   Active: active (running)
   Status: "Running"
```

**Warnungen sind normal:**
- `"experimental not enabled"` = erweiterte Features (nicht benötigt)
- `"sap-server: Operation not permitted"` = SIM-Access (nicht benötigt)

### **7.3 Bluetooth-Funktionalität testen**

```bash
# Bluetooth-Controller testen
sudo bluetoothctl
```

**In bluetoothctl:**
```
[bluetooth]# scan on
Discovery started
[CHG] Controller XX:XX:XX:XX:XX:XX Discovering: yes
[NEW] Device 78:77:EA:73:2A:A8 LE-Bose QuietComfort 35
...

[bluetooth]# scan off
Discovery stopped

[bluetooth]# exit
```

✅ **Erfolg:** Geräte werden gefunden (ESP32 wird später erkannt)

---

## 8. Repository-Setup

### **8.1 Repository klonen**

```bash
# Ins Home-Verzeichnis wechseln
cd ~

# Smart Plant Monitor Repository klonen
git clone https://github.com/joha1na/smart-plant-monitor.git

# Ins Repository wechseln
cd smart-plant-monitor

# Struktur anzeigen
ls -la
```

**Erwartete Struktur:**
```
drwxr-xr-x docs/
drwxr-xr-x .git/
-rw-r--r-- .gitignore
-rw-r--r-- README.md
```

### **8.2 Git-Konfiguration (optional)**

```bash
# Git-User konfigurieren (für Commits vom Pi)
git config --global user.name "Ihr Name"
git config --global user.email "ihre.email@example.com"
```

---

## 9. Troubleshooting

### **Häufige Probleme & Lösungen**

#### **Problem: Pi erscheint nicht im Netzwerk**
**Lösung:**
1. Router-Interface prüfen (zuverlässigster Weg)
2. WiFi-Konfiguration manuell erstellen (siehe Schritt 3.2)
3. Ethernet-Kabel als Backup verwenden
4. 5-10 Minuten warten (Pi kann langsam sein)

#### **Problem: SSH Connection refused**
**Lösung:**
1. Pi vollständig booten lassen (grüne LED aus)
2. SSH-Datei auf boot-Partition prüfen: `touch ssh`
3. IP-Adresse nochmal bestätigen
4. Pi neustarten

#### **Problem: Docker Permission denied**
**Lösung:**
1. `sudo usermod -aG docker pi`
2. `sudo reboot`
3. Nach Neustart: `docker run hello-world` (ohne sudo)

#### **Problem: Bluetooth nicht gefunden**
**Lösung:**
1. `sudo systemctl restart bluetooth`
2. `sudo bluetoothctl scan on`
3. USB-Geräte können interferieren - entfernen

#### **Problem: nmap Segmentation Fault (macOS)**
**Lösung:**
1. Router-Interface verwenden (empfohlen)
2. `arp -a | grep 192.168.x` verwenden  
3. `brew uninstall nmap && brew install nmap`

### **Ordentliches Herunterfahren**

```bash
# Niemals einfach Strom ziehen!
sudo shutdown -h now

# Warten bis grüne LED aus ist
# Dann sicher Strom trennen
```

### **Neustart**

```bash
# System neustarten
sudo reboot

# Nach 2-3 Minuten neu verbinden
ssh pi@[IP-ADRESSE]
```

---

## 10. Erfolgskriterien

### ✅ **Setup erfolgreich wenn:**

- [ ] SSH-Verbindung funktioniert ohne Probleme
- [ ] `docker run hello-world` läuft ohne sudo
- [ ] `sudo bluetoothctl scan on` findet Geräte
- [ ] Repository ist geklont und zugänglich
- [ ] Python IoT-Libraries sind installiert

### 🎯 **Bereit für Sprint 2:**

- ESP32 BLE-Kommunikation
- Docker-Container Deployment
- MQTT-Services

---

**Setup-Zeit:** ~45-90 Minuten (je nach Erfahrung)  
**Nächster Schritt:** ESP32 MicroPython Setup  
**Viel Erfolg!** 🍓🚀

# Sprint-Tracking-Guide
## Smart-Plant-Monitor - Projekt-Tracking

**Zweck:** Tägliche Fortschrittsverfolgung und Lessons-Learned-Dokumentation

---

## 📋 Sprint-Tracking-Workflow

### **Tagesbeginn (15min):**
1. Kopiere das Template: `cp sprint-tracking-template.md sprint-X-YYYY-MM-DD.md`
2. Sprint-Goal aus dem [Projektplan](../project-plan.md) übernehmen
3. Tasks aus dem Projektplan in "🔄 Planned" eintragen
4. Realistische Zeitschätzung für den Tag machen

### **Während der Arbeit (5min alle 2h):**
- ✅ Abgeschlossene Tasks nach "Completed" verschieben
- 📝 Tatsächlich benötigte Zeit notieren
- 🚨 Probleme sofort in "Notes" dokumentieren
- ⚠️ Blocker identifizieren und Lösungsansätze notieren

### **Tagesende (15min):**
- 📊 Alle Tasks kategorisieren
- 📚 Lessons Learned dokumentieren
- 📅 Nächsten Tag planen
- 🔄 Template für nächsten Sprint vorbereiten

Siehe [Vorlage für Sprint-Tracking](sprint-tracking-template.md)

---

## 📁 Datei-Naming-Convention

sprint-{NUMMER}-{YYYY-MM-DD}.md

Beispiele:

- sprint-1-2025-07-25.md
- sprint-2-2025-07-26.md
- sprint-3-2025-07-27.md

---

## 📊 Sprint-Übersicht

| Sprint | Datum | Ziel | Status | Zeit | Completed |
|--------|-------|------|--------|------|-----------|
| 1 | 2025-07-25 | Foundation & Setup | 🔄 | 0/6h | 0/7 |
| 2 | 2025-07-28 | BLE Communication | ⏳ | 0/6h | 0/6 |
| 3 | 2025-07-29 | Sensor Integration | ⏳ | 0/6h | 0/6 |
| 4 | 2025-07-30 | Cloud Pipeline & Dashboards | ⏳ | 0/6h | 0/6 |
| 5 | 2025-07-31 | Stabilization & Documentation | ⏳ | 0/6h | 0/6 |
| 6 | 2025-08-01 | Nice-to-Haves (Security, ESP32-Cam) | ⏳ | 0/6h | 0/6 |

**Legende:**
- 🔄 In Progress
- ✅ Completed  
- ⏳ Planned
- ❌ Blocked

---

## 📈 Wöchentliches Review

Ende der Woche (30min):

1. Alle Sprint-Files durchgehen
2. Zeitschätzungen vs. Realität analysieren
3. Wiederkehrende Probleme identifizieren
4. Projektplan bei Bedarf anpassen
5. Lessons Learned zusammenfassen

Siehe [Vorlage für Project-Review](review-template.md)

---

## 🔧 Hilfreiche Git Commands

```bash
# Sprint-Tracking committen
git add docs/sprints/
git commit -m "Sprint X: Daily tracking update"

# Alle Sprint-Files anzeigen
ls docs/sprints/

# Letztes Sprint-File anzeigen
cat docs/sprints/sprint-$(date +%Y-%m-%d).md
```
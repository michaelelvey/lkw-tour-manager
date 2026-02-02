# 🚛 LKW Tour Manager - Vollständige Dokumentation

## Übersicht

Der **LKW Tour Manager** ist eine Progressive Web App (PWA) speziell entwickelt für Seitenlader-LKW-Fahrer im Bereich kommunale Müllentsorgung. Die App ermöglicht GPS-basierte Tourenaufzeichnung und -navigation mit spezifischen Funktionen für die Müllabfuhr.

---

## ✨ Hauptfunktionen

### 1️⃣ Tour Aufzeichnung (Recording Mode)

#### Tour-Setup
- **Tour-Name**: Freie Benennung (z.B. "Bezirk Nord", "Industriegebiet Ost")
- **Tour-Typ**: 
  - Ungerade Woche
  - Gerade Woche

#### Während der Aufzeichnung
**Pflicht-Aktionen:**
- 🟢 **Touranfang** - Startet die GPS-Aufzeichnung
- 🔴 **Tourende** - Beendet und speichert die Tour

**Tonnen-Position** (eine muss immer aktiv sein):
- 🟦 **Rechts** - Tonnen stehen rechts (Standard für Seitenlader)
- 🟥 **Links** - Tonnen stehen links (Wenden erforderlich)
- 🟪 **Beide Seiten** - Tonnen beidseitig
- ⚪ **Keine Tonnen** - Durchfahrt ohne Tonnen

**Fahrmanöver** (punktgenau markiert):
- ↩️ **Links abbiegen**
- ↪️ **Rechts abbiegen**
- 🔄 **Hier wenden**
- ⬅️ **Rückwärts Fahrt**
- ➡️ **Ende Rückwärts Fahrt**

**Fehlerkorrektur:**
- ↶ **Letzte Aktion rückgängig** - Entfernt die zuletzt gesetzte Aktion

#### Was wird automatisch gespeichert?
1. **GPS-Trackliste** - Jeder Punkt mit Zeitstempel
2. **Segmente** - Streckenabschnitte mit Tonnenposition
3. **Events** - Alle Manöver mit exakter Position
4. **Metadaten** - Name, Typ, Datum, Dauer

---

### 2️⃣ Tour Navigation (Navigation Mode)

#### Tour-Start
1. Gespeicherte Tour aus Liste auswählen
2. Optional: Navigation zum Touranfang
3. Tour wird auf Karte angezeigt

#### Während der Fahrt

**Visuelle Darstellung:**
- **Blaue durchgezogene Linie** - Nächste 250m
- **Blaue gestrichelte Linie** - Weitere Strecke
- **Graue Linie** - Bereits gefahrene Strecke
- **Farbige Segmente**:
  - Blau = Tonnen rechts
  - Rot = Tonnen links
  - Lila = Tonnen beidseitig
  - Grau = Keine Tonnen

**Akustische Hinweise:**
- Automatische Sprachausgabe bei:
  - Kommenden Abbiegungen (30m vorher)
  - Wende- und Rückwärtspunkten
  - Änderung der Tonnenlage
  - Abweichung von der Route

**Optische Warnungen:**
- Große Symbole für kommende Manöver
- Farbcodierung nach Dringlichkeit
- Routenabweichungs-Alarm

---

## 🔧 Technische Details

### Verwendete Technologien
- **Frontend**: HTML5 + CSS3 + Vanilla JavaScript
- **Karten**: Leaflet.js (OpenStreetMap)
- **GPS**: HTML5 Geolocation API
- **Speicher**: LocalStorage (offline-fähig)
- **Audio**: Web Speech API (Text-to-Speech)
- **Design**: Responsive, Touch-optimiert

### Browser-Kompatibilität
✅ Chrome/Edge (Android/Desktop)  
✅ Safari (iOS/iPad)  
✅ Firefox (Android/Desktop)  
⚠️ Mindestanforderung: GPS-fähiges Gerät

### Datenstruktur

```javascript
// Tour Object
{
  id: 1706789123456,
  name: "Bezirk Nord",
  type: "ungerade",
  created: "2026-02-01T10:30:00Z",
  segments: [
    {
      tonPosition: "right",
      points: [
        [52.5200, 13.4050],
        [52.5201, 13.4051],
        ...
      ]
    }
  ],
  events: [
    {
      type: "turn_left",
      position: [52.5205, 13.4055],
      timestamp: "2026-02-01T10:35:00Z"
    }
  ]
}
```

---

## 📱 Installation & Nutzung

### Schritt 1: Datei auf Gerät laden
1. **Auf Computer:**
   - Datei `lkw-tour-manager.html` herunterladen
   
2. **Auf Handy/Tablet übertragen:**
   - Per E-Mail an dich selbst senden
   - Via Cloud-Dienst (Google Drive, Dropbox)
   - Via USB-Kabel auf Gerät kopieren

### Schritt 2: Im Browser öffnen
1. Datei-Manager öffnen
2. `lkw-tour-manager.html` antippen
3. "Mit Chrome öffnen" wählen (empfohlen)

### Schritt 3: Als App installieren (Optional)
**Android Chrome:**
1. Im Browser: Menü → "Zum Startbildschirm hinzufügen"
2. App erscheint auf dem Home-Screen
3. Startet wie normale App (ohne Browser-Leiste)

**iOS Safari:**
1. Teilen-Button → "Zum Home-Bildschirm"
2. App wird zum Home-Screen hinzugefügt

### Schritt 4: GPS-Berechtigung erteilen
- Beim ersten Start: "Standort erlauben" → **Immer erlauben**
- Bei Problemen: Geräteeinstellungen → Apps → Berechtigungen

---

## 🎯 Praktische Anwendung

### Beispiel: Erste Tour aufzeichnen

1. **App starten** → "Neue Tour aufzeichnen"

2. **Tour-Daten eingeben:**
   - Name: "Innenstadt Ost"
   - Typ: "Ungerade Woche"
   - → "Tour starten"

3. **Am Startpunkt:**
   - Warten bis GPS grün ist (< 10m Genauigkeit)
   - 🟢 **Touranfang** drücken

4. **Während der Fahrt:**
   - Losfahren
   - 🟦 **Rechts** drücken (Tonnen stehen rechts)
   - Bei Straßenecke: ↪️ **Rechts abbiegen** drücken
   - Weiterfahren...
   - Wenn Tonnen links stehen: 🟥 **Links** drücken
   - Bei Wendepunkt: 🔄 **Wenden** drücken

5. **Am Endpunkt:**
   - 🔴 **Tourende** drücken
   - Tour wird automatisch gespeichert

### Beispiel: Tour abfahren

1. **App starten** → "Tour abfahren"

2. **Tour wählen:** "Innenstadt Ost" antippen

3. **Navigation starten:**
   - "Zum Touranfang navigieren?" → Ja/Nein
   - Route wird auf Karte angezeigt

4. **Während der Fahrt:**
   - Blauer Linie folgen
   - Akustische Ansagen beachten
   - Bei Abweichung: Warnung erscheint

---

## 🛠️ Problemlösung

### GPS findet keine Position
**Lösung:**
- Draußen im Freien testen (Gebäude blockieren Signal)
- Flugmodus aus/ein schalten
- Gerät neu starten
- GPS in Systemeinstellungen aktivieren

### Karte lädt nicht
**Lösung:**
- Internetverbindung prüfen (beim ersten Laden)
- Seite neu laden (F5 / Refresh)
- Cache leeren

### Ton funktioniert nicht
**Lösung:**
- Lautstärke erhöhen
- Nicht-Stören-Modus prüfen
- Browser-Berechtigungen für Audio prüfen

### Tour wurde nicht gespeichert
**Lösung:**
- Immer 🔴 **Tourende** drücken!
- Private-Modus deaktivieren (löscht LocalStorage)
- Ausreichend Speicherplatz auf Gerät

### App ist langsam/hängt
**Lösung:**
- Andere Apps schließen
- Browser-Cache leeren
- Gerät neu starten
- Alte Touren löschen (LocalStorage voll)

---

## 🔐 Datenschutz & Sicherheit

### Wo werden Daten gespeichert?
- **Lokal auf dem Gerät** (LocalStorage)
- **NICHT in der Cloud**
- **KEIN Server-Upload**

### Was passiert bei Geräteverlust?
- Daten gehen verloren (kein Backup)
- **Empfehlung**: Regelmäßig exportieren (Feature in v2.0)

### GPS-Tracking
- Nur während App-Nutzung aktiv
- Keine Hintergrund-Verfolgung
- Kann jederzeit deaktiviert werden

---

## 🚀 Geplante Erweiterungen (Version 2.0)

### In Entwicklung:
- ☁️ **Cloud-Backup** - Tour-Synchronisation
- 📤 **Export-Funktion** - GPX/KML-Export
- 🗺️ **Offline-Karten** - Keine Internet-Verbindung nötig
- 📊 **Statistiken** - Gefahrene km, Tonnenzahl, Zeitanalyse
- 🔄 **Tour-Optimierung** - Automatische Routenverbesserung
- 👥 **Multi-User** - Touren im Team teilen
- 🎨 **Manuelle Editor** - Nachträgliche Streckenbearbeitung
- 🔔 **Push-Benachrichtigungen** - Erinnerungen, Updates

### Gewünscht?
Feedback gerne per:
- E-Mail: [deine-email@beispiel.de]
- Feedback-Button in der App

---

## 📋 FAQ

**Q: Funktioniert die App offline?**  
A: Teilweise. GPS und gespeicherte Touren funktionieren offline. Kartenladen benötigt Internet (beim ersten Mal).

**Q: Wie viele Touren kann ich speichern?**  
A: Unbegrenzt, solange Gerätespeicher verfügbar ist. Empfohlen: Max. 50 Touren.

**Q: Kann ich Touren löschen?**  
A: Aktuell nur über Browser-Entwicklertools (LocalStorage). Lösch-Funktion kommt in v2.0.

**Q: Läuft die App im Hintergrund?**  
A: Nein. GPS-Tracking stoppt, wenn App geschlossen wird.

**Q: Wie genau ist das GPS?**  
A: Typisch 5-15m. Bei gutem Signal <10m. Status wird oben angezeigt.

**Q: Verbraucht die App viel Akku?**  
A: Mittel. GPS ist akkuintensiv. Empfehlung: Powerbank/Auto-Ladekabel.

**Q: Kann ich Touren exportieren?**  
A: Noch nicht. Kommt in v2.0 als GPX/KML-Export.

**Q: Brauche ich einen Account?**  
A: Nein! Alles läuft lokal auf deinem Gerät.

---

## 💡 Best Practices

### Vor der Fahrt
✅ GPS-Genauigkeit prüfen (sollte grün sein)  
✅ Akku-Stand checken (min. 50%)  
✅ Bildschirm-Helligkeit erhöhen (Sonnenlicht)  
✅ Gerätehalterung sicher befestigen  

### Während der Aufzeichnung
✅ Beim Losfahren Tonnenposition direkt setzen  
✅ Manöver BEVOR du sie machst drücken (nicht nachträglich)  
✅ Bei Fehlern sofort "Rückgängig" nutzen  
✅ Regelmäßig GPS-Status checken  

### Während der Navigation
✅ Lautstärke auf 70-80% stellen  
✅ Nicht nur auf Karte verlassen (Verkehr beachten!)  
✅ Bei Abweichung: Sicher anhalten, neu orientieren  

### Nach der Tour
✅ Immer "Tourende" drücken (sonst nicht gespeichert!)  
✅ Tour direkt überprüfen (in Tour-Liste)  
✅ Bei Fehlern: Tour nochmal fahren  

---

## 📞 Support

### Technische Probleme
1. Diese Dokumentation durchlesen
2. FAQ checken
3. Browser-Konsole öffnen (F12) → Fehlermeldungen screenshoten
4. Gerätedaten sammeln:
   - Gerätemodell
   - Betriebssystem-Version
   - Browser + Version

### Feature-Wünsche
Gerne! Schreib mir:
- Was genau brauchst du?
- In welcher Situation?
- Wie dringend?

---

## 📄 Lizenz & Credits

**Entwickelt für:** LKW-Fahrer in der kommunalen Müllentsorgung  
**Version:** 1.0.0  
**Datum:** Februar 2026  
**Lizenz:** Freie Nutzung (keine kommerzielle Weitergabe)

**Verwendete Open-Source-Bibliotheken:**
- Leaflet.js (BSD-2-Clause)
- OpenStreetMap (ODbL)

---

## 🎓 Schulungs-Checkliste

Vor dem ersten Einsatz:
- [ ] App installiert
- [ ] GPS-Berechtigung erteilt
- [ ] Test-Tour aufgezeichnet (Parkplatz)
- [ ] Test-Tour abgefahren
- [ ] Akustische Hinweise getestet
- [ ] Alle Buttons ausprobiert
- [ ] Dokumentation gelesen

**Bereit für den Einsatz! 🚛💪**

---

## Changelog

### Version 1.0.0 (Feb 2026)
- ✨ Initiale Veröffentlichung
- ✅ GPS-Tracking
- ✅ Tonnen-Positionierung
- ✅ Manöver-Events
- ✅ Tour-Navigation
- ✅ Sprachausgabe
- ✅ Offline-Speicherung

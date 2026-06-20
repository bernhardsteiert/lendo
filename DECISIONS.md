# Lendo – Architektur-Entscheidungen

## Technologie-Stack

| Entscheidung | Gewählt | Verworfen | Begründung |
|---|---|---|---|
| App-Typ | PWA (Single HTML-Datei) | React Native, Expo | Kein App Store nötig, einfache Verteilung |
| Hosting | GitHub Pages | Netlify (Credits aufgebraucht), wint.global | Kostenlos, kein Limit, einfaches Upload |
| Datenbank | Firebase Realtime Database | Supabase, lokale Lösung | Kostenlos, Echtzeit-Sync, einfache REST API |
| Firebase Region | europe-west1 (Frankfurt) | US-Server | Datenschutz |
| Sync-Methode | Polling alle 5 Sekunden | WebSockets, SSE | Einfachheit, Firebase REST reicht |
| Authentifizierung | Gruppen-Code (kein Login) | E-Mail-Accounts | Einfachheit, Familiennutzung |
| Framework | Vanilla JS + CSS | React, Vue | Keine Build-Pipeline nötig, eine Datei |
| Icon-Format | Externe PNG-Dateien | Base64 in HTML | Android erkennt Base64 nicht im manifest |

## Firebase Konfiguration
- **URL:** `https://verliehen-44d47-default-rtdb.europe-west1.firebasedatabase.app`
- **Modus:** Testmodus (offen, kein Auth)
- **Datenpfad:** `rooms/{gruppenCode}/items/{itemId}`
- **Sicherheit:** Nur wer den Gruppen-Code kennt, kann Daten lesen

## Design-Entscheidungen
- **Design-Sprache:** Natives iOS (SF Pro / -apple-system, #f2f2f7 Hintergrund, 0.5px Separator)
- **Karten:** Abgerundet (12px), mit Rand (16px), kein Bold, 19px Schrift
- **Karten-Liste:** Nur Gegenstandsname + Toggle + Chevron – Details nur in Detailansicht
- **Toggle statt Haken:** iOS-Style Toggle Switch (grau = offen, grün = zurückbekommen)
- **Überfällig:** Rötliche Schrift + rotes Ausrufezeichen-SVG, kein Text-Badge
- **Zurück:** Leicht grüner Hintergrund, grauer Text
- **Animationen:** Crossfade (opacity 0.22s) zwischen Screens – keine Slide-Animation (technisch zu aufwändig als PWA)
- **Suchleiste:** Scrollt mit der Liste (nicht sticky)
- **Filter:** Bottom-Sheet mit Status + Sortierung

## Offline-Strategie
- **Service Worker:** `sw.js` cached App-Assets, Network-first für HTML
- **Lokaler Cache:** Letzter Firebase-Stand in `localStorage` unter `lendo_cache_{gruppenCode}`
- **Ausstehende Änderungen:** Offline-Änderungen in `localStorage` unter `lendo_pending`
- **Auto-Sync:** Beim Reconnect werden pending changes zu Firebase hochgeladen
- **Offline-Indikator:** Im Nav-Header, oranges WLAN-Symbol + i-Button

## Verworfene Ideen
- Tab-Bar unten (zu viele Probleme mit safe-area-inset-bottom)
- Collapsing Large Title (deaktiviert, zu instabil)
- Slide-Animationen (zu aufwändig ohne Framework)
- Push-Notifications (nicht möglich in PWA ohne Backend)
- Foto des Gegenstands (nicht implementiert)

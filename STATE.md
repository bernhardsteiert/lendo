# Lendo – Aktueller Stand

## Version
**3.5** (aktuelle deployed Version)

Die Versionsnummer ist zentral als `APP_VERSION` Konstante im Script gespeichert.
Wird automatisch auf Splash-Screen und in Einstellungen angezeigt.

## Deployment
- **GitHub Repo:** https://github.com/bernhardsteiert/lendo
- **Live URL:** https://bernhardsteiert.github.io/lendo/
- **Upload:** https://github.com/bernhardsteiert/lendo/upload/main
- **Hosting:** GitHub Pages (Branch: main)

## Dateien im Repo
| Datei | Zweck |
|---|---|
| `index.html` | Komplette App (HTML + CSS + JS in einer Datei) |
| `manifest.json` | PWA Manifest (Icons, Display, Orientation) |
| `sw.js` | Service Worker (Offline-Cache, Network-first für HTML) |
| `icon.png` | iOS Homescreen Icon (180x180) |
| `icon-192.png` | Android Icon (192x192) |
| `icon-512.png` | Android Splash Icon (512x512) |

## Firebase
- **Projekt:** verliehen-44d47
- **URL:** https://verliehen-44d47-default-rtdb.europe-west1.firebasedatabase.app
- **Aktueller Gruppen-Code (Bernhard & Frau):** bernyalex

## Implementierte Features
- [x] Eintrag erstellen (Gegenstand, Verliehen an, von, Datum, Rückgabe bis)
- [x] Eintrag bearbeiten
- [x] Eintrag löschen (nur in Detailansicht)
- [x] Toggle zurückbekommen (direkt auf Karte, mit Animation)
- [x] Toggle rückgängig machen (nochmal tippen)
- [x] Echtzeit-Sync via Firebase Polling (5 Sekunden)
- [x] Gruppen-Code für gemeinsame Liste
- [x] Gruppen-Code wird lokal gespeichert (kein erneutes Eingeben)
- [x] Offline-Modus (lokaler Cache + pending changes)
- [x] Offline-Indikator im Header
- [x] Suche (Gegenstand, Person, Verleiher)
- [x] Filter Bottom-Sheet (Status: Alle/Offen/Zurück/Überfällig, Sortierung)
- [x] Detailansicht mit allen Infos
- [x] Überfällig-Banner oben
- [x] Personen-Vorschläge beim Eingeben
- [x] Pflichtfelder markiert mit rotem *
- [x] iOS-Design (SF Pro, native Farben, Segmente, Gruppen)
- [x] PWA (Homescreen-fähig iOS + Android)
- [x] Service Worker (Offline-fähig)
- [x] Crossfade-Animation zwischen Screens
- [x] Einstellungen (Gruppen-Code ändern, App teilen, GitHub-Link, Credits)
- [x] App teilen via Navigator.share (iOS Share Sheet)
- [x] Versionsnummer zentral (APP_VERSION Konstante)
- [x] Rotationssperre (portrait via manifest + screen.orientation.lock)

## Bekannte Einschränkungen / Offene Punkte
- Slide-Animation (links/rechts) nicht implementiert – technisch zu aufwändig als PWA ohne Framework
- Rotationssperre funktioniert nur wenn als PWA installiert, nicht im Browser
- Firebase im Testmodus (kein Auth) – Gruppen-Code ist kein echter Schutz
- Service Worker auf iOS manchmal verzögert beim Update

## Aktuelle App-Texte
- **App-Name:** Lendo
- **Splash-Subtitle:** „Gemeinsam verleihen mit Überblick"
- **Hint:** „Gebt denselben Code auf mehreren Geräten ein, um eure Liste zu teilen."
- **Gruppen-Code** (statt Raum-Code)
- **Credits:** Bernhard Steiert & Claude

## JavaScript Variablen (global)
```js
const APP_VERSION = "3.5";
const FB = "https://verliehen-44d47-default-rtdb.europe-west1.firebasedatabase.app";
let roomCode = "";       // aktueller Gruppen-Code
let items = {};          // alle Items aus Firebase
let filter = "offen";   // aktueller Filter
let filterStatus = 'alle';
let filterSort = 'datum';
let pollTimer = null;    // Polling-Interval
let searchQ = "";        // Suchbegriff
let editingId = null;    // ID beim Bearbeiten
let currentDetailId = null;
let listEventsInited = false;
let pendingChanges = {}; // Offline-Änderungen
```

## localStorage Keys
| Key | Inhalt |
|---|---|
| `lendo_group` | Gespeicherter Gruppen-Code |
| `lendo_cache_{gruppenCode}` | Letzter Firebase-Stand als JSON |
| `lendo_pending` | Ausstehende Offline-Änderungen als JSON |

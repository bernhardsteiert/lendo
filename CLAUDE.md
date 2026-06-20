# Lendo – Anleitung für Claude Code

## Projekt-Überblick
Lendo ist eine PWA (Progressive Web App) – **eine einzige HTML-Datei** plus Assets.
Alles (HTML, CSS, JS) ist in `index.html`. Kein Build-Prozess, kein Framework.

## Wichtige Regeln

### Versionierung
- Versionsnummer ist **zentral** als `APP_VERSION = "x.x"` Konstante am Anfang des Scripts
- **Immer** nach jeder Änderung die Version erhöhen
- Wird automatisch auf Splash-Screen (`#version-splash`) und Settings (`#version-settings`) angezeigt
- Nach jeder neuen `index.html` auch immer `index.html` als Kopie bereitstellen

### Deployment
- Nach jeder Änderung: neue `index.html` hochladen auf:
  https://github.com/bernhardsteiert/lendo/upload/main
- Live-URL: https://bernhardsteiert.github.io/lendo/
- **Immer beide Links** am Ende jeder Antwort nennen

### Code-Stil
- Vanilla JS, kein Framework
- CSS in `<style>` Tag im `<head>`
- JS am Ende des `<body>` (nach allen HTML-Elementen)
- Alle Screens haben `display:none` im CSS (`#screen-name { display: none; }`)
- Screens werden per `show(id)` ein/ausgeblendet
- Screen-Transitions via `transitionTo(fromId, toId, direction)` – Crossfade

### Firebase
- URL: `https://verliehen-44d47-default-rtdb.europe-west1.firebasedatabase.app`
- Pfad: `rooms/{gruppenCode}/items/{itemId}`
- Offline-fähig via `fbSetSafe()` und `fbDelSafe()` statt direktem `fbSet()`/`fbDel()`

### localStorage Keys
- `lendo_group` – Gespeicherter Gruppen-Code
- `lendo_cache_{gruppenCode}` – Letzter Firebase-Stand
- `lendo_pending` – Ausstehende Offline-Änderungen

### iOS Design
- Hintergrund: `#f2f2f7`
- Separator: `rgba(60,60,67,0.12)`
- Akzent: `#007aff`
- Grün: `#34c759`, Rot: `#ff3b30`
- Schrift: `-apple-system, "SF Pro Text", "Helvetica Neue", sans-serif`
- Karten: border-radius 12px, padding 12px 16px, margin 8px 16px

### Vor jeder Änderung
1. Aktuelle Datei lesen
2. Gezielt ändern (Python-Skript oder str_replace)
3. JS Syntax prüfen: `node --check /tmp/check_js.js`
4. Version erhöhen
5. `index.html` kopieren
6. Beide Links nennen

### Häufige Fehler vermeiden
- Niemals `const list` oder andere Variablen doppelt in derselben Funktion deklarieren
- Script-Tag muss **nach** allen HTML-Elementen stehen (am Ende von `<body>`)
- Alle Screens brauchen `display:none` im CSS, nicht als inline style
- `fbSetSafe()`/`fbDelSafe()` nutzen, nicht `fbSet()`/`fbDel()` direkt

## Datei-Struktur im Repo
```
index.html      ← Komplette App
manifest.json   ← PWA Manifest
sw.js           ← Service Worker
icon.png        ← iOS Icon (180x180, weißer Hintergrund)
icon-192.png    ← Android Icon (192x192)
icon-512.png    ← Android Splash (512x512)
```

## Screen-Struktur
```
#join-screen    → Gruppen-Code eingeben
#main-screen    → Hauptliste (mit #main-scroll, #main-nav)
#detail-screen  → Detailansicht eines Eintrags
#add-screen     → Formular (neu + bearbeiten)
#settings-screen → Einstellungen
#filter-sheet   → Bottom-Sheet für Filter (position:fixed)
#offline-sheet  → Bottom-Sheet für Offline-Info (position:fixed)
```

## Globale JS-Variablen
```js
const APP_VERSION   // Versionsnummer – zentral!
const FB            // Firebase URL
let roomCode        // Aktueller Gruppen-Code
let items           // Alle Items { id: item }
let filter          // "offen" | "alle" | "zurueck"
let filterStatus    // "alle" | "offen" | "zurueck" | "ueberfaellig"
let filterSort      // "datum" | "rueckgabe" | "person" | "verleiher" | "gegenstand"
let pollTimer       // setInterval für Firebase-Polling
let searchQ         // Aktueller Suchbegriff
let editingId       // ID beim Bearbeiten (null = neu)
let currentDetailId // ID in Detailansicht
let listEventsInited // Event-Delegation nur einmal setzen
let pendingChanges  // Offline-Änderungen { path: data }
```

# Lendo 📦

**Gemeinsam verleihen mit Überblick**

Eine PWA für Familien und Freundesgruppen um verliehene Gegenstände im Überblick zu behalten. Entwickelt von Bernhard Steiert mit Claude (Anthropic).

🔗 **[App öffnen](https://bernhardsteiert.github.io/lendo/)**

---

## Features

- 📋 Verliehene Gegenstände tracken (Gegenstand, Person, Datum, Rückgabefrist)
- 🔄 Echtzeit-Sync zwischen mehreren Geräten via Gruppen-Code
- ✅ Toggle zum Abhaken wenn etwas zurückgekommen ist
- ⚠️ Überfällige Einträge werden rot markiert
- 🔍 Suche und Filter (Status, Sortierung)
- 📵 Offline-fähig mit lokalem Cache und Auto-Sync
- 📱 Als App installierbar auf iOS und Android (PWA)

## Installation auf dem Homescreen

**iPhone:** Link in Safari öffnen → Teilen → „Zum Home-Bildschirm"

**Android:** Link in Chrome öffnen → Drei Punkte → „Zum Startbildschirm hinzufügen"

## Technologie

| | |
|---|---|
| Frontend | Vanilla HTML/CSS/JS (eine Datei) |
| Datenbank | Firebase Realtime Database |
| Hosting | GitHub Pages |
| Offline | Service Worker + localStorage |

## Entwicklung

Entwickelt iterativ in einer Claude-Konversation (claude.ai).
Für Claude Code: siehe [`CLAUDE.md`](CLAUDE.md) für Kontext und Regeln.

## Lizenz

Privates Projekt – kein öffentliches Lizenzmodell.

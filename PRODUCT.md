# Lendo – Produktvision & Anforderungen

## Was ist Lendo?
Eine PWA für Familien und Freundesgruppen um verliehene Gegenstände im Überblick zu behalten.
Entwickelt von Bernhard Steiert mit Claude (Anthropic).

## Kern-Idee
Man verleiht Bücher, Werkzeug, Gegenstände – und vergisst nach Monaten wem.
Lendo löst das mit einer gemeinsamen, synchronisierten Liste.

## Nutzer
- Primär: Bernhard Steiert und seine Frau (Gruppen-Code: bernyalex)
- Sekundär: Freunde und Familie die eingeladen werden
- Plattform: iPhone (primär), Android (sekundär)

## Kern-Flows

### Neuen Eintrag erstellen
1. + Button oben rechts
2. Gegenstand (Pflicht), Verliehen an (Pflicht, mit Vorschlägen), Verliehen von (Pflicht, mit Vorschlägen)
3. Verliehen am (Pflicht), Rückgabe bis (optional)
4. „Fertig" → speichert zu Firebase

### Eintrag abhaken
- Toggle auf der Karte tippen → grün = zurückbekommen
- Nochmal tippen → wieder grau = offen

### Detailansicht
- Auf Karte tippen → Detailansicht mit allen Infos
- „Bearbeiten" oben rechts → Formular
- Zurückbekommen / Löschen als Buttons

### Sync
- Automatisch alle 5 Sekunden
- Sofort bei eigenen Änderungen
- Offline: lokaler Cache, Sync beim Reconnect

## Design-Prinzipien
- **Natives iOS-Feeling:** SF Pro, 19px normal weight, #f2f2f7 Hintergrund
- **Karten:** Nur Gegenstandsname sichtbar, Details auf Tippen
- **Überfällig:** Rötliche Schrift + Ausrufezeichen-Icon
- **Zurück:** Leicht grüner Hintergrund, grauer Text
- **Keine Ablenkung:** Kein Bold, keine bunten Badges in der Liste

## App-Struktur (Screens)
1. **Join-Screen** – Gruppen-Code eingeben (nur beim ersten Start)
2. **Main-Screen** – Liste aller Einträge, Suche, Filter, Offline-Indikator
3. **Detail-Screen** – Alle Infos eines Eintrags, Aktionen
4. **Add/Edit-Screen** – Formular für neuen/bestehenden Eintrag
5. **Settings-Screen** – Gruppen-Code, App teilen, GitHub, Credits, Version

## Nicht implementiert (bewusste Entscheidungen)
- Fotos von Gegenständen
- Push-Notifications (technisch nicht möglich ohne Backend)
- Echte Authentifizierung (Gruppen-Code reicht für Familiennutzung)
- Kategorien
- Mehrere Listen pro Gerät

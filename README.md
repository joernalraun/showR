# showR

Animierte Präsentationen aus einer Markdown-Datei.

```bash
npm install
npm run dev      # http://localhost:5173 – Änderungen an slides.md erscheinen sofort
npm run build    # statische Version in dist/
```

## Folien schreiben (`slides.md`)

```md
layout: split          ← optionale Kopfzeilen
bg: sunset
transition: zoom

## Überschrift

- Punkt eins
- Punkt zwei
{.steps}               ← Punkte erscheinen per Klick

![Beschreibung](media/clip.mp4)

???
Sprechernotizen (Taste N)

---                    ← nächste Folie
```

| Schlüssel    | Werte |
|--------------|-------|
| `layout`     | `default`, `hero`, `center`, `split`, `split-left`, `media`, `grid`, `quote` |
| `bg`         | `aurora`, `sunset`, `ocean`, `forest`, `candy`, `ember`, `mono` oder drei Farben `#112233 #445566 #778899` |
| `transition` | `morph` (Standard), `slide`, `zoom`, `flip`, `blur` |
| `background` | Bild oder Video, füllt das ganze Fenster und läuft im Loop (stumm, außer `sound: on`) |
| `class`      | eigene CSS-Klassen |
| `shade`      | `light` legt einen weißen Verlauf über den `background` und schaltet auf dunkle Schrift (Standard: dunkler Schatten) |
| `sound`      | `off` schaltet alle Videos der Folie stumm, `on` aktiviert auch den Ton von Hintergrundvideos |

**Magic Morph:** Gleiche Überschriften, gleiche Medien oder gleiche IDs (`# Titel {#logo}`) gleiten automatisch von Folie zu Folie.

**Extras:** `<div class="big count">12.480</div>` zählt hoch (Größen: `small` 40 px, `medium` 100 px, `big` 220 px), `<p class="kicker">` für Überzeilen, `{.step}` an beliebigen Absätzen.

## Medien

Dateien in `public/media/` legen und wie Bilder einbinden: `![Alt](media/datei.ext)`.

- **Bilder:** PNG, JPG, GIF (animiert), WebP, AVIF, SVG
- **Videos:** MP4 (H.264), WebM (VP8/VP9/AV1), OGV; MOV nur, wenn H.264-kodiert
- Videos laufen in Schleife mit Ton, sobald die Folie aktiv ist (Hintergrundvideos stumm). Stummschalten pro Folie mit `sound: off`, pro Video mit `{.mute}`. Weitere Optionen: `{.sound}` erzwingt Ton, `{.controls}` mit Bedienleiste, `{.once}` ohne Schleife, `{.contain}` ohne Beschnitt, `{.flat}` ohne Rahmen/Schatten
- `{.inline}` an einem Bild oder Video hält es im Textbereich, mittig und ohne Rahmen (300 px hoch). So lässt sich z. B. bei `layout: media` ein Logo über dem Text platzieren. Höhe anpassen: `{.inline style="height:200px"}`

## Tasten

→ / Leertaste weiter · ← zurück · O Übersicht · F Vollbild · N Notizen · ? Hilfe · Wischen auf Touch-Geräten

Hinweis: Browser erlauben Ton erst nach der ersten Interaktion (Taste/Klick). Startet die Präsentation direkt auf einer Video-Folie, läuft das Video zunächst stumm.

## Mehrere Präsentationen

`slides.md` ist die Hauptpräsentation (`http://localhost:5173/`). Weitere Präsentationen liegen als eigene Dateien in `decks/` und öffnen sich mit `?deck=<Dateiname>`:

- `decks/anderepraesentation.md` → `http://localhost:5173/?deck=anderepraesentation`

Alle Präsentationen teilen sich `public/media/` und das Design, die Inhalte sind unabhängig. Neue Präsentation: Datei in `decks/` anlegen (z. B. `slides.md` kopieren).

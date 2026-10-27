# Pogoradio

Archiv der Radiosendung Pogoradio auf Bermudafunk 105,4: Interviews und Geschichten unter
**https://pogoradio.neocities.org**

## So kommt die Website online

- Der Ordner `site/` ist die Website. Jede Änderung auf `main` wird automatisch zu Neocities übertragen
  (`.github/workflows/neocities.yml`, Schlüssel im Repository-Secret `NEOCITIES_API_TOKEN`).
  Dateien, die nicht in `site/` liegen, werden auf Neocities gelöscht.
- **ZIP-Briefkasten:** Eine ZIP-Datei, die in den Hauptordner hochgeladen wird, entpackt die Automatik
  in `site/` und löscht die ZIP danach. Der Dateiname ist egal. Liegt in der ZIP eine `_loeschen.txt`,
  wird jeder darin genannte Pfad unter `site/` vorher gelöscht (eine Zeile pro Pfad).

## Aufbau

```
site/
  index.html                  Startseite mit der Liste aller Seiten
  pogoradio-logo.png          Logo für die Startseite
  favicon.ico, apple-touch-icon.png
  interviews/<name>/          eine Seite pro Interview: index.html + Bilder
  geschichten/<name>/         Geschichten und O-Töne
  sendungen/                  Sendungsarchiv: alle Sendungen 2000–2018 mit Gast, Songliste, MP3-Dateiname
  interview-archiv/           Interviews aus dem alten Blog pogoradio.de (2005–2015): Liste mit Suche
  interview-archiv/<name>/    die Text-Interviews aus dem Blog, behutsam redigiert, je eine Seite mit eigenem Look
```

Adressen: `pogoradio.neocities.org/interviews/<name>/`

Sendungsarchiv und Interview-Archiv wurden aus der alten WordPress-Datenbank (Stand August 2017) erzeugt.
Die Daten stecken als JSON direkt in der jeweiligen `index.html`. Die Datenbank selbst liegt nicht im Repo.
Die 36 Text-Interviews im Interview-Archiv sind behutsam redigiert (Rechtschreibung, Zeichensetzung, einheitliches
Frage-Antwort-Layout, tote Links entfernt; Inhalt und Ton unverändert). Die Liste verlinkt auf diese Seiten,
die Suche durchsucht ihren Text.

## Neue Seite hinzufügen

1. Ordner `site/interviews/<name>/` anlegen (Kleinbuchstaben, Bindestriche, keine Umlaute) mit `index.html` und den Bildern.
2. Jede Seite hat ihren eigenen Look. Oben steht immer die Rücklink-Leiste (siehe unten).
3. Bilder als JPEG, zugeschnitten und höchstens etwa 1200 Pixel breit.
4. Keine MP3-Dateien (kostenloses Neocities-Konto). Aufnahmen als SoundCloud-Link.
5. In `site/index.html` einen Eintrag in zeitlicher Reihenfolge ergänzen, den Zähler bei „Gespräche“ erhöhen und den Namen in der Beschreibung (`meta description`) nachtragen.

## Rücklink-Leiste

Ins `<head>`:

```html
<style id="pgr-bar-css">
.pgr-bar{position:relative;z-index:60;display:flex;align-items:center;min-height:44px;margin:0;padding:0 max(16px,env(safe-area-inset-right,0px)) 0 max(16px,env(safe-area-inset-left,0px));background:#2f2e2b;color:#ece8e1;border-bottom:1px solid #403e3a;font:600 14px/1.2 system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;letter-spacing:.01em;text-align:left}
.pgr-bar a.pgr-bar__home{display:inline-flex;align-items:center;gap:.55em;padding:12px 0;color:#ece8e1;text-decoration:none;font:inherit}
.pgr-bar a.pgr-bar__home:hover{color:#fff;text-decoration:underline;text-decoration-color:#ff4d3d;text-decoration-thickness:2px;text-underline-offset:.3em}
.pgr-bar a.pgr-bar__home:focus-visible{outline:2px solid #ff4d3d;outline-offset:3px;border-radius:2px}
.pgr-bar__dot{width:7px;height:7px;border-radius:50%;background:#ff4d3d;flex:none}
</style>
```

Direkt nach `<body>`:

```html
<div class="pgr-bar" role="navigation" aria-label="Pogoradio"><a class="pgr-bar__home" href="/"><span aria-hidden="true">←</span><span class="pgr-bar__dot" aria-hidden="true"></span>Pogoradio-Archiv</a></div>
```

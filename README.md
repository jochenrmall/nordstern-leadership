# NORDSTERN.Leadership — Gesamt V1

**Live:** https://nordstern-leadership.de

## Dateistruktur

| Datei | URL | Beschreibung |
|---|---|---|
| `index.html` | nordstern-leadership.de/ | Hauptseite / Über Jochen Mall |
| `kompass.html` | nordstern-leadership.de/kompass.html | Standortbestimmung (8-Fragen-Quiz) |
| `steuermann-test.html` | .../steuermann-test.html | Führungszeit-Check |
| `antreiber-test.html` | .../antreiber-test.html | Wirkungscheck |
| `vermittler-test.html` | .../vermittler-test.html | Energiebilanz-Check |
| `orientierungssucher-test.html` | .../orientierungssucher-test.html | Klarheits-Check |
| `kombinationen.pdf` | .../kombinationen.pdf | 14 Führungstyp-Kombinationen |

## Deployment

1. Alle Dateien in GitHub Repository `jochenrmall/nordstern-leadership` hochladen
2. GitHub Pages: Branch `main`, Root `/`
3. DNS: A-Records auf GitHub Pages IPs (185.199.108-111.153)

## Technisch

- Kein Framework, kein Build-Step — reines HTML/CSS/JS
- Formspree ID: `xreovnld`
- Cloudflare: `data-cfasync="false"` auf allen Scripts, keine E-Mail-Adressen im HTML

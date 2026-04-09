# NORDSTERN Leadership · Deployment Guide

## Dateistruktur

```
nordstern-leadership/
├── index.html                    Standortbestimmung (8-Fragen-Quiz, Typ-Routing)
├── steuermann-test.html          Führungszeit-Check (für den Steuermann)
├── antreiber-test.html           Wirkungscheck (für den Antreiber)
├── vermittler-test.html          Energiebilanz-Check (für den Vermittler)
├── orientierungssucher-test.html Klarheits-Check (für den Orientierungssucher)
├── kombinationen.pdf             Typkombinationen-Referenz (A4 Querformat)
├── CNAME                         nordstern-leadership.de
└── README.md                     Diese Datei
```

---

## Deployment: GitHub Pages

### Schritt 1 — Repository anlegen
1. github.com → New repository
2. Name: `nordstern-leadership`
3. Visibility: Public (erforderlich für kostenlose GitHub Pages)
4. Alle Dateien hochladen

### Schritt 2 — GitHub Pages aktivieren
1. Repository → Settings → Pages
2. Source: Deploy from branch
3. Branch: `main` / Ordner: `/ (root)`
4. Save

### Schritt 3 — Custom Domain
1. Settings → Pages → Custom domain → `nordstern-leadership.de`
2. HTTPS aktivieren (nach DNS-Konfiguration, dauert ~15 Min)

---

## DNS-Konfiguration (beim Domain-Registrar)

### A-Records (für nordstern-leadership.de)
```
@  A  185.199.108.153
@  A  185.199.109.153
@  A  185.199.110.153
@  A  185.199.111.153
```

### CNAME (für www-Weiterleitung)
```
www  CNAME  [dein-github-user].github.io
```

DNS-Propagation: ~15–60 Minuten.

---

## Formspree einrichten

1. formspree.io → Kostenloser Account mit jochen.r.mall@gmail.com
2. New Form → Name: "NORDSTERN Kompass"
3. Form ID kopieren (Format: `xxxxxxxx`)
4. In **allen 5 HTML-Dateien** ersetzen:
   ```javascript
   const FORMSPREE_ID = 'YOUR_FORM_ID';
   //  → ersetzen durch:
   const FORMSPREE_ID = 'xxxxxxxx';
   ```

Das gilt für: `index.html`, `steuermann-test.html`, `antreiber-test.html`,
`vermittler-test.html`, `orientierungssucher-test.html`

---

## Referral-Tracking verstehen

### Wie es funktioniert
Jeder Nutzer erhält beim ersten Besuch eine anonyme Session-ID (8 Zeichen, zufällig).

**Jochen teilt:** `nordstern-leadership.de` (ohne Parameter)

**Ebene 1 — Person A klickt den Share-Button:**
URL: `?ref=abc12345&depth=1`

**Ebene 2 — Person A teilt mit Person B:**
URL: `?ref=xyz67890&depth=2&parent=abc12345`

**Was bei jedem Besuch via Referral passiert:**
- Stiller POST an Formspree mit: `type=referral_visit, ref, depth, parent, page`
- Du bekommst eine E-Mail pro Referral-Visit

**Was bei einer Kontaktanfrage passiert:**
- Formspree-Submission mit Name, E-Mail, Typ, Score + `ref, depth`
- Du siehst: auf welcher Ebene der Kontakt entstanden ist

### Was du damit auswerten kannst
| Ebene | Metrik | Bedeutung |
|-------|--------|-----------|
| Direkt (depth=0) | Kontaktanfragen | Konversionsrate deiner direkten Kontakte |
| Ebene 1 (depth=1) | Visits + Anfragen | Weiterleitung durch deine Kontakte |
| Ebene 2+ (depth≥2) | Visits + Anfragen | Organische Verbreitung |

---

## Test-URLs (lokal)

Zum lokalen Testen einen einfachen HTTP-Server starten:
```bash
cd nordstern-leadership
python3 -m http.server 8080
# → http://localhost:8080
```

---

## Technische Details

- **Kein Backend** erforderlich — alle Daten laufen über Formspree
- **Mobile-first** — Touch-Targets ≥ 44px, clamp() für Schriftgrößen
- **Referral-ID** — in sessionStorage (nicht localStorage, kein Cookie)
- **Share-Mechanik** — `navigator.share()` auf Mobile, Clipboard-Fallback auf Desktop
- **Alle Tests** — kostenlos, kein Login, kein Tracking außer Formspree

---

*NORDSTERN Leadership · Dr.-Ing. Jochen Mall · nordstern-leadership.de*

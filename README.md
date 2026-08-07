# Head & Neck Ultrasound Conference — app-pakke

Denne mappe indeholder hele hjemmesiden som en installerbar app (PWA).
Når den er lagt på GitHub Pages, kan alle deltagere lægge den på deres
hjemmeskærm og bruge den som en almindelig app — med eget ikon, uden
adresselinje, og den virker delvist offline.

## Indhold

```
index.html               ← selve appen (side-navigation, runde hjørner)
manifest.json             ← fortæller telefonen navn, farve og ikon
sw.js                      ← service worker, gør appen offline-klar
icon-192.png               ← app-ikon (Android)
icon-512.png               ← app-ikon (Android, stor)
icon-maskable-512.png      ← app-ikon (Android, "maskable" variant)
apple-touch-icon.png       ← app-ikon (iPhone/iPad)
favicon-32.png              ← lille ikon til browserfanen
.nojekyll                   ← fortæller GitHub Pages at vise filerne som de er
```

## 1. Læg filerne på GitHub

**Nemmeste metode (uden terminal):**

1. Gå ind på [github.com](https://github.com) og log ind.
2. Opret et nyt repository (grønt "New" knap) — kald det fx `hnus-conference-app`.
   Vælg **Public** (GitHub Pages kræver et gratis offentligt repo, medmindre
   I har en betalt konto).
3. Klik **"uploading an existing file"** på den tomme repo-side.
4. Træk **alle filerne i denne mappe** ind i browservinduet (også `.nojekyll`
   — den kan se "usynlig" ud, men den skal med).
5. Klik **Commit changes**.

**Med terminal (hvis I foretrækker det):**
```bash
cd sti/til/denne/mappe
git init
git add .
git commit -m "Første version af konference-appen"
git branch -M main
git remote add origin https://github.com/BRUGERNAVN/hnus-conference-app.git
git push -u origin main
```

## 2. Slå GitHub Pages til

1. Inde i repoet: **Settings → Pages** (i venstre menu).
2. Under **Build and deployment** → **Source**: vælg **Deploy from a branch**.
3. Under **Branch**: vælg **main** og mappen **/ (root)**. Klik **Save**.
4. Vent ca. 1 minut. Siden linker du til vil se ud som:
   `https://BRUGERNAVN.github.io/hnus-conference-app/`

Det er **denne adresse**, deltagerne skal åbne på deres telefon.

## 3. "Installér" appen på telefonen (genvejsmetoden)

### iPhone / iPad (Safari)
1. Åbn linket ovenfor i **Safari** (skal være Safari, ikke Chrome).
2. Tryk på **Del-ikonet** (firkant med pil op) nederst.
3. Vælg **"Føj til hjemmeskærm"** (Add to Home Screen).
4. Bekræft navnet og tryk **Tilføj**.

Appen ligger nu som et ikon på hjemmeskærmen og åbner uden browser-ramme
omkring, ligesom en rigtig app.

### Android (Chrome)
1. Åbn linket i **Chrome**.
2. Tryk på **de tre prikker** øverst til højre.
3. Vælg **"Installer app"** eller **"Føj til startskærm"**.
4. Bekræft.

På mange Android-telefoner popper Chrome selv et lille "Installer"-banner
op efter et par sekunder på siden — så kan man bare trykke på det.

## Vigtigt at vide

- **HTTPS er et krav** for at "Installer app" / offline-funktionen virker.
  GitHub Pages giver automatisk HTTPS, så det er klaret, så snart siden er
  live på `github.io`-adressen.
- Hvis I **omdøber filer eller mappen**, skal stierne i `manifest.json`,
  `sw.js` og `<head>` i `index.html` opdateres til at matche — ellers kan
  ikonerne eller offline-cachen ikke findes.
- Hvis I opdaterer `index.html` senere og ændringerne ikke slår igennem på
  telefoner der allerede har installeret appen: opdatér tallet i
  `CACHE_NAME` øverst i `sw.js` (fx `hnus-conf-v2`). Det tvinger telefonen
  til at hente den nye version i stedet for at vise den gemte offline-kopi.
- Alt indhold og al logik (stationsrotation, admin-opslag, live "nu"-kort
  osv.) er uændret — denne pakke tilføjer kun det, der skal til for at
  gøre siden installerbar som app.

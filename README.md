# 💧 Apometre — Aplicație Web (PWA) — funcționează fără Mac!

Aceasta este o **aplicație web** care se comportă ca o aplicație nativă pe iPhone:
icon pe ecranul principal, ecran complet, funcționează offline.

**Avantaj major:** o testezi/hostezi de pe **Windows** — nu ai nevoie de Mac sau Xcode.

---

## Ce face aplicația

Identic cu versiunea nativă simplă:
1. Apeși **📷 Adaugă**
2. Se deschide camera telefonului
3. Fotografiezi apometrul
4. Introduci indexul (+ denumire opțională)
5. Salvezi → apare în listă
6. Poți exporta tot ca CSV

Toate datele rămân **local, pe iPhone**, salvate în memoria browserului (IndexedDB) — nimic nu trece prin server.

---

## PASUL 1 — Găzduiește aplicația (de pe Windows)

Ai nevoie ca cele 5 fișiere să fie accesibile printr-un URL `https://...`
(Safari pe iPhone cere HTTPS pentru cameră + funcționare offline).

### Cea mai simplă metodă: GitHub Pages (gratuit, 10 minute)

1. Creezi cont gratuit pe **github.com** (dacă nu ai deja)
2. Click **"New repository"** → nume: `apometre` → **Public** → Create
3. Click **"Add file" → "Upload files"**
4. Tragi cele 5 fișiere din arhivă: `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`
5. Click **"Commit changes"**
6. Mergi la **Settings → Pages** (meniul din stânga)
7. La **"Source"** selectezi branch-ul `main` → **Save**
8. După ~1 minut, apare un URL de forma:
   ```
   https://numele-tau.github.io/apometre/
   ```

Acesta e link-ul aplicației tale — funcționează pe orice telefon, oriunde.

### Alternativă: Netlify Drop (și mai simplu, fără cont GitHub)

1. Deschizi **app.netlify.com/drop** în browser (pe Windows)
2. Tragi folderul `ApometrePWA` direct în pagină
3. În câteva secunde primești un URL gen `https://ceva-random.netlify.app`
4. Gata — acesta e link-ul aplicației

---

## PASUL 2 — Instalezi pe iPhone

1. Deschizi link-ul (de la Pasul 1) în **Safari** pe iPhone (obligatoriu Safari, nu Chrome!)
2. Apeși butonul **Share** (pătratul cu săgeata în sus, jos pe ecran)
3. Derulezi și apeși **"Add to Home Screen"** (Adaugă pe ecranul principal)
4. Apeși **"Add"** sus-dreapta

Acum ai o iconiță albastră cu picătură pe ecranul principal, exact ca o aplicație nativă. Se deschide în ecran complet, fără bara de Safari.

---

## De ce funcționează fără Mac

| | Aplicație nativă (Swift) | Aplicație PWA (asta) |
|---|---|---|
| Necesită Mac + Xcode | ✅ Da | ❌ Nu |
| Cont Apple Developer | ✅ Da (chiar și gratuit) | ❌ Nu |
| Expiră după 7 zile | ✅ Da (cont gratuit) | ❌ Nu, permanent |
| Acces la cameră | ✅ Da | ✅ Da |
| Funcționează offline | ✅ Da | ✅ Da (după prima încărcare) |
| Icon pe ecran principal | ✅ Da | ✅ Da |
| Din App Store | ✅ Posibil | ❌ Nu (dar nu ai nevoie) |

---

## Testare locală pe Windows (opțional, înainte de hosting)

Dacă vrei să vezi aplicația funcțională direct pe laptopul Windows înainte s-o pui online:

1. Instalezi Python (python.org), dacă nu-l ai deja
2. Deschizi Command Prompt în folderul `ApometrePWA`
3. Rulezi:
   ```
   python -m http.server 8000
   ```
4. Deschizi în browser: `http://localhost:8000`

> Notă: camera nu va funcționa pe `localhost` din alt device — testarea reală a camerei se face doar de pe iPhone, după ce ai hostat aplicația (Pasul 1).

---

## Structura fișierelor

```
ApometrePWA/
├── index.html      ← toată aplicația (HTML+CSS+JS într-un singur fișier)
├── manifest.json   ← configurare PWA (nume, iconițe, culori)
├── sw.js           ← service worker (funcționare offline)
├── icon-192.png    ← iconiță
└── icon-512.png    ← iconiță (rezoluție mare)
```

---

## Limitări față de aplicația nativă Swift

- Spațiul de stocare e limitat de browser (de obicei sute de MB — suficient pentru mii de poze comprimate)
- Dacă ștergi datele Safari ("Clear website data"), pierzi înregistrările — exportă CSV periodic ca backup
- Nu apare în App Store (dar nu ai nevoie, e deja pe ecranul principal)

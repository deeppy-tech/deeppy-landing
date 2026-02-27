# DeePPy Landing Page — Deploy Guide

## Cosa c'è in questo progetto

Landing page standalone per **deeppy.eu** — React + Vite, pronta per GitHub Pages.

Include: landing page completa (hero, features, catalogo demo, form contatto, footer), GDPR cookie banner bilingue IT/EN, GA4 + PostHog (si attivano solo dopo consenso), form contatto con Formspree, meta tag Open Graph per social sharing.

Non include: login, dashboard, piattaforma (quelli arrivano con l'MVP di Mousa).

---

## Step 1 — Attiva Formsubmit.co (dopo il deploy)

Formsubmit.co è gratuito, illimitato, e non richiede account.
L'integrazione è già nel codice — i lead arrivano a **info@deeppy.eu**.

Dopo che il sito è online (Step 6):
1. Vai su deeppy.eu e compila il form con dati di test
2. Ricevi un'email di conferma a info@deeppy.eu → clicca il link
3. Da quel momento tutti i lead arrivano automaticamente

Questa attivazione è **una tantum** — i lead non vedranno mai nulla di strano.

---

## Step 2 — Crea repository GitHub

1. Vai su [github.com/new](https://github.com/new)
2. Nome: `deeppy-landing` (privato va bene)
3. Non aggiungere README o .gitignore (il progetto li ha già)

---

## Step 3 — Carica il progetto

Apri terminale nella cartella `deeppy-landing/`:

```bash
git init
git add .
git commit -m "Initial deploy"
git branch -M main
git remote add origin https://github.com/TUO_USERNAME/deeppy-landing.git
git push -u origin main
```

---

## Step 4 — Attiva GitHub Pages

1. Vai in **Settings → Pages** nel tuo repository
2. Source: seleziona **GitHub Actions**
3. Il workflow `.github/workflows/deploy.yml` farà build e deploy automaticamente ad ogni push

---

## Step 5 — Configura DNS (deeppy.eu)

Nel pannello del tuo registrar DNS (dove hai comprato deeppy.eu), aggiungi questi record:

**Opzione A — CNAME (raccomandato se non hai altri servizi sul dominio)**:
```
Tipo: CNAME
Nome: @  (oppure deeppy.eu)
Valore: TUO_USERNAME.github.io
```

**Opzione B — A records (se il registrar non supporta CNAME su root)**:
```
Tipo: A    Nome: @    Valore: 185.199.108.153
Tipo: A    Nome: @    Valore: 185.199.109.153
Tipo: A    Nome: @    Valore: 185.199.110.153
Tipo: A    Nome: @    Valore: 185.199.111.153
```

Aggiungi anche il www:
```
Tipo: CNAME    Nome: www    Valore: TUO_USERNAME.github.io
```

---

## Step 6 — Verifica HTTPS

1. Vai in **Settings → Pages** nel repository
2. Sotto **Custom domain**, inserisci `deeppy.eu`
3. Spunta **Enforce HTTPS**
4. GitHub genera automaticamente il certificato SSL (può richiedere fino a 24h)

---

## Step 7 — Crea OG Image

Serve un'immagine 1200×630px per la condivisione social, da mettere in `public/og-image.png`.
Contenuto suggerito: sfondo navy #0B1D3A, logo DeePPy al centro, tagline sotto.

---

## Struttura file

```
deeppy-landing/
├── .github/workflows/deploy.yml  ← CI/CD automatico
├── public/
│   └── CNAME                     ← Dominio custom
├── src/
│   ├── main.jsx                  ← Entry point React
│   └── App.jsx                   ← Landing page completa (~620 righe)
├── index.html                    ← HTML base
├── package.json                  ← Dipendenze
├── vite.config.js                ← Config Vite
└── README.md                     ← Questo file
```

---

## Aggiornamenti

Per aggiornare il sito, modifica i file e fai push:

```bash
git add .
git commit -m "Descrizione modifica"
git push
```

Il deploy è automatico (1-2 minuti).

---

## Quando arriva l'MVP

Quando Mousa ha l'MVP pronto su AWS, cambi solo i record DNS:
- Rimuovi i record A/CNAME che puntano a GitHub
- Aggiungi i record che puntano all'AWS di Mousa

Transizione trasparente, zero downtime percepito.
 

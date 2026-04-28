# Sito campagna — Gison (Melito di Napoli)

Sito statico HTML/CSS, release **v1.0.0**.

## Pubblicazione su GitHub

1. Crea un repository vuoto su GitHub (es. `scuolaeguida` o `gison-2025`).
2. **Repository remoto:** [github.com/nikpalumbo/scuolaeguida](https://github.com/nikpalumbo/scuolaeguida) (già creato; `origin` punta lì).

   Per clonare altrove:

   ```bash
   git clone https://github.com/nikpalumbo/scuolaeguida.git
   ```

   Nel repo è già presente:
   - branch **main** (principale)
   - branch **v1** (stesso contenuto, utile se vuoi impostare Pages solo su `v1`)
   - tag annotato **`v1.0.0`** (release v1)

3. **GitHub Pages:** *Settings → Pages →* branch **main**, cartella **/** (root), Salva.

## Dominio: **scuolaeguida.com**

Il repo contiene un file `CNAME` con `scuolaeguida.com` (dominio “nudo”, senza `www`).

1. **Su GitHub:** *Settings → Pages → Custom domain* → inserisci `scuolaeguida.com` → *Save*. Attendi il check DNS/HTTPS (minuti, a volte ore).
2. **Dal pannello DNS** del registrar (dove comprato il dominio), per l’**apex** `scuolaeguida.com` aggiungi **quattro record A** (IPv4) verso i server di GitHub Pages, come in [questa guida ufficiale](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain) — tipicamente:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`  
   (Verifica l’elenco aggiornato nel link: GitHub a volte aggiorna gli IP.)
3. *Enforce HTTPS* in Pages quando il certificato risulta pronto.
4. Se invece preferisci solo **`www.scuolaeguida.com`**: nel DNS usa un **CNAME** `www` → `nikpalumbo.github.io` e in *Custom domain* metti `www.scuolaeguida.com`; in quel caso aggiorna anche la riga nel file `CNAME` in repo in modo che coincida (un solo hostname per file).

I path del sito (`/assets/...`, `/educazione/...`) vanno bene con il dominio in root.

### Il sito non compare / vedi ancora GoDaddy (“Launching soon”, Website Builder)

Succede se **il DNS del dominio non punta ai server di GitHub** oppure **GoDaddy sta servendo una pagina sua** (Website Builder / “parking”) invece del sito Pages.

1. **Nome del dominio:** usa **`scuolaeguida.com`** (una sola “e” in *scuola*), uguale al file `CNAME` e a *Custom domain* su GitHub.
2. **Nel pannello GoDaddy (o altro registrar):**
   - Apri **DNS** per `scuolaeguida.com` e **sostituisci** gli indirizzi non GitHub sugli record **A** @ (apex) con i **quattro IP** GitHub Pages sopra (185.199.108.153 ecc.), oppure elimina i record A “strani” e aggiungi quelli corretti.
   - Se usi **solo `www`**, CNAME `www` → `nikpalumbo.github.io` (come da guida GitHub).
   - **Disattiva / non usare** il sito “Website Builder” o la pagina di atterraggio GoDaddy sullo stesso hostname, altrimenti continua a vincere quella.
3. **Su GitHub:** *Settings → Pages* — *Custom domain* = `scuolaeguida.com`, salva; quando il check è verde, *Enforce HTTPS*.

Verifica rapida: `dig scuolaeguida.com +short` dovrebbe mostrare gli IP **185.199.108.x** (non 13.x / 76.x tipici di altri servizi) dopo la propagazione (anche 24 h).

Mentre sistemi il DNS, il sito resta visibile su: `https://nikpalumbo.github.io/scuolaeguida/`

## Se testi senza dominio (solo `user.github.io/nome-repo/`)

Fino a quando la pagina non è in root del dominio, i path assoluti `/assets/` non puntano al repo. Soluzioni: collegare subito il dominio, oppure aprire `index.html` in locale con `python3 -m http.server`, oppure in un secondo momento adottare un `<base href="/nome-repo/">` in tutte le HTML.

## Sviluppo locale

```bash
cd /percorso/scuolaeguida
python3 -m http.server 8080
# http://127.0.0.1:8080
```

## Struttura utile

- `index.html` — landing principale  
- `concetti-landing.html`, `landing-b.html`, `landing-c.html` — varianti  
- `bozze.html` — bozze “tecniche” (classico / moderno / comunità)  
- `educazione/` — pagine per ordini di scuola  
- `assets/` — logo, immagini, CSS  

Il file `.nojekyll` evita che GitHub tratti il sito con Jekyll (file/cartelle con `_`).

### Domini, `CNAME` e record TXT

- Il file **`CNAME`** in root (contenuto: `scuolaeguida.com`) è quello che GitHub Pages legge: va tenuto in repo e deve coincidere con *Settings → Pages → Custom domain* (senza `www` se usi l’apex come nel file).
- I record **DNS** (A per l’apex, oppure CNAME per `www`, eventuale **TXT** per verifica posta/SSL) si configurano **solo dal registrar / DNS** — non vanno inseriti come pagine del sito. Il sito statico li “vede” già se il dominio punta a GitHub.
- Nelle HTML ci sono i **`rel="canonical"`** con `https://scuolaeguida.com/...` più `robots.txt` e `sitemap.xml` per motore di ricerca e condivisione.

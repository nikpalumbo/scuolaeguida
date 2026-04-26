# Sito campagna — Nicola Gison (Melito di Napoli)

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

3. **GitHub Pages:** *Settings → Pages →* scegli branch **main** o **v1**, cartella **/** (root), Salva.  
4. Dopo qualche minuto il sito sarà su `https://TUO_UTENTE.github.io/TUO_REPO/` **solo se** adatti i percorsi (vedi sotto) **oppure** usi un dominio personalizzato a root.

## Dominio personalizzato (consigliato)

1. *Settings → Pages → Custom domain:* inserisci il dominio (es. `www.tuodominio.it`).
2. Segui le istruzioni per i record **DNS** (A/AAAA o CNAME) indicati da GitHub.
3. Spunta *Enforce HTTPS* quando disponibile.  
4. I link del sito usano la root del dominio (`/assets/...`, `/educazione/...`) e funzionano senza modifiche.

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

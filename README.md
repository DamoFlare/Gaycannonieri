# ⚽ Classifica Cannonieri Calcetto

SPA leggera (HTML + Tailwind CDN + JS vanilla) per la classifica marcatori e presenze del calcetto tra amici, pubblicata su **GitHub Pages**. Nessuno step di build: il workflow copia semplicemente `index.html` e `data.json` nella cartella `public/`.

## Struttura

```
.
├── .github/workflows/pages.yml   # workflow di deploy su GitHub Pages
├── index.html                    # tutta l'app (markup + logica JS)
├── data.json                     # dati dei giocatori (unico file da aggiornare)
└── README.md
```

## Come aggiornare la classifica (anche da smartphone)

I dati vivono tutti in `data.json`. Non serve toccare `index.html`.

1. Apri il repository su **GitHub** dal browser del telefono (anche dentro WhatsApp/Chrome va bene).
2. Vai sul file `data.json`.
3. Tocca l'icona della matita ✏️ in alto a destra per aprire l'editor da mobile (se vedi solo l'icona "occhio", tocca prima quella e poi la matita).
4. Modifica i valori del giocatore che vuoi aggiornare, ad esempio dopo una partita:

   ```json
   {
     "id": 1,
     "nome": "Marco Bianchi",
     "soprannome": "Il Falco dell'Area Piccola",
     "gol": 19,
     "partite": 11,
     "ammonizioni": 1,
     "foto": ""
   }
   ```

5. Per aggiungere un nuovo giocatore, copia un blocco `{ ... }` esistente, incollalo dentro le parentesi quadre `[ ]` (separato dagli altri con una virgola) e assegna un `id` non ancora usato.
6. Scorri in fondo, scrivi un messaggio di commit (es. "Aggiornamento partita 11/09") e tocca **Commit changes** scegliendo di committare direttamente sul branch `main`.
7. Il workflow GitHub Actions parte automaticamente e in ~1 minuto il sito è aggiornato su GitHub Pages.

### Attenzione al formato JSON

- Ogni giocatore è un oggetto `{ }` separato da virgola dagli altri.
- L'ultimo oggetto della lista **non** deve avere la virgola dopo la parentesi graffa finale.
- I campi `gol`, `partite`, `ammonizioni` sono numeri (senza virgolette), `nome`, `soprannome`, `foto` sono testo (con virgolette).
- Se il sito dopo il deploy mostra l'errore "Impossibile caricare data.json", quasi sempre è una virgola o una parentesi fuori posto: usa un validatore JSON online (es. jsonlint.com) per controllare velocemente.

## Campo `foto`

Puoi lasciare `"foto": ""` per usare le iniziali del nome come avatar, oppure incollare l'URL di un'immagine pubblica (es. link diretto a un'immagine su Imgur) per mostrare una foto vera.

## Attivare GitHub Pages

Il workflow in `.github/workflows/pages.yml` è già pronto, ma la prima volta devi collegare il repository a GitHub Pages:

1. Vai su **Settings → Pages** nel repository.
2. Alla voce **Source**, seleziona **GitHub Actions** (non "Deploy from a branch").
3. Al primo push sul branch `main`, il workflow **Deploy to GitHub Pages** parte da solo (visibile nel tab **Actions**) e pubblica il sito.
4. L'URL del sito compare in **Settings → Pages** una volta completato il primo deploy.

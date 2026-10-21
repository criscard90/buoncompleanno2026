# Biglietto di auguri interattivo – Buon Compleanno 🎉

Pagina web **autocontenuta** (un solo file `index.html`) che mostra un carosello di
10 immagini con musica di sottofondo, effetti Ken Burns, dissolvenze incrociate e
particelle animate. Funziona offline e su GitHub Pages.

## Struttura del progetto

| File             | Descrizione                                                   |
|------------------|---------------------------------------------------------------|
| `index.html`     | Tutta la logica, gli stili e le animazioni (CSS + JS inline). |
| `musica.mp3`     | La traccia audio di sottofondo (in loop). **Da caricare tu.**  |
| `foto1.jpg` … `foto10.jpg` | Le 10 immagini del carosello. **Da sostituire con le tue foto** (oppure usa i segnaposto numerati già presenti). |

## Come usarlo

1. **Immagini** – Sostituisci `foto1.jpg`, `foto2.jpg`, … `foto10.jpg` con le tue
   foto mantenendo **gli stessi nomi** (o modifica l'array `images` nel file
   `index.html` se preferisci nomi/estensioni diversi).
2. **Musica** – Carica il tuo file audio chiamandolo `musica.mp3` nella stessa
   cartella (se usi un altro formato, aggiorna anche il tag `<source>` nell'HTML).
3. **Testi** – Sono già inseriti i 10 messaggi. Li trovi nell'array `texts` nel
   file `index.html` (una frase per immagine, in ordine).
4. **Anteprima** – Apri `index.html` con un browser (doppio click) e premi
   **«Inizia»**.

## Personalizzare i parametri (in cima allo `<script>` di `index.html`)

```js
const musicStartTime = 0;      // secondo da cui parte la musica (0 = dall'inizio)
const slideDuration = 10000;   // durata di ogni slide in ms (10000 = 10 s)
const boostGapMin = 9000;      // min ms tra uno scoppio di foglie e l'altro
const boostGapMax = 18000;     // max ms (il ritardo è casuale tra min e max)
```

- `musicStartTime`: se la tua canzone ha un'intro da saltare, imposta qui il
  secondo di inizio.
- `boostGapMin` / `boostGapMax`: intervalli (in ms) tra gli scopi di foglie. Ogni
  boost parte dopo un ritardo CASUALE tra min e max, per tutta la durata del carosello.
- `slideDuration`: **se lo cambi, ricordati di aggiornare anche la durata
  dell'animazione Ken Burns nel CSS**: cerca `.kb-animation-1 … 6` e sostituisci
  i `10s` con il valore in secondi equivalente a `slideDuration`.

## Suoni degli auguri 💝 (cuoricini)

Toccando un cuoricino parte un suono a caso preso dalla cartella **`auguri/`**,
senza ripetizioni: tutti i file vengono riprodotti a turno in ordine casuale e,
quando finiscono, la sequenza si **rimescola** e ricomincia.

### 🔉 Ducking della musica di sottofondo

Quando parte il messaggio di auguri, la musica di sfondo (`musica.mp3`) viene
**abbassata automaticamente** per sentire meglio l'audio, e **rilizzata** al
volume normale appena il messaggio termina.

| Parametro | Valore | Descrizione |
|---|---|---|
| `MUSIC_BASE_VOLUME` | `1.0` | Volume normale della musica |
| `DUCK_VOLUME` | `0.18` | Volume durante il messaggio di auguri |
| `DUCK_FADE_MS` | `500` | Durata dell'abbassamento/rialzo (ms) |

> Se due auguri suonano in contemporanea, la musica resta abbassata finché
> **non terminano entrambi**. Se il carosello è già finito, la musica non viene
> più rialzata.

Il sito statico **non può elencare i file di una cartella da solo**, quindi
l'elenco viene cercato in questo ordine:

1. **`auguri/list.json`** — fonte primaria (usata su **GitHub Pages** e con la
   **Live Preview** di VS Code, che non fa directory listing);
2. **Directory listing** della cartella `auguri/` (solo se manca `list.json`;
   funziona con server tipo `python -m http.server`);
3. **Elenco inline** in `index.html` (riserva).

> ⚠️ Quando aggiungi/rimuovi un MP3 in `auguri/`, aggiorna anche
> **`auguri/list.json`** (lista di nomi, es. `["selene.mp3","altro.mp3"]`),
> altrimenti il nuovo file non viene rilevato.

## Pubblicare su GitHub Pages

1. Crea una repo (pubblica o privata con Pages attivo).
2. Carica `index.html`, `musica.mp3` e le 10 immagini nella root.
3. Su GitHub: **Settings → Pages**, scegli il branch `main` e la cartella `/root`.
4. Il sito sarà raggiungibile all'indirizzo `https://<tuo-utente>.github.io/<repo>/`.

> Nota: l'autoplay dell'audio è bloccato dai browser, per questo all'apertura
> compare la schermata **«Tocca per iniziare»**: al tocco/clic parte la musica.

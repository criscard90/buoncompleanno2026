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
const boostStartTimes = [];    // secondi in cui fanno "scoppiare" le particelle
```

- `musicStartTime`: se la tua canzone ha un'intro da saltare, imposta qui il
  secondo di inizio.
- `boostStartTimes`: indica i secondi (rispetto a `musicStartTime`) in corrispondenza
  dei ritornelli per intensificare le particelle. Lascia `[]` per disattivare.
- `slideDuration`: **se lo cambi, ricordati di aggiornare anche la durata
  dell'animazione Ken Burns nel CSS**: cerca `.kb-animation-1 … 6` e sostituisci
  i `10s` con il valore in secondi equivalente a `slideDuration`.

## Pubblicare su GitHub Pages

1. Crea una repo (pubblica o privata con Pages attivo).
2. Carica `index.html`, `musica.mp3` e le 10 immagini nella root.
3. Su GitHub: **Settings → Pages**, scegli il branch `main` e la cartella `/root`.
4. Il sito sarà raggiungibile all'indirizzo `https://<tuo-utente>.github.io/<repo>/`.

> Nota: l'autoplay dell'audio è bloccato dai browser, per questo all'apertura
> compare la schermata **«Tocca per iniziare»**: al tocco/clic parte la musica.

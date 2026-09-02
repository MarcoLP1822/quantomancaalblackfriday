# Quanto manca al Black Friday

Conto alla rovescia vaporwave per il Black Friday, con una strada guidabile e un player
in stile Windows 95.

**→ [marcolp1822.github.io/quantomancaalblackfriday](https://marcolp1822.github.io/quantomancaalblackfriday/)**

Una sola pagina HTML, nessuna dipendenza, nessun build step. Si apre anche facendo
doppio clic su `index.html`.

## Comandi

| Comando | Effetto |
| --- | --- |
| `←` `→` oppure `A` `D` | Sterza l'auto |
| Tocca metà schermo | Sterza su telefono e tablet |
| `▶ Play` | Avvia e mette in pausa la musica |
| Display LCD, o menu `File` | Cambia traccia |
| `◄◄ Slow` / `►► Fast` | Andatura da 0.4× a 2.5× |
| `▦ Grid`, o menu `Options` | Cicla i cinque paesaggi |
| Tasti colorati `CAR` | Colore della carrozzeria |
| Menu `View` | Scanline del monitor on/off |
| Menu `Help` | Finestra con tutti i comandi |
| Barra del titolo | Trascina la finestra; `_ □ ✕` la richiudono |

## Com'è fatto

**Il conto alla rovescia** non ha una data scritta nel codice: calcola ogni volta il
prossimo Black Friday come quarto giovedì di novembre più un giorno, e passa all'anno
successivo appena quello corrente è passato. La differenza è scomposta in mesi, settimane,
giorni, ore e minuti avanzando di mese in mese con il giorno bloccato all'ultimo valido,
così il 31 gennaio più un mese resta dentro febbraio invece di scivolare a marzo.

**La strada** è disegnata su `<canvas>` con una prospettiva esplicita: la banda di indice
`i` sta a `y = orizzonte + altezza / (i + off)`, quindi far scorrere `off` da 1 a 0 e
riavvolgerlo produce un movimento continuo senza giunte. La stessa formula dà la scala
laterale, e da lì derivano larghezza della strada, strisce, tratteggio e posizione
dell'auto — che resta allineata all'asfalto per costruzione invece che per taratura.
Un primo tentativo con `perspective` e `rotateX` in CSS comprimeva l'intera griglia in una
fascia di due unità di viewport: la matematica esplicita è più corta e non va tarata a occhio.

**Il profilo delle montagne** è statico. Una versione precedente scorreva insieme alla
strada e leggeva come un muro che slitta di lato; ora è un tracciato costruito una volta
sola e ridisegnato solo al ridimensionamento.

**Gli oggetti a bordo strada** — sciacallo, palo al neon, cartellone, cactus, e ogni tanto
un arco che scavalca la carreggiata — sono decisi da una funzione hash sull'indice assoluto
della banda. Non esiste una lista di oggetti da aggiornare: la stessa banda produce sempre
lo stesso oggetto, quindi scorrono agganciati alla griglia e non serve memoria.

**La musica** ha due tracce. Una è un mp3. L'altra, `LUNAR WIND.gen`, non è un file: è
synthwave costruito in WebAudio mentre la pagina gira — giro Am7–F–C–G a 100 BPM, basso a
dente di sega, arpeggio quadro dentro una linea di delay con feedback, batteria di rumore
bianco filtrato. Parte da sola al caricamento; se il browser blocca l'audio, cosa normale
finché non c'è un'interazione, la riproduzione si avvia al primo tasto o tocco.

## Verifica

Apri la pagina con `#test` in fondo all'URL: la console esegue i controlli sul conto alla
rovescia (date del Black Friday di più anni e il caso limite di fine mese) e stampa
`self-test passed`.

```
index.html                 tutto: markup, stile, logica
sciacallo-sfaticato.mp3    traccia predefinita
```

## Crediti

Le silhouette vengono da [Openclipart](https://openclipart.org/), **CC0 / pubblico dominio**:

- palme, dall'albero di sinistra di [Camel Palm Trees Silhouette](https://openclipart.org/detail/233917/camel-palm-trees-silhouette) (#233917)
- sciacallo, da [Anubis silhouette](https://openclipart.org/detail/292955/anubis-silhouette) (#292955)

Nient'altro è importato: tipografia solo di sistema, nessun font remoto, nessuna libreria.

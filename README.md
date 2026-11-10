# Template layer GIS

Template Svelte per sviluppare un layer della mappa GIS di Square. Include
una mappa di base e il layer dimostrativo `New layer` con un campo CSV e
due campi numerici. Il template espone gli input; non interpreta il CSV e
non disegna dati personalizzati finché non si implementa il layer.

## Avvio locale

Servono Node.js e npm compatibili con le dipendenze di [`package.json`](package.json).
Dalla radice:

```sh
npm install
npm run dev
```

Aprire l'indirizzo stampato da Vite (porta predefinita `9001`) e visitare
`/gis`. Nelle opzioni di `New layer` caricare
[`src/test.csv`](src/test.csv) e modificare `Minimo` e `Massimo`.
I campi numerici aggiornano lo stato del layer con valori numerici.
Controllare la console del browser: l'implementazione dimostrativa
registra il valore di `min` durante il refresh.

## Personalizzare il layer

1. Aprire [`src/layers/NewLayer/index.js`](src/layers/NewLayer/index.js).
   Impostare nome, stato iniziale e definizioni dei controlli in `_options`.
2. Implementare `render()` per il disegno iniziale e `refresh()` per
   aggiornare dati e stile quando cambia lo stato. Rimuovere risorse e
   sottoscrizioni del layer in `remove()` e `destroy()`.
3. Se si aggiunge un layer separato, registrarne l'istanza con un ID distinto
   in [`src/pages/gis/index.svelte`](src/pages/gis/index.svelte), dove sono
   creati la mappa di base e il layer di esempio.
4. I controlli delle opzioni sono implementati in
   [`src/pages/gis/LayerItem.svelte`](src/pages/gis/LayerItem.svelte).

## Build e anteprima

```sh
npm run build
npm run preview
```

La build genera `build/web/`. L'anteprima usa la porta `9001`; fermare il
server di sviluppo prima di avviarla. Verificare apertura di `/gis`,
selezione del file e comportamento del layer dopo una modifica dei valori.

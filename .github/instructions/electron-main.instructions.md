---
name: Electron main e preload
description: Regole per processo principale e preload
applyTo: "src/main/**,src/preload/**,src/shared/**"
---
- Ogni canale IPC ha nome costante in `src/shared`, input e output tipizzati e input validato con Zod nel main.
- Il main non si fida mai del renderer: valida percorsi, date e payload.
- Percorso dati: `path.join(app.getPath('userData'), 'diario.json')`. Crea il file vuoto valido se manca.
- Scrittura atomica: scrivi su `diario.json.tmp`, poi `rename`. Tieni una copia `diario.json.bak` dell'ultima versione valida.
- Export PDF: finestra nascosta che carica la rotta di stampa del renderer, poi `webContents.printToPDF({ pageSize: 'A4', printBackground: true })`,
  poi `dialog.showSaveDialog` e `fs.writeFile`. Stampa diretta con `webContents.print()`.
- Gestisci gli errori con messaggi chiari verso il renderer, senza stack trace.

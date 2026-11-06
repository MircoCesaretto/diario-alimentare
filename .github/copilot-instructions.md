# Diario Alimentare — istruzioni per Copilot

## Obiettivo
App desktop (Windows) per registrare gli alimenti consumati ogni giorno.
I dati stanno in un file JSON locale. Il diario si esporta in PDF e si può stampare.
Nessun backend, nessun account, nessuna chiamata di rete.
La specifica funzionale è in `docs/spec.md`: leggila prima di implementare una funzione.

## Stack (non cambiarlo senza chiedere)
Electron + electron-vite, React, TypeScript (strict), Tailwind CSS, Zod, date-fns,
Vitest (unit), Playwright (e2e su Electron), ESLint + Prettier, electron-builder.
- Niente moduli nativi (es. better-sqlite3): rompono la build di Electron.
- Aggiungi una dipendenza solo se serve davvero e spiega perché.

## Struttura delle cartelle
- `src/main`      processo principale: finestra, file system, IPC, PDF/stampa
- `src/preload`   bridge sicuro con `contextBridge`: espone solo funzioni tipizzate
- `src/renderer`  interfaccia React (nessun accesso diretto a Node o `fs`)
- `src/shared`    tipi e schemi Zod usati da main e renderer
- `tests/`        test unitari (Vitest) ed e2e (Playwright)

## Comandi (esegui sempre prima di dire che hai finito)
`npm run typecheck`, `npm run lint`, `npm test`, `npm run test:e2e`, `npm run build`.
Dopo ogni modifica lancia i controlli pertinenti e correggi finché passano.

## Regole di sviluppo
- Codice e nomi in inglese; testi dell'interfaccia in italiano.
- Sicurezza Electron: `contextIsolation: true`, `nodeIntegration: false`, `sandbox: true`,
  CSP restrittiva, nessun `remote`, nessun contenuto esterno.
- Il renderer parla col main solo tramite le API del preload (canali IPC tipizzati).
- Date salvate come stringhe `YYYY-MM-DD` e orari `HH:mm` locali (niente oggetti `Date` nel file, niente fusi orari).
- Il file dati ha un campo `version`; ogni lettura è validata con Zod; la scrittura è atomica
  (file temporaneo + rename) e non perde mai i dati esistenti se qualcosa fallisce.
- Interfaccia accessibile: label sui campi, focus visibile, uso da tastiera, contrasto adeguato.
- Stile di stampa/PDF curato (`@media print`, A4, tabelle che non si spezzano male).
- Funzioni piccole, tipi espliciti, niente `any`. Aggiungi test per la logica nuova.

## Agenti
Non c'è backend: non usare `dotnet-dev`.
Flusso: `planner` → `electron-dev` (main/preload/IPC/PDF) e `react-dev` (renderer) → `reviewer` → `tester`,
coordinati da `team`.

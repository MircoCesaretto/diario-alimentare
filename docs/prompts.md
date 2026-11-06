# Prompt da dare in sequenza a `team` (modalità agente)

Dopo ogni passo verifica che i controlli passino e fai un commit prima di passare al successivo.

## 1 — Strumenti di base
@team Il progetto è lo scaffold electron-vite (react-ts). Aggiungi e configura: Tailwind CSS, Zod, date-fns,
Vitest, Playwright per Electron, ESLint + Prettier, TypeScript strict. Crea la cartella `src/shared` e gli script npm
`typecheck`, `lint`, `test`, `test:e2e`, `build`. Verifica che `npm run dev` apra la finestra e che tutti gli script girino.
Aggiorna `.github/copilot-instructions.md` solo se la struttura reale differisce da quella descritta.

## 2 — Dati e salvataggio
@team Leggi `docs/spec.md`. Implementa schema Zod, tipi, repository del file `diario.json` nel main
(lettura validata, scrittura atomica, backup .bak), canali IPC e API nel preload (aggiungi, modifica, elimina, elenca per intervallo).
Test Vitest su repository e validazione, compreso il caso di file corrotto.

## 3 — Inserimento e vista giornaliera
@team Implementa nel renderer il form di inserimento rapido e la vista giornaliera raggruppata per pasto con navigazione tra i giorni.
Usa solo `window.api`. Test e2e Playwright: inserisco una voce, chiudo e riapro l'app, la voce c'è.

## 4 — Modifica, eliminazione, suggerimenti
@team Aggiungi modifica ed eliminazione (con conferma) e i suggerimenti sul campo alimento. Copri con test.

## 5 — Export PDF e stampa
@team Implementa la rotta di stampa, l'export PDF (selezione intervallo, "Salva con nome") e la stampa di sistema.
Curare `@media print` per A4. Test e2e: genera un PDF di un intervallo e verifica che il file esista e non sia vuoto.

## 6 — Backup, rifinitura, installer
@team Aggiungi esportazione/importazione del file JSON (unisci o sostituisci), rivedi accessibilità da tastiera,
poi configura electron-builder per un installer Windows. Esegui la revisione completa con `reviewer` e `tester`.

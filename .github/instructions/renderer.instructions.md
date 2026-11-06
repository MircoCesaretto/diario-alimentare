---
name: Renderer React
description: Regole per l'interfaccia React
applyTo: "src/renderer/**"
---
- Componenti funzionali, hook, TypeScript strict. Stato locale con `useState`/`useReducer`; Zustand solo se serve davvero.
- Mai `window.require` o import di moduli Node: usa solo `window.api` esposto dal preload.
- Stili con classi Tailwind; niente CSS globale oltre a base e `@media print`.
- Form con validazione chiara e messaggi in italiano; salvataggio ottimistico con gestione dell'errore.
- La pagina di stampa è una rotta dedicata (`#/print?from=YYYY-MM-DD&to=YYYY-MM-DD`) senza elementi di navigazione.
- Ogni componente interattivo ha `data-testid` stabili per i test Playwright.

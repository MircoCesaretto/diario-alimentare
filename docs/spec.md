# Specifica — Diario Alimentare (MVP)

## Utente e scopo
Una persona che annota ciò che mangia durante la giornata e, quando serve, ottiene un documento
(PDF o stampa) da consegnare o inviare.

## Funzioni
1. **Inserimento rapido**: data (default oggi), ora (default adesso), pasto
   (colazione, spuntino, pranzo, merenda, cena, altro), alimento (testo libero), quantità (testo libero, opzionale), note (opzionali).
2. **Vista giornaliera**: elenco delle voci del giorno raggruppate per pasto, con navigazione giorno precedente/successivo e selezione data.
3. **Modifica ed eliminazione** di una voce, con conferma per l'eliminazione.
4. **Suggerimenti**: nell'campo alimento, completamento dai valori già inseriti in passato.
5. **Export PDF**: scelta intervallo di date → PDF A4 con intestazione (titolo, periodo, data di generazione)
   e tabella raggruppata per giorno e pasto. Salvataggio con finestra "Salva con nome".
6. **Stampa**: stesso layout dell'export PDF, aperto nella finestra di stampa di sistema.
7. **Backup**: esporta e importa il file JSON (l'importazione chiede se unire o sostituire).

## Fuori ambito (per ora)
Calorie/macro, database di alimenti, sincronizzazione cloud, più profili, app mobile.

## Modello dati (file `diario.json`)
```json
{
  "version": 1,
  "entries": [
    {
      "id": "uuid",
      "date": "2026-11-06",
      "time": "08:30",
      "meal": "colazione",
      "food": "Yogurt greco con miele",
      "quantity": "150 g",
      "notes": ""
    }
  ]
}
```
Regole: `date` = `YYYY-MM-DD`, `time` = `HH:mm`, `food` obbligatorio (max 200 caratteri), `quantity` e `notes` opzionali.

## Criteri di accettazione
- Chiudendo e riaprendo l'app le voci ci sono ancora.
- Se il file è corrotto, l'app non lo sovrascrive: segnala l'errore e propone il ripristino da `.bak`.
- Il PDF di un intervallo con più giorni è leggibile, senza tabelle spezzate a metà riga.
- Tutte le funzioni sono usabili da tastiera.
- `npm run typecheck`, `lint`, `test`, `test:e2e` e `build` passano.

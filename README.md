# Annuario FantAmici — Archivio Storico (Fase 1 · 5 stagioni)

Webapp statica per l'archivio storico del FantAmici: **classifiche finali, Coppa e rose iniziali**, stagione per stagione, con importazione diretta dei file Excel.

## Contenuto
```
index.html                 → la webapp (single-file, nessun backend)
season-data/
    index.json             → elenco stagioni pubblicate (manifest)
    2025-26 · 2024-25 · 2023-24 · 2022-23 · 2021-22 (.json)
```

## Stagioni in archivio
| Stagione | Campione Campionato | Campione Coppa |
|---|---|---|
| 2025/26 | Roberto | Ale&Max |
| 2024/25 | Marco | Fabio |
| 2023/24 | Ale&Max | Ale&Max *(doppietta)* |
| 2022/23 | Fabio | Marco |
| 2021/22 | Roberto | Mario & Amedeo |

## Gestione nomi allenatori (alias + normalizzazione)
Gli stessi allenatori compaiono con grafie diverse tra i file storici. La webapp li unifica automaticamente:
- **Punti rimossi** in fase di normalizzazione: `MARCO D.` → `MARCO D`, `MARCO S.` → `MARCO S`.
- Alias (`NAME_ALIAS` in `index.html`):
  - **Peppe → Greg**
  - **Alessio&Max → Ale&Max**
  - **Mario&Ame → Mario & Amedeo**
  - **Marco S → Santoro** e **Marco D → Marco**
  - **Claudio&Ste → Claudio & Stefano**

> **Santoro** e **Claudio & Stefano** sono allenatori diversi, presenti in annate diverse: la rosa dei 10 partecipanti cambia legittimamente da stagione a stagione.

## Parser Coppa a doppio formato
- **Tabellare** (2025/26): una partita per riga.
- **Testuale andata/ritorno** (dal 2024/25 all'indietro): coppie "Casa - Trasferta" con punteggi "andata / ritorno" e giornate tipo "1 - 17".

Ogni importazione **ricostruisce la classifica Coppa dai singoli risultati** e la confronta con quella ufficiale (obiettivo 10/10).
> Piccole incoerenze note nei file sorgente (solo aggregati gol, non i risultati né V-N-P): **2023/24 Ale&Max** e **2022/23 Domenico**. In entrambi i casi punti e V-N-P coincidono; la sezione Coppa mostra i valori ufficiali del file.

## Come funziona
- **Apertura locale**: doppio clic su `index.html`. Le cinque stagioni sono incorporate.
- **Importa stagione** ⬆: carica i due file, controlla l'anteprima (coerenza risultati Coppa, composizione rose 3-9-9-7, coerenza nomi), poi **Conferma**.
- **Esporta** ⬇ / **Gestisci** ⚙ come nelle versioni precedenti.

## Sezioni
🏆 Riepilogo · 📈 Campionato (classifica + evoluzione animata del podio) · 🏅 Coppa (classifica, Final Four, **scontri diretti cross-stagione**) · 👥 Rose (tutte le rose + Top 3 acquisti per ruolo).

## Pubblicare su GitHub Pages
1. Carica i file mantenendo `season-data/`.
2. `Settings → Pages → Deploy from a branch → main / (root)`.
3. Le stagioni in `season-data/` vengono caricate automaticamente per ogni visitatore.

## Note tecniche
- Parsing lato client: nessun dato lascia il browser.
- Sezioni riconosciute tramite **etichette**, non celle fisse. Normalizzazione nomi con rimozione punti + alias estendibili in `NAME_ALIAS`.
- Librerie da CDN: SheetJS + Chart.js.

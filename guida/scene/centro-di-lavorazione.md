---
title: Centro di lavorazione
parent: Scene
nav_order: 4
---

# Centro di lavorazione

Un erogatore lascia cadere un pezzo sul carrello, che lo porta a due stazioni (ganascia + fresa); a fine corsa un comando di scarico lo espelle nella cassetta. Il pannello in basso ha **Start** (NA), **Stop** (NC), **Emergenza** (NC, bistabile) e il **selettore Auto**, più tre spie (arresto, lavorazione, emergenza) comandate dalle uscite Q1.0–Q1.2; il blocco **Reset scena / Velocità** è comune a tutte le scene.

![Centro di lavorazione]({{ site.baseurl }}/assets/scene/centro-di-lavorazione.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Pezzo caricato |
| I0.1 | Carrello in stazione 1 |
| I0.2 | Carrello in stazione 2 |
| I0.3 | Ganascia 1 chiusa |
| I0.4 | Ganascia 1 aperta |
| I0.5 | Fresa 1: fine lavorazione |
| I0.6 | Fresa 1 spenta |
| I0.7 | Ganascia 2 chiusa |
| I1.0 | Ganascia 2 aperta |
| I1.1 | Fresa 2: fine lavorazione |
| I1.2 | Fresa 2 spenta |
| I1.3 | Carrello a inizio corsa |
| I1.4 | Pulsante Start |
| I1.5 | Pulsante Stop |
| I1.6 | Pulsante di emergenza |
| I1.7 | Selettore Auto |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Carica Pezzo |
| Q0.1 | Carrello avanti (verso destra) |
| Q0.2 | Carrello indietro (verso sinistra) |
| Q0.3 | Ganascia 1: chiudi |
| Q0.4 | Fresa 1: accendi |
| Q0.5 | Ganascia 2: chiudi |
| Q0.6 | Fresa 2: accendi |
| Q0.7 | Scarica Pezzo |
| Q1.0 | Spia di arresto |
| Q1.1 | Spia lavorazione |
| Q1.2 | Spia di emergenza |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

La scena ripete da sola il ciclo: carica un pezzo, il carrello lo porta alla stazione 1, la ganascia si chiude e la fresa lavora (3 s), poi alla stazione 2 con la stessa sequenza, torna a inizio corsa e scarica il pezzo nella cassetta.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

La scena non esegue il ciclo: il carrello si muove solo con i comandi avanti / indietro e ganasce e frese rispondono alle uscite. «Carica pezzo» agisce a fronte di salita. La scena controlla che i comandi siano sensati e segnala le anomalie con un avviso: comandi incompatibili, movimento bloccato (ganascia chiusa o fresa giù), fine corsa, ganascia o fresa a vuoto, pezzo difettoso o danneggiato, lavorazione incompleta, scarico fuori posizione, pezzo incastrato (si sblocca con Reset scena).

## Note

**Sensori trascinabili.** I sensori «Carrello in stazione 1» e «Carrello in stazione 2» sono due testine nere con un led rosso (acceso = carrello rilevato) che si trascinano in orizzontale con il mouse: servono con i sistemi di controllo lenti, che altrimenti fermano il carrello troppo avanti. Doppio clic = posizione standard; la posizione resta memorizzata. Se il carrello si ferma a meno di 16 px dalla stazione si aggancia al centro; oltre, resta dov'è e la fresa va a vuoto.

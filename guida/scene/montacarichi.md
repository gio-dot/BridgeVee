---
title: Montacarichi
parent: Scene
nav_order: 11
---

# Montacarichi

Montacarichi esterno a una casa di 3 livelli (piano terra, 1P, 2P). Il cestello scorre su due colonne; a ogni piano c'è un
balcone con un cancelletto a sblocco elettrico. Pulsantiera fissa a ogni piano e pulsantiera del cestello.

![Montacarichi]({{ site.baseurl }}/assets/scene/montacarichi.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione                                 |
| --------- | ------------------------------------------- |
| I0.0      | Chiamata piano terra                        |
| I0.1      | Chiamata 1° piano                           |
| I0.2      | Chiamata 2° piano                           |
| I0.3      | Pulsante di emergenza (NC: 1 = non premuto) |
| I0.4      | Cestello al piano terra                     |
| I0.5      | Cestello al 1° piano                        |
| I0.6      | Cestello al 2° piano                        |
| I0.7      | Cancelletto piano terra chiuso              |
| I1.0      | Cancelletto 1° piano chiuso                 |
| I1.1      | Cancelletto 2° piano chiuso                 |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione                     |
| --------- | ------------------------------- |
| Q0.0      | Motore SU                       |
| Q0.1      | Motore GIÙ                      |
| Q0.2      | Sblocco cancelletto piano terra |
| Q0.3      | Sblocco cancelletto 1° piano    |
| Q0.4      | Sblocco cancelletto 2° piano    |

## Come lavora

### In DEMO (modalità AUTO, senza PLC collegato)

Il cestello va al piano chiamato con un pulsante oppure, dopo qualche secondo, al piano successivo (PT → 1P → 2P → PT...). Arrivato, la scena attiva lo sblocco del cancelletto di quel piano: il cancelletto si apre da solo insieme alle ante del cestello; dopo qualche secondo toglie lo sblocco, i cancelletti si richiudono e il ciclo riparte.

### Comandata da CadeSimu o da un PLC (EasyPort)

Il PLC comanda il motore (SU / GIÙ) e gli sblocchi dei cancelletti; la scena si occupa del resto:

- **Cancelletti**: con lo sblocco attivo e il cestello fermo al piano il cancelletto si apre da solo (insieme alle due ante del cestello); tolto lo sblocco si richiude. Il sensore «cancelletto chiuso» vale 1 solo a cancelletto chiuso, e la spia sul montante è accesa quando è chiuso.
- **Blocco del motore**: con un cancelletto aperto il motore non parte e compare l'avviso.
- **Pulsanti di chiamata**: si accendono alla pressione e si spengono quando il cestello è fermo al piano; i display mostrano il piano attuale. Lo gestisce la scena, non il PLC; il PLC legge solo il contatto del pulsante.
- **Finecorsa**: la corsa è limitata al piano terra e al 2° piano (coincidono con i rispettivi sensori di piano); se il PLC lascia il motore acceso, dopo 1 s compare l'avviso «Fine corsa».
- **Fermata al 1° piano (approccio ottimistico)**: se è stata chiamata la fermata al 1° piano, il cestello si ferma comunque al piano per 1 s anche se il comando di stop non è ancora arrivato (utile con CadeSimu, che ritarda le uscite). Se dopo 1 s il PLC non ha fermato il motore, il cestello riparte e si ferma dove lo ferma il PLC.
- Con il cestello fermo a meno di 3 unità da un piano, la pedana si allinea al balcone.
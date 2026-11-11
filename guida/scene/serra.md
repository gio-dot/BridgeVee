---
title: Serra
parent: Scene
nav_order: 12
---

# Serra

Casetta a pareti trasparenti con tetto a serrande (lamelle orientabili), vista isometrica, con piantine dentro e giorno/notte animato. Il quadro in basso ha un orologio (solo lancetta delle ore: si trascina con il mouse, oppure gira da solo con la spunta «Orologio auto»), un cursore della temperatura ambiente (a mano, oppure con andamento casuale) e le spie delle tre fasce orarie e delle quattro soglie di temperatura.

![Serra]({{ site.baseurl }}/assets/scene/serra.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Serrande aperte (finecorsa) |
| I0.1 | Serrande chiuse (finecorsa) |
| I0.2 | Temperatura > 23+1 |
| I0.3 | Temperatura < 23-1 |
| I0.4 | Temperatura < 12-1 |
| I0.5 | Temperatura > 12+1 |
| I0.6 | Fascia oraria 1 (21-9) |
| I0.7 | Fascia oraria 2 (9-12 e 17-21) |
| I1.0 | Fascia oraria 3 (12-17) |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Apri le serrande |
| Q0.1 | Chiudi le serrande |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

Senza PLC la scena esegue da sola la logica descritta qui sotto.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

Le uscite sono a livello: le serrande si muovono finché il comando c'è o fino al finecorsa; con entrambi i comandi insieme non si muovono. Le soglie hanno isteresi di 1 grado: tra le due soglie di una coppia nessuno dei due ingressi è attivo e il PLC deve ricordare l'ultimo comando. Logica da realizzare nel PLC: **fascia 1** sempre chiuso; **fascia 2**: T > 24 apre, T < 22 chiude (in mezzo resta com'è); **fascia 3**: T < 11 chiude, T > 13 apre (in mezzo resta com'è).

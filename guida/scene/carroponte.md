---
title: 0 · Carroponte
parent: Scene
nav_order: 0
---

# 0 · Carroponte

File: `00-carroponte.swf`

Carroponte a cavalletto in vista frontale. Il carrello scorre sulla trave e porta i **due motori**: quello del sollevamento (a sinistra, con il gancio) e quello della traslazione del carrello (a destra, specchiato). Si vede quando girano: nella gabbia della ventola scorrono delle righine. Tra i due motori c'è un blocco grigio con due piccoli led, che si accendono ai finecorsa di salita e di discesa. I finecorsa del carrello (sinistra, centrale e destra) sono sulla trave. Il telecomando è disegnato in basso e ha le quattro frecce, MARCIA (verde) e ARRESTO (fungo rosso). In basso a sinistra, sul pavimento, ci sono i due relè termici **RT1** (motore del sollevamento) e **RT2** (motore del carrello): un clic sulla metà sinistra li fa scattare, sulla metà destra li riarma.

![Carroponte]({{ site.baseurl }}/assets/scene/carroponte.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | SU (a pressione) |
| I0.1 | GIÙ (a pressione) |
| I0.2 | SINISTRA (a pressione) |
| I0.3 | DESTRA (a pressione) |
| I0.4 | ARRESTO (NC: 1 = a riposo, 0 = premuto; fungo bistabile: un clic lo preme, il successivo lo sblocca) |
| I0.5 | MARCIA (a pressione) |
| I0.6 | Relè termico RT1 NO (1 = scattato) |
| I0.7 | Relè termico RT1 NC (0 = scattato) |
| I1.0 | Relè termico RT2 NO (1 = scattato) |
| I1.1 | Relè termico RT2 NC (0 = scattato) |
| I1.2 | Finecorsa salita (NC: 1 = libero, 0 = raggiunto) |
| I1.3 | Finecorsa discesa (NC) |
| I1.4 | Finecorsa carrello a sinistra (NC) |
| I1.5 | Finecorsa carrello a destra (NC) |
| I1.6 | Finecorsa carrello al centro (NC) |

## Uscite (attuatori dal PLC)

Ogni motore ha un comando di **direzione** e un comando di **velocità**.

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Sollevamento SU |
| Q0.1 | Sollevamento GIÙ |
| Q0.2 | Sollevamento LENTO |
| Q0.3 | Sollevamento VELOCE |
| Q0.4 | Carrello a DESTRA |
| Q0.5 | Carrello a SINISTRA |
| Q0.6 | Carrello LENTO |
| Q0.7 | Carrello VELOCE |
| Q1.0 | Spia MARCIA (verde) |
| Q1.1 | Spia ARRESTO (rossa) |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

Senza PLC la scena esegue da sola la logica di un impianto di questo tipo. MARCIA abilita i movimenti e accende la spia verde; ARRESTO li disabilita e accende la spia rossa. Con i movimenti abilitati, le frecce del telecomando muovono gancio e carrello finché sono premute: il movimento parte **lento** e dopo circa un secondo e mezzo di pulsante tenuto diventa **veloce**. Si ferma ai finecorsa e non parte se il relè termico del suo motore è scattato.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

Il telecomando ha solo le quattro frecce: il passaggio da lento a veloce è **a tempo** e lo deve fare il PLC. Le uscite sono a livello: il motore gira se ci sono sia la direzione sia **uno** dei due comandi di velocità. Senza comando di velocità, oppure con LENTO e VELOCE insieme, il motore non gira e la scena avvisa. Lo stesso per SU e GIÙ insieme e per DESTRA e SINISTRA insieme. La velocità lenta è un quarto di quella veloce. Con il relè termico scattato il motore non gira, anche se il PLC lo comanda. I finecorsa sono contatti NC (a 1 quando liberi); se il PLC continua a comandare un motore contro il suo finecorsa, dopo circa un secondo la scena avvisa. Il PLC deve gestire MARCIA e ARRESTO, le spie e i movimenti (per esempio fermarsi al finecorsa centrale, se serve).

### Timer facoltativi

Eventuali timer della scheda dell'esercizio sono facoltativi.

### Velocità

A velocità **4** il gancio, alla velocità veloce del motore, percorre tutta la corsa in circa 4 secondi e il carrello tutta la trave in circa 5 secondi; alla velocità lenta ci mette quattro volte tanto. A velocità più bassa della scena i tempi si allungano in proporzione.
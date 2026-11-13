---
title: 16 · Forno
parent: Scene
nav_order: 16
---

# 16 · Forno

File: `16-forno.swf`

Forno elettrico con tre resistenze (collegamento trifase, protette da fusibili) e tre interruttori termici (Tmin 165 °C, Tmax 225 °C, Tsic 270 °C). Non c'è un motore, quindi non c'è il relè termico. Il quadro a sinistra ha un orologio a 12 ore (si ruota a mano la lancetta delle ore; la lancetta dei minuti la segue; di default segna le 10:10) con la fascia fissa 9:00-18:00 e un led che si accende in fascia, e un cursore verticale che forza a mano la temperatura.

![Forno]({{ site.baseurl }}/assets/scene/forno.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Sonda minima NO (chiuso quando la soglia è raggiunta) |
| I0.1 | Sonda minima NC |
| I0.2 | Sonda massima NO |
| I0.3 | Sonda massima NC |
| I0.4 | Sonda di sicurezza NO |
| I0.5 | Sonda di sicurezza NC |
| I0.6 | Fascia oraria 9:00-18:00 (1 = in fascia) |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Resistenze riscaldanti (contattore) |
| Q0.1 | Spia HB (blu): fascia oraria attiva |
| Q0.2 | Spia HV (verde): resistenze spente |
| Q0.3 | Spia HG (gialla): resistenze in funzione |
| Q0.4 | Spia HR (rossa): intervento dell'interruttore termico Tsic |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

Le resistenze si accendono quando la temperatura scende a Tmin (solo in fascia oraria) e si spengono a Tmax. L'interruttore Tsic le spegne e accende la spia di sicurezza. Senza PLC la scena esegue da sola la logica descritta nella scheda. Fuori dalla fascia oraria le resistenze sono sempre spente.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

Le uscite sono a livello. Le sonde sono attive (NO chiuso, NC aperto) quando la grandezza ha raggiunto la loro soglia. Logica da realizzare nel PLC secondo la scheda dell'esercizio.

### Timer facoltativi

I timer descritti nella scheda dell'esercizio **sono facoltativi**: si possono inserire oppure no, la scena funziona in entrambi i casi. Nella DEMO, dove usa un ritardo, vale al massimo 2,5 secondi (indicativo).

### Velocità

A velocità **4** la grandezza misurata percorre l'intero campo, da 0 a 100 %, in 5 secondi, e lo ripercorre in senso inverso in altri 5 secondi. A velocità più bassa i tempi si allungano in proporzione. I ritardi del PLC non dipendono dalla velocità della scena.
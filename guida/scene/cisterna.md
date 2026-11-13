---
title: 17 · Cisterna
parent: Scene
nav_order: 17
---

# 17 · Cisterna

File: `17-cisterna.swf`

Cisterna da riempire con una pompa azionata da un motore trifase, con consumo d'acqua continuo e tre sonde di livello (Lmin 25 %, Lmax 65 %, Lsic 90 %). Il quadro a sinistra ha un orologio a 12 ore (si ruota a mano la lancetta delle ore; la lancetta dei minuti la segue; di default segna le 10:10) con la fascia fissa 9:00-18:00 e un led che si accende in fascia, e un cursore verticale che forza a mano la grandezza misurata. Il relè termico (clic sulla metà sinistra = scatta, sulla metà destra = si riarma) protegge il motore e invia al PLC un contatto NC.

![Cisterna]({{ site.baseurl }}/assets/scene/cisterna.png)

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
| I0.7 | Relè termico (NC: 1 = ok, 0 = scattato) |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Pompa (contattore del motore) |
| Q0.1 | Spia HB (blu): fascia oraria attiva |
| Q0.2 | Spia HV (verde): spento |
| Q0.3 | Spia HG (gialla): in funzione |
| Q0.4 | Spia HR (rossa): intervento del relè termico |
| Q0.5 | Spia HR (rossa): intervento della sonda di sicurezza |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

La pompa parte quando il livello scende a Lmin (solo in fascia oraria) e si ferma dopo un breve ritardo dal raggiungimento di Lmax. La sonda Lsic arresta la pompa e accende la spia di sicurezza. Se il relè termico scatta il motore non parte: si riarma con un clic sulla metà destra del relè. Senza PLC la scena esegue da sola la logica descritta nella scheda. Fuori dalla fascia oraria il motore è sempre spento.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

Le uscite sono a livello. Le sonde sono attive (NO chiuso, NC aperto) quando la grandezza ha raggiunto la loro soglia. Logica da realizzare nel PLC secondo la scheda dell'esercizio.

### Timer facoltativi

I timer descritti nella scheda dell'esercizio **sono facoltativi**: si possono inserire oppure no, la scena funziona in entrambi i casi. Nella DEMO, dove usa un ritardo, vale al massimo 2,5 secondi (indicativo).

### Velocità

A velocità **4** la grandezza misurata percorre l'intero campo, da 0 a 100 %, in 5 secondi, e lo ripercorre in senso inverso in altri 5 secondi. A velocità più bassa i tempi si allungano in proporzione. I ritardi del PLC non dipendono dalla velocità della scena.
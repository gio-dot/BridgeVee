---
title: Cancello scorrevole
parent: Scene
nav_order: 3
---

# Cancello scorrevole

Vista frontale: un'anta scorre davanti al muro e chiude il passo carraio tra due colonne. Comandi: telecomando a un tasto, chiave a ritorno automatico (apri / chiudi), due finecorsa (sul motore), una fotocellula e un lampeggiante giallo sulla colonna destra. Il motore ha due velocità per verso, quindi i comandi di movimento sono quattro.

![Cancello scorrevole]({{ site.baseurl }}/assets/scene/cancello-scorrevole.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Finecorsa aperto |
| I0.1 | Finecorsa chiuso |
| I0.2 | Fotocellula (1 = libera) |
| I0.3 | Telecomando |
| I0.4 | Chiave: apri |
| I0.5 | Chiave: chiudi |
| I0.6 | Telecomando: apertura pedonale |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Apre veloce |
| Q0.1 | Apre lento |
| Q0.2 | Chiude veloce |
| Q0.3 | Chiude lento |
| Q0.4 | Lampeggiante giallo |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

Senza PLC il cancello apre e chiude da solo (veloce, poi lento verso il finecorsa).

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

L'anta si muove solo con i quattro comandi di movimento (apre/chiude, veloce/lento) e si ferma contro i finecorsa. Il PLC legge il telecomando (impulso), la chiave, i finecorsa e la fotocellula (contatto NC: 1 = libera) e comanda il motore e il lampeggiante. Si può trascinare con il mouse la persona: quando entra nel varco interrompe la fotocellula.

## Note

Nella scena non ci sono testi: le scritte sono solo nel pannello comandi.

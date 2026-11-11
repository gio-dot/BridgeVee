---
title: Linea yogurt
parent: Scene
nav_order: 9
---

# Linea yogurt

Un nastro porta un vasetto dal caricamento alla stazione 1 (riempimento con yogurt e cereali: due valvole e due sensori di livello), poi alla stazione 2 (posizionatore «Chiusura vasetto»); poi torna indietro e un comando di prelievo lo spinge nella cassetta a lato del nastro. Il pannello in basso ha **Start** (NA), **Stop** (NC), **Emergenza** (NC, bistabile) e il **selettore Auto**, più tre spie (arresto, lavorazione, emergenza) comandate dalle uscite Q1.0–Q1.2; il blocco **Reset scena / Velocità** è comune a tutte le scene.

![Linea yogurt]({{ site.baseurl }}/assets/scene/linea-yogurt.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Vasetto presente (inizio nastro) |
| I0.1 | Vasetto in stazione 1 |
| I0.2 | Livello yogurt raggiunto |
| I0.3 | Livello cereali raggiunto |
| I0.4 | Vasetto in stazione 2 |
| I0.5 | Posizionatore in alto |
| I0.6 | Chiusura completa |
| I1.4 | Pulsante Start |
| I1.5 | Pulsante Stop |
| I1.6 | Pulsante di emergenza |
| I1.7 | Selettore Auto |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Carica vasetto |
| Q0.1 | Nastro avanti (verso destra) |
| Q0.2 | Nastro indietro (verso sinistra) |
| Q0.3 | Valvola yogurt |
| Q0.4 | Valvola cereali |
| Q0.5 | Chiusura vasetto |
| Q0.6 | Preleva vasetto |
| Q1.0 | Spia di arresto |
| Q1.1 | Spia lavorazione |
| Q1.2 | Spia di emergenza |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

La scena ripete da sola il ciclo completo: carica il vasetto, lo porta alla stazione 1, riempie, lo porta alla stazione 2, chiude, torna indietro e lo preleva.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

La scena non esegue il ciclo: il nastro si muove solo con i comandi avanti / indietro, le valvole riempiono finché sono aperte (fino ai sensori di livello), il posizionatore chiude con «Chiusura vasetto» e «Preleva vasetto» spinge il vasetto nella cassetta. «Carica vasetto» agisce a fronte di salita. Il PLC deve realizzare la sequenza leggendo i sensori.

## Note

**Sensori trascinabili.** «Vasetto in stazione 1» e «Vasetto in stazione 2» si possono trascinare con il mouse fino a 60 px a sinistra (con un braccetto che li sostiene): serve con i sistemi di controllo lenti, che altrimenti fermano il vasetto troppo avanti. Di partenza stanno contro le colonne di sinistra; doppio clic = posizione standard; la posizione resta memorizzata.

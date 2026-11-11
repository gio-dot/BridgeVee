---
title: Smistamento pacchi
parent: Scene
nav_order: 13
---

# Smistamento pacchi

Due nastri trasportatori e un braccio pick & place a portale, in vista isometrica. Con l'uscita «Eroga pacco» (a fronte di salita) esce un pacco basso o alto dal generatore (riquadro tratteggiato) e il nastro lontano (KM0) lo porta sotto al braccio, dove una fotocellula lo ferma. I pacchi escono a «mazzo»: ogni due, uno alto e uno basso, in ordine casuale. Il braccio scende (Y-Z), la ventosa (Y-VEN) prende il pacco, il braccio risale, avanza in X (Y-X) sul nastro vicino, scende e lascia il pacco; poi risale e torna a riposo. Il nastro vicino porta i pacchi alti a sinistra (KM2) e quelli bassi a destra (KM1) fino agli scivoli. Il pannello in basso ha **Start** (NA), **Stop** (NC), **Emergenza** (NC, bistabile) e il **selettore Auto**, più tre spie (arresto, lavorazione, emergenza) comandate dalle uscite Q1.0–Q1.2; il blocco **Reset scena / Velocità** è comune a tutte le scene.

![Smistamento pacchi]({{ site.baseurl }}/assets/scene/smistamento-pacchi.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Fotocellula: pacco sotto il braccio |
| I0.1 | Braccio X indietro (riposo) |
| I0.2 | Braccio X avanti |
| I0.3 | Braccio Z su |
| I0.4 | Braccio Z giù (fine corsa, senza pacchi) |
| I0.5 | Fotocellula bassa: pacco arrivato |
| I0.6 | Fotocellula alta: pacco alto |
| I0.7 | Ventosa: oggetto |
| I1.4 | Pulsante Start |
| I1.5 | Pulsante Stop |
| I1.6 | Pulsante di emergenza |
| I1.7 | Selettore Auto |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Y-Z braccio giù |
| Q0.1 | Y-X braccio avanti |
| Q0.2 | Y-VEN ventosa |
| Q0.3 | KM0 nastro lontano |
| Q0.4 | KM1 nastro vicino a destra |
| Q0.5 | KM2 nastro vicino a sinistra |
| Q0.6 | Eroga pacco |
| Q1.0 | Spia di arresto |
| Q1.1 | Spia lavorazione |
| Q1.2 | Spia di emergenza |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

La scena esegue da sola i tre cicli (nastro lontano, braccio, nastro vicino) e li ripete: eroga un pacco, lo porta sotto al braccio, il braccio lo sposta sul nastro vicino e il nastro lo manda a sinistra (alto) o a destra (basso) fino agli scivoli.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

Gli attuatori del braccio sono a semplice effetto: uscita a 1 = giù / avanti, a 0 = su / indietro. Il PLC deve realizzare tre cicli semi-indipendenti: **(1)** Start: Eroga pacco (impulso) e KM0 fino alla fotocellula del pacco sotto il braccio. **(2)** Braccio: parte con quella fotocellula; Y-Z giù fino al contatto della ventosa (con un pacco il finecorsa «giù» non scatta), Y-VEN, Y-Z su, Y-X avanti, Y-Z giù fino a «pacco arrivato»: Y-VEN off, Y-Z su, Y-X indietro. **(3)** Nastro vicino: parte con «pacco arrivato» ma solo con il braccio su e la ventosa spenta: KM2 se il pacco è alto, KM1 se è basso, per un tratto poco superiore al percorso più lungo.

La scena tiene conto dei ritardi di CadeSimu: tolto il comando, l'asse Z resta giù ancora 0,7 s, l'asse X resta fuori 0,25 s e la ventosa resta in presa 0,5 s; la ventosa prende subito appena tocca il pacco con il comando attivo; dopo un comando «Eroga pacco» il successivo è accettato solo dopo 2 s. Una barriera fisica ferma il pacco sotto il braccio: se KM0 non viene fermato entro 1 s compare l'anomalia.

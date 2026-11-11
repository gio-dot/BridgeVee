---
title: Smistamento pacchi 2
parent: Scene
nav_order: 14
---

# Smistamento pacchi 2

Come «Smistamento pacchi» (stessi oggetti: due nastri, braccio pick & place, generatore di pacchi), ma qui lo smistamento fra pacchi alti e bassi lo fa il nastro lontano. A metà strada fra il generatore e il punto di presa c'è una fotocellula **alta** (vede solo i pacchi alti); al punto di presa una **sbarra mobile** (tipo passaggio a livello, uscita «APRI SBARRA») e una fotocellula bassa. In fondo al nastro lontano c'è uno scivolo. I pacchi escono a «mazzo»: ogni due, uno alto e uno basso, in ordine casuale. Il pannello in basso ha **Start** (NA), **Stop** (NC), **Emergenza** (NC, bistabile) e il **selettore Auto**, più tre spie (arresto, lavorazione, emergenza) comandate dalle uscite Q1.0–Q1.2; il blocco **Reset scena / Velocità** è comune a tutte le scene.

![Smistamento pacchi 2]({{ site.baseurl }}/assets/scene/smistamento-pacchi-2.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Fotocellula bassa: pacco sotto il braccio |
| I0.1 | Braccio X indietro (riposo) |
| I0.2 | Braccio X avanti |
| I0.3 | Braccio Z su |
| I0.4 | Braccio Z giù (fine corsa, senza pacchi) |
| I0.5 | Nastro vicino: pacco arrivato (fotocellula bassa) |
| I0.6 | Nastro lontano: pacco alto (fotocellula alta) |
| I0.7 | Ventosa: oggetto |
| I1.0 | Sbarra aperta |
| I1.1 | Sbarra chiusa |
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
| Q0.4 | KM1 nastro vicino (verso destra) |
| Q0.5 | Eroga pacco |
| Q0.6 | APRI SBARRA |
| Q1.0 | Spia di arresto |
| Q1.1 | Spia lavorazione |
| Q1.2 | Spia di emergenza |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

La scena esegue da sola i tre cicli e li ripete: eroga un pacco; se è alto la sbarra si apre e il pacco va in fondo al nastro e cade sullo scivolo, poi la sbarra si richiude e il nastro si ferma; se è basso si ferma sotto al braccio, che lo porta sul nastro vicino, dove KM1 lo manda a destra fino allo scivolo.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

Il PLC deve realizzare tre cicli semi-indipendenti. **(1)** Start: Eroga pacco (impulso) e KM0. Con la fotocellula alta attiva (pacco alto): APRI SBARRA finché il pacco è caduto in fondo, poi sbarra chiusa e KM0 fermo; se il pacco è basso: KM0 fino alla fotocellula del pacco sotto il braccio. **(2)** Braccio: come in «Smistamento pacchi» (giù fino al contatto, ventosa, su, avanti, giù fino a «pacco arrivato», lascia, su, indietro). **(3)** Nastro vicino: KM1, solo verso destra, parte con «pacco arrivato» a braccio su e ventosa spenta, per il tempo necessario a far cadere il pacco sullo scivolo di destra.

Come nella scena 1, tolto il comando l'asse Z resta giù 0,7 s, l'asse X resta fuori 0,25 s e la ventosa resta in presa 0,5 s; dopo «Eroga pacco» il successivo è accettato solo dopo 2 s. Con la sbarra chiusa il pacco si ferma contro di essa: se KM0 resta acceso per più di 1 s compare un avviso.

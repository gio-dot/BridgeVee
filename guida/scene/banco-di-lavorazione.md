---
title: Banco di lavorazione
parent: Scene
nav_order: 1
---

# Banco di lavorazione

Banco di foratura in vista isometrica, con tre pistoni (destro, sinistro, centrale) e un mandrino. Tutti gli attuatori sono a semplice effetto: uscita a 1 = avanti (o giù), a 0 = indietro (o su). Il pannello in basso ha **Start** (NA), **Stop** (NC), **Emergenza** (NC, bistabile) e il **selettore Auto**, più tre spie (arresto, lavorazione, emergenza) comandate dalle uscite Q1.0–Q1.2; il blocco **Reset scena / Velocità** è comune a tutte le scene.

![Banco di lavorazione]({{ site.baseurl }}/assets/scene/banco-di-lavorazione.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Pezzo presente |
| I0.1 | Pistone destro arretrato |
| I0.2 | Pistone destro avanti |
| I0.3 | Pistone sinistro arretrato |
| I0.4 | Pistone sinistro avanti |
| I0.5 | Pistone centrale arretrato |
| I0.6 | Pistone centrale avanti |
| I0.7 | Mandrino in alto |
| I1.0 | Fine lavorazione |
| I1.4 | Pulsante Start |
| I1.5 | Pulsante Stop |
| I1.6 | Pulsante di emergenza |
| I1.7 | Selettore Auto |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Carica pezzo |
| Q0.1 | Pistone destro avanti |
| Q0.2 | Pistone sinistro avanti |
| Q0.3 | Mandrino giù (fora) |
| Q0.4 | Pistone centrale avanti |
| Q1.0 | Spia di arresto |
| Q1.1 | Spia lavorazione |
| Q1.2 | Spia di emergenza |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

La scena esegue da sola il ciclo e lo ripete: carica un pezzo, il pistone destro lo porta al centro del banco, il pistone sinistro lo blocca insieme al destro come una morsa, il mandrino scende e fora (dopo 0,8 s di lavoro si attiva «Fine lavorazione»), poi risale, i due pistoni laterali si aprono e il pistone centrale spinge il pezzo lavorato nella cassetta davanti al banco.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

La scena non esegue il ciclo: pistoni e mandrino si muovono solo con le uscite e i sensori seguono la posizione reale. «Carica pezzo» agisce a fronte di salita e fa comparire il pezzo a destra del banco. Il PLC deve realizzare la sequenza descritta sopra, leggendo i finecorsa dei pistoni, il mandrino in alto e la fine lavorazione.

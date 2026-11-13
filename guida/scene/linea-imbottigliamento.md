---
title: 6 · Linea imbottigliamento
parent: Scene
nav_order: 6
---

# 6 · Linea imbottigliamento

File: `06-imbottigliamento.swf`

Linea di imbottigliamento del vino in vista frontale (ispirata al modello Festo «Bottling wine», con grafica, nomi e un sensore in più propri). Un nastro porta le bottiglie (vino rosso = bottiglia scura, vino bianco = bottiglia chiara) davanti a 4 stazioni: riempimento, tappatura, etichetta sul collo, etichetta sul corpo. Le bottiglie entrano da sole a sinistra con colore casuale (il colore cambia al massimo ogni 2 bottiglie) ed escono a destra, dove un sensore segnala la fine della lavorazione. Il pannello in basso ha **Start** (NA), **Stop** (NC), **Emergenza** (NC, bistabile) e il **selettore Auto**, più tre spie (arresto, lavorazione, emergenza) comandate dalle uscite Q1.0–Q1.2; il blocco **Reset scena / Velocità** è comune a tutte le scene.

![Linea imbottigliamento]({{ site.baseurl }}/assets/scene/linea-imbottigliamento.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Bottiglia al dosatore S1 |
| I0.1 | Bottiglia alla pressa S2 |
| I0.2 | Bottiglia al collarino S3 |
| I0.3 | Bottiglia all'etichettatrice S4 |
| I0.4 | Bottiglia scura (rosso) |
| I0.5 | Bottiglia chiara (bianco) |
| I0.6 | Operazione completata |
| I0.7 | Fine linea (bottiglia in uscita) |
| I1.4 | Pulsante Start |
| I1.5 | Pulsante Stop |
| I1.6 | Pulsante di emergenza |
| I1.7 | Selettore Auto |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Dosatore vino rosso |
| Q0.1 | Dosatore vino bianco |
| Q0.2 | Pressa tappo |
| Q0.3 | Collarino rosso |
| Q0.4 | Collarino bianco |
| Q0.5 | Etichetta rosso |
| Q0.6 | Etichetta bianco |
| Q0.7 | Motore nastro |
| Q1.0 | Spia di arresto |
| Q1.1 | Spia lavorazione |
| Q1.2 | Spia di emergenza |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

Senza PLC la linea si comporta come se fosse comandata: lavora le bottiglie presenti nelle stazioni, poi avanza di un passo.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

Il PLC comanda il motore del nastro e le stazioni in base ai sensori: legge il colore della bottiglia (scura o chiara) prima della stazione 1 e sceglie il dosatore e le etichette giuste (rosso o bianco), comanda la pressa del tappo e usa «Operazione completata» e «Fine linea» per far avanzare il nastro.

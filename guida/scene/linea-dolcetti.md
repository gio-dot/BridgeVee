---
title: 8 · Linea dolcetti
parent: Scene
nav_order: 8
---

# 8 · Linea dolcetti

File: `08-linea-dolcetti.swf`

Vista frontale: un pistone verticale che solleva i dolcetti, un erogatore di guarnizione (panna, cioccolato e frutti rossi) e un pistone orizzontale che li spinge su uno scivolo. Gli attuatori sono a semplice effetto: uscita a 1 = su / avanti. Il pannello in basso ha **Start** (NA), **Stop** (NC), **Emergenza** (NC, bistabile) e il **selettore Auto**, più tre spie (arresto, lavorazione, emergenza) comandate dalle uscite Q1.0–Q1.2; il blocco **Reset scena / Velocità** è comune a tutte le scene.

![Linea dolcetti]({{ site.baseurl }}/assets/scene/linea-dolcetti.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Dolcetto presente |
| I0.1 | Pistone verticale giù |
| I0.2 | Pistone verticale su |
| I0.3 | Dolcetto arrivato |
| I0.4 | Pistone orizzontale arretrato |
| I0.5 | Pistone orizzontale avanti |
| I0.6 | Erogazione finita |
| I0.7 | Dolcetto uscito |
| I1.4 | Pulsante Start |
| I1.5 | Pulsante Stop |
| I1.6 | Pulsante di emergenza |
| I1.7 | Selettore Auto |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Carica dolcetto |
| Q0.1 | Pistone verticale su |
| Q0.2 | Pistone orizzontale avanti |
| Q0.3 | Erogatore |
| Q1.0 | Spia di arresto |
| Q1.1 | Spia lavorazione |
| Q1.2 | Spia di emergenza |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

La scena ripete da sola il ciclo: arriva un dolcetto sul nastro, sale sulla testa del pistone verticale, viene sollevato fino al pistone orizzontale, l'erogatore mette la guarnizione e il pistone orizzontale spinge il dolcetto sullo scivolo di sinistra, dove scompare.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

La scena non esegue il ciclo. «Carica dolcetto» agisce a fronte di salita e fa arrivare un dolcetto dal nastro; il pistone verticale lo solleva di mezza corsa (si accende «Dolcetto arrivato» quando è all'altezza del pistone orizzontale), l'erogatore completa la guarnizione («Erogazione finita») e il pistone orizzontale lo spinge sullo scivolo. Il PLC deve realizzare la sequenza leggendo i sensori.

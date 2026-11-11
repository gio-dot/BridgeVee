---
title: Miscelatore
parent: Scene
nav_order: 10
---

# Miscelatore

Grande recipiente cilindrico trasparente (vista isometrica) con due tubi dall'alto che portano i liquidi A e B alle elettrovalvole EV1 ed EV2, resistenza riscaldante e miscelatore a pale sul fondo, scarico con elettrovalvola EV3. Tre sensori di livello (basso, metà, 3/4), un sensore di temperatura (T < 40, T < 60, T > 65 °C) e due sensori (aperta / chiusa) per ciascuna valvola. Il pannello in basso ha **Start** (NA), **Stop** (NC), **Emergenza** (NC, bistabile) e il **selettore Auto**, più tre spie (arresto, lavorazione, emergenza) comandate dalle uscite Q1.0–Q1.2; il blocco **Reset scena / Velocità** è comune a tutte le scene. Nel pannello c'è anche un cursore che forza la temperatura del liquido, per provare le soglie.

![Miscelatore]({{ site.baseurl }}/assets/scene/miscelatore.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Livello basso (>= 2 %) |
| I0.1 | Livello metà |
| I0.2 | Livello 3/4 |
| I0.3 | Temperatura < 40 °C |
| I0.4 | Temperatura < 60 °C |
| I0.5 | Temperatura > 65 °C |
| I0.6 | EV1 aperta |
| I0.7 | EV1 chiusa |
| I1.0 | EV2 aperta |
| I1.1 | EV2 chiusa |
| I1.2 | EV3 aperta |
| I1.3 | EV3 chiusa |
| I1.4 | Pulsante Start |
| I1.5 | Pulsante Stop |
| I1.6 | Pulsante di emergenza |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | EV1 liquido A |
| Q0.1 | EV2 liquido B |
| Q0.2 | EV3 scarico |
| Q0.3 | Motore miscelatore |
| Q0.4 | Resistenza |
| Q1.0 | Spia di arresto |
| Q1.1 | Spia lavorazione |
| Q1.2 | Spia di emergenza |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

Senza PLC la scena esegue da sola il ciclo descritto qui sotto.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

Ciclo da realizzare nel PLC: **Start** → EV1 fino a metà (livello metà), poi resistenza ON; a 40 °C parte il miscelatore; con T > 65 °C si apre EV2 fino al livello 3/4; per 30 s miscelatore ON e temperatura tenuta tra 60 e 65 °C (resistenza ON se T < 60, OFF se T > 65); poi resistenza e miscelatore OFF e, dopo altri 10 s, si apre EV3 fino a recipiente vuoto (livello basso = 0), poi si chiude e il ciclo finisce.

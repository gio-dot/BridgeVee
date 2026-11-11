---
title: Boiler
parent: Scene
nav_order: 2
---

# Boiler

Serbatoio di acqua calda con un'elettrovalvola di ingresso, due sensori di livello fissi, una resistenza riscaldante, due termostati di regolazione a soglia (TMIN e TMAX), un termostato di sicurezza e un termometro analogico e digitale. L'acqua esce con prelievi casuali, regolabili dal pannello. Il pannello ha Start, Stop (NC), Emergenza (NC bistabile), le soglie MAX e MIN (pulsanti − e +, da 0 a 80 °C, TMAX mai sotto TMIN), la frequenza dei prelievi, tre spie e Reset scena.

![Boiler]({{ site.baseurl }}/assets/scene/boiler.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Livello minimo LS1 |
| I0.1 | Livello massimo LS2 |
| I0.2 | Termostato soglia min TMIN (1 = T >= soglia) |
| I0.3 | Termostato soglia max TMAX (1 = T >= soglia) |
| I0.4 | Termostato sicurezza TS (NC) |
| I0.5 | Pulsante Start S1 |
| I0.6 | Pulsante Stop S2 (NC) |
| I0.7 | Emergenza S3 (NC) |
| I1.0 | Livello sicurezza LS0 (resistenza coperta) |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Elettrovalvola ingresso EV1 |
| Q0.1 | Resistenza R1 |
| Q0.2 | Spia resistenza ON |
| Q0.3 | Spia sistema ON |
| Q0.4 | Spia termostato sicurezza |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

Senza PLC il boiler si comporta come se fosse comandato: riempie, scalda con isteresi e accende le spie.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

La scena fa solo da impianto: il livello sale con l'elettrovalvola EV1 aperta, la temperatura sale con la resistenza R1 accesa, l'acqua esce con i prelievi casuali. I termostati TMIN e TMAX sono contatti NA (1 quando la temperatura ha raggiunto la propria soglia) e non hanno isteresi interna: la regolazione si fa nel PLC (si scalda sotto TMIN fino a TMAX). Il termostato di sicurezza (NC) scatta oltre 90 °C e rientra sotto 85 °C; il livello di sicurezza LS0 dice se la resistenza è coperta. Il PLC comanda EV1, la resistenza e le tre spie.

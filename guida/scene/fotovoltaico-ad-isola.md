---
title: 10 · Fotovoltaico ad isola
parent: Scene
nav_order: 10
---

# 10 · Fotovoltaico ad isola

File: `10-fotovoltaico-isola.swf`

Casa vista di fronte (solo di giorno) con il tetto a pannelli e, sulla parete, il quadro dell'inverter aperto (blocco CB, blocco INV e i tre interruttori che si aprono e si chiudono) con la batteria accanto. Il pannello in basso ha l'interruttore magnetotermico generale della rete, un cursore per la carica della batteria (0–100 %) e uno per i consumi della casa (0–4 kW), ciascuno con la spunta «Casuale» per farli variare da soli, e le spie degli 8 segnali verso il PLC.

![Fotovoltaico ad isola]({{ site.baseurl }}/assets/scene/fotovoltaico-ad-isola.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Batteria > 25 % |
| I0.1 | Batteria = 100 % |
| I0.2 | Batteria <= 20 % |
| I0.3 | Batteria <= 90 % |
| I0.4 | Consumo <= 3 kW |
| I0.5 | Consumo > 3,1 kW |
| I0.6 | Batteria <= 5 % |
| I0.7 | Rete KO |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Interruttore CB (carica) |
| Q0.1 | Bypass su rete (0 = su inverter) |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

La scena esegue da sola la logica descritta qui sotto (interruttore CB e bypass), con batteria e consumi che variano.

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

Le uscite sono a livello. La logica da realizzare nel PLC, con isteresi (tra le due soglie si resta come si era): **CB** si chiude con batteria ≤ 90 % e si apre con batteria = 100 %; **bypass** va su RETE con batteria ≤ 20 % oppure consumi > 3,1 kW (se la rete c'è) e torna su INVERTER con batteria > 25 % e consumi ≤ 3 kW, e in ogni caso quando la rete è KO. Tra 3,0 e 3,1 kW nessuno dei due ingressi di consumo è attivo.

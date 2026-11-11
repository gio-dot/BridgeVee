---
title: Incrocio
parent: Scene
nav_order: 6
---

# Incrocio

Incrocio stradale in vista isometrica con due semafori a tre luci (asse A e asse B) e due attraversamenti pedonali sull'asse B, con pulsante di chiamata e semafori pedonali (rosso, verde, verde lampeggiante). Dodici auto arrivano a caso e si adeguano ai semafori: con il rosso si fermano alla linea e fanno coda; con il giallo passano solo se sono troppo vicine per fermarsi. Nella scena restano solo il cursore di velocità e Reset (non c'è il pannello comandi).

![Incrocio]({{ site.baseurl }}/assets/scene/incrocio.png)

## Ingressi (sensori verso il PLC)

| Indirizzo | Descrizione |
|---|---|
| I0.0 | Pulsante chiamata pedoni PP |

## Uscite (attuatori dal PLC)

| Indirizzo | Descrizione |
|---|---|
| Q0.0 | Semaforo A rosso |
| Q0.1 | Semaforo A giallo |
| Q0.2 | Semaforo A verde |
| Q0.3 | Semaforo B rosso |
| Q0.4 | Semaforo B giallo |
| Q0.5 | Semaforo B verde |
| Q0.6 | Pedoni rosso |
| Q0.7 | Pedoni verde |
| Q1.0 | Pedoni verde lampeggiante |

## Come lavora

### In **DEMO** (modalità AUTO, senza PLC collegato)

Senza PLC l'incrocio segue un ciclo fisso: A verde, giallo, B verde, giallo, pedoni se chiamati (con verde lampeggiante finale).

### Comandata da **CadeSimu** o da un **PLC** (EasyPort)

I semafori si comandano solo a tempo dal PLC con le uscite. L'unico ingresso è il pulsante di chiamata pedoni (PP), bistabile: resta a 1 dopo la pressione e si azzera da solo quando si accende il verde pedonale (Q0.7). Le auto reagiscono alle luci che il PLC accende.

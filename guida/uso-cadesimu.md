---
title: Uso con CADeSIMU
parent: Guida
nav_order: 3
---

# Uso con CADeSIMU

Per collegare **CADeSIMU** con le scene di **BridgeVee** facciamo uso delle tabelle di I/O presenti in esso; con queste associamo tutti gli ingressi e uscite presenti in una certa scena  , con contatti, bobine, transizioni o uscite (se usiamo il Grafcet) che andremo a usare nel disegno CADeSIMU.

![Uso con CADeSIMU]({{ site.baseurl }}/assets/uso-cadesimu.png)

- Scegliamo la scena che vogliamo automatizzare in BridgeVee; nel pannello di sinistra vediamo tutti gli ingressi e uscite presenti nella scena.

- Apriamo un nuovo schema CADeSIMU e inseriamo le tabelle di I/O (**punti 1 e 2 in figura**); se la scena prevede più di 8 IN o 8 OUT si possono usare 2 tabelle cambiando l'indirizzo di byte da 0 a 1 nella seconda, come in figura.

- Fare doppio clic sulle tabelle aggiunte e inserire delle sigle che indichino la funzione di ogni I/O facendo riferimento al pannello laterale della scena di BridgeVee (**punto 3 in figura**). Le sigle si possono mettere a piacere (**max 5 caratteri**); il consiglio è che dovrebbero indicare in forma abbreviata cosa fa ogni ingresso o uscita.

- Da ora in poi potrò usare quelle sigle in tutti i contatti e bobine dello schema (o transizioni e uscite se uso il Grafcet) per creare l'automazione necessaria.

- Per avviare la simulazione devo premere la `freccina verde`  in CADeSIMU e il pulsante `Connetti CadeSimu` in BridgeVee (**punti 4 in figura**).
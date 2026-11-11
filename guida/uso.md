---
title: Uso del programma
parent: Guida
nav_order: 2
---

# Uso del programma

## La schermata

- **In alto**: l'elenco delle scene, il pulsante di collegamento (**Connetti EasyPort** o **Connetti CadeSimu**) e l'ingranaggio delle impostazioni.
  Nell'elenco le scene di BridgeVee sono in testa; dopo una linea di separazione, sotto **SCENE FESTO** e in azzurro, ci sono quelle di EasyVeep.

  ![Elenco delle scene]({{ site.baseurl }}/assets/scene/menu-scene.png)

- **Al centro**: la scena. Quelle di BridgeVee hanno in basso un pannello con **Reset scena**, il cursore **Velocità** e la spunta **Vel. dinamica**; molte hanno anche pulsanti, selettori e spie collegati agli ingressi e alle uscite del PLC. In alto a sinistra c'è il numero di versione della scena.
- **A destra**: gli **ingressi** (sensori, verso il PLC) e le **uscite** (attuatori, dal PLC) con i loro nomi. Una pallina verde significa "attivo". Si allarga o si stringe la colonna trascinando la barretta a sinistra; con un doppio clic torna alla larghezza standard.

![Ingressi e uscite]({{ site.baseurl }}/assets/scene/riquadro-io.png)

## Senza PLC: DEMO, AUTO, MANUALE

Senza PLC collegato compaiono in alto **DEMO**, **AUTO** e **MANUALE**.

- **AUTO**: la scena esegue da sola la sua logica. Le spie delle uscite a destra mostrano i comandi che sta dando.
- **MANUALE**: la demo si ferma e puoi fare clic sulle uscite per attivarle o spegnerle a mano e vedere la scena muoversi.
- Premendo di nuovo **AUTO** la scena riparte dall'inizio.

## Con un PLC

1. Apri le **Impostazioni** (l'ingranaggio) e scegli la sorgente: **EasyPort** o **CadeSimu** (si cambia solo da scollegati).
2. Premi il pulsante verde **Connetti...** in alto. Da quel momento le uscite le comanda il PLC e la demo si ferma.
3. Per scollegarti premi **Disconnetti**.

**EasyPort**: collega la scheda al PC con il cavo USB e scegli la porta quando richiesto.

**CadeSimu**: avvia CADe_SIMU e fai partire la simulazione. Mentre BridgeVee è collegato usa gli **appunti di Windows**: non copiare e incollare altro. Lascia visibile la finestra di BridgeVee, affiancata a CADe_SIMU e non nascosta dietro.

## Velocità e PC lenti

- **Velocità** (0,5 / 1 / 2 / 3 / 4): rallenta nastri, carrelli e cancelli. 4 è la velocità originale, **1 (predefinito) un quarto**. Utile con i PC lenti o con sistemi di controllo lenti.
- **Vel. dinamica**: gli oggetti vanno a velocità piena e rallentano al livello scelto solo vicino ai sensori.
- Le scelte restano memorizzate per ogni scena.
- **Filtro uscite CadeSimu** (in fondo alla colonna ingressi/uscite, per ogni scena): con la spunta **Default** tutto funziona come al solito. Se su un PC lento le uscite hanno dei "buchi" (si spengono e si riaccendono per un istante), togli la spunta e scrivi un tempo in millisecondi, da 40 a 2000 (per esempio 150): uno spegnimento arriva alla scena solo se dura almeno quel tempo. Le accensioni non vengono ritardate.
- Alcune scene hanno sensori **trascinabili con il mouse** (per esempio Linea yogurt e Centro di lavorazione) per compensare il ritardo dei sistemi di controllo lenti: i dettagli sono nelle pagine delle scene. Un doppio clic sul sensore lo riporta alla posizione standard.

## Impostazioni

L'ingranaggio in alto a destra apre il pannello delle impostazioni.

![Impostazioni]({{ site.baseurl }}/assets/scene/impostazioni.png)

- **Collegamento I/O**: EasyPort o CadeSimu (si cambia solo da scollegati).
- **Cartella dei modelli (flash)**: la cartella `flash` di EasyVeep (**Cambia cartella...**). Viene ricordata.
- **Scene aggiunte a mano**: **Apri cartella**, copia lì i file `.swf` e premi **Aggiorna elenco**.
- **Aggiornamenti**: **Cerca** per controllare a mano scene e programma.
- **Lingua dei nomi** dei sensori e delle uscite: quelli originali dei modelli Festo (senza italiano) e i nostri modelli (anche in italiano); dove la lingua manca si usa l'inglese.
- **Diagnostica**: **Mostra il log** e **Mostra il log del server**, utili solo per chi deve capire un problema.
- **Server**: **Esci** ferma il programma.
- **Informazioni**: i numeri di versione di Scene e Core.

Per chiudere BridgeVee basta chiudere la sua finestra: il resto si ferma da solo.
## Se qualcosa non va

- **L'elenco delle scene Festo è vuoto**: apri Impostazioni → **Cambia cartella...** e scegli la cartella `flash` di EasyVeep.
- **La scena si ferma o va a scatti**: non minimizzare la finestra e non coprirla del tutto con altre finestre.
- **Con CadeSimu le uscite hanno dei buchi o i movimenti si interrompono**: abbassa la velocità e prova il filtro uscite (vedi sopra).
- **Un antivirus o i criteri aziendali bloccano il programma**: chiedi aiuto all'amministratore del computer.
---
title: Installazione e aggiornamenti
parent: Guida
nav_order: 1
---

# Installazione e aggiornamenti

## Requisiti

- Windows 10 o 11 (64 bit).
- Per i modelli Festo: l'installazione di **EasyVeep 2** sullo stesso computer (facoltativa). BridgeVee non contiene i modelli Festo, legge quelli già presenti nella cartella `flash` di EasyVeep. Le scene di BridgeVee sono incluse e non richiedono EasyVeep.
- Per collegare un PLC reale: scheda **EasyPort** con cavo USB (e il suo driver USB), oppure **CADe_SIMU**.

## Installazione

1. Vai alla pagina delle [Releases](https://github.com/gio-dot/BridgeVee/releases), cerca la versione `core-vx.x.x` più alta e in **Assets** scarica `BridgeVee-Setup-x.x.x.exe`. Non serve scaricare il pacchetto scene: è incluso nel Setup.
2. Esegui il file scaricato e scegli se installare **solo per te** (non serve la password di amministratore) o **per tutti gli utenti** (serve).
3. Avvia BridgeVee dall'icona sul Desktop o dal menu Start.

{: .note }
**Avviso di Windows.** Il programma non ha una firma digitale a pagamento, quindi Windows (SmartScreen) può mostrare "Windows ha protetto il PC". Premi **Ulteriori informazioni** e poi **Esegui comunque**.

## Scene di EasyVeep

Se sul PC c'è **Festo EasyVeep**, le sue scene compaiono da sole nell'elenco, sotto l'intestazione "SCENE FESTO". Se non vengono trovate, apri le **Impostazioni** (l'ingranaggio in alto a destra), premi **Cambia cartella...** e scegli la cartella `flash` di EasyVeep (di solito `C:\Program Files (x86)\didactic\EasyVeep 2\flash`). La scelta resta memorizzata.

## Aggiornamenti

All'apertura BridgeVee controlla (serve internet) se ci sono novità, e se ci sono lo segnala in alto con un avviso:

- **Scene nuove o corrette**: premi **Aggiorna** nell'avviso. Si scaricano solo le scene cambiate e si applicano subito.
- **Nuova versione del programma (Core)**: il programma propone di scaricarla e di installarla; BridgeVee si chiude, si aggiorna e si riapre da solo.

Puoi controllare anche a mano da **Impostazioni → Aggiornamenti**.

Il titolo della finestra mostra due numeri indipendenti: **Scene** (per esempio `2026.11.6`, cresce a ogni aggiornamento del pacchetto scene) e **Core** (il numero del programma di base).

## Scene aggiunte a mano

Altri file `.swf` si possono copiare nella cartella `%APPDATA%\BridgeVee\MyScenes` (Impostazioni → *Scene aggiunte a mano* → *Apri cartella*). Compaiono nell'elenco dopo **Aggiorna elenco**.
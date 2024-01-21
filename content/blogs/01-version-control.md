---
title: "Controllo di versione del Software"
date: 2024-01-21T23:15:00+07:00
slug: controllo-di-versione-del-software
category: sviluppo software
summary:
description: 
cover:
  image: 
  alt: 
  caption: 
  relative: true
showtoc: true
draft: false
---
# Introduzione
Benvenuti, in questo articolo parleremo del controllo di versione del software. Ci tengo a precisare che questo sarà un articolo di "alto livello", ossia non scenderò nel tecnico dei comandi specifici o di come si utilizza il controllo di versione del software, ma cercherò di rispondere alla domanda: cos'è e a cosa serve il version control? Sebbene questa domanda possa sembrare banale per chi ha un forte background informatico e si occupa, quotidianamente, dello sviluppo software, potrebbe non essere altrettanto per coloro che di mestiere non sono sviluppatori ma che, per curiosità o necessità, hanno scritto del codice nonostante non fosse la loro attività principale. Vedremo come questo sia uno strumento relativamente semplice, da imparare e da utilizzare, e che può, anzi deve essere integrato nella nostra normale di routine di progettazione. Il consiglio che vi dò è, se non lo sapete già usare, di imparare a farlo il prima possibile, in quanto si rivelerà uno strumento indispensabile e d'aiuto. 
# Cos'è il controllo di versione del Software
Da un punto di vista generale, il controllo di versione del software consiste in un sistema che tiene traccia del cambiamento di un determinato file durante il tempo. Quindi, con il version control, abbiamo uno strumento in grado di mostrarci tutta l'evoluzione temporale di un determinato file. Questo ovviamente non si limita a soltanto un singolo file, ma può essere fatto su un gruppo di file. Spesso e volentieri, durante lo sviluppo di un progetto x, avremo una cartella che conterrà tutti i file sorgenti di progetto, se stiamo parlando di sviluppo software. Bene, sottoponendo la cartella principale, la radice, a controllo di versione, potremo tracciare tutti i cambiamenti dei singoli file che effettuiamo durante lo sviluppo. E se avete mai sviluppato del codice, software o firmware che sia, avrete ben presente quante volte si effettuano cambiamenti ad un singolo file sorgente. D'altronde la progettazione, informatica, elettronica o meccanica, è un processo iterativo. Si parte dal foglio bianco e, tramite iterazioni successive, si arriverà ad un primo prototipo del prodotto/sistema. Raramente si arriva ad una soluzione definitiva, finale e robusta, senza effettuare n iterazioni in mezzo. 

Quindi, ritornando al version control, avremo tutta la storia temporale dei nostri sorgenti, proprio come se fosse un grafico di una serie temporale che ne mostra l'evoluzione nel tempo. Quindi, la prima cosa da fare è versionare il nostro intero progetto e, non appena introdurremo delle modifiche significative all'interno dei nostri file, ecco che lo segnaleremo al sistema di versione in modo che lui possa tenerne traccia. Il funzionamento è del tutto analogo ad un diario, infatti interagiremo con il version control tramite dei semplicissimi messaggi, in cui descriveremo ciò che è stato introdotto dall'ultima versione a quella corrente che sto caricando. Immaginiamo quindi un software che è stato sviluppato da zero e che è arrivato ad una versione stabile in 6 mesi. Questo progetto ci ha richiesto quindi 6 mesi di tempo di lavoro full time. Ora, se avessimo trackato in modo rigoroso il nostro sviluppo, riusciremo a vedere ciò che abbiamo fatto in questi 6 mesi, quando lo abbiamo fatto e quanto tempo ci abbiamo impiegato. Questo può essere utile sia per tornare indietro nel tempo, ad una versione meno recente del software ma anche per un altro motivo, meno tecnico. Spesso, prima di partire a progettare, è necessario effettuare una stima dei tempi che ci potremmo impiegare per completare il progetto. Spoiler: nessuno sa con precisione quanto ci metterete, la progettazione è piena di insidie e, anche un dettaglio apparentemente irrilevante può richiedere ore, se non giorni di sviluppo. Ora immaginate di avere un po' di anni di esperienza e di aver trackato rigorosamente i vostri progetti nel tempo. Ora avrete accesso a dati reali, ossia sapete esattamente quanto tempo ci avete messo sia per completare gli interi progetti ma anche le singole feature all'interno dei progetti. Questo può dare una grossa mano nello stimare i tempi di un progetto futuro. Ora, chiaramente un progetto è diverso dall'altro e ha le sue caratteristiche, però spesso alcuni pattern si ripetono e sapere quanto ci ho impiegato in passato a risolvere un problema simile può essere una stima più accurata rispetto ad una stima grossolana basata semplicemente sull'esperienza e le sensazioni personali. 
# Git
Git è uno dei software più famosi per il version control. La prima versione di Git, in accordo con Wikipedia, risale al 7 Aprile 2005. Non esiste soltanto Git, ne esistono altri, però parliamo di questo in quanto è uno dei più diffusi. 

Git è quindi un software che scarichiamo fisicamente sul nostro PC ([qui il link](https://www.git-scm.com/downloads)) e che poi utilizzeremo sui nostri progetti. Git possiamo usarlo sia tramite interfaccia grafica che tramite riga di comando. Saper utilizzare git da riga di comando implica sicuramente il saperlo utilizzare anche tramite interfaccia grafica, ma non vale il viceversa. Ci sono anche dei software come GitExtensions ([qui il link](https://github.com/gitextensions/gitextensions/releases/tag/v4.2.1)) i quali, tramite un interfaccia grafica, permettono di utilizzare git nella sua interezza. 

Tramite questi software, che sia la git bash, la git GUI o altri software esterni, possiamo effettuare il discorso che facevamo prima, ossia, periodicamente, segnalare a git che il nostro progetto è arrivato ad un determinato stato di avanzamento. Poi, tramite opportuni comandi, avremo modo di rileggere tutta la storia temporale del nostro progetto. 

Alcuni IDE, come Qt Creator o Visual Studio, hanno la possibilità di integrare git al loro interno e utilizzare il version control direttamente all'interno dell'IDE, senza la necessità di software aggiuntivi. 

spiegare un po' cos'è git, a grandi linee. Utilizzo a riga di comando o GitExtension. Integrazione in Qt Creator e Visual Studio. 

# Server 
discorso Github e bitbucket per

# Quando usare il controllo di versione
fare gli esempi di sviluppo software personale o da solo
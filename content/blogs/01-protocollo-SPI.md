---
title: "Il Protocollo SPI"
date: 2024-01-28T23:15:00+07:00
slug: protocollo-SPI
category: progettazione elettronica
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

# Il protcollo SPI

### Introduzione
Benvenuti!

In questo articolo parleremo del protocollo di comunicazione SPI (Serial Pheripheral Interface). L'SPI è definita come un'interfaccia sincrona full-duplex. Svisceriamo i termini uno per uno per capire di cosa si tratta. 

Per interfaccia sincrona, a livello generale, si intende un protocollo in cui il segnale di clock viene condiviso tra i dispositivi che devono parlare tra di loro. Quindi l'SPI, avendo un pin fisico di clock (SCLK) è un protocollo di comunicazione sincrono. Lo stesso vale per il protocollo I2C, in quanto ha la linea di clock (SCK) e la linea dati (SDA). Ciò non vale per l'UART, in quanto ha soltanto RX e TX. Nei protocolli sincroni il clock viene utilizzato per sincronizzare i vari dispositivi collegati al bus, e permettere loro di campionare il dato, sulla linea dati, nell'istante corretto. 

Con il termine full-duplex indichiamo il fatto che l'SPI può ricevere e trasmettere contemporaneamente dati. Infatti, come vedremo meglio nel seguito, abbiamo due linee fisiche distinte per la trasmissione e ricezione dati, MOSI e MISO. Quindi il controller mentre trasmette sulla linea MOSI può ricevere dati sull'altra linea MISO. Parliamo di controller perchè l'SPI ha un meccanismo in cui vi è un master che fa da direttore di orchestra per tutti i dispositivi collegati al bus. Utilizzeremo il termine dispositivo, nodo o periferica in modo intercambiabile, per indicare un componente connesso fisicamente al bus SPI. 

Inoltre l'SPI è un protocollo di comunicazione seriale, il che significa che i dati vengono trasmessi in modo seriale appunto su un'unica linea, uno dopo l'altro, sincronizzati dal clock:

![Comunicazione seriale](/static/images/seriale.png)

*Comunicazione Seriale*

Nella comunicazione parallela i bit vengono mandati contemporaneamente su n linee diverse:

![Comunicazione parallela](/static/images/parallela.png)

*Comunicazione Parallela*

Il caso tipico di comunicazione SPI è quello tra microcontrollore e sensore, in cui il micro funge da master e il sensore da dispositivo collegato al bus SPI. 

### SPI a 4 fili
Fisicamente l'SPI ha 4 pin fisici. Esiste anche la versione a 3 fili, però in questo caso considereremo quella più comune, con le linee di Chip Select (CS o SS), clock (SCLK), Master Output Slave Input (MOSI), Master Input Slave Output (MISO):

![SPI a 4 fili](/static/images//spi-4-wire.png)

*SPI a 4 fili*

Il pin di Chip Select si dice essere un segnale active-low. Questo significa che normalmente questo è un segnale alto e, non appena diventa basso il dispositivo viene collegato. In particolare, consideriamo lo scenario dell'immagine sopra in cui abbiamo un master ed un nodo collegato al bus SPI. Il pin CS del master è collegato fisicamente al pin CS della periferica. Questo pin sarà normalmente a livello logico alto, quando non ci sarà comunicazione. Non appena si vorrà effettuare una comunicazione, il master inizierà a generare il segnale di clock e forzerà basso il pin di CS. In questo modo, lo slave, leggendo il pin di CS e vedendo che esso da alto è diventato basso, saprà che il master ha iniziato una comunicazione e che vuole parlare proprio con lui. Approfondiremo nel seguito il caso in cui ci siano più di un dispositivo collegato al bus SPI. Quindi, in definitiva, il pin di CS viene forzato basso dal master non appena viene iniziata una comunicazione. Passiamo ora al secondo pin, il clock (SCLK). 

Il pin SCLK è collegato fisicamente al pin SCLK del nodo o dei nodi. Su questa linea il master genererà il clock, che permetterà al dispositivo con cui sta parlando di sincronizzarsi. Ricordiamo infatti che l'SPI è un protocollo di comunicazione sincrono, per cui abbiamo un segnale di clock comune tra i due dispositivi che si parlano. Il master può decidere due caratteristiche del clock:

* il suo stato di idle (CPOL, Clock Polarity)
* su quale fronte campionare il dato (CPHA, Clock Phase)

lo stato del clock può essere o alto o basso, il fronte può essere di salita o di discesa, per cui nascono quattro combinazioni a seconda di questi valori, ossia i 4 modi in cui può operare l'SPI:

// tabella modi SPI

Lo stato di idle indica lo stato del clock quando non sta comunicando. Quindi a riposo, il clock può essere alto o basso, a seconda di come impostiamo il CPOL, se a 1 o a 0. Con il chip select impostato come active-low signal avremo che lo stato di idle del clock sarà delimitato a quei casi in cui il pin CS sarà alto, in quanto quando sarà basso significa che stiamo comunicando sul bus SPI. Con il CPHA indichiamo invece su quale fronte del clock il ricevitore dovrà campionare il dato. Possiamo impostare che il ricevitore campioni il dato sul fronte di salita o sul fronte di discesa del clock. Attenzione che il termine ricevitore non è sinonimo di dispositivo collegato al bus SPI, in quanto anche il master può essere un ricevitore, in quanto può ricevere dati sulla linea MISO. 

CS: active low
CPOL e CPHA: modi SPI, velocità comunicazione
MOSI
MISO

Necessità di sapere quando ricevo i dati dallo slave. 

### Comunicazione con n nodi


### Conclusione


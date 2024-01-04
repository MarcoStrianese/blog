# STM32 HAL Library
L'ecosistema STMCube permette allo sviluppatore di concentrarsi sul layer applicativo, utilizzando i driver di bassi livello per controllare l'hardware forniti direttamente dalla ST. 

## STM32 HAL Library Drivers
Le HAL sono disponibili per qualsiasi periferica hardware presente nei microcontrollori ST. Inoltre, sono portabili, il che significa che se sviluppo un firmware con, ad esempio, il microcontrollore della famiglia G4 allora, quel firmware, potrà girare su tutti i microcontrollori si quella famiglia e, forse, anche su microcontrollori di altre famiglie, come F4. È dichiarato così dall'ST, da verificare realmente com'è questo porting, sporcandosi le mani. 

Oltre alle HAL, ci sono delle Low Layer API (LL API), le quali sono più vicine all'hardware e quindi più veloci ed ottimizzate rispetto alle HAL. Le LL API non sono disponibili per tutte le periferiche hardware. Le LL API sono meno portabili, anzi non lo sono quasi per niente, in quanto sono driver a livello dei registri del microcontrollore. Quindi, per usare le LL API, è necessario anche entrare nel dettaglio dell'hardware dello specifico microcontrollore e sapere cosa c'è effettivamente dentro. Il codice sorgente delle HAL e delle LL è scritto in C. 

# STM32 GPIO Tutorial
## STM32 GPIO Ports
Per configurare le general purpose input output porte è necessario andare a settare valori opportuni nei registri di configurazione delle porte. Le porte hanno diversi registri, tutti a 32 bit, che permettono di configurare le porte e i singoli GPIO. Ogni GPIO, al suo interno, ha la possibilità di essere messo in pull-up o pull-down tramite un flag, il quale si tradurrà fisicamente in un interruttore che chiuderà un circuito che metterà il pin a VDD o GND, con relativa resistenza. Può essere settato come input o output. È importante notare come, qualsiasi configurazione del GPIO diamo via software, si traduca in un cambiamento effettivo del circuito all'intero del GPIO. Se impostiamo un GPIO come output allora stiamo abilitando un certo circuito interno. Se lo impostiamo come input invece un altro. Tutti i GPIO, se non specificato chiaramente, lavorano a 3.3 V. Quindi non possiamo collegare un input a 5 V direttamente su un GPIO, ma è necessario un level shifter. La massima corrente che può erogare o ricevere un GPIO è di 25 mA; fare comunque riferimento al datasheet del microcontrollore di interesse. 

## STM32 GPIO Speed
### Input Mode
Quando il GPIO è settato come input mode, l'input viene campionato ogni ciclo di clock dell'APB2. Questo significa che la frequenza di campionamento del GPIO coincide con la frequenza dell'APB2. 
### Output Mode
In output mode, la velocità del GPIO è configurabile. Questo, come ogni cosa, si traduce nel programmare i rispettivi bit nel registro di configurazione del GPIO di interesse. In genere la velocità di un output GPIO può variare tra 4 livelli, ad esempio 10 MHz, 50 MHz, 100 MHz e 180 MHz. 

## External Interrupts
Tutte le porte hanno possibilità di gestire interrupt. Per fare questo dobbiamo configurare la porta in input mode. 

## Locking Mechanism
Il meccanismo di bloccaggio permette di congelare una configurazione di una porta. Dopo essere stata configurata, la porta non è più modificabile, se no dopo un reset. 

## GPIO Configurations
Un GPIO in output può essere configurato come output Open-Drain o output Push-Pull. Un GPIO in input può essere configurato come input messo a pull-up, pull-down o ingresso ad alta impedenza. Se non settiamo un GPIO in input come pull up o pull down esso verrà settato automaticamente, di default, come ingresso ad alta impedenza. 

# STM32 Interrupts Tutorial | NVIC & EXTI
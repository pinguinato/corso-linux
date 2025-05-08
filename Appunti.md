# Corso Linux per certificazione LPIC-1

Famiglie principali di distribuzioni Linux
- Debian / Ubuntu / Mint --> pacchetti DEB
- Red Hat / Fedora / Centos --> pacchetti RPM
- Arc --> Pacman

## Gli Interrupts in Linux

### /proc/interrupts

Le periferiche, le porte parallele, le tastiere ... comunicano con il sistema operativo attraverso degli **interrupts**.  Mandano degli impulsi di interruzione al processore fisico, facendogli capire che così stanno interagendo con esso. In Linux possiamo vedere gli interrupts in uso consultando un file chiamato **/proc/interrupts**.

Esempio di uso: 

        cat /proc/interrupts

Questo file viene rigenerato all'avvio del sistema. Ogni volta che lo richiamo, ad esempio se guardo l'interrupts della tastiera **i8042** cambierà di valore.
Non è un file persistente nel file system, viene generato ad ogni avvio. In questo file vengono elencate le seguenti informazioni in colonna:
- processori
- tipologia di interrupts
- numero di volete che l'interrupts ha interagito con il processore

### /proc/ioports

Esempio di uso:

        cat /proc/ioports

All'interno di questo file vediamo ogni dispositivo e il suo corrispettivo spazio in memoria. Una volta che un dispositivo ha mandato 
l'interrupt alla CPU, la CPU deve mediare il trasferimento di dati tra la periferica e la memoria e questo è lo scopo delle IO ports, 
cioè fornire ad un device un range di memoria in cui possa essere assegnato. 

Esempio:


        0000-0000 : dma1
        0000-0000 : pic1
        0000-0000 : timer0
        0000-0000 : timer1

Ognuno di questi indirizzi in memoria non deve essere condivisibile con altri. Sono riservati, altrimenti ci sarebbero dei 
grossi problemi di conflitto.



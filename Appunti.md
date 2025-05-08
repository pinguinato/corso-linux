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


## Dispositivi e drivers

- Dispositivi cold plug: vanno collegati e scollegati dal computer quando è spento (schede video...)
- Dispositivi hto plug: si possono collegare anche a computer acceso (pennette usb, mouse usb, tastiere...)

In linux possiamo vedere un elenco di questi dispositivi con il comando:

                lspci

Esempio:

                00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
                00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (rev 07)
                00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 08)
                00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)

Qui si vede indirizzo PCI a cui è collegato ed il nome della periferica.

Si può visualizzare con struttura ad albero con il comando:


                lspci -t

                lspci -tv

**Importante** dal kernel 2.6 i device vengono creati dinamicamente. Esempio: la cartella /dev dove stanno i device, se diamo il comando ls /dev/sd? per avere l'elenco dei device sotto dev che iniziano per sd...

Con il comando:

                lsmod 

Vediamo tutti i driver che sono stati caricati.

Per rimuovere un driver:

                rmmod nome-driver

Si può soltanto se si è amministratori del sistema!

Per aggiungere un driver in memoria:

                insmod percorso/completo/del/driver/sul-filesystem

Ma come facciamo a trovarlo???

Tutti i driver/moduli in Linux si trovano sotto il percorso **/lib/modules**, entriamo dentro la versione del kernel attuale ecc...

Oppure possiamo usare la funzione **find**

                find /lib/modules/$(uname -r)/ -iname "*pcrspkr*.ko*"

Una volta trovato il percorso completo possiamo usare il comando **insmod** con il percorso completo per installare di nuovo correttamente il driver.
Per superare l'esame di certificazione bisogna saper usare rmmod e insmod, però è più semplice usare il 
comando:

                modprobe -r pcspkr

per rimuovere, e poi:

                modprobe pcspkr

per ricaricarlo in memoria, il che è più semplice e flessibile da usare. Usare però insmod è più 
immediato per caricare da un percorso diverso il mio modulo custom.





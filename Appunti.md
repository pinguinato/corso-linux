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





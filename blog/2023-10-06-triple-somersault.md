---
authors: pieroproietti
slug: triple-somersault
title: "Triple somersault!"
lang: it
enableComments: true
---
import Translactions from '@site/src/components/Translactions';

<Translactions />

# Triplo salto mortale!

Una volta creato e testato eggs per l'architettura [ARM64](https://developer.arm.com/Architectures/A64%20Instruction%20Set%20Architecture), abbiamo il problema di provarlo su hardware reale.

Non essendo un esperto del caso, ho chiesto assistenza a chi conosce meglio, specificatamente al buon Jon West di [BlissOS](https://blissos.org/) ed al "solito" Stefano Capitali di [Manjaro](https://manjaro.org/), che mi ha poi re-indirizzato a Furkan che si occupa delle versioni ARM per Manjaro stesso.

Jon mi ha avvisato che, per quanto di sua conoscenza, i dispositivi ARM64 utilizzano soprattutto [uboot](https://u-boot.readthedocs.io/en/latest/) come bootloader al posto di GRUB, Furkan mi ha allargato un po' di più la prospettiva spiegandomi che esistono diverse versioni di Manjaro ognuna per degli specifici dispositivi e che, non tutti i dispositivi ARM sono compatibili UEFI, ma alcuni si: dai grandi sistemi come [Ampere](https://amperecomputing.com/products/processors), a sistemi anche molto piccoli il [rockpro64](https://www.pine64.org/rockpro64/) di pine64, o il [rock64](https://wiki.radxa.com/Rock4) di radxa, entrambi con il rockchip [rk3399](http://rockchip.wikidot.com/rk3399).

Ho continuato quindi a documentarmi e mi sono imbattuto in [Raspberry Pi 4 UEFI Firmware Images](https://github.com/pftf/RPi4), che - nello specifico - fa proprio il caso nostro in quanto consente di avviare RPI4 con UEFI e, sembra da USB come specificato nell'articolo [ESXi on ARM - Installing ESXi on a Raspberry Pi](https://rudimartinsen.com/2020/10/07/esxi-on-arm-fling-install-on-rpi/) in bibliografia.

Disponendo quindi di un abbastanza datato RPI4 - forse con 8 GB di RAM - mi sto accingendo a prepararmi al grande salto.

## Installazione
Scarica l'ultimo archivio dalla repository Releases.

Crea un SD card o un disco USB, con almeno una partizione formattata come FAT16 o FAT32

Nota: Avviando da USB o da ESP richiede un versione di PI EEPROM recente (così come una versione del firmware UEFI). Se state utilizzando l'ultima versione del firmware UEFI e trovate che il boot da USB o da ESP non si avvia, visitate https://github.com/raspberrypi/rpi-eeprom/releases per aggiornare la vostra EEPROM.

Estraete tutti i file dell'archivio nella partizione che avete creato precedentemente.

Notate che - a parte questo README.md, che potete rimuovere liberamente - non dovete cambiare assolutamente i nomi dei file e delle directory estratte.

## Utilizzo
Inserita la card SD accesa la vostra Raspberry Pi, dovreste vedere uno schermo multicolore (che indica che il bootloaded embedded sta leggendo i dati dalla partizione SB/USB) quindi, appare il logo Raspberry in bianco e nero una volta che il firmware UEFI è prondo.

A questo punto, potete premere il tasto ESC per entrare nel setup, F1 per lanciare la shell UEFI e - se fornito - avere un bootloader UEFI in `efi/bootaa64.efi`` che potete avviare (sarà il vostro default se non verrà intrapresa alcuna azione)

![uefi boot](https://www.bujarra.com/wp-content/uploads/2020/10/VMware-ESXi-Raspberry-Pi-06.jpg)

## Metodo
Ho scritto questa parte ancora prima di provarla. L'ho fatto presso il negozio [DNetware computer](http://www.dnetware.com/) di Tor Sapienza a Roma, su un missile i9 per gamer in preparazione ed una chiavetta USB con adattatore per SD card.

### Create an msdos partition table
* `sudo parted --script /dev/sdb mklabel msdos`

### Create, format, and label a 10M fat32 partition
* `sudo parted --script /dev/sdb mkpart primary fat32 0% 10M`
* `sudo mkfs.vfat /dev/sdb1`
* `sudo fatlabel /dev/sdb1 RPI-FW`

### Get the UEFI firmware onto the SD card
* `sudo mount /dev/sdb1 /mnt/`
* Download from [RPi4 UEFI Firmware](https://github.com/pftf/RPi4/releases)
* `sudo unzip Downloads/RPi4_UEFI_Firmware_v1.35.zip -d /mnt/`
* `sudo umount /mnt/`

A questo punto la card SD può essere usata per avviare la RPi e vi troverete nel firmware UEFI.

Non resta che creare la chiavetta con la normale procedura descritta nella [guida](https://www.debian.org/releases/bookworm/arm64/ch04s03.en.html).

## Funziona!
Oggi, con l'aiuto dell'amico Walter di [DNetware computer](https://www.facebook.com/DnetwareComputer/), finalmente ho avuto il "coraggio" di aprire il minicase del mio Raspberry ed effettuare la prova.

Abbiamo semplicemente formattato tutta la SD card con fat32 direttamente da uno dei computer Windows in costruzione, quindi - effettuato il download del firmware - il contenuto è stato decompresso nell'unica partizione creata: una SD è da 16GB. In effetti sarebbero bastati pochi Kb per il firmware.

A questo punto ho avviato il Raspberry che, correttamente, ha riconosciuto la chiavetta USB sulla quale avevo posto la ISO del sistema operativo e, con soddisfazione il piccolo s'è avviato.

Dopo un tentativo, non riuscito di installazione, ho effettuato nuovamente una ulteriore prova, Questa volta, però, il boot è stato effettuato da un disco SSD da 128 GB, sempre formattato con fat32, sul quale avevo installato [ventoy](https://www.ventoy.net/en/index.html). Anche in questo caso il disco è stato riconosciuto correttamente, ventoy ha creato la lista delle ISO disponibili e, selezionata `egg-of-debian-bookworm-arm64` il sistema si è avviato correttamente.

La soddisfazione è enorme: `eggs` riesce a rimasterizzare buona parte delle distribuzioni Linux e su tre architetture di processore diverse: amd64, i386 ed adesso anche arm64.

L'utilità - al momento - è ancora poca, e manca infine l'installazione su Raspberry ed ARM in genere, ma ormai è questione di tempo e di test.

Ringrazio molto l'amico Walter, ed attendo notizie su eventuali repliche, vero [Franco Conidi](https://francoconidi.it/)?

![El “salto de la muerte” de la gimnasia que teme Simone Biles](https://www.telemundo.com/sites/nbcutelemundo/files/styles/fit-1240w/public/images/article/cover/2016/08/17/simone-biles.jpg?ramen_itok=iqwQftIcTf)

# E' nato, è nato!
E così dopo una ulteriore avventura con Franco, lottando contro i Titani, con problemi di saturazione della memoria per lui, ed incapacità di capire come abilitare il boot sul sistema installato per me, il giorno 13 ottobre 2023, il primo uovo da Raspberry 4 si è schiuso: nato, è nato!

![is-born!](/images/arm64-first-egg-born.jpeg)

# Downloads
Al momento sto creando immagini Debian bookworm ARM64, quindi, le trovate sulla pagina di penguins-eggs di sourceforge sotto [Debian](https://sourceforge.net/projects/penguins-eggs/files/ISOS/debian/bookworm/).

Per avviarle, naturalmente è necessario predisporre il Raspberry per il boot UEFI come indicato in precedenza.

Buon divertimento!

## Bibliografia

* [Raspberry Pi 4 UEFI Firmware Images](https://github.com/pftf/RPi4)
* [Raspberry Pi 4 UEFI Boot](https://www.reddit.com/r/raspberry_pi/comments/gte2lp/raspberry_pi_4_uefi_boot/)
* [UEFI Secure Boot on the Raspberry Pi](https://www.linux.it/~ema/posts/secure-boot-rpi/)
* [Pimox 7](https://github.com/pimox/pimox7) Proxmox VE V7 for Raspberry Pi
* [instalando-vmware-esxi-en-una-raspberry-pi](https://www.bujarra.com/instalando-vmware-esxi-en-una-raspberry-pi/)

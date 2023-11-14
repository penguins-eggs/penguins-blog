---
authors: pieroproietti
slug: return-of-the-jedi
title: "Return of the Jedi"
lang: it
enableComments: true
---

import Translactions from '@site/src/components/Translactions';

<Translactions />

Il [Ritorno dello Jedi](https://it.wikipedia.org/wiki/Il_ritorno_dello_Jedi) è il terzo episodio di Guerre Stellari, uscito nel 1983.

Forse è l'età e per questo mi deve essere rimasto in testa, con le Guerre Stellari non c'entra niente, però volevo raccontarvi la novità del gradito ritorno all'architettura i386 su penguins-eggs.

# Come sono riuscito a "ricompilare" eggs sia i386 che su arm64?
penguins-eggs è un programma scritto in typescript quindi compilare è qui utilizzato in maniera un po' improria. Sarebbe più corretto scrivere come sono riuscito a generare nuovamente il pacchetto su l'architettura i386 non più supportata da node.

Qua dobbiamo ringraziare la Regina Debian. 

Cercando di aiutare un utente alle prese con LMDE 6 ho notato che sulla macchina era presente node18, grazie alla versione pacchettizzata da Debian. 

Su bullseye è presente solo node12, usando da tempo node16 - non si può fare - ma qua essendo presente la versione 18 mi è venuto il dubbio e l'idea di provarci.

Eggs è costruito con [oclif](https://oclif.io/), e genero il pacchetto con lo stesso framework che - tra l'altro - racchiude l'eseguibile di node nel pacchetto stesso.

Se su Debian node18 esiste, perchè non provare a sostituirlo con un semplice link?

Ha funzionato!

![Il ritorno dello Jedi](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d1/Spade_laser_incrociate.svg/675px-Spade_laser_incrociate.svg.png?20110813225109)

**Nota** La storia è naturalmente un po' più lunga e non priva di una certa fatica, ma è la stessa che mi ha portato - usando sostanzialmente lo stesso schema - ad ottenere una versione arm64 funzionante.

Ma di questo parleremo un'altra volta.

# E come la mettiamo con Visual Studio code?

Non sò quante volte ho bestemmiato in turco la mancanza di code su i386, ho tentato con lite, un editor LUA un po' somigliante; ho smadonnato con sublime - bello ma diverso - alla fine, non usando più di tanto i386, m'ero adattato a geany.

Ecco il sistema per installare l'ultima versione di code funzionante su i386

```
wget https://az764295.vo.msecnd.net/stable/c7d83e57cd18f18026a8162d042843bda1bcf21f/code_1.35.1-1560349847_i386.deb 

sudo dpkg -i ./code*.deb
```

Era pure facile! A saperlo, però...
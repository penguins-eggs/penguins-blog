---
authors: pieroproietti
slug: state-of-the-art
title: "State of the art"
lang: it
enableComments: true
---

import Translactions from '@site/src/components/Translactions';

<Translactions />

Quando ho cominciato `eggs` ho utilizzato javascript con nodejs per creare un programma CLI.

La ragione risiedeva nella difficoltà trovata ad effettuare manutenzione su script bash, dalla mancata conoscenza di python e dal fatto che javascript era molto diffuso e di moda.

Dopo i primi approcci, sono passato ad utilizzare [oclif](https://oclif.io/) per tutta la struttura. oclif permette di gestire tutto insieme dal README.md ai vari comandi, il parse degli argomenti, etc.

Con oclif e con l'esplosione di typescript sono passato a quest'ultimo che trovo più semplice da gestire rispetto a javascript ed utile sia per rintracciare gli errori in fase di transplilazione che per un maggiore aiuto disponibile sull'editor.

Successivamente, sempre attraverso oclif sono riuscito a creare i primi pacchetti debian, quindi, in una enfasi di novità ho trovato il modo di utilizzare [ink](https://github.com/vadimdemedes/ink) per ottenere una interfaccia TUI più pulita e basata su [react](https://react.dev/).

Il programma cresceva e si dilungava il tempo di compilazione, così decisi di cominciare ad utilizzare [pnpm](https://pnpm.io) al posto di [npm](https://www.npmjs.com/). L'operazione non si mostrò affatto indolore, oclif non era compatibile con pnpm e decisi di fare un fork di oclif denominato [oclif-phpm](https://github.com/pieroproietti/oclif-pnpm) attualmente allineato alla versione di oclif v3.4.3.

Ho provato a chiedere l'inclusione del supporto per pnpm in oclif, sembra non ve ne sia l'opportunità e, naturalmente, oclif - un progetto importante - va avanti e rilascia continuamente nuove versioni, ed ho difficoltà con il mio fork a seguirle.

La stessa cosa sta pure succedendo con ink, eggs riesce a lavorare con la versione 3.x ma non con la nuova versione 4.x.

# Una via d'uscita?

L'ideale sarebbe uno strumento come oclif, che consenta di gestire il tutto compatibile con ink o similari che consentano di utilizzare React in una CLI.

Al momento tutto questo non esiste.

Potrebbe essere anche una opportunità pensare di scrivere qualcosa del genere utilizzando [deno](https://deno.com/) o [bun](https://bun.sh/).

Consultando tra le [issue](https://github.com/vadimdemedes/ink/issues/250) di ink, sembra che vi sia una certa compatibilità tra ink e deno.

Mentre una alternativa ad oclif potrebbe essere [cliffy](https://cliffy.io/).

Ma c'è tanto mare da attraversare!

![deno](/images/DenoLogo3D-Anim.gif)

Credits: [MasterJames](https://github.com/MasterJames/high-res-deno-logo)


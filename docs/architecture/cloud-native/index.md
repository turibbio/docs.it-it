---
title: Architettura di applicazioni .NET cloud native per Azure
description: Guida per la creazione di applicazioni native del cloud che sfruttano contenitori, microservizi e funzionalità senza server di Azure.
author: ardalis
ms.date: 05/13/2020
ms.openlocfilehash: 172097b4915deb2d6f0b06441d7c4ca389bbca25
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051506"
---
# <a name="architecting-cloud-native-net-applications-for-azure"></a>Architettura di applicazioni .NET cloud native per Azure

![Immagine di copertina](./media/cover.png)

**EDIZIONE v. 1.0**

PUBBLICATO DA

Microsoft Developer Division, team dei prodotti .NET e Visual Studio

Una divisione di Microsoft Corporation

One Microsoft Way

Redmond, Washington 98052-6399

Copyright &copy; 2020 di Microsoft Corporation

Tutti i diritti sono riservati. Nessuna parte del contenuto di questo libro può essere riprodotta o trasmessa in qualsiasi forma o con qualsiasi mezzo, senza il permesso scritto dell'editore.

Questo libro viene fornito "così com'è" ed esprime i punti di vista e le opinioni dell'autore. I punti di vista, le opinioni e le informazioni contenute nel presente libro, inclusi gli URL e altri riferimenti a siti Web, possono essere soggetti a modifiche senza preavviso.

 Alcuni esempi usati in questo documento vengono forniti a scopo puramente illustrativo e sono fittizi. Nessuna associazione reale o connessione è intenzionale o può essere desunta.

Microsoft e i marchi elencati nella pagina Web relativa ai marchi all'indirizzo <https://www.microsoft.com> sono marchi delle società del gruppo Microsoft.

Mac e macOS sono marchi registrati di Apple Inc.

Il logo Docker Whale è un marchio registrato di Docker, Inc. usato dall'autorizzazione.

Tutti gli altri marchi e logo appartengono ai rispettivi proprietari.

Autori:

> **Rob Vettor**, Principal Cloud System Architect/IP architect- [thinkingincloudnative.com](https://thinkingincloudnative.com/about/), Microsoft
>
> **Steve "ardalis" Smith**, Software Architect e Trainer- [Ardalis.com](https://ardalis.com)

Partecipanti e revisori:

> **Cesar de la Torre**, responsabile del programma principale, team di .NET, Microsoft
>
> **Nitura Anil**, Senior Program Manager, team di .NET, Microsoft
>
> **Jeremy Likness**, Senior Program Manager, team di .NET, Microsoft
>
> **Cecil Phillip**, senior cloud Advocate, Microsoft

Editor:

> **Maira Wenzel**, Program Manager, team di .NET, Microsoft

## <a name="version"></a>Versione

Questa guida è stata scritta per coprire la versione di **.net core 3,1** insieme a molti aggiornamenti aggiuntivi relativi alla stessa "Wave" delle tecnologie (ovvero, Azure e altre tecnologie di terze parti) in concomitanza con la versione di .net core 3,1.

## <a name="who-should-use-this-guide"></a>Destinatari della guida

I destinatari di questa guida sono principalmente sviluppatori, lead di sviluppo e architetti che sono interessati ad apprendere come creare applicazioni progettate per il cloud.

Un pubblico secondario è costituito da Decision Maker tecnici che pianificano di scegliere se compilare le proprie applicazioni usando un approccio nativo per il cloud.

## <a name="how-you-can-use-this-guide"></a>Come usare questa guida

Questa guida inizia definendo cloud native e introducendo un'applicazione di riferimento compilata usando principi e tecnologie native del cloud. Oltre a questi primi due capitoli, il resto del libro è suddiviso in capitoli specifici che riguardano argomenti comuni alla maggior parte delle applicazioni native del cloud. È possibile passare a uno di questi capitoli per ottenere informazioni sugli approcci nativi del cloud per:

- Accesso ai dati e ai dati
- Modelli di comunicazione
- Scalabilità e scalabilità
- Resilienza delle applicazioni
- Monitoraggio e integrità
- Identità e sicurezza
- DevOps

Questa guida è disponibile sia in formato [PDF](https://dotnet.microsoft.com/download/e-book/cloud-native-azure/pdf) che in linea. È possibile inviare questo documento o collegamenti alla relativa versione online al team per garantire una conoscenza comune di questi argomenti. La maggior parte di questi argomenti trae vantaggio da una comprensione coerente dei principi e dei modelli sottostanti, nonché dei compromessi che interessano le decisioni correlate a questi argomenti. Il nostro obiettivo di questo documento è quello di dotare i team e i loro leader con le informazioni necessarie per prendere decisioni ben informate per l'architettura, lo sviluppo e l'hosting delle proprie applicazioni.

## <a name="send-your-feedback"></a>Invia commenti e suggerimenti

Questo libro ed esempi correlati sono in continua evoluzione, quindi il feedback è stato accolto. Per Commenti su come migliorare questo libro, usare la sezione feedback nella parte inferiore di qualsiasi pagina basata su [problemi di GitHub](https://github.com/dotnet/docs/issues).

>[!div class="step-by-step"]
>[Avanti](introduction.md)

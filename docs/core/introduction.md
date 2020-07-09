---
title: Introduzione e panoramica di .NET Core
description: .NET Core è un'implementazione modulare e ad alte prestazioni di .NET per la creazione di app Windows, Linux e macOS. Vedere l'introduzione a .NET Core per iniziare.
author: richlander
ms.date: 03/26/2020
ms.custom: updateeachrelease
ms.openlocfilehash: f99b446bbd38b2b814c13afa13ab34cd5c9aa086
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/20/2020
ms.locfileid: "81645520"
---
# <a name="introduction-to-net-core"></a>Introduzione a .NET Core

[.NET Core](about.md) è una piattaforma di sviluppo [open source](https://github.com/dotnet/runtime/blob/master/LICENSE.TXT)generica. Puoi creare app .NET Core per processori Windows, macOS e Linux per x64, x86, ARM32 e ARM64 usando più linguaggi di programmazione. Framework e API vengono forniti per [cloud](/aspnet/core/), [IoT](/archive/msdn-magazine/2019/august/net-core-cross-platform-iot-programming-with-net-core-3-0), [interfaccia utente client](../desktop-wpf/overview/index.md)e machine [learning](/dotnet/machine-learning/).

[Scaricare .NET Core SDK](https://dotnet.microsoft.com/download) per provare .NET Core nel computer. La versione più recente è [.NET Core 3.1](https://devblogs.microsoft.com/dotnet/announcing-net-core-3-1/).

## <a name="download-net-core"></a>Download di .NET Core

È possibile ottenere .NET Core nei modi seguenti:You can get .NET Core in the following ways:

* [Programmi di installazione per Windows e macOS](https://dotnet.microsoft.com/download)
* [Pacchetti Linux](https://docs.microsoft.com/dotnet/core/install/linux-package-managers)
* [Contenitori Docker](https://hub.docker.com/_/microsoft-dotnet-core/)
* [zip e tarball](https://dotnet.microsoft.com/download/dotnet-core/3.1)
* [Installare gli script](https://dotnet.microsoft.com/download/dotnet-core/scripts)
* [Note sulla versione](https://github.com/dotnet/core/tree/master/release-notes)

## <a name="create-your-first-application"></a>Creare la prima applicazione

Dopo aver installato .NET Core SDK, aprire un prompt dei comandi. Utilizzare i comandi seguenti per creare ed eseguire un'applicazione:Use the following commands to create and run an application:

```dotnetcli
dotnet new console
dotnet run
```

Dovrebbe venire visualizzato l'output seguente.

```output
Hello World!
```

## <a name="contribute"></a>Collaborazione

.NET Core è una piattaforma aperta. Tutti sono invitati a partecipare.

* Archiviare problemi e domande sul prodotto [nella community degli sviluppatori](https://developercommunity.visualstudio.com/spaces/61/index.html).
* I contributi del prodotto devono essere effettuati in uno dei repository di progetto, ad esempio [dotnet/runtime](https://github.com/dotnet/runtime), [dotnet/sdk](https://github.com/dotnet/sdk), [dotnet/rosyln](https://github.com/dotnet/roslyn)o [aspnetcore](https://github.com/dotnet/aspnetcore). Per ulteriori informazioni, vedere [.NET Core repos](https://github.com/dotnet/core/blob/master/Documentation/core-repos.md).

## <a name="support"></a>Supporto

.NET Core è supportato da Microsoft su Windows, macOS e Linux e da Red Hat su Red Hat Enterprise Linux.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Esercitazioni di .NET Core](tutorials/index.md)

> [!div class="nextstepaction"]
> [Prova .NET Core nel tuo browser](../csharp/tutorials/intro-to-csharp/numbers-in-csharp.yml)

---
ms.openlocfilehash: 9ba55c45dc8087c2f7766e5cad32dae97784ffd0
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84603027"
---

### <a name="install-the-sdk"></a>Installare l'SDK

.NET Core SDK consente di sviluppare app con .NET Core. Se si installa .NET Core SDK, non è necessario installare il runtime corrispondente. Per installare .NET Core SDK, eseguire i comandi seguenti:

```bash
sudo dnf install dotnet-sdk-3.1
```

### <a name="install-the-runtime"></a>Installare il runtime

Il runtime di .NET Core consente di eseguire app eseguite con .NET Core che non includevano il Runtime. I comandi seguenti consentono di installare il runtime di ASP.NET Core, che è il runtime più compatibile per .NET Core. Nel terminale eseguire i comandi seguenti.

```bash
sudo dnf install aspnetcore-runtime-3.1
```

In alternativa al runtime di ASP.NET Core, è possibile installare il runtime di .NET Core che non include il supporto ASP.NET Core: sostituire `aspnetcore-runtime-3.1` nel comando precedente con `dotnet-runtime-3.1` .

```bash
sudo dnf install dotnet-runtime-3.1
```

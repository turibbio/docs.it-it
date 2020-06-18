---
title: Catalogo RID (Runtime Identifier) di .NET Core
description: Informazioni sull'identificatore di runtime (RID) e su come vengono usati i RID in .NET Core.
ms.date: 02/22/2019
ms.openlocfilehash: 903dd9c619008c9e3c6149a471ba814bdc9c97cc
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84903285"
---
# <a name="net-core-rid-catalog"></a>Catalogo RID di .NET Core

RID è breve per l' *identificatore di runtime*. I valori RID vengono usati per identificare le piattaforme di destinazione in cui viene eseguita l'applicazione
e vengono usati dai pacchetti .NET per rappresentare risorse specifiche della piattaforma in pacchetti NuGet. I valori seguenti sono esempi di RID: `linux-x64`, `ubuntu.14.04-x64`, `win7-x64` o `osx.10.12-x64`.
Per i pacchetti con dipendenze native, il RID specifica le piattaforme su cui può essere ripristinato il pacchetto.

Un singolo RID può essere impostato nell'elemento `<RuntimeIdentifier>` del file di progetto. Più RID possono essere definiti come elenco delimitato da punto e virgola nell'elemento `<RuntimeIdentifiers>` del file di progetto. Vengono usati anche tramite l'opzione `--runtime` con i [comandi CLI di .NET Core](./tools/index.md) seguenti:

- [dotnet build](./tools/dotnet-build.md)
- [dotnet clean](./tools/dotnet-clean.md)
- [dotnet pack](./tools/dotnet-pack.md)
- [dotnet publish](./tools/dotnet-publish.md)
- [dotnet restore](./tools/dotnet-restore.md)
- [dotnet run](./tools/dotnet-run.md)
- [dotnet store](./tools/dotnet-store.md)

I RID che rappresentano un sistema operativo reale seguono in genere il modello seguente: `[os].[version]-[architecture]-[additional qualifiers]` dove:

- `[os]` è il moniker di sistema operativo/piattaforma. Ad esempio: `ubuntu`.

- `[version]` è il numero di versione del sistema operativo nel formato separato da punti (`.`). Ad esempio: `15.10`.

  - **Non deve** trattarsi di versioni marketing, poiché tali versioni rappresentano spesso più versioni discrete del sistema operativo con una superficie delle API della piattaforma variabile.

- `[architecture]` indica l'architettura del processore, ad esempio `x86`, `x64`, `arm` o `arm64`.

- `[additional qualifiers]` differenziano ulteriormente piattaforme diverse. Ad esempio: `aot`.

## <a name="rid-graph"></a>Grafico RID

Il grafico RID o grafico di fallback di runtime è un elenco di RID compatibili tra loro. I RID sono definiti nel pacchetto [Microsoft.NETCore.Platforms](https://www.nuget.org/packages/Microsoft.NETCore.Platforms/). È possibile visualizzare l'elenco di RID supportati e il grafico RID nella [*runtime.jssu*](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/runtime.json) file, che si trova nel `dotnet/runtime` repository. In questo file, si noterà che tutti i RID, ad eccezione di quello di base, contengono un'istruzione `"#import"`. Queste istruzioni indicano RID compatibili.

Quando NuGet ripristina i pacchetti, tenta di trovare una corrispondenza esatta per il runtime specificato.
Se non trova una corrispondenza esatta, NuGet ripercorre il grafico a ritroso fino a individuare il sistema compatibile più simile in base al grafico RID.

L'esempio seguente è la voce effettiva per il RID `osx.10.12-x64`:

```json
"osx.10.12-x64": {
    "#import": [ "osx.10.12", "osx.10.11-x64" ]
}
```

Il RID sopra riportato specifica che `osx.10.12-x64` importa `osx.10.11-x64`. Quando NuGet ripristina i pacchetti, quindi, tenta di trovare una corrispondenza esatta per `osx.10.12-x64` nel pacchetto. Se NuGet non riesce a trovare il runtime specifico, può ripristinare i pacchetti che specificano i runtime `osx.10.11-x64`, ad esempio.

L'esempio seguente mostra un grafico RID leggermente più ampio, anch'esso definito nel file *runtime.json*:

```
    win7-x64    win7-x86
       |   \   /    |
       |   win7     |
       |     |      |
    win-x64  |  win-x86
          \  |  /
            win
             |
            any
```

Tutti i RID finiscono per mappare nuovamente al RID `any` radice.

Esistono alcune considerazioni che è necessario tenere presenti quando si lavora con i RID:

- I RID sono **stringhe opache** e devono essere trattati come black box.
- Non creare i RID a livello di codice.
- Usare i RID già definiti per la piattaforma.
- I RID devono essere specifici, quindi non desumere nulla dal valore RID effettivo.

## <a name="using-rids"></a>Uso dei RID

Per usare i RID, è necessario sapere quali sono quelli disponibili. Alla piattaforma vengono regolarmente aggiunti nuovi valori.
Per la versione più recente e completa, vedere il [runtime.jssu](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/runtime.json) file nel `dotnet/runtime` repository.

.NET Core 2.0 SDK introduce il concetto di RID portabili. Si tratta di nuovi valori aggiunti al grafico RID che non sono associati a una versione specifica o a una distribuzione specifica del sistema operativo e sono la scelta preferibile quando si usa .NET Core 2.0 e versioni successive. Risultano particolarmente utili per la gestione di più distribuzioni di Linux, perché la maggior parte dei RID di distribuzione sono mappati ai RID portabili.

L'elenco seguente mostra un piccolo subset dei RID più comuni usati per ogni sistema operativo.

## <a name="windows-rids"></a>RID Windows

Sono elencati solo i valori comuni. Per la versione più recente e completa, vedere il [runtime.jssu](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/runtime.json) file nel `dotnet/runtime` repository.

- Portable (.NET Core 2.0 o versioni successive)
  - `win-x64`
  - `win-x86`
  - `win-arm`
  - `win-arm64`
- Windows 7/Windows Server 2008 R2
  - `win7-x64`
  - `win7-x86`
- Windows 8.1/Windows Server 2012 R2
  - `win81-x64`
  - `win81-x86`
  - `win81-arm`
- Windows 10/Windows Server 2016
  - `win10-x64`
  - `win10-x86`
  - `win10-arm`
  - `win10-arm64`

Per altre informazioni, vedere [dipendenze e requisiti di .NET Core](install/dependencies.md?pivots=os-windows).

## <a name="linux-rids"></a>RID Linux

Sono elencati solo i valori comuni. Per la versione più recente e completa, vedere il [runtime.jssu](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/runtime.json) file nel `dotnet/runtime` repository. I dispositivi che eseguono una distribuzione non elencata di seguito potrebbero funzionare con uno dei RID portabili. Ad esempio, i dispositivi Raspberry Pi che eseguono una distribuzione di Linux non elencata possono essere assegnati a `linux-arm`.

- Portable (.NET Core 2.0 o versioni successive)
  - `linux-x64`(La maggior parte delle distribuzioni desktop, ad esempio CentOS, Debian, Fedora, Ubuntu e derivati)
  - `linux-musl-x64` (Le distribuzioni leggere che usano [musl](https://wiki.musl-libc.org/projects-using-musl.html) come Alpine Linux)
  - `linux-arm`(Distribuzioni di Linux in esecuzione su ARM come raspbian su Raspberry Pi modello 2 +)
  - `linux-arm64`(Distribuzioni di Linux in esecuzione su ARM a 64 bit come Ubuntu Server 64-bit su Raspberry Pi modello 3 +)
- Red Hat Enterprise Linux
  - `rhel-x64` (Sostituito da `linux-x64` per RHEL versioni successive alla versione 6)
  - `rhel.6-x64` (.NET Core 2.0 o versioni successive)
- Tizen (.NET Core 2.0 o versioni successive)
  - `tizen`
  - `tizen.4.0.0`
  - `tizen.5.0.0`

Per altre informazioni, vedere [dipendenze e requisiti di .NET Core](install/dependencies.md?pivots=os-linux).

## <a name="macos-rids"></a>RID macOS

I RID macOS usano la personalizzazione "OSX" precedente. Sono elencati solo i valori comuni. Per la versione più recente e completa, vedere il [runtime.jssu](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/runtime.json) file nel `dotnet/runtime` repository.

- Portable (.NET Core 2.0 o versioni successive)
  - `osx-x64` (La versione minima del sistema operativo è macOS 10.12 Sierra)
- macOS 10.10  Yosemite
  - `osx.10.10-x64`
- macOS 10.11 El Capitan
  - `osx.10.11-x64`
- macOS 10.12 Sierra (.NET Core 1.1 o versioni successive)
  - `osx.10.12-x64`
- macOS 10.13 High Sierra (.NET Core 1.1 o versioni successive)
  - `osx.10.13-x64`
- macOS 10.14 Mojave (.NET Core 1.1 o versioni successive)
  - `osx.10.14-x64`

Per altre informazioni, vedere [dipendenze e requisiti di .NET Core](install/dependencies.md?pivots=os-macos).

## <a name="see-also"></a>Vedere anche

- [ID di runtime](https://github.com/dotnet/runtime/blob/master/src/libraries/pkg/Microsoft.NETCore.Platforms/readme.md)

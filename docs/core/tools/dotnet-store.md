---
title: comando dotnet store
description: Il comando 'dotnet store' archivia gli assembly specificati nell'archivio pacchetti di runtime.
ms.date: 02/14/2020
ms.openlocfilehash: 2f28a9bc287a87f600bda385c579e8070cbaa5ab
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463390"
---
# <a name="dotnet-store"></a>dotnet store

**Questo articolo si applica a:** ✔️ .NET Core 2.x SDK e versioni successive

## <a name="name"></a>Nome

`dotnet store`: archivia gli assembly specificati nell'[archivio pacchetti di runtime](../deploying/runtime-store.md).

## <a name="synopsis"></a>Riepilogo

```dotnetcli
dotnet store -m|--manifest <PATH_TO_MANIFEST_FILE>
    -f|--framework <FRAMEWORK_VERSION> -r|--runtime <RUNTIME_IDENTIFIER>
    [--framework-version <FRAMEWORK_VERSION>] [--output <OUTPUT_DIRECTORY>]
    [--skip-optimization] [--skip-symbols] [-v|--verbosity <LEVEL>]
    [--working-dir <WORKING_DIRECTORY>]

dotnet store -h|--help
```

## <a name="description"></a>Descrizione

`dotnet store` archivia gli assembly specificati nell'[archivio pacchetti di runtime](../deploying/runtime-store.md). Per impostazione predefinita, gli assembly sono ottimizzati per il framework e il runtime di destinazione. Per altre informazioni, vedere l'argomento [Archivio pacchetti di runtime](../deploying/runtime-store.md).

## <a name="required-options"></a>Opzioni obbligatorie

- **`-f|--framework <FRAMEWORK>`**

  Specifica il [framework di destinazione](../../standard/frameworks.md). Il framework di destinazione deve essere specificato nel file di progetto.

- **`-m|--manifest <PATH_TO_MANIFEST_FILE>`**

  Il *file manifesto dell'archivio pacchetti* è un file XML che contiene l'elenco di pacchetti da archiviare. Il formato del file manifesto è compatibile con il formato di progetto SDK. È quindi possibile usare un file di progetto che fa riferimento ai pacchetti desiderati con l'opzione `-m|--manifest` per archiviare gli assembly nell'archivio pacchetti di runtime. Per specificare più file manifesto, ripetere l'opzione e il percorso per ogni file. Ad esempio: `--manifest packages1.csproj --manifest packages2.csproj`.

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  [Identificatore di runtime](../rid-catalog.md) di destinazione.

## <a name="optional-options"></a>Opzioni facoltative

- **`--framework-version <FRAMEWORK_VERSION>`**

  Specifica la versione di .NET Core SDK. Questa opzione consente di selezionare una versione di framework specifica, oltre al framework specificato dall'opzione `-f|--framework`.

- **`-h|--help`**

  Visualizza le informazioni sulla guida.

- **`-o|--output <OUTPUT_DIRECTORY>`**

  Specifica il percorso dell'archivio pacchetti di runtime. Se non viene specificato, per impostazione predefinita viene usata la sottodirectory *store* della directory di installazione di .NET Core del profilo utente.

- **`--skip-optimization`**

  Ignora la fase di ottimizzazione.

- **`--skip-symbols`**

  Ignora la generazione di simboli. Attualmente è possibile generare simboli solo in Windows e Linux.

- **`-v|--verbosity <LEVEL>`**

  Imposta il livello di dettaglio del comando. I valori consentiti sono `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

- **`-w|--working-dir <WORKING_DIRECTORY>`**

  Directory di lavoro usata dal comando. Se non viene specificata, viene usata la sottodirectory *obj* della directory corrente.

## <a name="examples"></a>Esempi

- Archiviare i pacchetti specificati nel file di progetto *packages.csproj* per .NET Core 2.0.0:

  ```dotnetcli
  dotnet store --manifest packages.csproj --framework-version 2.0.0
  ```

- Archiviare i pacchetti specificati nel file di progetto *packages.csproj* senza ottimizzazione:

  ```dotnetcli
  dotnet store --manifest packages.csproj --skip-optimization
  ```

## <a name="see-also"></a>Vedere anche

- [Archivio pacchetti di runtime](../deploying/runtime-store.md)

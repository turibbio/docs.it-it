---
title: Comando dotnet msbuild
description: Il comando dotnet msbuild consente di accedere alla riga di comando di MSBuild.
ms.date: 02/14/2020
ms.openlocfilehash: 9739fe782e17db3955db087ca1781ad4280cd491
ms.sourcegitcommit: 1eae045421d9ea2bfc82aaccfa5b1ff1b8c9e0e4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/16/2020
ms.locfileid: "84803167"
---
# <a name="dotnet-msbuild"></a>dotnet msbuild

**Questo articolo si applica a:** ✔️ .NET Core 2. x SDK e versioni successive

## <a name="name"></a>Nome

`dotnet msbuild`: consente di compilare un progetto e tutte le relative dipendenze. Nota: potrebbe essere necessario specificare un file di soluzione o di progetto se sono presenti più file.

## <a name="synopsis"></a>Riepilogo

```dotnetcli
dotnet msbuild <MSBUILD_ARGUMENTS>

dotnet msbuild -h
```

## <a name="description"></a>Descrizione

Il comando `dotnet msbuild` consente di accedere a un'istanza completamente funzionante di MSBuild.

Il comando ha esattamente le stesse funzionalità del client della riga di comando MSBuild esistente solo per i progetti in stile SDK. Le opzioni sono uguali. Per ulteriori informazioni sulle opzioni disponibili, vedere la Guida di [riferimento alla riga di comando di MSBuild](/visualstudio/msbuild/msbuild-command-line-reference).

Il comando [dotnet build](dotnet-build.md) equivale a `dotnet msbuild -restore`. Quando non si vuole compilare il progetto e si dispone di una destinazione specifica che si vuole eseguire, usare `dotnet build` o `dotnet msbuild` e specificare la destinazione.

## <a name="examples"></a>Esempi

- Compilare un progetto e le relative dipendenze:

  ```dotnetcli
  dotnet msbuild
  ```

- Compilare un progetto e le relative dipendenze usando la configurazione per il rilascio:

  ```dotnetcli
  dotnet msbuild -property:Configuration=Release
  ```

- Eseguire la destinazione di pubblicazione e pubblicare per il RID `osx.10.11-x64`:

  ```dotnetcli
  dotnet msbuild -target:Publish -property:RuntimeIdentifiers=osx.10.11-x64
  ```

- Vedere l'intero progetto con tutte le destinazioni incluse dall'SDK:

  ```dotnetcli
  dotnet msbuild -preprocess
  dotnet msbuild -preprocess:<fileName>.xml
  ```

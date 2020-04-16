---
title: Comando dotnet build-server
description: Il comando dotnet build-server interagisce con i server avviati da una compilazione.
ms.date: 02/14/2020
ms.openlocfilehash: 882b697c07aac0e20266f3ad4e6c11888a0b7acc
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463733"
---
# <a name="dotnet-build-server"></a><span data-ttu-id="92e82-103">dotnet build-server</span><span class="sxs-lookup"><span data-stu-id="92e82-103">dotnet build-server</span></span>

<span data-ttu-id="92e82-104">**Questo articolo si applica a:** ✔️ .NET Core 2.1 SDK e versioni successive</span><span class="sxs-lookup"><span data-stu-id="92e82-104">**This article applies to:** ✔️ .NET Core 2.1 SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="92e82-105">Nome</span><span class="sxs-lookup"><span data-stu-id="92e82-105">Name</span></span>

<span data-ttu-id="92e82-106">`dotnet build-server`: interagisce con i server avviati da una compilazione.</span><span class="sxs-lookup"><span data-stu-id="92e82-106">`dotnet build-server` - Interacts with servers started by a build.</span></span>

## <a name="synopsis"></a><span data-ttu-id="92e82-107">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="92e82-107">Synopsis</span></span>

```dotnetcli
dotnet build-server shutdown [--msbuild] [--razor] [--vbcscompiler]

dotnet build-server shutdown -h|--help

dotnet build-server -h|--help
```

## <a name="commands"></a><span data-ttu-id="92e82-108">Comandi:</span><span class="sxs-lookup"><span data-stu-id="92e82-108">Commands</span></span>

- **`shutdown`**

  <span data-ttu-id="92e82-109">Arresta i server di compilazione avviati da dotnet.</span><span class="sxs-lookup"><span data-stu-id="92e82-109">Shuts down build servers that are started from dotnet.</span></span> <span data-ttu-id="92e82-110">Per impostazione predefinita, vengono arrestati tutti i server.</span><span class="sxs-lookup"><span data-stu-id="92e82-110">By default, all servers are shut down.</span></span>

## <a name="options"></a><span data-ttu-id="92e82-111">Opzioni</span><span class="sxs-lookup"><span data-stu-id="92e82-111">Options</span></span>

- **`-h|--help`**

  <span data-ttu-id="92e82-112">Stampa una breve guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="92e82-112">Prints out a short help for the command.</span></span>

- **`--msbuild`**

  <span data-ttu-id="92e82-113">Arresta il server di compilazione MSBuild.</span><span class="sxs-lookup"><span data-stu-id="92e82-113">Shuts down the MSBuild build server.</span></span>

- **`--razor`**

  <span data-ttu-id="92e82-114">Arresta il server di compilazione Razor.</span><span class="sxs-lookup"><span data-stu-id="92e82-114">Shuts down the Razor build server.</span></span>

- **`--vbcscompiler`**

  <span data-ttu-id="92e82-115">Arresta il server di compilazione del compilatore VB/C#.</span><span class="sxs-lookup"><span data-stu-id="92e82-115">Shuts down the VB/C# compiler build server.</span></span>

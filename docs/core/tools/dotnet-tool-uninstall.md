---
title: Comando dotnet tool uninstall
description: Il comando dotnet tool uninstalls lo strumento .NET Core specificato dal computer.
ms.date: 02/14/2020
ms.openlocfilehash: 0416f91019a49e17f1be14a1d928ad1fafaa736c
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463316"
---
# <a name="dotnet-tool-uninstall"></a><span data-ttu-id="c14f7-103">dotnet tool uninstall</span><span class="sxs-lookup"><span data-stu-id="c14f7-103">dotnet tool uninstall</span></span>

<span data-ttu-id="c14f7-104">**Questo articolo si applica a:** ✔️ .NET Core 2.1 SDK e versioni successive</span><span class="sxs-lookup"><span data-stu-id="c14f7-104">**This article applies to:** ✔️ .NET Core 2.1 SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="c14f7-105">Nome</span><span class="sxs-lookup"><span data-stu-id="c14f7-105">Name</span></span>

<span data-ttu-id="c14f7-106">`dotnet tool uninstall`- Disinstalla lo [strumento .NET Core](global-tools.md) specificato dal computer.</span><span class="sxs-lookup"><span data-stu-id="c14f7-106">`dotnet tool uninstall` - Uninstalls the specified [.NET Core tool](global-tools.md) from your machine.</span></span>

## <a name="synopsis"></a><span data-ttu-id="c14f7-107">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="c14f7-107">Synopsis</span></span>

```dotnetcli
dotnet tool uninstall <PACKAGE_NAME> -g|--global

dotnet tool uninstall <PACKAGE_NAME> --tool-path <PATH>

dotnet tool uninstall <PACKAGE_NAME>

dotnet tool uninstall -h|--help
```

## <a name="description"></a><span data-ttu-id="c14f7-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c14f7-108">Description</span></span>

<span data-ttu-id="c14f7-109">Il `dotnet tool uninstall` comando consente di disinstallare gli strumenti .NET Core dal computer.</span><span class="sxs-lookup"><span data-stu-id="c14f7-109">The `dotnet tool uninstall` command provides a way for you to uninstall .NET Core tools from your machine.</span></span> <span data-ttu-id="c14f7-110">Per utilizzare il comando, specificare una delle seguenti opzioni:</span><span class="sxs-lookup"><span data-stu-id="c14f7-110">To use the command, you specify one of the following options:</span></span>

* <span data-ttu-id="c14f7-111">Per disinstallare uno strumento globale installato nel `--global` percorso predefinito, utilizzare l'opzione .</span><span class="sxs-lookup"><span data-stu-id="c14f7-111">To uninstall a global tool that was installed in the default location, use the `--global` option.</span></span>
* <span data-ttu-id="c14f7-112">Per disinstallare uno strumento globale installato in `--tool-path` un percorso personalizzato, utilizzare l'opzione .</span><span class="sxs-lookup"><span data-stu-id="c14f7-112">To uninstall a global tool that was installed in a custom location,  use the `--tool-path` option.</span></span>
* <span data-ttu-id="c14f7-113">Per disinstallare uno strumento locale, omettere le `--global` opzioni e `--tool-path` .</span><span class="sxs-lookup"><span data-stu-id="c14f7-113">To uninstall a local tool, omit the `--global` and `--tool-path` options.</span></span>

<span data-ttu-id="c14f7-114">**Gli strumenti locali sono disponibili a partire da .NET Core SDK 3.0.**</span><span class="sxs-lookup"><span data-stu-id="c14f7-114">**Local tools are available starting with .NET Core SDK 3.0.**</span></span>

## <a name="arguments"></a><span data-ttu-id="c14f7-115">Argomenti</span><span class="sxs-lookup"><span data-stu-id="c14f7-115">Arguments</span></span>

- **`PACKAGE_NAME`**

  <span data-ttu-id="c14f7-116">Nome/ID del pacchetto NuGet che contiene lo strumento .NET Core da disinstallare.</span><span class="sxs-lookup"><span data-stu-id="c14f7-116">Name/ID of the NuGet package that contains the .NET Core tool to uninstall.</span></span> <span data-ttu-id="c14f7-117">È possibile trovare il nome del pacchetto usando il comando [dotnet tool list](dotnet-tool-list.md).</span><span class="sxs-lookup"><span data-stu-id="c14f7-117">You can find the package name using the [dotnet tool list](dotnet-tool-list.md) command.</span></span>

## <a name="options"></a><span data-ttu-id="c14f7-118">Opzioni</span><span class="sxs-lookup"><span data-stu-id="c14f7-118">Options</span></span>

- **`-g|--global`**

  <span data-ttu-id="c14f7-119">Specifica che lo strumento da rimuovere appartiene a un'installazione a livello utente.</span><span class="sxs-lookup"><span data-stu-id="c14f7-119">Specifies that the tool to be removed is from a user-wide installation.</span></span> <span data-ttu-id="c14f7-120">Non può essere usata con l'opzione `--tool-path`.</span><span class="sxs-lookup"><span data-stu-id="c14f7-120">Can't be combined with the `--tool-path` option.</span></span> <span data-ttu-id="c14f7-121">Omettendo `--global` entrambi `--tool-path` e specifica che lo strumento da rimuovere è uno strumento locale.</span><span class="sxs-lookup"><span data-stu-id="c14f7-121">Omitting both `--global` and `--tool-path` specifies that the tool to be removed is a local tool.</span></span>

- **`-h|--help`**

  <span data-ttu-id="c14f7-122">Stampa una breve guida per il comando.</span><span class="sxs-lookup"><span data-stu-id="c14f7-122">Prints out a short help for the command.</span></span>

- **`--tool-path <PATH>`**

  <span data-ttu-id="c14f7-123">Specifica il percorso in cui disinstallare lo strumento.</span><span class="sxs-lookup"><span data-stu-id="c14f7-123">Specifies the location where to uninstall the tool.</span></span> <span data-ttu-id="c14f7-124">Il valore di PATH può essere assoluto o relativo.</span><span class="sxs-lookup"><span data-stu-id="c14f7-124">PATH can be absolute or relative.</span></span> <span data-ttu-id="c14f7-125">Non può essere usata con l'opzione `--global`.</span><span class="sxs-lookup"><span data-stu-id="c14f7-125">Can't be combined with the `--global` option.</span></span> <span data-ttu-id="c14f7-126">Omettendo `--global` entrambi `--tool-path` e specifica che lo strumento da rimuovere è uno strumento locale.</span><span class="sxs-lookup"><span data-stu-id="c14f7-126">Omitting both `--global` and `--tool-path` specifies that the tool to be removed is a local tool.</span></span>

## <a name="examples"></a><span data-ttu-id="c14f7-127">Esempi</span><span class="sxs-lookup"><span data-stu-id="c14f7-127">Examples</span></span>

- **`dotnet tool uninstall -g dotnetsay`**

  <span data-ttu-id="c14f7-128">Disinstalla lo strumento globale [dotnetsay.](https://www.nuget.org/packages/dotnetsay/)</span><span class="sxs-lookup"><span data-stu-id="c14f7-128">Uninstalls the [dotnetsay](https://www.nuget.org/packages/dotnetsay/) global tool.</span></span>

- **`dotnet tool uninstall dotnetsay --tool-path c:\global-tools`**

  <span data-ttu-id="c14f7-129">Disinstalla lo strumento globale [dotnetsay](https://www.nuget.org/packages/dotnetsay/) da una directory di Windows specifica.</span><span class="sxs-lookup"><span data-stu-id="c14f7-129">Uninstalls the [dotnetsay](https://www.nuget.org/packages/dotnetsay/) global tool from a specific Windows directory.</span></span>

- **`dotnet tool uninstall dotnetsay --tool-path ~/bin`**

  <span data-ttu-id="c14f7-130">Disinstalla lo strumento globale [dotnetsay](https://www.nuget.org/packages/dotnetsay/) da una directory Linux/macOS specifica.</span><span class="sxs-lookup"><span data-stu-id="c14f7-130">Uninstalls the [dotnetsay](https://www.nuget.org/packages/dotnetsay/) global tool from a specific Linux/macOS directory.</span></span>

- **`dotnet tool uninstall dotnetsay`**

  <span data-ttu-id="c14f7-131">Disinstalla lo strumento locale [dotnetsay](https://www.nuget.org/packages/dotnetsay/) dalla directory corrente.</span><span class="sxs-lookup"><span data-stu-id="c14f7-131">Uninstalls the [dotnetsay](https://www.nuget.org/packages/dotnetsay/) local tool from the current directory.</span></span>

## <a name="see-also"></a><span data-ttu-id="c14f7-132">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c14f7-132">See also</span></span>

- [<span data-ttu-id="c14f7-133">Strumenti .NET Core</span><span class="sxs-lookup"><span data-stu-id="c14f7-133">.NET Core tools</span></span>](global-tools.md)
- [<span data-ttu-id="c14f7-134">Esercitazione: Installare e usare uno strumento globale .NET Core usando l'interfaccia della riga di comando di .NET CoreTutorial: Install and use a .NET Core global tool using the .NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="c14f7-134">Tutorial: Install and use a .NET Core global tool using the .NET Core CLI</span></span>](global-tools-how-to-use.md)
- [<span data-ttu-id="c14f7-135">Esercitazione: Installare e usare uno strumento locale .NET Core usando l'interfaccia della riga di comando di .NET CoreTutorial: Install and use a .NET Core local tool using the .NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="c14f7-135">Tutorial: Install and use a .NET Core local tool using the .NET Core CLI</span></span>](local-tools-how-to-use.md)

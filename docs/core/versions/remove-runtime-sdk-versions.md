---
title: Rimuovere il runtime di .NET Core e l'SDK
description: Questo articolo descrive come determinare le versioni del runtime di .NET Core e dell'SDK attualmente installate e quindi come rimuoverle in Windows, Mac e Linux.
ms.date: 04/22/2020
author: billwagner
ms.author: wiwagn
ms.custom: updateeachrelease
ms.openlocfilehash: 0b3501bf7c730120d3885b8c3f29b901fb131215
ms.sourcegitcommit: 8b02d42f93adda304246a47f49f6449fc74a3af4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82135763"
---
# <a name="how-to-remove-the-net-core-runtime-and-sdk"></a><span data-ttu-id="3fa07-103">Come rimuovere Runtime di .NET Core e .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="3fa07-103">How to remove the .NET Core Runtime and SDK</span></span>

<span data-ttu-id="3fa07-104">Nel corso del tempo, via via che si installano le versioni aggiornate di runtime e SDK di .NET Core l'utente potrebbe voler rimuovere le versioni obsolete di .NET Core dal computer.</span><span class="sxs-lookup"><span data-stu-id="3fa07-104">Over time, as you install updated versions of the .NET Core runtime and SDK, you may want to remove outdated versions of .NET Core from your machine.</span></span> <span data-ttu-id="3fa07-105">La rimozione delle versioni precedenti del runtime può cambiare il runtime scelto per eseguire le applicazioni di framework condiviso, come descritto in dettaglio nell'articolo [Scelta della versione di .NET Core](selection.md).</span><span class="sxs-lookup"><span data-stu-id="3fa07-105">Removing older versions of the runtime may change the runtime chosen to run shared framework applications, as detailed in the article on [.NET Core version selection](selection.md).</span></span>

## <a name="should-i-remove-a-version"></a><span data-ttu-id="3fa07-106">Stabilire se è necessario rimuovere una versione</span><span class="sxs-lookup"><span data-stu-id="3fa07-106">Should I remove a version?</span></span>

<span data-ttu-id="3fa07-107">La [selezione delle versioni di .NET Core](selection.md) e la compatibilità di runtime di .NET Core tra gli aggiornamenti consente la rimozione sicura delle versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="3fa07-107">The [.NET Core version selection](selection.md) behaviors and the runtime compatibility of .NET Core across updates enables safe removal of previous versions.</span></span> <span data-ttu-id="3fa07-108">Gli aggiornamenti al runtime di .NET Core sono compatibili all'interno delle versioni principali, ad esempio 1.x e 2.x.</span><span class="sxs-lookup"><span data-stu-id="3fa07-108">.NET Core runtime updates are compatible within a major version 'band' such as 1.x and 2.x.</span></span> <span data-ttu-id="3fa07-109">Inoltre, le nuove versioni di .NET Core SDK mantengono in genere la possibilità di creare applicazioni destinate a versioni precedenti del runtime in modo compatibile.</span><span class="sxs-lookup"><span data-stu-id="3fa07-109">Additionally, newer releases of the .NET Core SDK generally maintain the ability to build applications that target previous versions of the runtime in a compatible manner.</span></span>

<span data-ttu-id="3fa07-110">In generale, sono necessari solo l'SDK più recente e l'ultima versione patch dei runtime richiesti per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3fa07-110">In general, you only need the latest SDK and latest patch version of the runtimes required for your application.</span></span> <span data-ttu-id="3fa07-111">Istanze in cui mantenere le versioni precedenti di SDK o Runtime includono la gestione di applicazioni basate su **Project. JSON**.</span><span class="sxs-lookup"><span data-stu-id="3fa07-111">Instances where keeping older SDK or Runtime versions include maintaining **project.json**-based applications.</span></span> <span data-ttu-id="3fa07-112">Se l'applicazione non ha ragioni specifiche per mantenere le versioni precedenti di SDK o Runtime, è possibile rimuovere le versioni precedenti in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="3fa07-112">Unless your application has specific reasons for earlier SDKs or runtimes, you may safely remove older versions.</span></span>

## <a name="determine-what-is-installed"></a><span data-ttu-id="3fa07-113">Determinare che cosa è installato</span><span class="sxs-lookup"><span data-stu-id="3fa07-113">Determine what is installed</span></span>

<span data-ttu-id="3fa07-114">A partire da .NET Core 2.1, la CLI di .NET include opzioni che è possibile usare per elencare le versioni di SDK e runtime installate nel computer.</span><span class="sxs-lookup"><span data-stu-id="3fa07-114">Starting with .NET Core 2.1, the .NET CLI has options you can use to list the versions of the SDK and runtime that are installed on your machine.</span></span>  <span data-ttu-id="3fa07-115">Usare [`dotnet --list-sdks`](../tools/dotnet.md#options) per visualizzare l'elenco di SDK installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="3fa07-115">Use [`dotnet --list-sdks`](../tools/dotnet.md#options) to see the list of SDKs installed on your machine.</span></span> <span data-ttu-id="3fa07-116">Usare [`dotnet --list-runtimes`](../tools/dotnet.md#options) per visualizzare l'elenco dei runtime installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="3fa07-116">Use [`dotnet --list-runtimes`](../tools/dotnet.md#options) to see the list of runtimes installed on your machine.</span></span> <span data-ttu-id="3fa07-117">Il testo seguente illustra un output tipico per Windows, macOS o Linux:</span><span class="sxs-lookup"><span data-stu-id="3fa07-117">The following text shows typical output for Windows, macOS, or Linux:</span></span>

<!-- markdownlint-disable MD025 -->

# <a name="windows"></a>[<span data-ttu-id="3fa07-118">Windows</span><span class="sxs-lookup"><span data-stu-id="3fa07-118">Windows</span></span>](#tab/windows)

<span data-ttu-id="3fa07-119">Eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-119">By running the following command:</span></span>

```dotnetcli
dotnet --list-sdks
```

<span data-ttu-id="3fa07-120">Si otterrà un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-120">You get output similar to the following:</span></span>

```console
2.1.200-preview-007474 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007480 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007509 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007570 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007576 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007587 [C:\Program Files\dotnet\sdk]
2.1.200-preview-007589 [C:\Program Files\dotnet\sdk]
2.1.200 [C:\Program Files\dotnet\sdk]
2.1.201 [C:\Program Files\dotnet\sdk]
2.1.202 [C:\Program Files\dotnet\sdk]
2.1.300-preview2-008533 [C:\Program Files\dotnet\sdk]
2.1.300 [C:\Program Files\dotnet\sdk]
2.1.400-preview-009063 [C:\Program Files\dotnet\sdk]
2.1.400-preview-009088 [C:\Program Files\dotnet\sdk]
2.1.400-preview-009171 [C:\Program Files\dotnet\sdk]
```

<span data-ttu-id="3fa07-121">Eseguire quindi il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-121">And by running the following command:</span></span>

```dotnetcli
dotnet --list-runtimes
```

<span data-ttu-id="3fa07-122">Si otterrà un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-122">You get output similar to the following:</span></span>

```console
Microsoft.AspNetCore.All 2.1.0-preview2-final [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.0 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.1 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.2 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.0-preview2-final [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.0 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.1 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.2 [C:\Program Files\dotnet\shared\Microsoft.AspNetCore.App]
Microsoft.NETCore.App 2.0.6 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.7 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.9 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0-preview2-26406-04 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.1 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.2 [C:\Program Files\dotnet\shared\Microsoft.NETCore.App]
```

# <a name="linux"></a>[<span data-ttu-id="3fa07-123">Linux</span><span class="sxs-lookup"><span data-stu-id="3fa07-123">Linux</span></span>](#tab/linux)

<span data-ttu-id="3fa07-124">Eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-124">By running the following command:</span></span>

```dotnetcli
dotnet --list-sdks
```

<span data-ttu-id="3fa07-125">Si otterrà un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-125">You get output similar to the following:</span></span>

```console
1.0.1 [/usr/share/dotnet/sdk]
1.0.4 [/usr/share/dotnet/sdk]
2.0.0-preview1-005977 [/usr/share/dotnet/sdk]
2.0.0-preview2-006497 [/usr/share/dotnet/sdk]
2.0.0 [/usr/share/dotnet/sdk]
2.1.4 [/usr/share/dotnet/sdk]
2.1.300-preview2-008530 [/usr/share/dotnet/sdk]
2.1.300 [/usr/share/dotnet/sdk]
2.1.301 [/usr/share/dotnet/sdk]
```

<span data-ttu-id="3fa07-126">Eseguire quindi il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-126">And by running the following command:</span></span>

```dotnetcli
dotnet --list-runtimes
```

<span data-ttu-id="3fa07-127">Si otterrà un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-127">You get output similar to the following:</span></span>

```console
Microsoft.AspNetCore.All 2.1.0-preview2-final [/usr/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.0 [/usr/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.1 [/usr/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.0-preview2-final [/usr/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.0 [/usr/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.1 [/usr/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.NETCore.App 1.0.4 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.0.5 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.1.1 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.1.2 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0-preview1-002111-00 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0-preview2-25407-01 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.5 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0-preview2-26406-04 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.1 [/usr/share/dotnet/shared/Microsoft.NETCore.App]
```

# <a name="macos"></a>[<span data-ttu-id="3fa07-128">macOS</span><span class="sxs-lookup"><span data-stu-id="3fa07-128">macOS</span></span>](#tab/macos)

<span data-ttu-id="3fa07-129">Eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-129">By running the following command:</span></span>

```dotnetcli
dotnet --list-sdks
```

<span data-ttu-id="3fa07-130">Si otterrà un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-130">You get output similar to the following:</span></span>

```console
1.0.1 [/usr/local/share/dotnet/sdk]
1.0.4 [/usr/local/share/dotnet/sdk]
2.0.0-preview1-005977 [/usr/local/share/dotnet/sdk]
2.0.0-preview2-006497 [/usr/local/share/dotnet/sdk]
2.0.0 [/usr/local/share/dotnet/sdk]
2.1.4 [/usr/local/share/dotnet/sdk]
2.1.300-preview2-008530 [/usr/local/share/dotnet/sdk]
2.1.300 [/usr/local/share/dotnet/sdk]
2.1.301 [/usr/local/share/dotnet/sdk]
```

<span data-ttu-id="3fa07-131">Eseguire quindi il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-131">And by running the following command:</span></span>

```dotnetcli
dotnet --list-runtimes
```

<span data-ttu-id="3fa07-132">Si otterrà un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-132">You get output similar to the following:</span></span>

```console
Microsoft.AspNetCore.All 2.1.0-preview2-final [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.All 2.1.1 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.All]
Microsoft.AspNetCore.App 2.1.0-preview2-final [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.0 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.AspNetCore.App 2.1.1 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
Microsoft.NETCore.App 1.0.4 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.0.5 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.1.1 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 1.1.2 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0-preview1-002111-00 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0-preview2-25407-01 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.0 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.0.5 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0-preview2-26406-04 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.0 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
Microsoft.NETCore.App 2.1.1 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
```

---

## <a name="uninstall-net-core"></a><span data-ttu-id="3fa07-133">Disinstallare .NET Core</span><span class="sxs-lookup"><span data-stu-id="3fa07-133">Uninstall .NET Core</span></span>

# <a name="windows"></a>[<span data-ttu-id="3fa07-134">Windows</span><span class="sxs-lookup"><span data-stu-id="3fa07-134">Windows</span></span>](#tab/windows)

<span data-ttu-id="3fa07-135">.NET Core usa la finestra di dialogo **Installazione applicazioni** di Windows per rimuovere le versioni di runtime e SDK di .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3fa07-135">.NET Core uses the Windows **Add/Remove Programs** dialog to remove versions of the .NET Core runtime and SDK.</span></span> <span data-ttu-id="3fa07-136">La figura seguente illustra la finestra di dialogo **Installazione applicazioni** con diverse versioni di runtime e SDK di .NET Core installati.</span><span class="sxs-lookup"><span data-stu-id="3fa07-136">The following figure shows the **Add/Remove Programs** dialog with several versions of the .NET runtime and SDK installed.</span></span>

![Installazione applicazioni per la rimozione di .NET Core](./media/remove-runtime-sdk-versions/programs-and-features.png)

<span data-ttu-id="3fa07-138">Selezionare tutte le versioni da rimuovere dal computer e fare clic su **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="3fa07-138">Select any versions you want to remove from your machine and click **Uninstall**.</span></span>

# <a name="linux"></a>[<span data-ttu-id="3fa07-139">Linux</span><span class="sxs-lookup"><span data-stu-id="3fa07-139">Linux</span></span>](#tab/linux)

<span data-ttu-id="3fa07-140">Per disinstallare .NET Core (SDK o runtime) in Linux sono disponibili varie opzioni.</span><span class="sxs-lookup"><span data-stu-id="3fa07-140">There are more options to uninstall .NET Core (either SDK or runtime) on Linux.</span></span> <span data-ttu-id="3fa07-141">Il modo migliore per disinstallare .NET Core è eseguire il mirroring dell'azione usata per installare .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3fa07-141">The best way for you to uninstall .NET Core is to mirror the action you used to install .NET Core.</span></span> <span data-ttu-id="3fa07-142">Le specifiche variano in base alla distribuzione scelta e al metodo di installazione.</span><span class="sxs-lookup"><span data-stu-id="3fa07-142">The specifics depend on your chosen distribution and the installation method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3fa07-143">Per le installazioni di Red Hat, vedere l'[introduzione a Red Hat](https://access.redhat.com/documentation/en-us/net_core/2.0/html/getting_started_guide/gs_install_dotnet#install_register_rehel) per informazioni sull'installazione e la disinstallazione di .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3fa07-143">For Red Hat installations, consult the [Red Hat Getting Started Guide](https://access.redhat.com/documentation/en-us/net_core/2.0/html/getting_started_guide/gs_install_dotnet#install_register_rehel) for information on installing and uninstalling .NET Core.</span></span>

<span data-ttu-id="3fa07-144">A partire da .NET Core 2,1, non è necessario disinstallare il .NET Core SDK durante l'aggiornamento con gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="3fa07-144">Starting with .NET Core 2.1, there's no need to uninstall the .NET Core SDK when upgrading it using a package manager.</span></span> <span data-ttu-id="3fa07-145">La gestione pacchetti o i comandi `update` o `refresh` rimuoveranno automaticamente la versione precedente al termine dell'installazione di una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="3fa07-145">The package manager `update` or `refresh` commands will automatically remove the older version upon the successful installation of a newer version.</span></span>

<span data-ttu-id="3fa07-146">Se si è installato .NET Core usando uno strumento di gestione pacchetti, si userà la stessa gestione pacchetti per la disinstallazione dell'SDK o runtime .NET.</span><span class="sxs-lookup"><span data-stu-id="3fa07-146">If you installed .NET Core using a package manager, you use that same package manager to uninstall .NET SDK or runtime.</span></span> <span data-ttu-id="3fa07-147">Le installazioni di .NET Core supportano gli strumenti di gestione pacchetti più diffusi.</span><span class="sxs-lookup"><span data-stu-id="3fa07-147">.NET Core installations support most popular package managers.</span></span> <span data-ttu-id="3fa07-148">Vedere la documentazione relativa alla gestione pacchetti della propria distribuzione per l'esatta sintassi nel proprio ambiente:</span><span class="sxs-lookup"><span data-stu-id="3fa07-148">Consult the documentation for your distribution's package manager for the precise syntax on your environment:</span></span>

- <span data-ttu-id="3fa07-149">[apt-get(8)](https://linux.die.net/man/8/apt-get) viene usato dai sistemi basati su Debian, tra cui Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3fa07-149">[apt-get(8)](https://linux.die.net/man/8/apt-get) is used by Debian based systems, including Ubuntu.</span></span>
- <span data-ttu-id="3fa07-150">[yum(8)](https://linux.die.net/man/8/yum) viene usato in Fedora, CentOS e Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="3fa07-150">[yum(8)](https://linux.die.net/man/8/yum) is used on Fedora, CentOS, and Oracle Linux.</span></span>
- <span data-ttu-id="3fa07-151">[zypper(8)](https://en.opensuse.org/SDB:Zypper_manual_(plain)) viene usato in openSUSE e SUSE Linux Enterprise System (SLES).</span><span class="sxs-lookup"><span data-stu-id="3fa07-151">[zypper(8)](https://en.opensuse.org/SDB:Zypper_manual_(plain)) is used on openSUSE and SUSE Linux Enterprise System (SLES).</span></span>
- <span data-ttu-id="3fa07-152">[dnf(8)](https://dnf.readthedocs.io/en/latest/command_ref.html) viene usato in Fedora.</span><span class="sxs-lookup"><span data-stu-id="3fa07-152">[dnf(8)](https://dnf.readthedocs.io/en/latest/command_ref.html) is used on Fedora.</span></span>

<span data-ttu-id="3fa07-153">Nella quasi totalità dei casi, il comando per rimuovere un pacchetto è `remove`.</span><span class="sxs-lookup"><span data-stu-id="3fa07-153">In almost all cases, the command to remove a package is `remove`.</span></span>

<span data-ttu-id="3fa07-154">Il nome del pacchetto per l'installazione di .NET Core SDK per la maggior parte degli strumenti di gestione pacchetti è `dotnet-sdk`, seguito dal numero di versione.</span><span class="sxs-lookup"><span data-stu-id="3fa07-154">The package name for the .NET Core SDK installation for most package managers is `dotnet-sdk`, followed by the version number.</span></span> <span data-ttu-id="3fa07-155">A partire dalla versione 2.1.300 di .NET Core SDK e dalla versione `2.1` del runtime, sono necessari solo i numeri di versione principale e secondario: ad esempio, .NET Core SDK versione 2.1.300 può essere indicato come pacchetto `dotnet-sdk-2.1`.</span><span class="sxs-lookup"><span data-stu-id="3fa07-155">Starting with the version 2.1.300 of the .NET Core SDK and version `2.1` of the runtime, only the major and minor version numbers are necessary: for example, the .NET Core SDK version 2.1.300 can be referenced as the package `dotnet-sdk-2.1`.</span></span> <span data-ttu-id="3fa07-156">Le versioni precedenti richiedono l'intera stringa di versione: ad esempio, per la versione 2.1.200 di .NET Core SDK sarebbe necessario `dotnet-sdk-2.1.200`.</span><span class="sxs-lookup"><span data-stu-id="3fa07-156">Prior versions require the entire version string: for example, `dotnet-sdk-2.1.200` would be required for version 2.1.200 of the .NET Core SDK.</span></span>

<span data-ttu-id="3fa07-157">Per i computer su cui è installato solo il runtime e non l'SDK, il nome del pacchetto è `dotnet-runtime-<version>` per il runtime di .NET Core e `aspnetcore-runtime-<version>` per lo stack di runtime intero.</span><span class="sxs-lookup"><span data-stu-id="3fa07-157">For machines that have installed only the runtime, and not the SDK, the package name is `dotnet-runtime-<version>` for the .NET Core runtime, and `aspnetcore-runtime-<version>` for the entire runtime stack.</span></span>

<span data-ttu-id="3fa07-158">Le installazioni di .NET Core precedenti alla 2,0 non hanno disinstallato l'applicazione host quando l'SDK è stato disinstallato tramite Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="3fa07-158">.NET Core installations earlier than 2.0 didn't uninstall the host application when the SDK was uninstalled using the package manager.</span></span> <span data-ttu-id="3fa07-159">Usando `apt-get`, il comando è:</span><span class="sxs-lookup"><span data-stu-id="3fa07-159">Using `apt-get`, the command is:</span></span>

```bash
apt-get remove dotnet-host
```

<span data-ttu-id="3fa07-160">Si noti che non è presente alcuna versione `dotnet-host`collegata a.</span><span class="sxs-lookup"><span data-stu-id="3fa07-160">Note that there's no version attached to `dotnet-host`.</span></span>

<span data-ttu-id="3fa07-161">Se è l'installazione è stata eseguita tramite un file tarball, è necessario rimuovere .NET Core usando il metodo manuale.</span><span class="sxs-lookup"><span data-stu-id="3fa07-161">If you installed using a tarball, you must remove .NET Core using the manual method.</span></span>

<span data-ttu-id="3fa07-162">In Linux è necessario rimuovere gli SDK e i runtime separatamente, rimuovendo le directory con versione.</span><span class="sxs-lookup"><span data-stu-id="3fa07-162">On Linux, you must remove the SDKs and runtimes separately, by removing the versioned directories.</span></span> <span data-ttu-id="3fa07-163">Per chiarire questo problema, l'SDK e il runtime vengono eliminati dal disco.</span><span class="sxs-lookup"><span data-stu-id="3fa07-163">To be clear, this deletes the SDK and runtime from disk.</span></span> <span data-ttu-id="3fa07-164">Ad esempio, per rimuovere l'SDK e il runtime versione 1.0.1, è necessario usare i comandi bash seguenti:</span><span class="sxs-lookup"><span data-stu-id="3fa07-164">For example, to remove the 1.0.1 SDK and runtime, you would use the following bash commands:</span></span>

```bash
version="1.0.1"
sudo rm -rf /usr/local/share/dotnet/sdk/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.NETCore.App/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.All/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.App/$version
sudo rm -rf /usr/local/share/dotnet/host/fxr/$version
```

<span data-ttu-id="3fa07-165">Le directory padre per l'SDK e il runtime sono elencate nell'output dai comandi `dotnet --list-sdks` e `dotnet --list-runtimes`, come illustrato nella tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="3fa07-165">The parent directories for the SDK and runtime are listed in the output from the `dotnet --list-sdks` and `dotnet --list-runtimes` command, as shown in the earlier table.</span></span>

# <a name="macos"></a>[<span data-ttu-id="3fa07-166">macOS</span><span class="sxs-lookup"><span data-stu-id="3fa07-166">macOS</span></span>](#tab/macos)

<span data-ttu-id="3fa07-167">In Mac è necessario rimuovere gli SDK e i runtime separatamente, rimuovendo le directory con versione.</span><span class="sxs-lookup"><span data-stu-id="3fa07-167">On Mac, you must remove the SDKs and runtimes separately, by removing the versioned directories.</span></span> <span data-ttu-id="3fa07-168">Per chiarire questo problema, l'SDK e il runtime vengono eliminati dal disco.</span><span class="sxs-lookup"><span data-stu-id="3fa07-168">To be clear, this deletes the SDK and runtime from disk.</span></span> <span data-ttu-id="3fa07-169">Ad esempio, per rimuovere l'SDK e il runtime versione 1.0.1, è necessario usare i comandi bash seguenti:</span><span class="sxs-lookup"><span data-stu-id="3fa07-169">For example, to remove the 1.0.1 SDK and runtime, you would use the following bash commands:</span></span>

```bash
version="1.0.1"
sudo rm -rf /usr/local/share/dotnet/sdk/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.NETCore.App/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.All/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.App/$version
sudo rm -rf /usr/local/share/dotnet/host/fxr/$version
```

<span data-ttu-id="3fa07-170">Le directory padre per l'SDK e il runtime sono elencate nell'output dai comandi `dotnet --list-sdks` e `dotnet --list-runtimes`, come illustrato nella tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="3fa07-170">The parent directories for the SDK and runtime are listed in the output from the `dotnet --list-sdks` and `dotnet --list-runtimes` command, as shown in the earlier table.</span></span>

---

## <a name="net-core-uninstall-tool"></a><span data-ttu-id="3fa07-171">Strumento di disinstallazione di .NET Core</span><span class="sxs-lookup"><span data-stu-id="3fa07-171">.NET Core Uninstall Tool</span></span>

<span data-ttu-id="3fa07-172">Lo [strumento di disinstallazione di .NET Core](../additional-tools/uninstall-tool.md) (`dotnet-core-uninstall`) consente di rimuovere gli SDK e i runtime di .NET Core da un sistema.</span><span class="sxs-lookup"><span data-stu-id="3fa07-172">The [.NET Core Uninstall Tool](../additional-tools/uninstall-tool.md) (`dotnet-core-uninstall`) lets you remove .NET Core SDKs and runtimes from a system.</span></span> <span data-ttu-id="3fa07-173">È disponibile una raccolta di opzioni per specificare le versioni che devono essere disinstallate.</span><span class="sxs-lookup"><span data-stu-id="3fa07-173">A collection of options is available to specify which versions should be uninstalled.</span></span>

## <a name="visual-studio-dependency-on-net-core-sdk-versions"></a><span data-ttu-id="3fa07-174">Dipendenza di Visual Studio dalle versioni .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="3fa07-174">Visual Studio dependency on .NET Core SDK versions</span></span>

<span data-ttu-id="3fa07-175">Prima di Visual Studio 2019 versione 16,3, i programmi di installazione di Visual Studio denominavano il programma di installazione .NET Core SDK autonomo.</span><span class="sxs-lookup"><span data-stu-id="3fa07-175">Before Visual Studio 2019 version 16.3, Visual Studio installers called the standalone .NET Core SDK installer.</span></span> <span data-ttu-id="3fa07-176">Di conseguenza, le versioni dell'SDK vengono visualizzate nella finestra di dialogo **Installazione applicazioni** di Windows.</span><span class="sxs-lookup"><span data-stu-id="3fa07-176">As a result, the SDK versions appear in the Windows **Add/Remove Programs** dialog.</span></span> <span data-ttu-id="3fa07-177">La rimozione di SDK di .NET Core installati da Visual Studio usando il programma di installazione autonomo potrebbe interrompere Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fa07-177">Removing .NET Core SDKs that were installed by Visual Studio using the standalone installer may break Visual Studio.</span></span> <span data-ttu-id="3fa07-178">Se si verificano problemi in Visual Studio dopo la disinstallazione di SDK, eseguire Repair sulla versione specifica di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fa07-178">If Visual Studio has problems after you uninstall SDKs, run Repair on that specific version of Visual Studio.</span></span> <span data-ttu-id="3fa07-179">La tabella seguente illustra alcune delle dipendenze di Visual Studio sulle versioni .NET Core SDK:</span><span class="sxs-lookup"><span data-stu-id="3fa07-179">The following table shows some of the Visual Studio dependencies on .NET Core SDK versions:</span></span>

| <span data-ttu-id="3fa07-180">Versione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3fa07-180">Visual Studio version</span></span> | <span data-ttu-id="3fa07-181">Versione .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="3fa07-181">.NET Core SDK version</span></span> |
| -- | -- |
| <span data-ttu-id="3fa07-182">Visual Studio 2019 versione 16.2</span><span class="sxs-lookup"><span data-stu-id="3fa07-182">Visual Studio 2019 version 16.2</span></span> | <span data-ttu-id="3fa07-183">.NET Core SDK 2.2.4 XX, 2.1.8 XX</span><span class="sxs-lookup"><span data-stu-id="3fa07-183">.NET Core SDK 2.2.4xx, 2.1.8xx</span></span> |
| <span data-ttu-id="3fa07-184">Visual Studio 2019 versione 16.1</span><span class="sxs-lookup"><span data-stu-id="3fa07-184">Visual Studio 2019 version 16.1</span></span> | <span data-ttu-id="3fa07-185">.NET Core SDK 2.2.3 XX, 2.1.7 XX</span><span class="sxs-lookup"><span data-stu-id="3fa07-185">.NET Core SDK 2.2.3xx, 2.1.7xx</span></span> |
| <span data-ttu-id="3fa07-186">Visual Studio 2019 versione 16,0</span><span class="sxs-lookup"><span data-stu-id="3fa07-186">Visual Studio 2019 version 16.0</span></span> | <span data-ttu-id="3fa07-187">.NET Core SDK 2.2.2 XX, 2.1.6 XX</span><span class="sxs-lookup"><span data-stu-id="3fa07-187">.NET Core SDK 2.2.2xx, 2.1.6xx</span></span> |
| <span data-ttu-id="3fa07-188">Visual Studio 2017 versione 15,9</span><span class="sxs-lookup"><span data-stu-id="3fa07-188">Visual Studio 2017 version 15.9</span></span> | <span data-ttu-id="3fa07-189">.NET Core SDK 2.2.1 XX, 2.1.5 XX</span><span class="sxs-lookup"><span data-stu-id="3fa07-189">.NET Core SDK 2.2.1xx, 2.1.5xx</span></span> |
| <span data-ttu-id="3fa07-190">Visual Studio 2017 versione 15.8</span><span class="sxs-lookup"><span data-stu-id="3fa07-190">Visual Studio 2017 version 15.8</span></span> | <span data-ttu-id="3fa07-191">.NET Core SDK 2.1.4 XX</span><span class="sxs-lookup"><span data-stu-id="3fa07-191">.NET Core SDK 2.1.4xx</span></span> |

<span data-ttu-id="3fa07-192">A partire da Visual Studio 2019 versione 16,3, Visual Studio è responsabile della propria copia del .NET Core SDK.</span><span class="sxs-lookup"><span data-stu-id="3fa07-192">Starting with Visual Studio 2019 version 16.3, Visual Studio is in charge of its own copy of the .NET Core SDK.</span></span> <span data-ttu-id="3fa07-193">Per questo motivo, le versioni dell'SDK non vengono più visualizzate nella finestra di dialogo **Installazione applicazioni** .</span><span class="sxs-lookup"><span data-stu-id="3fa07-193">For that reason, you no longer see those SDK versions in the **Add/Remove Programs** dialog.</span></span>

## <a name="remove-the-nuget-fallback-folder"></a><span data-ttu-id="3fa07-194">Rimuovere la cartella di fallback NuGet</span><span class="sxs-lookup"><span data-stu-id="3fa07-194">Remove the NuGet fallback folder</span></span>

<span data-ttu-id="3fa07-195">Prima di .NET Core 3,0 SDK, i programmi di .NET Core SDK hanno usato *NuGetFallbackFolder* per archiviare una cache di pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="3fa07-195">Before .NET Core 3.0 SDK, the .NET Core SDK installers used the *NuGetFallbackFolder* to store a cache of NuGet packages.</span></span> <span data-ttu-id="3fa07-196">Questa cache è stata utilizzata durante le operazioni `dotnet restore` , `dotnet build /t:Restore`ad esempio o.</span><span class="sxs-lookup"><span data-stu-id="3fa07-196">This cache was used during operations such as `dotnet restore` or `dotnet build /t:Restore`.</span></span> <span data-ttu-id="3fa07-197">Si trova in *C:\Program Files\dotnet\sdk* in Windows e in/usr/local/share/DotNet/SDK in MacOS. */usr/local/share/dotnet/sdk* `NuGetFallbackFolder`</span><span class="sxs-lookup"><span data-stu-id="3fa07-197">The `NuGetFallbackFolder` is located at *C:\Program Files\dotnet\sdk* on Windows and at */usr/local/share/dotnet/sdk* on macOS.</span></span>

<span data-ttu-id="3fa07-198">Potrebbe essere necessario rimuovere questa cartella, se:</span><span class="sxs-lookup"><span data-stu-id="3fa07-198">You may want to remove this folder, if:</span></span>

* <span data-ttu-id="3fa07-199">Si sta sviluppando solo usando .NET Core 3,0 SDK o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="3fa07-199">You're only developing using .NET Core 3.0 SDK or later versions.</span></span>
* <span data-ttu-id="3fa07-200">Si sta sviluppando usando .NET Core SDK versioni precedenti alla 3,0, ma è possibile lavorare online e le cose possono risultare più lente una volta.</span><span class="sxs-lookup"><span data-stu-id="3fa07-200">You're developing using .NET Core SDK versions earlier than 3.0, but you can work online and things can be slower once.</span></span>

<span data-ttu-id="3fa07-201">Se si vuole rimuovere la cartella fallback di NuGet, è possibile eliminarla, ma saranno necessari i privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="3fa07-201">If you want to remove the NuGet fallback folder, you can delete it, but you'll need admin privileges to do so.</span></span>

<span data-ttu-id="3fa07-202">Non è consigliabile eliminare la cartella *DotNet* .</span><span class="sxs-lookup"><span data-stu-id="3fa07-202">It's not recommended to delete the *dotnet* folder.</span></span> <span data-ttu-id="3fa07-203">Questa operazione rimuoverà tutti gli strumenti globali installati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3fa07-203">Doing so would remove any global tools you've previously installed.</span></span> <span data-ttu-id="3fa07-204">Inoltre, in Windows:</span><span class="sxs-lookup"><span data-stu-id="3fa07-204">Also, on Windows:</span></span>

- <span data-ttu-id="3fa07-205">Si interrompe Visual Studio 2019 versione 16,3 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="3fa07-205">You'll break Visual Studio 2019 version 16.3 and later versions.</span></span> <span data-ttu-id="3fa07-206">È possibile eseguire **Repair** per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="3fa07-206">You can run **Repair** to recover.</span></span>
- <span data-ttu-id="3fa07-207">Se sono presenti .NET Core SDK voci nella finestra di dialogo **Aggiungi/Rimuovi programmi** , saranno orfane.</span><span class="sxs-lookup"><span data-stu-id="3fa07-207">If there are .NET Core SDK entries in the **Add/Remove Programs** dialog, they'll be orphaned.</span></span>

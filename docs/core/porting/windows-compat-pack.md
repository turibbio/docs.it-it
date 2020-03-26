---
title: Usare Windows Compatibility Pack per convertire il codice per .NET Core
description: Informazioni sul pacchetto di compatibilità di Windows e su come utilizzarlo per trasferire il codice .NET Framework esistente in .NET Core.
author: terrajobst
ms.date: 12/07/2018
ms.openlocfilehash: 166259ca37a2005d67f6c545e4843a940f05fb71
ms.sourcegitcommit: b75a45f0cfe012b71b45dd9bf723adf32369d40c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/24/2020
ms.locfileid: "80228641"
---
# <a name="use-the-windows-compatibility-pack-to-port-code-to-net-core"></a><span data-ttu-id="5b638-103">Usare Windows Compatibility Pack per convertire il codice per .NET Core</span><span class="sxs-lookup"><span data-stu-id="5b638-103">Use the Windows Compatibility Pack to port code to .NET Core</span></span>

<span data-ttu-id="5b638-104">Alcuni dei problemi più comuni rilevati durante il porting di codice esistente in .NET Core sono le dipendenze da API e tecnologie che si trovano solo in .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5b638-104">Some of the most common issues found when porting existing code to .NET Core are dependencies on APIs and technologies that are only found in .NET Framework.</span></span> <span data-ttu-id="5b638-105">*Windows Compatibility Pack* fornisce molte di queste tecnologie ed è quindi molto più semplice compilare applicazioni .NET Core e librerie .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="5b638-105">The *Windows Compatibility Pack* provides many of these technologies, so it's much easier to build .NET Core applications and .NET Standard libraries.</span></span>

<span data-ttu-id="5b638-106">Il pacchetto di compatibilità è [un'estensione logica di .NET Standard 2.0](../whats-new/dotnet-core-2-0.md#api-changes-and-library-support) che aumenta in modo significativo il set di API.</span><span class="sxs-lookup"><span data-stu-id="5b638-106">The compatibility pack is a logical [extension of .NET Standard 2.0](../whats-new/dotnet-core-2-0.md#api-changes-and-library-support) that significantly increases the API set.</span></span> <span data-ttu-id="5b638-107">Il codice esistente viene compilato con quasi nessuna modifica.</span><span class="sxs-lookup"><span data-stu-id="5b638-107">Existing code compiles with almost no modifications.</span></span> <span data-ttu-id="5b638-108">Per mantenere la promessa di "il set di API che forniscono tutte le implementazioni di .NET", .NET Standard non include tecnologie che non possono funzionare su tutte le piattaforme, ad esempio il Registro di sistema, Strumentazione gestione Windows (WMI) o la reflection generano API.</span><span class="sxs-lookup"><span data-stu-id="5b638-108">To keep its promise of "the set of APIs that all .NET implementations provide", .NET Standard doesn't include technologies that can't work across all platforms, such as registry, Windows Management Instrumentation (WMI), or reflection emit APIs.</span></span> <span data-ttu-id="5b638-109">Il pacchetto di compatibilità di Windows si trova in cima a .NET Standard e fornisce l'accesso a queste tecnologie solo Windows.</span><span class="sxs-lookup"><span data-stu-id="5b638-109">The Windows Compatibility Pack sits on top of .NET Standard and provides access to these Windows-only technologies.</span></span> <span data-ttu-id="5b638-110">È particolarmente utile per i clienti che vogliono passare a .NET Core ma hanno intenzione di rimanere su Windows, almeno come primo passaggio.</span><span class="sxs-lookup"><span data-stu-id="5b638-110">It's especially useful for customers that want to move to .NET Core but plan to stay on Windows, at least as a first step.</span></span> <span data-ttu-id="5b638-111">In questo scenario, la possibilità di utilizzare tecnologie solo Windows rimuove l'ostacolo per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="5b638-111">In that scenario, being able to use Windows-only technologies removes the migration hurdle.</span></span>

## <a name="package-contents"></a><span data-ttu-id="5b638-112">Contenuto del pacchetto</span><span class="sxs-lookup"><span data-stu-id="5b638-112">Package contents</span></span>

<span data-ttu-id="5b638-113">Il pacchetto di compatibilità di Windows viene fornito tramite il [pacchetto Microsoft.Windows.Compatibility NuGet](https://www.nuget.org/packages/Microsoft.Windows.Compatibility) ed è possibile farvi riferimento da progetti destinati a .NET Core o .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="5b638-113">The Windows Compatibility Pack is provided via the [Microsoft.Windows.Compatibility NuGet package](https://www.nuget.org/packages/Microsoft.Windows.Compatibility) and can be referenced from projects that target .NET Core or .NET Standard.</span></span>

<span data-ttu-id="5b638-114">Include circa 20.000 API, incluse API solo per Windows e API multipiattaforma per le aree tecnologiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="5b638-114">It provides about 20,000 APIs, including Windows-only as well as cross-platform APIs from the following technology areas:</span></span>

- <span data-ttu-id="5b638-115">Tabelle codici</span><span class="sxs-lookup"><span data-stu-id="5b638-115">Code Pages</span></span>
- <span data-ttu-id="5b638-116">CodeDom</span><span class="sxs-lookup"><span data-stu-id="5b638-116">CodeDom</span></span>
- <span data-ttu-id="5b638-117">Configurazione</span><span class="sxs-lookup"><span data-stu-id="5b638-117">Configuration</span></span>
- <span data-ttu-id="5b638-118">Servizi directory</span><span class="sxs-lookup"><span data-stu-id="5b638-118">Directory Services</span></span>
- <span data-ttu-id="5b638-119">Disegno</span><span class="sxs-lookup"><span data-stu-id="5b638-119">Drawing</span></span>
- <span data-ttu-id="5b638-120">ODBC</span><span class="sxs-lookup"><span data-stu-id="5b638-120">ODBC</span></span>
- <span data-ttu-id="5b638-121">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="5b638-121">Permissions</span></span>
- <span data-ttu-id="5b638-122">Porte</span><span class="sxs-lookup"><span data-stu-id="5b638-122">Ports</span></span>
- <span data-ttu-id="5b638-123">Elenchi di controllo degli accessi (ACL) di Windows</span><span class="sxs-lookup"><span data-stu-id="5b638-123">Windows Access Control Lists (ACL)</span></span>
- <span data-ttu-id="5b638-124">Windows Communication Foundation (WCF)</span><span class="sxs-lookup"><span data-stu-id="5b638-124">Windows Communication Foundation (WCF)</span></span>
- <span data-ttu-id="5b638-125">Crittografia di Windows</span><span class="sxs-lookup"><span data-stu-id="5b638-125">Windows Cryptography</span></span>
- <span data-ttu-id="5b638-126">Registro eventi di Windows</span><span class="sxs-lookup"><span data-stu-id="5b638-126">Windows EventLog</span></span>
- <span data-ttu-id="5b638-127">Strumentazione gestione Windows (WMI, Windows Management Instrumentation)</span><span class="sxs-lookup"><span data-stu-id="5b638-127">Windows Management Instrumentation (WMI)</span></span>
- <span data-ttu-id="5b638-128">Contatori delle prestazioni di Windows</span><span class="sxs-lookup"><span data-stu-id="5b638-128">Windows Performance Counters</span></span>
- <span data-ttu-id="5b638-129">Registro di sistema di Windows</span><span class="sxs-lookup"><span data-stu-id="5b638-129">Windows Registry</span></span>
- <span data-ttu-id="5b638-130">Memorizzazione nella cache di Windows Runtime</span><span class="sxs-lookup"><span data-stu-id="5b638-130">Windows Runtime Caching</span></span>
- <span data-ttu-id="5b638-131">servizi Windows</span><span class="sxs-lookup"><span data-stu-id="5b638-131">Windows Services</span></span>

<span data-ttu-id="5b638-132">Per altre informazioni, vedere la [specifica del pacchetto di compatibilità](https://github.com/dotnet/designs/blob/master/accepted/2018/compat-pack/compat-pack.md).</span><span class="sxs-lookup"><span data-stu-id="5b638-132">For more information, see the [specification of the compatibility pack](https://github.com/dotnet/designs/blob/master/accepted/2018/compat-pack/compat-pack.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="5b638-133">Introduzione</span><span class="sxs-lookup"><span data-stu-id="5b638-133">Get started</span></span>

1. <span data-ttu-id="5b638-134">Prima del porting, assicurarsi di dare un'occhiata al [processo di porting](index.md).</span><span class="sxs-lookup"><span data-stu-id="5b638-134">Before porting, make sure to take a look at the [Porting process](index.md).</span></span>

2. <span data-ttu-id="5b638-135">Quando si esegue il porting di codice esistente in .NET Core o .NET Standard, installare il [pacchetto Microsoft.Windows.Compatibility NuGet](https://www.nuget.org/packages/Microsoft.Windows.Compatibility).</span><span class="sxs-lookup"><span data-stu-id="5b638-135">When porting existing code to .NET Core or .NET Standard, install the [Microsoft.Windows.Compatibility NuGet package](https://www.nuget.org/packages/Microsoft.Windows.Compatibility).</span></span>

   <span data-ttu-id="5b638-136">Se si desidera rimanere in ambiente Windows, questo è tutto.</span><span class="sxs-lookup"><span data-stu-id="5b638-136">If you want to stay on Windows, you're all set.</span></span>

3. <span data-ttu-id="5b638-137">Se si vuole eseguire l'applicazione .NET Core o la libreria .NET Standard in Linux o macOS, usare l'[analizzatore delle API](../../standard/analyzers/api-analyzer.md) per trovare informazioni sull'utilizzo delle API non supportato in tutte le piattaforme.</span><span class="sxs-lookup"><span data-stu-id="5b638-137">If you want to run the .NET Core application or .NET Standard library on Linux or macOS, use the [API Analyzer](../../standard/analyzers/api-analyzer.md) to find usage of APIs that won't work cross-platform.</span></span>

4. <span data-ttu-id="5b638-138">Rimuovere questi utilizzi di tali API, sostituirli con alternative multipiattaforma o proteggerli con un controllo di piattaforma, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5b638-138">Either remove the usages of those APIs, replace them with cross-platform alternatives, or guard them using a platform check, like:</span></span>

    ```csharp
    private static string GetLoggingPath()
    {
        // Verify the code is running on Windows.
        if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
        {
            using (var key = Registry.CurrentUser.OpenSubKey(@"Software\Fabrikam\AssetManagement"))
            {
                if (key?.GetValue("LoggingDirectoryPath") is string configuredPath)
                    return configuredPath;
            }
        }

        // This is either not running on Windows or no logging path was configured,
        // so just use the path for non-roaming user-specific data files.
        var appDataPath = Environment.GetFolderPath(Environment.SpecialFolder.LocalApplicationData);
        return Path.Combine(appDataPath, "Fabrikam", "AssetManagement", "Logging");
    }
    ```

<span data-ttu-id="5b638-139">Per una demo, vedere il [video di Channel 9 dedicato a Windows Compatibility Pack](https://channel9.msdn.com/Events/Connect/2017/T123).</span><span class="sxs-lookup"><span data-stu-id="5b638-139">For a demo, check out the [Channel 9 video of the Windows Compatibility Pack](https://channel9.msdn.com/Events/Connect/2017/T123).</span></span>

---
ms.openlocfilehash: 64e854b06895ca54a9ab9870b85868788a731c00
ms.sourcegitcommit: 34dc3c0d0d0a1cc418abff259d9daa8078d00b81
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/19/2020
ms.locfileid: "79549589"
---
### <a name="shared-framework-assemblies-removed-from-microsoftaspnetcoreapp"></a><span data-ttu-id="e6b55-101">Framework condiviso: assembly rimossi da Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="e6b55-101">Shared framework: Assemblies removed from Microsoft.AspNetCore.App</span></span>

<span data-ttu-id="e6b55-102">A partire da ASP.NET Core 3.0,`Microsoft.AspNetCore.App`il framework condiviso di ASP.NET Core ( ) contiene solo assembly di terze parti completamente sviluppati, supportati e utilizzabili da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e6b55-102">Starting in ASP.NET Core 3.0, the ASP.NET Core shared framework (`Microsoft.AspNetCore.App`) only contains first-party assemblies that are fully developed, supported, and serviceable by Microsoft.</span></span>

#### <a name="change-description"></a><span data-ttu-id="e6b55-103">Descrizione modifica:</span><span class="sxs-lookup"><span data-stu-id="e6b55-103">Change description</span></span>

<span data-ttu-id="e6b55-104">Considerare il cambiamento come la ridefinizione dei confini per la ASP.NET base "piattaforma".</span><span class="sxs-lookup"><span data-stu-id="e6b55-104">Think of the change as the redefining of boundaries for the ASP.NET Core "platform."</span></span> <span data-ttu-id="e6b55-105">Il framework condiviso sarà [compilabile da chiunque tramite GitHub](https://github.com/dotnet/source-build) e continuerà a offrire i vantaggi esistenti dei framework condivisi .NET Core alle app.</span><span class="sxs-lookup"><span data-stu-id="e6b55-105">The shared framework will be [source-buildable by anybody via GitHub](https://github.com/dotnet/source-build) and will continue to offer the existing benefits of .NET Core shared frameworks to your apps.</span></span> <span data-ttu-id="e6b55-106">Alcuni vantaggi includono dimensioni di distribuzione più piccole, applicazione centralizzata di patch e tempi di avvio più rapidi.</span><span class="sxs-lookup"><span data-stu-id="e6b55-106">Some benefits include smaller deployment size, centralized patching, and faster startup time.</span></span>

<span data-ttu-id="e6b55-107">Come parte della modifica, alcune modifiche di `Microsoft.AspNetCore.App`rilievo importanti vengono introdotte in .</span><span class="sxs-lookup"><span data-stu-id="e6b55-107">As part of the change, some notable breaking changes are introduced in `Microsoft.AspNetCore.App`.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="e6b55-108">Versione introdotta</span><span class="sxs-lookup"><span data-stu-id="e6b55-108">Version introduced</span></span>

<span data-ttu-id="e6b55-109">3.0</span><span class="sxs-lookup"><span data-stu-id="e6b55-109">3.0</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="e6b55-110">Comportamento precedente</span><span class="sxs-lookup"><span data-stu-id="e6b55-110">Old behavior</span></span>

<span data-ttu-id="e6b55-111">Progetti a `Microsoft.AspNetCore.App` cui `<PackageReference>` viene fatto riferimento tramite un elemento nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="e6b55-111">Projects referenced `Microsoft.AspNetCore.App` via a `<PackageReference>` element in the project file.</span></span>

<span data-ttu-id="e6b55-112">Inoltre, `Microsoft.AspNetCore.App` conteneva i seguenti sottocomponenti:</span><span class="sxs-lookup"><span data-stu-id="e6b55-112">Additionally, `Microsoft.AspNetCore.App` contained the following subcomponents:</span></span>

- <span data-ttu-id="e6b55-113">Json.NET`Newtonsoft.Json`( )</span><span class="sxs-lookup"><span data-stu-id="e6b55-113">Json.NET (`Newtonsoft.Json`)</span></span>
- <span data-ttu-id="e6b55-114">Entity Framework Core (assembly `Microsoft.EntityFrameworkCore.`con prefisso )</span><span class="sxs-lookup"><span data-stu-id="e6b55-114">Entity Framework Core (assemblies prefixed with `Microsoft.EntityFrameworkCore.`)</span></span>
- <span data-ttu-id="e6b55-115">Roslyn`Microsoft.CodeAnalysis`( )</span><span class="sxs-lookup"><span data-stu-id="e6b55-115">Roslyn (`Microsoft.CodeAnalysis`)</span></span>

#### <a name="new-behavior"></a><span data-ttu-id="e6b55-116">Nuovo comportamento</span><span class="sxs-lookup"><span data-stu-id="e6b55-116">New behavior</span></span>

<span data-ttu-id="e6b55-117">Un riferimento `Microsoft.AspNetCore.App` a non `<PackageReference>` richiede più un elemento nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="e6b55-117">A reference to `Microsoft.AspNetCore.App` no longer requires a `<PackageReference>` element in the project file.</span></span> <span data-ttu-id="e6b55-118">.NET Core SDK supporta un `<FrameworkReference>`nuovo elemento denominato , `<PackageReference>`che sostituisce l'utilizzo di .</span><span class="sxs-lookup"><span data-stu-id="e6b55-118">The .NET Core SDK supports a new element called `<FrameworkReference>`, which replaces the use of `<PackageReference>`.</span></span>

<span data-ttu-id="e6b55-119">Per ulteriori informazioni, vedere [dotnet/aspnetcore-3612](https://github.com/dotnet/aspnetcore/issues/3612).</span><span class="sxs-lookup"><span data-stu-id="e6b55-119">For more information, see [dotnet/aspnetcore#3612](https://github.com/dotnet/aspnetcore/issues/3612).</span></span>

<span data-ttu-id="e6b55-120">Entity Framework Core viene fornito come pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="e6b55-120">Entity Framework Core ships as NuGet packages.</span></span> <span data-ttu-id="e6b55-121">Questa modifica allinea il modello di spedizione con tutte le altre librerie di accesso ai dati in .NET.</span><span class="sxs-lookup"><span data-stu-id="e6b55-121">This change aligns the shipping model with all other data access libraries on .NET.</span></span> <span data-ttu-id="e6b55-122">Fornisce Entity Framework Core il percorso più semplice per continuare a innovare supportando le varie piattaforme .NET.</span><span class="sxs-lookup"><span data-stu-id="e6b55-122">It provides Entity Framework Core the simplest path to continue innovating while supporting the various .NET platforms.</span></span> <span data-ttu-id="e6b55-123">Lo spostamento di Entity Framework Core dal framework condiviso non ha alcun impatto sul relativo stato di libreria sviluppata, supportata e utilizzabile da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e6b55-123">The move of Entity Framework Core out of the shared framework has no impact on its status as a Microsoft-developed, supported, and serviceable library.</span></span> <span data-ttu-id="e6b55-124">I criteri di [supporto di .NET Core](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) continuano a coprirlo.</span><span class="sxs-lookup"><span data-stu-id="e6b55-124">The [.NET Core support policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) continues to cover it.</span></span>

<span data-ttu-id="e6b55-125">Json.NET ed Entity Framework Core continuano a funzionare con ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="e6b55-125">Json.NET and Entity Framework Core continue to work with ASP.NET Core.</span></span> <span data-ttu-id="e6b55-126">Non saranno, tuttavia, inclusi nel framework condiviso.</span><span class="sxs-lookup"><span data-stu-id="e6b55-126">They won't, however, be included in the shared framework.</span></span>

<span data-ttu-id="e6b55-127">Per altre informazioni, vedere [Il futuro di JSON in .NET Core 3.0.](https://github.com/dotnet/announcements/issues/90)</span><span class="sxs-lookup"><span data-stu-id="e6b55-127">For more information, see [The future of JSON in .NET Core 3.0](https://github.com/dotnet/announcements/issues/90).</span></span> <span data-ttu-id="e6b55-128">Vedere anche [l'elenco completo dei file binari rimossi](https://github.com/dotnet/aspnetcore/issues/3755) dal framework condiviso.</span><span class="sxs-lookup"><span data-stu-id="e6b55-128">Also see [the complete list of binaries](https://github.com/dotnet/aspnetcore/issues/3755) removed from the shared framework.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="e6b55-129">Motivo della modifica</span><span class="sxs-lookup"><span data-stu-id="e6b55-129">Reason for change</span></span>

<span data-ttu-id="e6b55-130">Questa modifica semplifica l'utilizzo `Microsoft.AspNetCore.App` di e riduce la duplicazione tra i pacchetti NuGet e i framework condivisi.</span><span class="sxs-lookup"><span data-stu-id="e6b55-130">This change simplifies the consumption of `Microsoft.AspNetCore.App` and reduces the duplication between NuGet packages and shared frameworks.</span></span>

<span data-ttu-id="e6b55-131">Per ulteriori informazioni sulla motivazione di questa modifica, vedere [questo post](https://devblogs.microsoft.com/aspnet/a-first-look-at-changes-coming-in-asp-net-core-3-0/)di blog .</span><span class="sxs-lookup"><span data-stu-id="e6b55-131">For more information on the motivation for this change, see [this blog post](https://devblogs.microsoft.com/aspnet/a-first-look-at-changes-coming-in-asp-net-core-3-0/).</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="e6b55-132">Azione consigliata</span><span class="sxs-lookup"><span data-stu-id="e6b55-132">Recommended action</span></span>

<span data-ttu-id="e6b55-133">Non sarà necessario per i progetti `Microsoft.AspNetCore.App` utilizzare assembly come pacchetti NuGet.It won't be necessary for projects to consume assemblies in as NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="e6b55-133">It won't be necessary for projects to consume assemblies in `Microsoft.AspNetCore.App` as NuGet packages.</span></span> <span data-ttu-id="e6b55-134">Per semplificare il targeting e l'utilizzo del framework condiviso ASP.NET Core, molti pacchetti NuGet forniti da ASP.NET Core 1.0 non vengono più prodotti.</span><span class="sxs-lookup"><span data-stu-id="e6b55-134">To simplify the targeting and usage of the ASP.NET Core shared framework, many NuGet packages shipped since ASP.NET Core 1.0 are no longer produced.</span></span> <span data-ttu-id="e6b55-135">Le API fornite da tali pacchetti sono ancora `<FrameworkReference>` `Microsoft.AspNetCore.App`disponibili per le app usando un oggetto to .</span><span class="sxs-lookup"><span data-stu-id="e6b55-135">The APIs those packages provide are still available to apps by using a `<FrameworkReference>` to `Microsoft.AspNetCore.App`.</span></span> <span data-ttu-id="e6b55-136">Esempi di API comuni includono Kestrel, MVC e Razor.Common API examples include Kestrel, MVC, and Razor.</span><span class="sxs-lookup"><span data-stu-id="e6b55-136">Common API examples include Kestrel, MVC, and Razor.</span></span>

<span data-ttu-id="e6b55-137">Questa modifica non si applica a tutti `Microsoft.AspNetCore.App` i file binari a cui viene fatto riferimento tramite ASP.NET Core 2.x.</span><span class="sxs-lookup"><span data-stu-id="e6b55-137">This change doesn't apply to all binaries referenced via `Microsoft.AspNetCore.App` in ASP.NET Core 2.x.</span></span> <span data-ttu-id="e6b55-138">Eccezioni degne di nota includono:</span><span class="sxs-lookup"><span data-stu-id="e6b55-138">Notable exceptions include:</span></span>

- <span data-ttu-id="e6b55-139">`Microsoft.Extensions`Le librerie che continuano a essere destinate https://github.com/dotnet/extensions)a .NET Standard saranno disponibili come pacchetti NuGet (vedere .</span><span class="sxs-lookup"><span data-stu-id="e6b55-139">`Microsoft.Extensions` libraries that continue to target .NET Standard will be available as NuGet packages (see https://github.com/dotnet/extensions).</span></span>
- <span data-ttu-id="e6b55-140">API prodotte dal team di ASP.NET Core `Microsoft.AspNetCore.App`che non fanno parte di .</span><span class="sxs-lookup"><span data-stu-id="e6b55-140">APIs produced by the ASP.NET Core team that aren't part of `Microsoft.AspNetCore.App`.</span></span> <span data-ttu-id="e6b55-141">Ad esempio, i seguenti componenti sono disponibili come pacchetti NuGet:For example, the following components are available as NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="e6b55-141">For example, the following components are available as NuGet packages:</span></span>
  - <span data-ttu-id="e6b55-142">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="e6b55-142">Entity Framework Core</span></span>
  - <span data-ttu-id="e6b55-143">API che forniscono l'integrazione di terze parti</span><span class="sxs-lookup"><span data-stu-id="e6b55-143">APIs that provide third-party integration</span></span>
  - <span data-ttu-id="e6b55-144">Funzionalità sperimentali</span><span class="sxs-lookup"><span data-stu-id="e6b55-144">Experimental features</span></span>
  - <span data-ttu-id="e6b55-145">API con dipendenze che non potevano [soddisfare i requisiti per essere nel framework condiviso](https://github.com/dotnet/aspnetcore/blob/4e44e5bcbedd961cc0d4f6b846699c7c494f5597/docs/SharedFramework.md)</span><span class="sxs-lookup"><span data-stu-id="e6b55-145">APIs with dependencies that couldn't [fulfill the requirements to be in the shared framework](https://github.com/dotnet/aspnetcore/blob/4e44e5bcbedd961cc0d4f6b846699c7c494f5597/docs/SharedFramework.md)</span></span>
- <span data-ttu-id="e6b55-146">Estensioni di MVC che mantengono il supporto per Json.NET.</span><span class="sxs-lookup"><span data-stu-id="e6b55-146">Extensions to MVC that maintain support for Json.NET.</span></span> <span data-ttu-id="e6b55-147">Un'API verrà fornita come pacchetto NuGet per supportare l'utilizzo di Json.NET e MVC.</span><span class="sxs-lookup"><span data-stu-id="e6b55-147">An API will be provided as a NuGet package to support using Json.NET and MVC.</span></span>
- <span data-ttu-id="e6b55-148">Il client .NET SignalR continuerà a supportare .NET Standard e verrà spedito come pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="e6b55-148">The SignalR .NET client will continue to support .NET Standard and ship as a NuGet package.</span></span> <span data-ttu-id="e6b55-149">È destinato all'utilizzo in molti runtime .NET, ad esempio Xamarin e UWP.</span><span class="sxs-lookup"><span data-stu-id="e6b55-149">It's intended for use on many .NET runtimes, such as Xamarin and UWP.</span></span>

<span data-ttu-id="e6b55-150">Per ulteriori informazioni, consultate [Interrompere la produzione di pacchetti per assembly di framework condivisi in 3.0.](https://github.com/dotnet/aspnetcore/issues/3756)</span><span class="sxs-lookup"><span data-stu-id="e6b55-150">For more information, see [Stop producing packages for shared framework assemblies in 3.0](https://github.com/dotnet/aspnetcore/issues/3756).</span></span> <span data-ttu-id="e6b55-151">Per una discussione, vedere [dotnet/aspnetcore-3757](https://github.com/dotnet/aspnetcore/issues/3757).</span><span class="sxs-lookup"><span data-stu-id="e6b55-151">For discussion, see [dotnet/aspnetcore#3757](https://github.com/dotnet/aspnetcore/issues/3757).</span></span>

#### <a name="category"></a><span data-ttu-id="e6b55-152">Category</span><span class="sxs-lookup"><span data-stu-id="e6b55-152">Category</span></span>

<span data-ttu-id="e6b55-153">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e6b55-153">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="e6b55-154">API interessate</span><span class="sxs-lookup"><span data-stu-id="e6b55-154">Affected APIs</span></span>

- <xref:Microsoft.CodeAnalysis?displayProperty=nameWithType>
- <xref:Microsoft.EntityFrameworkCore?displayProperty=nameWithType>

<!--

#### Affected APIs

- `N:Microsoft.CodeAnalysis`
- `N:Microsoft.EntityFrameworkCore`

-->

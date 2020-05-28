---
title: Panoramica dell'SDK del progetto .NET Core
titleSuffix: ''
description: Informazioni sugli SDK per progetti .NET Core.
ms.date: 02/02/2020
ms.topic: conceptual
ms.openlocfilehash: 67dede3caabd2967adca22e7563376c761829655
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144239"
---
# <a name="net-core-project-sdks"></a><span data-ttu-id="dc126-103">SDK per progetti .NET Core</span><span class="sxs-lookup"><span data-stu-id="dc126-103">.NET Core project SDKs</span></span>

<span data-ttu-id="dc126-104">I progetti .NET Core sono associati a un Software Development Kit (SDK).</span><span class="sxs-lookup"><span data-stu-id="dc126-104">.NET Core projects are associated with a software development kit (SDK).</span></span> <span data-ttu-id="dc126-105">Ogni *SDK di progetto* è un set di [destinazioni](/visualstudio/msbuild/msbuild-targets) MSBuild e [attività](/visualstudio/msbuild/msbuild-tasks) associate responsabili della compilazione, della compressione e della pubblicazione di codice.</span><span class="sxs-lookup"><span data-stu-id="dc126-105">Each *project SDK* is a set of MSBuild [targets](/visualstudio/msbuild/msbuild-targets) and associated [tasks](/visualstudio/msbuild/msbuild-tasks) that are responsible for compiling, packing, and publishing code.</span></span> <span data-ttu-id="dc126-106">Un progetto che fa riferimento a un SDK di progetto viene talvolta definito *progetto di tipo SDK*.</span><span class="sxs-lookup"><span data-stu-id="dc126-106">A project that references a project SDK is sometimes referred to as an *SDK-style project*.</span></span>

## <a name="available-sdks"></a><span data-ttu-id="dc126-107">SDK disponibili</span><span class="sxs-lookup"><span data-stu-id="dc126-107">Available SDKs</span></span>

<span data-ttu-id="dc126-108">Per .NET Core sono disponibili gli SDK seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc126-108">The following SDKs are available for .NET Core:</span></span>

| <span data-ttu-id="dc126-109">ID</span><span class="sxs-lookup"><span data-stu-id="dc126-109">ID</span></span> | <span data-ttu-id="dc126-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dc126-110">Description</span></span> | <span data-ttu-id="dc126-111">Repo</span><span class="sxs-lookup"><span data-stu-id="dc126-111">Repo</span></span>|
| - | - | - |
| `Microsoft.NET.Sdk` | <span data-ttu-id="dc126-112">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="dc126-112">The .NET Core SDK</span></span> | <https://github.com/dotnet/sdk> |
| `Microsoft.NET.Sdk.Web` | <span data-ttu-id="dc126-113">[SDK Web](/aspnet/core/razor-pages/web-sdk) di .NET Core</span><span class="sxs-lookup"><span data-stu-id="dc126-113">The .NET Core [Web SDK](/aspnet/core/razor-pages/web-sdk)</span></span> | <https://github.com/aspnet/websdk> |
| `Microsoft.NET.Sdk.Razor` | <span data-ttu-id="dc126-114">.NET Core [Razor SDK](/aspnet/core/razor-pages/sdk)</span><span class="sxs-lookup"><span data-stu-id="dc126-114">The .NET Core [Razor SDK](/aspnet/core/razor-pages/sdk)</span></span> |
| `Microsoft.NET.Sdk.Worker` | <span data-ttu-id="dc126-115">SDK del servizio Worker di .NET Core</span><span class="sxs-lookup"><span data-stu-id="dc126-115">The .NET Core Worker Service SDK</span></span> |
| `Microsoft.NET.Sdk.WindowsDesktop` | <span data-ttu-id="dc126-116">.NET Core WinForms e WPF SDK</span><span class="sxs-lookup"><span data-stu-id="dc126-116">The .NET Core WinForms and WPF SDK</span></span> |

<span data-ttu-id="dc126-117">Il .NET Core SDK è l'SDK di base per .NET Core.</span><span class="sxs-lookup"><span data-stu-id="dc126-117">The .NET Core SDK is the base SDK for .NET Core.</span></span> <span data-ttu-id="dc126-118">Gli altri SDK fanno riferimento al .NET Core SDK e i progetti associati agli altri SDK hanno tutte le proprietà di .NET Core SDK disponibili.</span><span class="sxs-lookup"><span data-stu-id="dc126-118">The other SDKs reference the .NET Core SDK, and projects that are associated with the other SDKs have all the .NET Core SDK properties available to them.</span></span> <span data-ttu-id="dc126-119">Il Web SDK, ad esempio, dipende dal .NET Core SDK e Razor SDK.</span><span class="sxs-lookup"><span data-stu-id="dc126-119">The Web SDK, for example, depends on both the .NET Core SDK and the Razor SDK.</span></span>

<span data-ttu-id="dc126-120">È anche possibile creare un proprio SDK che può essere distribuito tramite NuGet.</span><span class="sxs-lookup"><span data-stu-id="dc126-120">You can also author your own SDK that can be distributed via NuGet.</span></span>

## <a name="project-files"></a><span data-ttu-id="dc126-121">File di progetto</span><span class="sxs-lookup"><span data-stu-id="dc126-121">Project files</span></span>

<span data-ttu-id="dc126-122">I progetti .NET Core sono basati sul formato [MSBuild](/visualstudio/msbuild/msbuild) .</span><span class="sxs-lookup"><span data-stu-id="dc126-122">.NET Core projects are based on the [MSBuild](/visualstudio/msbuild/msbuild) format.</span></span> <span data-ttu-id="dc126-123">I file di progetto, che hanno estensioni come *. csproj* per i progetti C# e *. fsproj* per i progetti F #, sono in formato XML.</span><span class="sxs-lookup"><span data-stu-id="dc126-123">Project files, which have extensions like *.csproj* for C# projects and *.fsproj* for F# projects, are in XML format.</span></span> <span data-ttu-id="dc126-124">L'elemento radice di un file di progetto MSBuild è l'elemento [Project](/visualstudio/msbuild/project-element-msbuild) .</span><span class="sxs-lookup"><span data-stu-id="dc126-124">The root element of an MSBuild project file is the [Project](/visualstudio/msbuild/project-element-msbuild) element.</span></span> <span data-ttu-id="dc126-125">L' `Project` elemento dispone di un `Sdk` attributo facoltativo che specifica quale SDK (e versione) utilizzare.</span><span class="sxs-lookup"><span data-stu-id="dc126-125">The `Project` element has an optional `Sdk` attribute that specifies which SDK (and version) to use.</span></span> <span data-ttu-id="dc126-126">Per usare gli strumenti di .NET Core e compilare il codice, impostare l' `Sdk` attributo su uno degli ID nella tabella [SDK disponibili](#available-sdks) .</span><span class="sxs-lookup"><span data-stu-id="dc126-126">To use the .NET Core tools and build your code, set the `Sdk` attribute to one of the IDs in the [Available SDKs](#available-sdks) table.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  ...
</Project>
```

<span data-ttu-id="dc126-127">Per specificare un SDK che deriva da NuGet, includere la versione alla fine del nome o specificare il nome e la versione nel file *Global. JSON* .</span><span class="sxs-lookup"><span data-stu-id="dc126-127">To specify an SDK that comes from NuGet, include the version at the end of the name, or specify the name and version in the *global.json* file.</span></span>

```xml
<Project Sdk="MSBuild.Sdk.Extras/2.0.54">
  ...
</Project>
```

<span data-ttu-id="dc126-128">Un altro modo per specificare l'SDK è con l'elemento dell' [SDK](/visualstudio/msbuild/sdk-element-msbuild) di primo livello:</span><span class="sxs-lookup"><span data-stu-id="dc126-128">Another way to specify the SDK is with the top-level [Sdk](/visualstudio/msbuild/sdk-element-msbuild) element:</span></span>

```xml
<Project>
  <Sdk Name="Microsoft.NET.Sdk" />
  ...
</Project>
```

<span data-ttu-id="dc126-129">Il riferimento a un SDK in uno di questi modi semplifica notevolmente i file di progetto per .NET Core.</span><span class="sxs-lookup"><span data-stu-id="dc126-129">Referencing an SDK in one of these ways greatly simplifies project files for .NET Core.</span></span> <span data-ttu-id="dc126-130">Durante la valutazione del progetto, MSBuild aggiunge le importazioni implicite per `Sdk.props` all'inizio del file di progetto e `Sdk.targets` nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="dc126-130">While evaluating the project, MSBuild adds implicit imports for `Sdk.props` at the top of the project file and `Sdk.targets` at the bottom.</span></span>

```xml
<Project>
  <!-- Implicit top import -->
  <Import Project="Sdk.props" Sdk="Microsoft.NET.Sdk" />
  ...
  <!-- Implicit bottom import -->
  <Import Project="Sdk.targets" Sdk="Microsoft.NET.Sdk" />
</Project>
```

> [!TIP]
> <span data-ttu-id="dc126-131">In un computer Windows, i file *SDK. props* e *SDK. targets* si trovano nella cartella *%ProgramFiles%\dotnet\sdk \\ [Version] \Sdks\Microsoft.NET.Sdk\Sdk*</span><span class="sxs-lookup"><span data-stu-id="dc126-131">On a Windows machine, the *Sdk.props* and *Sdk.targets* files can be found in the *%ProgramFiles%\dotnet\sdk\\[version]\Sdks\Microsoft.NET.Sdk\Sdk* folder.</span></span>

### <a name="preprocess-the-project-file"></a><span data-ttu-id="dc126-132">Pre-elaborare il file di progetto</span><span class="sxs-lookup"><span data-stu-id="dc126-132">Preprocess the project file</span></span>

<span data-ttu-id="dc126-133">È possibile visualizzare il progetto completamente espanso poiché MSBuild lo rileva dopo che l'SDK e le relative destinazioni sono inclusi tramite il `dotnet msbuild -preprocess` comando.</span><span class="sxs-lookup"><span data-stu-id="dc126-133">You can see the fully expanded project as MSBuild sees it after the SDK and its targets are included by using the `dotnet msbuild -preprocess` command.</span></span> <span data-ttu-id="dc126-134">L'opzione di [pre-elaborazione](/visualstudio/msbuild/msbuild-command-line-reference#preprocess) del [`dotnet msbuild`](../tools/dotnet-msbuild.md) comando Mostra i file che vengono importati, le relative origini e i relativi contributi alla compilazione senza compilare effettivamente il progetto.</span><span class="sxs-lookup"><span data-stu-id="dc126-134">The [preprocess](/visualstudio/msbuild/msbuild-command-line-reference#preprocess) switch of the [`dotnet msbuild`](../tools/dotnet-msbuild.md) command shows which files are imported, their sources, and their contributions to the build without actually building the project.</span></span>

<span data-ttu-id="dc126-135">Se il progetto dispone di più framework di destinazione, concentrare i risultati del comando su un solo Framework specificandone il risultato come proprietà di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="dc126-135">If the project has multiple target frameworks, focus the results of the command on only one framework by specifying it as an MSBuild property.</span></span> <span data-ttu-id="dc126-136">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="dc126-136">For example:</span></span>

`dotnet msbuild -property:TargetFramework=netcoreapp2.0 -preprocess:output.xml`

### <a name="default-compilation-includes"></a><span data-ttu-id="dc126-137">La compilazione predefinita include</span><span class="sxs-lookup"><span data-stu-id="dc126-137">Default compilation includes</span></span>

<span data-ttu-id="dc126-138">L'impostazione predefinita include ed esclude gli elementi di compilazione, le risorse incorporate e `None` gli elementi sono definiti nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="dc126-138">The default includes and excludes for compile items, embedded resources, and `None` items are defined in the SDK.</span></span> <span data-ttu-id="dc126-139">A differenza dei progetti non SDK .NET Framework, non è necessario specificare questi elementi nel file di progetto, perché i valori predefiniti coprono i casi d'uso più comuni.</span><span class="sxs-lookup"><span data-stu-id="dc126-139">Unlike non-SDK .NET Framework projects, you don't need to specify these items in your project file, because the defaults cover most common use cases.</span></span> <span data-ttu-id="dc126-140">In questo modo, il file di progetto risulta più piccolo e più semplice da comprendere e modificare manualmente, se necessario.</span><span class="sxs-lookup"><span data-stu-id="dc126-140">This makes the project file smaller and easier to understand and edit by hand, if needed.</span></span>

<span data-ttu-id="dc126-141">La tabella seguente Mostra gli elementi e i [glob](https://en.wikipedia.org/wiki/Glob_(programming)) che vengono inclusi ed esclusi nella .NET Core SDK:</span><span class="sxs-lookup"><span data-stu-id="dc126-141">The following table shows which elements and which [globs](https://en.wikipedia.org/wiki/Glob_(programming)) are included and excluded in the .NET Core SDK:</span></span>

| <span data-ttu-id="dc126-142">Elemento</span><span class="sxs-lookup"><span data-stu-id="dc126-142">Element</span></span>           | <span data-ttu-id="dc126-143">GLOB Include</span><span class="sxs-lookup"><span data-stu-id="dc126-143">Include glob</span></span>                              | <span data-ttu-id="dc126-144">GLOB Exclude</span><span class="sxs-lookup"><span data-stu-id="dc126-144">Exclude glob</span></span>                                                  | <span data-ttu-id="dc126-145">GLOB Remove</span><span class="sxs-lookup"><span data-stu-id="dc126-145">Remove glob</span></span>              |
|-------------------|-------------------------------------------|---------------------------------------------------------------|--------------------------|
| <span data-ttu-id="dc126-146">Compilazione</span><span class="sxs-lookup"><span data-stu-id="dc126-146">Compile</span></span>           | <span data-ttu-id="dc126-147">\*\*/\*.cs (o altre estensioni del linguaggio)</span><span class="sxs-lookup"><span data-stu-id="dc126-147">\*\*/\*.cs (or other language extensions)</span></span> | <span data-ttu-id="dc126-148">\*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc</span><span class="sxs-lookup"><span data-stu-id="dc126-148">\*\*/\*.user;  \*\*/\*.\*proj;  \*\*/\*.sln;  \*\*/\*.vssscc</span></span>  | <span data-ttu-id="dc126-149">N/D</span><span class="sxs-lookup"><span data-stu-id="dc126-149">N/A</span></span>                      |
| <span data-ttu-id="dc126-150">EmbeddedResource</span><span class="sxs-lookup"><span data-stu-id="dc126-150">EmbeddedResource</span></span>  | <span data-ttu-id="dc126-151">\*\*/\*.resx</span><span class="sxs-lookup"><span data-stu-id="dc126-151">\*\*/\*.resx</span></span>                              | <span data-ttu-id="dc126-152">\*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc</span><span class="sxs-lookup"><span data-stu-id="dc126-152">\*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc</span></span>     | <span data-ttu-id="dc126-153">N/D</span><span class="sxs-lookup"><span data-stu-id="dc126-153">N/A</span></span>                      |
| <span data-ttu-id="dc126-154">Nessuno</span><span class="sxs-lookup"><span data-stu-id="dc126-154">None</span></span>              | \*\*/\*                                   | <span data-ttu-id="dc126-155">\*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc</span><span class="sxs-lookup"><span data-stu-id="dc126-155">\*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc</span></span>     | <span data-ttu-id="dc126-156">\*\*/\*.cs; \*\*/\*.resx</span><span class="sxs-lookup"><span data-stu-id="dc126-156">\*\*/\*.cs; \*\*/\*.resx</span></span> |

> [!NOTE]
> <span data-ttu-id="dc126-157">`./bin` `./obj` Per impostazione predefinita, le cartelle e, che sono rappresentate dalle `$(BaseOutputPath)` `$(BaseIntermediateOutputPath)` proprietà e MSBuild, sono escluse dai glob.</span><span class="sxs-lookup"><span data-stu-id="dc126-157">The `./bin` and `./obj` folders, which are represented by the `$(BaseOutputPath)` and `$(BaseIntermediateOutputPath)` MSBuild properties, are excluded from the globs by default.</span></span> <span data-ttu-id="dc126-158">Le esclusioni sono rappresentate dalla proprietà `$(DefaultItemExcludes)` .</span><span class="sxs-lookup"><span data-stu-id="dc126-158">Excludes are represented by the property `$(DefaultItemExcludes)`.</span></span>

#### <a name="build-errors"></a><span data-ttu-id="dc126-159">Errori di compilazione</span><span class="sxs-lookup"><span data-stu-id="dc126-159">Build errors</span></span>

<span data-ttu-id="dc126-160">Se si definisce in modo esplicito uno di questi elementi nel file di progetto, è probabile che si ottenga un errore di compilazione "NETSDK1022" simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="dc126-160">If you explicitly define any of these items in your project file, you're likely to get a "NETSDK1022" build error similar to the following:</span></span>

  > <span data-ttu-id="dc126-161">Sono stati inclusi elementi ' Compile ' duplicati.</span><span class="sxs-lookup"><span data-stu-id="dc126-161">Duplicate 'Compile' items were included.</span></span> <span data-ttu-id="dc126-162">.NET SDK include gli elementi di compilazione dalla directory del progetto per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="dc126-162">The .NET SDK includes 'Compile' items from your project directory by default.</span></span> <span data-ttu-id="dc126-163">You can either remove these items from your project file, or set the 'EnableDefaultCompileItems' property to 'false' if you want to explicitly include them in your project file. (Rimuovere questi elementi dal file di progetto o impostare la proprietà 'EnableDefaultCompileItems' su 'false' se li si vuole includere esplicitamente nel file di progetto)</span><span class="sxs-lookup"><span data-stu-id="dc126-163">You can either remove these items from your project file, or set the 'EnableDefaultCompileItems' property to 'false' if you want to explicitly include them in your project file.</span></span>

  > <span data-ttu-id="dc126-164">Sono stati inclusi elementi ' EmbeddedResource ' duplicati.</span><span class="sxs-lookup"><span data-stu-id="dc126-164">Duplicate 'EmbeddedResource' items were included.</span></span> <span data-ttu-id="dc126-165">Per impostazione predefinita, .NET SDK include gli elementi "EmbeddedResource" della directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="dc126-165">The .NET SDK includes 'EmbeddedResource' items from your project directory by default.</span></span> <span data-ttu-id="dc126-166">È possibile rimuovere questi elementi dal file di progetto o impostare la proprietà' EnableDefaultEmbeddedResourceItems ' su' false ' se si desidera includerli in modo esplicito nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="dc126-166">You can either remove these items from your project file, or set the 'EnableDefaultEmbeddedResourceItems' property to 'false' if you want to explicitly include them in your project file.</span></span>

<span data-ttu-id="dc126-167">Per risolvere gli errori, eseguire una delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc126-167">To resolve the errors, do one of the following:</span></span>

- <span data-ttu-id="dc126-168">Rimuovere gli `Compile` elementi, `EmbeddedResource` o espliciti `None` che corrispondono a quelli impliciti elencati nella tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="dc126-168">Remove the explicit `Compile`, `EmbeddedResource`, or `None` items that match the implicit ones listed on the previous table.</span></span>

- <span data-ttu-id="dc126-169">Impostare la `EnableDefaultItems` proprietà su `false` per disabilitare tutte le inclusioni di file implicite:</span><span class="sxs-lookup"><span data-stu-id="dc126-169">Set the `EnableDefaultItems` property to `false` to disable all implicit file inclusion:</span></span>

  ```xml
  <PropertyGroup>
    <EnableDefaultItems>false</EnableDefaultItems>
  </PropertyGroup>
  ```

  <span data-ttu-id="dc126-170">Se si vuole specificare i file da pubblicare con l'app, è comunque possibile usare i meccanismi di MSBuild noti, ad esempio l' `Content` elemento.</span><span class="sxs-lookup"><span data-stu-id="dc126-170">If you want to specify files to be published with your app, you can still use the known MSBuild mechanisms for that, for example, the `Content` element.</span></span>

- <span data-ttu-id="dc126-171">Disabilitare selettivamente solo `Compile` `EmbeddedResource` i glob, o impostando `None` la `EnableDefaultCompileItems` proprietà, `EnableDefaultEmbeddedResourceItems` o `EnableDefaultNoneItems` su `false` :</span><span class="sxs-lookup"><span data-stu-id="dc126-171">Selectively disable only `Compile`, `EmbeddedResource`, or `None` globs by setting the `EnableDefaultCompileItems`, `EnableDefaultEmbeddedResourceItems`, or `EnableDefaultNoneItems` property to `false`:</span></span>

  ```xml
  <PropertyGroup>
    <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
    <EnableDefaultEmbeddedResourceItems>false</EnableDefaultEmbeddedResourceItems>
    <EnableDefaultNoneItems>false</EnableDefaultNoneItems>
  </PropertyGroup>
  ```

  <span data-ttu-id="dc126-172">Se si disabilitano solo i `Compile` glob, Esplora soluzioni in Visual Studio Visualizza ancora \* gli elementi. cs come parte del progetto, inclusi come `None` elementi.</span><span class="sxs-lookup"><span data-stu-id="dc126-172">If you only disable `Compile` globs, Solution Explorer in Visual Studio still shows \*.cs items as part of the project, included as `None` items.</span></span> <span data-ttu-id="dc126-173">Per disabilitare il glob implicito `None` , `EnableDefaultNoneItems` impostare `false` anche su.</span><span class="sxs-lookup"><span data-stu-id="dc126-173">To disable the implicit `None` glob, set `EnableDefaultNoneItems` to `false` too.</span></span>

## <a name="customize-the-build"></a><span data-ttu-id="dc126-174">Personalizzare la compilazione</span><span class="sxs-lookup"><span data-stu-id="dc126-174">Customize the build</span></span>

<span data-ttu-id="dc126-175">Esistono diversi modi per [personalizzare una compilazione](/visualstudio/msbuild/customize-your-build).</span><span class="sxs-lookup"><span data-stu-id="dc126-175">There are various ways to [customize a build](/visualstudio/msbuild/customize-your-build).</span></span> <span data-ttu-id="dc126-176">Potrebbe essere necessario eseguire l'override di una proprietà passandola come argomento a un comando [MSBuild](/visualstudio/msbuild/msbuild-command-line-reference) o [DotNet](../tools/index.md) .</span><span class="sxs-lookup"><span data-stu-id="dc126-176">You may want to override a property by passing it as an argument to an [msbuild](/visualstudio/msbuild/msbuild-command-line-reference) or [dotnet](../tools/index.md) command.</span></span> <span data-ttu-id="dc126-177">È anche possibile aggiungere la proprietà al file di progetto o a un file *Directory. Build. props* .</span><span class="sxs-lookup"><span data-stu-id="dc126-177">You can also add the property to the project file or to a *Directory.Build.props* file.</span></span> <span data-ttu-id="dc126-178">Per un elenco di proprietà utili per i progetti .NET Core, vedere informazioni di [riferimento su MSBuild per progetti .NET Core SDK](msbuild-props.md).</span><span class="sxs-lookup"><span data-stu-id="dc126-178">For a list of useful properties for .NET Core projects, see [MSBuild reference for .NET Core SDK projects](msbuild-props.md).</span></span>

### <a name="custom-targets"></a><span data-ttu-id="dc126-179">Destinazioni personalizzate</span><span class="sxs-lookup"><span data-stu-id="dc126-179">Custom targets</span></span>

<span data-ttu-id="dc126-180">I progetti .NET Core possono comprimere le proprietà e le destinazioni di MSBuild personalizzate per l'uso da parte di progetti che utilizzano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="dc126-180">.NET Core projects can package custom MSBuild targets and properties for use by projects that consume the package.</span></span> <span data-ttu-id="dc126-181">Utilizzare questo tipo di estendibilità quando si desidera:</span><span class="sxs-lookup"><span data-stu-id="dc126-181">Use this type of extensibility when you want to:</span></span>

- <span data-ttu-id="dc126-182">Estendere il processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="dc126-182">Extend the build process.</span></span>
- <span data-ttu-id="dc126-183">Accedere agli elementi del processo di compilazione, ad esempio i file generati.</span><span class="sxs-lookup"><span data-stu-id="dc126-183">Access artifacts of the build process, such as generated files.</span></span>
- <span data-ttu-id="dc126-184">Esaminare la configurazione in cui viene richiamata la compilazione.</span><span class="sxs-lookup"><span data-stu-id="dc126-184">Inspect the configuration under which the build is invoked.</span></span>

<span data-ttu-id="dc126-185">Per aggiungere destinazioni o proprietà di compilazione personalizzate, inserire i file nel formato `<package_id>.targets` o `<package_id>.props` (ad esempio, `Contoso.Utility.UsefulStuff.targets` ) nella cartella di *compilazione* del progetto.</span><span class="sxs-lookup"><span data-stu-id="dc126-185">You add custom build targets or properties by placing files in the form `<package_id>.targets` or `<package_id>.props` (for example, `Contoso.Utility.UsefulStuff.targets`) in the *build* folder of the project.</span></span>

<span data-ttu-id="dc126-186">Il codice XML seguente è un frammento di codice di un file con estensione *csproj* che indica al [`dotnet pack`](../tools/dotnet-pack.md) comando cosa eseguire il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="dc126-186">The following XML is a snippet from a *.csproj* file that instructs the [`dotnet pack`](../tools/dotnet-pack.md) command what to package.</span></span> <span data-ttu-id="dc126-187">L' `<ItemGroup Label="dotnet pack instructions">` elemento inserisce i file di destinazione nella cartella di *compilazione* all'interno del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="dc126-187">The `<ItemGroup Label="dotnet pack instructions">` element places the targets files into the *build* folder inside the package.</span></span> <span data-ttu-id="dc126-188">L' `<Target Name="CollectRuntimeOutputs" BeforeTargets="_GetPackageFiles">` elemento inserisce gli assembly e i file *JSON* nella cartella di *compilazione* .</span><span class="sxs-lookup"><span data-stu-id="dc126-188">The `<Target Name="CollectRuntimeOutputs" BeforeTargets="_GetPackageFiles">` element places the assemblies and *.json* files into the *build* folder.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  ...
  <ItemGroup Label="dotnet pack instructions">
    <Content Include="build\*.targets">
      <Pack>true</Pack>
      <PackagePath>build\</PackagePath>
    </Content>
  </ItemGroup>
  <Target Name="CollectRuntimeOutputs" BeforeTargets="_GetPackageFiles">
    <!-- Collect these items inside a target that runs after build but before packaging. -->
    <ItemGroup>
      <Content Include="$(OutputPath)\*.dll;$(OutputPath)\*.json">
        <Pack>true</Pack>
        <PackagePath>build\</PackagePath>
      </Content>
    </ItemGroup>
  </Target>
  ...
  
</Project>
```

<span data-ttu-id="dc126-189">Per utilizzare una destinazione personalizzata nel progetto, aggiungere un `PackageReference` elemento che punti al pacchetto e alla relativa versione.</span><span class="sxs-lookup"><span data-stu-id="dc126-189">To consume a custom target in your project, add a `PackageReference` element that points to the package and its version.</span></span> <span data-ttu-id="dc126-190">Diversamente dagli strumenti, il pacchetto di destinazioni personalizzato è incluso nella chiusura delle dipendenze del progetto che lo utilizza.</span><span class="sxs-lookup"><span data-stu-id="dc126-190">Unlike the tools, the custom targets package is included in the consuming project's dependency closure.</span></span>

<span data-ttu-id="dc126-191">È possibile configurare la modalità di utilizzo della destinazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="dc126-191">You can configure how to use the custom target.</span></span> <span data-ttu-id="dc126-192">Poiché si tratta di una destinazione MSBuild, può dipendere da una destinazione specificata, essere eseguita dopo un'altra destinazione oppure essere richiamata manualmente tramite il `dotnet msbuild -t:<target-name>` comando.</span><span class="sxs-lookup"><span data-stu-id="dc126-192">Since it's an MSBuild target, it can depend on a given target, run after another target, or be manually invoked by using the `dotnet msbuild -t:<target-name>` command.</span></span> <span data-ttu-id="dc126-193">Tuttavia, per offrire un'esperienza utente migliore, è possibile combinare gli strumenti per progetto e le destinazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="dc126-193">However, to provide a better user experience, you can combine per-project tools and custom targets.</span></span> <span data-ttu-id="dc126-194">In questo scenario, lo strumento per progetto accetta qualsiasi parametro necessario e lo traduce nella [`dotnet msbuild`](../tools/dotnet-msbuild.md) chiamata necessaria che esegue la destinazione.</span><span class="sxs-lookup"><span data-stu-id="dc126-194">In this scenario, the per-project tool accepts whatever parameters are needed and translates that into the required [`dotnet msbuild`](../tools/dotnet-msbuild.md) invocation that executes the target.</span></span> <span data-ttu-id="dc126-195">È possibile visualizzare un esempio di questo tipo di sinergia nel repository degli [esempi di MVP Summit 2016 Hackathon](https://github.com/dotnet/MVPSummitHackathon2016) nel progetto [`dotnet-packer`](https://github.com/dotnet/MVPSummitHackathon2016/tree/master/dotnet-packer).</span><span class="sxs-lookup"><span data-stu-id="dc126-195">You can see a sample of this kind of synergy on the [MVP Summit 2016 Hackathon samples](https://github.com/dotnet/MVPSummitHackathon2016) repo in the [`dotnet-packer`](https://github.com/dotnet/MVPSummitHackathon2016/tree/master/dotnet-packer) project.</span></span>

## <a name="see-also"></a><span data-ttu-id="dc126-196">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="dc126-196">See also</span></span>

- [<span data-ttu-id="dc126-197">Installare .NET Core</span><span class="sxs-lookup"><span data-stu-id="dc126-197">Install .NET Core</span></span>](../install/index.md)
- [<span data-ttu-id="dc126-198">Come usare gli SDK di progetto MSBuild</span><span class="sxs-lookup"><span data-stu-id="dc126-198">How to use MSBuild project SDKs</span></span>](/visualstudio/msbuild/how-to-use-project-sdk)
- [<span data-ttu-id="dc126-199">Creare pacchetti di destinazioni e oggetti personalizzati MSBuild con NuGet</span><span class="sxs-lookup"><span data-stu-id="dc126-199">Package custom MSBuild targets and props with NuGet</span></span>](/nuget/create-packages/creating-a-package#include-msbuild-props-and-targets-in-a-package)

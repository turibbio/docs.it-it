---
title: Panoramica dello strumento WCF svcutil
description: Panoramica dello strumento Microsoft WCF dotnet-svcutil che aggiunge funzionalità per i progetti .NET Core e ASP.NET Core, come lo strumento WCF svcutil per i progetti .NET Framework.
author: mlacouture
ms.date: 02/22/2019
ms.openlocfilehash: fde42f7d040fba91f51ce6faa58282ed0206a853
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396212"
---
# <a name="wcf-dotnet-svcutil-tool-for-net-core"></a><span data-ttu-id="d30ff-103">Strumento WCF dotnet-svcutil per .NET Core</span><span class="sxs-lookup"><span data-stu-id="d30ff-103">WCF dotnet-svcutil tool for .NET Core</span></span>

<span data-ttu-id="d30ff-104">Lo strumento **DotNet-svcutil** Windows Communication Foundation (WCF) è uno strumento .NET che consente di recuperare metadati da un servizio Web in un percorso di rete o da un file WSDL e genera una classe WCF contenente metodi proxy client che accedono alle operazioni del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="d30ff-104">The Windows Communication Foundation (WCF) **dotnet-svcutil** tool is a .NET tool that retrieves metadata from a web service on a network location or from a WSDL file, and generates a WCF class containing client proxy methods that access the web service operations.</span></span>

<span data-ttu-id="d30ff-105">Analogo allo strumento [**Service Model Metadata - svcutil**](../../framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per i progetti .NET Framework, **dotnet-svcutil** è uno strumento da riga di comando per la generazione di un riferimento al servizio Web compatibile con i progetti .NET Core e .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="d30ff-105">Similar to the [**Service Model Metadata - svcutil**](../../framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) tool for .NET Framework projects, the **dotnet-svcutil** is a command-line tool for generating a web service reference compatible with .NET Core and .NET Standard projects.</span></span>

<span data-ttu-id="d30ff-106">Lo strumento **DotNet-Svcutil** è un'opzione alternativa al [**servizio Web WCF riferimento**](wcf-web-service-reference-guide.md) al provider di servizi connessi di Visual Studio, fornito per la prima volta con Visual Studio 2017 versione 15,5.</span><span class="sxs-lookup"><span data-stu-id="d30ff-106">The **dotnet-svcutil** tool is an alternative option to the [**WCF Web Service Reference**](wcf-web-service-reference-guide.md) Visual Studio connected service provider that first shipped with Visual Studio 2017 version 15.5.</span></span> <span data-ttu-id="d30ff-107">Lo strumento **DotNet-Svcutil** come strumento .NET è disponibile su più piattaforme in Linux, MacOS e Windows.</span><span class="sxs-lookup"><span data-stu-id="d30ff-107">The **dotnet-svcutil** tool as a .NET tool, is available cross-platform on Linux, macOS, and Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d30ff-108">Si consiglia di fare riferimento solo a servizi provenienti da un'origine attendibile.</span><span class="sxs-lookup"><span data-stu-id="d30ff-108">You should only reference services from a trusted source.</span></span> <span data-ttu-id="d30ff-109">L'aggiunta di riferimenti da un'origine non attendibile può compromettere la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d30ff-109">Adding references from an untrusted source may compromise security.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d30ff-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d30ff-110">Prerequisites</span></span>

<!-- markdownlint-disable MD025 -->

# <a name="dotnet-svcutil-2x"></a>[<span data-ttu-id="d30ff-111">dotnet-svcutil 2.x</span><span class="sxs-lookup"><span data-stu-id="d30ff-111">dotnet-svcutil 2.x</span></span>](#tab/dotnetsvcutil2x)

- <span data-ttu-id="d30ff-112">[.NET Core 2,1 SDK](https://dotnet.microsoft.com/download) o versioni successive</span><span class="sxs-lookup"><span data-stu-id="d30ff-112">[.NET Core 2.1 SDK](https://dotnet.microsoft.com/download) or later versions</span></span>
- <span data-ttu-id="d30ff-113">Editor di codice preferito</span><span class="sxs-lookup"><span data-stu-id="d30ff-113">Your favorite code editor</span></span>

# <a name="dotnet-svcutil-1x"></a>[<span data-ttu-id="d30ff-114">dotnet-svcutil 1.x</span><span class="sxs-lookup"><span data-stu-id="d30ff-114">dotnet-svcutil 1.x</span></span>](#tab/dotnetsvcutil1x)

- <span data-ttu-id="d30ff-115">[.NET Core 1.0.4 SDK](https://dotnet.microsoft.com/download) o versioni successive</span><span class="sxs-lookup"><span data-stu-id="d30ff-115">[.NET Core 1.0.4 SDK](https://dotnet.microsoft.com/download) or later versions</span></span>
- <span data-ttu-id="d30ff-116">Editor di codice preferito</span><span class="sxs-lookup"><span data-stu-id="d30ff-116">Your favorite code editor</span></span>

---

## <a name="getting-started"></a><span data-ttu-id="d30ff-117">Guida introduttiva</span><span class="sxs-lookup"><span data-stu-id="d30ff-117">Getting started</span></span>

<span data-ttu-id="d30ff-118">L'esempio seguente illustra la procedura necessaria per aggiungere un riferimento al servizio Web a un progetto Web .NET Core e richiamare il servizio.</span><span class="sxs-lookup"><span data-stu-id="d30ff-118">The following example walks you through the steps required to add a web service reference to a .NET Core web project and invoke the service.</span></span> <span data-ttu-id="d30ff-119">Si creerà un'applicazione Web .NET Core denominata *HelloSvcutil* e verrà aggiunto un riferimento a un servizio Web che implementa il contratto seguente:</span><span class="sxs-lookup"><span data-stu-id="d30ff-119">You'll create a .NET Core web application named *HelloSvcutil* and add a reference to a web service that implements the following contract:</span></span>

```csharp
[ServiceContract]
public interface ISayHello
{
    [OperationContract]
    string Hello(string name);
}
```

<span data-ttu-id="d30ff-120">In questo esempio si presuppone che il servizio Web sia ospitato all'indirizzo seguente: `http://contoso.com/SayHello.svc`</span><span class="sxs-lookup"><span data-stu-id="d30ff-120">For this example, let's assume the web service will be hosted at the following address: `http://contoso.com/SayHello.svc`</span></span>

<span data-ttu-id="d30ff-121">Da una finestra di comando di Windows, macOS o Linux eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d30ff-121">From a Windows, macOS, or Linux command window perform the following steps:</span></span>

1. <span data-ttu-id="d30ff-122">Creare una directory denominata _HelloSvcutil_ per il progetto e renderla la directory corrente, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d30ff-122">Create a directory named _HelloSvcutil_ for your project and make it your current directory, as in the following example:</span></span>

    ```console
    mkdir HelloSvcutil
    cd HelloSvcutil
    ```

2. <span data-ttu-id="d30ff-123">Creare un nuovo progetto Web C# in tale directory usando il [`dotnet new`](../tools/dotnet-new.md) comando come segue:</span><span class="sxs-lookup"><span data-stu-id="d30ff-123">Create a new C# web project in that directory using the [`dotnet new`](../tools/dotnet-new.md) command as follows:</span></span>

    ```dotnetcli
    dotnet new web
    ```

3. <span data-ttu-id="d30ff-124">Installare il [ `dotnet-svcutil` pacchetto NuGet](https://nuget.org/packages/dotnet-svcutil) come strumento dell'interfaccia della riga di comando: </span><span class="sxs-lookup"><span data-stu-id="d30ff-124">Install the [`dotnet-svcutil` NuGet package](https://nuget.org/packages/dotnet-svcutil) as a CLI tool:  </span></span><!-- markdownlint-disable MD023 -->
    # <a name="dotnet-svcutil-2x"></a>[<span data-ttu-id="d30ff-125">dotnet-svcutil 2.x</span><span class="sxs-lookup"><span data-stu-id="d30ff-125">dotnet-svcutil 2.x</span></span>](#tab/dotnetsvcutil2x)

    ```dotnetcli
    dotnet tool install --global dotnet-svcutil
    ```

    # <a name="dotnet-svcutil-1x"></a>[<span data-ttu-id="d30ff-126">dotnet-svcutil 1.x</span><span class="sxs-lookup"><span data-stu-id="d30ff-126">dotnet-svcutil 1.x</span></span>](#tab/dotnetsvcutil1x)
    <span data-ttu-id="d30ff-127">Aprire il `HelloSvcutil.csproj` file di progetto nell'editor, modificare l' `Project` elemento e aggiungere il [ `dotnet-svcutil` pacchetto NuGet](https://nuget.org/packages/dotnet-svcutil) come riferimento allo strumento dell'interfaccia della riga di comando usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d30ff-127">Open the `HelloSvcutil.csproj` project file in your editor, edit the `Project` element, and add the [`dotnet-svcutil` NuGet package](https://nuget.org/packages/dotnet-svcutil) as a CLI tool reference, using the following code:</span></span>

    ```xml
    <ItemGroup>
      <DotNetCliToolReference Include="dotnet-svcutil" Version="1.0.*" />
    </ItemGroup>
    ```

    <span data-ttu-id="d30ff-128">Ripristinare quindi il pacchetto _dotnet-svcutil_ usando il comando [`dotnet restore`](../tools/dotnet-restore.md) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d30ff-128">Then restore the _dotnet-svcutil_ package using the [`dotnet restore`](../tools/dotnet-restore.md) command as follows:</span></span>

    ```dotnetcli
    dotnet restore
    ```

    ---

4. <span data-ttu-id="d30ff-129">Eseguire il comando _dotnet-svcutil_ per generare il file di riferimento al servizio Web come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d30ff-129">Run the _dotnet-svcutil_ command to generate the web service reference file as follows:</span></span>

    # <a name="dotnet-svcutil-2x"></a>[<span data-ttu-id="d30ff-130">dotnet-svcutil 2.x</span><span class="sxs-lookup"><span data-stu-id="d30ff-130">dotnet-svcutil 2.x</span></span>](#tab/dotnetsvcutil2x)

    ```dotnetcli
    dotnet-svcutil http://contoso.com/SayHello.svc
    ```

    # <a name="dotnet-svcutil-1x"></a>[<span data-ttu-id="d30ff-131">dotnet-svcutil 1.x</span><span class="sxs-lookup"><span data-stu-id="d30ff-131">dotnet-svcutil 1.x</span></span>](#tab/dotnetsvcutil1x)

    ```dotnetcli
    dotnet svcutil http://contoso.com/SayHello.svc
    ```

    ---

<span data-ttu-id="d30ff-132">Il file generato viene salvato come _HelloSvcutil/ServiceReference/Reference.cs_.</span><span class="sxs-lookup"><span data-stu-id="d30ff-132">The generated file is saved as _HelloSvcutil/ServiceReference/Reference.cs_.</span></span> <span data-ttu-id="d30ff-133">Lo strumento _dotnet-svcutil_ aggiunge inoltre al progetto i pacchetti WCF appropriati richiesti dal codice del proxy come riferimenti ai pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d30ff-133">The _dotnet-svcutil_ tool also adds to the project the appropriate WCF packages required by the proxy code as package references.</span></span>

## <a name="using-the-service-reference"></a><span data-ttu-id="d30ff-134">Uso del riferimento al servizio</span><span class="sxs-lookup"><span data-stu-id="d30ff-134">Using the Service Reference</span></span>

1. <span data-ttu-id="d30ff-135">Ripristinare i pacchetti WCF utilizzando il [`dotnet restore`](../tools/dotnet-restore.md) comando come segue:</span><span class="sxs-lookup"><span data-stu-id="d30ff-135">Restore the WCF packages using the [`dotnet restore`](../tools/dotnet-restore.md) command as follows:</span></span>

    ```dotnetcli
    dotnet restore
    ```

2. <span data-ttu-id="d30ff-136">Trovare il nome della classe client e dell'operazione da usare.</span><span class="sxs-lookup"><span data-stu-id="d30ff-136">Find the name of the client class and operation you want to use.</span></span> <span data-ttu-id="d30ff-137">`Reference.cs` conterrà una classe che eredita da `System.ServiceModel.ClientBase`, con i metodi che possono essere usati per chiamare operazioni sul servizio.</span><span class="sxs-lookup"><span data-stu-id="d30ff-137">`Reference.cs` will contain a class that inherits from `System.ServiceModel.ClientBase`, with methods that can be used to call operations on the service.</span></span> <span data-ttu-id="d30ff-138">In questo esempio si vuole chiamare l'operazione _Hello_ del servizio _SayHello_.</span><span class="sxs-lookup"><span data-stu-id="d30ff-138">In this example, you want to call the _SayHello_ service's _Hello_ operation.</span></span> <span data-ttu-id="d30ff-139">`ServiceReference.SayHelloClient` è il nome della classe client e ha un metodo chiamato `HelloAsync` che può essere usato per chiamare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="d30ff-139">`ServiceReference.SayHelloClient` is the name of the client class, and has a method called `HelloAsync` that can be used to call the operation.</span></span>

3. <span data-ttu-id="d30ff-140">Aprire il `Startup.cs` file nell'editor e aggiungere una `using` direttiva per lo spazio dei nomi del riferimento al servizio nella parte superiore:</span><span class="sxs-lookup"><span data-stu-id="d30ff-140">Open the `Startup.cs` file in your editor, and add a `using` directive for the service reference namespace at the top:</span></span>

    ```csharp
    using ServiceReference;
    ```

4. <span data-ttu-id="d30ff-141">Modificare il metodo `Configure` per richiamare il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="d30ff-141">Edit the `Configure` method to invoke the web service.</span></span> <span data-ttu-id="d30ff-142">Per eseguire questa operazione, creare un'istanza della classe che eredita da `ClientBase` e chiamare il metodo sull'oggetto client:</span><span class="sxs-lookup"><span data-stu-id="d30ff-142">You do this by creating an instance of the class that inherits from `ClientBase` and calling the method on the client object:</span></span>

    ```csharp
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }

        app.Run(async (context) =>
        {
            var client = new SayHelloClient();
            var response = await client.HelloAsync();
            await context.Response.WriteAsync(response);
        });
    }

    ```

5. <span data-ttu-id="d30ff-143">Eseguire l'applicazione usando il [`dotnet run`](../tools/dotnet-run.md) comando come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d30ff-143">Run the application using the [`dotnet run`](../tools/dotnet-run.md) command as follows:</span></span>

    ```dotnetcli
    dotnet run
    ```

6. <span data-ttu-id="d30ff-144">Passare all'URL elencato nella console di (ad esempio, `http://localhost:5000`) nel Web browser.</span><span class="sxs-lookup"><span data-stu-id="d30ff-144">Navigate to the URL listed in the console (for example, `http://localhost:5000`) in your web browser.</span></span>

<span data-ttu-id="d30ff-145">Si dovrebbe vedere l'output seguente: "Hello dotnet-svcutil!"</span><span class="sxs-lookup"><span data-stu-id="d30ff-145">You should see the following output: "Hello dotnet-svcutil!"</span></span>

<span data-ttu-id="d30ff-146">Per una descrizione dettagliata dei parametri dello strumento `dotnet-svcutil`, richiamare lo strumento passando il parametro help come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d30ff-146">For a detailed description of the `dotnet-svcutil` tool parameters, invoke the tool passing the help parameter as follows:</span></span>
# <a name="dotnet-svcutil-2x"></a>[<span data-ttu-id="d30ff-147">dotnet-svcutil 2.x</span><span class="sxs-lookup"><span data-stu-id="d30ff-147">dotnet-svcutil 2.x</span></span>](#tab/dotnetsvcutil2x)

```dotnetcli
dotnet-svcutil --help
```

# <a name="dotnet-svcutil-1x"></a>[<span data-ttu-id="d30ff-148">dotnet-svcutil 1.x</span><span class="sxs-lookup"><span data-stu-id="d30ff-148">dotnet-svcutil 1.x</span></span>](#tab/dotnetsvcutil1x)

```dotnetcli
dotnet svcutil --help
```

---

## <a name="feedback--questions"></a><span data-ttu-id="d30ff-149">Commenti, suggerimenti e domande</span><span class="sxs-lookup"><span data-stu-id="d30ff-149">Feedback & questions</span></span>

<span data-ttu-id="d30ff-150">In caso di domande o commenti e suggerimenti, [segnalare un problema in GitHub](https://github.com/dotnet/wcf/issues/new).</span><span class="sxs-lookup"><span data-stu-id="d30ff-150">If you have any questions or feedback, [open an issue on GitHub](https://github.com/dotnet/wcf/issues/new).</span></span> <span data-ttu-id="d30ff-151">È anche possibile rivedere domande o problemi esistenti [nel repository WCF in GitHub](https://github.com/dotnet/wcf/issues?utf8=%E2%9C%93&q=is:issue%20label:tooling).</span><span class="sxs-lookup"><span data-stu-id="d30ff-151">You can also review any existing questions or issues [at the WCF repo on GitHub](https://github.com/dotnet/wcf/issues?utf8=%E2%9C%93&q=is:issue%20label:tooling).</span></span>

## <a name="release-notes"></a><span data-ttu-id="d30ff-152">Note sulla versione</span><span class="sxs-lookup"><span data-stu-id="d30ff-152">Release notes</span></span>

- <span data-ttu-id="d30ff-153">Fare riferimento alle [note sulla versione](https://github.com/dotnet/wcf/blob/master/release-notes/dotnet-svcutil-notes.md) per informazioni aggiornate sulle versioni, compresi i problemi noti.</span><span class="sxs-lookup"><span data-stu-id="d30ff-153">Refer to the [Release notes](https://github.com/dotnet/wcf/blob/master/release-notes/dotnet-svcutil-notes.md) for updated release information, including known issues.</span></span>

## <a name="information"></a><span data-ttu-id="d30ff-154">Informazioni</span><span class="sxs-lookup"><span data-stu-id="d30ff-154">Information</span></span>

- [<span data-ttu-id="d30ff-155">Pacchetto NuGet dotnet-svcutil</span><span class="sxs-lookup"><span data-stu-id="d30ff-155">dotnet-svcutil NuGet Package</span></span>](https://nuget.org/packages/dotnet-svcutil)

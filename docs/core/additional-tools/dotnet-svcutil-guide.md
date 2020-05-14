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
# <a name="wcf-dotnet-svcutil-tool-for-net-core"></a>Strumento WCF dotnet-svcutil per .NET Core

Lo strumento **DotNet-svcutil** Windows Communication Foundation (WCF) è uno strumento .NET che consente di recuperare metadati da un servizio Web in un percorso di rete o da un file WSDL e genera una classe WCF contenente metodi proxy client che accedono alle operazioni del servizio Web.

Analogo allo strumento [**Service Model Metadata - svcutil**](../../framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) per i progetti .NET Framework, **dotnet-svcutil** è uno strumento da riga di comando per la generazione di un riferimento al servizio Web compatibile con i progetti .NET Core e .NET Standard.

Lo strumento **DotNet-Svcutil** è un'opzione alternativa al [**servizio Web WCF riferimento**](wcf-web-service-reference-guide.md) al provider di servizi connessi di Visual Studio, fornito per la prima volta con Visual Studio 2017 versione 15,5. Lo strumento **DotNet-Svcutil** come strumento .NET è disponibile su più piattaforme in Linux, MacOS e Windows.

> [!IMPORTANT]
> Si consiglia di fare riferimento solo a servizi provenienti da un'origine attendibile. L'aggiunta di riferimenti da un'origine non attendibile può compromettere la sicurezza.

## <a name="prerequisites"></a>Prerequisiti

<!-- markdownlint-disable MD025 -->

# <a name="dotnet-svcutil-2x"></a>[dotnet-svcutil 2.x](#tab/dotnetsvcutil2x)

- [.NET Core 2,1 SDK](https://dotnet.microsoft.com/download) o versioni successive
- Editor di codice preferito

# <a name="dotnet-svcutil-1x"></a>[dotnet-svcutil 1.x](#tab/dotnetsvcutil1x)

- [.NET Core 1.0.4 SDK](https://dotnet.microsoft.com/download) o versioni successive
- Editor di codice preferito

---

## <a name="getting-started"></a>Guida introduttiva

L'esempio seguente illustra la procedura necessaria per aggiungere un riferimento al servizio Web a un progetto Web .NET Core e richiamare il servizio. Si creerà un'applicazione Web .NET Core denominata *HelloSvcutil* e verrà aggiunto un riferimento a un servizio Web che implementa il contratto seguente:

```csharp
[ServiceContract]
public interface ISayHello
{
    [OperationContract]
    string Hello(string name);
}
```

In questo esempio si presuppone che il servizio Web sia ospitato all'indirizzo seguente: `http://contoso.com/SayHello.svc`

Da una finestra di comando di Windows, macOS o Linux eseguire la procedura seguente:

1. Creare una directory denominata _HelloSvcutil_ per il progetto e renderla la directory corrente, come nell'esempio seguente:

    ```console
    mkdir HelloSvcutil
    cd HelloSvcutil
    ```

2. Creare un nuovo progetto Web C# in tale directory usando il [`dotnet new`](../tools/dotnet-new.md) comando come segue:

    ```dotnetcli
    dotnet new web
    ```

3. Installare il [ `dotnet-svcutil` pacchetto NuGet](https://nuget.org/packages/dotnet-svcutil) come strumento dell'interfaccia della riga di comando: <!-- markdownlint-disable MD023 -->
    # <a name="dotnet-svcutil-2x"></a>[dotnet-svcutil 2.x](#tab/dotnetsvcutil2x)

    ```dotnetcli
    dotnet tool install --global dotnet-svcutil
    ```

    # <a name="dotnet-svcutil-1x"></a>[dotnet-svcutil 1.x](#tab/dotnetsvcutil1x)
    Aprire il `HelloSvcutil.csproj` file di progetto nell'editor, modificare l' `Project` elemento e aggiungere il [ `dotnet-svcutil` pacchetto NuGet](https://nuget.org/packages/dotnet-svcutil) come riferimento allo strumento dell'interfaccia della riga di comando usando il codice seguente:

    ```xml
    <ItemGroup>
      <DotNetCliToolReference Include="dotnet-svcutil" Version="1.0.*" />
    </ItemGroup>
    ```

    Ripristinare quindi il pacchetto _dotnet-svcutil_ usando il comando [`dotnet restore`](../tools/dotnet-restore.md) come indicato di seguito:

    ```dotnetcli
    dotnet restore
    ```

    ---

4. Eseguire il comando _dotnet-svcutil_ per generare il file di riferimento al servizio Web come indicato di seguito:

    # <a name="dotnet-svcutil-2x"></a>[dotnet-svcutil 2.x](#tab/dotnetsvcutil2x)

    ```dotnetcli
    dotnet-svcutil http://contoso.com/SayHello.svc
    ```

    # <a name="dotnet-svcutil-1x"></a>[dotnet-svcutil 1.x](#tab/dotnetsvcutil1x)

    ```dotnetcli
    dotnet svcutil http://contoso.com/SayHello.svc
    ```

    ---

Il file generato viene salvato come _HelloSvcutil/ServiceReference/Reference.cs_. Lo strumento _dotnet-svcutil_ aggiunge inoltre al progetto i pacchetti WCF appropriati richiesti dal codice del proxy come riferimenti ai pacchetti.

## <a name="using-the-service-reference"></a>Uso del riferimento al servizio

1. Ripristinare i pacchetti WCF utilizzando il [`dotnet restore`](../tools/dotnet-restore.md) comando come segue:

    ```dotnetcli
    dotnet restore
    ```

2. Trovare il nome della classe client e dell'operazione da usare. `Reference.cs` conterrà una classe che eredita da `System.ServiceModel.ClientBase`, con i metodi che possono essere usati per chiamare operazioni sul servizio. In questo esempio si vuole chiamare l'operazione _Hello_ del servizio _SayHello_. `ServiceReference.SayHelloClient` è il nome della classe client e ha un metodo chiamato `HelloAsync` che può essere usato per chiamare l'operazione.

3. Aprire il `Startup.cs` file nell'editor e aggiungere una `using` direttiva per lo spazio dei nomi del riferimento al servizio nella parte superiore:

    ```csharp
    using ServiceReference;
    ```

4. Modificare il metodo `Configure` per richiamare il servizio Web. Per eseguire questa operazione, creare un'istanza della classe che eredita da `ClientBase` e chiamare il metodo sull'oggetto client:

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

5. Eseguire l'applicazione usando il [`dotnet run`](../tools/dotnet-run.md) comando come indicato di seguito:

    ```dotnetcli
    dotnet run
    ```

6. Passare all'URL elencato nella console di (ad esempio, `http://localhost:5000`) nel Web browser.

Si dovrebbe vedere l'output seguente: "Hello dotnet-svcutil!"

Per una descrizione dettagliata dei parametri dello strumento `dotnet-svcutil`, richiamare lo strumento passando il parametro help come indicato di seguito:
# <a name="dotnet-svcutil-2x"></a>[dotnet-svcutil 2.x](#tab/dotnetsvcutil2x)

```dotnetcli
dotnet-svcutil --help
```

# <a name="dotnet-svcutil-1x"></a>[dotnet-svcutil 1.x](#tab/dotnetsvcutil1x)

```dotnetcli
dotnet svcutil --help
```

---

## <a name="feedback--questions"></a>Commenti, suggerimenti e domande

In caso di domande o commenti e suggerimenti, [segnalare un problema in GitHub](https://github.com/dotnet/wcf/issues/new). È anche possibile rivedere domande o problemi esistenti [nel repository WCF in GitHub](https://github.com/dotnet/wcf/issues?utf8=%E2%9C%93&q=is:issue%20label:tooling).

## <a name="release-notes"></a>Note sulla versione

- Fare riferimento alle [note sulla versione](https://github.com/dotnet/wcf/blob/master/release-notes/dotnet-svcutil-notes.md) per informazioni aggiornate sulle versioni, compresi i problemi noti.

## <a name="information"></a>Informazioni

- [Pacchetto NuGet dotnet-svcutil](https://nuget.org/packages/dotnet-svcutil)

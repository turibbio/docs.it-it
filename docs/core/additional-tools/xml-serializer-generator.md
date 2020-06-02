---
title: Strumento Microsoft per la generazione di serializzatori XML
description: Panoramica dello strumento Microsoft per la generazione di serializzatori XML. Usare lo strumento per la generazione di serializzatori XML per generare un assembly di serializzazione XML per i tipi contenuti nel progetto.
author: mlacouture
ms.date: 01/19/2017
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: efa0925a96fcdd4356109632fa77199edde73c26
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84284286"
---
# <a name="using-microsoft-xml-serializer-generator-on-net-core"></a>Uso dello strumento Microsoft per la generazione di serializzatori XML in .NET Core

In questa esercitazione viene illustrato come usare lo strumento Microsoft per la generazione di serializzatori XML in un'applicazione .NET Core di C#. Nel corso di questa esercitazione verranno illustrate le attività seguenti:

> [!div class="checklist"]
>
> - Come creare un'app .NET Core
> - Come aggiungere un riferimento al pacchetto Microsoft.XmlSerializer.Generator
> - Come modificare il file MyApp.cspro per aggiungere dipendenze
> - Come aggiungere una classe e un oggetto XmlSerializer
> - Come compilare ed eseguire l'applicazione

Lo [strumento per la generazione di serializzatori XML (sgen.exe)](../../standard/serialization/xml-serializer-generator-tool-sgen-exe.md) è la soluzione per .NET Framework, mentre il [pacchetto NuGet Microsoft.XmlSerializer.Generator](https://www.nuget.org/packages/Microsoft.XmlSerializer.Generator) è la soluzione equivalente per NET Core e .NET Standard. Crea un assembly di serializzazione XML per tipi contenuti in un assembly per migliorare le prestazioni di avvio della serializzazione XML durante la serializzazione o deserializzazione di oggetti di questi tipi usando <xref:System.Xml.Serialization.XmlSerializer>.

## <a name="prerequisites"></a>Prerequisiti

Per completare questa esercitazione:

- [.NET Core 2,1 SDK](https://dotnet.microsoft.com/download) o versione successiva.
- Editor di codice preferito.

> [!TIP]
> È necessario installare un editor del codice? Provare [Visual Studio](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).

## <a name="use-microsoft-xml-serializer-generator-in-a-net-core-console-application"></a>Usare lo strumento Microsoft per la generazione di serializzatori XML in un'applicazione console .NET Core

Le istruzioni seguenti illustrano come usare lo strumento per la generazione di serializzatori XML in un'applicazione console .NET Core.

### <a name="create-a-net-core-console-application"></a>Creare un'applicazione console .NET Core

Aprire un prompt dei comandi e creare una cartella denominata *MyApp*. Passare alla cartella creata e digitare il comando seguente:

```dotnetcli
dotnet new console
```

### <a name="add-a-reference-to-the-microsoftxmlserializergenerator-package-in-the-myapp-project"></a>Aggiungere un riferimento al pacchetto Microsoft.XmlSerializer.Generator nel progetto MyApp

Usare il [`dotnet add package`](../tools/dotnet-add-package.md) comando per aggiungere il riferimento nel progetto.

Digitare:

```dotnetcli
dotnet add package Microsoft.XmlSerializer.Generator -v 1.0.0
```

### <a name="verify-changes-to-myappcsproj-after-adding-the-package"></a>Verificare le modifiche a MyApp.csproj dopo aver aggiunto il pacchetto

Prima di iniziare, aprire l'editor del codice. Si lavorerà ancora dalla directory *MyApp* in cui è stata compilata l'app.

Aprire *MyApp.csproj* nell'editor di testo.

Dopo aver eseguito il [`dotnet add package`](../tools/dotnet-add-package.md) comando, vengono aggiunte le righe seguenti al file di progetto *MyApp. csproj* :

 ```xml
 <ItemGroup>
    <PackageReference Include="Microsoft.XmlSerializer.Generator" Version="1.0.0" />
 </ItemGroup>
 ```

### <a name="add-another-itemgroup-section-for-net-core-cli-tool-support"></a>Aggiungere un'altra sezione denominata ItemGroup per il supporto dello strumento dell'interfaccia della riga di comando .NET Core

Aggiungere le righe seguenti dopo la sezione `ItemGroup` analizzata:

 ```xml
 <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.XmlSerializer.Generator" Version="1.0.0" />
 </ItemGroup>
 ```

### <a name="add-a-class-in-the-application"></a>Aggiungere una classe nell'applicazione

Aprire *Program.cs* nell'editor di testo. Aggiungere la classe denominata *MyClass* in *Program.cs*.

```csharp
public class MyClass
{
   public int Value;
}
```

### <a name="create-an-xmlserializer-for-myclass"></a>Creare un oggetto `XmlSerializer` per MyClass

Aggiungere la riga seguente in *Main* per creare un oggetto `XmlSerializer` per MyClass:

```csharp
var serializer = new System.Xml.Serialization.XmlSerializer(typeof(MyClass));
```

### <a name="build-and-run-the-application"></a>Compilare ed eseguire l'applicazione

Sempre all'interno della cartella *MyApp* , eseguire l'applicazione tramite [`dotnet run`](../tools/dotnet-run.md) e carica automaticamente e usa i serializzatori pre-generati in fase di esecuzione.

Nella finestra di console digitare il comando seguente:

```dotnetcli
dotnet run
```

> [!NOTE]
> [`dotnet run`](../tools/dotnet-run.md)chiama [`dotnet build`](../tools/dotnet-build.md) per assicurarsi che le destinazioni di compilazione siano state compilate e quindi chiama `dotnet <assembly.dll>` per eseguire l'applicazione di destinazione.

> [!IMPORTANT]
> I comandi e i passaggi illustrati in questa esercitazione per eseguire l'applicazione vengono usati solo durante la fase di sviluppo. Quando si è pronti a distribuire l'app, è opportuno esaminare le diverse [strategie di distribuzione](../deploying/index.md) per le app .NET Core e il comando [`dotnet publish`](../tools/dotnet-publish.md).

Se è stato eseguito tutto correttamente, un assembly denominato *MyApp.XmlSerializers.dll* viene generato nella cartella di output.

Congratulazioni! Sono state eseguite le attività seguenti:
> [!div class="checklist"]
>
> - Creazione di un'app .NET Core.
> - Aggiunta di un riferimento al pacchetto Microsoft.XmlSerializer.Generator.
> - Modifica del file MyApp.cspro per l'aggiunta di dipendenze.
> - Aggiunta di una classe e un oggetto XmlSerializer.
> - Compilazione ed esecuzione dell'applicazione.

## <a name="related-resources"></a>Risorse correlate

- [Introduzione alla serializzazione XML](../../standard/serialization/introducing-xml-serialization.md)
- [Come serializzare tramite XmlSerializer (C#)](../../csharp/programming-guide/concepts/linq/how-to-serialize-using-xmlserializer.md)
- [Procedura: Serializzare tramite XmlSerializer (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/how-to-serialize-using-xmlserializer.md)

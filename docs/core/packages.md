---
title: Pacchetti, metapacchetti e Framework-.NET Core
description: Informazioni sulla terminologia relativa a pacchetti, metapacchetti e framework.
author: richlander
ms.date: 04/29/2020
ms.openlocfilehash: a6575226feb71b96f1fe5070406c118081a8cbf0
ms.sourcegitcommit: d7666f6e49c57a769612602ea7857b927294ce47
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/30/2020
ms.locfileid: "82595585"
---
# <a name="packages-metapackages-and-frameworks"></a>Pacchetti, metapacchetti e framework

.NET Core è una piattaforma costituita da pacchetti NuGet. Alcuni prodotti traggono vantaggio da una definizione dei pacchetti con granularità fine, mentre altri da una definizione con granularità più grossolana. Per supportare questa dualità, .NET Core viene distribuito come set di pacchetti con granularità fine e in blocchi più grossolani con un tipo di pacchetto denominato in modo informale da un [metapacchetto](#metapackages).

Ognuno dei pacchetti .NET Core supporta l'esecuzione su più implementazioni di .NET, rappresentate come Framework. Alcuni di questi Framework sono Framework tradizionali, come `net46`, che rappresenta il .NET Framework. Un altro insieme è costituito da nuovi framework che possono essere considerati come "framework basati su pacchetti", il che stabilisce un nuovo modello di definizione dei framework stessi. Questi framework basati su pacchetti sono interamente creati e definiti come pacchetti, creando una relazione forte tra pacchetti e Framework.

## <a name="packages"></a>Pacchetti

.NET Core è suddiviso in un set di pacchetti che forniscono primitive, tipi di dati di livello superiore, tipi di composizione delle app e utilità comuni. Ognuno di questi pacchetti rappresenta un singolo assembly con lo stesso nome. Ad esempio, il [pacchetto System. Runtime](https://www.nuget.org/packages/System.Runtime) contiene System. Runtime. dll.

La definizione dei pacchetti con granularità fine presenta alcuni vantaggi:

- I pacchetti con granularità fine possono essere distribuiti in base a una specifica pianificazione, con operazioni di test di altri pacchetti relativamente limitate.
- I pacchetti con granularità fine possono fornire supporto per diversi sistemi operativi e CPU.
- I pacchetti con granularità fine possono avere dipendenze specifiche da una sola libreria.
- Le app hanno dimensioni ridotte perché i pacchetti senza riferimenti non diventano parte della distribuzione delle app stesse.

Alcuni di questi vantaggi vengono sfruttati solo in particolari circostanze. I pacchetti .NET Core, ad esempio, possono essere distribuiti in base alla stessa pianificazione con lo stesso supporto di piattaforma. Nel caso di interventi di manutenzione, le correzioni possono essere distribuite e installate come piccoli aggiornamenti di singoli pacchetti. A causa del ristretto ambito di modifica, le operazioni di convalida e il tempo necessario per rendere una correzione disponibile sono limitati a quanto necessario per una singola libreria.

Di seguito è riportato un elenco dei principali pacchetti NuGet per .NET Core:

- [System. Runtime](https://www.nuget.org/packages/System.Runtime) : il pacchetto .NET Core più fondamentale, tra <xref:System.Object>cui <xref:System.String>, <xref:System.Array>, <xref:System.Action>, e <xref:System.Collections.Generic.IList%601>.
- [System.Collections](https://www.nuget.org/packages/System.Collections): set di raccolte essenzialmente generiche, che include <xref:System.Collections.Generic.List%601> e <xref:System.Collections.Generic.Dictionary%602>.
- [System.Net.Http](https://www.nuget.org/packages/System.Net.Http): set di tipi per la comunicazione di rete HTTP, che include <xref:System.Net.Http.HttpClient> e <xref:System.Net.Http.HttpResponseMessage>.
- [System.IO.FileSystem](https://www.nuget.org/packages/System.IO.FileSystem): set di tipi per la lettura e la scrittura in sistemi di archiviazione basati su dischi locali o di rete, che include <xref:System.IO.File> e <xref:System.IO.Directory>.
- [System.Linq](https://www.nuget.org/packages/System.Linq): set di tipi per le query su oggetti, che include `Enumerable` e <xref:System.Linq.ILookup%602>.
- [System. Reflection](https://www.nuget.org/packages/System.Reflection) : set di tipi per il caricamento, l'ispezione e l'attivazione di tipi, <xref:System.Reflection.Assembly>tra <xref:System.Reflection.TypeInfo> cui <xref:System.Reflection.MethodInfo>e.

In genere, anziché includere ogni pacchetto, è più semplice e affidabile includere un [metapacchetto](#metapackages). Tuttavia, se è necessario usare un singolo pacchetto, è possibile includerlo come mostrato nell'esempio seguente, che fa riferimento al pacchetto [System.Runtime](https://www.nuget.org/packages/System.Runtime/).

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard1.6</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="System.Runtime" Version="4.3.0" />
  </ItemGroup>
</Project>
```

## <a name="metapackages"></a>Metapacchetti

Un metapacchetto è una convenzione di pacchetti NuGet per descrivere un set di pacchetti che sono significativi insieme. Un metapacchetto rappresenta questo set di pacchetti rendendoli le dipendenze. Il metapacchetto può facoltativamente definire un Framework per il set di pacchetti specificando un Framework.

Per impostazione predefinita, le versioni precedenti degli strumenti di .NET Core (strumenti basati su *Project. JSON* e * \*. csproj* ) specificano sia un Framework che un metapacchetto. Il framework di destinazione fa attualmente riferimento in modo implicito al metapacchetto, in modo che ogni metapacchetto sia associato a un framework di destinazione. Ad esempio, il `netstandard1.6` Framework fa riferimento al metapacchetto NETStandard. Library versione 1.6.0. Analogamente, il framework `netcoreapp2.1` fa riferimento al metapacchetto Microsoft.NETCore.App versione 2.1.0. Per altre informazioni, vedere [Implicit metapackage package reference in the .NET Core SDK](https://github.com/dotnet/core/blob/master/release-notes/1.0/sdk/1.0-rc3-implicit-package-refs.md) (Riferimento implicito a un pacchetto di un metapacchetto in .NET Core SDK).

La destinazione di un Framework e il riferimento implicito a un metapacchetto significa che, in effetti, si aggiunge un riferimento a ogni pacchetto dipendente come singolo gesto. Ciò rende disponibili tutte le librerie incluse nei pacchetti per IntelliSense (o metodi simili) e per la pubblicazione dell'app.

L'uso dei metapacchetti presenta i vantaggi seguenti:

- Fornisce un'esperienza utente che consente di fare facilmente riferimento a un elevato numero di pacchetti con granularità fine.
- Definisce un set di pacchetti (incluse versioni specifiche) che vengono testati e funzionano bene insieme.

Il metapacchetto di .NET Standard è:

- [NETStandard. Library](https://www.nuget.org/packages/NETStandard.Library) : descrive le librerie che fanno parte di .NET standard. Si applica a tutte le implementazioni di .NET che supportano .NET Standard, ad esempio .NET Framework, .NET Core e mono. Stabilisce il `netstandard` Framework.

I metapacchetti principali di .NET Core sono:

- [Microsoft.NETCore.App](https://www.nuget.org/packages/Microsoft.NETCore.App): descrive le librerie che fanno parte della distribuzione .NET Core. Stabilisce il `.NETCoreApp` Framework. Dipende dalla `NETStandard.Library` di minori dimensioni.
- [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.App): include tutti i pacchetti supportati da ASP.NET Core ed Entity Framework Core, ad eccezione di quelli che contengono dipendenze di terze parti. Per altre informazioni, vedere [Metapacchetto Microsoft.AspNetCore.All per ASP.NET Core](/aspnet/core/fundamentals/metapackage-app).
- [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) - Include tutti i pacchetti supportati da ASP.NET Core, Entity Framework Core e dipendenze interne e di terze parti usate da ASP.NET Core ed Entity Framework Core. Per altre informazioni, vedere [Metapacchetto Microsoft.AspNetCore.All per ASP.NET Core 2.x](/aspnet/core/fundamentals/metapackage).
- [Microsoft.NETCore.Portable.Compatibility](https://www.nuget.org/packages/Microsoft.NETCore.Portable.Compatibility): set di caratteristiche di compatibilità che abilitano l'esecuzione in .NET Core di librerie di classi portabili basate su mscorlib.

## <a name="frameworks"></a>Framework

Ogni pacchetto di .NET Core supporta un set di framework di runtime. I framework descrivono un set di API disponibili (e potenzialmente altre caratteristiche) che è possibile usare quando si definisce un determinato framework come destinazione. Vengono sottoposti al controllo delle versioni quando si aggiungono nuove API.

Ad esempio, [System.IO.FileSystem](https://www.nuget.org/packages/System.IO.FileSystem) supporta i framework seguenti:

- .NETFramework, versione 4.6
- .NETStandard,versione 1.3
- 6 piattaforme Xamarin, ad esempio xamarinios10

È utile confrontare i primi due di questi Framework, in quanto sono esempi dei due diversi modi di definire i Framework:

- Il `.NETFramework,Version=4.6` Framework rappresenta le API disponibili nella .NET Framework 4,6. È possibile creare librerie compilate con gli assembly di riferimento .NET Framework 4,6 e quindi distribuire tali librerie in pacchetti NuGet in una cartella ' net46 lib. Verrà usato per le app destinate a .NET Framework 4,6 o compatibili con esso. Quella sopra descritta è la tradizionale modalità di funzionamento dei framework.

- `.NETStandard,Version=1.3` è un framework basato su pacchetti. Si basa su pacchetti che hanno come destinazione il framework per definire ed esporre le API in termini di framework.

## <a name="package-based-frameworks"></a>Framework basati su pacchetti

Tra i framework e i pacchetti è presente una relazione bidirezionale. La prima parte consiste nella definizione delle API disponibili per un determinato framework, ad esempio `netstandard1.3`. I pacchetti che hanno come destinazione `netstandard1.3` (o framework compatibili quali `netstandard1.0`) definiscono le API disponibili per `netstandard1.3`. Può sembrare una definizione circolare, ma non lo è. Poiché è basato su pacchetti, la definizione delle API per il framework deriva dai pacchetti. Il framework stesso non definisce alcuna API.

La seconda parte della relazione è la selezione delle risorse. I pacchetti possono contenere risorse per più framework. Dato un riferimento a un set di pacchetti e/o metapacchetti, il framework è necessario per determinare quale risorsa deve essere selezionata, ad esempio `net46` o `netstandard1.3`. È importante selezionare la risorsa corretta. Ad esempio, è improbabile che una risorsa `net46` sia compatibile con .NET Framework 4.0 o .NET Core 1.0.

La relazione è illustrata nella figura seguente. L'*API* identifica il *framework* come destinazione e lo definisce. Il *framework* viene usato per la *selezione delle risorse*. La *risorsa* fornisce l'API.

![Composizione dei framework basati su pacchetti](./media/packages/package-framework.png)

I due principali framework basati su pacchetti usati con .NET Core sono i seguenti:

- `netstandard`
- `netcoreapp`

### <a name="net-standard"></a>.NET Standard

Il Framework di .NET standard ([moniker Framework di destinazione](../standard/frameworks.md): `netstandard`) rappresenta le API definite da e compilate sopra [.NET standard](../standard/net-standard.md). Le librerie che devono essere eseguite in più runtime devono avere come destinazione questo framework. Saranno supportati in qualsiasi runtime conforme a .NET Standard, ad esempio .NET Core, .NET Framework e mono/Novell. Ciascuno di questi runtime supporta un set di versioni di .NET Standard, a seconda delle API implementate.

Il `netstandard` Framework fa riferimento in modo [`NETStandard.Library`](https://www.nuget.org/packages/NETStandard.Library) implicito al metapacchetto. Ad esempio, il file di progetto MSBuild seguente indica che il progetto `netstandard1.6`è destinato a, che fa riferimento al metapacchetto della [ `NETStandard.Library` versione 1,6](https://www.nuget.org/packages/NETStandard.Library/1.6.0) .

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard1.6</TargetFramework>
  </PropertyGroup>
</Project>
```

Aggiungendo l' `<NetStandardImplicitPackageVersion>` elemento al file di progetto, che specifica in modo implicito una versione del metapacchetto, è possibile specificare una versione del Framework inferiore alla versione del metapacchetto. L' `<NetStandardImplicitPackageVersion>` elemento è applicabile solo quando la destinazione è .NET Core e .NET standard. Ad esempio, il file di progetto seguente è valido.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard1.3</TargetFramework>
    <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
  </PropertyGroup>
</Project>
```

Può sembrare strano definire come destinazione `netstandard1.3` ma usare la versione 1.6.0 della `NETStandard.Library`. Si tratta di un caso di uso valido, dal momento che il metapacchetto mantiene il supporto per le precedenti versioni di `netstandard`. Può trattarsi di una situazione in cui è stata definita come standard la versione 1.6.0 del pacchetto e tale versione è stata usata per tutte le librerie, che hanno come destinazione un'ampia gamma di versioni di `netstandard`. Con questo approccio, è sufficiente ripristinare `NETStandard.Library` 1.6.0 e non le versioni precedenti.

La situazione opposta, ovvero la definizione di `netstandard1.6` come destinazione con la versione 1.3.0 della `NETStandard.Library`, non è valida. Non è possibile definire come destinazione la versione più recente di un framework con una versione precedente di un metapacchetto. La versione precedente del metapacchetto, infatti, non espone alcuna risorsa per la versione più recente del framework. Lo schema di controllo delle versioni per i metapacchetti impone che questi ultimi siano di una versione più recente del framework che descrivono. In base a questo schema di versionamento, la prima versione della `NETStandard.Library` è la 1.6.0, dato che contiene le risorse `netstandard1.6`. Per la simmetria con l'esempio precedente, v 1.3.0 viene usato qui, ma in realtà non esiste.

### <a name="net-core-application"></a>Applicazione .NET Core

Il Framework .NET Core ([moniker Framework](../standard/frameworks.md)di `netcoreapp`destinazione:) rappresenta i pacchetti e le API associate fornite con la distribuzione di .NET Core e il modello di applicazione console fornito. Le app .NET Core devono usare questo framework poiché hanno come destinazione il modello dell'applicazione console. Devono usare questo framework anche le librerie da eseguire solo in .NET Core. L'uso di questo framework impone che le app e le librerie vengano eseguite solo in .NET Core.

Il metapacchetto `Microsoft.NETCore.App` ha come destinazione il framework `netcoreapp`. Consente l'accesso a circa 60 librerie, circa 40 fornite dal pacchetto `NETStandard.Library` e le rimanenti 20 in aggiunta. È possibile fare riferimento a librerie aggiuntive che hanno come destinazione `netcoreapp` o framework compatibili, ad esempio `netstandard`, per ottenere l'accesso ad altre API.

Anche la maggior parte delle librerie fornite da `Microsoft.NETCore.App` ha come destinazione `netstandard`, dato che le relative dipendenze sono soddisfatte da altre librerie `netstandard`. Questo significa che anche le librerie `netstandard` possono fare riferimento a tali pacchetti come dipendenze.

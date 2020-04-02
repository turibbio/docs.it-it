---
title: Scrivere un semplice programma parallelo usando Parallel.ForEach
ms.date: 02/14/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- foreach, parallel version
- parallel programming, foreach
ms.assetid: cb5fab92-1c19-499e-ae91-8b7525dd875f
ms.openlocfilehash: 0300f8900cd18159ba3a2170cfba96f302f282a0
ms.sourcegitcommit: 961ec21c22d2f1d55c9cc8a7edf2ade1d1fd92e3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80588147"
---
# <a name="how-to-write-a-simple-parallelforeach-loop"></a><span data-ttu-id="ac13b-102">Procedura: scrivere un ciclo Parallel.ForEach sempliceHow to: Write a simple Parallel.ForEach loop</span><span class="sxs-lookup"><span data-stu-id="ac13b-102">How to: Write a simple Parallel.ForEach loop</span></span>

<span data-ttu-id="ac13b-103">Questo esempio mostra come usare un ciclo <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> per abilitare il parallelismo dei dati in un'origine dati <xref:System.Collections.IEnumerable?displayProperty=nameWithType> o <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="ac13b-103">This example shows how to use a <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> loop to enable data parallelism over any <xref:System.Collections.IEnumerable?displayProperty=nameWithType> or <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> data source.</span></span>

> [!NOTE]
> <span data-ttu-id="ac13b-104">Le espressioni lambda sono usate nella documentazione per definire i delegati in PLINQ.</span><span class="sxs-lookup"><span data-stu-id="ac13b-104">This documentation uses lambda expressions to define delegates in PLINQ.</span></span> <span data-ttu-id="ac13b-105">Se non si ha familiarità con le espressioni lambda in C# o Visual Basic, vedere [Espressioni lambda in PLINQ e TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md).</span><span class="sxs-lookup"><span data-stu-id="ac13b-105">If you are not familiar with lambda expressions in C# or Visual Basic, see [Lambda expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md).</span></span>

## <a name="example"></a><span data-ttu-id="ac13b-106">Esempio</span><span class="sxs-lookup"><span data-stu-id="ac13b-106">Example</span></span>

<span data-ttu-id="ac13b-107">Questo esempio presuppone che diversi file con estensione jpg siano presenti in una cartella *C:\Users\Public\Pictures\Sample Pictures* e crea una nuova sottocartella con nome *Modified*.</span><span class="sxs-lookup"><span data-stu-id="ac13b-107">This example assumes you have several .jpg files in a *C:\Users\Public\Pictures\Sample Pictures* folder and creates a new sub-folder named *Modified*.</span></span> <span data-ttu-id="ac13b-108">Quando si esegue l'esempio, il codice ruota ogni immagine con estensione jpg in *Sample Pictures* e la salva in *Modified*.</span><span class="sxs-lookup"><span data-stu-id="ac13b-108">When you run the example, it rotates each .jpg image in *Sample Pictures* and saves it to *Modified*.</span></span> <span data-ttu-id="ac13b-109">È possibile modificare i due percorsi in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="ac13b-109">You can modify the two paths as necessary.</span></span>

[!code-csharp[TPL_Parallel#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/simpleforeach.cs#03)]
[!code-vb[TPL_Parallel#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/simpleforeach.vb#03)]

<span data-ttu-id="ac13b-110">Un ciclo <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> funziona come un ciclo <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="ac13b-110">A <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> loop works like a <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> loop.</span></span> <span data-ttu-id="ac13b-111">Il ciclo esegue il partizionamento della raccolta di origine e pianifica il lavoro in più thread in base all'ambiente di sistema.</span><span class="sxs-lookup"><span data-stu-id="ac13b-111">The loop partitions the source collection and schedules the work on multiple threads based on the system environment.</span></span> <span data-ttu-id="ac13b-112">Più processori ci sono nel sistema, più velocemente viene eseguito il metodo parallelo.</span><span class="sxs-lookup"><span data-stu-id="ac13b-112">The more processors on the system, the faster the parallel method runs.</span></span> <span data-ttu-id="ac13b-113">Per alcune raccolte di origine può risultare più veloce un ciclo sequenziale, a seconda delle dimensioni dell'origine e del tipo di attività svolta dal ciclo.</span><span class="sxs-lookup"><span data-stu-id="ac13b-113">For some source collections, a sequential loop may be faster, depending on the size of the source and the kind of work the loop performs.</span></span> <span data-ttu-id="ac13b-114">Per ulteriori informazioni sulle prestazioni, vedere [Potenziali insidie nei dati e nel parallelismo delle attività](potential-pitfalls-in-data-and-task-parallelism.md).</span><span class="sxs-lookup"><span data-stu-id="ac13b-114">For more information about performance, see [Potential pitfalls in data and task parallelism](potential-pitfalls-in-data-and-task-parallelism.md).</span></span>

<span data-ttu-id="ac13b-115">Per ulteriori informazioni sui cicli paralleli, vedere [Procedura: scrivere un ciclo Parallel.For semplice.](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-for-loop.md)</span><span class="sxs-lookup"><span data-stu-id="ac13b-115">For more information about parallel loops, see [How to: Write a simple Parallel.For loop](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-for-loop.md).</span></span>

<span data-ttu-id="ac13b-116">Per usare <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> con una raccolta non generica, è possibile usare il metodo di estensione <xref:System.Linq.Enumerable.Cast%2A?displayProperty=nameWithType> per convertire la raccolta in una generica, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="ac13b-116">To use <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> with a non-generic collection, you can use the <xref:System.Linq.Enumerable.Cast%2A?displayProperty=nameWithType> extension method to convert the collection to a generic collection, as shown in the following example:</span></span>

[!code-csharp[TPL_Parallel#07](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/nongeneric.cs#07)]
[!code-vb[TPL_Parallel#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/nongeneric.vb#07)]

<span data-ttu-id="ac13b-117">È anche possibile usare Parallel LINQ (PLINQ) per parallelizzare l'elaborazione di origini dati <xref:System.Collections.Generic.IEnumerable%601>.</span><span class="sxs-lookup"><span data-stu-id="ac13b-117">You can also use Parallel LINQ (PLINQ) to parallelize processing of <xref:System.Collections.Generic.IEnumerable%601> data sources.</span></span> <span data-ttu-id="ac13b-118">PLINQ consente di usare la sintassi di query dichiarativa per esprimere il comportamento di ciclo.</span><span class="sxs-lookup"><span data-stu-id="ac13b-118">PLINQ enables you to use declarative query syntax to express the loop behavior.</span></span> <span data-ttu-id="ac13b-119">Per altre informazioni, vedere [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/introduction-to-plinq.md).</span><span class="sxs-lookup"><span data-stu-id="ac13b-119">For more information, see [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/introduction-to-plinq.md).</span></span>

## <a name="compile-and-run-the-code"></a><span data-ttu-id="ac13b-120">Compilare ed eseguire il codice</span><span class="sxs-lookup"><span data-stu-id="ac13b-120">Compile and run the code</span></span>

<span data-ttu-id="ac13b-121">È possibile compilare il codice come applicazione console per .NET Framework o come applicazione console per .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ac13b-121">You can compile the code as a console application for .NET Framework or as a console application for .NET Core.</span></span>

<span data-ttu-id="ac13b-122">In Visual Studio esistono modelli di applicazione console Visual Basic e C# per Windows Desktop e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ac13b-122">In Visual Studio, there are Visual Basic and C# console application templates for Windows Desktop and .NET Core.</span></span>

<span data-ttu-id="ac13b-123">Dalla riga di comando è possibile utilizzare i comandi dell'interfaccia della riga di comando di .NET Core, `dotnet new console` ad esempio oppure `dotnet new console -lang vb`oppure , oppure è possibile creare il file e utilizzare il compilatore della riga di comando per un'applicazione .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ac13b-123">From the command line, you can use either the .NET Core CLI commands (for example, `dotnet new console` or `dotnet new console -lang vb`), or you can create the file and use the command-line compiler for a .NET Framework application.</span></span>

<span data-ttu-id="ac13b-124">Per un progetto .NET Core è necessario fare riferimento al pacchetto NuGet **System.Drawing.Common**.</span><span class="sxs-lookup"><span data-stu-id="ac13b-124">For a .NET Core project, you must reference the **System.Drawing.Common** NuGet package.</span></span> <span data-ttu-id="ac13b-125">In Visual Studio usare Gestione pacchetti NuGet per installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="ac13b-125">In Visual Studio, use the NuGet Package Manager to install the package.</span></span> <span data-ttu-id="ac13b-126">In alternativa, è possibile aggiungere un riferimento al pacchetto nel file con estensione \*.csproj o \*.vbproj:</span><span class="sxs-lookup"><span data-stu-id="ac13b-126">Alternatively, you can add a reference to the package in your \*.csproj or \*.vbproj file:</span></span>

```xml
<ItemGroup>
     <PackageReference Include="System.Drawing.Common" Version="4.5.1" />
</ItemGroup>
```

<span data-ttu-id="ac13b-127">Per eseguire un'applicazione console .NET Core dalla riga di comando, usare `dotnet run` dalla cartella che contiene l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ac13b-127">To run a .NET Core console application from the command line, use `dotnet run` from the folder that contains your application.</span></span>

<span data-ttu-id="ac13b-128">Per eseguire l'applicazione console da Visual Studio, premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="ac13b-128">To run your console application from Visual Studio, press **F5**.</span></span>

## <a name="see-also"></a><span data-ttu-id="ac13b-129">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ac13b-129">See also</span></span>

- [<span data-ttu-id="ac13b-130">Parallelismo dei dati</span><span class="sxs-lookup"><span data-stu-id="ac13b-130">Data parallelism</span></span>](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)
- [<span data-ttu-id="ac13b-131">Programmazione parallela</span><span class="sxs-lookup"><span data-stu-id="ac13b-131">Parallel programming</span></span>](../../../docs/standard/parallel-programming/index.md)
- [<span data-ttu-id="ac13b-132">Parallel LINQ (PLINQ)</span><span class="sxs-lookup"><span data-stu-id="ac13b-132">Parallel LINQ (PLINQ)</span></span>](../../../docs/standard/parallel-programming/introduction-to-plinq.md)

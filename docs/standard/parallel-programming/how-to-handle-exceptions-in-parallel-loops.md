---
title: 'Procedura: Gestire le eccezioni nei cicli paralleli'
description: Informazioni su come gestire le eccezioni nei cicli paralleli in .NET. Vedere un esempio di come eseguire il wrapping di tutte le eccezioni dal ciclo in un oggetto System. AggregateException.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel loops, how to handle exceptions
ms.assetid: 512f0d5a-4636-4875-b766-88f20044f143
ms.openlocfilehash: 61c22d6e82282f8aeb54818c813d4489e3bc9641
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768976"
---
# <a name="how-to-handle-exceptions-in-parallel-loops"></a><span data-ttu-id="327d1-104">Procedura: Gestire le eccezioni nei cicli paralleli</span><span class="sxs-lookup"><span data-stu-id="327d1-104">How to: Handle Exceptions in Parallel Loops</span></span>
<span data-ttu-id="327d1-105">Gli overload dei metodi <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> e <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> non presentano alcun meccanismo speciale per gestire le eccezioni eventualmente generate.</span><span class="sxs-lookup"><span data-stu-id="327d1-105">The <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> and <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> overloads do not have any special mechanism to handle exceptions that might be thrown.</span></span> <span data-ttu-id="327d1-106">In questo senso, sono simili ai `for` cicli e ai `foreach` cicli ( `For` e `For Each` in Visual Basic); un'eccezione non gestita causa la terminazione del ciclo non appena tutte le iterazioni attualmente in esecuzione vengono completate.</span><span class="sxs-lookup"><span data-stu-id="327d1-106">In this respect, they resemble regular `for` and `foreach` loops (`For` and `For Each` in Visual Basic); an unhandled exception causes the loop to terminate as soon as all currently running iterations finish.</span></span>
  
 <span data-ttu-id="327d1-107">Quando si aggiunge una logica personalizzata di gestione delle eccezioni nei cicli paralleli, gestire il caso della generazione simultanea di eccezioni simili in più thread e il caso in cui un'eccezione generata in un determinato thread comporta la generazione di un'altra eccezione in un altro thread.</span><span class="sxs-lookup"><span data-stu-id="327d1-107">When you add your own exception-handling logic to parallel loops, handle the case in which similar exceptions might be thrown on multiple threads concurrently, and the case in which an exception thrown on one thread causes another exception to be thrown on another thread.</span></span> <span data-ttu-id="327d1-108">Per gestire entrambi questi casi è possibile eseguire il wrapping di tutte le eccezioni del ciclo in un oggetto <xref:System.AggregateException?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="327d1-108">You can handle both cases by wrapping all exceptions from the loop in a <xref:System.AggregateException?displayProperty=nameWithType>.</span></span> <span data-ttu-id="327d1-109">L'esempio seguente mostra uno degli approcci possibili.</span><span class="sxs-lookup"><span data-stu-id="327d1-109">The following example shows one possible approach.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="327d1-110">Quando "Just My Code" è abilitato, Visual Studio in alcuni casi si interromperà in corrispondenza della riga che genera l'eccezione e visualizzerà un messaggio di errore simile a "Eccezione non gestita dal codice utente".</span><span class="sxs-lookup"><span data-stu-id="327d1-110">When "Just My Code" is enabled, Visual Studio in some cases will break on the line that throws the exception and display an error message that says "exception not handled by user code."</span></span> <span data-ttu-id="327d1-111">Questo errore non è grave.</span><span class="sxs-lookup"><span data-stu-id="327d1-111">This error is benign.</span></span> <span data-ttu-id="327d1-112">È possibile premere F5 per continuare e osservare il comportamento di gestione delle eccezioni illustrato negli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="327d1-112">You can press F5 to continue from it, and see the exception-handling behavior that is demonstrated in the example below.</span></span> <span data-ttu-id="327d1-113">Per impedire l'interruzione di Visual Studio al primo errore, deselezionare semplicemente la casella di controllo "Just My Code" in **Strumenti, Opzioni, Debug, Generale**.</span><span class="sxs-lookup"><span data-stu-id="327d1-113">To prevent Visual Studio from breaking on the first error, just uncheck the "Just My Code" checkbox under **Tools, Options, Debugging, General**.</span></span>  
  
## <a name="example"></a><span data-ttu-id="327d1-114">Esempio</span><span class="sxs-lookup"><span data-stu-id="327d1-114">Example</span></span>  
 <span data-ttu-id="327d1-115">In questo esempio vengono rilevate tutte le eccezioni e quindi ne viene eseguito il wrapping in un oggetto <xref:System.AggregateException?displayProperty=nameWithType> che viene generato.</span><span class="sxs-lookup"><span data-stu-id="327d1-115">In this example, all exceptions are caught and then wrapped in an <xref:System.AggregateException?displayProperty=nameWithType> which is thrown.</span></span> <span data-ttu-id="327d1-116">Il chiamante può decidere quali eccezioni gestire.</span><span class="sxs-lookup"><span data-stu-id="327d1-116">The caller can decide which exceptions to handle.</span></span>  
  
 [!code-csharp[TPL_Exceptions#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/exceptions.cs#08)]
 [!code-vb[TPL_Exceptions#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/exceptionsinloops.vb#08)]  
  
## <a name="see-also"></a><span data-ttu-id="327d1-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="327d1-117">See also</span></span>

- [<span data-ttu-id="327d1-118">Parallelismo dei dati</span><span class="sxs-lookup"><span data-stu-id="327d1-118">Data Parallelism</span></span>](data-parallelism-task-parallel-library.md)
- [<span data-ttu-id="327d1-119">Espressioni lambda in PLINQ e TPL</span><span class="sxs-lookup"><span data-stu-id="327d1-119">Lambda Expressions in PLINQ and TPL</span></span>](lambda-expressions-in-plinq-and-tpl.md)

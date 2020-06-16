---
title: "Procedura: Restituire un valore da un'attività"
description: Vedere come usare il tipo System. Threading. Tasks. Task <TResult> per restituire un valore dalla proprietà Result in .NET.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to return a value
ms.assetid: c4bc0f44-eba2-4e96-9e03-1cc787461e61
ms.openlocfilehash: 051cef7cac654e4369ec1486884876004370ba0b
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2020
ms.locfileid: "84767975"
---
# <a name="how-to-return-a-value-from-a-task"></a><span data-ttu-id="b5ac4-103">Procedura: Restituire un valore da un'attività</span><span class="sxs-lookup"><span data-stu-id="b5ac4-103">How to: Return a Value from a Task</span></span>
<span data-ttu-id="b5ac4-104">In questo esempio viene illustrato come usare il tipo <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> per restituire un valore dalla proprietà <xref:System.Threading.Tasks.Task%601.Result%2A>.</span><span class="sxs-lookup"><span data-stu-id="b5ac4-104">This example shows how to use the <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> type to return a value from the <xref:System.Threading.Tasks.Task%601.Result%2A> property.</span></span> <span data-ttu-id="b5ac4-105">È necessaria la presenza della directory C:\Users\Public\Pictures\Sample Pictures\ e che in essa siano contenuti dei file.</span><span class="sxs-lookup"><span data-stu-id="b5ac4-105">It requires that the C:\Users\Public\Pictures\Sample Pictures\ directory exists, and that it contains files.</span></span>  
  
## <a name="example"></a><span data-ttu-id="b5ac4-106">Esempio</span><span class="sxs-lookup"><span data-stu-id="b5ac4-106">Example</span></span>  
 [!code-csharp[TPL#10](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/returnavalue10.cs#10)]
 [!code-vb[TPL#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/10_returnavalue.vb#10)]  
  
 <span data-ttu-id="b5ac4-107">La proprietà <xref:System.Threading.Tasks.Task%601.Result%2A> blocca il thread chiamante fino al termine dell'attività.</span><span class="sxs-lookup"><span data-stu-id="b5ac4-107">The <xref:System.Threading.Tasks.Task%601.Result%2A> property blocks the calling thread until the task finishes.</span></span>  
  
 <span data-ttu-id="b5ac4-108">Per informazioni su come passare il risultato di un oggetto <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> a un'attività di continuazione, vedere [Concatenamento di attività tramite attività di continuazione](chaining-tasks-by-using-continuation-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="b5ac4-108">To see how to pass the result of one <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> to a continuation task, see [Chaining Tasks by Using Continuation Tasks](chaining-tasks-by-using-continuation-tasks.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b5ac4-109">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b5ac4-109">See also</span></span>

- [<span data-ttu-id="b5ac4-110">Programmazione asincrona basata su attività</span><span class="sxs-lookup"><span data-stu-id="b5ac4-110">Task-based Asynchronous Programming</span></span>](task-based-asynchronous-programming.md)
- [<span data-ttu-id="b5ac4-111">Espressioni lambda in PLINQ e TPL</span><span class="sxs-lookup"><span data-stu-id="b5ac4-111">Lambda Expressions in PLINQ and TPL</span></span>](lambda-expressions-in-plinq-and-tpl.md)

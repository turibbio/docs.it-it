---
title: 'Procedura: implementare un client del modello asincrono basato su eventi'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- components [.NET Framework], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 21a858c1-3c99-4904-86ee-0d17b49804fa
ms.openlocfilehash: f834ce4a0ec2208eee80ce8c3ffebfa6fdeeb5b1
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289408"
---
# <a name="how-to-implement-a-client-of-the-event-based-asynchronous-pattern"></a><span data-ttu-id="a81a5-102">Procedura: implementare un client del modello asincrono basato su eventi</span><span class="sxs-lookup"><span data-stu-id="a81a5-102">How to: Implement a Client of the Event-based Asynchronous Pattern</span></span>
<span data-ttu-id="a81a5-103">L'esempio di codice seguente mostra come usare un componente che aderisce a quanto indicato in [Panoramica del modello asincrono basato su eventi](event-based-asynchronous-pattern-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a81a5-103">The following code example demonstrates how to use a component that adheres to the [Event-based Asynchronous Pattern Overview](event-based-asynchronous-pattern-overview.md).</span></span> <span data-ttu-id="a81a5-104">Il form per questo esempio usa il componente `PrimeNumberCalculator` descritto in [Procedura: Implementare un componente che supporta il modello asincrono basato su eventi](component-that-supports-the-event-based-asynchronous-pattern.md).</span><span class="sxs-lookup"><span data-stu-id="a81a5-104">The form for this example uses the `PrimeNumberCalculator` component described in [How to: Implement a Component That Supports the Event-based Asynchronous Pattern](component-that-supports-the-event-based-asynchronous-pattern.md).</span></span>  
  
 <span data-ttu-id="a81a5-105">Quando si esegue un progetto che usa questo esempio, viene visualizzato un form "Calcolatrice di numeri primi" con una griglia e due pulsanti: **Avvia nuova attività** e **Annulla**.</span><span class="sxs-lookup"><span data-stu-id="a81a5-105">When you run a project that uses this example, you will see a "Prime Number Calculator" form with a grid and two buttons: **Start New Task** and **Cancel**.</span></span> <span data-ttu-id="a81a5-106">È possibile fare clic sul pulsante **Avvia nuova attività** più volte in successione. Per ogni clic, un'operazione asincrona avvierà un calcolo per determinare se un numero di test generato in modo casuale è un numero primo.</span><span class="sxs-lookup"><span data-stu-id="a81a5-106">You can click the **Start New Task** button several times in succession, and for each click, an asynchronous operation will begin a computation to determine if a randomly generated test number is prime.</span></span> <span data-ttu-id="a81a5-107">Il form visualizzerà periodicamente l'avanzamento e i risultati incrementali.</span><span class="sxs-lookup"><span data-stu-id="a81a5-107">The form will periodically display progress and incremental results.</span></span> <span data-ttu-id="a81a5-108">A ogni operazione viene assegnato un ID attività univoco.</span><span class="sxs-lookup"><span data-stu-id="a81a5-108">Each operation is assigned a unique task ID.</span></span> <span data-ttu-id="a81a5-109">Il risultato del calcolo viene visualizzato nella colonna **Risultato**. Se il numero di test non è un numero primo, viene contrassegnato come **Composito** e ne viene visualizzato il primo divisore.</span><span class="sxs-lookup"><span data-stu-id="a81a5-109">The result of the computation is displayed in the **Result** column; if the test number is not prime, it is labeled as **Composite,** and its first divisor is displayed.</span></span>  
  
 <span data-ttu-id="a81a5-110">Qualsiasi operazione in sospeso può essere annullata con il pulsante **Annulla**.</span><span class="sxs-lookup"><span data-stu-id="a81a5-110">Any pending operation can be canceled with the **Cancel** button.</span></span> <span data-ttu-id="a81a5-111">È possibile eseguire più selezioni.</span><span class="sxs-lookup"><span data-stu-id="a81a5-111">Multiple selections can be made.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="a81a5-112">La maggior parte dei numeri non sarà un numero primo.</span><span class="sxs-lookup"><span data-stu-id="a81a5-112">Most numbers will not be prime.</span></span> <span data-ttu-id="a81a5-113">Se non è stato trovato alcun numero primo dopo il completamento di diverse operazioni, avviare semplicemente altre attività e si finirà certamente per trovare alcuni numeri primi.</span><span class="sxs-lookup"><span data-stu-id="a81a5-113">If you have not found a prime number after several completed operations, simply start more tasks, and eventually you will find some prime numbers.</span></span>  
  
## <a name="example"></a><span data-ttu-id="a81a5-114">Esempio</span><span class="sxs-lookup"><span data-stu-id="a81a5-114">Example</span></span>  
 [!code-csharp[System.ComponentModel.AsyncOperationManager#10](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#10)]
 [!code-vb[System.ComponentModel.AsyncOperationManager#10](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#10)]  
  
## <a name="see-also"></a><span data-ttu-id="a81a5-115">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a81a5-115">See also</span></span>

- <xref:System.ComponentModel.AsyncOperation>
- <xref:System.ComponentModel.AsyncOperationManager>
- <xref:System.Windows.Forms.WindowsFormsSynchronizationContext>

---
title: MDA dangerousThreadingAPI
description: Esaminare l'assistente al debug gestito dangerousThreadingAPI, che viene attivato quando viene chiamato thread. Suspend su un thread diverso dal thread corrente.
ms.date: 03/30/2017
helpviewer_keywords:
- suspending threads
- DangerousThreadingAPI MDA
- managed debugging assistants (MDAs), dangerous threading operations
- threading [.NET Framework], suspending
- MDAs (managed debugging assistants), dangerous threading operations
- Suspend method
- threading [.NET Framework], managed debugging assistants
ms.assetid: 3e5efbc5-92e4-4229-b31f-ce368a1adb96
ms.openlocfilehash: 9069ccb6f106c83db94f88bc464bc0888d28586c
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85416005"
---
# <a name="dangerousthreadingapi-mda"></a><span data-ttu-id="7a685-103">MDA dangerousThreadingAPI</span><span class="sxs-lookup"><span data-stu-id="7a685-103">dangerousThreadingAPI MDA</span></span>
<span data-ttu-id="7a685-104">L'assistente al debug gestito `dangerousThreadingAPI` viene attivato quando il metodo <xref:System.Threading.Thread.Suspend%2A?displayProperty=nameWithType> viene chiamato per un thread diverso da quello attuale.</span><span class="sxs-lookup"><span data-stu-id="7a685-104">The `dangerousThreadingAPI` managed debugging assistant (MDA) is activated when the <xref:System.Threading.Thread.Suspend%2A?displayProperty=nameWithType> method is called on a thread other than the current thread.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="7a685-105">Sintomi</span><span class="sxs-lookup"><span data-stu-id="7a685-105">Symptoms</span></span>  
 <span data-ttu-id="7a685-106">Un'applicazione non risponde o si blocca per un tempo imprecisato.</span><span class="sxs-lookup"><span data-stu-id="7a685-106">An application is unresponsive or hangs indefinitely.</span></span> <span data-ttu-id="7a685-107">È possibile che i dati del sistema e dell'applicazione rimangano in uno stato non prevedibile temporaneamente o anche dopo la chiusura di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7a685-107">System or application data might be left in an unpredictable state temporarily or even after an application has been shut down.</span></span> <span data-ttu-id="7a685-108">Alcune operazioni non vengono completate come previsto.</span><span class="sxs-lookup"><span data-stu-id="7a685-108">Some operations are not completing as expected.</span></span>  
  
 <span data-ttu-id="7a685-109">I sintomi possono variare ampiamente a causa della casualità implicita nel problema.</span><span class="sxs-lookup"><span data-stu-id="7a685-109">Symptoms can vary widely due to the randomness inherent to the problem.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="7a685-110">Causa</span><span class="sxs-lookup"><span data-stu-id="7a685-110">Cause</span></span>  
 <span data-ttu-id="7a685-111">Un thread viene sospeso in modo asincrono da un altro thread tramite il metodo <xref:System.Threading.Thread.Suspend%2A>.</span><span class="sxs-lookup"><span data-stu-id="7a685-111">A thread is asynchronously suspended by another thread using the <xref:System.Threading.Thread.Suspend%2A> method.</span></span> <span data-ttu-id="7a685-112">Non c'è modo di stabilire se sia sicuro sospendere un altro thread che potrebbe avere un'operazione in corso.</span><span class="sxs-lookup"><span data-stu-id="7a685-112">There is no way to determine when it is safe to suspend another thread which might be in the middle of an operation.</span></span> <span data-ttu-id="7a685-113">La sospensione del thread può causare il danneggiamento dei dati o l'interruzione di invariabili.</span><span class="sxs-lookup"><span data-stu-id="7a685-113">Suspending the thread can result in the corruption of data or the breaking of invariants.</span></span> <span data-ttu-id="7a685-114">Se un thread viene sospeso e non viene mai ripreso tramite il metodo <xref:System.Threading.Thread.Resume%2A>, l'applicazione può bloccarsi per un tempo imprecisato, danneggiando i dati.</span><span class="sxs-lookup"><span data-stu-id="7a685-114">Should a thread be placed into a suspended state and never resumed using the <xref:System.Threading.Thread.Resume%2A> method, the application can hang indefinitely and possibly damage application data.</span></span> <span data-ttu-id="7a685-115">Questi metodi sono stati contrassegnati come obsoleti.</span><span class="sxs-lookup"><span data-stu-id="7a685-115">These methods have been marked as obsolete.</span></span>  
  
 <span data-ttu-id="7a685-116">Se le primitive di sincronizzazione si trovano nel thread di destinazione, vi rimarranno durante la sospensione,</span><span class="sxs-lookup"><span data-stu-id="7a685-116">If synchronization primitives are held by the target thread, they remain held during suspension.</span></span> <span data-ttu-id="7a685-117">con la possibilità di un deadlock se un altro thread, ad esempio quello che esegue il metodo <xref:System.Threading.Thread.Suspend%2A>, tenta di acquisire un blocco sulla primitiva.</span><span class="sxs-lookup"><span data-stu-id="7a685-117">This can lead to deadlocks should another thread, for example the thread performing the <xref:System.Threading.Thread.Suspend%2A>, attempt to acquire a lock on the primitive.</span></span> <span data-ttu-id="7a685-118">In questa situazione, il problema si manifesta sotto forma di deadlock.</span><span class="sxs-lookup"><span data-stu-id="7a685-118">In this situation, the problem manifests itself as a deadlock.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="7a685-119">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="7a685-119">Resolution</span></span>  
 <span data-ttu-id="7a685-120">Evitare progettazioni che richiedano l'uso di <xref:System.Threading.Thread.Suspend%2A> e <xref:System.Threading.Thread.Resume%2A>.</span><span class="sxs-lookup"><span data-stu-id="7a685-120">Avoid designs that require the use of <xref:System.Threading.Thread.Suspend%2A> and <xref:System.Threading.Thread.Resume%2A>.</span></span> <span data-ttu-id="7a685-121">Per l'interazione tra thread, usare le primitive di sincronizzazione, ad esempio <xref:System.Threading.Monitor>, <xref:System.Threading.ReaderWriterLock>, <xref:System.Threading.Mutex> o l'istruzione C# `lock`.</span><span class="sxs-lookup"><span data-stu-id="7a685-121">For cooperation between threads, use synchronization primitives such as <xref:System.Threading.Monitor>, <xref:System.Threading.ReaderWriterLock>, <xref:System.Threading.Mutex>, or the C# `lock` statement.</span></span> <span data-ttu-id="7a685-122">Se è necessario usare questi metodi, ridurre il periodo di tempo e la quantità di codice eseguito quando il thread si trova in uno stato di sospensione.</span><span class="sxs-lookup"><span data-stu-id="7a685-122">If you must use these methods, reduce the window of time and minimize the amount of code that executes while the thread is in a suspended state.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="7a685-123">Effetto sull'ambiente di esecuzione</span><span class="sxs-lookup"><span data-stu-id="7a685-123">Effect on the Runtime</span></span>  
 <span data-ttu-id="7a685-124">L'assistente al debug gestito non ha alcun effetto su CLR.</span><span class="sxs-lookup"><span data-stu-id="7a685-124">This MDA has no effect on the CLR.</span></span> <span data-ttu-id="7a685-125">Si limita a generare un report dei dati relativi alle operazioni di threading dannose.</span><span class="sxs-lookup"><span data-stu-id="7a685-125">It only reports data about dangerous threading operations.</span></span>  
  
## <a name="output"></a><span data-ttu-id="7a685-126">Output</span><span class="sxs-lookup"><span data-stu-id="7a685-126">Output</span></span>  
 <span data-ttu-id="7a685-127">L'assistente al debug gestito identifica il metodo di threading dannoso che ha causato l'attivazione dell'assistente stesso.</span><span class="sxs-lookup"><span data-stu-id="7a685-127">The MDA identifies the dangerous threading method that caused it to be activated.</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="7a685-128">Configurazione</span><span class="sxs-lookup"><span data-stu-id="7a685-128">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dangerousThreadingAPI />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a><span data-ttu-id="7a685-129">Esempio</span><span class="sxs-lookup"><span data-stu-id="7a685-129">Example</span></span>  
 <span data-ttu-id="7a685-130">Il codice di esempio seguente illustra una chiamata al metodo <xref:System.Threading.Thread.Suspend%2A> che causa l'attivazione di `dangerousThreadingAPI`.</span><span class="sxs-lookup"><span data-stu-id="7a685-130">The following code example demonstrates a call to the <xref:System.Threading.Thread.Suspend%2A> method that causes the activation of the `dangerousThreadingAPI`.</span></span>  
  
```csharp
using System.Threading;  
void FireMda()  
{  
Thread t = new Thread(delegate() { Thread.Sleep(1000); });  
    t.Start();  
    // The following line activates the MDA.  
    t.Suspend();
    t.Resume();  
    t.Join();  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="7a685-131">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="7a685-131">See also</span></span>

- <xref:System.Threading.Thread>
- [<span data-ttu-id="7a685-132">Diagnostica degli errori tramite gli assistenti al debug gestito</span><span class="sxs-lookup"><span data-stu-id="7a685-132">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
- [<span data-ttu-id="7a685-133">Istruzione lock</span><span class="sxs-lookup"><span data-stu-id="7a685-133">lock Statement</span></span>](../../csharp/language-reference/keywords/lock-statement.md)

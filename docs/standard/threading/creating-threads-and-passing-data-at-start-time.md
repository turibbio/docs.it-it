---
title: Creazione di thread e passaggio di dati all'avvio
description: Informazioni su come creare thread e passare i dati all'ora di inizio di un processo del sistema operativo in .NET.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- threading [.NET Framework], creating
- threading [.NET Framework], passing data to threads
- threading [.NET Framework], retrieving data from threads
ms.assetid: 52b32222-e185-4f42-91a7-eaca65c0ab6d
ms.openlocfilehash: 811028d3c853441ff3a61d3628a44e5c65ba7059
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2020
ms.locfileid: "84661914"
---
# <a name="creating-threads-and-passing-data-at-start-time"></a><span data-ttu-id="ae54d-103">Creazione di thread e passaggio di dati all'avvio</span><span class="sxs-lookup"><span data-stu-id="ae54d-103">Creating threads and passing data at start time</span></span>

<span data-ttu-id="ae54d-104">Quando viene creato un processo del sistema operativo, il sistema operativo inserisce un thread per eseguire il codice in tale processo, inclusi i domini dell'applicazione originali.</span><span class="sxs-lookup"><span data-stu-id="ae54d-104">When an operating-system process is created, the operating system injects a thread to execute code in that process, including any original application domain.</span></span> <span data-ttu-id="ae54d-105">Da quel momento, i domini dell'applicazione possono essere creati ed eliminati definitivamente senza dover creare o eliminare definitivamente i thread del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ae54d-105">From that point on, application domains can be created and destroyed without any operating system threads necessarily being created or destroyed.</span></span> <span data-ttu-id="ae54d-106">Se il codice eseguito è codice gestito, si può ottenere un oggetto <xref:System.Threading.Thread> per il thread in esecuzione nel dominio dell'applicazione corrente recuperando la proprietà statica <xref:System.Threading.Thread.CurrentThread%2A> di tipo <xref:System.Threading.Thread>.</span><span class="sxs-lookup"><span data-stu-id="ae54d-106">If the code being executed is managed code, then a <xref:System.Threading.Thread> object for the thread executing in the current application domain can be obtained by retrieving the static <xref:System.Threading.Thread.CurrentThread%2A> property of type <xref:System.Threading.Thread>.</span></span> <span data-ttu-id="ae54d-107">Questo argomento descrive la creazione dei thread e illustra le alternative per passare i dati alla routine del thread.</span><span class="sxs-lookup"><span data-stu-id="ae54d-107">This topic describes thread creation and discusses alternatives for passing data to the thread procedure.</span></span>  
  
## <a name="creating-a-thread"></a><span data-ttu-id="ae54d-108">Creazione di un thread</span><span class="sxs-lookup"><span data-stu-id="ae54d-108">Creating a thread</span></span>

 <span data-ttu-id="ae54d-109">La creazione di un nuovo oggetto <xref:System.Threading.Thread> crea un nuovo thread gestito.</span><span class="sxs-lookup"><span data-stu-id="ae54d-109">Creating a new <xref:System.Threading.Thread> object creates a new managed thread.</span></span> <span data-ttu-id="ae54d-110">La classe <xref:System.Threading.Thread> ha costruttori che accettano un delegato <xref:System.Threading.ThreadStart> o un delegato <xref:System.Threading.ParameterizedThreadStart>. Il delegato esegue il wrapping del metodo richiamato dal nuovo thread quando si chiama il metodo <xref:System.Threading.Thread.Start%2A>.</span><span class="sxs-lookup"><span data-stu-id="ae54d-110">The <xref:System.Threading.Thread> class has constructors that take a <xref:System.Threading.ThreadStart> delegate or a <xref:System.Threading.ParameterizedThreadStart> delegate; the delegate wraps the method that is invoked by the new thread when you call the <xref:System.Threading.Thread.Start%2A> method.</span></span> <span data-ttu-id="ae54d-111">Se si chiama <xref:System.Threading.Thread.Start%2A> più di una volta, viene generata un'eccezione <xref:System.Threading.ThreadStateException>.</span><span class="sxs-lookup"><span data-stu-id="ae54d-111">Calling <xref:System.Threading.Thread.Start%2A> more than once causes a <xref:System.Threading.ThreadStateException> to be thrown.</span></span>  
  
 <span data-ttu-id="ae54d-112">Il metodo <xref:System.Threading.Thread.Start%2A> restituisce il controllo immediatamente, spesso prima che il nuovo thread sia stato effettivamente avviato.</span><span class="sxs-lookup"><span data-stu-id="ae54d-112">The <xref:System.Threading.Thread.Start%2A> method returns immediately, often before the new thread has actually started.</span></span> <span data-ttu-id="ae54d-113">È possibile usare le proprietà <xref:System.Threading.Thread.ThreadState%2A> e <xref:System.Threading.Thread.IsAlive%2A> per determinare lo stato del thread in qualsiasi momento, ma è consigliabile non usare mai queste proprietà per la sincronizzazione delle attività dei thread.</span><span class="sxs-lookup"><span data-stu-id="ae54d-113">You can use the <xref:System.Threading.Thread.ThreadState%2A> and <xref:System.Threading.Thread.IsAlive%2A> properties to determine the state of the thread at any one moment, but these properties should never be used for synchronizing the activities of threads.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ae54d-114">Dopo che un thread è stato avviato, non è necessario mantenere un riferimento all'oggetto <xref:System.Threading.Thread>.</span><span class="sxs-lookup"><span data-stu-id="ae54d-114">Once a thread is started, it is not necessary to retain a reference to the <xref:System.Threading.Thread> object.</span></span> <span data-ttu-id="ae54d-115">Il thread continua l'esecuzione fino al termine della routine del thread.</span><span class="sxs-lookup"><span data-stu-id="ae54d-115">The thread continues to execute until the thread procedure ends.</span></span>  
  
 <span data-ttu-id="ae54d-116">L'esempio di codice seguente crea due nuovi thread per chiamare metodi di istanza e statici su un altro oggetto.</span><span class="sxs-lookup"><span data-stu-id="ae54d-116">The following code example creates two new threads to call instance and static methods on another object.</span></span>  
  
 [!code-cpp[System.Threading.ThreadStart2#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source2.cpp#2)]
 [!code-csharp[System.Threading.ThreadStart2#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source2.cs#2)]
 [!code-vb[System.Threading.ThreadStart2#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source2.vb#2)]  
  
## <a name="passing-data-to-threads"></a><span data-ttu-id="ae54d-117">Passaggio di dati ai thread</span><span class="sxs-lookup"><span data-stu-id="ae54d-117">Passing data to threads</span></span>

 <span data-ttu-id="ae54d-118">In .NET Framework versione 2.0 il delegato <xref:System.Threading.ParameterizedThreadStart> consente di passare facilmente un oggetto contenente dati da un thread quando si chiama l'overload del metodo <xref:System.Threading.Thread.Start%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="ae54d-118">In the .NET Framework version 2.0, the <xref:System.Threading.ParameterizedThreadStart> delegate provides an easy way to pass an object containing data to a thread when you call the <xref:System.Threading.Thread.Start%2A?displayProperty=nameWithType> method overload.</span></span> <span data-ttu-id="ae54d-119">Per un esempio di codice, vedere <xref:System.Threading.ParameterizedThreadStart>.</span><span class="sxs-lookup"><span data-stu-id="ae54d-119">See <xref:System.Threading.ParameterizedThreadStart> for a code example.</span></span>  
  
 <span data-ttu-id="ae54d-120">L'uso del delegato <xref:System.Threading.ParameterizedThreadStart> non è un modo indipendente dai tipi per passare i dati, perché l'overload del metodo <xref:System.Threading.Thread.Start%2A?displayProperty=nameWithType> accetta qualsiasi oggetto.</span><span class="sxs-lookup"><span data-stu-id="ae54d-120">Using the <xref:System.Threading.ParameterizedThreadStart> delegate is not a type-safe way to pass data, because the <xref:System.Threading.Thread.Start%2A?displayProperty=nameWithType> method overload accepts any object.</span></span> <span data-ttu-id="ae54d-121">In alternativa è possibile incapsulare la routine del thread e i dati in una classe helper e usare il delegato <xref:System.Threading.ThreadStart> per eseguire la routine del thread.</span><span class="sxs-lookup"><span data-stu-id="ae54d-121">An alternative is to encapsulate the thread procedure and the data in a helper class and use the <xref:System.Threading.ThreadStart> delegate to execute the thread procedure.</span></span> <span data-ttu-id="ae54d-122">L'esempio che segue illustra questa tecnica:</span><span class="sxs-lookup"><span data-stu-id="ae54d-122">The following example demonstrates this technique:</span></span>

 [!code-cpp[System.Threading.ThreadStart2#3](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source3.cpp#3)]
 [!code-csharp[System.Threading.ThreadStart2#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source3.cs#3)]
 [!code-vb[System.Threading.ThreadStart2#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source3.vb#3)]  

<span data-ttu-id="ae54d-123">Nessuno dei due delegati, <xref:System.Threading.ThreadStart> e <xref:System.Threading.ParameterizedThreadStart>, ha un valore restituito, perché non è possibile restituire i dati da una chiamata asincrona.</span><span class="sxs-lookup"><span data-stu-id="ae54d-123">Neither <xref:System.Threading.ThreadStart> nor <xref:System.Threading.ParameterizedThreadStart> delegate has a return value, because there is no place to return the data from an asynchronous call.</span></span> <span data-ttu-id="ae54d-124">Per recuperare i risultati di un metodo di thread, è possibile usare un metodo di callback, come illustrato nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="ae54d-124">To retrieve the results of a thread method, you can use a callback method, as shown in the next section.</span></span>
  
## <a name="retrieving-data-from-threads-with-callback-methods"></a><span data-ttu-id="ae54d-125">Recupero dei dati dai thread con i metodi di callback</span><span class="sxs-lookup"><span data-stu-id="ae54d-125">Retrieving data from threads with callback methods</span></span>

 <span data-ttu-id="ae54d-126">L'esempio seguente illustra un metodo di callback che recupera i dati da un thread.</span><span class="sxs-lookup"><span data-stu-id="ae54d-126">The following example demonstrates a callback method that retrieves data from a thread.</span></span> <span data-ttu-id="ae54d-127">Il costruttore della classe che contiene i dati e il metodo del thread accetta anche un delegato che rappresenta il metodo di callback. Prima che il metodo del thread termini, richiama il delegato di callback.</span><span class="sxs-lookup"><span data-stu-id="ae54d-127">The constructor for the class that contains the data and the thread method also accepts a delegate representing the callback method; before the thread method ends, it invokes the callback delegate.</span></span>  
  
 [!code-cpp[System.Threading.ThreadStart2#4](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source4.cpp#4)]
 [!code-csharp[System.Threading.ThreadStart2#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source4.cs#4)]
 [!code-vb[System.Threading.ThreadStart2#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source4.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="ae54d-128">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ae54d-128">See also</span></span>

- <xref:System.Threading.Thread>
- <xref:System.Threading.ThreadStart>
- <xref:System.Threading.ParameterizedThreadStart>
- <xref:System.Threading.Thread.Start%2A?displayProperty=nameWithType>
- [<span data-ttu-id="ae54d-129">Threading</span><span class="sxs-lookup"><span data-stu-id="ae54d-129">Threading</span></span>](index.md)
- [<span data-ttu-id="ae54d-130">Utilizzo di thread e threading</span><span class="sxs-lookup"><span data-stu-id="ae54d-130">Using Threads and Threading</span></span>](using-threads-and-threading.md)

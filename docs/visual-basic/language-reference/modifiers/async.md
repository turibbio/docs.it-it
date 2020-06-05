---
title: Async
ms.date: 07/20/2015
f1_keywords:
- vb.Async
helpviewer_keywords:
- Async [Visual Basic]
- Async keyword [Visual Basic]
ms.assetid: 1be8b4b5-9689-41b5-bd33-b906bfd53bc5
ms.openlocfilehash: 35df7a464937647c6d110142a3e2801cebbea505
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84373167"
---
# <a name="async-visual-basic"></a><span data-ttu-id="5d835-102">Async (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="5d835-102">Async (Visual Basic)</span></span>

<span data-ttu-id="5d835-103">Il `Async` modificatore indica che il metodo o l' [espressione lambda](../../programming-guide/language-features/procedures/lambda-expressions.md) modificata è asincrona.</span><span class="sxs-lookup"><span data-stu-id="5d835-103">The `Async` modifier indicates that the method or [lambda expression](../../programming-guide/language-features/procedures/lambda-expressions.md) that it modifies is asynchronous.</span></span> <span data-ttu-id="5d835-104">Questi metodi sono detti *metodi asincroni*.</span><span class="sxs-lookup"><span data-stu-id="5d835-104">Such methods are referred to as *async methods*.</span></span>

<span data-ttu-id="5d835-105">Un metodo asincrono è un modo pratico per eseguire le operazioni potenzialmente di lunga durata senza bloccare il thread del chiamante.</span><span class="sxs-lookup"><span data-stu-id="5d835-105">An async method provides a convenient way to do potentially long-running work without blocking the caller's thread.</span></span> <span data-ttu-id="5d835-106">Il chiamante di un metodo asincrono può riprendere il proprio lavoro senza attendere il completamento del metodo asincrono.</span><span class="sxs-lookup"><span data-stu-id="5d835-106">The caller of an async method can resume its work without waiting for the async method to finish.</span></span>

> [!NOTE]
> <span data-ttu-id="5d835-107">Le parole chiave `Async` e `Await` sono state introdotte in Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="5d835-107">The `Async` and `Await` keywords were introduced in Visual Studio 2012.</span></span> <span data-ttu-id="5d835-108">Per un'introduzione alla programmazione asincrona, vedere [programmazione asincrona con Async e await](../../programming-guide/concepts/async/index.md).</span><span class="sxs-lookup"><span data-stu-id="5d835-108">For an introduction to async programming, see [Asynchronous Programming with Async and Await](../../programming-guide/concepts/async/index.md).</span></span>

<span data-ttu-id="5d835-109">Nell'esempio seguente viene illustrata la struttura di un metodo async.</span><span class="sxs-lookup"><span data-stu-id="5d835-109">The following example shows the structure of an async method.</span></span> <span data-ttu-id="5d835-110">Per convenzione, i nomi dei metodi async terminano con "Async".</span><span class="sxs-lookup"><span data-stu-id="5d835-110">By convention, async method names end in "Async."</span></span>

```vb
Public Async Function ExampleMethodAsync() As Task(Of Integer)
    ' . . .

    ' At the Await expression, execution in this method is suspended and,
    ' if AwaitedProcessAsync has not already finished, control returns
    ' to the caller of ExampleMethodAsync. When the awaited task is
    ' completed, this method resumes execution.
    Dim exampleInt As Integer = Await AwaitedProcessAsync()

    ' . . .

    ' The return statement completes the task. Any method that is
    ' awaiting ExampleMethodAsync can now get the integer result.
    Return exampleInt
End Function
```

<span data-ttu-id="5d835-111">In genere, un metodo modificato dalla `Async` parola chiave contiene almeno un'espressione o un'istruzione [await](async.md) .</span><span class="sxs-lookup"><span data-stu-id="5d835-111">Typically, a method modified by the `Async` keyword contains at least one [Await](async.md) expression or statement.</span></span> <span data-ttu-id="5d835-112">Il metodo funziona in modo sincrono fino al primo `Await`, a quel punto viene sospeso finché l'attività di cui si è in attesa non viene completata.</span><span class="sxs-lookup"><span data-stu-id="5d835-112">The method runs synchronously until it reaches the first `Await`, at which point it suspends until the awaited task completes.</span></span> <span data-ttu-id="5d835-113">Nel frattempo, il controllo viene restituito al chiamante del metodo.</span><span class="sxs-lookup"><span data-stu-id="5d835-113">In the meantime, control is returned to the caller of the method.</span></span> <span data-ttu-id="5d835-114">Se il metodo non contiene un' `Await` espressione o un'istruzione, il metodo non viene sospeso ed eseguito come metodo sincrono.</span><span class="sxs-lookup"><span data-stu-id="5d835-114">If the method doesn't contain an `Await` expression or statement, the method isn't suspended and executes as a synchronous method does.</span></span> <span data-ttu-id="5d835-115">Un avviso del compilatore segnala eventuali metodi asincroni che non contengono `Await` perché questa situazione potrebbe indicare un errore.</span><span class="sxs-lookup"><span data-stu-id="5d835-115">A compiler warning alerts you to any async methods that don't contain `Await` because that situation might indicate an error.</span></span> <span data-ttu-id="5d835-116">Per ulteriori informazioni, vedere l' [errore del compilatore](../error-messages/bc42358.md).</span><span class="sxs-lookup"><span data-stu-id="5d835-116">For more information, see the [compiler error](../error-messages/bc42358.md).</span></span>

<span data-ttu-id="5d835-117">La parola chiave `Async` è una parola chiave non riservata.</span><span class="sxs-lookup"><span data-stu-id="5d835-117">The `Async` keyword is an unreserved keyword.</span></span> <span data-ttu-id="5d835-118">È una parola chiave quando si modifica un metodo o un'espressione lambda.</span><span class="sxs-lookup"><span data-stu-id="5d835-118">It is a keyword when it modifies a method or a lambda expression.</span></span> <span data-ttu-id="5d835-119">In tutti gli altri contesti, viene interpretata come identificatore.</span><span class="sxs-lookup"><span data-stu-id="5d835-119">In all other contexts, it is interpreted as an identifier.</span></span>

## <a name="return-types"></a><span data-ttu-id="5d835-120">Tipi restituiti</span><span class="sxs-lookup"><span data-stu-id="5d835-120">Return Types</span></span>

<span data-ttu-id="5d835-121">Un metodo asincrono è una routine [Sub](../../programming-guide/language-features/procedures/sub-procedures.md) o una routine di [funzione](../../programming-guide/language-features/procedures/function-procedures.md) con un tipo restituito <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601> .</span><span class="sxs-lookup"><span data-stu-id="5d835-121">An async method is either a [Sub](../../programming-guide/language-features/procedures/sub-procedures.md) procedure, or a [Function](../../programming-guide/language-features/procedures/function-procedures.md) procedure that has a return type of <xref:System.Threading.Tasks.Task> or <xref:System.Threading.Tasks.Task%601>.</span></span> <span data-ttu-id="5d835-122">Il metodo non può dichiarare parametri [ByRef](byref.md) .</span><span class="sxs-lookup"><span data-stu-id="5d835-122">The method cannot declare any [ByRef](byref.md) parameters.</span></span>

<span data-ttu-id="5d835-123">Specificare `Task(Of TResult)` per il tipo restituito di un metodo asincrono se l'istruzione [Return](../statements/return-statement.md) del metodo ha un operando di tipo TResult.</span><span class="sxs-lookup"><span data-stu-id="5d835-123">You specify `Task(Of TResult)` for the return type of an async method if the [Return](../statements/return-statement.md) statement of the method has an operand of type TResult.</span></span> <span data-ttu-id="5d835-124">Utilizzare `Task` se non viene restituito alcun valore significativo al completamento del metodo.</span><span class="sxs-lookup"><span data-stu-id="5d835-124">You use `Task` if no meaningful value is returned when the method is completed.</span></span> <span data-ttu-id="5d835-125">In altre parole, una chiamata al metodo restituisce `Task`, ma quando `Task` viene completato, ogni istruzione `Await` in attesa di `Task` non produce un valore risultante.</span><span class="sxs-lookup"><span data-stu-id="5d835-125">That is, a call to the method returns a `Task`, but when the `Task` is completed, any `Await` statement that's awaiting the `Task` doesn’t produce a result value.</span></span>

<span data-ttu-id="5d835-126">Le subroutine async vengono utilizzate principalmente per definire i gestori eventi in cui è richiesta una procedura `Sub`.</span><span class="sxs-lookup"><span data-stu-id="5d835-126">Async subroutines are used primarily to define event handlers where a `Sub` procedure is required.</span></span> <span data-ttu-id="5d835-127">Il chiamante di una subroutine async non può attendere il metodo e non può intercettare le eccezioni generate dal metodo.</span><span class="sxs-lookup"><span data-stu-id="5d835-127">The caller of an async subroutine can't await it and can't catch exceptions that the method throws.</span></span>

<span data-ttu-id="5d835-128">Per altre informazioni ed esempi, vedere [Tipi restituiti asincroni](../../programming-guide/concepts/async/async-return-types.md).</span><span class="sxs-lookup"><span data-stu-id="5d835-128">For more information and examples, see [Async Return Types](../../programming-guide/concepts/async/async-return-types.md).</span></span>

## <a name="example"></a><span data-ttu-id="5d835-129">Esempio</span><span class="sxs-lookup"><span data-stu-id="5d835-129">Example</span></span>

<span data-ttu-id="5d835-130">Negli esempi seguenti viene illustrato un gestore eventi async, un'espressione lambda async e un metodo async.</span><span class="sxs-lookup"><span data-stu-id="5d835-130">The following examples show an async event handler, an async lambda expression, and an async method.</span></span> <span data-ttu-id="5d835-131">Per un esempio completo in cui vengono usati questi elementi, vedere [procedura dettagliata: accesso al Web tramite Async e await](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).</span><span class="sxs-lookup"><span data-stu-id="5d835-131">For a full example that uses these elements, see [Walkthrough: Accessing the Web by Using Async and Await](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).</span></span> <span data-ttu-id="5d835-132">È possibile scaricare il codice della procedura dettagliata dalla pagina [Developer Code Samples](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f) (Esempi di codice per sviluppatori).</span><span class="sxs-lookup"><span data-stu-id="5d835-132">You can download the walkthrough code from [Developer Code Samples](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f).</span></span>

```vb
' An event handler must be a Sub procedure.
Async Sub button1_Click(sender As Object, e As RoutedEventArgs) Handles button1.Click
    textBox1.Clear()
    ' SumPageSizesAsync is a method that returns a Task.
    Await SumPageSizesAsync()
    textBox1.Text = vbCrLf & "Control returned to button1_Click."
End Sub

' The following async lambda expression creates an equivalent anonymous
' event handler.
AddHandler button1.Click, Async Sub(sender, e)
                              textBox1.Clear()
                              ' SumPageSizesAsync is a method that returns a Task.
                              Await SumPageSizesAsync()
                              textBox1.Text = vbCrLf & "Control returned to button1_Click."
                          End Sub

' The following async method returns a Task(Of T).
' A typical call awaits the Byte array result:
'      Dim result As Byte() = Await GetURLContents("https://msdn.com")
Private Async Function GetURLContentsAsync(url As String) As Task(Of Byte())

    ' The downloaded resource ends up in the variable named content.
    Dim content = New MemoryStream()

    ' Initialize an HttpWebRequest for the current URL.
    Dim webReq = CType(WebRequest.Create(url), HttpWebRequest)

    ' Send the request to the Internet resource and wait for
    ' the response.
    Using response As WebResponse = Await webReq.GetResponseAsync()
        ' Get the data stream that is associated with the specified URL.
        Using responseStream As Stream = response.GetResponseStream()
            ' Read the bytes in responseStream and copy them to content.
            ' CopyToAsync returns a Task, not a Task<T>.
            Await responseStream.CopyToAsync(content)
        End Using
    End Using

    ' Return the result as a byte array.
    Return content.ToArray()
End Function
```

## <a name="see-also"></a><span data-ttu-id="5d835-133">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5d835-133">See also</span></span>

- <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>
- [<span data-ttu-id="5d835-134">Operatore await</span><span class="sxs-lookup"><span data-stu-id="5d835-134">Await Operator</span></span>](../operators/await-operator.md)
- [<span data-ttu-id="5d835-135">Programmazione asincrona con Async e await</span><span class="sxs-lookup"><span data-stu-id="5d835-135">Asynchronous Programming with Async and Await</span></span>](../../programming-guide/concepts/async/index.md)
- [<span data-ttu-id="5d835-136">Procedura dettagliata: accesso al Web tramite Async e await</span><span class="sxs-lookup"><span data-stu-id="5d835-136">Walkthrough: Accessing the Web by Using Async and Await</span></span>](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)

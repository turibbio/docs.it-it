---
title: Gestione delle eccezioni (Task Parallel Library)
description: Esplorare la gestione delle eccezioni usando il Task Parallel Library (TPL) in .NET. Vedere eccezioni aggregate annidate, eccezioni interne, eccezioni di attività non osservate, & altro.
ms.date: 04/20/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, exceptions
ms.assetid: beb51e50-9061-4d3d-908c-56a4f7c2e8c1
ms.openlocfilehash: f1c1a994f4b3a8df0556a0190bc4eacb63f2921e
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2020
ms.locfileid: "84662537"
---
# <a name="exception-handling-task-parallel-library"></a>Gestione delle eccezioni (Task Parallel Library)

Salvo in determinati scenari descritti più avanti in questo argomento, le eccezioni non gestite generate da codice utente in esecuzione in un'attività vengono propagate nel thread di unione. Le eccezioni vengono propagate quando si usa uno dei metodi <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> di istanza e li si gestisce includendo la chiamata in un'istruzione `try`/`catch`. Se un'attività è il padre di attività figlio connesse o se si è in attesa di più attività, potrebbero essere generate più eccezioni.

Per propagare tutte le eccezioni nel thread chiamante, l'infrastruttura di Task ne esegue il wrapping in un'istanza di <xref:System.AggregateException> . L'eccezione <xref:System.AggregateException> ha una proprietà <xref:System.AggregateException.InnerExceptions%2A> che può essere enumerata per esaminare tutte le eccezioni originali generate e per gestire (o non gestire) individualmente ognuna di esse. È anche possibile gestire le eccezioni originali usando il metodo <xref:System.AggregateException.Handle%2A?displayProperty=nameWithType>.

Anche se viene generata un'unica eccezione, il sistema ne esegue comunque il wrapping in un oggetto <xref:System.AggregateException> , come illustrato nell'esempio seguente.

[!code-csharp[TPL_Exceptions#21](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/handling21.cs#21)]
[!code-vb[TPL_Exceptions#21](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/handling21.vb#21)]

È possibile evitare un'eccezione non gestita rilevando solo l'oggetto <xref:System.AggregateException> senza osservare alcuna eccezione interna. Tuttavia, è consigliabile evitare questo approccio perché è analogo al rilevamento del tipo <xref:System.Exception> di base negli scenari senza parallelismo. Rilevare un'eccezione senza intraprendere azioni specifiche per gestirla può lasciare il programma in uno stato indeterminato.

Se non si vuole chiamare il metodo <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> per attendere il completamento dell'attività, è anche possibile recuperare l'eccezione <xref:System.AggregateException> dalla proprietà <xref:System.Threading.Tasks.Task.Exception%2A> dell'attività, come illustrato nell'esempio seguente. Per ulteriori informazioni, vedere la sezione [osservazione delle eccezioni mediante la proprietà Task. Exception](#observing-exceptions-by-using-the-taskexception-property) in questo argomento.

[!code-csharp[TPL_Exceptions#29](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/handling22.cs#29)]
[!code-vb[TPL_Exceptions#29](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/handling22.vb#29)]

Se non si resta in attesa di un'attività che propaga un'eccezione o se si accede alla relativa proprietà <xref:System.Threading.Tasks.Task.Exception%2A> , il sistema esegue l'escalation dell'eccezione in base ai criteri delle eccezioni di .NET quando l'attività viene raccolta nel Garbage Collector.

Quando alle eccezioni è consentita la propagazione fino al thread di unione, un'attività potrebbe continuare a elaborare alcuni elementi dopo la generazione dell'eccezione.

> [!NOTE]
> Quando "Just My Code" è abilitato, Visual Studio in alcuni casi si interromperà in corrispondenza della riga che genera l'eccezione e visualizzerà un messaggio di errore simile a "Eccezione non gestita dal codice utente". Questo errore non è grave. È possibile premere F5 per continuare e osservare il comportamento di gestione delle eccezioni illustrato in questi esempi. Per impedire l'interruzione di Visual Studio al primo errore, deselezionare semplicemente la casella di controllo **Abilita Just My Code** in **Strumenti, Opzioni, Debug, Generale**.

## <a name="attached-child-tasks-and-nested-aggregateexceptions"></a>Attività figlio connesse e oggetti AggregateException annidati

Se un'attività presenta un'attività figlio connessa che genera un'eccezione, il sistema ne eseguirà il wrapping in un oggetto <xref:System.AggregateException> prima che venga propagata nell'attività padre che a sua volta ne eseguirà il wrapping nel proprio oggetto <xref:System.AggregateException> prima che venga ripropagata al thread chiamante. In casi di questo tipo, nella proprietà <xref:System.AggregateException.InnerExceptions%2A> dell'eccezione <xref:System.AggregateException> rilevata nel metodo <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> o <xref:System.Threading.Tasks.Task.WaitAny%2A> o <xref:System.Threading.Tasks.Task.WaitAll%2A> sono contenute una o più istanze di <xref:System.AggregateException>, non le eccezioni originali che hanno provocato l'errore. Per evitare di dover eseguire l'iterazione di oggetti <xref:System.AggregateException> annidati, è possibile usare il metodo <xref:System.AggregateException.Flatten%2A> per rimuovere tutti gli oggetti <xref:System.AggregateException> annidati, in modo che nella proprietà <xref:System.AggregateException.InnerExceptions%2A?displayProperty=nameWithType> siano contenute le eccezioni originali. L'esempio seguente applica automaticamente il metodo Flatten alle istanze di <xref:System.AggregateException> annidate e le gestisce in un solo ciclo.

[!code-csharp[TPL_Exceptions#22](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/flatten2.cs#22)]
[!code-vb[TPL_Exceptions#22](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/flatten2.vb#22)]

È anche possibile usare il metodo <xref:System.AggregateException.Flatten%2A?displayProperty=nameWithType> per generare nuovamente le eccezioni interne da più istanze di <xref:System.AggregateException> generate da più attività in una singola istanza di <xref:System.AggregateException>, come illustrato nell'esempio seguente.

[!code-csharp[TPL_Exceptions#13](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/taskexceptions2.cs#13)]
[!code-vb[TPL_Exceptions#13](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/taskexceptions2.vb#13)]

## <a name="exceptions-from-detached-child-tasks"></a>Eccezioni provenienti da attività figlio disconnesse

Per impostazione predefinita, le attività figlio vengono create come disconnesse. Le eccezioni generate dalle attività disconnesse devono essere gestite o generate nuovamente nell'attività padre immediata. A differenza di quanto accade per le attività figlio connesse, tali eccezioni non vengono propagate nel thread chiamante. Il padre di primo livello può rigenerare manualmente un'eccezione proveniente da un figlio disconnesso per fare in modo che ne venga eseguito il wrapping in un oggetto <xref:System.AggregateException> e venga propagata nel thread di unione.

[!code-csharp[TPL_Exceptions#23](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/detached21.cs#23)]
[!code-vb[TPL_Exceptions#23](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/detached21.vb#23)]

Anche se si usa una continuazione per osservare un'eccezione in un'attività figlio, l'eccezione deve comunque essere osservata dall'attività padre.

## <a name="exceptions-that-indicate-cooperative-cancellation"></a>Eccezioni che indicano un annullamento cooperativo

Quando il codice utente in un'attività risponde a una richiesta di annullamento, la procedura corretta è generare un oggetto <xref:System.OperationCanceledException> che passa il token di annullamento usato per comunicare la richiesta. Prima di provare a propagare l'eccezione, l'istanza dell'attività confronta il token nell'eccezione con quello che le è stato passato quando è stata creata. Se sono uguali, l'attività propaga un oggetto <xref:System.Threading.Tasks.TaskCanceledException> con wrapping nell'oggetto <xref:System.AggregateException>e che può essere visto quando vengono esaminate le eccezioni interne. Tuttavia, se il thread di unione non è in attesa dell'attività, questa eccezione specifica non verrà propagata. Per altre informazioni, vedere [Task Cancellation](task-cancellation.md).

[!code-csharp[TPL_Exceptions#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/exceptions.cs#4)]
[!code-vb[TPL_Exceptions#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/tpl_exceptions.vb#4)]

## <a name="using-the-handle-method-to-filter-inner-exceptions"></a>Uso del metodo Handle per filtrare le eccezioni interne

È possibile usare il metodo <xref:System.AggregateException.Handle%2A?displayProperty=nameWithType> per escludere le eccezioni che è possibile trattare come "gestite" senza dover usare altre risorse di logica. Nel delegato dell'utente fornito al metodo <xref:System.AggregateException.Handle%28System.Func%7BSystem.Exception%2CSystem.Boolean%7D%29?displayProperty=nameWithType> è possibile esaminare il tipo di eccezione o la relativa proprietà <xref:System.Exception.Message%2A> o qualsiasi altra informazione relativa a essa che consentirà di determinare se è non dannosa. Qualsiasi eccezione per cui viene restituito `false` dal delegato viene generata nuovamente in una nuova istanza di <xref:System.AggregateException> subito dopo la restituzione di un valore da parte del metodo <xref:System.AggregateException.Handle%2A?displayProperty=nameWithType>.

L'esempio seguente è funzionalmente equivalente al primo esempio in questo argomento, che esamina ogni eccezione nella raccolta <xref:System.AggregateException.InnerExceptions%2A?displayProperty=nameWithType>.  Al contrario, questo gestore di eccezioni chiama l'oggetto del metodo <xref:System.AggregateException.Handle%2A?displayProperty=nameWithType> per ogni eccezione e rigenera solo le eccezioni che non sono istanze di `CustomException`.

[!code-csharp[TPL_Exceptions#26](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/handlemethod21.cs#26)]
[!code-vb[TPL_Exceptions#26](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/handlemethod21.vb#26)]

Di seguito è riportato un esempio più completo che usa il metodo <xref:System.AggregateException.Handle%2A?displayProperty=nameWithType> per fornire una gestione speciale di un'eccezione <xref:System.UnauthorizedAccessException> durante l'enumerazione dei file.

[!code-csharp[TPL_Exceptions#12](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/taskexceptions.cs#12)]
[!code-vb[TPL_Exceptions#12](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/taskexceptions.vb#12)]

## <a name="observing-exceptions-by-using-the-taskexception-property"></a>Osservazione delle eccezioni con la proprietà Task.Exception

Se un'attività viene completata con lo stato <xref:System.Threading.Tasks.TaskStatus.Faulted?displayProperty=nameWithType>, è possibile esaminarne la proprietà <xref:System.Threading.Tasks.Task.Exception%2A> per trovare l'eccezione specifica che ha provocato l'errore. Un modo efficiente per osservare la proprietà <xref:System.Threading.Tasks.Task.Exception%2A> consiste nell'usare una continuazione che viene eseguita solo se nell'attività precedente si verifica un errore, come illustrato nell'esempio seguente.

[!code-csharp[TPL_Exceptions#27](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/exceptionprop21.cs#27)]
[!code-vb[TPL_Exceptions#27](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/exceptionprop21.vb#27)]

In un'applicazione significativa, il delegato di continuazione potrebbe registrare informazioni dettagliate sull'eccezione ed eventualmente generare nuove attività per il recupero dall'eccezione. Se si verifica un errore in un'attività, le espressioni seguenti generano l'eccezione:

- `await task`
- `task.Wait()`
- `task.Result`
- `task.GetAwaiter().GetResult()`

Utilizzare un' [`try-catch`](../../csharp/language-reference/keywords/try-catch.md) istruzione per gestire e osservare le eccezioni generate. In alternativa, osservare l'eccezione accedendo alla <xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=nameWithType> Proprietà.

## <a name="unobservedtaskexception-event"></a>Evento UnobservedTaskException

In alcuni scenari, ad esempio durante l'hosting di plug-in non attendibili, le eccezioni benigne potrebbero essere comuni e potrebbe risultare troppo difficile osservarle tutte manualmente. In questi casi è possibile gestire l'evento <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException?displayProperty=nameWithType>. L'istanza di <xref:System.Threading.Tasks.UnobservedTaskExceptionEventArgs?displayProperty=nameWithType> passata al gestore può essere usata per evitare la propagazione dell'eccezione non osservata al thread di unione.

## <a name="see-also"></a>Vedere anche

- [Task Parallel Library (TPL)](task-parallel-library-tpl.md)

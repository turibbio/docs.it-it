---
title: Classificazione di operatori di query standard in base alla modalità di esecuzione
ms.date: 07/20/2015
ms.assetid: 7f55b0be-9f6e-44f8-865c-6afbea50cc54
ms.openlocfilehash: e1ba5d8bdc2b7a521a11ca5c055323fde4bcb9d9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410903"
---
# <a name="classification-of-standard-query-operators-by-manner-of-execution-visual-basic"></a>Classificazione degli operatori di query standard in base alla modalità di esecuzione (Visual Basic)
Le implementazioni LINQ to Objects dei metodi degli operatori di query standard vengono eseguite in due modi principali: implementazione immediata o posticipata. Gli operatori di query che usano l'esecuzione posticipata possono essere anche suddivisi in due categorie: di flusso e non di flusso. Se si conosce la modalità di esecuzione dei vari operatori di query, sarà più facile capire i risultati che si ottengono da una determinata query. Ciò è particolarmente vero se l'origine dei dati viene modificata oppure se si sta creando una query su un'altra query. Questo argomento classifica gli operatori di query standard in base alla relativa modalità di esecuzione.  
  
## <a name="manners-of-execution"></a>Modalità di esecuzione  
  
### <a name="immediate"></a>Immediato  
 L'esecuzione immediata indica che l'origine dei dati è in lettura e l'operazione viene eseguita in corrispondenza del punto del codice in cui viene dichiarata la query. Tutti gli operatori di query standard che restituiscono un risultato singolo non enumerabile vengono eseguiti immediatamente.  
  
### <a name="deferred"></a>Rinviata  
 L'esecuzione posticipata indica che l'operazione non viene eseguita in corrispondenza del punto del codice in cui viene dichiarata la query. L'operazione viene eseguita solo quando la variabile di query viene enumerata, ad esempio tramite un'istruzione `For Each`. Ciò significa che i risultati dell'esecuzione della query dipendono dal contenuto dell'origine dei dati nel momento in cui viene eseguita la query e non quando viene definita. Se la variabile di query viene enumerata più volte, i risultati potrebbero essere diversi ogni volta. Quasi tutti gli operatori query standard con tipo restituito <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Linq.IOrderedEnumerable%601> vengono eseguiti in modo posticipato.  
  
 Gli operatori di query che usano l'esecuzione posticipata possono essere anche suddivisi in due categorie: di flusso e non di flusso.  
  
#### <a name="streaming"></a>Streaming  
 Gli operatori di flusso non devono leggere tutti i dati di origine prima di restituire elementi. In fase di esecuzione, un operatore di flusso esegue l'operazione su ogni elemento di origine che legge e restituisce l'elemento, se appropriato. Un operatore di flusso continua a leggere gli elementi fino a quando non può essere prodotto un elemento di risultato. Ciò significa che potrebbe essere letto più di un elemento di origine per produrre un elemento di risultato.  
  
#### <a name="non-streaming"></a>Non di flusso  
 Gli operatori non di flusso devono leggere tutti i dati di origine prima di produrre un elemento di risultato. In questa categoria rientrano operazioni quali ordinamento o raggruppamento. In fase di esecuzione, gli operatori di query non di flusso leggono tutti i dati di origine, li inseriscono in una struttura di dati, eseguono l'operazione e producono gli elementi risultanti.  
  
## <a name="classification-table"></a>Tabella di classificazione  
 La tabella seguente classifica ogni metodo di operatore di query standard in base al metodo di esecuzione.  
  
> [!NOTE]
> Se un operatore è contrassegnato in due colonne, vengono coinvolte due sequenze di input nell'operazione e ogni sequenza viene restituita in modo diverso. In questi casi, viene restituita sempre la prima sequenza nell'elenco dei parametri in modo posticipato e di flusso.  
  
|Operatore di query standard|Tipo restituito|Esecuzione immediata|Esecuzione posticipata di flusso|Esecuzione posticipata di non flusso|  
|-----------------------------|-----------------|-------------------------|----------------------------------|---------------------------------------|  
|<xref:System.Linq.Enumerable.Aggregate%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.All%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.Any%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.AsEnumerable%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Average%2A>|Valore numerico singolo|X|||  
|<xref:System.Linq.Enumerable.Cast%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Concat%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Contains%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.Count%2A>|<xref:System.Int32>|X|||  
|<xref:System.Linq.Enumerable.DefaultIfEmpty%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Distinct%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.ElementAt%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.ElementAtOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.Empty%2A>|<xref:System.Collections.Generic.IEnumerable%601>|X|||  
|<xref:System.Linq.Enumerable.Except%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
|<xref:System.Linq.Enumerable.First%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.FirstOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.GroupBy%2A>|<xref:System.Collections.Generic.IEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.GroupJoin%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
<xref:System.Linq.Enumerable.Intersect%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
|<xref:System.Linq.Enumerable.Join%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X|X|  
|<xref:System.Linq.Enumerable.Last%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.LastOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.LongCount%2A>|<xref:System.Int64>|X|||  
|<xref:System.Linq.Enumerable.Max%2A>|Valore numerico singolo, TSource o TResult|X|||  
|<xref:System.Linq.Enumerable.Min%2A>|Valore numerico singolo, TSource o TResult|X|||  
|<xref:System.Linq.Enumerable.OfType%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.OrderBy%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.OrderByDescending%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.Range%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Repeat%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Reverse%2A>|<xref:System.Collections.Generic.IEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.Select%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.SelectMany%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.SequenceEqual%2A>|<xref:System.Boolean>|X|||  
|<xref:System.Linq.Enumerable.Single%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.SingleOrDefault%2A>|TSource|X|||  
|<xref:System.Linq.Enumerable.Skip%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.SkipWhile%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Sum%2A>|Valore numerico singolo|X|||  
|<xref:System.Linq.Enumerable.Take%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
<xref:System.Linq.Enumerable.TakeWhile%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.ThenBy%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.ThenByDescending%2A>|<xref:System.Linq.IOrderedEnumerable%601>|||X|  
|<xref:System.Linq.Enumerable.ToArray%2A>|Matrice TSource|X|||  
|<xref:System.Linq.Enumerable.ToDictionary%2A>|<xref:System.Collections.Generic.Dictionary%602>|X|||  
|<xref:System.Linq.Enumerable.ToList%2A>|<xref:System.Collections.Generic.IList%601>|X|||  
|<xref:System.Linq.Enumerable.ToLookup%2A>|<xref:System.Linq.ILookup%602>|X|||  
|<xref:System.Linq.Enumerable.Union%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
|<xref:System.Linq.Enumerable.Where%2A>|<xref:System.Collections.Generic.IEnumerable%601>||X||  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Linq.Enumerable>
- [Panoramica degli operatori query standard (Visual Basic)](standard-query-operators-overview.md)
- [Sintassi delle espressioni di query per gli operatori di query standard (Visual Basic)](query-expression-syntax-for-standard-query-operators.md)
- [LINQ to Objects (Visual Basic)](linq-to-objects.md)

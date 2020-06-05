---
title: Sintassi di espressione della query per operatori di query standard
ms.date: 07/20/2015
ms.assetid: eb978d86-d3b5-497b-95ce-a054bea8f510
ms.openlocfilehash: 69bb50007c04bf8d1ee1553a37aca542afbffab0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396285"
---
# <a name="query-expression-syntax-for-standard-query-operators-visual-basic"></a>Sintassi delle espressioni di query per gli operatori di query standard (Visual Basic)
Alcuni degli operatori di query standard usati più di frequente hanno una sintassi dedicata per le parole chiave del linguaggio Visual Basic che consente di chiamarli come parte di un' *espressione di query*. Un'espressione di query rappresenta un modo diverso e più leggibile per esprimere una query rispetto alla sintassi equivalente *basata su metodo*. Le clausole di espressione di query vengono convertite in chiamate ai metodi di query in fase di compilazione.  
  
## <a name="query-expression-syntax-table"></a>Tabella della sintassi di espressione di query  
 La tabella seguente elenca gli operatori di query standard che hanno clausole di espressione di query equivalenti.  
  
|Metodo|Visual Basic sintassi delle espressioni di query|  
|------------|------------------------------------------|  
|<xref:System.Linq.Enumerable.All%2A>|`Aggregate … In … Into All(…)`<br /><br /> Per ulteriori informazioni, vedere [clausola Aggregate](../../../language-reference/queries/aggregate-clause.md).|  
|<xref:System.Linq.Enumerable.Any%2A>|`Aggregate … In … Into Any()`<br /><br /> Per ulteriori informazioni, vedere [clausola Aggregate](../../../language-reference/queries/aggregate-clause.md).|  
|<xref:System.Linq.Enumerable.Average%2A>|`Aggregate … In … Into Average()`<br /><br /> Per ulteriori informazioni, vedere [clausola Aggregate](../../../language-reference/queries/aggregate-clause.md).|  
|<xref:System.Linq.Enumerable.Cast%2A>|`From … As …`<br /><br /> Per ulteriori informazioni, vedere [clausola from](../../../language-reference/queries/from-clause.md).|  
|<xref:System.Linq.Enumerable.Count%2A>|`Aggregate … In … Into Count()`<br /><br /> Per ulteriori informazioni, vedere [clausola Aggregate](../../../language-reference/queries/aggregate-clause.md).|  
|<xref:System.Linq.Enumerable.Distinct%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>|`Distinct`<br /><br /> (Per altre informazioni, vedere [clausola DISTINCT](../../../language-reference/queries/distinct-clause.md)).|  
|<xref:System.Linq.Enumerable.GroupBy%2A>|`Group … By … Into …`<br /><br /> Per ulteriori informazioni, vedere [clausola Group by](../../../language-reference/queries/group-by-clause.md).|  
|<xref:System.Linq.Enumerable.GroupJoin%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2C%60%603%7D%29>|`Group Join … In … On …`<br /><br /> Per ulteriori informazioni, vedere [clausola Group Join](../../../language-reference/queries/group-join-clause.md).|  
|<xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%29>|`From x In …, y In … Where x.a = b.a`<br /><br /> -oppure-<br /><br /> `Join … [As …]In … On …`<br /><br /> Per ulteriori informazioni, vedere [clausola join](../../../language-reference/queries/join-clause.md).|  
|<xref:System.Linq.Enumerable.LongCount%2A>|`Aggregate … In … Into LongCount()`<br /><br /> Per ulteriori informazioni, vedere [clausola Aggregate](../../../language-reference/queries/aggregate-clause.md).|  
|<xref:System.Linq.Enumerable.Max%2A>|`Aggregate … In … Into Max()`<br /><br /> Per ulteriori informazioni, vedere [clausola Aggregate](../../../language-reference/queries/aggregate-clause.md).|  
|<xref:System.Linq.Enumerable.Min%2A>|`Aggregate … In … Into Min()`<br /><br /> Per ulteriori informazioni, vedere [clausola Aggregate](../../../language-reference/queries/aggregate-clause.md).|  
|<xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By`<br /><br /> Per ulteriori informazioni, vedere [clausola ORDER BY](../../../language-reference/queries/order-by-clause.md).|  
|<xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By … Descending`<br /><br /> Per ulteriori informazioni, vedere [clausola ORDER BY](../../../language-reference/queries/order-by-clause.md).|  
|<xref:System.Linq.Enumerable.Select%2A>|`Select`<br /><br /> Per ulteriori informazioni, vedere [clausola SELECT](../../../language-reference/queries/select-clause.md).|  
|<xref:System.Linq.Enumerable.SelectMany%2A>|Più `From` clausole<br /><br /> Per ulteriori informazioni, vedere [clausola from](../../../language-reference/queries/from-clause.md).|  
|<xref:System.Linq.Enumerable.Skip%2A>|`Skip`<br /><br /> Per ulteriori informazioni, vedere [clausola Skip](../../../language-reference/queries/skip-clause.md).|  
|<xref:System.Linq.Enumerable.SkipWhile%2A>|`Skip While`<br /><br /> Per ulteriori informazioni, vedere [clausola Skip While](../../../language-reference/queries/skip-while-clause.md).|  
|<xref:System.Linq.Enumerable.Sum%2A>|`Aggregate … In … Into Sum()`<br /><br /> Per ulteriori informazioni, vedere [clausola Aggregate](../../../language-reference/queries/aggregate-clause.md).|  
|<xref:System.Linq.Enumerable.Take%2A>|`Take`<br /><br /> Per ulteriori informazioni, vedere [clausola Take](../../../language-reference/queries/take-clause.md).|  
|<xref:System.Linq.Enumerable.TakeWhile%2A>|`Take While`<br /><br /> Per ulteriori informazioni, vedere [clausola Take While](../../../language-reference/queries/take-while-clause.md).|  
|<xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By …, …`<br /><br /> Per ulteriori informazioni, vedere [clausola ORDER BY](../../../language-reference/queries/order-by-clause.md).|  
|<xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By …, … Descending`<br /><br /> Per ulteriori informazioni, vedere [clausola ORDER BY](../../../language-reference/queries/order-by-clause.md).|  
|<xref:System.Linq.Enumerable.Where%2A>|`Where`<br /><br /> Per ulteriori informazioni, vedere [clausola WHERE](../../../language-reference/queries/where-clause.md).|  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Linq.Enumerable>
- <xref:System.Linq.Queryable>
- [Panoramica degli operatori query standard (Visual Basic)](standard-query-operators-overview.md)
- [Classificazione degli operatori di query standard in base alla modalità di esecuzione (Visual Basic)](classification-of-standard-query-operators-by-manner-of-execution.md)

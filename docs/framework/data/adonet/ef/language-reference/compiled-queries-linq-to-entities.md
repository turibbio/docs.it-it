---
title: Query compilate (LINQ to Entities)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8025ba1d-29c7-4407-841b-d5a3bed40b7a
ms.openlocfilehash: d4101eae755ac698d4cef5b2e1334d01e02c3e35
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895426"
---
# <a name="compiled-queries--linq-to-entities"></a>Query compilate (LINQ to Entities)
Quando si usa un'applicazione che esegue molte volte query strutturalmente simili in Entity Framework, è spesso possibile migliorare le prestazioni compilando la query una volta ed eseguendola più volte con parametri diversi. Un'applicazione potrebbe ad esempio essere usata per recuperare tutti i clienti di una determinata città, specificata in fase di runtime dall'utente in un modulo. In LINQ to Entities è supportato l'uso di query compilate per questo scopo.  
  
 A partire da.NET Framework 4.5, le query LINQ vengono memorizzate nella cache automaticamente. Tuttavia, è comunque possibile usare le query LINQ compilate per ridurre il costo nelle esecuzioni successive e le query compilate possono essere più efficienti di quelle LINQ che vengono memorizzate nella cache automaticamente. Si noti che le query LINQ to Entities che applicano l'operatore `Enumerable.Contains` alle raccolte in memoria non vengono memorizzate automaticamente nella cache. Inoltre, la parametrizzazione delle raccolte in memoria nelle query LINQ compilate non è consentita.  
  
 La classe <xref:System.Data.Objects.CompiledQuery> consente di compilare e memorizzare nella cache le query da riusare. Dal punto di vista concettuale, questa classe contiene un metodo <xref:System.Data.Objects.CompiledQuery> di `Compile` con numerosi overload. Chiamare il metodo `Compile` per creare un nuovo delegato che rappresenti la query compilata. I metodi `Compile` forniti con un oggetto <xref:System.Data.Objects.ObjectContext> e i valori di parametro restituiscono un delegato che produce un risultato, ad esempio un'istanza di <xref:System.Linq.IQueryable%601>. La query viene compilata solo una volta durante la prima esecuzione. Le opzioni di merge impostate per la query durante la compilazione non possono essere modificate successivamente. Una volta compilata la query, è possibile fornire solo parametri di tipo primitivo ma non è possibile sostituire parti della query che modificherebbe il codice SQL generato. Per altre informazioni, vedere [Opzioni di merge EF e query compilate](https://docs.microsoft.com/archive/blogs/dsimmons/ef-merge-options-and-compiled-queries).
  
 Il LINQ to Entities espressione di query che <xref:System.Data.Objects.CompiledQuery>il `Compile` metodo di compila è rappresentato da uno dei delegati generici `Func` , <xref:System.Func%605>ad esempio. L'espressione di query può incapsulare al massimo un parametro `ObjectContext`, un parametro restituito e 16 parametri di query. Se sono richiesti più di 16 parametri di query, è possibile creare una struttura le cui proprietà rappresentino tali parametri. È possibile quindi usare le proprietà sulla struttura nell'espressione di query dopo averle impostate.  
  
## <a name="example-1"></a>Esempio 1  
 Nell'esempio seguente viene compilata e quindi richiamata una query che accetta un parametro di input <xref:System.Decimal> e restituisce una sequenza di ordini in cui il totale dovuto è maggiore o uguale a 200,00 dollari:  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery2)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery2)]  
  
## <a name="example-2"></a>Esempio 2  
 Nell'esempio seguente viene compilata e quindi richiamata una query che restituisce un'istanza di <xref:System.Data.Objects.ObjectQuery%601>:  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery1_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery1_mq)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery1_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery1_mq)]  
  
## <a name="example-3"></a>Esempio 3  
 Nell'esempio seguente viene compilata e quindi richiamata una query che restituisce la media del prezzo di listino dei prodotti come valore <xref:System.Decimal>:  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery3_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery3_mq)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery3_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery3_mq)]  
  
## <a name="example-4"></a>Esempio 4  
 Nell'esempio seguente viene compilata e quindi richiamata una query che <xref:System.String> accetta un parametro di input e `Contact` quindi restituisce un oggetto il cui indirizzo di posta elettronica inizia con la stringa specificata:  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery4_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery4_mq)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery4_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery4_mq)]  
  
## <a name="example-5"></a>Esempio 5  
 Nell'esempio seguente viene compilata e quindi richiamata una query che accetta parametri di input <xref:System.DateTime> e <xref:System.Decimal> e restituisce una sequenza di ordini in cui la data di ordine è successiva all'8 marzo 2003 e il totale dovuto è inferiore a 300,00 dollari:  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery5)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery5)]  
  
## <a name="example-6"></a>Esempio 6  
 Nell'esempio seguente viene compilata e quindi richiamata una query che accetta un parametro di input <xref:System.DateTime> e restituisce una sequenza di ordini in cui la data di ordine è successiva all'8 marzo 2004. Questa query restituisce le informazioni sull'ordine come sequenza di tipi anonimi. I tipi anonimi vengono dedotti dal compilatore, pertanto non è possibile specificare parametri di tipo nel metodo <xref:System.Data.Objects.CompiledQuery>'s `Compile` e il tipo viene definito nella query stessa.  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery6)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery6)]  
  
## <a name="example-7"></a>Esempio 7  
 Nell'esempio seguente viene compilata e quindi richiamata una query che accetta un parametro di input di una struttura definita dall'utente e restituisce una sequenza di ordini La struttura definisce i parametri di query della data di inizio, della data di fine e del totale dovuto e la query restituisce gli ordini inviati tra il 3 e l'8 marzo 2003 con un totale dovuto maggiore di 700,00 dollari.  
  
 [!code-csharp[DP L2E Conceptual Examples#CompiledQuery7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery7)]
 [!code-vb[DP L2E Conceptual Examples#CompiledQuery7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery7)]  
  
 La struttura che definisce i parametri di query:  
  
 [!code-csharp[DP L2E Conceptual Examples#MyParamsStruct](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#myparamsstruct)]
 [!code-vb[DP L2E Conceptual Examples#MyParamsStruct](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#myparamsstruct)]  
  
## <a name="see-also"></a>Vedere anche

- [ADO.NET Entity Framework](../index.md)
- [LINQ to Entities](linq-to-entities.md)
- [Opzioni di Unione EF e query compilate](https://docs.microsoft.com/archive/blogs/dsimmons/ef-merge-options-and-compiled-queries)

---
title: Quando utilizzare raccolte generiche
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- collections [.NET Framework], generic
- generic collections [.NET Framework]
ms.assetid: e7b868b1-11fe-4ac5-bed3-de68aca47739
ms.openlocfilehash: bbf8ec7f61981332b6984488b369fee62959b92a
ms.sourcegitcommit: 1c1a1f9ec0bd1efb3040d86a79f7ee94e207cca5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/03/2020
ms.locfileid: "80635891"
---
# <a name="when-to-use-generic-collections"></a>Quando utilizzare raccolte generiche

L'utilizzo di raccolte generiche offre i vantaggi automatici dell'indipendenza dai tipi senza dover derivare da un tipo di raccolta di base e implementare membri specifici del tipo. I tipi di raccolta generici in genere offrono anche prestazioni migliori rispetto ai tipi di raccolta non generici corrispondenti (e migliori dei tipi derivati da tipi di raccolta di base non generici) quando gli elementi della raccolta sono tipi di valore, perché con i generics non è necessario eseguire il boxe degli elementi.  
  
 Per programmi destinati a .NET Framework 4 o versione successiva, è necessario usare le classi di raccolte generiche nello spazio dei nomi <xref:System.Collections.Concurrent> quando più thread potrebbero aggiungere o rimuovere elementi dalla raccolta contemporaneamente.  
  
 I seguenti tipi generici corrispondono ai tipi di raccolte esistenti:  
  
- <xref:System.Collections.Generic.List%601> è la classe generica che corrisponde a <xref:System.Collections.ArrayList>.  
  
- <xref:System.Collections.Generic.Dictionary%602> e <xref:System.Collections.Concurrent.ConcurrentDictionary%602> sono le classi generiche che corrispondono a <xref:System.Collections.Hashtable>.  
  
- <xref:System.Collections.ObjectModel.Collection%601> è la classe generica che corrisponde a <xref:System.Collections.CollectionBase>. <xref:System.Collections.ObjectModel.Collection%601>può essere utilizzato come classe <xref:System.Collections.CollectionBase>base, ma a differenza di , non è astratto, il che lo rende molto più facile da usare.  
  
- <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> è la classe generica che corrisponde a <xref:System.Collections.ReadOnlyCollectionBase>. <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> non è astratta, e ha un costruttore che semplifica l'esposizione di una <xref:System.Collections.Generic.List%601> esistente come raccolta di sola lettura.  
  
- Le classi generiche <xref:System.Collections.Generic.Queue%601>, <xref:System.Collections.Concurrent.ConcurrentQueue%601>, <xref:System.Collections.Generic.Stack%601>, <xref:System.Collections.Concurrent.ConcurrentStack%601>e <xref:System.Collections.Generic.SortedList%602> corrispondono alle rispettive classi non generiche con gli stessi nomi.  
  
## <a name="additional-types"></a>Tipi aggiuntivi  
 Diversi tipi di raccolte generiche non hanno controparti non generiche. incluse le seguenti:  
  
- <xref:System.Collections.Generic.LinkedList%601> è un elenco collegato di uso generale che fornisce le operazioni di inserimento e rimozione O(1).  
  
- <xref:System.Collections.Generic.SortedDictionary%602> è un dizionario ordinato con operazioni di inserimento e recupero O(log `n`), che lo rende un'utile alternativa a <xref:System.Collections.Generic.SortedList%602>.  
  
- <xref:System.Collections.ObjectModel.KeyedCollection%602> è un ibrido tra un elenco e un dizionario, che fornisce un metodo per memorizzare oggetti contenenti le loro stesse chiavi.  
  
- <xref:System.Collections.Concurrent.BlockingCollection%601> implementa una classe di raccolta con funzionalità di delimitazione e blocco.  
  
- <xref:System.Collections.Concurrent.ConcurrentBag%601> permette di eseguire rapidamente le operazioni di inserimento e rimozione di elementi non ordinati.  
  
## <a name="linq-to-objects"></a>LINQ to Objects  
 La funzionalità LINQ to Objects consente di usare le query LINQ per accedere agli oggetti in memoria purché il tipo dell'oggetto implementi l'interfaccia <xref:System.Collections.IEnumerable?displayProperty=nameWithType> o <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> . Le query LINQ forniscono un modello comune per l'accesso ai dati. sono in genere più concisi `foreach` e leggibili rispetto ai loop standard; e forniscono funzionalità di filtraggio, ordinamento e raggruppamento. Le query LINQ possono inoltre migliorare le prestazioni. Per altre informazioni, vedere [LINQ to Objects (C#)](../../csharp/programming-guide/concepts/linq/linq-to-objects.md), [LINQ to Objects (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md) e [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/introduction-to-plinq.md).  
  
## <a name="additional-functionality"></a>Funzionalità aggiuntive  
 Alcuni tipi generici hanno funzionalità che non si trovano nei tipi di raccolte non generiche. Ad esempio, la classe <xref:System.Collections.Generic.List%601> , che corrisponde alla classe <xref:System.Collections.ArrayList> non generica, ha una serie di metodi che accettano i delegati generici, come ad esempio il delegato <xref:System.Predicate%601> che consente di specificare metodi per la ricerca nell'elenco, il delegato <xref:System.Action%601> che rappresenta metodi che agiscono su ciascun elemento dell'elenco e il delegato <xref:System.Converter%602> che consente di definire le conversioni tra tipi.  
  
 La classe <xref:System.Collections.Generic.List%601> consente di specificare le proprie implementazioni di interfaccia <xref:System.Collections.Generic.IComparer%601> generica per l'ordinamento e la ricerca nell'elenco. Anche le classi <xref:System.Collections.Generic.SortedDictionary%602> e <xref:System.Collections.Generic.SortedList%602> hanno la stessa capacità. Inoltre, queste classi consentono di specificare gli operatori di confronto quando viene creata la raccolta. In modo analogo, le classi <xref:System.Collections.Generic.Dictionary%602> e <xref:System.Collections.ObjectModel.KeyedCollection%602> consentono di specificare operatori di confronto di uguaglianza personalizzati.  
  
## <a name="see-also"></a>Vedere anche

- [Raccolte e strutture di dati](../../../docs/standard/collections/index.md)
- [Tipi di Collection comunemente utilizzate](../../../docs/standard/collections/commonly-used-collection-types.md)
- [Generics](../../../docs/standard/generics/index.md)

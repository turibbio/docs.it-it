---
title: Esecuzione posticipata e valutazione differita in LINQ to XML
ms.date: 07/20/2015
ms.assetid: 31998eed-b95e-47fb-a865-9de1f337d1fb
ms.openlocfilehash: 98a5010de6ea7ef46d845c6a921c54d4e7692370
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410812"
---
# <a name="deferred-execution-and-lazy-evaluation-in-linq-to-xml-visual-basic"></a>Esecuzione posticipata e valutazione lazy in LINQ to XML (Visual Basic)
Operazioni di query e su asse vengono spesso implementate in modo da usare l'esecuzione posticipata. In questo argomento vengono illustrati requisiti e vantaggi dell'esecuzione posticipata e vengono fornite alcune considerazioni sull'implementazione.  
  
## <a name="deferred-execution"></a>Esecuzione posticipata  
 Per esecuzione posticipata si intende che la valutazione di un'espressione viene ritardata finché il relativo valore *realizzato* non risulta effettivamente necessario. L'esecuzione posticipata può contribuire a migliorare notevolmente le prestazioni quando è necessario modificare grandi raccolte di dati, in particolare in programmi che contengono una serie di modifiche o query concatenate. Nel migliore dei casi l'esecuzione posticipata consente di eseguire un'unica iterazione nella raccolta di origine.  
  
 Le tecnologie LINQ usano notevolmente l'esecuzione posticipata sia nei membri di classi <xref:System.Linq?displayProperty=nameWithType> principali che nei metodi di estensione dei diversi spazi dei nomi LINQ, ad esempio <xref:System.Xml.Linq.Extensions?displayProperty=nameWithType>.  
  
## <a name="eager-vs-lazy-evaluation"></a>Valutazione eager e valutazione lazy  
 Quando si scrive un metodo che implementa l'esecuzione posticipata, è inoltre necessario decidere se implementare il metodo tramite la valutazione lazy o la valutazione eager.  
  
- Nella *valutazione lazy* durante ogni chiamata all'iteratore viene elaborato un unico elemento della raccolta di origine. Si tratta della modalità di implementazione tipica degli iteratori.  
  
- Nella *valutazione eager* in seguito alla prima chiamata all'iteratore verrà elaborata l'intera raccolta. Potrebbe inoltre essere necessaria una copia temporanea della raccolta di origine. Ad esempio, il metodo <xref:System.Linq.Enumerable.OrderBy%2A> deve ordinare l'intera raccolta prima di restituire il primo elemento.  
  
 La valutazione lazy offre in genere prestazioni migliori perché implica una distribuzione uniforme dell'overhead di elaborazione in tutte le fasi della valutazione della raccolta e riduce al minimo l'uso di dati temporanei. Per alcune operazioni è naturalmente inevitabile dover materializzare i risultati intermedi.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Nel successivo argomento dell'esercitazione verrà illustrata l'esecuzione posticipata:  
  
- [Esempio di esecuzione posticipata (Visual Basic)](deferred-execution-example.md)  
  
## <a name="see-also"></a>Vedere anche

- [Esercitazione: esecuzione posticipata (Visual Basic)](tutorial-deferred-execution.md)
- [Concetti e terminologia (trasformazione funzionale) (Visual Basic)](concepts-and-terminology-functional-transformation.md)
- [Operazioni di aggregazione (Visual Basic)](aggregation-operations.md)

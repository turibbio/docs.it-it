---
title: Bug nel codice dichiarativo/imperativo misto (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: f12b1ab4-bb92-4b92-a648-0525e45b3ce7
ms.openlocfilehash: e5526a64805b19ea293d3ef28636738923d03662
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84361073"
---
# <a name="mixed-declarative-codeimperative-code-bugs-linq-to-xml-visual-basic"></a>Bug nel codice dichiarativo/imperativo misto (LINQ to XML) (Visual Basic)
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] contiene i vari metodi che consentono di modificare direttamente un albero XML. È possibile aggiungere elementi, eliminare elementi, modificare il contenuto di un elemento, aggiungere attributi e così via. Questa interfaccia di programmazione è descritta in [modifica di alberi XML (LINQ to XML) (Visual Basic)](modifying-xml-trees-linq-to-xml.md). Se si scorre uno degli assi, ad esempio <xref:System.Xml.Linq.XContainer.Elements%2A>, e si modifica l'albero XML durante lo scorrimento dell'asse, è possibile che vengano individuati alcuni bug strani.  
  
 Questo problema viene talvolta definito come "problema di Halloween".  
  
## <a name="definition-of-the-problem"></a>Definizione del problema  
 Quando si scrive codice usando LINQ che scorre in una raccolta, si usa uno stile dichiarativo. Si tratta in pratica più di descrivere *cosa* si vuole eseguire, anziché *come* si vuole che venga eseguito. Se invece si scrive codice che 1) ottiene il primo elemento, 2) lo verifica in base ad alcune condizioni, 3) lo modifica e 4) lo reinserisce nell'elenco, si usa lo stile del codice imperativo. In pratica si indica al computer *come* eseguire le operazioni desiderate.  
  
 È proprio la combinazione di questi stili di codice nella stessa operazione a comportare problemi. Considerare quanto segue:  
  
 Si supponga di disporre di un elenco collegato contenente tre elementi (a, b e c):  
  
 `a -> b -> c`  
  
 Si supponga ora di volersi spostare nell'elenco collegato, aggiungendo tre nuovi elementi (a', b' e c'). Si desidera che l'elenco collegato risultante sia simile al seguente:  
  
 `a -> a' -> b -> b' -> c -> c'`  
  
 Si scrive pertanto codice che scorre l'elenco e aggiunge un nuovo elemento subito dopo ogni elemento già esistente. Il codice rileverà quindi per primo l'elemento `a` e inserirà `a'` dopo di esso. A questo punto il codice si sposterà al nodo successivo dell'elenco, che però corrisponde ora a `a'`, aggiungendo tranquillamente un nuovo elemento all'elenco, `a''`.  
  
 Per risolvere questo problema nel mondo reale, sarebbe possibile fare una copia dell'elenco collegato originale e creare un elenco completamente nuovo. In alternativa, se si scrive codice esclusivamente imperativo, è possibile individuare il primo elemento, aggiungere il nuovo elemento e quindi avanzare di due posizioni nell'elenco collegato oppure ignorare l'elemento appena aggiunto.  
  
## <a name="adding-while-iterating"></a>Aggiunta durante lo scorrimento  
 Ad esempio, si supponga di voler scrivere codice che crea un elemento duplicato per ogni elemento di un albero:  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
For Each e As XElement In root.Elements()  
    root.Add(New XElement(e.Name, e.Value))  
Next  
```  
  
 Questo codice entra in un ciclo infinito. L'istruzione `foreach` scorre l'asse `Elements()`, aggiungendo nuovi elementi all'elemento `doc`, ma finisce per scorrere anche gli elementi appena aggiunti. Poiché inoltre alloca oggetti nuovi a ogni iterazione del ciclo, finisce con il consumare tutta la memoria disponibile.  
  
 Per risolvere questo problema, è possibile effettuare il pull della raccolta in memoria usando l'operatore di query standard <xref:System.Linq.Enumerable.ToList%2A>, come descritto di seguito:  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
For Each e As XElement In root.Elements().ToList()  
    root.Add(New XElement(e.Name, e.Value))  
Next  
Console.WriteLine(root)  
```  
  
 A questo punto il codice viene eseguito correttamente. l'albero XML risultante è la seguente:  
  
```xml  
<Root>  
  <A>1</A>  
  <B>2</B>  
  <C>3</C>  
  <A>1</A>  
  <B>2</B>  
  <C>3</C>  
</Root>  
```  
  
## <a name="deleting-while-iterating"></a>Eliminazione durante lo scorrimento  
 Se si desidera eliminare tutti i nodi a un determinato livello, si può essere tentati di scrivere codice simile al seguente:  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
For Each e As XElement In root.Elements()  
    e.Remove()  
Next  
Console.WriteLine(root)  
```  
  
 Tuttavia, questo codice non consente di eseguire l'operazione desiderata. In questa situazione, dopo aver rimosso il primo elemento, A, l'elemento viene rimosso dall'albero XML contenuto nella radice e il codice del metodo Elements usato per eseguire lo scorrimento non riesce a individuare l'elemento successivo.  
  
 L'output del codice precedente è il seguente:  
  
```xml  
<Root>  
  <B>2</B>  
  <C>3</C>  
</Root>  
```  
  
 Anche in questo caso la soluzione consiste nel chiamare <xref:System.Linq.Enumerable.ToList%2A> per materializzare la raccolta, come segue:  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
For Each e As XElement In root.Elements().ToList()  
    e.Remove()  
Next  
Console.WriteLine(root)  
```  
  
 Viene prodotto l'output seguente:  
  
```xml  
<Root />  
```  
  
 In alternativa, è possibile eliminare del tutto l'iterazione chiamando <xref:System.Xml.Linq.XElement.RemoveAll%2A> sull'elemento padre:  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
root.RemoveAll()  
Console.WriteLine(root)  
```  
  
## <a name="why-cant-linq-automatically-handle-this"></a>Motivi per i quali LINQ non è in grado di gestire automaticamente questi problemi  
 Un approccio potrebbe essere inserire sempre tutto in memoria anziché ricorrere alla valutazione lazy. Tuttavia, un tale approccio sarebbe molto oneroso in termini di prestazioni e utilizzo della memoria. Di fatto se pure questo approccio venisse usato con LINQ e LINQ to XML, non consentirebbe di ottenere risultati validi in situazioni realistiche.  
  
 Un altro possibile approccio potrebbe essere inserire in LINQ una qualche forma di sintassi delle transazione e fare in modo che il compilatore analizzi il codice per determinare se è necessario materializzare un'eventuale raccolta specifica. Tuttavia, il tentativo di determinare tutto il codice con effetti collaterali è incredibilmente complesso. Esaminare il codice seguente:  
  
```vb  
Dim z = _  
    From e In root.Elements() _  
    Where (TestSomeCondition(e)) _  
    Select DoMyProjection(e)  
```  
  
 Tale codice di analisi dovrebbe analizzare i metodi TestSomeCondition e DoMyProjection, nonché tutti i metodi da questi chiamati, per determinare se il codice presenta effetti collaterali. Tuttavia il codice di analisi potrebbe non cercare solo il codice con effetti collaterali e dovrebbe selezionare solo quello che ha effetti collaterali sugli elementi figlio di `root` in questa situazione.  
  
 LINQ to XML non tenta di eseguire un tale tipo di analisi.  
  
 È responsabilità dell'utente evitare questi problemi.  
  
## <a name="guidance"></a>Indicazioni  
 In primo luogo, non combinare codice dichiarativo e codice imperativo.  
  
 Anche se si conosce esattamente la semantica delle raccolte e la semantica dei metodi che modificano l'albero XML, eventuale codice scritto appositamente per evitare queste categorie di problemi dovrà essere gestito da altri sviluppatori in futuro che potrebbero non avere ugualmente chiara la situazione. Se si combinano stili di codifica dichiarativa e imperativa, il codice sarà più fragile.  
  
 Se si scrive codice che materializza una raccolta allo scopo di evitare questi problemi, annotarlo in appositi commenti nel codice, per consentire ai programmatori che effettuano interventi di manutenzione di comprendere il problema.  
  
 In secondo luogo, usare solo codice dichiarativo, se consentito dalle prestazioni e da altre considerazioni. Non modificare l'albero XML esistente, ma generarne una nuova.  
  
```vb  
Dim root As XElement = _  
    <Root>  
        <A>1</A>  
        <B>2</B>  
        <C>3</C>  
    </Root>  
Dim newRoot As XElement = New XElement("Root", _  
    root.Elements(), root.Elements())  
Console.WriteLine(newRoot)  
```  
  
## <a name="see-also"></a>Vedere anche

- [Programmazione LINQ to XML avanzata (Visual Basic)](advanced-linq-to-xml-programming.md)

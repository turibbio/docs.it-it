---
title: Covarianza e controvarianza nei generics
description: Informazioni sulla covarianza, che consente di usare un tipo più derivato e la controvarianza, che consente di usare un tipo meno derivato, in generics di .NET.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generics, covariance and contravariance
- generics, variance
- covariance and contravariance in generics
- generic type parameters
ms.assetid: 2678dc63-c7f9-4590-9ddc-0a4df684d42e
ms.openlocfilehash: 12de1554bb6e33b69d0d2bba24001e7e4c2d8a65
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663044"
---
# <a name="covariance-and-contravariance-in-generics"></a>Covarianza e controvarianza nei generics
 La covarianza e la controvarianza sono termini che fanno riferimento alla possibilità di usare un tipo più derivato (più specifico) o un tipo meno derivato (meno specifico) di quanto specificato in origine. I parametri di tipo generico supportano la covarianza e la controvarianza per offrire la massima flessibilità nell'assegnazione e nell'utilizzo dei tipi generici. Quando si fa riferimento a un sistema di tipi, la covarianza, la controvarianza e l'invarianza hanno le seguenti definizioni. Negli esempi si presuppone una classe di base denominata `Base` e una classe derivata denominata `Derived`.  
  
- `Covariance`  
  
     Permette di usare un tipo più derivato di quello originariamente specificato.  
  
     È possibile assegnare un'istanza di `IEnumerable<Derived>` (`IEnumerable(Of Derived)` in Visual Basic) a una variabile di tipo `IEnumerable<Base>`.  
  
- `Contravariance`  
  
     Consente di utilizzare un tipo più generico (meno derivato) di quello originariamente specificato.  
  
     È possibile assegnare un'istanza di `Action<Base>` (`Action(Of Base)` in Visual Basic) a una variabile di tipo `Action<Derived>`.  
  
- `Invariance`  
  
     Significa che è possibile usare solo il tipo specificato originariamente; pertanto un parametro di tipo generico invariante non è covariante o controvariante.  
  
     Non è possibile assegnare un'istanza di `List<Base>` (`List(Of Base)` in Visual Basic) a una variabile di tipo `List<Derived>` o viceversa.  
  
 I parametri di tipo covariante consentono di effettuare assegnazioni simili al [polimorfismo](../../csharp/programming-guide/classes-and-structs/polymorphism.md) ordinario., come illustrato nel codice seguente.  
  
 [!code-csharp[CoContraSimpleIEnum#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontrasimpleienum/cs/example.cs#1)]
 [!code-vb[CoContraSimpleIEnum#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontrasimpleienum/vb/example.vb#1)]  
  
 La classe <xref:System.Collections.Generic.List%601> implementa l'interfaccia <xref:System.Collections.Generic.IEnumerable%601> , pertanto `List<Derived>` (`List(Of Derived)` in Visual Basic) implementa `IEnumerable<Derived>`. Il parametro di tipo covariante completa l'operazione.  
  
 Viceversa, la controvarianza è poco intuitiva. Nell'esempio seguente viene creato un delegato di tipo `Action<Base>` (`Action(Of Base)` in Visual Basic), che viene quindi assegnato a una variabile di tipo `Action<Derived>`.  
  
 [!code-csharp[CoContraSimpleAction#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontrasimpleaction/cs/example.cs#1)]
 [!code-vb[CoContraSimpleAction#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontrasimpleaction/vb/example.vb#1)]  
  
 Può sembrare un passo indietro, ma si tratta di codice indipendente dai tipi che viene compilato ed eseguito. L'espressione lambda corrisponde al delegato a cui è assegnato, pertanto definisce un metodo che accetta un parametro di tipo `Base` senza valore restituito. Il delegato risultante può essere assegnato a una variabile di tipo `Action<Derived>` poiché il parametro di tipo `T` del delegato <xref:System.Action%601> è controvariante. Il codice è indipendente dai tipi perché `T` specifica un tipo di parametro. Quando il delegato di tipo `Action<Base>` viene richiamato come se fosse un delegato di tipo `Action<Derived>`, il relativo argomento deve essere di tipo `Derived`. Questo argomento può sempre essere passato in modo sicuro al metodo sottostante, perché il parametro del metodo è di tipo `Base`.  
  
 In genere, un parametro di tipo covariante può essere utilizzato come tipo restituito di un delegato e i parametri di tipo controvariante possono essere utilizzati come tipi di parametri. Per un'interfaccia, i parametri di tipo covariante possono essere utilizzati come tipi restituiti dei metodi dell'interfaccia e i parametri di tipo controvariante possono essere utilizzati come tipi di parametri dei metodi dell'interfaccia.  
  
 La covarianza e la controvarianza sono definite collettivamente *varianza*. Un parametro di tipo generico non contrassegnato come covariante o controvariante viene definito *invariante*. Di seguito vengono riepilogati i concetti relativi alla varianza in Common Language Runtime:  
  
- In .NET Framework 4, i parametri di tipo variante sono limitati ai tipi di interfaccia generica e delegato generico.  
  
- Un tipo di interfaccia generica o delegato generico può presentare parametri di tipo sia covariante sia controvariante.  
  
- La varianza si applica solo ai tipi di riferimento. Se si specifica un tipo di valore per un parametro di tipo variante, tale parametro di tipo è invariante per il tipo costruito risultante.  
  
- La varianza non si applica alla combinazione di delegati. Ciò significa che nel caso di due delegati di tipo `Action<Derived>` e `Action<Base>` (`Action(Of Derived)` e `Action(Of Base)` in Visual Basic), non è possibile combinare il secondo delegato con il primo anche se il risultato sarebbe indipendente dai tipi. La varianza consente l'assegnazione del secondo delegato a una variabile di tipo `Action<Derived>`, ma i delegati possono essere combinati solo se il loro tipo corrisponde esattamente.

<a name="InterfaceCovariantTypeParameters"></a>
## <a name="generic-interfaces-with-covariant-type-parameters"></a>Interfacce generiche con parametri di tipo covariante  
 A partire da .NET Framework 4, diverse interfacce generiche presentano parametri di tipo covariante, ad esempio <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.Generic.IEnumerator%601>, <xref:System.Linq.IQueryable%601> e <xref:System.Linq.IGrouping%602>. Tutti i parametri del tipo di queste interfacce sono covarianti, pertanto i parametri del tipo vengono utilizzati solo per i tipi restituiti dei membri.  
  
 Nell'esempio seguente vengono illustrati parametri di tipo covariante. Nell'esempio vengono definiti due tipi: `Base` presenta un metodo statico denominato `PrintBases` che accetta `IEnumerable<Base>` (`IEnumerable(Of Base)` in Visual Basic) e stampa gli elementi. `Derived` eredita da `Base`. Nell'esempio viene creato un tipo `List<Derived>` (`List(Of Derived)` in Visual Basic) vuoto e viene illustrato che è possibile passare tale tipo a `PrintBases` e assegnarlo a una variabile di tipo `IEnumerable<Base>` senza eseguire il cast. <xref:System.Collections.Generic.List%601> implementa <xref:System.Collections.Generic.IEnumerable%601>, che dispone di un solo parametro di tipo covariante. Il parametro di tipo covariante è il motivo per cui è possibile usare un'istanza di `IEnumerable<Derived>` anziché di `IEnumerable<Base>`.  
  
 [!code-csharp[CoContravarianceInClrGenericI#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravarianceinclrgenerici/cs/example.cs#1)]
 [!code-vb[CoContravarianceInClrGenericI#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravarianceinclrgenerici/vb/example.vb#1)]  
  
## <a name="generic-interfaces-with-contravariant-generic-type-parameters"></a>Interfacce generiche con parametri di tipo generico controvariante  
 A partire da .NET Framework 4, diverse interfacce generiche presentano parametri di tipo contravariante, ad esempio <xref:System.Collections.Generic.IComparer%601>, <xref:System.IComparable%601> e <xref:System.Collections.Generic.IEqualityComparer%601>. Queste interfacce dispongono solo di parametri di tipo controvariante, pertanto i parametri di tipo vengono utilizzati solo come tipi di parametri nei membri delle interfacce.  
  
 Nell'esempio seguente vengono illustrati parametri di tipo controvariante. Nell'esempio viene definita una classe`MustInherit` astratta ( `Shape` in Visual Basic) con una proprietà `Area` . Nell'esempio viene definita anche una classe `ShapeAreaComparer` che implementa `IComparer<Shape>` (`IComparer(Of Shape)` in Visual Basic). L'implementazione del metodo <xref:System.Collections.Generic.IComparer%601.Compare%2A?displayProperty=nameWithType> è basata sul valore della proprietà `Area` , pertanto `ShapeAreaComparer` può essere utilizzato per ordinare gli oggetti `Shape` in base all'area.  
  
 La classe `Circle` eredita dalla classe `Shape` ed esegue l'override di `Area`. Nell'esempio viene creato un oggetto <xref:System.Collections.Generic.SortedSet%601> di oggetti `Circle` , usando un costruttore che accetta un oggetto `IComparer<Circle>` (`IComparer(Of Circle)` in Visual Basic). Tuttavia, anziché passare un oggetto `IComparer<Circle>`, nell'esempio viene passato un oggetto `ShapeAreaComparer` che implementa `IComparer<Shape>`. È possibile passare un operatore di confronto di un tipo meno derivato (`Shape`) quando il codice chiama un operatore di confronto di un tipo più derivato (`Circle`), poiché il parametro di tipo dell'interfaccia generica <xref:System.Collections.Generic.IComparer%601> è controvariante.  
  
 Quando un nuovo oggetto `Circle` viene aggiunto all'oggetto `SortedSet<Circle>`, il metodo `IComparer<Shape>.Compare` (metodo`IComparer(Of Shape).Compare` in Visual Basic) dell'oggetto `ShapeAreaComparer` viene chiamato ogni volta che il nuovo elemento viene confrontato con un elemento esistente. Il tipo di parametro del metodo (`Shape`) è meno derivato rispetto al tipo passato (`Circle`), pertanto la chiamata è indipendente dai tipi. La controvarianza consente a `ShapeAreaComparer` di ordinare una raccolta di qualsiasi singolo tipo nonché una raccolta mista di tipi che derivano da `Shape`.  
  
 [!code-csharp[CoContravarianceInClrGenericI2#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravarianceinclrgenerici2/cs/example.cs#1)]
 [!code-vb[CoContravarianceInClrGenericI2#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravarianceinclrgenerici2/vb/example.vb#1)]  

## <a name="generic-delegates-with-variant-type-parameters"></a>Delegati generici con parametri di tipo variante  
 In .NET Framework 4 i delegati generici `Func`, ad esempio <xref:System.Func%602>, presentano tipi restituiti covarianti e tipi di parametro controvarianti. I delegati generici `Action` , ad esempio <xref:System.Action%602>, presentano tipi di parametro controvarianti. Ciò significa che i delegati possono essere assegnati a variabili che presentano tipi di parametro più derivati e (nel caso dei delegati generici `Func` ) tipi restituiti meno derivati.  
  
> [!NOTE]
> L'ultimo parametro di tipo generico dei delegati generici `Func` specifica il tipo del valore restituito nella firma del delegato. È covariante (parola chiave`out` ), mentre gli altri parametri di tipo generico sono controvarianti (parola chiave`in` ).  
  
 Questa condizione è illustrata nel codice che segue. Nella prima parte di codice vengono definite una classe denominata `Base`, una classe denominata `Derived` che eredita da `Base`e un'altra classe con un metodo `static` (`Shared` in Visual Basic) denominata `MyMethod`. Il metodo accetta un'istanza di `Base` e restituisce un'istanza di `Derived`. Se l'argomento è un'istanza di `Derived` , lo `MyMethod` restituisce. se l'argomento è un'istanza di `Base` , `MyMethod` restituisce una nuova istanza di `Derived` . In `Main()` l'esempio crea un'istanza di `Func<Base, Derived>` ( `Func(Of Base, Derived)` in Visual Basic) che rappresenta `MyMethod` e la archivia nella variabile `f1` .  
  
 [!code-csharp[CoContravarianceDelegates#2](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#2)]
 [!code-vb[CoContravarianceDelegates#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#2)]  
  
 Nella seconda parte di codice viene illustrato che è possibile assegnare il delegato a una variabile di tipo `Func<Base, Base>` (`Func(Of Base, Base)` in Visual Basic), poiché il tipo restituito è covariante.  
  
 [!code-csharp[CoContravarianceDelegates#3](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#3)]
 [!code-vb[CoContravarianceDelegates#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#3)]  
  
 Nella terza parte di codice viene illustrato che è possibile assegnare il delegato a una variabile di tipo `Func<Derived, Derived>` (`Func(Of Derived, Derived)` in Visual Basic), poiché il tipo di parametro è controvariante.  
  
 [!code-csharp[CoContravarianceDelegates#4](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#4)]
 [!code-vb[CoContravarianceDelegates#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#4)]  
  
 Nella parte finale di codice viene illustrato che è possibile assegnare il delegato a una variabile di tipo `Func<Derived, Base>` (`Func(Of Derived, Base)` in Visual Basic), combinando gli effetti del tipo di parametro controvariante e del tipo restituito covariante.  
  
 [!code-csharp[CoContravarianceDelegates#5](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#5)]
 [!code-vb[CoContravarianceDelegates#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#5)]  
  
### <a name="variance-in-generic-and-non-generic-delegates"></a>Varianza nei delegati generici e non generici  
 Nel codice precedente la firma di `MyMethod` corrisponde esattamente alla firma del delegato generico costruito: `Func<Base, Derived>` (`Func(Of Base, Derived)` in Visual Basic). Nell'esempio viene illustrato che è possibile archiviare questo delegato generico in variabili o parametri del metodo che presentano tipi di parametro più derivati e tipi restituiti meno derivati, purché tutti i tipi delegati vengano costruiti a partire dal tipo delegato generico <xref:System.Func%602>.  
  
 Questo è un punto importante. Gli effetti della covarianza e della controvarianza nei parametri di tipo dei delegati generici sono simili agli effetti della covarianza e della controvarianza nel normale binding di delegati. Vedere [Varianza nei delegati (C#)](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) e [Varianza nei delegati (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md). Tuttavia, la varianza nell'associazione di delegati funziona con tutti i tipi delegati, non solo con quelli generici aventi parametri di tipo variante. Inoltre, la varianza nell'associazione di delegati consente l'associazione di un metodo a qualsiasi delegato con tipi di parametro più restrittivi e un tipo restituito meno restrittivo, mentre l'assegnazione di delegati generici funziona solo se entrambi i tipi di delegati sono costruiti a partire dalla stessa definizione di tipo generico.  
  
 Nell'esempio seguente sono mostrati gli effetti combinati della varianza nell'associazione di delegati e della varianza nei parametri di tipo generico. Nell'esempio viene definita una gerarchia di tre tipi, da quello meno derivato (`Type1`) a quello più derivato (`Type3`). La varianza nella normale associazione di delegati viene utilizzata per associare un metodo con un tipo di parametro `Type1` e un tipo restituito `Type3` a un delegato generico con un tipo di parametro `Type2` e un tipo restituito `Type2`. Il delegato generico risultante viene quindi assegnato a un'altra variabile il cui tipo delegato generico presenta un parametro di tipo `Type3` e un tipo restituito `Type1`, utilizzando la covarianza e la controvarianza di parametri di tipo generico. Per la seconda assegnazione è necessario che sia il tipo della variabile sia quello del delegato vengano costruiti a partire dalla stessa definizione di tipo generico, in questo caso <xref:System.Func%602>.  
  
 [!code-csharp[CoContravarianceDelegatesGenRelaxed#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegatesgenrelaxed/cs/example.cs#1)]
 [!code-vb[CoContravarianceDelegatesGenRelaxed#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegatesgenrelaxed/vb/example.vb#1)]  

## <a name="defining-variant-generic-interfaces-and-delegates"></a>Definizione di interfacce e delegati generici varianti
 A partire da .NET Framework 4, Visual Basic e C# presentano parole chiave che consentono di contrassegnare i parametri di tipo generico di interfacce e delegati come covarianti o controvarianti.  
  
> [!NOTE]
> A partire dalla versione 2.0 di .NET Framework, Common Language Runtime supporta le annotazioni di variante nei parametri di tipo generico. Nelle versioni precedenti a .NET Framework 4, l'unico modo per definire una classe generica con queste annotazioni consiste nell'usare Microsoft Intermediate Language (MSIL), compilando la classe con [Ilasm.exe (IL Assembler)](../../framework/tools/ilasm-exe-il-assembler.md) oppure creandola in un assembly dinamico.  
  
 Un parametro di tipo covariante è contrassegnato con la parola chiave `out` (parola chiave`Out` in Visual Basic, `+` per l' [assembler MSIL](../../framework/tools/ilasm-exe-il-assembler.md)). È possibile usare un parametro di tipo covariante come valore restituito di un metodo che appartiene a un'interfaccia o come tipo restituito di un delegato. Non è possibile usare un parametro di tipo covariante come vincolo di tipo generico per i metodi di interfaccia.  
  
> [!NOTE]
> Se un metodo di un'interfaccia presenta un parametro che è un tipo delegato generico, per specificare un parametro di tipo controvariante del tipo delegato è possibile usare un parametro di tipo covariante del tipo di interfaccia.  
  
 Un parametro di tipo controvariante è contrassegnato con la parola chiave `in` (parola chiave`In` in Visual Basic, `-` per l' [assembler MSIL](../../framework/tools/ilasm-exe-il-assembler.md)). È possibile usare un parametro di tipo controvariante come tipo di un parametro di un metodo che appartiene a un'interfaccia o come tipo di un parametro di un delegato. È possibile usare un parametro di tipo controvariante come vincolo di tipo generico per un metodo di interfaccia.  
  
 Solo i tipi di interfaccia e i tipi delegati possono presentare parametri di tipo variante. Un tipo di interfaccia o delegato può presentare parametri di tipo sia covariante sia controvariante.  
  
 Visual Basic e C# non consentono di violare le regole per l'utilizzo di parametri di tipo covariante e controvariante o aggiungere annotazioni di covarianza e controvarianza ai parametri relativi a tipi diversi da interfacce e delegati. L' [assembler MSIL](../../framework/tools/ilasm-exe-il-assembler.md) non esegue tali controlli. Tuttavia, se si tenta di caricare un tipo che viola le regole, viene generato un oggetto <xref:System.TypeLoadException> .  
  
 Per informazioni e codice di esempio, vedere [Varianza nelle interfacce generiche (C#)](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md) e [Varianza nelle interfacce generiche (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md).  

## <a name="list-of-variant-generic-interface-and-delegate-types"></a>Elenco di tipi di interfacce e delegati generici varianti
 In .NET Framework 4 il tipo di interfaccia e il tipo delegato seguenti presentano parametri di tipo covariante e/o controvariante.  
  
|Type|Parametri di tipo covariante|Parametri di tipo controvariante|  
|----------|-------------------------------|-----------------------------------|  
|Da <xref:System.Action%601> a <xref:System.Action%6016>||Sì|  
|<xref:System.Comparison%601>||Sì|  
|<xref:System.Converter%602>|Sì|Sì|  
|<xref:System.Func%601>|Sì||  
|Da <xref:System.Func%602> a <xref:System.Func%6017>|Sì|Sì|  
|<xref:System.IComparable%601>||Sì|  
|<xref:System.Predicate%601>||Sì|  
|<xref:System.Collections.Generic.IComparer%601>||Sì|  
|<xref:System.Collections.Generic.IEnumerable%601>|Sì||  
|<xref:System.Collections.Generic.IEnumerator%601>|Sì||  
|<xref:System.Collections.Generic.IEqualityComparer%601>||Sì|  
|<xref:System.Linq.IGrouping%602>|Sì||  
|<xref:System.Linq.IOrderedEnumerable%601>|Sì||  
|<xref:System.Linq.IOrderedQueryable%601>|Sì||  
|<xref:System.Linq.IQueryable%601>|Sì||  
  
## <a name="see-also"></a>Vedere anche

- [Covarianza e controvarianza (C#)](../../csharp/programming-guide/concepts/covariance-contravariance/index.md)
- [Covarianza e controvarianza (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/index.md)
- [Varianza nei delegati (C#)](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
- [Varianza nei delegati (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)

---
title: Operatori ed espressioni di accesso ai membri - Informazioni di riferimento su C
description: Informazioni sugli operatori C# che è possibile usare per accedere ai membri di tipo.
ms.date: 09/18/2019
author: pkulikov
f1_keywords:
- ._CSharpKeyword
- '[]_CSharpKeyword'
- ()_CSharpKeyword
- ^_CSharpKeyword
- .._CSharpKeyword
helpviewer_keywords:
- member access operators [C#]
- member access operator [C#]
- dot operator [C#]
- . operator [C#]
- subscript operator [C#]
- square brackets [] operator [C#]
- indexer operator [C#]
- '[] operator [C#]'
- null-conditional operators [C#]
- Elvis operator [C#]
- ?. operator [C#]
- ?[] operator [C#]
- invocation operator [C#]
- method call [C#]
- method invocation [C#]
- delegate invocation [C#]
- () operator [C#]
- ^ operator [C#]
- index from end operator [C#]
- hat operator [C#]
- .. operator [C#]
- range operator [C#]
ms.openlocfilehash: da2ca4517bd007678d74ae9b76e10cad4c2696b4
ms.sourcegitcommit: 34dc3c0d0d0a1cc418abff259d9daa8078d00b81
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/19/2020
ms.locfileid: "79546640"
---
# <a name="member-access-operators-and-expressions-c-reference"></a><span data-ttu-id="fd19f-103">Operatori ed espressioni di accesso ai membri (riferimenti per C</span><span class="sxs-lookup"><span data-stu-id="fd19f-103">Member access operators and expressions (C# reference)</span></span>

<span data-ttu-id="fd19f-104">Quando si accede a un membro di tipo, è possibile utilizzare gli operatori e le espressioni seguenti:You can use the following operators and expressions when you access a type member:</span><span class="sxs-lookup"><span data-stu-id="fd19f-104">You can use the following operators and expressions when you access a type member:</span></span>

- <span data-ttu-id="fd19f-105">(accesso ai membri): per accedere a un membro di uno spazio dei nomi o di un tipo [ `.` ](#member-access-expression-)</span><span class="sxs-lookup"><span data-stu-id="fd19f-105">[`.` (member access)](#member-access-expression-): to access a member of a namespace or a type</span></span>
- <span data-ttu-id="fd19f-106">[(elemento matrice o accesso all'indicizzatore): per accedere a un elemento di matrice o a un indicizzatore di tipo `[]` ](#indexer-operator-)</span><span class="sxs-lookup"><span data-stu-id="fd19f-106">[`[]` (array element or indexer access)](#indexer-operator-): to access an array element or a type indexer</span></span>
- <span data-ttu-id="fd19f-107">e (operatori null-conditional) : per eseguire un'operazione di accesso a un membro o a un elemento solo se un operando non è null [ `?.` `?[]` ](#null-conditional-operators--and-)</span><span class="sxs-lookup"><span data-stu-id="fd19f-107">[`?.` and `?[]` (null-conditional operators)](#null-conditional-operators--and-): to perform a member or element access operation only if an operand is non-null</span></span>
- <span data-ttu-id="fd19f-108">(chiamata) : per chiamare un metodo a cui si accede o richiamare un delegato [ `()` ](#invocation-expression-)</span><span class="sxs-lookup"><span data-stu-id="fd19f-108">[`()` (invocation)](#invocation-expression-): to call an accessed method or invoke a delegate</span></span>
- <span data-ttu-id="fd19f-109">(indice dalla fine) : per indicare che la posizione dell'elemento è dalla fine di una sequenza [ `^` ](#index-from-end-operator-)</span><span class="sxs-lookup"><span data-stu-id="fd19f-109">[`^` (index from end)](#index-from-end-operator-): to indicate that the element position is from the end of a sequence</span></span>
- <span data-ttu-id="fd19f-110">(intervallo) : per specificare un intervallo di indici che è possibile utilizzare per ottenere un intervallo di elementi di sequenza [ `..` ](#range-operator-)</span><span class="sxs-lookup"><span data-stu-id="fd19f-110">[`..` (range)](#range-operator-): to specify a range of indices that you can use to obtain a range of sequence elements</span></span>

## <a name="member-access-expression-"></a><span data-ttu-id="fd19f-111">Espressione di accesso ai membri .</span><span class="sxs-lookup"><span data-stu-id="fd19f-111">Member access expression .</span></span>

<span data-ttu-id="fd19f-112">Si usa il token `.` per accedere a un membro di uno spazio dei nomi o di un tipo, come illustrano gli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd19f-112">You use the `.` token to access a member of a namespace or a type, as the following examples demonstrate:</span></span>

- <span data-ttu-id="fd19f-113">Utilizzare `.` per accedere a uno spazio dei nomi annidato all'interno di uno spazio dei nomi, come illustrato nell'esempio seguente di una [ `using` direttiva:Use](../keywords/using-directive.md) to access a nested namespace within a namespace, as the following example of a directive shows:</span><span class="sxs-lookup"><span data-stu-id="fd19f-113">Use `.` to access a nested namespace within a namespace, as the following example of a [`using` directive](../keywords/using-directive.md) shows:</span></span>

  [!code-csharp[nested namespaces](snippets/MemberAccessOperators.cs#NestedNamespace)]

- <span data-ttu-id="fd19f-114">Usare `.` per formare un *nome qualificato* per accedere a un tipo in uno spazio dei nomi, come illustra il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="fd19f-114">Use `.` to form a *qualified name* to access a type within a namespace, as the following code shows:</span></span>

  [!code-csharp[qualified name](snippets/MemberAccessOperators.cs#QualifiedName)]

  <span data-ttu-id="fd19f-115">Utilizzare una [ `using` direttiva](../keywords/using-directive.md) per rendere facoltativo l'utilizzo di nomi qualificati.</span><span class="sxs-lookup"><span data-stu-id="fd19f-115">Use a [`using` directive](../keywords/using-directive.md) to make the use of qualified names optional.</span></span>

- <span data-ttu-id="fd19f-116">Usare `.` per accedere ai [membri dei tipi](../../programming-guide/classes-and-structs/index.md#members), statici e non statici, come illustra il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="fd19f-116">Use `.` to access [type members](../../programming-guide/classes-and-structs/index.md#members), static and non-static, as the following code shows:</span></span>

  [!code-csharp-interactive[type members](snippets/MemberAccessOperators.cs#TypeMemberAccess)]

<span data-ttu-id="fd19f-117">È anche possibile usare `.` per accedere a un [metodo di estensione](../../programming-guide/classes-and-structs/extension-methods.md).</span><span class="sxs-lookup"><span data-stu-id="fd19f-117">You can also use `.` to access an [extension method](../../programming-guide/classes-and-structs/extension-methods.md).</span></span>

## <a name="indexer-operator-"></a><span data-ttu-id="fd19f-118">Operatore indicizzatore []</span><span class="sxs-lookup"><span data-stu-id="fd19f-118">Indexer operator []</span></span>

<span data-ttu-id="fd19f-119">Le parentesi quadre `[]` vengono in genere usate per l'accesso agli elementi matrice, indicizzatore o puntatore.</span><span class="sxs-lookup"><span data-stu-id="fd19f-119">Square brackets, `[]`, are typically used for array, indexer, or pointer element access.</span></span>

### <a name="array-access"></a><span data-ttu-id="fd19f-120">Accesso a matrici</span><span class="sxs-lookup"><span data-stu-id="fd19f-120">Array access</span></span>

<span data-ttu-id="fd19f-121">Nell'esempio seguente viene illustrato come accedere agli elementi matrice:</span><span class="sxs-lookup"><span data-stu-id="fd19f-121">The following example demonstrates how to access array elements:</span></span>

[!code-csharp-interactive[array access](snippets/MemberAccessOperators.cs#Arrays)]

<span data-ttu-id="fd19f-122">Se un indice di matrice è fuori dai limiti della dimensione corrispondente di una matrice, viene generata un'eccezione <xref:System.IndexOutOfRangeException>.</span><span class="sxs-lookup"><span data-stu-id="fd19f-122">If an array index is outside the bounds of the corresponding dimension of an array, an <xref:System.IndexOutOfRangeException> is thrown.</span></span>

<span data-ttu-id="fd19f-123">Come illustrato nell'esempio precedente, si usano le parentesi quadre anche per dichiarare un tipo di matrice o creare un'istanza di matrice.</span><span class="sxs-lookup"><span data-stu-id="fd19f-123">As the preceding example shows, you also use square brackets when you declare an array type or instantiate an array instance.</span></span>

<span data-ttu-id="fd19f-124">Per altre informazioni sulle matrici, vedere [Matrici](../../programming-guide/arrays/index.md).</span><span class="sxs-lookup"><span data-stu-id="fd19f-124">For more information about arrays, see [Arrays](../../programming-guide/arrays/index.md).</span></span>

### <a name="indexer-access"></a><span data-ttu-id="fd19f-125">Accesso all'indicizzatore</span><span class="sxs-lookup"><span data-stu-id="fd19f-125">Indexer access</span></span>

<span data-ttu-id="fd19f-126">Nell'esempio seguente viene <xref:System.Collections.Generic.Dictionary%602> utilizzato il tipo .NET per illustrare l'accesso all'indicizzatore:The following example uses the .NET type to demonstrate indexer access:</span><span class="sxs-lookup"><span data-stu-id="fd19f-126">The following example uses the .NET <xref:System.Collections.Generic.Dictionary%602> type to demonstrate indexer access:</span></span>

[!code-csharp-interactive[indexer access](snippets/MemberAccessOperators.cs#Indexers)]

<span data-ttu-id="fd19f-127">Gli indicizzatori consentono di indicizzare le istanze di un tipo definito dall'utente con modalità simili a quelle dell'indicizzazione della matrice.</span><span class="sxs-lookup"><span data-stu-id="fd19f-127">Indexers allow you to index instances of a user-defined type in the similar way as array indexing.</span></span> <span data-ttu-id="fd19f-128">A differenza degli indici di matrice, che devono essere integer, i parametri dell'indicizzatore possono essere dichiarati di qualsiasi tipo.</span><span class="sxs-lookup"><span data-stu-id="fd19f-128">Unlike array indices, which must be integer, the indexer parameters can be declared to be of any type.</span></span>

<span data-ttu-id="fd19f-129">Per altre informazioni sugli indicizzatori, vedere [Indicizzatori](../../programming-guide/indexers/index.md).</span><span class="sxs-lookup"><span data-stu-id="fd19f-129">For more information about indexers, see [Indexers](../../programming-guide/indexers/index.md).</span></span>

### <a name="other-usages-of-"></a><span data-ttu-id="fd19f-130">Altri utilizzi di []</span><span class="sxs-lookup"><span data-stu-id="fd19f-130">Other usages of []</span></span>

<span data-ttu-id="fd19f-131">Per informazioni sull'accesso agli elementi del puntatore, vedere la sezione [Operatore [] (accesso agli elementi del puntatore)](pointer-related-operators.md#pointer-element-access-operator-) dell'articolo [Operatori relativi al puntatore](pointer-related-operators.md).</span><span class="sxs-lookup"><span data-stu-id="fd19f-131">For information about pointer element access, see the [Pointer element access operator []](pointer-related-operators.md#pointer-element-access-operator-) section of the [Pointer related operators](pointer-related-operators.md) article.</span></span>

<span data-ttu-id="fd19f-132">Le parentesi quadre possono anche essere usate per specificare [attributi](../../programming-guide/concepts/attributes/index.md):</span><span class="sxs-lookup"><span data-stu-id="fd19f-132">You also use square brackets to specify [attributes](../../programming-guide/concepts/attributes/index.md):</span></span>

```csharp
[System.Diagnostics.Conditional("DEBUG")]
void TraceMethod() {}
```

## <a name="null-conditional-operators--and-"></a><span data-ttu-id="fd19f-133">Operatori condizionali Null ?.</span><span class="sxs-lookup"><span data-stu-id="fd19f-133">Null-conditional operators ?.</span></span> <span data-ttu-id="fd19f-134">e ?[]</span><span class="sxs-lookup"><span data-stu-id="fd19f-134">and ?[]</span></span>

<span data-ttu-id="fd19f-135">Disponibile in C, 6 e versioni successive, un `?.`operatore null-condizionale applica un [accesso ai membri](#member-access-expression-), , o accesso [all'elemento](#indexer-operator-), `?[]`operazione all'operando solo se tale operando restituisce non null; in caso `null`contrario, restituisce .</span><span class="sxs-lookup"><span data-stu-id="fd19f-135">Available in C# 6 and later, a null-conditional operator applies a [member access](#member-access-expression-), `?.`, or [element access](#indexer-operator-), `?[]`, operation to its operand only if that operand evaluates to non-null; otherwise, it returns `null`.</span></span> <span data-ttu-id="fd19f-136">Cioè</span><span class="sxs-lookup"><span data-stu-id="fd19f-136">That is,</span></span>

- <span data-ttu-id="fd19f-137">Se `a` restituisce `null`, il `a?.x` `a?[x]` risultato di o è `null`.</span><span class="sxs-lookup"><span data-stu-id="fd19f-137">If `a` evaluates to `null`, the result of `a?.x` or `a?[x]` is `null`.</span></span>
- <span data-ttu-id="fd19f-138">Se `a` restituisce non null, il `a?.x` `a?[x]` risultato di o `a.x` è `a[x]`uguale al risultato di o , rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="fd19f-138">If `a` evaluates to non-null, the result of `a?.x` or `a?[x]` is the same as the result of `a.x` or `a[x]`, respectively.</span></span>

  > [!NOTE]
  > <span data-ttu-id="fd19f-139">Se `a.x` `a[x]` o genera un'eccezione `a?.x` o `a?[x]` la stessa `a`eccezione per non null .</span><span class="sxs-lookup"><span data-stu-id="fd19f-139">If `a.x` or `a[x]` throws an exception, `a?.x` or `a?[x]` would throw the same exception for non-null `a`.</span></span> <span data-ttu-id="fd19f-140">Se, ad `a` esempio, se è `x` un'istanza di `a`matrice `a?[x]` non <xref:System.IndexOutOfRangeException>null e si trova all'esterno dei limiti di , verrà generato un'eccezione .</span><span class="sxs-lookup"><span data-stu-id="fd19f-140">For example, if `a` is a non-null array instance and `x` is outside the bounds of `a`, `a?[x]` would throw an <xref:System.IndexOutOfRangeException>.</span></span>

<span data-ttu-id="fd19f-141">Gli operatori condizionali Null causano corto circuiti.</span><span class="sxs-lookup"><span data-stu-id="fd19f-141">The null-conditional operators are short-circuiting.</span></span> <span data-ttu-id="fd19f-142">Vale a dire, se un'operazione in una catena di operazioni condizionali di accesso a un membro o a un elemento restituisce `null`, l'esecuzione delle altre operazioni della catena viene interrotta.</span><span class="sxs-lookup"><span data-stu-id="fd19f-142">That is, if one operation in a chain of conditional member or element access operations returns `null`, the rest of the chain doesn't execute.</span></span> <span data-ttu-id="fd19f-143">Nell'esempio seguente `B` non viene valutato se `A` restituisce `null` e `C` non viene valutato se `A` oppure `B` restituisce `null`:</span><span class="sxs-lookup"><span data-stu-id="fd19f-143">In the following example, `B` is not evaluated if `A` evaluates to `null` and `C` is not evaluated if `A` or `B` evaluates to `null`:</span></span>

```csharp
A?.B?.Do(C);
A?.B?[C];
```

<span data-ttu-id="fd19f-144">Nell'esempio seguente viene illustrato l'uso degli operatori `?.` e `?[]`:</span><span class="sxs-lookup"><span data-stu-id="fd19f-144">The following example demonstrates the usage of the `?.` and `?[]` operators:</span></span>

[!code-csharp-interactive[null-conditional operators](snippets/MemberAccessOperators.cs#NullConditional)]

<span data-ttu-id="fd19f-145">Nell'esempio precedente viene inoltre utilizzato `null`l'operatore [ `??` null-coalescing](null-coalescing-operator.md) per specificare un'espressione alternativa da valutare nel caso in cui il risultato di un'operazione null-conditional sia .</span><span class="sxs-lookup"><span data-stu-id="fd19f-145">The preceding example also uses the [null-coalescing operator `??`](null-coalescing-operator.md) to specify an alternative expression to evaluate in case the result of a null-conditional operation is `null`.</span></span>

<span data-ttu-id="fd19f-146">L'operatore di accesso ai membri condizionale Null `?.` è anche noto come operatore Elvis.</span><span class="sxs-lookup"><span data-stu-id="fd19f-146">The null-conditional member access operator `?.` is also known as the Elvis operator.</span></span>

### <a name="thread-safe-delegate-invocation"></a><span data-ttu-id="fd19f-147">Chiamata a delegati thread-safe</span><span class="sxs-lookup"><span data-stu-id="fd19f-147">Thread-safe delegate invocation</span></span>

<span data-ttu-id="fd19f-148">Usare l'operatore `?.` per controllare se un delegato è diverso da Null e richiamarlo in un modo thread-safe, ad esempio, quando si [genera un evento](../../../standard/events/how-to-raise-and-consume-events.md), come illustrato nel codice seguente:</span><span class="sxs-lookup"><span data-stu-id="fd19f-148">Use the `?.` operator to check if a delegate is non-null and invoke it in a thread-safe way (for example, when you [raise an event](../../../standard/events/how-to-raise-and-consume-events.md)), as the following code shows:</span></span>

```csharp
PropertyChanged?.Invoke(…)
```

<span data-ttu-id="fd19f-149">Il codice equivale alla versione C# 5 o precedente del codice seguente:</span><span class="sxs-lookup"><span data-stu-id="fd19f-149">That code is equivalent to the following code that you would use in C# 5 or earlier:</span></span>

```csharp
var handler = this.PropertyChanged;
if (handler != null)
{
    handler(…);
}
```

## <a name="invocation-expression-"></a><span data-ttu-id="fd19f-150">Espressione di chiamata ()</span><span class="sxs-lookup"><span data-stu-id="fd19f-150">Invocation expression ()</span></span>

<span data-ttu-id="fd19f-151">Usare le parentesi, `()`, per chiamare un [metodo](../../programming-guide/classes-and-structs/methods.md) oppure richiamare un [delegato](../../programming-guide/delegates/index.md).</span><span class="sxs-lookup"><span data-stu-id="fd19f-151">Use parentheses, `()`, to call a [method](../../programming-guide/classes-and-structs/methods.md) or invoke a [delegate](../../programming-guide/delegates/index.md).</span></span>

<span data-ttu-id="fd19f-152">L'esempio seguente illustra come chiamare un metodo, con o senza argomenti, e come richiamare un delegato:</span><span class="sxs-lookup"><span data-stu-id="fd19f-152">The following example demonstrates how to call a method, with or without arguments, and invoke a delegate:</span></span>

[!code-csharp-interactive[invocation with ()](snippets/MemberAccessOperators.cs#Invocation)]

<span data-ttu-id="fd19f-153">Le parentesi si usano anche per richiamare un [costruttore](../../programming-guide/classes-and-structs/constructors.md) con l'operatore [`new`](new-operator.md).</span><span class="sxs-lookup"><span data-stu-id="fd19f-153">You also use parentheses when you invoke a [constructor](../../programming-guide/classes-and-structs/constructors.md) with the [`new`](new-operator.md) operator.</span></span>

### <a name="other-usages-of-"></a><span data-ttu-id="fd19f-154">Altri utilizzi di ()</span><span class="sxs-lookup"><span data-stu-id="fd19f-154">Other usages of ()</span></span>

<span data-ttu-id="fd19f-155">È anche possibile usare le parentesi per specificare l'ordine in cui valutare le operazioni in un'espressione.</span><span class="sxs-lookup"><span data-stu-id="fd19f-155">You also use parentheses to adjust the order in which to evaluate operations in an expression.</span></span> <span data-ttu-id="fd19f-156">Per altre informazioni, vedere [Operatori C#](index.md).</span><span class="sxs-lookup"><span data-stu-id="fd19f-156">For more information, see [C# operators](index.md).</span></span>

<span data-ttu-id="fd19f-157">Anche le [espressioni cast](type-testing-and-cast.md#cast-operator-), che eseguono conversioni dei tipi esplicite, usano le parentesi.</span><span class="sxs-lookup"><span data-stu-id="fd19f-157">[Cast expressions](type-testing-and-cast.md#cast-operator-), which perform explicit type conversions, also use parentheses.</span></span>

## <a name="index-from-end-operator-"></a><span data-ttu-id="fd19f-158">Indice dall'operatore finale</span><span class="sxs-lookup"><span data-stu-id="fd19f-158">Index from end operator ^</span></span>

<span data-ttu-id="fd19f-159">Disponibile in C , 8.0 `^` e versioni successive, l'operatore indica la posizione dell'elemento dalla fine di una sequenza.</span><span class="sxs-lookup"><span data-stu-id="fd19f-159">Available in C# 8.0 and later, the `^` operator indicates the element position from the end of a sequence.</span></span> <span data-ttu-id="fd19f-160">Per una sequenza di lunghezza `length`, `^n` punta all'elemento con offset `length - n` dall'inizio di una sequenza.</span><span class="sxs-lookup"><span data-stu-id="fd19f-160">For a sequence of length `length`, `^n` points to the element with offset `length - n` from the start of a sequence.</span></span> <span data-ttu-id="fd19f-161">Ad esempio, `^1` punta all'ultimo elemento `^length` di una sequenza e al primo elemento di una sequenza.</span><span class="sxs-lookup"><span data-stu-id="fd19f-161">For example, `^1` points to the last element of a sequence and `^length` points to the first element of a sequence.</span></span>

[!code-csharp[index from end](snippets/MemberAccessOperators.cs#IndexFromEnd)]

<span data-ttu-id="fd19f-162">Come illustrato nell'esempio `^e` precedente, <xref:System.Index?displayProperty=nameWithType> expression è del tipo.</span><span class="sxs-lookup"><span data-stu-id="fd19f-162">As the preceding example shows, expression `^e` is of the <xref:System.Index?displayProperty=nameWithType> type.</span></span> <span data-ttu-id="fd19f-163">In `^e`expression , `e` il risultato di deve `int`essere convertibile in modo implicito in .</span><span class="sxs-lookup"><span data-stu-id="fd19f-163">In expression `^e`, the result of `e` must be implicitly convertible to `int`.</span></span>

<span data-ttu-id="fd19f-164">È inoltre possibile `^` utilizzare l'operatore con l'operatore [di intervallo](#range-operator-) per creare un intervallo di indici.</span><span class="sxs-lookup"><span data-stu-id="fd19f-164">You also can use the `^` operator with the [range operator](#range-operator-) to create a range of indices.</span></span> <span data-ttu-id="fd19f-165">Per ulteriori informazioni, consultate [Indici e intervalli.](../../tutorials/ranges-indexes.md)</span><span class="sxs-lookup"><span data-stu-id="fd19f-165">For more information, see [Indices and ranges](../../tutorials/ranges-indexes.md).</span></span>

## <a name="range-operator-"></a><span data-ttu-id="fd19f-166">Operatore di intervallo ..</span><span class="sxs-lookup"><span data-stu-id="fd19f-166">Range operator ..</span></span>

<span data-ttu-id="fd19f-167">Disponibile in C , 8.0 `..` e versioni successive, l'operatore specifica l'inizio e la fine di un intervallo di indici come operandi.</span><span class="sxs-lookup"><span data-stu-id="fd19f-167">Available in C# 8.0 and later, the `..` operator specifies the start and end of a range of indices as its operands.</span></span> <span data-ttu-id="fd19f-168">L'operando di sinistra è un inizio *inclusivo* di un intervallo.</span><span class="sxs-lookup"><span data-stu-id="fd19f-168">The left-hand operand is an *inclusive* start of a range.</span></span> <span data-ttu-id="fd19f-169">L'operando di destra è *un'estremità esclusiva* di un intervallo.</span><span class="sxs-lookup"><span data-stu-id="fd19f-169">The right-hand operand is an *exclusive* end of a range.</span></span> <span data-ttu-id="fd19f-170">Uno degli operandi può essere un indice dall'inizio o dalla fine di una sequenza, come illustrato nell'esempio seguente:Either of operands can be an index from the start or from the end of a sequence, as the following example shows:</span><span class="sxs-lookup"><span data-stu-id="fd19f-170">Either of operands can be an index from the start or from the end of a sequence, as the following example shows:</span></span>

[!code-csharp[range examples](snippets/MemberAccessOperators.cs#Ranges)]

<span data-ttu-id="fd19f-171">Come illustrato nell'esempio `a..b` precedente, <xref:System.Range?displayProperty=nameWithType> expression è del tipo.</span><span class="sxs-lookup"><span data-stu-id="fd19f-171">As the preceding example shows, expression `a..b` is of the <xref:System.Range?displayProperty=nameWithType> type.</span></span> <span data-ttu-id="fd19f-172">In `a..b`expression , `a` i `b` risultati di e devono `int` <xref:System.Index>essere convertibili in modo implicito in o .</span><span class="sxs-lookup"><span data-stu-id="fd19f-172">In expression `a..b`, the results of `a` and `b` must be implicitly convertible to `int` or <xref:System.Index>.</span></span>

<span data-ttu-id="fd19f-173">È possibile omettere uno qualsiasi degli operandi dell'operatore `..` per ottenere un intervallo aperto:</span><span class="sxs-lookup"><span data-stu-id="fd19f-173">You can omit any of the operands of the `..` operator to obtain an open-ended range:</span></span>

- <span data-ttu-id="fd19f-174">`a..`equivale a`a..^0`</span><span class="sxs-lookup"><span data-stu-id="fd19f-174">`a..` is equivalent to `a..^0`</span></span>
- <span data-ttu-id="fd19f-175">`..b`equivale a`0..b`</span><span class="sxs-lookup"><span data-stu-id="fd19f-175">`..b` is equivalent to `0..b`</span></span>
- <span data-ttu-id="fd19f-176">`..`equivale a`0..^0`</span><span class="sxs-lookup"><span data-stu-id="fd19f-176">`..` is equivalent to `0..^0`</span></span>

[!code-csharp[ranges with omitted operands](snippets/MemberAccessOperators.cs#RangesOptional)]

<span data-ttu-id="fd19f-177">Per ulteriori informazioni, consultate [Indici e intervalli.](../../tutorials/ranges-indexes.md)</span><span class="sxs-lookup"><span data-stu-id="fd19f-177">For more information, see [Indices and ranges](../../tutorials/ranges-indexes.md).</span></span>

## <a name="operator-overloadability"></a><span data-ttu-id="fd19f-178">Overload degli operatori</span><span class="sxs-lookup"><span data-stu-id="fd19f-178">Operator overloadability</span></span>

<span data-ttu-id="fd19f-179">Gli `.` `()`operatori `^`, `..` , e non possono essere sottoposti a overload.</span><span class="sxs-lookup"><span data-stu-id="fd19f-179">The `.`, `()`, `^`, and `..` operators cannot be overloaded.</span></span> <span data-ttu-id="fd19f-180">Anche l'operatore `[]` viene considerato un operatore che non supporta l'overload.</span><span class="sxs-lookup"><span data-stu-id="fd19f-180">The `[]` operator is also considered a non-overloadable operator.</span></span> <span data-ttu-id="fd19f-181">Per il supporto dell'indicizzazione con tipi definiti dall'utente, usare gli [indicizzatori](../../programming-guide/indexers/index.md).</span><span class="sxs-lookup"><span data-stu-id="fd19f-181">Use [indexers](../../programming-guide/indexers/index.md) to support indexing with user-defined types.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="fd19f-182">Specifiche del linguaggio C#</span><span class="sxs-lookup"><span data-stu-id="fd19f-182">C# language specification</span></span>

<span data-ttu-id="fd19f-183">Per altre informazioni, vedere le sezioni seguenti delle [specifiche del linguaggio C#](~/_csharplang/spec/introduction.md):</span><span class="sxs-lookup"><span data-stu-id="fd19f-183">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="fd19f-184">Accesso ai membri</span><span class="sxs-lookup"><span data-stu-id="fd19f-184">Member access</span></span>](~/_csharplang/spec/expressions.md#member-access)
- [<span data-ttu-id="fd19f-185">Accesso a elementi</span><span class="sxs-lookup"><span data-stu-id="fd19f-185">Element access</span></span>](~/_csharplang/spec/expressions.md#element-access)
- [<span data-ttu-id="fd19f-186">Operatori condizionali Null</span><span class="sxs-lookup"><span data-stu-id="fd19f-186">Null-conditional operator</span></span>](~/_csharplang/spec/expressions.md#null-conditional-operator)
- [<span data-ttu-id="fd19f-187">Espressioni di chiamata</span><span class="sxs-lookup"><span data-stu-id="fd19f-187">Invocation expressions</span></span>](~/_csharplang/spec/expressions.md#invocation-expressions)

<span data-ttu-id="fd19f-188">Per ulteriori informazioni su indici e intervalli, vedere la nota della [proposta di feature.](~/_csharplang/proposals/csharp-8.0/ranges.md)</span><span class="sxs-lookup"><span data-stu-id="fd19f-188">For more information about indices and ranges, see the [feature proposal note](~/_csharplang/proposals/csharp-8.0/ranges.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fd19f-189">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="fd19f-189">See also</span></span>

- [<span data-ttu-id="fd19f-190">Informazioni di riferimento su C#</span><span class="sxs-lookup"><span data-stu-id="fd19f-190">C# reference</span></span>](../index.md)
- [<span data-ttu-id="fd19f-191">Operatori C#</span><span class="sxs-lookup"><span data-stu-id="fd19f-191">C# operators</span></span>](index.md)
- <span data-ttu-id="fd19f-192">[?? (null-coalescing operator)](null-coalescing-operator.md) ?? (operatore null-coalescing)</span><span class="sxs-lookup"><span data-stu-id="fd19f-192">[?? (null-coalescing operator)](null-coalescing-operator.md)</span></span>
- [<span data-ttu-id="fd19f-193">:: (operatore)</span><span class="sxs-lookup"><span data-stu-id="fd19f-193">:: operator</span></span>](namespace-alias-qualifier.md)

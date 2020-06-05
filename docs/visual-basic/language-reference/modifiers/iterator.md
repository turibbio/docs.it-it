---
title: Iterator
ms.date: 07/20/2015
f1_keywords:
- vb.Iterator
helpviewer_keywords:
- Iterator keyword [Visual Basic]
ms.assetid: 69cb0b04-ac87-49d0-bcfe-810c0d60daff
ms.openlocfilehash: bb19289c69f4c523363e88e91a58f37d232b07df
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396233"
---
# <a name="iterator-visual-basic"></a><span data-ttu-id="4e089-102">Iteratore (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="4e089-102">Iterator (Visual Basic)</span></span>
<span data-ttu-id="4e089-103">Specifica che una funzione o una funzione di `Get` accesso è un iteratore.</span><span class="sxs-lookup"><span data-stu-id="4e089-103">Specifies that a function or `Get` accessor is an iterator.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="4e089-104">Commenti</span><span class="sxs-lookup"><span data-stu-id="4e089-104">Remarks</span></span>  
 <span data-ttu-id="4e089-105">Un *iteratore* esegue un'iterazione personalizzata su una raccolta.</span><span class="sxs-lookup"><span data-stu-id="4e089-105">An *iterator* performs a custom iteration over a collection.</span></span> <span data-ttu-id="4e089-106">Un iteratore usa l'istruzione [yield](../statements/yield-statement.md) per restituire ogni elemento della raccolta uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="4e089-106">An iterator uses the [Yield](../statements/yield-statement.md) statement to return each element in the collection one at a time.</span></span> <span data-ttu-id="4e089-107">Quando `Yield` viene raggiunta un'istruzione, viene mantenuta la posizione corrente nel codice.</span><span class="sxs-lookup"><span data-stu-id="4e089-107">When a `Yield` statement is reached, the current location in code is retained.</span></span> <span data-ttu-id="4e089-108">L'esecuzione viene riavviata a partire da quella posizione la volta successiva che viene chiamata la funzione iteratore.</span><span class="sxs-lookup"><span data-stu-id="4e089-108">Execution is restarted from that location the next time that the iterator function is called.</span></span>  
  
 <span data-ttu-id="4e089-109">Un iteratore può essere implementato come funzione o come funzione `Get` di accesso di una definizione di proprietà.</span><span class="sxs-lookup"><span data-stu-id="4e089-109">An iterator can be implemented as a function or as a `Get` accessor of a property definition.</span></span> <span data-ttu-id="4e089-110">Il `Iterator` modificatore viene visualizzato nella dichiarazione della funzione o della funzione di accesso iteratore `Get` .</span><span class="sxs-lookup"><span data-stu-id="4e089-110">The `Iterator` modifier appears in the declaration of the iterator function or `Get` accessor.</span></span>  
  
 <span data-ttu-id="4e089-111">È possibile chiamare un iteratore dal codice client usando un [per ogni... Istruzione successiva](../statements/for-each-next-statement.md).</span><span class="sxs-lookup"><span data-stu-id="4e089-111">You call an iterator from client code by using a [For Each...Next Statement](../statements/for-each-next-statement.md).</span></span>  
  
 <span data-ttu-id="4e089-112">Il tipo restituito di una funzione o di una funzione di accesso iteratore `Get` può essere <xref:System.Collections.IEnumerable> ,, <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Collections.IEnumerator> o <xref:System.Collections.Generic.IEnumerator%601> .</span><span class="sxs-lookup"><span data-stu-id="4e089-112">The return type of an iterator function or `Get` accessor can be <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, or <xref:System.Collections.Generic.IEnumerator%601>.</span></span>  
  
 <span data-ttu-id="4e089-113">Un iteratore non può avere `ByRef` parametri.</span><span class="sxs-lookup"><span data-stu-id="4e089-113">An iterator cannot have any `ByRef` parameters.</span></span>  
  
 <span data-ttu-id="4e089-114">Un iteratore non può verificarsi in un evento, costruttore di istanza, costruttore statico o distruttore statico.</span><span class="sxs-lookup"><span data-stu-id="4e089-114">An iterator cannot occur in an event, instance constructor, static constructor, or static destructor.</span></span>  
  
 <span data-ttu-id="4e089-115">Un iteratore può essere una funzione anonima.</span><span class="sxs-lookup"><span data-stu-id="4e089-115">An iterator can be an anonymous function.</span></span> <span data-ttu-id="4e089-116">Per ulteriori informazioni, vedere [iteratori](../../programming-guide/concepts/iterators.md).</span><span class="sxs-lookup"><span data-stu-id="4e089-116">For more information, see [Iterators](../../programming-guide/concepts/iterators.md).</span></span>  
  
## <a name="usage"></a><span data-ttu-id="4e089-117">Uso</span><span class="sxs-lookup"><span data-stu-id="4e089-117">Usage</span></span>  
 <span data-ttu-id="4e089-118">Il modificatore `Iterator` può essere usato nei contesti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4e089-118">The `Iterator` modifier can be used in these contexts:</span></span>  
  
- [<span data-ttu-id="4e089-119">Istruzione Function</span><span class="sxs-lookup"><span data-stu-id="4e089-119">Function Statement</span></span>](../statements/function-statement.md)  
  
- [<span data-ttu-id="4e089-120">Property Statement</span><span class="sxs-lookup"><span data-stu-id="4e089-120">Property Statement</span></span>](../statements/property-statement.md)  
  
## <a name="example"></a><span data-ttu-id="4e089-121">Esempio</span><span class="sxs-lookup"><span data-stu-id="4e089-121">Example</span></span>  
 <span data-ttu-id="4e089-122">Nell'esempio seguente viene illustrata una funzione iteratore.</span><span class="sxs-lookup"><span data-stu-id="4e089-122">The following example demonstrates an iterator function.</span></span> <span data-ttu-id="4e089-123">La funzione iteratore ha un' `Yield` istruzione che si trova all'interno di un oggetto [per... Ciclo successivo](../statements/for-next-statement.md) .</span><span class="sxs-lookup"><span data-stu-id="4e089-123">The iterator function has a `Yield` statement that is inside a [For…Next](../statements/for-next-statement.md) loop.</span></span> <span data-ttu-id="4e089-124">Ogni iterazione del corpo dell'istruzione [for each](../statements/for-each-next-statement.md) in `Main` Crea una chiamata alla `Power` funzione iteratore.</span><span class="sxs-lookup"><span data-stu-id="4e089-124">Each iteration of the [For Each](../statements/for-each-next-statement.md) statement body in `Main` creates a call to the `Power` iterator function.</span></span> <span data-ttu-id="4e089-125">Ogni chiamata alla funzione iteratore procede fino alla prossima esecuzione dell'istruzione `Yield`, che si verifica durante l'iterazione successiva del ciclo `For…Next`.</span><span class="sxs-lookup"><span data-stu-id="4e089-125">Each call to the iterator function proceeds to the next execution of the `Yield` statement, which occurs during the next iteration of the `For…Next` loop.</span></span>  
  
 [!code-vb[VbVbalrStatements#98](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#98)]  
  
## <a name="example"></a><span data-ttu-id="4e089-126">Esempio</span><span class="sxs-lookup"><span data-stu-id="4e089-126">Example</span></span>  
 <span data-ttu-id="4e089-127">Nell'esempio seguente viene illustrata una funzione di accesso `Get` che è un iteratore.</span><span class="sxs-lookup"><span data-stu-id="4e089-127">The following example demonstrates a `Get` accessor that is an iterator.</span></span> <span data-ttu-id="4e089-128">Il `Iterator` modificatore si trova nella dichiarazione della proprietà.</span><span class="sxs-lookup"><span data-stu-id="4e089-128">The `Iterator` modifier is in the property declaration.</span></span>  
  
 [!code-vb[VbVbalrStatements#99](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class2.vb#99)]  
  
 <span data-ttu-id="4e089-129">Per altri esempi, vedere [iteratori](../../programming-guide/concepts/iterators.md).</span><span class="sxs-lookup"><span data-stu-id="4e089-129">For additional examples, see [Iterators](../../programming-guide/concepts/iterators.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4e089-130">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="4e089-130">See also</span></span>

- <xref:System.Runtime.CompilerServices.IteratorStateMachineAttribute>
- [<span data-ttu-id="4e089-131">Iterators</span><span class="sxs-lookup"><span data-stu-id="4e089-131">Iterators</span></span>](../../programming-guide/concepts/iterators.md)
- [<span data-ttu-id="4e089-132">Istruzione Yield</span><span class="sxs-lookup"><span data-stu-id="4e089-132">Yield Statement</span></span>](../statements/yield-statement.md)

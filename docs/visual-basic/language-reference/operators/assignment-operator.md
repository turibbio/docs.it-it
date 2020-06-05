---
title: Operatore =
ms.date: 07/20/2015
f1_keywords:
- vb.Assign
- vb.=
helpviewer_keywords:
- = operator [Visual Basic]
- = assignment statements [Visual Basic]
ms.assetid: 2dac2e49-86c8-42f8-80c1-458452fb5e29
ms.openlocfilehash: 516cb21e02d9fb2cd4b8d72282bb74163e1fb14b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371765"
---
# <a name="-operator-visual-basic"></a><span data-ttu-id="7ac8f-102">Operatore = (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="7ac8f-102">= Operator (Visual Basic)</span></span>
<span data-ttu-id="7ac8f-103">Assegna un valore a una variabile o a una proprietà.</span><span class="sxs-lookup"><span data-stu-id="7ac8f-103">Assigns a value to a variable or property.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7ac8f-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="7ac8f-104">Syntax</span></span>  
  
```vb  
variableorproperty = value  
```  
  
## <a name="parts"></a><span data-ttu-id="7ac8f-105">Parti</span><span class="sxs-lookup"><span data-stu-id="7ac8f-105">Parts</span></span>  
 `variableorproperty`  
 <span data-ttu-id="7ac8f-106">Qualsiasi variabile scrivibile o qualsiasi proprietà.</span><span class="sxs-lookup"><span data-stu-id="7ac8f-106">Any writable variable or any property.</span></span>  
  
 `value`  
 <span data-ttu-id="7ac8f-107">Qualsiasi valore letterale, costante o espressione.</span><span class="sxs-lookup"><span data-stu-id="7ac8f-107">Any literal, constant, or expression.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="7ac8f-108">Commenti</span><span class="sxs-lookup"><span data-stu-id="7ac8f-108">Remarks</span></span>  
 <span data-ttu-id="7ac8f-109">L'elemento sul lato sinistro del segno di uguale ( `=` ) può essere una variabile scalare semplice, una proprietà o un elemento di una matrice.</span><span class="sxs-lookup"><span data-stu-id="7ac8f-109">The element on the left side of the equal sign (`=`) can be a simple scalar variable, a property, or an element of an array.</span></span> <span data-ttu-id="7ac8f-110">La variabile o la proprietà non può essere di sola [lettura](../modifiers/readonly.md).</span><span class="sxs-lookup"><span data-stu-id="7ac8f-110">The variable or property cannot be [ReadOnly](../modifiers/readonly.md).</span></span> <span data-ttu-id="7ac8f-111">L' `=` operatore assegna il valore a destra alla variabile o alla proprietà a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7ac8f-111">The `=` operator assigns the value on its right to the variable or property on its left.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="7ac8f-112">L' `=` operatore viene utilizzato anche come operatore di confronto.</span><span class="sxs-lookup"><span data-stu-id="7ac8f-112">The `=` operator is also used as a comparison operator.</span></span> <span data-ttu-id="7ac8f-113">Per informazioni dettagliate, vedere [operatori di confronto](comparison-operators.md).</span><span class="sxs-lookup"><span data-stu-id="7ac8f-113">For details, see [Comparison Operators](comparison-operators.md).</span></span>  
  
## <a name="overloading"></a><span data-ttu-id="7ac8f-114">Overload</span><span class="sxs-lookup"><span data-stu-id="7ac8f-114">Overloading</span></span>  
 <span data-ttu-id="7ac8f-115">`=`È possibile eseguire l'overload dell'operatore solo come operatore di confronto relazionale, non come operatore di assegnazione.</span><span class="sxs-lookup"><span data-stu-id="7ac8f-115">The `=` operator can be overloaded only as a relational comparison operator, not as an assignment operator.</span></span> <span data-ttu-id="7ac8f-116">Per altre informazioni, vedere [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).</span><span class="sxs-lookup"><span data-stu-id="7ac8f-116">For more information, see [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="7ac8f-117">Esempio</span><span class="sxs-lookup"><span data-stu-id="7ac8f-117">Example</span></span>  
 <span data-ttu-id="7ac8f-118">Nell'esempio seguente viene illustrato l'operatore di assegnazione.</span><span class="sxs-lookup"><span data-stu-id="7ac8f-118">The following example demonstrates the assignment operator.</span></span> <span data-ttu-id="7ac8f-119">Il valore a destra viene assegnato alla variabile a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7ac8f-119">The value on the right is assigned to the variable on the left.</span></span>  
  
 [!code-vb[VbVbalrOperators#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#9)]  
  
## <a name="see-also"></a><span data-ttu-id="7ac8f-120">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7ac8f-120">See also</span></span>

- [<span data-ttu-id="7ac8f-121">Operatore&=</span><span class="sxs-lookup"><span data-stu-id="7ac8f-121">&= Operator</span></span>](and-assignment-operator.md)
- [<span data-ttu-id="7ac8f-122">Operatore \* =</span><span class="sxs-lookup"><span data-stu-id="7ac8f-122">\*= Operator</span></span>](multiplication-assignment-operator.md)
- [<span data-ttu-id="7ac8f-123">Operatore + =</span><span class="sxs-lookup"><span data-stu-id="7ac8f-123">+= Operator</span></span>](addition-assignment-operator.md)
- [<span data-ttu-id="7ac8f-124">Operatore-= (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="7ac8f-124">-= Operator (Visual Basic)</span></span>](subtraction-assignment-operator.md)
- [<span data-ttu-id="7ac8f-125">Operatore /= (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="7ac8f-125">/= Operator (Visual Basic)</span></span>](floating-point-division-assignment-operator.md)
- [<span data-ttu-id="7ac8f-126">\\= (Operatore)</span><span class="sxs-lookup"><span data-stu-id="7ac8f-126">\\= Operator</span></span>](integer-division-assignment-operator.md)
- [<span data-ttu-id="7ac8f-127">^ = (Operatore)</span><span class="sxs-lookup"><span data-stu-id="7ac8f-127">^= Operator</span></span>](exponentiation-assignment-operator.md)
- [<span data-ttu-id="7ac8f-128">Istruzioni</span><span class="sxs-lookup"><span data-stu-id="7ac8f-128">Statements</span></span>](../../programming-guide/language-features/statements.md)
- [<span data-ttu-id="7ac8f-129">Operatori di confronto</span><span class="sxs-lookup"><span data-stu-id="7ac8f-129">Comparison Operators</span></span>](comparison-operators.md)
- [<span data-ttu-id="7ac8f-130">ReadOnly</span><span class="sxs-lookup"><span data-stu-id="7ac8f-130">ReadOnly</span></span>](../modifiers/readonly.md)
- [<span data-ttu-id="7ac8f-131">Inferenza del tipo di variabile locale</span><span class="sxs-lookup"><span data-stu-id="7ac8f-131">Local Type Inference</span></span>](../../programming-guide/language-features/variables/local-type-inference.md)

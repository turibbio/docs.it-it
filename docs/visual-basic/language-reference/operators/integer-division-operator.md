---
title: Operatore \
ms.date: 07/20/2015
f1_keywords:
- vb.\
- '\'
helpviewer_keywords:
- division operator [Visual Basic], integer
- integer division operator [Visual Basic]
- zero, division by zero
- arithmetic operators [Visual Basic], division
- division [Visual Basic], by zero
- backslash (\) [Visual Basic]
- '\ operator [Visual Basic]'
- integer quotient
- math operators [Visual Basic]
- quotients, integer
- truncation [Visual Basic], integer division
ms.assetid: 4b0ee347-950c-45c9-8e23-54bc85df208e
ms.openlocfilehash: 1f8095afc5f096928b946607adc715af49827022
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84370882"
---
# <a name="-operator-visual-basic"></a><span data-ttu-id="be212-102">Operatore \ (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="be212-102">\ Operator (Visual Basic)</span></span>
<span data-ttu-id="be212-103">Divide due numeri e restituisce un risultato intero.</span><span class="sxs-lookup"><span data-stu-id="be212-103">Divides two numbers and returns an integer result.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="be212-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="be212-104">Syntax</span></span>  
  
```vb  
expression1 \ expression2  
```  
  
## <a name="parts"></a><span data-ttu-id="be212-105">Parti</span><span class="sxs-lookup"><span data-stu-id="be212-105">Parts</span></span>  
 `expression1`  
 <span data-ttu-id="be212-106">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="be212-106">Required.</span></span> <span data-ttu-id="be212-107">Qualsiasi espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="be212-107">Any numeric expression.</span></span>  
  
 `expression2`  
 <span data-ttu-id="be212-108">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="be212-108">Required.</span></span> <span data-ttu-id="be212-109">Qualsiasi espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="be212-109">Any numeric expression.</span></span>  
  
## <a name="supported-types"></a><span data-ttu-id="be212-110">Tipi supportati</span><span class="sxs-lookup"><span data-stu-id="be212-110">Supported Types</span></span>  
 <span data-ttu-id="be212-111">Tutti i tipi numerici, inclusi i tipi senza segno e a virgola mobile e `Decimal` .</span><span class="sxs-lookup"><span data-stu-id="be212-111">All numeric types, including the unsigned and floating-point types and `Decimal`.</span></span>  
  
## <a name="result"></a><span data-ttu-id="be212-112">Risultato</span><span class="sxs-lookup"><span data-stu-id="be212-112">Result</span></span>  
 <span data-ttu-id="be212-113">Il risultato è il quoziente intero di `expression1` diviso per `expression2` , che elimina qualsiasi resto e mantiene solo la parte intera.</span><span class="sxs-lookup"><span data-stu-id="be212-113">The result is the integer quotient of `expression1` divided by `expression2`, which discards any remainder and retains only the integer portion.</span></span> <span data-ttu-id="be212-114">Questa operazione è nota come *troncamento*.</span><span class="sxs-lookup"><span data-stu-id="be212-114">This is known as *truncation*.</span></span>  
  
 <span data-ttu-id="be212-115">Il tipo di dati del risultato è un tipo numerico appropriato per i tipi di dati di `expression1` e `expression2` .</span><span class="sxs-lookup"><span data-stu-id="be212-115">The result data type is a numeric type appropriate for the data types of `expression1` and `expression2`.</span></span> <span data-ttu-id="be212-116">Vedere le tabelle "aritmetiche di interi" nei [tipi di dati dei risultati dell'operatore](data-types-of-operator-results.md).</span><span class="sxs-lookup"><span data-stu-id="be212-116">See the "Integer Arithmetic" tables in [Data Types of Operator Results](data-types-of-operator-results.md).</span></span>  
  
 <span data-ttu-id="be212-117">L' [operatore/(Visual Basic)](floating-point-division-operator.md) restituisce il quoziente completo, che mantiene il resto della parte frazionaria.</span><span class="sxs-lookup"><span data-stu-id="be212-117">The [/ Operator (Visual Basic)](floating-point-division-operator.md) returns the full quotient, which retains the remainder in the fractional portion.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="be212-118">Commenti</span><span class="sxs-lookup"><span data-stu-id="be212-118">Remarks</span></span>  
 <span data-ttu-id="be212-119">Prima di eseguire la divisione, Visual Basic tenta di convertire qualsiasi espressione numerica a virgola mobile in `Long` .</span><span class="sxs-lookup"><span data-stu-id="be212-119">Before performing the division, Visual Basic attempts to convert any floating-point numeric expression to `Long`.</span></span> <span data-ttu-id="be212-120">Se `Option Strict` è `On` , si verifica un errore del compilatore.</span><span class="sxs-lookup"><span data-stu-id="be212-120">If `Option Strict` is `On`, a compiler error occurs.</span></span> <span data-ttu-id="be212-121">Se `Option Strict` è `Off` , un <xref:System.OverflowException> è possibile se il valore non è compreso nell'intervallo del [tipo di dati Long](../data-types/long-data-type.md).</span><span class="sxs-lookup"><span data-stu-id="be212-121">If `Option Strict` is `Off`, an <xref:System.OverflowException> is possible if the value is outside the range of the [Long Data Type](../data-types/long-data-type.md).</span></span> <span data-ttu-id="be212-122">La conversione in `Long` è anche soggetta all' *arrotondamento del banco*.</span><span class="sxs-lookup"><span data-stu-id="be212-122">The conversion to `Long` is also subject to *banker's rounding*.</span></span> <span data-ttu-id="be212-123">Per ulteriori informazioni, vedere "parti frazionarie" nelle [funzioni di conversione dei tipi](../functions/type-conversion-functions.md).</span><span class="sxs-lookup"><span data-stu-id="be212-123">For more information, see "Fractional Parts" in [Type Conversion Functions](../functions/type-conversion-functions.md).</span></span>  
  
 <span data-ttu-id="be212-124">Se `expression1` o `expression2` restituisce [Nothing](../nothing.md), viene considerato come zero.</span><span class="sxs-lookup"><span data-stu-id="be212-124">If `expression1` or `expression2` evaluates to [Nothing](../nothing.md), it is treated as zero.</span></span>  
  
## <a name="attempted-division-by-zero"></a><span data-ttu-id="be212-125">Tentativo di divisione per zero</span><span class="sxs-lookup"><span data-stu-id="be212-125">Attempted Division by Zero</span></span>  
 <span data-ttu-id="be212-126">Se `expression2` restituisce zero, l' `\` operatore genera un' <xref:System.DivideByZeroException> eccezione.</span><span class="sxs-lookup"><span data-stu-id="be212-126">If `expression2` evaluates to zero, the `\` operator throws a <xref:System.DivideByZeroException> exception.</span></span> <span data-ttu-id="be212-127">Questo vale per tutti i tipi di dati numerici degli operandi.</span><span class="sxs-lookup"><span data-stu-id="be212-127">This is true for all numeric data types of the operands.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="be212-128">L' `\` operatore può essere sottoposto a *Overload*, il che significa che una classe o una struttura può ridefinire il comportamento quando un operando ha il tipo della classe o della struttura.</span><span class="sxs-lookup"><span data-stu-id="be212-128">The `\` operator can be *overloaded*, which means that a class or structure can redefine its behavior when an operand has the type of that class or structure.</span></span> <span data-ttu-id="be212-129">Se il codice usa questo operatore su una classe o una struttura di questo tipo, assicurarsi di comprendere il comportamento ridefinito.</span><span class="sxs-lookup"><span data-stu-id="be212-129">If your code uses this operator on such a class or structure, be sure you understand its redefined behavior.</span></span> <span data-ttu-id="be212-130">Per altre informazioni, vedere [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).</span><span class="sxs-lookup"><span data-stu-id="be212-130">For more information, see [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="be212-131">Esempio</span><span class="sxs-lookup"><span data-stu-id="be212-131">Example</span></span>  
 <span data-ttu-id="be212-132">Nell'esempio seguente viene usato l' `\` operatore per eseguire la divisione di interi.</span><span class="sxs-lookup"><span data-stu-id="be212-132">The following example uses the `\` operator to perform integer division.</span></span> <span data-ttu-id="be212-133">Il risultato è un numero intero che rappresenta il quoziente integer dei due operandi, con il resto ignorato.</span><span class="sxs-lookup"><span data-stu-id="be212-133">The result is an integer that represents the integer quotient of the two operands, with the remainder discarded.</span></span>  
  
 [!code-vb[VbVbalrOperators#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#18)]  
  
 <span data-ttu-id="be212-134">Le espressioni nell'esempio precedente restituiscono rispettivamente i valori 2, 3, 33 e-22.</span><span class="sxs-lookup"><span data-stu-id="be212-134">The expressions in the preceding example return values of 2, 3, 33, and -22, respectively.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="be212-135">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="be212-135">See also</span></span>

- [<span data-ttu-id="be212-136">\\= (Operatore)</span><span class="sxs-lookup"><span data-stu-id="be212-136">\\= Operator</span></span>](integer-division-assignment-operator.md)
- [<span data-ttu-id="be212-137">Operatore/(Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="be212-137">/ Operator (Visual Basic)</span></span>](floating-point-division-operator.md)
- [<span data-ttu-id="be212-138">Option Strict Statement</span><span class="sxs-lookup"><span data-stu-id="be212-138">Option Strict Statement</span></span>](../statements/option-strict-statement.md)
- [<span data-ttu-id="be212-139">Operatori aritmetici</span><span class="sxs-lookup"><span data-stu-id="be212-139">Arithmetic Operators</span></span>](arithmetic-operators.md)
- [<span data-ttu-id="be212-140">Precedenza tra gli operatori in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="be212-140">Operator Precedence in Visual Basic</span></span>](operator-precedence.md)
- [<span data-ttu-id="be212-141">Elenco degli operatori per funzionalità</span><span class="sxs-lookup"><span data-stu-id="be212-141">Operators Listed by Functionality</span></span>](operators-listed-by-functionality.md)
- [<span data-ttu-id="be212-142">Operatori aritmetici in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="be212-142">Arithmetic Operators in Visual Basic</span></span>](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)

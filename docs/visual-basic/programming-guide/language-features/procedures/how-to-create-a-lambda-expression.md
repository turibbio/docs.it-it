---
title: "Procedura: creare un'espressione lambda"
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [Visual Basic]
- expressions [Visual Basic], lambda
ms.assetid: 3279bd5c-80f7-410a-a7ba-f7085ed36aa5
ms.openlocfilehash: 7affc84fa501ba98bdfa93835f0b0e381580b9bd
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388387"
---
# <a name="how-to-create-a-lambda-expression-visual-basic"></a><span data-ttu-id="c68b0-102">Procedura: creare un'espressione lambda (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="c68b0-102">How to: Create a Lambda Expression (Visual Basic)</span></span>
<span data-ttu-id="c68b0-103">Un' *espressione lambda* è una funzione o una subroutine che non ha un nome.</span><span class="sxs-lookup"><span data-stu-id="c68b0-103">A *lambda expression* is a function or subroutine that does not have a name.</span></span> <span data-ttu-id="c68b0-104">Un'espressione lambda può essere usata ovunque sia valido un tipo delegato.</span><span class="sxs-lookup"><span data-stu-id="c68b0-104">A lambda expression can be used wherever a delegate type is valid.</span></span>  
  
### <a name="to-create-a-single-line-lambda-expression-function"></a><span data-ttu-id="c68b0-105">Per creare una funzione di espressione lambda a riga singola</span><span class="sxs-lookup"><span data-stu-id="c68b0-105">To create a single-line lambda expression function</span></span>  
  
1. <span data-ttu-id="c68b0-106">In ogni situazione in cui è possibile usare un tipo delegato, digitare la parola chiave `Function` , come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c68b0-106">In any situation where a delegate type could be used, type the keyword `Function`, as in the following example:</span></span>  
  
     <span data-ttu-id="c68b0-107">`Dim add1 =`   `Function`</span><span class="sxs-lookup"><span data-stu-id="c68b0-107">`Dim add1 =`   `Function`</span></span>  
  
2. <span data-ttu-id="c68b0-108">Tra parentesi, immediatamente dopo `Function` , digitare i parametri della funzione.</span><span class="sxs-lookup"><span data-stu-id="c68b0-108">In parentheses, directly after `Function`, type the parameters of the function.</span></span> <span data-ttu-id="c68b0-109">Si noti che non viene specificato un nome dopo `Function` .</span><span class="sxs-lookup"><span data-stu-id="c68b0-109">Notice that you do not specify a name after `Function`.</span></span>  
  
     <span data-ttu-id="c68b0-110">`Dim add1 = Function`   `(num As Integer)`</span><span class="sxs-lookup"><span data-stu-id="c68b0-110">`Dim add1 = Function`   `(num As Integer)`</span></span>  
  
3. <span data-ttu-id="c68b0-111">Dopo l'elenco dei parametri, digitare una singola espressione come corpo della funzione.</span><span class="sxs-lookup"><span data-stu-id="c68b0-111">Following the parameter list, type a single expression as the body of the function.</span></span> <span data-ttu-id="c68b0-112">Il valore restituito dall'espressione è il valore restituito dalla funzione.</span><span class="sxs-lookup"><span data-stu-id="c68b0-112">The value that the expression evaluates to is the value returned by the function.</span></span> <span data-ttu-id="c68b0-113">Non si utilizza una `As` clausola per specificare il tipo restituito.</span><span class="sxs-lookup"><span data-stu-id="c68b0-113">You do not use an `As` clause to specify the return type.</span></span>  
  
     [!code-vb[VbVbalrLambdas#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#1)]  
  
     <span data-ttu-id="c68b0-114">Per chiamare l'espressione lambda, passare un argomento integer.</span><span class="sxs-lookup"><span data-stu-id="c68b0-114">You call the lambda expression by passing in an integer argument.</span></span>  
  
     [!code-vb[VbVbalrLambdas#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#2)]  
  
4. <span data-ttu-id="c68b0-115">In alternativa, lo stesso risultato viene ottenuto nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c68b0-115">Alternatively, the same result is accomplished by the following example:</span></span>  
  
     [!code-vb[VbVbalrLambdas#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#3)]  
  
### <a name="to-create-a-single-line-lambda-expression-subroutine"></a><span data-ttu-id="c68b0-116">Per creare una subroutine di espressione lambda a riga singola</span><span class="sxs-lookup"><span data-stu-id="c68b0-116">To create a single-line lambda expression subroutine</span></span>  
  
1. <span data-ttu-id="c68b0-117">In ogni situazione in cui è possibile usare un tipo delegato, digitare la parola chiave `Sub` , come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="c68b0-117">In any situation where a delegate type could be used, type the keyword `Sub`, as shown in the following example.</span></span>  
  
     <span data-ttu-id="c68b0-118">`Dim add1 =`   `Sub`</span><span class="sxs-lookup"><span data-stu-id="c68b0-118">`Dim add1 =`   `Sub`</span></span>  
  
2. <span data-ttu-id="c68b0-119">In parentesi, immediatamente dopo `Sub` , digitare i parametri della subroutine.</span><span class="sxs-lookup"><span data-stu-id="c68b0-119">In parentheses, directly after `Sub`, type the parameters of the subroutine.</span></span> <span data-ttu-id="c68b0-120">Si noti che non viene specificato un nome dopo `Sub` .</span><span class="sxs-lookup"><span data-stu-id="c68b0-120">Notice that you do not specify a name after `Sub`.</span></span>  
  
     <span data-ttu-id="c68b0-121">`Dim add1 = Sub`   `(msg As String)`</span><span class="sxs-lookup"><span data-stu-id="c68b0-121">`Dim add1 = Sub`   `(msg As String)`</span></span>  
  
3. <span data-ttu-id="c68b0-122">Dopo l'elenco dei parametri, digitare una singola istruzione come corpo della subroutine.</span><span class="sxs-lookup"><span data-stu-id="c68b0-122">Following the parameter list, type a single statement as the body of the subroutine.</span></span>  
  
     [!code-vb[VbVbalrLambdas#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#17)]  
  
     <span data-ttu-id="c68b0-123">Per chiamare l'espressione lambda, passare un argomento di stringa.</span><span class="sxs-lookup"><span data-stu-id="c68b0-123">You call the lambda expression by passing in a string argument.</span></span>  
  
     [!code-vb[VbVbalrLambdas#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#18)]  
  
### <a name="to-create-a-multiline-lambda-expression-function"></a><span data-ttu-id="c68b0-124">Per creare una funzione di espressione lambda su più righe</span><span class="sxs-lookup"><span data-stu-id="c68b0-124">To create a multiline lambda expression function</span></span>  
  
1. <span data-ttu-id="c68b0-125">In ogni situazione in cui è possibile usare un tipo delegato, digitare la parola chiave `Function` , come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="c68b0-125">In any situation where a delegate type could be used, type the keyword `Function`, as shown in the following example.</span></span>  
  
     <span data-ttu-id="c68b0-126">`Dim add1 =`   `Function`</span><span class="sxs-lookup"><span data-stu-id="c68b0-126">`Dim add1 =`   `Function`</span></span>  
  
2. <span data-ttu-id="c68b0-127">Tra parentesi, immediatamente dopo `Function` , digitare i parametri della funzione.</span><span class="sxs-lookup"><span data-stu-id="c68b0-127">In parentheses, directly after `Function`, type the parameters of the function.</span></span> <span data-ttu-id="c68b0-128">Si noti che non viene specificato un nome dopo `Function` .</span><span class="sxs-lookup"><span data-stu-id="c68b0-128">Notice that you do not specify a name after `Function`.</span></span>  
  
     <span data-ttu-id="c68b0-129">`Dim add1 = Function`   `(index As Integer)`</span><span class="sxs-lookup"><span data-stu-id="c68b0-129">`Dim add1 = Function`   `(index As Integer)`</span></span>  
  
3. <span data-ttu-id="c68b0-130">Premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="c68b0-130">Press ENTER.</span></span> <span data-ttu-id="c68b0-131">L' `End Function` istruzione viene aggiunta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c68b0-131">The `End Function` statement is automatically added.</span></span>  
  
4. <span data-ttu-id="c68b0-132">All'interno del corpo della funzione, aggiungere il codice seguente per creare un'espressione e restituire il valore.</span><span class="sxs-lookup"><span data-stu-id="c68b0-132">Within the body of the function, add the following code to create an expression and return the value.</span></span> <span data-ttu-id="c68b0-133">Non si utilizza una `As` clausola per specificare il tipo restituito.</span><span class="sxs-lookup"><span data-stu-id="c68b0-133">You do not use an `As` clause to specify the return type.</span></span>  
  
     [!code-vb[VbVbalrLambdas#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#19)]  
  
     <span data-ttu-id="c68b0-134">Per chiamare l'espressione lambda, passare un argomento integer.</span><span class="sxs-lookup"><span data-stu-id="c68b0-134">You call the lambda expression by passing in an integer argument.</span></span>  
  
     [!code-vb[VbVbalrLambdas#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#20)]  
  
### <a name="to-create-a-multiline-lambda-expression-subroutine"></a><span data-ttu-id="c68b0-135">Per creare una subroutine per un'espressione lambda su più righe</span><span class="sxs-lookup"><span data-stu-id="c68b0-135">To create a multiline lambda expression subroutine</span></span>  
  
1. <span data-ttu-id="c68b0-136">In ogni situazione in cui è possibile usare un tipo delegato, digitare la parola chiave `Sub` , come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c68b0-136">In any situation where a delegate type could be used, type the keyword `Sub`, as shown in the following example:</span></span>  
  
     <span data-ttu-id="c68b0-137">`Dim add1 =`   `Sub`</span><span class="sxs-lookup"><span data-stu-id="c68b0-137">`Dim add1 =`   `Sub`</span></span>  
  
2. <span data-ttu-id="c68b0-138">In parentesi, immediatamente dopo `Sub` , digitare i parametri della subroutine.</span><span class="sxs-lookup"><span data-stu-id="c68b0-138">In parentheses, directly after `Sub`, type the parameters of the subroutine.</span></span> <span data-ttu-id="c68b0-139">Si noti che non viene specificato un nome dopo `Sub` .</span><span class="sxs-lookup"><span data-stu-id="c68b0-139">Notice that you do not specify a name after `Sub`.</span></span>  
  
     <span data-ttu-id="c68b0-140">`Dim add1 = Sub`  `(msg As String)`</span><span class="sxs-lookup"><span data-stu-id="c68b0-140">`Dim add1 = Sub`  `(msg As String)`</span></span>  
  
3. <span data-ttu-id="c68b0-141">Premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="c68b0-141">Press ENTER.</span></span> <span data-ttu-id="c68b0-142">L' `End Sub` istruzione viene aggiunta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c68b0-142">The `End Sub` statement is automatically added.</span></span>  
  
4. <span data-ttu-id="c68b0-143">All'interno del corpo della funzione, aggiungere il codice seguente da eseguire quando viene richiamata la subroutine.</span><span class="sxs-lookup"><span data-stu-id="c68b0-143">Within the body of the function, add the following code to execute when the subroutine is invoked.</span></span>  
  
     [!code-vb[VbVbalrLambdas#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#21)]  
  
     <span data-ttu-id="c68b0-144">Per chiamare l'espressione lambda, passare un argomento di stringa.</span><span class="sxs-lookup"><span data-stu-id="c68b0-144">You call the lambda expression by passing in a string argument.</span></span>  
  
     [!code-vb[VbVbalrLambdas#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#22)]  
  
## <a name="example"></a><span data-ttu-id="c68b0-145">Esempio</span><span class="sxs-lookup"><span data-stu-id="c68b0-145">Example</span></span>  
 <span data-ttu-id="c68b0-146">Un uso comune delle espressioni lambda consiste nel definire una funzione che può essere passata come argomento per un parametro il cui tipo è `Delegate` .</span><span class="sxs-lookup"><span data-stu-id="c68b0-146">A common use of lambda expressions is to define a function that can be passed in as the argument for a parameter whose type is `Delegate`.</span></span> <span data-ttu-id="c68b0-147">Nell'esempio seguente, il <xref:System.Diagnostics.Process.GetProcesses%2A> metodo restituisce una matrice dei processi in esecuzione nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="c68b0-147">In the following example, the <xref:System.Diagnostics.Process.GetProcesses%2A> method returns an array of the processes running on the local computer.</span></span> <span data-ttu-id="c68b0-148">Il <xref:System.Linq.Enumerable.Where%2A> metodo della <xref:System.Linq.Enumerable> classe richiede un `Boolean` delegato come argomento.</span><span class="sxs-lookup"><span data-stu-id="c68b0-148">The <xref:System.Linq.Enumerable.Where%2A> method from the <xref:System.Linq.Enumerable> class requires a `Boolean` delegate as its argument.</span></span> <span data-ttu-id="c68b0-149">A tale scopo, viene utilizzata l'espressione lambda nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="c68b0-149">The lambda expression in the example is used for that purpose.</span></span> <span data-ttu-id="c68b0-150">Restituisce `True` per ogni processo che ha un solo thread e che sono selezionati in `filteredList` .</span><span class="sxs-lookup"><span data-stu-id="c68b0-150">It returns `True` for each process that has only one thread, and those are selected in `filteredList`.</span></span>  
  
 [!code-vb[VbVbalrLambdas#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class4.vb#10)]  
  
 <span data-ttu-id="c68b0-151">L'esempio precedente è equivalente al codice seguente, scritto nella sintassi LINQ (Language-Integrated Query):</span><span class="sxs-lookup"><span data-stu-id="c68b0-151">The previous example is equivalent to the following code, which is written in Language-Integrated Query (LINQ) syntax:</span></span>  
  
 [!code-vb[VbVbalrLambdas#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class5.vb#11)]  
  
## <a name="see-also"></a><span data-ttu-id="c68b0-152">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c68b0-152">See also</span></span>

- <xref:System.Linq.Enumerable>
- [<span data-ttu-id="c68b0-153">Espressioni lambda</span><span class="sxs-lookup"><span data-stu-id="c68b0-153">Lambda Expressions</span></span>](./lambda-expressions.md)
- [<span data-ttu-id="c68b0-154">Istruzione Function</span><span class="sxs-lookup"><span data-stu-id="c68b0-154">Function Statement</span></span>](../../../language-reference/statements/function-statement.md)
- [<span data-ttu-id="c68b0-155">Istruzione Sub</span><span class="sxs-lookup"><span data-stu-id="c68b0-155">Sub Statement</span></span>](../../../language-reference/statements/sub-statement.md)
- [<span data-ttu-id="c68b0-156">Delegati</span><span class="sxs-lookup"><span data-stu-id="c68b0-156">Delegates</span></span>](../delegates/index.md)
- [<span data-ttu-id="c68b0-157">Procedura: passare una routine a un'altra routine in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="c68b0-157">How to: Pass Procedures to Another Procedure in Visual Basic</span></span>](../delegates/how-to-pass-procedures-to-another-procedure.md)
- [<span data-ttu-id="c68b0-158">Istruzione Delegate</span><span class="sxs-lookup"><span data-stu-id="c68b0-158">Delegate Statement</span></span>](../../../language-reference/statements/delegate-statement.md)
- [<span data-ttu-id="c68b0-159">Introduzione a LINQ in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="c68b0-159">Introduction to LINQ in Visual Basic</span></span>](../linq/introduction-to-linq.md)

---
title: Operatori di test dei tipi ed espressione di cast - Riferimento in C
description: Informazioni sugli operatori C# che è possibile usare per controllare il tipo del risultato di un'espressione e, se necessario, convertirlo in un altro tipo.
ms.date: 06/21/2019
author: pkulikov
f1_keywords:
- is_CSharpKeyword
- as_CSharpKeyword
- ()_CSharpKeyword
- typeof_CSharpKeyword
helpviewer_keywords:
- type-testing operators [C#]
- conversion operators [C#]
- type conversion [C#]
- is operator [C#]
- as operator [C#]
- cast operator [C#]
- cast expression [C#]
- () operator [C#]
- typeof operator [C#]
ms.openlocfilehash: bc293c359af5744eebc63c0d0f94b4cebe3d450a
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "82021247"
---
# <a name="type-testing-operators-and-cast-expression-c-reference"></a><span data-ttu-id="dade3-103">Operatori di test dei tipi ed espressione cast (riferimenti per C</span><span class="sxs-lookup"><span data-stu-id="dade3-103">Type-testing operators and cast expression (C# reference)</span></span>

<span data-ttu-id="dade3-104">È possibile utilizzare gli operatori e le espressioni seguenti per eseguire il controllo dei tipi o la conversione del tipo:</span><span class="sxs-lookup"><span data-stu-id="dade3-104">You can use the following operators and expressions to perform type checking or type conversion:</span></span>

- <span data-ttu-id="dade3-105">[operatore is](#is-operator): per controllare se il tipo di runtime di un'espressione è compatibile con un determinato tipo</span><span class="sxs-lookup"><span data-stu-id="dade3-105">[is operator](#is-operator): to check if the runtime type of an expression is compatible with a given type</span></span>
- <span data-ttu-id="dade3-106">[operatore as](#as-operator): per convertire in modo esplicito un'espressione in un tipo specificato se il tipo di runtime è compatibile con esso</span><span class="sxs-lookup"><span data-stu-id="dade3-106">[as operator](#as-operator): to explicitly convert an expression to a given type if its runtime type is compatible with that type</span></span>
- <span data-ttu-id="dade3-107">[espressione cast](#cast-expression): per eseguire una conversione esplicita</span><span class="sxs-lookup"><span data-stu-id="dade3-107">[cast expression](#cast-expression): to perform an explicit conversion</span></span>
- <span data-ttu-id="dade3-108">[operatore typeof](#typeof-operator): per ottenere l'istanza <xref:System.Type?displayProperty=nameWithType> per un tipo</span><span class="sxs-lookup"><span data-stu-id="dade3-108">[typeof operator](#typeof-operator): to obtain the <xref:System.Type?displayProperty=nameWithType> instance for a type</span></span>

## <a name="is-operator"></a><span data-ttu-id="dade3-109">Operatore is</span><span class="sxs-lookup"><span data-stu-id="dade3-109">is operator</span></span>

<span data-ttu-id="dade3-110">L' operatore `is` controlla se il tipo di runtime del risultato di un'espressione è compatibile con un determinato tipo.</span><span class="sxs-lookup"><span data-stu-id="dade3-110">The `is` operator checks if the runtime type of an expression result is compatible with a given type.</span></span> <span data-ttu-id="dade3-111">A partire dalla versione 7.0 di C, l'operatore verifica anche il `is` risultato di un'espressione rispetto a un modello.</span><span class="sxs-lookup"><span data-stu-id="dade3-111">Beginning with C# 7.0, the `is` operator also tests an expression result against a pattern.</span></span>

<span data-ttu-id="dade3-112">L'espressione con l'operatore di test del tipo `is` ha il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="dade3-112">The expression with the type-testing `is` operator has the following form</span></span>

```csharp
E is T
```

<span data-ttu-id="dade3-113">in cui `E` è un'espressione che restituisce un valore e `T` è il nome di un tipo o un parametro di tipo.</span><span class="sxs-lookup"><span data-stu-id="dade3-113">where `E` is an expression that returns a value and `T` is the name of a type or a type parameter.</span></span> <span data-ttu-id="dade3-114">`E` non può essere un metodo anonimo o un'espressione lambda.</span><span class="sxs-lookup"><span data-stu-id="dade3-114">`E` cannot be an anonymous method or a lambda expression.</span></span>

<span data-ttu-id="dade3-115">L'espressione `E is T` restituisce `true` se il risultato di `E` è diverso da null e può essere convertito nel tipo `T` da una conversione di riferimento, una conversione boxing o una conversione unboxing; in caso contrario, restituisce `false`.</span><span class="sxs-lookup"><span data-stu-id="dade3-115">The `E is T` expression returns `true` if the result of `E` is non-null and can be converted to type `T` by a reference conversion, a boxing conversion, or an unboxing conversion; otherwise, it returns `false`.</span></span> <span data-ttu-id="dade3-116">L'operatore `is` non considera le conversioni definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="dade3-116">The `is` operator doesn't consider user-defined conversions.</span></span>

<span data-ttu-id="dade3-117">L'esempio seguente dimostra che l'operatore `is` restituisce `true` se il tipo di runtime del risultato di un'espressione deriva da un determinato tipo, ovvero se esiste una conversione di riferimento tra i tipi:</span><span class="sxs-lookup"><span data-stu-id="dade3-117">The following example demonstrates that the `is` operator returns `true` if the runtime type of an expression result derives from a given type, that is, there exists a reference conversion between types:</span></span>

[!code-csharp[is with reference conversion](snippets/TypeTestingAndConversionOperators.cs#IsWithReferenceConversion)]

<span data-ttu-id="dade3-118">L'esempio seguente `is` mostra che l'operatore prende in considerazione le conversioni boxing e unboxing, ma non considera [le conversioni numeriche:](../builtin-types/numeric-conversions.md)</span><span class="sxs-lookup"><span data-stu-id="dade3-118">The next example shows that the `is` operator takes into account boxing and unboxing conversions but doesn't consider [numeric conversions](../builtin-types/numeric-conversions.md):</span></span>

[!code-csharp-interactive[is with int](snippets/TypeTestingAndConversionOperators.cs#IsWithInt)]

<span data-ttu-id="dade3-119">Per informazioni sulle conversioni C#, vedere il capito [Conversioni](~/_csharplang/spec/conversions.md) della [specifica del linguaggio C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dade3-119">For information about C# conversions, see the [Conversions](~/_csharplang/spec/conversions.md) chapter of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

### <a name="type-testing-with-pattern-matching"></a><span data-ttu-id="dade3-120">Test del tipo con criteri di ricerca</span><span class="sxs-lookup"><span data-stu-id="dade3-120">Type testing with pattern matching</span></span>

<span data-ttu-id="dade3-121">A partire dalla versione 7.0 di C, l'operatore verifica anche il `is` risultato di un'espressione rispetto a un modello.</span><span class="sxs-lookup"><span data-stu-id="dade3-121">Beginning with C# 7.0, the `is` operator also tests an expression result against a pattern.</span></span> <span data-ttu-id="dade3-122">In particolare, supporta il criterio del tipo nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="dade3-122">In particular, it supports the type pattern in the following form:</span></span>

```csharp
E is T v
```

<span data-ttu-id="dade3-123">in cui `E` è un'espressione che restituisce un valore, `T` è il nome di un tipo o un parametro di tipo e `v` è una nuova variabile locale di tipo `T`.</span><span class="sxs-lookup"><span data-stu-id="dade3-123">where `E` is an expression that returns a value, `T` is the name of a type or a type parameter, and `v` is a new local variable of type `T`.</span></span> <span data-ttu-id="dade3-124">Se il risultato di `E` è diverso da null e può essere convertito in `T` con una conversione di riferimento, boxing o unboxing, l'espressione `E is T v` restituisce `true` e il valore convertito del risultato di `E` viene assegnato alla variabile `v`.</span><span class="sxs-lookup"><span data-stu-id="dade3-124">If the result of `E` is non-null and can be converted to `T` by a reference, boxing, or unboxing conversion, the `E is T v` expression returns `true` and the converted value of the result of `E` is assigned to variable `v`.</span></span>

<span data-ttu-id="dade3-125">L'esempio seguente illustra l'uso dell'operatore `is` con un criterio del tipo:</span><span class="sxs-lookup"><span data-stu-id="dade3-125">The following example demonstrates the usage of the `is` operator with the type pattern:</span></span>

[!code-csharp-interactive[is with type pattern](snippets/TypeTestingAndConversionOperators.cs#IsTypePattern)]

<span data-ttu-id="dade3-126">Per altre informazioni sul criterio del tipo e sugli altri criteri supportati, vedere [Criteri di ricerca con is](../keywords/is.md#pattern-matching-with-is).</span><span class="sxs-lookup"><span data-stu-id="dade3-126">For more information about the type pattern and other supported patterns, see [Pattern matching with is](../keywords/is.md#pattern-matching-with-is).</span></span>

## <a name="as-operator"></a><span data-ttu-id="dade3-127">operatore as</span><span class="sxs-lookup"><span data-stu-id="dade3-127">as operator</span></span>

<span data-ttu-id="dade3-128">L'operatore `as` converte in modo esplicito il risultato di un'espressione in un tipo di valore nullable o di riferimento specificato.</span><span class="sxs-lookup"><span data-stu-id="dade3-128">The `as` operator explicitly converts the result of an expression to a given reference or nullable value type.</span></span> <span data-ttu-id="dade3-129">Se la conversione non è possibile, l'operatore `as` restituisce `null`.</span><span class="sxs-lookup"><span data-stu-id="dade3-129">If the conversion is not possible, the `as` operator returns `null`.</span></span> <span data-ttu-id="dade3-130">A differenza di `as` [un'espressione cast](#cast-expression), l'operatore non genera mai un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="dade3-130">Unlike a [cast expression](#cast-expression), the `as` operator never throws an exception.</span></span>

<span data-ttu-id="dade3-131">Un'espressione nel formato</span><span class="sxs-lookup"><span data-stu-id="dade3-131">The expression of the form</span></span>

```csharp
E as T
```

<span data-ttu-id="dade3-132">in cui `E` è un'espressione che restituisce un valore e `T` è il nome di un tipo o un parametro di tipo, produce lo stesso risultato di</span><span class="sxs-lookup"><span data-stu-id="dade3-132">where `E` is an expression that returns a value and `T` is the name of a type or a type parameter, produces the same result as</span></span>

```csharp
E is T ? (T)(E) : (T)null
```

<span data-ttu-id="dade3-133">con la differenza che `E` viene valutato una sola volta.</span><span class="sxs-lookup"><span data-stu-id="dade3-133">except that `E` is only evaluated once.</span></span>

<span data-ttu-id="dade3-134">L'operatore `as` considera solo conversioni di riferimenti, nullable, boxing e unboxing.</span><span class="sxs-lookup"><span data-stu-id="dade3-134">The `as` operator considers only reference, nullable, boxing, and unboxing conversions.</span></span> <span data-ttu-id="dade3-135">Non è possibile usare l'operatore `as` per eseguire una conversione definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="dade3-135">You cannot use the `as` operator to perform a user-defined conversion.</span></span> <span data-ttu-id="dade3-136">A tale scopo, utilizzare [un'espressione cast](#cast-expression).</span><span class="sxs-lookup"><span data-stu-id="dade3-136">To do that, use a [cast expression](#cast-expression).</span></span>

<span data-ttu-id="dade3-137">Nell'esempio seguente viene illustrato l'uso dell'operatore `as`:</span><span class="sxs-lookup"><span data-stu-id="dade3-137">The following example demonstrates the usage of the `as` operator:</span></span>

[!code-csharp-interactive[as operator](snippets/TypeTestingAndConversionOperators.cs#AsOperator)]

> [!NOTE]
> <span data-ttu-id="dade3-138">Come mostrato nell'esempio precedente, è necessario confrontare il risultato dell'espressione `as` con `null` per verificare se la conversione riesce.</span><span class="sxs-lookup"><span data-stu-id="dade3-138">As the preceding example shows, you need to compare the result of the `as` expression with `null` to check if the conversion is successful.</span></span> <span data-ttu-id="dade3-139">A partire dalla versione 7.0 di C, è possibile usare [l'operatore is](#type-testing-with-pattern-matching) sia per verificare se la conversione ha esito positivo e, in caso di esito positivo, assegnare il risultato a una nuova variabile.</span><span class="sxs-lookup"><span data-stu-id="dade3-139">Beginning with C# 7.0, you can use the [is operator](#type-testing-with-pattern-matching) both to test if the conversion succeeds and, if it succeeds, assign its result to a new variable.</span></span>

## <a name="cast-expression"></a><span data-ttu-id="dade3-140">Espressione cast</span><span class="sxs-lookup"><span data-stu-id="dade3-140">Cast expression</span></span>

<span data-ttu-id="dade3-141">Un'espressione cast nel formato `(T)E` esegue una conversione esplicita del risultato dell'espressione `E` nel tipo `T`.</span><span class="sxs-lookup"><span data-stu-id="dade3-141">A cast expression of the form `(T)E` performs an explicit conversion of the result of expression `E` to type `T`.</span></span> <span data-ttu-id="dade3-142">Se non esiste alcuna conversione esplicita dal tipo `E` al tipo `T`, si verifica un errore in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="dade3-142">If no explicit conversion exists from the type of `E` to type `T`, a compile-time error occurs.</span></span> <span data-ttu-id="dade3-143">In fase di esecuzione, è possibile che una conversione esplicita non riesca e che un'espressione cast generi un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="dade3-143">At run time, an explicit conversion might not succeed and a cast expression might throw an exception.</span></span>

<span data-ttu-id="dade3-144">L'esempio seguente illustra conversioni esplicite numeriche e di riferimento:</span><span class="sxs-lookup"><span data-stu-id="dade3-144">The following example demonstrates explicit numeric and reference conversions:</span></span>

[!code-csharp-interactive[cast expression](snippets/TypeTestingAndConversionOperators.cs#Cast)]

<span data-ttu-id="dade3-145">Per informazioni sulle conversioni esplicite supportate, vedere la sezione [Conversioni esplicite](~/_csharplang/spec/conversions.md#explicit-conversions) della [specifica del linguaggio C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dade3-145">For information about supported explicit conversions, see the [Explicit conversions](~/_csharplang/spec/conversions.md#explicit-conversions) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span> <span data-ttu-id="dade3-146">Per informazioni su come definire una conversione personalizzata del tipo esplicito o implicito, vedere [Operatori di conversione definiti dall'utente](user-defined-conversion-operators.md).</span><span class="sxs-lookup"><span data-stu-id="dade3-146">For information about how to define a custom explicit or implicit type conversion, see [User-defined conversion operators](user-defined-conversion-operators.md).</span></span>

### <a name="other-usages-of-"></a><span data-ttu-id="dade3-147">Altri utilizzi di ()</span><span class="sxs-lookup"><span data-stu-id="dade3-147">Other usages of ()</span></span>

<span data-ttu-id="dade3-148">È possibile usare le parentesi anche per [chiamare un metodo oppure richiamare un delegato](member-access-operators.md#invocation-expression-).</span><span class="sxs-lookup"><span data-stu-id="dade3-148">You also use parentheses to [call a method or invoke a delegate](member-access-operators.md#invocation-expression-).</span></span>

<span data-ttu-id="dade3-149">Le parentesi possono essere usate anche per specificare l'ordine in cui valutare le operazioni in un'espressione.</span><span class="sxs-lookup"><span data-stu-id="dade3-149">Other use of parentheses is to adjust the order in which to evaluate operations in an expression.</span></span> <span data-ttu-id="dade3-150">Per altre informazioni, vedere [Operatori C#](index.md).</span><span class="sxs-lookup"><span data-stu-id="dade3-150">For more information, see [C# operators](index.md).</span></span>

## <a name="typeof-operator"></a><span data-ttu-id="dade3-151">Operatore typeof</span><span class="sxs-lookup"><span data-stu-id="dade3-151">typeof operator</span></span>

<span data-ttu-id="dade3-152">L'operatore `typeof` ottiene l'istanza <xref:System.Type?displayProperty=nameWithType> per un tipo.</span><span class="sxs-lookup"><span data-stu-id="dade3-152">The `typeof` operator obtains the <xref:System.Type?displayProperty=nameWithType> instance for a type.</span></span> <span data-ttu-id="dade3-153">L'argomento dell'operatore `typeof` deve essere il nome o il parametro di un tipo, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="dade3-153">The argument to the `typeof` operator must be the name of a type or a type parameter, as the following example shows:</span></span>

[!code-csharp-interactive[typeof operator](snippets/TypeTestingAndConversionOperators.cs#TypeOf)]

<span data-ttu-id="dade3-154">È inoltre possibile `typeof` utilizzare l'operatore con tipi generici non associati.</span><span class="sxs-lookup"><span data-stu-id="dade3-154">You can also use the `typeof` operator with unbound generic types.</span></span> <span data-ttu-id="dade3-155">Il nome di un tipo generico non associato deve contenere il numero appropriato di virgole, ovvero una in meno rispetto al numero di parametri del tipo.</span><span class="sxs-lookup"><span data-stu-id="dade3-155">The name of an unbound generic type must contain the appropriate number of commas, which is one less than the number of type parameters.</span></span> <span data-ttu-id="dade3-156">L'esempio seguente illustra l'uso dell'operatore `typeof` con un tipo generico non associato:</span><span class="sxs-lookup"><span data-stu-id="dade3-156">The following example shows the usage of the `typeof` operator with an unbound generic type:</span></span>

[!code-csharp-interactive[typeof unbound generic](snippets/TypeTestingAndConversionOperators.cs#TypeOfUnboundGeneric)]

<span data-ttu-id="dade3-157">Un'espressione non può essere un argomento dell'operatore `typeof`.</span><span class="sxs-lookup"><span data-stu-id="dade3-157">An expression cannot be an argument of the `typeof` operator.</span></span> <span data-ttu-id="dade3-158">Per ottenere <xref:System.Type?displayProperty=nameWithType> l'istanza per il tipo di <xref:System.Object.GetType%2A?displayProperty=nameWithType> runtime di un risultato dell'espressione, utilizzare il metodo .</span><span class="sxs-lookup"><span data-stu-id="dade3-158">To get the <xref:System.Type?displayProperty=nameWithType> instance for the runtime type of an expression result, use the <xref:System.Object.GetType%2A?displayProperty=nameWithType> method.</span></span>

### <a name="type-testing-with-the-typeof-operator"></a><span data-ttu-id="dade3-159">Test del tipo con l'operatore `typeof`</span><span class="sxs-lookup"><span data-stu-id="dade3-159">Type testing with the `typeof` operator</span></span>

<span data-ttu-id="dade3-160">Usare l'operatore `typeof` per controllare se il tipo di runtime del risultato dell'espressione corrisponde esattamente a un determinato tipo.</span><span class="sxs-lookup"><span data-stu-id="dade3-160">Use the `typeof` operator to check if the runtime type of the expression result exactly matches a given type.</span></span> <span data-ttu-id="dade3-161">L'esempio seguente illustra la differenza tra il controllo del tipo eseguito con l'operatore `typeof` e il controllo del tipo con l'[operatore is](#is-operator):</span><span class="sxs-lookup"><span data-stu-id="dade3-161">The following example demonstrates the difference between type checking performed with the `typeof` operator and the [is operator](#is-operator):</span></span>

[!code-csharp[typeof vs is](snippets/TypeTestingAndConversionOperators.cs#TypeCheckWithTypeOf)]

## <a name="operator-overloadability"></a><span data-ttu-id="dade3-162">Overload degli operatori</span><span class="sxs-lookup"><span data-stu-id="dade3-162">Operator overloadability</span></span>

<span data-ttu-id="dade3-163">Gli `is` `as`operatori `typeof` , e non possono essere sottoposti a overload.</span><span class="sxs-lookup"><span data-stu-id="dade3-163">The `is`, `as`, and `typeof` operators cannot be overloaded.</span></span>

<span data-ttu-id="dade3-164">Un tipo definito dall'utente non può eseguire l'overload dell'operatore `()`, ma può definire conversioni di tipi personalizzate che possano essere eseguite da un'espressione cast.</span><span class="sxs-lookup"><span data-stu-id="dade3-164">A user-defined type cannot overload the `()` operator, but can define custom type conversions that can be performed by a cast expression.</span></span> <span data-ttu-id="dade3-165">Per altre informazioni, vedere [Operatori di conversione definiti dall'utente](user-defined-conversion-operators.md).</span><span class="sxs-lookup"><span data-stu-id="dade3-165">For more information, see [User-defined conversion operators](user-defined-conversion-operators.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="dade3-166">Specifiche del linguaggio C#</span><span class="sxs-lookup"><span data-stu-id="dade3-166">C# language specification</span></span>

<span data-ttu-id="dade3-167">Per altre informazioni, vedere le sezioni seguenti delle [specifiche del linguaggio C#](~/_csharplang/spec/introduction.md):</span><span class="sxs-lookup"><span data-stu-id="dade3-167">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="dade3-168">Operatore is</span><span class="sxs-lookup"><span data-stu-id="dade3-168">The is operator</span></span>](~/_csharplang/spec/expressions.md#the-is-operator)
- [<span data-ttu-id="dade3-169">Operatore as</span><span class="sxs-lookup"><span data-stu-id="dade3-169">The as operator</span></span>](~/_csharplang/spec/expressions.md#the-as-operator)
- [<span data-ttu-id="dade3-170">Espressioni cast</span><span class="sxs-lookup"><span data-stu-id="dade3-170">Cast expressions</span></span>](~/_csharplang/spec/expressions.md#cast-expressions)
- [<span data-ttu-id="dade3-171">Operatore typeof</span><span class="sxs-lookup"><span data-stu-id="dade3-171">The typeof operator</span></span>](~/_csharplang/spec/expressions.md#the-typeof-operator)

## <a name="see-also"></a><span data-ttu-id="dade3-172">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dade3-172">See also</span></span>

- [<span data-ttu-id="dade3-173">Informazioni di riferimento su C#</span><span class="sxs-lookup"><span data-stu-id="dade3-173">C# reference</span></span>](../index.md)
- [<span data-ttu-id="dade3-174">Operatori C#</span><span class="sxs-lookup"><span data-stu-id="dade3-174">C# operators</span></span>](index.md)
- [<span data-ttu-id="dade3-175">Come eseguire il cast in modo sicuro utilizzando criteri di ricerca e gli operatori is e as</span><span class="sxs-lookup"><span data-stu-id="dade3-175">How to safely cast by using pattern matching and the is and as operators</span></span>](../../how-to/safely-cast-using-pattern-matching-is-and-as-operators.md)
- [<span data-ttu-id="dade3-176">Generics in .NET</span><span class="sxs-lookup"><span data-stu-id="dade3-176">Generics in .NET</span></span>](../../../standard/generics/index.md)

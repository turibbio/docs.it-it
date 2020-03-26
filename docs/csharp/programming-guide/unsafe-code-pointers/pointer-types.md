---
title: Tipi di puntatori - Guida per programmatori C#
ms.date: 04/20/2018
helpviewer_keywords:
- unsafe code [C#], pointers
- pointers [C#]
ms.openlocfilehash: 7bbfa6b2238458d3248da830cf9d6ac36551b431
ms.sourcegitcommit: 2514f4e3655081dcfe1b22470c0c28500f952c42
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/18/2020
ms.locfileid: "79507035"
---
# <a name="pointer-types-c-programming-guide"></a><span data-ttu-id="5afe2-102">Tipi di puntatori (Guida per programmatori C#)</span><span class="sxs-lookup"><span data-stu-id="5afe2-102">Pointer types (C# Programming Guide)</span></span>

<span data-ttu-id="5afe2-103">In un contesto unsafe, un tipo può essere un tipo di puntatore, un tipo di valore o un tipo di riferimento.</span><span class="sxs-lookup"><span data-stu-id="5afe2-103">In an unsafe context, a type may be a pointer type, a value type, or a reference type.</span></span> <span data-ttu-id="5afe2-104">La dichiarazione di un tipo di puntatore può assumere uno dei seguenti formati:</span><span class="sxs-lookup"><span data-stu-id="5afe2-104">A pointer type declaration takes one of the following forms:</span></span>

``` csharp
type* identifier;
void* identifier; //allowed but not recommended
```

<span data-ttu-id="5afe2-105">Il tipo specificato prima di `*` in un tipo di puntatore viene chiamato **tipo referente**.</span><span class="sxs-lookup"><span data-stu-id="5afe2-105">The type specified before the `*` in a pointer type is called the **referent type**.</span></span> <span data-ttu-id="5afe2-106">Solo un [tipo non gestito](../../language-reference/builtin-types/unmanaged-types.md) può essere un tipo referente.</span><span class="sxs-lookup"><span data-stu-id="5afe2-106">Only an [unmanaged type](../../language-reference/builtin-types/unmanaged-types.md) can be a referent type.</span></span>

<span data-ttu-id="5afe2-107">I tipi di puntatore non ereditano da [object](../../language-reference/builtin-types/reference-types.md). Non sono inoltre previste conversioni tra i tipi di puntatore e `object`.</span><span class="sxs-lookup"><span data-stu-id="5afe2-107">Pointer types do not inherit from [object](../../language-reference/builtin-types/reference-types.md) and no conversions exist between pointer types and `object`.</span></span> <span data-ttu-id="5afe2-108">Con i puntatori non sono inoltre supportate le operazioni di boxing e unboxing.</span><span class="sxs-lookup"><span data-stu-id="5afe2-108">Also, boxing and unboxing do not support pointers.</span></span> <span data-ttu-id="5afe2-109">È tuttavia possibile eseguire conversioni tra tipi di puntatore diversi e tra tipi di puntatore e tipi integrali.</span><span class="sxs-lookup"><span data-stu-id="5afe2-109">However, you can convert between different pointer types and between pointer types and integral types.</span></span>

<span data-ttu-id="5afe2-110">Quando si dichiarano più puntatori nella stessa dichiarazione, l'asterisco (\*) viene scritto solo con il tipo sottostante. Non viene utilizzato come prefisso di ogni nome di puntatore.</span><span class="sxs-lookup"><span data-stu-id="5afe2-110">When you declare multiple pointers in the same declaration, the asterisk (\*) is written together with the underlying type only; it is not used as a prefix to each pointer name.</span></span> <span data-ttu-id="5afe2-111">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5afe2-111">For example:</span></span>

```csharp
int* p1, p2, p3;   // Ok
int *p1, *p2, *p3;   // Invalid in C#
```

<span data-ttu-id="5afe2-112">Un puntatore non può puntare a un riferimento o a uno [struct](../../language-reference/builtin-types/struct.md) che contiene riferimenti, perché un riferimento a un oggetto può essere sottoposto a processi di Garbage Collection anche se un puntatore punta a esso.</span><span class="sxs-lookup"><span data-stu-id="5afe2-112">A pointer cannot point to a reference or to a [struct](../../language-reference/builtin-types/struct.md) that contains references, because an object reference can be garbage collected even if a pointer is pointing to it.</span></span> <span data-ttu-id="5afe2-113">Il Garbage Collector non tiene traccia degli altri tipi di puntatore che puntano all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5afe2-113">The garbage collector does not keep track of whether an object is being pointed to by any pointer types.</span></span>

<span data-ttu-id="5afe2-114">Il valore della variabile del puntatore di tipo `myType*` è l'indirizzo di una variabile di tipo `myType`.</span><span class="sxs-lookup"><span data-stu-id="5afe2-114">The value of the pointer variable of type `myType*` is the address of a variable of type `myType`.</span></span> <span data-ttu-id="5afe2-115">Di seguito sono riportati alcuni esempi di dichiarazioni di tipi di puntatore:</span><span class="sxs-lookup"><span data-stu-id="5afe2-115">The following are examples of pointer type declarations:</span></span>

|<span data-ttu-id="5afe2-116">Esempio</span><span class="sxs-lookup"><span data-stu-id="5afe2-116">Example</span></span>|<span data-ttu-id="5afe2-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5afe2-117">Description</span></span>|
|-------------|-----------------|
|`int* p`|<span data-ttu-id="5afe2-118">`p` è un puntatore a un Integer.</span><span class="sxs-lookup"><span data-stu-id="5afe2-118">`p` is a pointer to an integer.</span></span>|
|`int** p`|<span data-ttu-id="5afe2-119">`p` è un puntatore a un puntatore a un Integer.</span><span class="sxs-lookup"><span data-stu-id="5afe2-119">`p` is a pointer to a pointer to an integer.</span></span>|
|`int*[] p`|<span data-ttu-id="5afe2-120">`p` è una matrice unidimensionale di puntatori a Integer.</span><span class="sxs-lookup"><span data-stu-id="5afe2-120">`p` is a single-dimensional array of pointers to integers.</span></span>|
|`char* p`|<span data-ttu-id="5afe2-121">`p` è un puntatore a un carattere.</span><span class="sxs-lookup"><span data-stu-id="5afe2-121">`p` is a pointer to a char.</span></span>|
|`void* p`|<span data-ttu-id="5afe2-122">`p` è un puntatore a un tipo sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="5afe2-122">`p` is a pointer to an unknown type.</span></span>|

<span data-ttu-id="5afe2-123">Per accedere al contenuto nella posizione a cui punta la variabile del puntatore, è possibile utilizzare \*, ovvero l'operatore di riferimento indiretto a puntatore.</span><span class="sxs-lookup"><span data-stu-id="5afe2-123">The pointer indirection operator \* can be used to access the contents at the location pointed to by the pointer variable.</span></span> <span data-ttu-id="5afe2-124">Si consideri ad esempio la seguente dichiarazione:</span><span class="sxs-lookup"><span data-stu-id="5afe2-124">For example, consider the following declaration:</span></span>

```csharp
int* myVariable;
```

<span data-ttu-id="5afe2-125">L'espressione `*myVariable` indica la variabile `int` individuata all'indirizzo contenuto in `myVariable`.</span><span class="sxs-lookup"><span data-stu-id="5afe2-125">The expression `*myVariable` denotes the `int` variable found at the address contained in `myVariable`.</span></span>

<span data-ttu-id="5afe2-126">Gli argomenti [Istruzione fixed](../../language-reference/keywords/fixed-statement.md) e [Conversioni di puntatori](./pointer-conversions.md) includono diversi esempi di puntatori.</span><span class="sxs-lookup"><span data-stu-id="5afe2-126">There are several examples of pointers in the topics [fixed Statement](../../language-reference/keywords/fixed-statement.md) and [Pointer Conversions](./pointer-conversions.md).</span></span> <span data-ttu-id="5afe2-127">L'esempio seguente usa la parola chiave `unsafe` e l'istruzione `fixed` e mostra come incrementare un puntatore interno.</span><span class="sxs-lookup"><span data-stu-id="5afe2-127">The following example uses the `unsafe` keyword and the `fixed` statement, and shows how to increment an interior pointer.</span></span>  <span data-ttu-id="5afe2-128">È possibile incollare il codice nella funzione Main di un'applicazione console per eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="5afe2-128">You can paste this code into the Main function of a console application to run it.</span></span> <span data-ttu-id="5afe2-129">Questi esempi devono essere compilati con il set di opzioni del compilatore [-unsafe](../../language-reference/compiler-options/unsafe-compiler-option.md).</span><span class="sxs-lookup"><span data-stu-id="5afe2-129">These examples must be compiled with the [-unsafe](../../language-reference/compiler-options/unsafe-compiler-option.md) compiler option set.</span></span>

[!code-csharp[Using pointer types](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#5)]

<span data-ttu-id="5afe2-130">Non è possibile applicare l'operatore di riferimento indiretto a un puntatore di tipo `void*`.</span><span class="sxs-lookup"><span data-stu-id="5afe2-130">You cannot apply the indirection operator to a pointer of type `void*`.</span></span> <span data-ttu-id="5afe2-131">È tuttavia possibile eseguire un cast per convertire un puntatore void in qualsiasi altro tipo e viceversa.</span><span class="sxs-lookup"><span data-stu-id="5afe2-131">However, you can use a cast to convert a void pointer to any other pointer type, and vice versa.</span></span>

<span data-ttu-id="5afe2-132">Un puntatore può essere `null`.</span><span class="sxs-lookup"><span data-stu-id="5afe2-132">A pointer can be `null`.</span></span> <span data-ttu-id="5afe2-133">Se l'operatore di riferimento indiretto viene applicato a un puntatore Null, si otterrà un comportamento definito dall'implementazione.</span><span class="sxs-lookup"><span data-stu-id="5afe2-133">Applying the indirection operator to a null pointer causes an implementation-defined behavior.</span></span>

<span data-ttu-id="5afe2-134">Tenere presente che il passaggio di puntatori tra metodi può generare un comportamento non definito.</span><span class="sxs-lookup"><span data-stu-id="5afe2-134">Passing pointers between methods can cause undefined behavior.</span></span> <span data-ttu-id="5afe2-135">Prendere in considerazione un metodo che restituisce un puntatore a una variabile locale tramite un parametro `in`, `out` o `ref` oppure come risultato della funzione.</span><span class="sxs-lookup"><span data-stu-id="5afe2-135">Consider a method that returns a pointer to a local variable through an `in`, `out`, or `ref` parameter or as the function result.</span></span> <span data-ttu-id="5afe2-136">Se il puntatore è stato impostato in un blocco fisso, la variabile a cui punta potrebbe non essere più fissa.</span><span class="sxs-lookup"><span data-stu-id="5afe2-136">If the pointer was set in a fixed block, the variable to which it points may no longer be fixed.</span></span>

<span data-ttu-id="5afe2-137">Nella tabella riportata di seguito sono elencati gli operatori e le istruzioni che è possibile utilizzare con i puntatori in un contesto unsafe:</span><span class="sxs-lookup"><span data-stu-id="5afe2-137">The following table lists the operators and statements that can operate on pointers in an unsafe context:</span></span>

|<span data-ttu-id="5afe2-138">Operatore/istruzione</span><span class="sxs-lookup"><span data-stu-id="5afe2-138">Operator/Statement</span></span>|<span data-ttu-id="5afe2-139">Uso</span><span class="sxs-lookup"><span data-stu-id="5afe2-139">Use</span></span>|
|-------------------------|---------|
|`*`|<span data-ttu-id="5afe2-140">Esegue il riferimento indiretto al puntatore.</span><span class="sxs-lookup"><span data-stu-id="5afe2-140">Performs pointer indirection.</span></span>|
|`->`|<span data-ttu-id="5afe2-141">Accede a un membro di struct tramite un puntatore.</span><span class="sxs-lookup"><span data-stu-id="5afe2-141">Accesses a member of a struct through a pointer.</span></span>|
|`[]`|<span data-ttu-id="5afe2-142">Indicizza un puntatore.</span><span class="sxs-lookup"><span data-stu-id="5afe2-142">Indexes a pointer.</span></span>|
|`&`|<span data-ttu-id="5afe2-143">Ottiene l'indirizzo di una variabile.</span><span class="sxs-lookup"><span data-stu-id="5afe2-143">Obtains the address of a variable.</span></span>|
|<span data-ttu-id="5afe2-144">`++` e `--`</span><span class="sxs-lookup"><span data-stu-id="5afe2-144">`++` and `--`</span></span>|<span data-ttu-id="5afe2-145">Incrementa e decrementa puntatori.</span><span class="sxs-lookup"><span data-stu-id="5afe2-145">Increments and decrements pointers.</span></span>|
|<span data-ttu-id="5afe2-146">`+` e `-`</span><span class="sxs-lookup"><span data-stu-id="5afe2-146">`+` and `-`</span></span>|<span data-ttu-id="5afe2-147">Utilizza l'aritmetica dei puntatori.</span><span class="sxs-lookup"><span data-stu-id="5afe2-147">Performs pointer arithmetic.</span></span>|
|<span data-ttu-id="5afe2-148">`==`, `!=`, `<`, `>`, `<=` e `>=`</span><span class="sxs-lookup"><span data-stu-id="5afe2-148">`==`, `!=`, `<`, `>`, `<=`, and `>=`</span></span>|<span data-ttu-id="5afe2-149">Confronta puntatori.</span><span class="sxs-lookup"><span data-stu-id="5afe2-149">Compares pointers.</span></span>|
|[`stackalloc`](../../language-reference/operators/stackalloc.md)|<span data-ttu-id="5afe2-150">Alloca memoria nello stack.</span><span class="sxs-lookup"><span data-stu-id="5afe2-150">Allocates memory on the stack.</span></span>|
|[<span data-ttu-id="5afe2-151">`fixed`affermazione</span><span class="sxs-lookup"><span data-stu-id="5afe2-151">`fixed` statement</span></span>](../../language-reference/keywords/fixed-statement.md)|<span data-ttu-id="5afe2-152">Corregge temporaneamente una variabile per consentire di trovarne l'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="5afe2-152">Temporarily fixes a variable so that its address may be found.</span></span>|

<span data-ttu-id="5afe2-153">Per altre informazioni sugli operatori correlati ai puntatori, vedere [Operatori correlati ai puntatori](../../language-reference/operators/pointer-related-operators.md).</span><span class="sxs-lookup"><span data-stu-id="5afe2-153">For more information about pointer related operators, see [Pointer related operators](../../language-reference/operators/pointer-related-operators.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="5afe2-154">Specifiche del linguaggio C#</span><span class="sxs-lookup"><span data-stu-id="5afe2-154">C# language specification</span></span>

<span data-ttu-id="5afe2-155">Per altre informazioni, vedere la sezione [Tipi puntatore](~/_csharplang/spec/unsafe-code.md#pointer-types) nella [specifica del linguaggio C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5afe2-155">For more information, see the [Pointer types](~/_csharplang/spec/unsafe-code.md#pointer-types) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5afe2-156">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5afe2-156">See also</span></span>

- [<span data-ttu-id="5afe2-157">Guida alla programmazione in C</span><span class="sxs-lookup"><span data-stu-id="5afe2-157">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="5afe2-158">Codice unsafe e puntatori</span><span class="sxs-lookup"><span data-stu-id="5afe2-158">Unsafe Code and Pointers</span></span>](index.md)
- [<span data-ttu-id="5afe2-159">Conversioni di puntatori</span><span class="sxs-lookup"><span data-stu-id="5afe2-159">Pointer Conversions</span></span>](pointer-conversions.md)
- [<span data-ttu-id="5afe2-160">Tipi riferimento</span><span class="sxs-lookup"><span data-stu-id="5afe2-160">Reference types</span></span>](../../language-reference/keywords/reference-types.md)
- [<span data-ttu-id="5afe2-161">Tipi valore</span><span class="sxs-lookup"><span data-stu-id="5afe2-161">Value types</span></span>](../../language-reference/builtin-types/value-types.md)
- [<span data-ttu-id="5afe2-162">Pericoloso</span><span class="sxs-lookup"><span data-stu-id="5afe2-162">unsafe</span></span>](../../language-reference/keywords/unsafe.md)

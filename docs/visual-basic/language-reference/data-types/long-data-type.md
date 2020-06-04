---
title: Tipo di dati Long
ms.date: 01/31/2018
f1_keywords:
- vb.Long
helpviewer_keywords:
- identifier type characters [Visual Basic], &
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- '& identifier type character'
- integer numbers
- literal type characters [Visual Basic], L
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- L literal type character [Visual Basic]
- integers [Visual Basic], types
- Long keyword [Visual Basic]
- data types [Visual Basic], integral
- data types [Visual Basic], assigning
- Long data type
ms.assetid: b4770c34-1804-4f8c-b512-c10b0893e516
ms.openlocfilehash: 7c076cd2198c85560f7c63c69e051697966c9524
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415596"
---
# <a name="long-data-type-visual-basic"></a><span data-ttu-id="beebc-102">Tipo di dati Long (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="beebc-102">Long data type (Visual Basic)</span></span>

<span data-ttu-id="beebc-103">Include interi con segno a 64 bit (8 byte) compresi tra-9.223.372.036.854.775.808 E 9.223.372.036.854.775.807 (9.2... E + 18).</span><span class="sxs-lookup"><span data-stu-id="beebc-103">Holds signed 64-bit (8-byte) integers ranging in value from -9,223,372,036,854,775,808 through 9,223,372,036,854,775,807 (9.2...E+18).</span></span>

## <a name="remarks"></a><span data-ttu-id="beebc-104">Commenti</span><span class="sxs-lookup"><span data-stu-id="beebc-104">Remarks</span></span>

<span data-ttu-id="beebc-105">Utilizzare il `Long` tipo di dati per contenere numeri interi troppo grandi per il tipo di `Integer` dati.</span><span class="sxs-lookup"><span data-stu-id="beebc-105">Use the `Long` data type to contain integer numbers that are too large to fit in the `Integer` data type.</span></span>

<span data-ttu-id="beebc-106">Il valore predefinito di `Long` è 0.</span><span class="sxs-lookup"><span data-stu-id="beebc-106">The default value of `Long` is 0.</span></span>

## <a name="literal-assignments"></a><span data-ttu-id="beebc-107">Assegnazioni di valori letterali</span><span class="sxs-lookup"><span data-stu-id="beebc-107">Literal assignments</span></span>

<span data-ttu-id="beebc-108">È possibile dichiarare e inizializzare una variabile assegnandogli un valore letterale `Long` decimale, un valore letterale esadecimale, un valore letterale ottale o (a partire da Visual Basic 2017) un valore letterale binario.</span><span class="sxs-lookup"><span data-stu-id="beebc-108">You can declare and initialize a `Long` variable by assigning it a decimal literal, a hexadecimal literal, an octal literal, or (starting with Visual Basic 2017) a binary literal.</span></span> <span data-ttu-id="beebc-109">Se il valore letterale integer è esterno all'intervallo di `Long`, vale a dire se è minore di <xref:System.Int64.MinValue?displayProperty=nameWithType> o maggiore di <xref:System.Int64.MaxValue?displayProperty=nameWithType>, si verifica un errore di compilazione.</span><span class="sxs-lookup"><span data-stu-id="beebc-109">If the integer literal is outside the range of `Long` (that is, if it is less than <xref:System.Int64.MinValue?displayProperty=nameWithType> or greater than <xref:System.Int64.MaxValue?displayProperty=nameWithType>, a compilation error occurs.</span></span>

<span data-ttu-id="beebc-110">Nell'esempio seguente, i valori interi uguali a 4.294.967.296 rappresentati come valori letterali decimali, esadecimali o binari vengono assegnati a valori `Long`.</span><span class="sxs-lookup"><span data-stu-id="beebc-110">In the following example, integers equal to 4,294,967,296 that are represented as decimal, hexadecimal, and binary literals are assigned to `Long` values.</span></span>

[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Long)]

> [!NOTE]
> <span data-ttu-id="beebc-111">Usare il prefisso `&h` o `&H` per indicare un valore letterale esadecimale, il prefisso `&b` o `&B` per indicare un valore letterale binario e il prefisso `&o` o `&O` per indicare un valore letterale ottale.</span><span class="sxs-lookup"><span data-stu-id="beebc-111">You use the prefix `&h` or `&H` to denote a hexadecimal literal, the prefix `&b` or `&B` to denote a binary literal, and the prefix `&o` or `&O` to denote an octal literal.</span></span> <span data-ttu-id="beebc-112">I valori letterali decimali non hanno prefissi.</span><span class="sxs-lookup"><span data-stu-id="beebc-112">Decimal literals have no prefix.</span></span>

<span data-ttu-id="beebc-113">A partire da Visual Basic 2017, è anche possibile usare il carattere di sottolineatura, `_` , come separatore di cifre per migliorare la leggibilità, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="beebc-113">Starting with Visual Basic 2017, you can also use the underscore character, `_`, as a digit separator to enhance readability, as the following example shows.</span></span>

[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#LongS)]

<span data-ttu-id="beebc-114">A partire da Visual Basic 15,5, è anche possibile usare il carattere di sottolineatura ( `_` ) come separatore iniziale tra il prefisso e le cifre esadecimali, binarie o ottali.</span><span class="sxs-lookup"><span data-stu-id="beebc-114">Starting with Visual Basic 15.5, you can also use the underscore character (`_`) as a leading separator between the prefix and the hexadecimal, binary, or octal digits.</span></span> <span data-ttu-id="beebc-115">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="beebc-115">For example:</span></span>

```vb
Dim number As Long = &H_0FAC_0326_1489_D68C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

<span data-ttu-id="beebc-116">I valori letterali numerici possono includere anche il `L` [carattere tipo](../../programming-guide/language-features/data-types/type-characters.md) per indicare il `Long` tipo di dati, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="beebc-116">Numeric literals can also include the `L` [type character](../../programming-guide/language-features/data-types/type-characters.md) to denote the `Long` data type, as the following example shows.</span></span>

```vb
Dim number = &H_0FAC_0326_1489_D68CL
```

## <a name="programming-tips"></a><span data-ttu-id="beebc-117">Suggerimenti per la programmazione</span><span class="sxs-lookup"><span data-stu-id="beebc-117">Programming tips</span></span>

- <span data-ttu-id="beebc-118">**Considerazioni sull'interoperabilità.**</span><span class="sxs-lookup"><span data-stu-id="beebc-118">**Interop Considerations.**</span></span> <span data-ttu-id="beebc-119">Se si è connessi con componenti non scritti per il .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che `Long` in altri ambienti è presente una larghezza dati diversa (32 bit).</span><span class="sxs-lookup"><span data-stu-id="beebc-119">If you are interfacing with components not written for the .NET Framework, for example Automation or COM objects, remember that `Long` has a different data width (32 bits) in other environments.</span></span> <span data-ttu-id="beebc-120">Se si passa un argomento a 32 bit a tale componente, dichiararlo come `Integer` anziché `Long` nel nuovo codice Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="beebc-120">If you are passing a 32-bit argument to such a component, declare it as `Integer` instead of `Long` in your new Visual Basic code.</span></span>

- <span data-ttu-id="beebc-121">**Conversioni.**</span><span class="sxs-lookup"><span data-stu-id="beebc-121">**Widening.**</span></span> <span data-ttu-id="beebc-122">Il `Long` tipo di dati viene ampliato in `Decimal` , `Single` o `Double` .</span><span class="sxs-lookup"><span data-stu-id="beebc-122">The `Long` data type widens to `Decimal`, `Single`, or `Double`.</span></span> <span data-ttu-id="beebc-123">È pertanto possibile convertire `Long` in uno di questi tipi senza generare un errore <xref:System.OverflowException?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="beebc-123">This means you can convert `Long` to any one of these types without encountering a <xref:System.OverflowException?displayProperty=nameWithType> error.</span></span>

- <span data-ttu-id="beebc-124">**Digitare i caratteri.**</span><span class="sxs-lookup"><span data-stu-id="beebc-124">**Type Characters.**</span></span> <span data-ttu-id="beebc-125">Aggiungendo il carattere di tipo letterale `L` a un valore letterale, se ne determina la conversione nel tipo di dati `Long`.</span><span class="sxs-lookup"><span data-stu-id="beebc-125">Appending the literal type character `L` to a literal forces it to the `Long` data type.</span></span> <span data-ttu-id="beebc-126">Aggiungendo il carattere identificatore di tipo `&` a qualsiasi identificatore, se ne determina la conversione al tipo di dati `Long`.</span><span class="sxs-lookup"><span data-stu-id="beebc-126">Appending the identifier type character `&` to any identifier forces it to `Long`.</span></span>

- <span data-ttu-id="beebc-127">**Tipo di framework.**</span><span class="sxs-lookup"><span data-stu-id="beebc-127">**Framework Type.**</span></span> <span data-ttu-id="beebc-128">Il tipo corrispondente in .NET Framework è la struttura <xref:System.Int64?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="beebc-128">The corresponding type in the .NET Framework is the <xref:System.Int64?displayProperty=nameWithType> structure.</span></span>

## <a name="see-also"></a><span data-ttu-id="beebc-129">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="beebc-129">See also</span></span>

- <xref:System.Int64>
- [<span data-ttu-id="beebc-130">Tipi di dati</span><span class="sxs-lookup"><span data-stu-id="beebc-130">Data Types</span></span>](index.md)
- [<span data-ttu-id="beebc-131">Tipo di dati Integer</span><span class="sxs-lookup"><span data-stu-id="beebc-131">Integer Data Type</span></span>](integer-data-type.md)
- [<span data-ttu-id="beebc-132">Tipo di dati Short</span><span class="sxs-lookup"><span data-stu-id="beebc-132">Short Data Type</span></span>](short-data-type.md)
- [<span data-ttu-id="beebc-133">CString</span><span class="sxs-lookup"><span data-stu-id="beebc-133">Type Conversion Functions</span></span>](../functions/type-conversion-functions.md)
- [<span data-ttu-id="beebc-134">Riepilogo della conversione</span><span class="sxs-lookup"><span data-stu-id="beebc-134">Conversion Summary</span></span>](../keywords/conversion-summary.md)
- [<span data-ttu-id="beebc-135">Uso efficiente dei tipi di dati</span><span class="sxs-lookup"><span data-stu-id="beebc-135">Efficient Use of Data Types</span></span>](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)

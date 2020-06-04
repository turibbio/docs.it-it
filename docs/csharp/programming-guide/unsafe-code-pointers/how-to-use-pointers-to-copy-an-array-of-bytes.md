---
title: Come usare i puntatori per copiare una matrice di byte (Guida per programmatori C#)
ms.date: 04/20/2018
helpviewer_keywords:
- byte arrays [C#]
- arrays [C#], byte
- pointers [C#], to copy bytes
ms.openlocfilehash: 8c1afc06fb567a923d604ad53dc26f94178a8d60
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397415"
---
# <a name="how-to-use-pointers-to-copy-an-array-of-bytes-c-programming-guide"></a><span data-ttu-id="d9b22-102">Come usare i puntatori per copiare una matrice di byte (Guida per programmatori C#)</span><span class="sxs-lookup"><span data-stu-id="d9b22-102">How to use pointers to copy an array of bytes (C# Programming Guide)</span></span>

<span data-ttu-id="d9b22-103">Nell'esempio seguente vengono usati i puntatori per copiare i byte da una matrice a un'altra.</span><span class="sxs-lookup"><span data-stu-id="d9b22-103">The following example uses pointers to copy bytes from one array to another.</span></span>

<span data-ttu-id="d9b22-104">In questo esempio viene usata la parola chiave [unsafe](../../language-reference/keywords/unsafe.md), che consente l'uso di puntatori nel metodo `Copy`.</span><span class="sxs-lookup"><span data-stu-id="d9b22-104">This example uses the [unsafe](../../language-reference/keywords/unsafe.md) keyword, which enables you to use pointers in the `Copy` method.</span></span> <span data-ttu-id="d9b22-105">Per dichiarare i puntatori nelle matrici di origine e destinazione, viene usata l'istruzione [fixed](../../language-reference/keywords/fixed-statement.md),</span><span class="sxs-lookup"><span data-stu-id="d9b22-105">The [fixed](../../language-reference/keywords/fixed-statement.md) statement is used to declare pointers to the source and destination arrays.</span></span> <span data-ttu-id="d9b22-106">L'istruzione `fixed`*blocca* la posizione delle matrici di origine e destinazione nella memoria in modo che non vengano rimosse da Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="d9b22-106">The `fixed` statement *pins* the location of the source and destination arrays in memory so that they will not be moved by garbage collection.</span></span> <span data-ttu-id="d9b22-107">I blocchi di memoria per le matrici vengono rimossi quando il blocco `fixed` è completato.</span><span class="sxs-lookup"><span data-stu-id="d9b22-107">The memory blocks for the arrays are unpinned when the `fixed` block is completed.</span></span> <span data-ttu-id="d9b22-108">Il metodo `Copy` in questo esempio usa la parola chiave `unsafe`. Deve pertanto essere compilato con l'opzione del compilatore [-unsafe](../../language-reference/compiler-options/unsafe-compiler-option.md).</span><span class="sxs-lookup"><span data-stu-id="d9b22-108">Because the `Copy` method in this example uses the `unsafe` keyword, it must be compiled with the [-unsafe](../../language-reference/compiler-options/unsafe-compiler-option.md) compiler option.</span></span>

<span data-ttu-id="d9b22-109">L'esempio accede agli elementi di entrambe le matrici usando gli indici invece di un secondo puntatore non gestito.</span><span class="sxs-lookup"><span data-stu-id="d9b22-109">This example accesses the elements of both arrays using indices rather than a second unmanaged pointer.</span></span> <span data-ttu-id="d9b22-110">La dichiarazione dei puntatori `pSource` e `pTarget` blocca le matrici.</span><span class="sxs-lookup"><span data-stu-id="d9b22-110">The declaration of the `pSource` and `pTarget` pointers pins the arrays.</span></span> <span data-ttu-id="d9b22-111">Questa funzionalità è disponibile a partire da C# 7.3.</span><span class="sxs-lookup"><span data-stu-id="d9b22-111">This feature is available starting with C# 7.3.</span></span>

## <a name="example"></a><span data-ttu-id="d9b22-112">Esempio</span><span class="sxs-lookup"><span data-stu-id="d9b22-112">Example</span></span>

[!code-csharp[Struct with embedded inline array](snippets/FixedKeywordExamples.cs#8)]

## <a name="see-also"></a><span data-ttu-id="d9b22-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d9b22-113">See also</span></span>

- [<span data-ttu-id="d9b22-114">Guida per programmatori C#</span><span class="sxs-lookup"><span data-stu-id="d9b22-114">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="d9b22-115">Codice unsafe e puntatori</span><span class="sxs-lookup"><span data-stu-id="d9b22-115">Unsafe Code and Pointers</span></span>](index.md)
- [<span data-ttu-id="d9b22-116">-unsafe (opzioni del compilatore C#)</span><span class="sxs-lookup"><span data-stu-id="d9b22-116">-unsafe (C# Compiler Options)</span></span>](../../language-reference/compiler-options/unsafe-compiler-option.md)
- [<span data-ttu-id="d9b22-117">Garbage Collection</span><span class="sxs-lookup"><span data-stu-id="d9b22-117">Garbage Collection</span></span>](../../../standard/garbage-collection/index.md)

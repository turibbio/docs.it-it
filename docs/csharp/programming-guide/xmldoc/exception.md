---
title: <exception>-Guida per programmatori C#
ms.date: 07/20/2015
f1_keywords:
- exception
- <exception>
helpviewer_keywords:
- <exception> C# XML tag
- exception C# XML tag
ms.assetid: dd73aac5-3c74-4fcf-9498-f11bff3a2f3c
ms.openlocfilehash: fb193c586456497ee60aad941d56241ad7c6b63a
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287387"
---
# <a name="exception-c-programming-guide"></a><span data-ttu-id="b47a9-102">\<exception>(Guida per programmatori C#)</span><span class="sxs-lookup"><span data-stu-id="b47a9-102">\<exception> (C# programming guide)</span></span>

## <a name="syntax"></a><span data-ttu-id="b47a9-103">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b47a9-103">Syntax</span></span>

```xml
<exception cref="member">description</exception>
```

## <a name="parameters"></a><span data-ttu-id="b47a9-104">Parametri</span><span class="sxs-lookup"><span data-stu-id="b47a9-104">Parameters</span></span>

- <span data-ttu-id="b47a9-105">cref = " `member`"</span><span class="sxs-lookup"><span data-stu-id="b47a9-105">cref = " `member`"</span></span>

  <span data-ttu-id="b47a9-106">Riferimento ad un'eccezione disponibile dall'ambiente di compilazione corrente.</span><span class="sxs-lookup"><span data-stu-id="b47a9-106">A reference to an exception that is available from the current compilation environment.</span></span> <span data-ttu-id="b47a9-107">Il compilatore controlla che l'eccezione specificata esista e converte `member` nel nome canonico dell'elemento nel file XML di output.</span><span class="sxs-lookup"><span data-stu-id="b47a9-107">The compiler checks that the given exception exists and translates `member` to the canonical element name in the output XML.</span></span> <span data-ttu-id="b47a9-108">`member` deve essere racchiuso tra virgolette doppie (" ").</span><span class="sxs-lookup"><span data-stu-id="b47a9-108">`member` must appear within double quotation marks (" ").</span></span>

  <span data-ttu-id="b47a9-109">Per altre informazioni su come formattare `member` per fare riferimento a un tipo generico, vedere [Elaborazione del file XML](processing-the-xml-file.md).</span><span class="sxs-lookup"><span data-stu-id="b47a9-109">For more information on how to format `member` to reference a generic type, see [Processing the XML File](processing-the-xml-file.md).</span></span>

- `description`

  <span data-ttu-id="b47a9-110">Descrizione dell'eccezione.</span><span class="sxs-lookup"><span data-stu-id="b47a9-110">A description of the exception.</span></span>

## <a name="remarks"></a><span data-ttu-id="b47a9-111">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="b47a9-111">Remarks</span></span>

<span data-ttu-id="b47a9-112">Il `<exception>` tag consente di specificare le eccezioni che possono essere generate.</span><span class="sxs-lookup"><span data-stu-id="b47a9-112">The `<exception>` tag lets you specify which exceptions can be thrown.</span></span> <span data-ttu-id="b47a9-113">Questo tag può essere applicato alle definizioni di metodi, proprietà, eventi e indicizzatori.</span><span class="sxs-lookup"><span data-stu-id="b47a9-113">This tag can be applied to definitions for methods, properties, events, and indexers.</span></span>

<span data-ttu-id="b47a9-114">Compilare con [-doc](../../language-reference/compiler-options/doc-compiler-option.md) per elaborare i commenti relativi alla documentazione in un file.</span><span class="sxs-lookup"><span data-stu-id="b47a9-114">Compile with [-doc](../../language-reference/compiler-options/doc-compiler-option.md) to process documentation comments to a file.</span></span>

<span data-ttu-id="b47a9-115">Per altre informazioni sulla gestione delle eccezioni, vedere [Eccezioni e gestione delle eccezioni](../exceptions/index.md).</span><span class="sxs-lookup"><span data-stu-id="b47a9-115">For more information about exception handling, see [Exceptions and Exception Handling](../exceptions/index.md).</span></span>

## <a name="example"></a><span data-ttu-id="b47a9-116">Esempio</span><span class="sxs-lookup"><span data-stu-id="b47a9-116">Example</span></span>

[!code-csharp[csProgGuideDocComments#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#4)]

## <a name="see-also"></a><span data-ttu-id="b47a9-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b47a9-117">See also</span></span>

- [<span data-ttu-id="b47a9-118">Guida per programmatori C#</span><span class="sxs-lookup"><span data-stu-id="b47a9-118">C# programming guide</span></span>](../index.md)
- [<span data-ttu-id="b47a9-119">Tag consigliati per i commenti relativi alla documentazione</span><span class="sxs-lookup"><span data-stu-id="b47a9-119">Recommended tags for documentation comments</span></span>](recommended-tags-for-documentation-comments.md)

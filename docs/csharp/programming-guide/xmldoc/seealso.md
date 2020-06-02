---
title: <seealso> -Guida per programmatori C#
ms.date: 07/20/2015
f1_keywords:
- cref
- <seealso>
- seealso
helpviewer_keywords:
- cref [C#], see also
- seealso C# XML tag
- cref [C#]
- cross-references [C#], tags
- <seealso> C# XML tag
ms.assetid: 8e157f3f-f220-4fcf-9010-88905b080b18
ms.openlocfilehash: 1b801ac1b5a0a59d97ccc35ec78930d99223e846
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287220"
---
# <a name="seealso-c-programming-guide"></a><span data-ttu-id="ec1c0-102">\<seealso>(Guida per programmatori C#)</span><span class="sxs-lookup"><span data-stu-id="ec1c0-102">\<seealso> (C# programming guide)</span></span>

## <a name="syntax"></a><span data-ttu-id="ec1c0-103">Sintassi</span><span class="sxs-lookup"><span data-stu-id="ec1c0-103">Syntax</span></span>

```xml
<seealso cref="member"/>
```

## <a name="parameters"></a><span data-ttu-id="ec1c0-104">Parametri</span><span class="sxs-lookup"><span data-stu-id="ec1c0-104">Parameters</span></span>

- <span data-ttu-id="ec1c0-105">cref = " `member`"</span><span class="sxs-lookup"><span data-stu-id="ec1c0-105">cref = " `member`"</span></span>

  <span data-ttu-id="ec1c0-106">Riferimento a un membro o a un campo disponibile per essere chiamato dall'ambiente di compilazione corrente.</span><span class="sxs-lookup"><span data-stu-id="ec1c0-106">A reference to a member or field that is available to be called from the current compilation environment.</span></span> <span data-ttu-id="ec1c0-107">Il compilatore verifica l'esistenza dell'elemento di codice specificato e passa `member` al nome dell'elemento nel file XML di output. `member`</span><span class="sxs-lookup"><span data-stu-id="ec1c0-107">The compiler checks that the given code element exists and passes `member` to the element name in the output XML.`member`</span></span> <span data-ttu-id="ec1c0-108">deve essere racchiuso tra virgolette doppie (" ").</span><span class="sxs-lookup"><span data-stu-id="ec1c0-108">must appear within double quotation marks (" ").</span></span>

  <span data-ttu-id="ec1c0-109">Per informazioni su come creare un riferimento cref a un tipo generico, vedere l' [attributo cref](./cref-attribute.md).</span><span class="sxs-lookup"><span data-stu-id="ec1c0-109">For information on how to create a cref reference to a generic type, see [cref attribute](./cref-attribute.md).</span></span>

## <a name="remarks"></a><span data-ttu-id="ec1c0-110">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="ec1c0-110">Remarks</span></span>

<span data-ttu-id="ec1c0-111">Il `<seealso>` tag consente di specificare il testo che potrebbe essere necessario visualizzare in una sezione vedere anche.</span><span class="sxs-lookup"><span data-stu-id="ec1c0-111">The `<seealso>` tag lets you specify the text that you might want to appear in a See Also section.</span></span> <span data-ttu-id="ec1c0-112">Usare [\<see>](./see.md) per specificare un collegamento dall'interno del testo.</span><span class="sxs-lookup"><span data-stu-id="ec1c0-112">Use [\<see>](./see.md) to specify a link from within text.</span></span>

<span data-ttu-id="ec1c0-113">Compilare con [-doc](../../language-reference/compiler-options/doc-compiler-option.md) per elaborare i commenti relativi alla documentazione in un file.</span><span class="sxs-lookup"><span data-stu-id="ec1c0-113">Compile with [-doc](../../language-reference/compiler-options/doc-compiler-option.md) to process documentation comments to a file.</span></span>

## <a name="example"></a><span data-ttu-id="ec1c0-114">Esempio</span><span class="sxs-lookup"><span data-stu-id="ec1c0-114">Example</span></span>

<span data-ttu-id="ec1c0-115">[\<summary>](./summary.md)Per un esempio dell'utilizzo di \<seealso> , vedere.</span><span class="sxs-lookup"><span data-stu-id="ec1c0-115">See [\<summary>](./summary.md) for an example of using \<seealso>.</span></span>

## <a name="see-also"></a><span data-ttu-id="ec1c0-116">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ec1c0-116">See also</span></span>

- [<span data-ttu-id="ec1c0-117">Guida per programmatori C#</span><span class="sxs-lookup"><span data-stu-id="ec1c0-117">C# programming guide</span></span>](../index.md)
- [<span data-ttu-id="ec1c0-118">Tag consigliati per i commenti relativi alla documentazione</span><span class="sxs-lookup"><span data-stu-id="ec1c0-118">Recommended tags for documentation comments</span></span>](./recommended-tags-for-documentation-comments.md)

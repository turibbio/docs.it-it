---
title: <value> -Guida per programmatori C#
ms.date: 07/20/2015
f1_keywords:
- <value>
helpviewer_keywords:
- <value> C# XML tag
- value C# XML tag
ms.assetid: 08dbadaf-9ab6-43d9-9493-98e43bed199a
ms.openlocfilehash: bd6630a8d5894fda39ad289c8dd584f6d84e5490
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287194"
---
# <a name="value-c-programming-guide"></a><span data-ttu-id="18217-102">\<value>(Guida per programmatori C#)</span><span class="sxs-lookup"><span data-stu-id="18217-102">\<value> (C# programming guide)</span></span>

## <a name="syntax"></a><span data-ttu-id="18217-103">Sintassi</span><span class="sxs-lookup"><span data-stu-id="18217-103">Syntax</span></span>

```xml
<value>property-description</value>
```

## <a name="parameters"></a><span data-ttu-id="18217-104">Parametri</span><span class="sxs-lookup"><span data-stu-id="18217-104">Parameters</span></span>

- `property-description`

  <span data-ttu-id="18217-105">Descrizione della proprietà.</span><span class="sxs-lookup"><span data-stu-id="18217-105">A description for the property.</span></span>

## <a name="remarks"></a><span data-ttu-id="18217-106">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="18217-106">Remarks</span></span>

<span data-ttu-id="18217-107">Il `<value>` tag consente di descrivere il valore rappresentato da una proprietà.</span><span class="sxs-lookup"><span data-stu-id="18217-107">The `<value>` tag lets you describe the value that a property represents.</span></span> <span data-ttu-id="18217-108">Quando si aggiunge una proprietà tramite la creazione guidata codice nell'ambiente di sviluppo Visual Studio .NET, viene aggiunto un [\<summary>](./summary.md) tag per la nuova proprietà.</span><span class="sxs-lookup"><span data-stu-id="18217-108">When you add a property via code wizard in the Visual Studio .NET development environment, it adds a [\<summary>](./summary.md) tag for the new property.</span></span> <span data-ttu-id="18217-109">È quindi necessario aggiungere manualmente un `<value>` tag per descrivere il valore rappresentato dalla proprietà.</span><span class="sxs-lookup"><span data-stu-id="18217-109">You should then manually add a `<value>` tag to describe the value that the property represents.</span></span>

<span data-ttu-id="18217-110">Compilare con [-doc](../../language-reference/compiler-options/doc-compiler-option.md) per elaborare i commenti relativi alla documentazione in un file.</span><span class="sxs-lookup"><span data-stu-id="18217-110">Compile with [-doc](../../language-reference/compiler-options/doc-compiler-option.md) to process documentation comments to a file.</span></span>

## <a name="example"></a><span data-ttu-id="18217-111">Esempio</span><span class="sxs-lookup"><span data-stu-id="18217-111">Example</span></span>

[!code-csharp[csProgGuideDocComments#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#14)]

## <a name="see-also"></a><span data-ttu-id="18217-112">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="18217-112">See also</span></span>

- [<span data-ttu-id="18217-113">Guida per programmatori C#</span><span class="sxs-lookup"><span data-stu-id="18217-113">C# programming guide</span></span>](../index.md)
- [<span data-ttu-id="18217-114">Tag consigliati per i commenti relativi alla documentazione</span><span class="sxs-lookup"><span data-stu-id="18217-114">Recommended tags for documentation comments</span></span>](./recommended-tags-for-documentation-comments.md)

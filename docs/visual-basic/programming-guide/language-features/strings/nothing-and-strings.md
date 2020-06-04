---
title: Nothing e stringhe
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], Nothing
ms.assetid: 261380af-2024-4ecf-823b-43b1034d92cd
ms.openlocfilehash: 392de45b0ee1688224f3e8170b0144f1acdb0912
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84360566"
---
# <a name="nothing-and-strings-in-visual-basic"></a><span data-ttu-id="c6425-102">Comportamento di Nothing con le stringhe in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="c6425-102">Nothing and Strings in Visual Basic</span></span>
<span data-ttu-id="c6425-103">Il runtime di Visual Basic e il .NET Framework `Nothing` vengono valutati in modo diverso per le stringhe.</span><span class="sxs-lookup"><span data-stu-id="c6425-103">The Visual Basic runtime and the .NET Framework evaluate `Nothing` differently when it comes to strings.</span></span>  
  
## <a name="visual-basic-runtime-and-the-net-framework"></a><span data-ttu-id="c6425-104">Visual Basic Runtime e il .NET Framework</span><span class="sxs-lookup"><span data-stu-id="c6425-104">Visual Basic Runtime and the .NET Framework</span></span>  
 <span data-ttu-id="c6425-105">Prendere in considerazione gli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c6425-105">Consider the following example:</span></span>  
  
 [!code-vb[VbVbalrStrings#47](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#47)]  
  
 <span data-ttu-id="c6425-106">Il runtime di Visual Basic in genere restituisce `Nothing` una stringa vuota ("").</span><span class="sxs-lookup"><span data-stu-id="c6425-106">The Visual Basic runtime usually evaluates `Nothing` as an empty string ("").</span></span> <span data-ttu-id="c6425-107">Il .NET Framework non, tuttavia, genera un'eccezione ogni volta che viene eseguito un tentativo di eseguire un'operazione di stringa su `Nothing` .</span><span class="sxs-lookup"><span data-stu-id="c6425-107">The .NET Framework does not, however, and throws an exception whenever an attempt is made to perform a string operation on `Nothing`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c6425-108">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c6425-108">See also</span></span>

- [<span data-ttu-id="c6425-109">Introduzione alle stringhe in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="c6425-109">Introduction to Strings in Visual Basic</span></span>](introduction-to-strings.md)

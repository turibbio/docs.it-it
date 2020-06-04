---
title: Clausola Alias
ms.date: 07/20/2015
f1_keywords:
- vb.Alias
helpviewer_keywords:
- Alias keyword [Visual Basic]
ms.assetid: 58c06b11-465d-4d87-906a-73200a3d7f19
ms.openlocfilehash: c28e931a376b20b2058a7187551405cd9523d4fe
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408471"
---
# <a name="alias-clause-visual-basic"></a><span data-ttu-id="03763-102">Clausola Alias (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="03763-102">Alias Clause (Visual Basic)</span></span>
<span data-ttu-id="03763-103">Indica che una routine esterna ha un altro nome nella relativa DLL.</span><span class="sxs-lookup"><span data-stu-id="03763-103">Indicates that an external procedure has another name in its DLL.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="03763-104">Commenti</span><span class="sxs-lookup"><span data-stu-id="03763-104">Remarks</span></span>  
 <span data-ttu-id="03763-105">La `Alias` parola chiave può essere usata in questo contesto:</span><span class="sxs-lookup"><span data-stu-id="03763-105">The `Alias` keyword can be used in this context:</span></span>  
  
 [<span data-ttu-id="03763-106">Declare Statement</span><span class="sxs-lookup"><span data-stu-id="03763-106">Declare Statement</span></span>](declare-statement.md)  
  
 <span data-ttu-id="03763-107">Nell'esempio seguente `Alias` viene usata la parola chiave per specificare il nome della funzione in Advapi32. dll, `GetUserNameA` , che `getUserName` viene usata al posto di in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="03763-107">In the following example, the `Alias` keyword is used to provide the name of the function in advapi32.dll, `GetUserNameA`, that `getUserName` is used in place of in this example.</span></span> <span data-ttu-id="03763-108">`getUserName`La funzione viene chiamata in Sub `getUser` , che Visualizza il nome dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="03763-108">Function `getUserName` is called in sub `getUser`, which displays the name of the current user.</span></span>  
  
 [!code-vb[VbVbalrStatements#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#15)]  
  
## <a name="see-also"></a><span data-ttu-id="03763-109">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="03763-109">See also</span></span>

- [<span data-ttu-id="03763-110">Parole chiave</span><span class="sxs-lookup"><span data-stu-id="03763-110">Keywords</span></span>](../keywords/index.md)

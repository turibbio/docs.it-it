---
title: "'<membername>' è ambiguo nelle interfacce ereditate '<interfacename1>' e '<interfacename2>'"
ms.date: 07/20/2015
f1_keywords:
- vbc30685
- bc30685
helpviewer_keywords:
- BC30685
ms.assetid: 756add7a-23d5-4b4f-a48d-8297d6459c73
ms.openlocfilehash: f242db9e02a1983e731dce280be0e8f8a8b12712
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397272"
---
# <a name="membername-is-ambiguous-across-the-inherited-interfaces-interfacename1-and-interfacename2"></a><span data-ttu-id="2ac93-102">'\<membername>' è ambiguo nelle interfacce ereditate '\<interfacename1>' e '\<interfacename2>'</span><span class="sxs-lookup"><span data-stu-id="2ac93-102">'\<membername>' is ambiguous across the inherited interfaces '\<interfacename1>' and '\<interfacename2>'</span></span>
<span data-ttu-id="2ac93-103">L'interfaccia eredita due o più membri con lo stesso nome da più interfacce.</span><span class="sxs-lookup"><span data-stu-id="2ac93-103">The interface inherits two or more members with the same name from multiple interfaces.</span></span>  
  
 <span data-ttu-id="2ac93-104">**ID errore:** BC30685</span><span class="sxs-lookup"><span data-stu-id="2ac93-104">**Error ID:** BC30685</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="2ac93-105">Per correggere l'errore</span><span class="sxs-lookup"><span data-stu-id="2ac93-105">To correct this error</span></span>  
  
- <span data-ttu-id="2ac93-106">Eseguire il cast del valore all'interfaccia di base che si desidera utilizzare. Per esempio:</span><span class="sxs-lookup"><span data-stu-id="2ac93-106">Cast the value to the base interface that you want to use; for example:</span></span>  
  
    ```vb  
    Interface Left  
        Sub MySub()  
    End Interface  
  
    Interface Right  
        Sub MySub()  
    End Interface  
  
    Interface LeftRight  
        Inherits Left, Right  
    End Interface  
  
    Module test  
        Sub Main()  
            Dim x As LeftRight  
            ' x.MySub()  'x is ambiguous.  
            CType(x, Left).MySub() ' Cast to base type.  
            CType(x, Right).MySub() ' Call the other base type.  
        End Sub  
    End Module  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="2ac93-107">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2ac93-107">See also</span></span>

- [<span data-ttu-id="2ac93-108">Interfacce</span><span class="sxs-lookup"><span data-stu-id="2ac93-108">Interfaces</span></span>](../../programming-guide/language-features/interfaces/index.md)

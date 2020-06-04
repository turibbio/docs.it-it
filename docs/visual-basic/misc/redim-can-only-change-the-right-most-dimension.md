---
title: "'ReDim' può modificare solo la prima dimensione a destra"
ms.date: 07/20/2015
f1_keywords:
- vbrArray_TypeMismatch
ms.assetid: d53cf41b-7a7a-466c-a29a-920d99698fa9
ms.openlocfilehash: 8e42e0df7b97fb96f468ce37dd4cfc52fad8c596
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84358296"
---
# <a name="redim-can-only-change-the-right-most-dimension"></a><span data-ttu-id="69545-102">'ReDim' può modificare solo la prima dimensione a destra</span><span class="sxs-lookup"><span data-stu-id="69545-102">'ReDim' can only change the right-most dimension</span></span>
<span data-ttu-id="69545-103">Un'istruzione `ReDim` ha tentato di usare la parola chiave `Preserve` per modificare una dimensione di una matrice che non è l'ultima dimensione.</span><span class="sxs-lookup"><span data-stu-id="69545-103">A `ReDim` statement attempted to use the `Preserve` keyword to change a dimension of an array that is not the last dimension.</span></span> <span data-ttu-id="69545-104">Quando si usa `Preserve`, si può ridimensionare solo l'ultima dimensione di una matrice.</span><span class="sxs-lookup"><span data-stu-id="69545-104">When using `Preserve`, you can resize only the last dimension of an array.</span></span> <span data-ttu-id="69545-105">Per tutte le altre, è necessario specificare le stesse dimensioni di una matrice esistente.</span><span class="sxs-lookup"><span data-stu-id="69545-105">For all other dimensions, you must specify the same size as for the existing array.</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="69545-106">Per correggere l'errore</span><span class="sxs-lookup"><span data-stu-id="69545-106">To correct this error</span></span>  
  
- <span data-ttu-id="69545-107">Rimuovere la parola chiave `Preserve` .</span><span class="sxs-lookup"><span data-stu-id="69545-107">Remove the `Preserve` keyword.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="69545-108">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="69545-108">See also</span></span>

- [<span data-ttu-id="69545-109">Matrici in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="69545-109">Arrays in Visual Basic</span></span>](../programming-guide/language-features/arrays/index.md)
- [<span data-ttu-id="69545-110">Dimensioni della matrice in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="69545-110">Array dimensions in Visual Basic</span></span>](../programming-guide/language-features/arrays/array-dimensions.md)
- [<span data-ttu-id="69545-111">Istruzione ReDim</span><span class="sxs-lookup"><span data-stu-id="69545-111">ReDim Statement</span></span>](../language-reference/statements/redim-statement.md)
- [<span data-ttu-id="69545-112">Istruzione Dim</span><span class="sxs-lookup"><span data-stu-id="69545-112">Dim Statement</span></span>](../language-reference/statements/dim-statement.md)

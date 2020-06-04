---
title: "Procedura: fare riferimento all'istanza corrente di un oggetto"
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], object
- objects [Visual Basic], referring to current instance
- instances [Visual Basic], referring to current
- current instance
- object variables [Visual Basic]
ms.assetid: 7f9b2c77-03cd-428f-adc2-b18070226e7c
ms.openlocfilehash: 43bfd54592fb1d26cbf7f268b7e098e01e3745d8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410425"
---
# <a name="how-to-refer-to-the-current-instance-of-an-object-visual-basic"></a><span data-ttu-id="d1dfa-102">Procedura: fare riferimento all'istanza corrente di un oggetto (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d1dfa-102">How to: Refer to the Current Instance of an Object (Visual Basic)</span></span>
<span data-ttu-id="d1dfa-103">L' *istanza corrente* di un oggetto è l'istanza di in cui è attualmente in esecuzione il codice.</span><span class="sxs-lookup"><span data-stu-id="d1dfa-103">The *current instance* of an object is the instance in which the code is currently executing.</span></span>  
  
 <span data-ttu-id="d1dfa-104">Usare la `Me` parola chiave per fare riferimento all'istanza corrente.</span><span class="sxs-lookup"><span data-stu-id="d1dfa-104">You use the `Me` keyword to refer to the current instance.</span></span>  
  
### <a name="to-refer-to-the-current-instance"></a><span data-ttu-id="d1dfa-105">Per fare riferimento all'istanza corrente</span><span class="sxs-lookup"><span data-stu-id="d1dfa-105">To refer to the current instance</span></span>  
  
- <span data-ttu-id="d1dfa-106">Usare la `Me` parola chiave in cui in genere si usa il nome di una variabile oggetto.</span><span class="sxs-lookup"><span data-stu-id="d1dfa-106">Use the `Me` keyword where you would normally use the name of an object variable.</span></span>  
  
    ```vb  
    Me.ForeColor = System.Drawing.Color.Crimson  
    Me.Close()  
    ```  
  
     <span data-ttu-id="d1dfa-107">Anche se `Me` si comporta come una variabile oggetto, non è possibile dichiararla o assegnarvi alcun elemento.</span><span class="sxs-lookup"><span data-stu-id="d1dfa-107">Although `Me` behaves like an object variable, you cannot declare it or assign anything to it.</span></span> <span data-ttu-id="d1dfa-108">`Me`fa sempre riferimento all'istanza corrente.</span><span class="sxs-lookup"><span data-stu-id="d1dfa-108">`Me` always refers to the current instance.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d1dfa-109">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d1dfa-109">See also</span></span>

- [<span data-ttu-id="d1dfa-110">Variabili oggetto</span><span class="sxs-lookup"><span data-stu-id="d1dfa-110">Object Variables</span></span>](object-variables.md)
- [<span data-ttu-id="d1dfa-111">Assegnazione di variabili oggetto</span><span class="sxs-lookup"><span data-stu-id="d1dfa-111">Object Variable Assignment</span></span>](object-variable-assignment.md)
- [<span data-ttu-id="d1dfa-112">Me, My, MyBase e MyClass</span><span class="sxs-lookup"><span data-stu-id="d1dfa-112">Me, My, MyBase, and MyClass</span></span>](../../program-structure/me-my-mybase-and-myclass.md)

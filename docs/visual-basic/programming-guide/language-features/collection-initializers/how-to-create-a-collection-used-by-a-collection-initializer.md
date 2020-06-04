---
title: 'Procedura: creare una raccolta utilizzata da un inizializzatore di raccolta'
ms.date: 07/20/2015
helpviewer_keywords:
- collection initializers [Visual Basic]
ms.assetid: c858db10-424d-47e0-92cd-e08087cc5ebc
ms.openlocfilehash: 7cba290b92f41125a93d1ed022e4db5ef62da789
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414556"
---
# <a name="how-to-create-a-collection-used-by-a-collection-initializer-visual-basic"></a><span data-ttu-id="dc415-102">Procedura: creare una raccolta utilizzata da un inizializzatore di raccolta (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="dc415-102">How to: Create a Collection Used by a Collection Initializer (Visual Basic)</span></span>
<span data-ttu-id="dc415-103">Quando si usa un inizializzatore di raccolta per creare una raccolta, il compilatore Visual Basic cerca un `Add` metodo del tipo di raccolta per il quale i parametri per il `Add` Metodo corrispondono ai tipi dei valori nell'inizializzatore di raccolta.</span><span class="sxs-lookup"><span data-stu-id="dc415-103">When you use a collection initializer to create a collection, the Visual Basic compiler searches for an `Add` method of the collection type for which the parameters for the `Add` method match the types of the values in the collection initializer.</span></span> <span data-ttu-id="dc415-104">Questo `Add` metodo viene utilizzato per popolare la raccolta con i valori dell'inizializzatore di raccolta.</span><span class="sxs-lookup"><span data-stu-id="dc415-104">This `Add` method is used to populate the collection with the values from the collection initializer.</span></span>  
  
## <a name="example"></a><span data-ttu-id="dc415-105">Esempio</span><span class="sxs-lookup"><span data-stu-id="dc415-105">Example</span></span>  
 <span data-ttu-id="dc415-106">Nell'esempio seguente viene illustrata una `OrderCollection` raccolta che contiene un `Add` Metodo pubblico che può essere utilizzato da un inizializzatore di raccolta per aggiungere oggetti di tipo `Order` .</span><span class="sxs-lookup"><span data-stu-id="dc415-106">The following example shows an `OrderCollection` collection that contains a public `Add` method that a collection initializer can use to add objects of type `Order`.</span></span> <span data-ttu-id="dc415-107">Il `Add` metodo consente di usare la sintassi abbreviata dell'inizializzatore di raccolta.</span><span class="sxs-lookup"><span data-stu-id="dc415-107">The `Add` method enables you to use the shortened collection initializer syntax.</span></span>  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#4)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#1)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#2)]  
  
 [!code-vb[VbVbalrCollectionInitializersHowTo2#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializersHowTo2/VB/Module1.vb#3)]  
  
## <a name="see-also"></a><span data-ttu-id="dc415-108">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dc415-108">See also</span></span>

- [<span data-ttu-id="dc415-109">Inizializzatori di insieme</span><span class="sxs-lookup"><span data-stu-id="dc415-109">Collection Initializers</span></span>](index.md)
- [<span data-ttu-id="dc415-110">Procedura: creare un metodo di estensione Add utilizzato da un inizializzatore di raccolta</span><span class="sxs-lookup"><span data-stu-id="dc415-110">How to: Create an Add Extension Method Used by a Collection Initializer</span></span>](how-to-create-an-add-extension-method-used-by-a-collection-initializer.md)

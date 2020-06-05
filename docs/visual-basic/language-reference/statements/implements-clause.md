---
title: Clausola Implements
ms.date: 07/20/2015
f1_keywords:
- vb.ImplementsClause
helpviewer_keywords:
- interface implementation [Visual Basic], reimplementation
- interface members [Visual Basic], reimplementation
- interface members [Visual Basic], Implements keyword
- interface members
- members [Visual Basic], reimplementation
- interface implementation [Visual Basic], Implements keyword
- interface members [Visual Basic], implementing
- Implements keyword [Visual Basic]
- Implements statement [Visual Basic], about Implements
- members [Visual Basic], implementing
- members [Visual Basic], Implements keyword
- reimplementation
ms.assetid: 5252cdf9-964d-4fc6-af0f-0449b7126b5a
ms.openlocfilehash: 46ab1a1148e8d73d91293aedfc407e5efdc7cfb4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404563"
---
# <a name="implements-clause-visual-basic"></a><span data-ttu-id="6b89d-102">Clausola Implements (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="6b89d-102">Implements Clause (Visual Basic)</span></span>
<span data-ttu-id="6b89d-103">Indica che un membro di classe o di struttura fornisce l'implementazione per un membro definito in un'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="6b89d-103">Indicates that a class or structure member is providing the implementation for a member defined in an interface.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="6b89d-104">Commenti</span><span class="sxs-lookup"><span data-stu-id="6b89d-104">Remarks</span></span>  
<span data-ttu-id="6b89d-105">La `Implements` parola chiave non corrisponde all' [istruzione Implements](implements-statement.md).</span><span class="sxs-lookup"><span data-stu-id="6b89d-105">The `Implements` keyword is not the same as the [Implements Statement](implements-statement.md).</span></span> <span data-ttu-id="6b89d-106">Usare l' `Implements` istruzione per specificare che una classe o una struttura implementa una o più interfacce, quindi per ogni membro si usa la `Implements` parola chiave per specificare l'interfaccia e il membro che implementa.</span><span class="sxs-lookup"><span data-stu-id="6b89d-106">You use the `Implements` statement to specify that a class or structure implements one or more interfaces, and then for each member you use the `Implements` keyword to specify which interface and which member it implements.</span></span>

<span data-ttu-id="6b89d-107">Se una classe o una struttura implementa un'interfaccia, deve includere l' `Implements` istruzione immediatamente dopo l'istruzione di [classe](class-statement.md) o di [struttura](structure-statement.md)e deve implementare tutti i membri definiti dall'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="6b89d-107">If a class or structure implements an interface, it must include the `Implements` statement immediately after the [Class Statement](class-statement.md) or [Structure Statement](structure-statement.md), and it must implement all the members defined by the interface.</span></span>

## <a name="reimplementation"></a><span data-ttu-id="6b89d-108">Reimplementazione</span><span class="sxs-lookup"><span data-stu-id="6b89d-108">Reimplementation</span></span>  
<span data-ttu-id="6b89d-109">In una classe derivata, è possibile reimplementare un membro di interfaccia che la classe base ha già implementato.</span><span class="sxs-lookup"><span data-stu-id="6b89d-109">In a derived class, you can reimplement an interface member that the base class has already implemented.</span></span> <span data-ttu-id="6b89d-110">Questa operazione è diversa rispetto all'override del membro della classe base nei seguenti aspetti:</span><span class="sxs-lookup"><span data-stu-id="6b89d-110">This is different from overriding the base class member in the following respects:</span></span>

- <span data-ttu-id="6b89d-111">Non è necessario che il membro della classe base sia [sottoponibile a override](../modifiers/overridable.md) per essere reimplementato.</span><span class="sxs-lookup"><span data-stu-id="6b89d-111">The base class member does not need to be [Overridable](../modifiers/overridable.md) to be reimplemented.</span></span>
- <span data-ttu-id="6b89d-112">È possibile reimplementare il membro con un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="6b89d-112">You can reimplement the member with a different name.</span></span>

<span data-ttu-id="6b89d-113">La `Implements` parola chiave può essere utilizzata nei contesti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6b89d-113">The `Implements` keyword can be used in the following contexts:</span></span>

- [<span data-ttu-id="6b89d-114">Istruzione Event</span><span class="sxs-lookup"><span data-stu-id="6b89d-114">Event Statement</span></span>](event-statement.md)
- [<span data-ttu-id="6b89d-115">Istruzione Function</span><span class="sxs-lookup"><span data-stu-id="6b89d-115">Function Statement</span></span>](function-statement.md)
- [<span data-ttu-id="6b89d-116">Property Statement</span><span class="sxs-lookup"><span data-stu-id="6b89d-116">Property Statement</span></span>](property-statement.md)
- [<span data-ttu-id="6b89d-117">Istruzione Sub</span><span class="sxs-lookup"><span data-stu-id="6b89d-117">Sub Statement</span></span>](sub-statement.md)  
  
## <a name="see-also"></a><span data-ttu-id="6b89d-118">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="6b89d-118">See also</span></span>

- [<span data-ttu-id="6b89d-119">Istruzione Implements</span><span class="sxs-lookup"><span data-stu-id="6b89d-119">Implements Statement</span></span>](implements-statement.md)
- [<span data-ttu-id="6b89d-120">Istruzione Interface</span><span class="sxs-lookup"><span data-stu-id="6b89d-120">Interface Statement</span></span>](interface-statement.md)
- [<span data-ttu-id="6b89d-121">Istruzione Class</span><span class="sxs-lookup"><span data-stu-id="6b89d-121">Class Statement</span></span>](class-statement.md)
- [<span data-ttu-id="6b89d-122">Istruzione Structure</span><span class="sxs-lookup"><span data-stu-id="6b89d-122">Structure Statement</span></span>](structure-statement.md)

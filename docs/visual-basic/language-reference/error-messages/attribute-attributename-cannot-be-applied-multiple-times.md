---
title: Impossibile applicare più volte l'attributo '<attributename>'
ms.date: 07/20/2015
f1_keywords:
- bc30663
- vbc30663
helpviewer_keywords:
- BC30663
ms.assetid: 3760e7ff-7238-40a1-8676-77d858a64fc0
ms.openlocfilehash: 14145f165adf5ccd20298a70ca5596488b488b0c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409959"
---
# <a name="attribute-attributename-cannot-be-applied-multiple-times"></a><span data-ttu-id="26f6a-102">Impossibile applicare più volte l'attributo '\<attributename>'</span><span class="sxs-lookup"><span data-stu-id="26f6a-102">Attribute '\<attributename>' cannot be applied multiple times</span></span>

<span data-ttu-id="26f6a-103">L'attributo può essere applicato una sola volta.</span><span class="sxs-lookup"><span data-stu-id="26f6a-103">The attribute can only be applied once.</span></span> <span data-ttu-id="26f6a-104">L' `AttributeUsage` attributo determina se un attributo può essere applicato più di una volta.</span><span class="sxs-lookup"><span data-stu-id="26f6a-104">The `AttributeUsage` attribute determines whether an attribute can be applied more than once.</span></span>  
  
 <span data-ttu-id="26f6a-105">**ID errore:** BC30663</span><span class="sxs-lookup"><span data-stu-id="26f6a-105">**Error ID:** BC30663</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="26f6a-106">Per correggere l'errore</span><span class="sxs-lookup"><span data-stu-id="26f6a-106">To correct this error</span></span>  
  
1. <span data-ttu-id="26f6a-107">Verificare che l'attributo venga applicato una sola volta.</span><span class="sxs-lookup"><span data-stu-id="26f6a-107">Make sure the attribute is only applied once.</span></span>  
  
2. <span data-ttu-id="26f6a-108">Se si usano attributi personalizzati sviluppati, provare a modificare l' `AttributeUsage` attributo per consentire l'utilizzo di più attributi, come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="26f6a-108">If you are using custom attributes you developed, consider changing their `AttributeUsage` attribute to allow multiple attribute usage, as with the following example.</span></span>  
  
```vb  
<AttributeUsage(AllowMultiple := True)>  
```  
  
## <a name="see-also"></a><span data-ttu-id="26f6a-109">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="26f6a-109">See also</span></span>

- <xref:System.AttributeUsageAttribute>
- [<span data-ttu-id="26f6a-110">Creazione di attributi personalizzati</span><span class="sxs-lookup"><span data-stu-id="26f6a-110">Creating Custom Attributes</span></span>](../../programming-guide/concepts/attributes/creating-custom-attributes.md)
- [<span data-ttu-id="26f6a-111">AttributeUsage</span><span class="sxs-lookup"><span data-stu-id="26f6a-111">AttributeUsage</span></span>](../../programming-guide/concepts/attributes/attributeusage.md)

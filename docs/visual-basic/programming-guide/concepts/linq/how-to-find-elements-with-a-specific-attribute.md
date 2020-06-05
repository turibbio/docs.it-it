---
title: 'Procedura: Trovare elementi con un attributo specifico (XPath-LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: 4bb38d2c-bc7c-4196-8909-aaf41fb86b28
ms.openlocfilehash: 4b625fcccc834f860072ad92587bbfd7ed5ec4ad
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364773"
---
# <a name="how-to-find-elements-with-a-specific-attribute-xpath-linq-to-xml-visual-basic"></a><span data-ttu-id="ce822-102">Procedura: trovare elementi con un attributo specifico (XPath-LINQ to XML) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="ce822-102">How to: Find Elements with a Specific Attribute (XPath-LINQ to XML) (Visual Basic)</span></span>
<span data-ttu-id="ce822-103">Talvolta si desidera individuare tutti gli elementi con un attributo specifico.</span><span class="sxs-lookup"><span data-stu-id="ce822-103">Sometimes you want to find all elements that have a specific attribute.</span></span> <span data-ttu-id="ce822-104">Il contenuto dell'attributo non è rilevante</span><span class="sxs-lookup"><span data-stu-id="ce822-104">You are not concerned about the contents of the attribute.</span></span> <span data-ttu-id="ce822-105">perché si desidera solo individuare gli elementi in cui tale attributo è presente.</span><span class="sxs-lookup"><span data-stu-id="ce822-105">Instead, you want to select based on the existence of the attribute.</span></span>  
  
 <span data-ttu-id="ce822-106">L'espressione XPath è:</span><span class="sxs-lookup"><span data-stu-id="ce822-106">The XPath expression is:</span></span>  
  
 `./*[@Select]`  
  
## <a name="example"></a><span data-ttu-id="ce822-107">Esempio</span><span class="sxs-lookup"><span data-stu-id="ce822-107">Example</span></span>  
 <span data-ttu-id="ce822-108">Nel codice seguente vengono selezionati solo gli elementi con attributo `Select`.</span><span class="sxs-lookup"><span data-stu-id="ce822-108">The following code selects just the elements that have the `Select` attribute.</span></span>  
  
```vb  
Dim doc As XElement = _
    <Root>  
        <Child1>1</Child1>  
        <Child2 Select='true'>2</Child2>  
        <Child3>3</Child3>  
        <Child4 Select='true'>4</Child4>  
        <Child5>5</Child5>  
    </Root>  
  
' LINQ to XML query  
Dim list1 As IEnumerable(Of XElement) = _  
    From el In doc.Elements() _  
    Where el.@Select <> Nothing _  
    Select el  
  
' XPath expression  
Dim list2 As IEnumerable(Of XElement) = DirectCast(doc.XPathEvaluate _  
    ("./*[@Select]"), IEnumerable).Cast(Of XElement)()  
  
If list1.Count() = list2.Count() And _  
    list1.Intersect(list2).Count() = list1.Count() Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
  
For Each el As XElement In list1  
    Console.WriteLine(el)  
Next  
```  
  
 <span data-ttu-id="ce822-109">Nell'esempio viene prodotto l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="ce822-109">This example produces the following output:</span></span>  
  
```console
Results are identical  
<Child2 Select="true">2</Child2>  
<Child4 Select="true">4</Child4>  
```  
  
## <a name="see-also"></a><span data-ttu-id="ce822-110">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ce822-110">See also</span></span>

- [<span data-ttu-id="ce822-111">LINQ to XML per gli utenti di XPath (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="ce822-111">LINQ to XML for XPath Users (Visual Basic)</span></span>](linq-to-xml-for-xpath-users.md)

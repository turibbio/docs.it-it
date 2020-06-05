---
title: 'Procedura: Filtrare in base a un attributo (XPath-LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: ffefb9d6-45ec-4677-a396-dd9c2b36298f
ms.openlocfilehash: 5bc0a621f0d3bb8e22701440383cdac54c7be51b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84394505"
---
# <a name="how-to-filter-on-an-attribute-xpath-linq-to-xml-visual-basic"></a><span data-ttu-id="b7211-102">Procedura: filtrare in un attributo (XPath-LINQ to XML) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b7211-102">How to: Filter on an Attribute (XPath-LINQ to XML) (Visual Basic)</span></span>
<span data-ttu-id="b7211-103">In questo argomento viene illustrato come ottenere gli elementi discendente con un nome specificato e con un attributo con un valore specificato.</span><span class="sxs-lookup"><span data-stu-id="b7211-103">This topic shows how to get the descendant elements with a specified name, and with an attribute with a specified value.</span></span>  
  
 <span data-ttu-id="b7211-104">L'espressione XPath è:</span><span class="sxs-lookup"><span data-stu-id="b7211-104">The XPath expression is:</span></span>  
  
 `.//Address[@Type='Shipping']`  
  
## <a name="example"></a><span data-ttu-id="b7211-105">Esempio</span><span class="sxs-lookup"><span data-stu-id="b7211-105">Example</span></span>  
 <span data-ttu-id="b7211-106">In questo esempio vengono individuati tutti gli elementi discendente il cui nome è `Address` e in cui il valore dell'attributo `Type` è "Shipping".</span><span class="sxs-lookup"><span data-stu-id="b7211-106">This example finds all descendants elements with the name of `Address`, and with a `Type` attribute with a value of "Shipping".</span></span>  
  
 <span data-ttu-id="b7211-107">Questo esempio usa il documento XML seguente: [File XML di esempio: più ordini di acquisto (LINQ to XML)](sample-xml-file-multiple-purchase-orders-linq-to-xml.md).</span><span class="sxs-lookup"><span data-stu-id="b7211-107">This example uses the following XML document: [Sample XML File: Multiple Purchase Orders (LINQ to XML)](sample-xml-file-multiple-purchase-orders-linq-to-xml.md).</span></span>  
  
```vb  
Dim po As XDocument = XDocument.Load("PurchaseOrders.xml")  
  
' LINQ to XML query  
Dim list1 As IEnumerable(Of XElement) = _  
    From el In po...<Address> _  
    Where el.@Type = "Shipping" _  
    Select el  
  
' XPath expression  
Dim list2 As IEnumerable(Of XElement) = _  
    po.XPathSelectElements(".//Address[@Type='Shipping']")  
  
If (list1.Count = list2.Count And _  
        list1.Intersect(list2).Count() = list1.Count()) Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
For Each el As XElement In list1  
    Console.WriteLine(el)  
Next  
```  
  
 <span data-ttu-id="b7211-108">Nell'esempio viene prodotto l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="b7211-108">This example produces the following output:</span></span>  
  
```console
Results are identical  
<Address Type="Shipping">  
  <Name>Ellen Adams</Name>  
  <Street>123 Maple Street</Street>  
  <City>Mill Valley</City>  
  <State>CA</State>  
  <Zip>10999</Zip>  
  <Country>USA</Country>  
</Address>  
<Address Type="Shipping">  
  <Name>Cristian Osorio</Name>  
  <Street>456 Main Street</Street>  
  <City>Buffalo</City>  
  <State>NY</State>  
  <Zip>98112</Zip>  
  <Country>USA</Country>  
</Address>  
<Address Type="Shipping">  
  <Name>Jessica Arnold</Name>  
  <Street>4055 Madison Ave</Street>  
  <City>Seattle</City>  
  <State>WA</State>  
  <Zip>98112</Zip>  
  <Country>USA</Country>  
</Address>  
```  
  
## <a name="see-also"></a><span data-ttu-id="b7211-109">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b7211-109">See also</span></span>

- [<span data-ttu-id="b7211-110">LINQ to XML per gli utenti di XPath (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b7211-110">LINQ to XML for XPath Users (Visual Basic)</span></span>](linq-to-xml-for-xpath-users.md)

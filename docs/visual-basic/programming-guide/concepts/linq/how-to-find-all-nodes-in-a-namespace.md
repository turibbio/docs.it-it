---
title: 'Procedura: Trovare tutti i nodi in uno spazio dei nomi'
ms.date: 07/20/2015
ms.assetid: b735d7da-5727-48a3-ab57-a16378adc32e
ms.openlocfilehash: f1660020db59b63dea86ed8953faef743c0f40d4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405313"
---
# <a name="how-to-find-all-nodes-in-a-namespace-visual-basic"></a><span data-ttu-id="9bb04-102">Procedura: trovare tutti i nodi in uno spazio dei nomi (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9bb04-102">How to: Find All Nodes in a Namespace (Visual Basic)</span></span>
<span data-ttu-id="9bb04-103">È possibile applicare un filtro sullo spazio dei nomi di ogni elemento o attributo per trovare tutti i nodi inclusi in questo determinato spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="9bb04-103">You can filter on the namespace of each element or attribute to find all nodes in that particular namespace.</span></span>  
  
## <a name="example"></a><span data-ttu-id="9bb04-104">Esempio</span><span class="sxs-lookup"><span data-stu-id="9bb04-104">Example</span></span>  
 <span data-ttu-id="9bb04-105">Nell'esempio seguente viene creato un albero XML con due spazi dei nomi.</span><span class="sxs-lookup"><span data-stu-id="9bb04-105">The following example creates an XML tree with two namespaces.</span></span> <span data-ttu-id="9bb04-106">L'albero viene quindi scorso e vengono stampati i nomi di tutti gli elementi e gli attributi inclusi in uno dei tali spazi dei nomi.</span><span class="sxs-lookup"><span data-stu-id="9bb04-106">It then iterates through the tree and prints the names of all the elements and attributes in one of those namespaces.</span></span>  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
Imports <xmlns:fc="www.fourthcoffee.com">  
  
Module Module1  
    Sub Main()  
        Dim xmlTree As XElement = _  
            <aw:Root>  
                <fc:Child1>abc</fc:Child1>  
                <fc:Child2>def</fc:Child2>  
                <aw:Child3>ghi</aw:Child3>  
                <fc:Child4>  
                    <fc:GrandChild1>jkl</fc:GrandChild1>  
                    <aw:GrandChild2>mno</aw:GrandChild2>  
                </fc:Child4>  
            </aw:Root>  
        Console.WriteLine("Nodes in the http://www.adventure-works.com namespace")  
        Dim awElements As IEnumerable(Of XElement) = _  
            From el In xmlTree.Descendants() _  
            Where (el.Name.Namespace = GetXmlNamespace(aw)) _  
            Select el  
        For Each el As XElement In awElements  
            Console.WriteLine(el.Name.ToString())  
        Next  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="9bb04-107">L'output del codice è il seguente:</span><span class="sxs-lookup"><span data-stu-id="9bb04-107">This code produces the following output:</span></span>  
  
```console  
Nodes in the http://www.adventure-works.com namespace  
{http://www.adventure-works.com}Child3  
{http://www.adventure-works.com}GrandChild2  
```  
  
## <a name="example"></a><span data-ttu-id="9bb04-108">Esempio</span><span class="sxs-lookup"><span data-stu-id="9bb04-108">Example</span></span>  
 <span data-ttu-id="9bb04-109">Il file XML cui accede la seguente query contiene gli ordini di acquisto in due spazi dei nomi diversi.</span><span class="sxs-lookup"><span data-stu-id="9bb04-109">The XML file accessed by the following query contains purchase orders in two different namespaces.</span></span> <span data-ttu-id="9bb04-110">Con la query viene creato un nuovo albero contenente solo gli elementi di uno degli spazi dei nomi.</span><span class="sxs-lookup"><span data-stu-id="9bb04-110">The query creates a new tree with just the elements in one of the namespaces.</span></span>  
  
 <span data-ttu-id="9bb04-111">Questo esempio usa il documento XML seguente: [File XML di esempio: ordini di acquisto consolidati](sample-xml-file-consolidated-purchase-orders.md).</span><span class="sxs-lookup"><span data-stu-id="9bb04-111">This example uses the following XML document: [Sample XML File: Consolidated Purchase Orders](sample-xml-file-consolidated-purchase-orders.md).</span></span>  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim cpo As XDocument = XDocument.Load("ConsolidatedPurchaseOrders.xml")  
        Dim newTree As XElement = _  
            <Root>  
                <%= From el In cpo.Root.Elements() _  
                    Where el.Name.Namespace = GetXmlNamespace(aw) _  
                    Select el %>  
            </Root>  
        Console.WriteLine(newTree)  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="9bb04-112">L'output del codice è il seguente:</span><span class="sxs-lookup"><span data-stu-id="9bb04-112">This code produces the following output:</span></span>  
  
```xml  
<Root>  
  <aw:PurchaseOrder PONumber="11223" Date="2000-01-15" xmlns:aw="http://www.adventure-works.com">  
    <aw:ShippingAddress>  
      <aw:Name>Chris Preston</aw:Name>  
      <aw:Street>123 Main St.</aw:Street>  
      <aw:City>Seattle</aw:City>  
      <aw:State>WA</aw:State>  
      <aw:Zip>98113</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:ShippingAddress>  
    <aw:BillingAddress>  
      <aw:Name>Chris Preston</aw:Name>  
      <aw:Street>123 Main St.</aw:Street>  
      <aw:City>Seattle</aw:City>  
      <aw:State>WA</aw:State>  
      <aw:Zip>98113</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:BillingAddress>  
    <aw:DeliveryInstructions>Ship only complete order.</aw:DeliveryInstructions>  
    <aw:Item PartNum="LIT-01">  
      <aw:ProductID>Litware Networking Card</aw:ProductID>  
      <aw:Qty>1</aw:Qty>  
      <aw:Price>20.99</aw:Price>  
    </aw:Item>  
    <aw:Item PartNum="LIT-25">  
      <aw:ProductID>Litware 17in LCD Monitor</aw:ProductID>  
      <aw:Qty>1</aw:Qty>  
      <aw:Price>199.99</aw:Price>  
    </aw:Item>  
  </aw:PurchaseOrder>  
</Root>  
```  
  
## <a name="see-also"></a><span data-ttu-id="9bb04-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9bb04-113">See also</span></span>

- [<span data-ttu-id="9bb04-114">Query di base (LINQ to XML) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9bb04-114">Basic Queries (LINQ to XML) (Visual Basic)</span></span>](basic-queries-linq-to-xml.md)

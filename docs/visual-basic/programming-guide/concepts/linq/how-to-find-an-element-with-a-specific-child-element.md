---
title: 'Procedura: Trovare un elemento con un elemento figlio specifico'
ms.date: 07/20/2015
ms.assetid: b0d0a463-6a85-46c3-8453-ad25b0ecf93c
ms.openlocfilehash: a05504070fe3d2ea5eb6135fd3bf697b131686c6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405287"
---
# <a name="how-to-find-an-element-with-a-specific-child-element-visual-basic"></a><span data-ttu-id="27ab5-102">Procedura: trovare un elemento con un elemento figlio specifico (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="27ab5-102">How to: Find an Element with a Specific Child Element (Visual Basic)</span></span>
<span data-ttu-id="27ab5-103">In questo argomento viene illustrato come trovare un determinato elemento che include un elemento figlio con un valore specifico.</span><span class="sxs-lookup"><span data-stu-id="27ab5-103">This topic shows how to find a particular element that has a child element with a specific value.</span></span>  
  
## <a name="example"></a><span data-ttu-id="27ab5-104">Esempio</span><span class="sxs-lookup"><span data-stu-id="27ab5-104">Example</span></span>  
 <span data-ttu-id="27ab5-105">Nell'esempio viene ricercato l'elemento `Test` contenente un elemento figlio `CommandLine` con valore "Examp2.EXE".</span><span class="sxs-lookup"><span data-stu-id="27ab5-105">The example finds the `Test` element that has a `CommandLine` child element with the value of "Examp2.EXE".</span></span>  
  
 <span data-ttu-id="27ab5-106">Questo esempio usa il documento XML seguente: [File XML di esempio: configurazione di test (LINQ to XML)](sample-xml-file-test-configuration-linq-to-xml.md).</span><span class="sxs-lookup"><span data-stu-id="27ab5-106">This example uses the following XML document: [Sample XML File: Test Configuration (LINQ to XML)](sample-xml-file-test-configuration-linq-to-xml.md).</span></span>  
  
```vb  
Dim root As XElement = XElement.Load("TestConfig.xml")  
Dim tests As IEnumerable(Of XElement) = _  
    From el In root.<Test> _  
    Where el.<CommandLine>.Value = "Examp2.EXE" _  
    Select el  
For Each el as XElement In tests  
    Console.WriteLine(el.@TestId)  
Next  
```  
  
 <span data-ttu-id="27ab5-107">L'output del codice è il seguente:</span><span class="sxs-lookup"><span data-stu-id="27ab5-107">This code produces the following output:</span></span>  
  
```console  
0002  
0006  
```  
  
 <span data-ttu-id="27ab5-108">Si noti che in questo esempio vengono utilizzate la proprietà [Axis Child XML](../../../language-reference/xml-axis/xml-child-axis-property.md), la [Proprietà Axis attribute XML](../../../language-reference/xml-axis/xml-attribute-axis-property.md)e la [proprietà Value XML](../../../language-reference/xml-axis/xml-value-property.md).</span><span class="sxs-lookup"><span data-stu-id="27ab5-108">Note that this example uses the [XML Child axis property](../../../language-reference/xml-axis/xml-child-axis-property.md), the [XML Attribute axis property](../../../language-reference/xml-axis/xml-attribute-axis-property.md), and the [XML Value property](../../../language-reference/xml-axis/xml-value-property.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="27ab5-109">Esempio</span><span class="sxs-lookup"><span data-stu-id="27ab5-109">Example</span></span>  
 <span data-ttu-id="27ab5-110">Nell'esempio seguente è illustrata la stessa query per XML in uno spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="27ab5-110">The following example shows the same query for XML that is in a namespace.</span></span> <span data-ttu-id="27ab5-111">Per ulteriori informazioni, vedere [Cenni preliminari sugli spazi dei nomi (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md).</span><span class="sxs-lookup"><span data-stu-id="27ab5-111">For more information, see [Namespaces Overview (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md).</span></span>  
  
 <span data-ttu-id="27ab5-112">Questo esempio usa il documento XML seguente: [File XML di esempio: configurazione di test in uno spazio dei nomi](sample-xml-file-test-configuration-in-a-namespace.md).</span><span class="sxs-lookup"><span data-stu-id="27ab5-112">This example uses the following XML document: [Sample XML File: Test Configuration in a Namespace](sample-xml-file-test-configuration-in-a-namespace.md).</span></span>  
  
```vb  
Imports <xmlns='http://www.adatum.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = XElement.Load("TestConfigInNamespace.xml")  
        Dim tests As IEnumerable(Of XElement) = _  
            From el In root.<Test> _  
            Where el.<CommandLine>.Value = "Examp2.EXE" _  
            Select el  
        For Each el As XElement In tests  
            Console.WriteLine(el.@TestId)  
        Next  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="27ab5-113">L'output del codice è il seguente:</span><span class="sxs-lookup"><span data-stu-id="27ab5-113">This code produces the following output:</span></span>  
  
```console  
0002  
0006  
```  
  
## <a name="see-also"></a><span data-ttu-id="27ab5-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="27ab5-114">See also</span></span>

- <xref:System.Xml.Linq.XElement.Attribute%2A>
- <xref:System.Xml.Linq.XContainer.Elements%2A>
- [<span data-ttu-id="27ab5-115">Query di base (LINQ to XML) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="27ab5-115">Basic Queries (LINQ to XML) (Visual Basic)</span></span>](basic-queries-linq-to-xml.md)
- [<span data-ttu-id="27ab5-116">Panoramica degli operatori query standard (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="27ab5-116">Standard Query Operators Overview (Visual Basic)</span></span>](standard-query-operators-overview.md)
- [<span data-ttu-id="27ab5-117">Operazioni di proiezione (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="27ab5-117">Projection Operations (Visual Basic)</span></span>](projection-operations.md)

---
title: Recupero di nodi ordinati in base all'indice
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 5412c90f-2703-4aa8-a9c4-1b8a35183c37
ms.openlocfilehash: 8ff02a81ab579cc0041074990a76166fcafe6eb5
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288719"
---
# <a name="ordered-node-retrieval-by-index"></a><span data-ttu-id="daea3-102">Recupero di nodi ordinati in base all'indice</span><span class="sxs-lookup"><span data-stu-id="daea3-102">Ordered Node Retrieval by Index</span></span>
<span data-ttu-id="daea3-103">Il DOM (Document Object Model) XML W3C (World Wide Web Consortium) descrive anche un oggetto NodeList, che ha la capacità di gestire un elenco ordinato di nodi, mentre i set non ordinati sono gestiti da **XmlNamedNodeMap**.</span><span class="sxs-lookup"><span data-stu-id="daea3-103">The World Wide Web Consortium (W3C) XML Document Object Model (DOM) also describes a NodeList, which has the ability to handle an ordered list of nodes, as opposed to the unordered set handled by the **XmlNamedNodeMap**.</span></span> <span data-ttu-id="daea3-104">L'oggetto NodeList in Microsoft .NET Framework è denominato **XmlNodeList**.</span><span class="sxs-lookup"><span data-stu-id="daea3-104">The NodeList in the Microsoft .NET Framework is called **XmlNodeList**.</span></span> <span data-ttu-id="daea3-105">I metodi e le proprietà che restituiscono un oggetto **XmlNodeList** sono:</span><span class="sxs-lookup"><span data-stu-id="daea3-105">Methods and properties that return an **XmlNodeList** are:</span></span>  
  
- <span data-ttu-id="daea3-106">XmlNode.ChildNodes</span><span class="sxs-lookup"><span data-stu-id="daea3-106">XmlNode.ChildNodes</span></span>  
  
- <span data-ttu-id="daea3-107">XmlDocument.GetElementsByTagName</span><span class="sxs-lookup"><span data-stu-id="daea3-107">XmlDocument.GetElementsByTagName</span></span>  
  
- <span data-ttu-id="daea3-108">XmlElement.GetElementsByTagName</span><span class="sxs-lookup"><span data-stu-id="daea3-108">XmlElement.GetElementsByTagName</span></span>  
  
- <span data-ttu-id="daea3-109">XmlNode.SelectNodes</span><span class="sxs-lookup"><span data-stu-id="daea3-109">XmlNode.SelectNodes</span></span>  
  
 <span data-ttu-id="daea3-110">Per l'oggetto **XmlNodeList** è disponibile una proprietà **Count** che può essere usata per scrivere cicli di iterazione per scorrere i nodi in **XmlNodeList**, come mostrato nell'esempio di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="daea3-110">The **XmlNodeList** has a **Count** property that can be used to write loops to iterate over the nodes in the **XmlNodeList**, as shown in the following code sample:</span></span>  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
   doc.Load("books.xml")  
  
    ' Retrieve all book titles.  
    Dim root as XmlElement = doc.DocumentElement  
    Dim elemList as XmlNodeList = root.GetElementsByTagName("title")  
    Dim i as integer  
    for i=0  to elemList.Count-1  
        ' Display all book titles in the Node List.  
        Console.WriteLine(elemList.ItemOf(i).InnerXml)  
    next  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.Load("books.xml");  
// Retrieve all book titles.  
XmlElement root = doc.DocumentElement;  
XmlNodeList elemList = root.GetElementsByTagName("title");  
for (int i=0; i < elemList.Count; i++)  
{
   // Display all book titles in the Node List.  
   Console.WriteLine(elemList[i].InnerXml);  
}
```  
  
 <span data-ttu-id="daea3-111">Oltre alla proprietà **Count**, è disponibile un metodo **GetEnumerator** che consente di eseguire un'iterazione in stile `foreach` sulla raccolta di nodi in **XmlNodeList**.</span><span class="sxs-lookup"><span data-stu-id="daea3-111">In addition to the **Count** property, there is a **GetEnumerator** method that provides a, `foreach` style iteration over the collection of nodes in the **XmlNodeList**.</span></span> <span data-ttu-id="daea3-112">Nell'esempio di codice seguente viene illustrato l'uso dell'istruzione `foreach`:</span><span class="sxs-lookup"><span data-stu-id="daea3-112">The following code example shows the use of the `foreach` statement.</span></span>  
  
```vb  
Dim doc As New XmlDocument()  
doc.Load("books.xml")  
  
' Get book titles.  
Dim root As XmlElement = doc.DocumentElement  
Dim elemList As XmlNodeList = root.GetElementsByTagName("title")  
Dim ienum As IEnumerator = elemList.GetEnumerator()  
' Loop over the XmlNodeList using the enumerator ienum
While ienum.MoveNext()  
    ' Display the book title.  
    Dim title As XmlNode = CType(ienum.Current, XmlNode)  
    Console.WriteLine(title.InnerText)  
End While  
```  
  
```csharp  
{  
     XmlDocument doc = new XmlDocument();  
     doc.Load("books.xml");  
  
     // Get book titles.  
     XmlElement root = doc.DocumentElement;  
     XmlNodeList elemList = root.GetElementsByTagName("title");  
     IEnumerator ienum = elemList.GetEnumerator();
     // Loop over the XmlNodeList using the enumerator ienum
     while (ienum.MoveNext())  
     {  
          // Display the book title.  
           XmlNode title = (XmlNode) ienum.Current;  
           Console.WriteLine(title.InnerText);  
     }  
  }  
```  
  
 <span data-ttu-id="daea3-113">Per altre informazioni sui metodi e sulle proprietà disponibili per **XmlNodeList**, vedere <xref:System.Xml.XmlNodeList>.</span><span class="sxs-lookup"><span data-stu-id="daea3-113">For more information on the methods and properties available on the **XmlNodeList**, see <xref:System.Xml.XmlNodeList>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="daea3-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="daea3-114">See also</span></span>

- [<span data-ttu-id="daea3-115">XML DOM (Document Object Model)</span><span class="sxs-lookup"><span data-stu-id="daea3-115">XML Document Object Model (DOM)</span></span>](xml-document-object-model-dom.md)

---
title: Programmazione con nodi
ms.date: 07/20/2015
ms.assetid: d8422a9b-dd37-44a3-8aac-2237ed9561e0
ms.openlocfilehash: 9c64c348f5d26172f26593b927e6bc24baf365bf
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82794403"
---
# <a name="programming-with-nodes-visual-basic"></a>Programmazione con nodi (Visual Basic)
Gli sviluppatori di [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] che hanno la necessità di scrivere programmi come un editor XML, un sistema di trasformazioni o un writer di rapporti, spesso devono scrivere programmi che funzionano a un livello di granularità maggiore rispetto a elementi e attributi. Devono spesso operare a livello di nodo, modificando i nodi di testo, elaborando istruzioni e commenti. In questo argomento vengono forniti dettagli sulla programmazione a livello di nodo.  
  
## <a name="node-details"></a>Dettagli sui nodi  
 I programmatori che operano a livello di nodo devono conoscere diversi dettagli di programmazione.  
  
### <a name="parent-property-of-children-nodes-of-xdocument-is-set-to-null"></a>La proprietà padre dei nodi figlio di XDocument è impostata su Null  
 La proprietà <xref:System.Xml.Linq.XObject.Parent%2A> contiene l'elemento padre <xref:System.Xml.Linq.XElement>, non il nodo padre. I nodi figlio di <xref:System.Xml.Linq.XDocument> non hanno un elemento <xref:System.Xml.Linq.XElement> padre. L'elemento padre è il documento, pertanto la proprietà <xref:System.Xml.Linq.XObject.Parent%2A> per tali nodi è impostata su Null.  
  
 Questo concetto è illustrato nell'esempio seguente:  
  
```vb  
Dim doc As XDocument = XDocument.Parse("<!-- a comment --><Root/>")  
Console.WriteLine(doc.Nodes().OfType(Of XComment).First().Parent Is Nothing)  
Console.WriteLine(doc.Root.Parent Is Nothing)  
```  
  
 Nell'esempio viene prodotto l'output seguente:  
  
```console  
True  
True  
```  
  
### <a name="adjacent-text-nodes-are-possible"></a>I nodi di testo adiacenti sono possibili  
 In diversi modelli di programmazione XML i nodi di testo adiacenti vengono sempre uniti. Questa operazione è denominata normalizzazione dei nodi di testo. In [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] i nodi di testo non vengono normalizzati. Se si aggiungono due nodi di testo allo stesso elemento, si otterranno nodi di testo adiacenti. Se, tuttavia, si aggiunge contenuto specificato come stringa anziché come nodo <xref:System.Xml.Linq.XText>, è possibile che in [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] la stringa venga unita con un nodo di testo adiacente.  
  
 Questo concetto è illustrato nell'esempio seguente:  
  
```vb  
Dim xmlTree As XElement = <Root>Content</Root>  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
  
' This does not add a new text node.  
xmlTree.Add("new content")  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
  
'// This does add a new, adjacent text node.  
xmlTree.Add(New XText("more text"))  
Console.WriteLine(xmlTree.Nodes().OfType(Of XText)().Count())  
```  
  
 Nell'esempio viene prodotto l'output seguente:  
  
```console  
1  
1  
2  
```  
  
### <a name="empty-text-nodes-are-possible"></a>I nodi di testo vuoti sono possibili  
 In alcuni modelli di programmazione di XML è garantito che i nodi di testo non contengono la stringa vuota. Il concetto di base è che un nodo di testo di questo tipo non ha impatto sulla serializzazione dell'XML. Tuttavia, per lo stesso motivo per cui i nodi di testo sono possibili, la rimozione di testo da un nodo di testo impostandone il valore sulla stringa vuota non comporta l'eliminazione del nodo di testo stesso.  
  
```vb  
Dim xmlTree As XElement = <Root>Content</Root>  
Dim textNode As XText = xmlTree.Nodes().OfType(Of XText)().First()  
  
' The following line does not cause the removal of the text node.  
textNode.Value = ""  
  
Dim textNode2 As XText = xmlTree.Nodes().OfType(Of XText)().First()  
Console.WriteLine(">>{0}<<", textNode2)  
```  
  
 Nell'esempio viene prodotto l'output seguente:  
  
```console  
>><<  
```  
  
### <a name="an-empty-text-node-impacts-serialization"></a>Un nodo di testo vuoto ha effetto sulla serializzazione  
 Se un elemento contiene solo un nodo di testo figlio vuoto, verrà serializzato con la sintassi lunga dei tag: `<Child></Child>`. Se un elemento non contiene alcun tipo di nodo figlio, verrà serializzato con la sintassi breve dei tag: `<Child />`.  
  
```vb  
Dim child1 As XElement = New XElement("Child1", _  
    New XText("") _  
)  
Dim child2 As XElement = New XElement("Child2")  
Console.WriteLine(child1)  
Console.WriteLine(child2)  
```  
  
 Nell'esempio viene prodotto l'output seguente:  
  
```xml  
<Child1></Child1>  
<Child2 />  
```  
  
### <a name="namespaces-are-attributes-in-the-linq-to-xml-tree"></a>Gli spazi dei nomi sono attributi nell'albero LINQ to XML  
 Anche se la sintassi delle dichiarazioni di spazi dei nomi è identica a quella degli attributi, in alcune interfacce di programmazione, ad esempio XSLT e XPath, le dichiarazioni di spazi dei nomi non sono considerati attributi. Tuttavia, in [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] gli spazi dei nomi vengono archiviati come oggetti <xref:System.Xml.Linq.XAttribute> nell'albero XML. Se si scorrono gli attributi per un elemento che contiene una dichiarazione di spazio dei nomi, le dichiarazioni di spazi dei nomi verranno visualizzate come uno degli elementi nella raccolta restituita.  
  
 La proprietà <xref:System.Xml.Linq.XAttribute.IsNamespaceDeclaration%2A> indica se un attributo è una dichiarazione di spazio dei nomi.  
  
```vb  
Dim root As XElement = _
<Root  
    xmlns='http://www.adventure-works.com'  
    xmlns:fc='www.fourthcoffee.com'  
    AnAttribute='abc'/>  
For Each att As XAttribute In root.Attributes()  
    Console.WriteLine("{0}  IsNamespaceDeclaration:{1}", att, _  
                      att.IsNamespaceDeclaration)  
Next  
```  
  
 Nell'esempio viene prodotto l'output seguente:  
  
```console  
xmlns="http://www.adventure-works.com"  IsNamespaceDeclaration:True  
xmlns:fc="www.fourthcoffee.com"  IsNamespaceDeclaration:True  
AnAttribute="abc"  IsNamespaceDeclaration:False  
```  
  
### <a name="xpath-axis-methods-do-not-return-child-white-space-of-xdocument"></a>I metodi dell'asse di XPath non restituiscono lo spazio vuoto figlio di XDocument  
 In [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] è possibile usare nodi di testo figlio di un oggetto <xref:System.Xml.Linq.XDocument>, purché i nodi di testo contengano solo spazio vuoto. Tuttavia, il modello a oggetti di XPath non include lo spazio vuoto come nodi figlio di un documento, pertanto quando si scorrono gli elementi figlio di <xref:System.Xml.Linq.XDocument> usando l'asse <xref:System.Xml.Linq.XContainer.Nodes%2A>, verranno restituiti nodi di testo di tipo spazio vuoto. Tuttavia, quando si scorrono gli elementi figlio di <xref:System.Xml.Linq.XDocument> usando i metodi dell'asse di XPath, i nodi di testo di tipo spazio vuoto non verranno restituiti.  
  
```vb  
' Create a document with some white space child nodes of the document.  
Dim root As XDocument = XDocument.Parse( _  
"<?xml version='1.0' encoding='utf-8' standalone='yes'?>" & _  
vbNewLine & "<Root/>" & vbNewLine & "<!--a comment-->" & vbNewLine, _  
LoadOptions.PreserveWhitespace)  
  
' Count the white space child nodes using LINQ to XML.  
Console.WriteLine(root.Nodes().OfType(Of XText)().Count())  
  
' Count the white space child nodes using XPathEvaluate.  
Dim nodes As IEnumerable = CType(root.XPathEvaluate("text()"), IEnumerable)  
Console.WriteLine(nodes.OfType(Of XText)().Count())  
```  
  
 Nell'esempio viene prodotto l'output seguente:  
  
```console  
3  
0  
```  
  
### <a name="xdeclaration-objects-are-not-nodes"></a>Gli oggetti XDeclaration non sono nodi  
 Quando si scorrono i nodi figlio di <xref:System.Xml.Linq.XDocument>, l'oggetto dichiarazione XML non verrà visualizzato. Si tratta di una proprietà, non di un nodo figlio del documento.  
  
```vb  
Dim doc As XDocument = _  
<?xml version='1.0' encoding='utf-8' standalone='yes'?>  
<Root/>  
  
doc.Save("Temp.xml")  
Console.WriteLine(File.ReadAllText("Temp.xml"))  
  
' This shows that there is only one child node of the document.  
Console.WriteLine(doc.Nodes().Count())  
```  
  
 Nell'esempio viene prodotto l'output seguente:  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<Root />
1
```  
  
## <a name="see-also"></a>Vedere anche

- [Programmazione LINQ to XML avanzata (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)

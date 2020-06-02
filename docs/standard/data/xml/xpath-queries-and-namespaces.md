---
title: Query e spazi dei nomi XPath
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: ef6402be-2f8e-4be2-8d3e-a80891cdef8b
ms.openlocfilehash: d3314a7ff4cf957dac4cd8ad0416aad434b19af2
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84283195"
---
# <a name="xpath-queries-and-namespaces"></a>Query e spazi dei nomi XPath
Le query XPath tengono in considerazione gli spazi dei nomi in un documento XML e possono usare i prefissi degli spazi dei nomi per qualificare i nomi di elemento e di attributo. La qualifica dei nomi di elemento e di attributo con un prefisso dello spazio dei nomi limita i nodi restituiti da una query XPath ai soli nodi che appartengono a uno spazio dei nomi specifico.  
  
 Se ad esempio il mapping del prefisso `books` è lo spazio dei nomi `http://www.contoso.com/books`, la query XPath `/books:books/books:book` seguente selezionerà solo quegli elementi `book` nello spazio dei nomi `http://www.contoso.com/books`.  
  
## <a name="the-xmlnamespacemanager"></a>XmlNamespaceManager  
 Per usare gli spazi dei nomi in una query XPath, un oggetto derivato dall'interfaccia <xref:System.Xml.IXmlNamespaceResolver> come la classe <xref:System.Xml.XmlNamespaceManager> viene costruito con l'URI e il prefisso dello spazio dei nomi da includere nella query XPath.  
  
 L'oggetto <xref:System.Xml.XmlNamespaceManager> può essere usato nella query in ciascuno dei seguenti modi.  
  
- L'oggetto <xref:System.Xml.XmlNamespaceManager> viene associato a un oggetto <xref:System.Xml.XPath.XPathExpression> esistente mediante il metodo <xref:System.Xml.XPath.XPathExpression.SetContext%2A> dell'oggetto <xref:System.Xml.XPath.XPathExpression>. È anche possibile compilare un nuovo oggetto <xref:System.Xml.XPath.XPathExpression> usando il metodo statico <xref:System.Xml.XPath.XPathExpression.Compile%2A>, che accetta una stringa che rappresenta l'espressione XPath e un oggetto <xref:System.Xml.XmlNamespaceManager> come parametri e restituisce un nuovo oggetto <xref:System.Xml.XPath.XPathExpression>.  
  
- Lo stesso oggetto <xref:System.Xml.XmlNamespaceManager> viene passato come parametro a un metodo della classe <xref:System.Xml.XPath.XPathNavigator> che lo accetti assieme a una stringa che rappresenta l'espressione XPath.  
  
 Di seguito sono indicati i metodi della classe <xref:System.Xml.XPath.XPathNavigator> che accettano come parametro un oggetto derivato dall'interfaccia <xref:System.Xml.IXmlNamespaceResolver>.  
  
- <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.Select%2A>  
  
- <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A>  
  
### <a name="the-default-namespace"></a>Spazio dei nomi predefinito  
 Nel seguente documento XML lo spazio dei nomi predefinito con un prefisso vuoto viene usato per dichiarare lo spazio dei nomi `http://www.contoso.com/books`.  
  
```xml  
<books xmlns="http://www.contoso.com/books">  
    <book>  
        <title>Title</title>  
        <author>Author Name</author>  
        <price>5.50</price>  
    </book>  
</books>  
```  
  
 XPath considera il prefisso vuoto come lo spazio dei nomi `null`. In altre parole, nelle query XPath possono essere usati solo i prefissi il cui mapping corrisponde a uno spazio dei nomi. Ciò significa che, se si desidera eseguire una query relativa a uno spazio dei nomi in un documento XML, anche se si tratta dello spazio dei nomi predefinito, è necessario definire un prefisso per tale spazio dei nomi.  
  
 Ad esempio, se non si definisce un prefisso per il documento XML indicato sopra, la query XPath `/books/book` non restituirà alcun risultato.  
  
 È necessario che sia associato un prefisso, per impedire ambiguità durante le operazioni di query su documenti con alcuni nodi che non rientrano in uno spazio dei nomi e alcuni nodi che rientrano in uno spazio dei nomi predefinito.  
  
 Il codice seguente definisce un prefisso per lo spazio dei nomi predefinito e seleziona tutti gli elementi `book` dallo spazio dei nomi `http://www.contoso.com/books`.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
Dim query As XPathExpression = navigator.Compile("/books:books/books:book")  
Dim manager As XmlNamespaceManager = New XmlNamespaceManager(navigator.NameTable)  
manager.AddNamespace("books", "http://www.contoso.com/books")  
query.SetContext(manager)  
Dim nodes As XPathNodeIterator = navigator.Select(query)  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
XPathExpression query = navigator.Compile("/books:books/books:book");  
XmlNamespaceManager manager = new XmlNamespaceManager(navigator.NameTable);  
manager.AddNamespace("books", "http://www.contoso.com/books");  
query.SetContext(manager);  
XPathNodeIterator nodes = navigator.Select(query);  
```  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [Elaborazione di dati XML con il modello di dati XPath](process-xml-data-using-the-xpath-data-model.md)
- [Selezione di dati XML con XPathNavigator](select-xml-data-using-xpathnavigator.md)
- [Valutazione di espressioni XPath con XPathNavigator](evaluate-xpath-expressions-using-xpathnavigator.md)
- [Corrispondenza di nodi utilizzando XPathNavigator](matching-nodes-using-xpathnavigator.md)
- [Tipi di nodo riconosciuti con le query XPath](node-types-recognized-with-xpath-queries.md)
- [Espressioni XPath compilate](compiled-xpath-expressions.md)

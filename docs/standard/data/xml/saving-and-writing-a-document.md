---
title: Salvataggio e scrittura di un documento
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 097b0cb1-5743-4c3a-86ef-caf5cbe6750d
ms.openlocfilehash: 0af160b720b9eddd9e72689c920316bffdc6d21e
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/07/2020
ms.locfileid: "75710219"
---
# <a name="saving-and-writing-a-document"></a>Salvataggio e scrittura di un documento
Quando si carica e si salva un <xref:System.Xml.XmlDocument>, il documento salvato potrebbe essere diverso dall'originale nei seguenti modi:  
  
- Se la proprietà <xref:System.Xml.XmlDocument.PreserveWhitespace%2A> è impostata su `true` prima della chiamata al metodo <xref:System.Xml.XmlDocument.Save%2A>, gli spazi vuoti nel documento verranno mantenuti nell'output. Se invece la proprietà è `false`, <xref:System.Xml.XmlDocument> produrrà il rientro automatico dell'output.  
  
- Tutti gli spazi vuoti tra gli attributi vengono ridotti a un singolo carattere di spazio.  
  
- Lo spazio vuoto tra gli elementi viene modificato. I caratteri spazio vuoto significativi vengono mantenuti, a differenza di quelli non significativi. Tuttavia, quando il documento viene salvato, per impostazione predefinita utilizzerà la modalità  **Rientri** del tipo <xref:System.Xml.XmlTextWriter> per stampare accuratamente l'output in modo che sia più leggibile.  
  
- Il carattere virgoletta usato intorno ai valori degli attributi viene modificato in virgolette doppie per impostazione predefinita. È possibile usare la proprietà <xref:System.Xml.XmlTextReader.QuoteChar%2A> su <xref:System.Xml.XmlTextWriter> per impostare il carattere virgoletta su virgolette doppie o virgoletta singola.  
  
- Per impostazione predefinita, le entità di caratteri numerici come `{` vengono espanse.  
  
- Il contrassegno dell'ordine dei byte trovato nel documento di input non viene mantenuto. Il formato UCS-2 viene salvato nel formato UTF-8, a meno che non si crei esplicitamente una dichiarazione XML che specifichi una codifica diversa.  
  
- Se si vuole riportare un <xref:System.Xml.XmlDocument> in un file o in un flusso, l'output riportato sarà uguale al contenuto del documento, il che significa che l'oggetto <xref:System.Xml.XmlDeclaration> viene riportato solo se è contenuto nel documento e la codifica usata per riportare il documento è uguale alla codifica specificata nel nodo di dichiarazione.  
  
## <a name="writing-an-xmldeclaration"></a>Scrittura di una XmlDeclaration  
 I membri <xref:System.Xml.XmlDocument> e <xref:System.Xml.XmlDeclaration> delle proprietà <xref:System.Xml.XmlNode.OuterXml%2A>, <xref:System.Xml.XmlNode.InnerXml%2A> e <xref:System.Xml.XmlNode.WriteTo%2A>, oltre ai metodi <xref:System.Xml.XmlDocument> di <xref:System.Xml.XmlDocument.Save%2A> e <xref:System.Xml.XmlDocument.WriteContentTo%2A>, consentono di creare una dichiarazione XML.  
  
 Per le proprietà <xref:System.Xml.XmlDocument> e <xref:System.Xml.XmlNode.OuterXml%2A> di <xref:System.Xml.XmlDocument.InnerXml%2A> e i metodi <xref:System.Xml.XmlDocument.Save%2A>, <xref:System.Xml.XmlDocument.WriteTo%2A> e <xref:System.Xml.XmlDocument.WriteContentTo%2A>, la codifica riportata nella dichiarazione XML deriva dal nodo <xref:System.Xml.XmlDeclaration>. Se non è presente <xref:System.Xml.XmlDeclaration> alcun nodo <xref:System.Xml.XmlDeclaration> , non viene scritto. Se non è presente alcuna codifica nel <xref:System.Xml.XmlDeclaration> nodo, la codifica non viene scritta nella dichiarazione XML.  
  
 I metodi <xref:System.Xml.XmlDocument.Save%2A?displayProperty=nameWithType> e <xref:System.Xml.XmlDocument.Save%2A?displayProperty=nameWithType> riportano sempre una <xref:System.Xml.XmlDeclaration>. Questi metodi prendono la codifica dal writer sul quale stanno scrivendo. Vale a dire che il valore di codifica nel writer sostituisce la codifica nel documento e nell'oggetto <xref:System.Xml.XmlDeclaration>. Il codice seguente, ad esempio, non scrive una codifica nella dichiarazione XML trovata nel file di output `out.xml`.  
  
```vb  
Dim doc As New XmlDocument()  
Dim tw As XmlTextWriter = New XmlTextWriter("out.xml", Nothing)  
doc.Load("text.xml")  
doc.Save(tw)  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
XmlTextWriter tw = new XmlTextWriter("out.xml", null);  
doc.Load("text.xml");  
doc.Save(tw);  
```  
  
 Per il metodo <xref:System.Xml.XmlDocument.Save%2A> la dichiarazione XML viene riportata usando il metodo <xref:System.Xml.XmlWriter.WriteStartDocument%2A> nella classe <xref:System.Xml.XmlWriter>. Per questo motivo, sovrascrivendo il metodo <xref:System.Xml.XmlWriter.WriteStartDocument%2A> si modifica il modo in cui viene scritto l'inizio del documento.  
  
 Per i <xref:System.Xml.XmlDeclaration> membri di <xref:System.Xml.XmlNode.OuterXml%2A>, <xref:System.Xml.XmlDeclaration.WriteTo%2A>e <xref:System.Xml.XmlNode.InnerXml%2A>, se la <xref:System.Xml.XmlDeclaration.Encoding%2A> proprietà non è impostata, non viene scritta alcuna codifica. In caso contrario, la codifica scritta nella dichiarazione XML corrisponde alla codifica trovata nella <xref:System.Xml.XmlDeclaration.Encoding%2A> proprietà.  
  
## <a name="writing-document-content-using-the-outerxml-property"></a>Scrittura del contenuto del documento tramite la proprietà OuterXml  
 La proprietà <xref:System.Xml.XmlNode.OuterXml%2A> è un'estensione Microsoft degli standard del modello DOM (Document Object Model) XML del World Wide Web Consortium (W3C). ‎La proprietà <xref:System.Xml.XmlNode.OuterXml%2A> viene usata per ottenere il markup dell'intero documento XML o solo il markup di un singolo nodo e dei relativi nodi figlio. <xref:System.Xml.XmlNode.OuterXml%2A> restituisce il markup che rappresenta il nodo specificato e tutti i relativi nodi figlio.  
  
 Nell'esempio di codice seguente viene illustrato il salvataggio di un intero documento come stringa.  
  
```vb  
Dim mydoc As New XmlDocument()  
' Perform application needs here, like mydoc.Load("myfile");  
' Now save the entire document to a string variable called "xml".  
Dim xml As String = mydoc.OuterXml  
```  
  
```csharp  
XmlDocument mydoc = new XmlDocument();  
// Perform application needs here, like mydoc.Load("myfile");  
// Now save the entire document to a string variable called "xml".  
string xml = mydoc.OuterXml;  
```  
  
 Nell'esempio di codice seguente viene illustrato il salvataggio del solo elemento del documento.  
  
```vb  
' For the content of the Document Element only.  
Dim xml As String = mydoc.DocumentElement.OuterXml  
```  
  
```csharp  
// For the content of the Document Element only.  
string xml = mydoc.DocumentElement.OuterXml;  
```  
  
 Al contrario, se si desidera il contenuto dei nodi figlio, è possibile usare la proprietà <xref:System.Xml.XmlNode.InnerText%2A>.  
  
## <a name="see-also"></a>Vedi anche

- [XML DOM (Document Object Model)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)

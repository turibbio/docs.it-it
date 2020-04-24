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
# <a name="saving-and-writing-a-document"></a><span data-ttu-id="1c7fa-102">Salvataggio e scrittura di un documento</span><span class="sxs-lookup"><span data-stu-id="1c7fa-102">Saving and Writing a Document</span></span>
<span data-ttu-id="1c7fa-103">Quando si carica e si salva un <xref:System.Xml.XmlDocument>, il documento salvato potrebbe essere diverso dall'originale nei seguenti modi:</span><span class="sxs-lookup"><span data-stu-id="1c7fa-103">When you load and save an <xref:System.Xml.XmlDocument>, the saved document may differ from the original in the following ways:</span></span>  
  
- <span data-ttu-id="1c7fa-104">Se la proprietà <xref:System.Xml.XmlDocument.PreserveWhitespace%2A> è impostata su `true` prima della chiamata al metodo <xref:System.Xml.XmlDocument.Save%2A>, gli spazi vuoti nel documento verranno mantenuti nell'output. Se invece la proprietà è `false`, <xref:System.Xml.XmlDocument> produrrà il rientro automatico dell'output.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-104">If the <xref:System.Xml.XmlDocument.PreserveWhitespace%2A> property is set to `true` before the <xref:System.Xml.XmlDocument.Save%2A> method is called, white space in the document is preserved in the output; if this property is `false`, <xref:System.Xml.XmlDocument> auto-indents the output.</span></span>  
  
- <span data-ttu-id="1c7fa-105">Tutti gli spazi vuoti tra gli attributi vengono ridotti a un singolo carattere di spazio.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-105">All the white space between attributes is reduced to a single space character.</span></span>  
  
- <span data-ttu-id="1c7fa-106">Lo spazio vuoto tra gli elementi viene modificato.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-106">The white space between elements is changed.</span></span> <span data-ttu-id="1c7fa-107">I caratteri spazio vuoto significativi vengono mantenuti, a differenza di quelli non significativi.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-107">Significant white space is preserved and insignificant white space is not.</span></span> <span data-ttu-id="1c7fa-108">Tuttavia, quando il documento viene salvato, per impostazione predefinita utilizzerà la modalità  **Rientri** del tipo <xref:System.Xml.XmlTextWriter> per stampare accuratamente l'output in modo che sia più leggibile.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-108">But when the document is saved, it will use the <xref:System.Xml.XmlTextWriter> **Indenting** mode by default to neatly print the output to make it more readable.</span></span>  
  
- <span data-ttu-id="1c7fa-109">Il carattere virgoletta usato intorno ai valori degli attributi viene modificato in virgolette doppie per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-109">The quote character used around attribute values is changed to double quote by default.</span></span> <span data-ttu-id="1c7fa-110">È possibile usare la proprietà <xref:System.Xml.XmlTextReader.QuoteChar%2A> su <xref:System.Xml.XmlTextWriter> per impostare il carattere virgoletta su virgolette doppie o virgoletta singola.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-110">You can use the <xref:System.Xml.XmlTextReader.QuoteChar%2A> property on <xref:System.Xml.XmlTextWriter> to set the quote character to either double quote or single quote.</span></span>  
  
- <span data-ttu-id="1c7fa-111">Per impostazione predefinita, le entità di caratteri numerici come `{` vengono espanse.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-111">By default, numeric character entities like `{` are expanded.</span></span>  
  
- <span data-ttu-id="1c7fa-112">Il contrassegno dell'ordine dei byte trovato nel documento di input non viene mantenuto.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-112">The byte-order mark found in the input document is not preserved.</span></span> <span data-ttu-id="1c7fa-113">Il formato UCS-2 viene salvato nel formato UTF-8, a meno che non si crei esplicitamente una dichiarazione XML che specifichi una codifica diversa.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-113">UCS-2 is saved as UTF-8 unless you explicitly create an XML declaration that specifies a different encoding.</span></span>  
  
- <span data-ttu-id="1c7fa-114">Se si vuole riportare un <xref:System.Xml.XmlDocument> in un file o in un flusso, l'output riportato sarà uguale al contenuto del documento,</span><span class="sxs-lookup"><span data-stu-id="1c7fa-114">If you want to write out the <xref:System.Xml.XmlDocument> into a file or stream, the output written out is the same as the content of the document.</span></span> <span data-ttu-id="1c7fa-115">il che significa che l'oggetto <xref:System.Xml.XmlDeclaration> viene riportato solo se è contenuto nel documento e la codifica usata per riportare il documento è uguale alla codifica specificata nel nodo di dichiarazione.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-115">That is, the <xref:System.Xml.XmlDeclaration> is written out only if there is one contained in the document, and the encoding used when writing out the document is the same encoding given in the declaration node.</span></span>  
  
## <a name="writing-an-xmldeclaration"></a><span data-ttu-id="1c7fa-116">Scrittura di una XmlDeclaration</span><span class="sxs-lookup"><span data-stu-id="1c7fa-116">Writing an XmlDeclaration</span></span>  
 <span data-ttu-id="1c7fa-117">I membri <xref:System.Xml.XmlDocument> e <xref:System.Xml.XmlDeclaration> delle proprietà <xref:System.Xml.XmlNode.OuterXml%2A>, <xref:System.Xml.XmlNode.InnerXml%2A> e <xref:System.Xml.XmlNode.WriteTo%2A>, oltre ai metodi <xref:System.Xml.XmlDocument> di <xref:System.Xml.XmlDocument.Save%2A> e <xref:System.Xml.XmlDocument.WriteContentTo%2A>, consentono di creare una dichiarazione XML.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-117">The <xref:System.Xml.XmlDocument> and <xref:System.Xml.XmlDeclaration> members of <xref:System.Xml.XmlNode.OuterXml%2A>, <xref:System.Xml.XmlNode.InnerXml%2A>, and <xref:System.Xml.XmlNode.WriteTo%2A>, in addition to the <xref:System.Xml.XmlDocument> methods of <xref:System.Xml.XmlDocument.Save%2A> and <xref:System.Xml.XmlDocument.WriteContentTo%2A>, create an XML declaration.</span></span>  
  
 <span data-ttu-id="1c7fa-118">Per le proprietà <xref:System.Xml.XmlDocument> e <xref:System.Xml.XmlNode.OuterXml%2A> di <xref:System.Xml.XmlDocument.InnerXml%2A> e i metodi <xref:System.Xml.XmlDocument.Save%2A>, <xref:System.Xml.XmlDocument.WriteTo%2A> e <xref:System.Xml.XmlDocument.WriteContentTo%2A>, la codifica riportata nella dichiarazione XML deriva dal nodo <xref:System.Xml.XmlDeclaration>.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-118">For the <xref:System.Xml.XmlDocument> properties of <xref:System.Xml.XmlNode.OuterXml%2A>, <xref:System.Xml.XmlDocument.InnerXml%2A>, and the <xref:System.Xml.XmlDocument.Save%2A>, <xref:System.Xml.XmlDocument.WriteTo%2A>, and <xref:System.Xml.XmlDocument.WriteContentTo%2A> methods, the encoding written out in the XML declaration is taken from the <xref:System.Xml.XmlDeclaration> node.</span></span> <span data-ttu-id="1c7fa-119">Se non è presente <xref:System.Xml.XmlDeclaration> alcun nodo <xref:System.Xml.XmlDeclaration> , non viene scritto. Se non è presente alcuna codifica nel <xref:System.Xml.XmlDeclaration> nodo, la codifica non viene scritta nella dichiarazione XML.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-119">If there is no <xref:System.Xml.XmlDeclaration> node, <xref:System.Xml.XmlDeclaration> is not written out. If there is no encoding in the <xref:System.Xml.XmlDeclaration> node, encoding is not written out in the XML declaration.</span></span>  
  
 <span data-ttu-id="1c7fa-120">I metodi <xref:System.Xml.XmlDocument.Save%2A?displayProperty=nameWithType> e <xref:System.Xml.XmlDocument.Save%2A?displayProperty=nameWithType> riportano sempre una <xref:System.Xml.XmlDeclaration>.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-120">The <xref:System.Xml.XmlDocument.Save%2A?displayProperty=nameWithType> and <xref:System.Xml.XmlDocument.Save%2A?displayProperty=nameWithType> methods always write out an <xref:System.Xml.XmlDeclaration>.</span></span> <span data-ttu-id="1c7fa-121">Questi metodi prendono la codifica dal writer sul quale stanno scrivendo.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-121">These methods take the encoding from the writer that it is writing to.</span></span> <span data-ttu-id="1c7fa-122">Vale a dire che il valore di codifica nel writer sostituisce la codifica nel documento e nell'oggetto <xref:System.Xml.XmlDeclaration>.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-122">That is, the encoding value on the writer overrides the encoding on the document and in the <xref:System.Xml.XmlDeclaration>.</span></span> <span data-ttu-id="1c7fa-123">Il codice seguente, ad esempio, non scrive una codifica nella dichiarazione XML trovata nel file di output `out.xml`.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-123">For example, the following code does not write an encoding in the XML declaration found in the output file `out.xml`.</span></span>  
  
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
  
 <span data-ttu-id="1c7fa-124">Per il metodo <xref:System.Xml.XmlDocument.Save%2A> la dichiarazione XML viene riportata usando il metodo <xref:System.Xml.XmlWriter.WriteStartDocument%2A> nella classe <xref:System.Xml.XmlWriter>.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-124">For the <xref:System.Xml.XmlDocument.Save%2A> method, the XML declaration is written out using the <xref:System.Xml.XmlWriter.WriteStartDocument%2A> method in the <xref:System.Xml.XmlWriter> class.</span></span> <span data-ttu-id="1c7fa-125">Per questo motivo, sovrascrivendo il metodo <xref:System.Xml.XmlWriter.WriteStartDocument%2A> si modifica il modo in cui viene scritto l'inizio del documento.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-125">Therefore, overwriting the <xref:System.Xml.XmlWriter.WriteStartDocument%2A> method changes how the start of the document is written.</span></span>  
  
 <span data-ttu-id="1c7fa-126">Per i <xref:System.Xml.XmlDeclaration> membri di <xref:System.Xml.XmlNode.OuterXml%2A>, <xref:System.Xml.XmlDeclaration.WriteTo%2A>e <xref:System.Xml.XmlNode.InnerXml%2A>, se la <xref:System.Xml.XmlDeclaration.Encoding%2A> proprietà non è impostata, non viene scritta alcuna codifica. In caso contrario, la codifica scritta nella dichiarazione XML corrisponde alla codifica trovata nella <xref:System.Xml.XmlDeclaration.Encoding%2A> proprietà.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-126">For the <xref:System.Xml.XmlDeclaration> members of <xref:System.Xml.XmlNode.OuterXml%2A>, <xref:System.Xml.XmlDeclaration.WriteTo%2A>, and <xref:System.Xml.XmlNode.InnerXml%2A>, if the <xref:System.Xml.XmlDeclaration.Encoding%2A> property is not set, no encoding is written out. Otherwise, the encoding written out in the XML declaration is the same as the encoding found in the <xref:System.Xml.XmlDeclaration.Encoding%2A> property.</span></span>  
  
## <a name="writing-document-content-using-the-outerxml-property"></a><span data-ttu-id="1c7fa-127">Scrittura del contenuto del documento tramite la proprietà OuterXml</span><span class="sxs-lookup"><span data-stu-id="1c7fa-127">Writing Document Content Using the OuterXml Property</span></span>  
 <span data-ttu-id="1c7fa-128">La proprietà <xref:System.Xml.XmlNode.OuterXml%2A> è un'estensione Microsoft degli standard del modello DOM (Document Object Model) XML del World Wide Web Consortium (W3C).</span><span class="sxs-lookup"><span data-stu-id="1c7fa-128">The <xref:System.Xml.XmlNode.OuterXml%2A> property is a Microsoft extension to the World Wide Web Consortium (W3C) XML Document Object Model (DOM) standards.</span></span> <span data-ttu-id="1c7fa-129">‎La proprietà <xref:System.Xml.XmlNode.OuterXml%2A> viene usata per ottenere il markup dell'intero documento XML o solo il markup di un singolo nodo e dei relativi nodi figlio.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-129">The <xref:System.Xml.XmlNode.OuterXml%2A> property is used to get the markup of the whole XML document, or just the markup of a single node and its child nodes.</span></span> <span data-ttu-id="1c7fa-130"><xref:System.Xml.XmlNode.OuterXml%2A> restituisce il markup che rappresenta il nodo specificato e tutti i relativi nodi figlio.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-130"><xref:System.Xml.XmlNode.OuterXml%2A> returns the markup representing the given node and all its child nodes.</span></span>  
  
 <span data-ttu-id="1c7fa-131">Nell'esempio di codice seguente viene illustrato il salvataggio di un intero documento come stringa.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-131">The following code sample shows how to save a document in its entirety as a string.</span></span>  
  
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
  
 <span data-ttu-id="1c7fa-132">Nell'esempio di codice seguente viene illustrato il salvataggio del solo elemento del documento.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-132">The following code sample shows how to save only the document element.</span></span>  
  
```vb  
' For the content of the Document Element only.  
Dim xml As String = mydoc.DocumentElement.OuterXml  
```  
  
```csharp  
// For the content of the Document Element only.  
string xml = mydoc.DocumentElement.OuterXml;  
```  
  
 <span data-ttu-id="1c7fa-133">Al contrario, se si desidera il contenuto dei nodi figlio, è possibile usare la proprietà <xref:System.Xml.XmlNode.InnerText%2A>.</span><span class="sxs-lookup"><span data-stu-id="1c7fa-133">In contrast, you can use the <xref:System.Xml.XmlNode.InnerText%2A> property if you want the content of child nodes.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1c7fa-134">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="1c7fa-134">See also</span></span>

- [<span data-ttu-id="1c7fa-135">XML DOM (Document Object Model)</span><span class="sxs-lookup"><span data-stu-id="1c7fa-135">XML Document Object Model (DOM)</span></span>](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)

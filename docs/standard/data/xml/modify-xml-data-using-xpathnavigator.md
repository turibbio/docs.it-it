---
title: Modifica dei dati XML con XPathNavigator
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 03a7c5a1-b296-4af4-b209-043c958dc0a5
ms.openlocfilehash: 3b64bc8666274798ebaefc87ef3883fcec1ef6b1
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288836"
---
# <a name="modify-xml-data-using-xpathnavigator"></a><span data-ttu-id="42a77-102">Modifica dei dati XML con XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="42a77-102">Modify XML Data using XPathNavigator</span></span>
<span data-ttu-id="42a77-103">La classe <xref:System.Xml.XPath.XPathNavigator> fornisce un set di metodi usati per modificare nodi e valori in un documento XML.</span><span class="sxs-lookup"><span data-stu-id="42a77-103">The <xref:System.Xml.XPath.XPathNavigator> class provides a set of methods used to modify nodes and values in an XML document.</span></span> <span data-ttu-id="42a77-104">Per usare questi metodi, è necessario che l'oggetto <xref:System.Xml.XPath.XPathNavigator> sia modificabile, ovvero, la relativa proprietà <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> deve essere `true`.</span><span class="sxs-lookup"><span data-stu-id="42a77-104">In order to use these methods, the <xref:System.Xml.XPath.XPathNavigator> object must be editable, that is, its <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> property must be `true`.</span></span>  
  
 <span data-ttu-id="42a77-105">Gli oggetti <xref:System.Xml.XPath.XPathNavigator> che possono modificare un documento XML vengono creati dal metodo <xref:System.Xml.XmlDocument.CreateNavigator%2A> della classe <xref:System.Xml.XmlDocument>.</span><span class="sxs-lookup"><span data-stu-id="42a77-105"><xref:System.Xml.XPath.XPathNavigator> objects that can edit an XML document are created by the <xref:System.Xml.XmlDocument.CreateNavigator%2A> method of the <xref:System.Xml.XmlDocument> class.</span></span> <span data-ttu-id="42a77-106">Gli oggetti <xref:System.Xml.XPath.XPathNavigator> creati dalla classe <xref:System.Xml.XPath.XPathDocument> sono di sola lettura e qualsiasi tentativo di usare i metodi di modifica di un oggetto <xref:System.Xml.XPath.XPathNavigator> creato da un oggetto <xref:System.Xml.XPath.XPathDocument> genererà un oggetto <xref:System.NotSupportedException>.</span><span class="sxs-lookup"><span data-stu-id="42a77-106"><xref:System.Xml.XPath.XPathNavigator> objects created by the <xref:System.Xml.XPath.XPathDocument> class are read-only and any attempt to use the editing methods of an <xref:System.Xml.XPath.XPathNavigator> object created by an <xref:System.Xml.XPath.XPathDocument> object result in a <xref:System.NotSupportedException>.</span></span>  
  
 <span data-ttu-id="42a77-107">Per altre informazioni sulla creazioni di oggetti <xref:System.Xml.XPath.XPathNavigator> modificabili, vedere [Lettura di dati XML con XPathDocument e XmlDocument](reading-xml-data-using-xpathdocument-and-xmldocument.md).</span><span class="sxs-lookup"><span data-stu-id="42a77-107">For more information about creating editable <xref:System.Xml.XPath.XPathNavigator> objects, see [Reading XML Data using XPathDocument and XmlDocument](reading-xml-data-using-xpathdocument-and-xmldocument.md).</span></span>  
  
## <a name="modifying-nodes"></a><span data-ttu-id="42a77-108">Modifica dei nodi</span><span class="sxs-lookup"><span data-stu-id="42a77-108">Modifying Nodes</span></span>  
 <span data-ttu-id="42a77-109">Una tecnica semplice per modificare il valore di un nodo è quella di usare i metodi <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> e <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.</span><span class="sxs-lookup"><span data-stu-id="42a77-109">A simple technique for changing the value of a node is to use the <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> and <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> methods of the <xref:System.Xml.XPath.XPathNavigator> class.</span></span>  
  
 <span data-ttu-id="42a77-110">Nella tabella seguente sono elencati gli effetti di tali metodi sui diversi tipi di nodo.</span><span class="sxs-lookup"><span data-stu-id="42a77-110">The following table lists the effects of these methods on different node types.</span></span>  
  
|<xref:System.Xml.XPath.XPathNodeType>|<span data-ttu-id="42a77-111">Dati modificati</span><span class="sxs-lookup"><span data-stu-id="42a77-111">Data Changed</span></span>|  
|---------------------------------------------------------------------------------------------------------------------------------------------|------------------|  
|<xref:System.Xml.XPath.XPathNodeType.Root>|<span data-ttu-id="42a77-112">Non supportato.</span><span class="sxs-lookup"><span data-stu-id="42a77-112">Not supported.</span></span>|  
|<xref:System.Xml.XPath.XPathNodeType.Element>|<span data-ttu-id="42a77-113">Contenuto dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="42a77-113">The content of the element.</span></span>|  
|<xref:System.Xml.XPath.XPathNodeType.Attribute>|<span data-ttu-id="42a77-114">Valore dell'attributo.</span><span class="sxs-lookup"><span data-stu-id="42a77-114">The value of the attribute.</span></span>|  
|<xref:System.Xml.XPath.XPathNodeType.Text>|<span data-ttu-id="42a77-115">Contenuto di testo.</span><span class="sxs-lookup"><span data-stu-id="42a77-115">The text content.</span></span>|  
|<xref:System.Xml.XPath.XPathNodeType.ProcessingInstruction>|<span data-ttu-id="42a77-116">Contenuto eccetto la destinazione.</span><span class="sxs-lookup"><span data-stu-id="42a77-116">The content, excluding the target.</span></span>|  
|<xref:System.Xml.XPath.XPathNodeType.Comment>|<span data-ttu-id="42a77-117">Contenuto del commento.</span><span class="sxs-lookup"><span data-stu-id="42a77-117">The content of the comment.</span></span>|  
|<xref:System.Xml.XPath.XPathNodeType.Namespace>|<span data-ttu-id="42a77-118">Non supportato.</span><span class="sxs-lookup"><span data-stu-id="42a77-118">Not Supported.</span></span>|  
  
> [!NOTE]
> <span data-ttu-id="42a77-119">La modifica dei nodi <xref:System.Xml.XPath.XPathNodeType.Namespace> o del nodo <xref:System.Xml.XPath.XPathNodeType.Root> non è supportata.</span><span class="sxs-lookup"><span data-stu-id="42a77-119">Editing <xref:System.Xml.XPath.XPathNodeType.Namespace> nodes or the <xref:System.Xml.XPath.XPathNodeType.Root> node is not supported.</span></span>  
  
 <span data-ttu-id="42a77-120">La classe <xref:System.Xml.XPath.XPathNavigator> fornisce inoltre un set di metodi usati per inserire e rimuovere nodi.</span><span class="sxs-lookup"><span data-stu-id="42a77-120">The <xref:System.Xml.XPath.XPathNavigator> class also provides a set of methods used to insert and remove nodes.</span></span> <span data-ttu-id="42a77-121">Per altre informazioni sull'inserimento e la rimozione di nodi da un documento XML, vedere gli argomenti [Inserire dati XML con XPathNavigator](insert-xml-data-using-xpathnavigator.md) e [Rimuovere dati XML con XPathNavigator](remove-xml-data-using-xpathnavigator.md).</span><span class="sxs-lookup"><span data-stu-id="42a77-121">For more information about inserting and removing nodes from an XML document, see the [Insert XML Data using XPathNavigator](insert-xml-data-using-xpathnavigator.md) and [Remove XML Data using XPathNavigator](remove-xml-data-using-xpathnavigator.md) topics.</span></span>  
  
### <a name="modifying-untyped-values"></a><span data-ttu-id="42a77-122">Modifica dei valori non tipizzati</span><span class="sxs-lookup"><span data-stu-id="42a77-122">Modifying Untyped Values</span></span>  
 <span data-ttu-id="42a77-123">Il metodo <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> consente semplicemente di inserire il valore non tipizzato `string`, passato come parametro, come valore del nodo su cui è attualmente posizionato l'oggetto <xref:System.Xml.XPath.XPathNavigator>.</span><span class="sxs-lookup"><span data-stu-id="42a77-123">The <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> method simply inserts the untyped `string` value passed as a parameter as the value of the node the <xref:System.Xml.XPath.XPathNavigator> object is currently positioned on.</span></span> <span data-ttu-id="42a77-124">Il valore viene inserito senza alcun tipo o senza verificare la validità del nuovo valore in base al tipo del nodo se sono disponibili le informazioni sullo schema.</span><span class="sxs-lookup"><span data-stu-id="42a77-124">The value is inserted without any type or without verifying that the new value is valid according to the type of the node if schema information is available.</span></span>  
  
 <span data-ttu-id="42a77-125">Nell'esempio seguente, il metodo <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> viene usato per aggiornare tutti gli elementi `price` nel file `contosoBooks.xml`.</span><span class="sxs-lookup"><span data-stu-id="42a77-125">In the following example, the <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> method is used to update all `price` elements in the `contosoBooks.xml` file.</span></span>  
  
 [!code-cpp[XPathNavigatorMethods#47](../../../../samples/snippets/cpp/VS_Snippets_Data/XPathNavigatorMethods/CPP/xpathnavigatormethods.cpp#47)]
 [!code-csharp[XPathNavigatorMethods#47](../../../../samples/snippets/csharp/VS_Snippets_Data/XPathNavigatorMethods/CS/xpathnavigatormethods.cs#47)]
 [!code-vb[XPathNavigatorMethods#47](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XPathNavigatorMethods/VB/xpathnavigatormethods.vb#47)]  
  
 <span data-ttu-id="42a77-126">Nell'esempio il file `contosoBooks.xml` viene considerato come input.</span><span class="sxs-lookup"><span data-stu-id="42a77-126">The example takes the `contosoBooks.xml` file as an input.</span></span>  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
### <a name="modifying-typed-values"></a><span data-ttu-id="42a77-127">Modifica dei valori tipizzati</span><span class="sxs-lookup"><span data-stu-id="42a77-127">Modifying Typed Values</span></span>  
 <span data-ttu-id="42a77-128">Quando il tipo di un nodo è un tipo semplice di W3C XML Schema, il nuovo valore inserito tramite il metodo <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> viene controllato rispetto ai facet del tipo semplice prima dell'impostazione del valore.</span><span class="sxs-lookup"><span data-stu-id="42a77-128">When the type of a node is a W3C XML Schema simple type, the new value inserted by the <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> method is checked against the facets of the simple type before the value is set.</span></span> <span data-ttu-id="42a77-129">Se il nuovo valore non è valido in base al tipo del nodo (ad esempio, l'impostazione di un valore `-1` su un elemento il cui tipo è `xs:positiveInteger`), viene generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="42a77-129">If the new value is not valid according to the type of the node (for example, setting a value of `-1` on an element whose type is `xs:positiveInteger`), it results in an exception.</span></span>  
  
 <span data-ttu-id="42a77-130">Nell'esempio seguente si tenta di modificare il valore dell'elemento `price` del primo elemento `book` nel file `contosoBooks.xml` in un valore <xref:System.DateTime>.</span><span class="sxs-lookup"><span data-stu-id="42a77-130">The following example attempts to change the value of the `price` element of the first `book` element in the `contosoBooks.xml` file to a <xref:System.DateTime> value.</span></span> <span data-ttu-id="42a77-131">Poiché il tipo XML Schema dell'elemento `price` viene definito come `xs:decimal` nei file `contosoBooks.xsd`, viene generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="42a77-131">Because the XML Schema type of the `price` element is defined as `xs:decimal` in the `contosoBooks.xsd` files, this results in an exception.</span></span>  
  
```vb  
Dim settings As XmlReaderSettings = New XmlReaderSettings()  
settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd")  
settings.ValidationType = ValidationType.Schema  
  
Dim reader As XmlReader = XmlReader.Create("contosoBooks.xml", settings)  
  
Dim document As XmlDocument = New XmlDocument()  
document.Load(reader)  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.SetTypedValue(DateTime.Now)  
```  
  
```csharp  
XmlReaderSettings settings = new XmlReaderSettings();  
settings.Schemas.Add("http://www.contoso.com/books", "contosoBooks.xsd");  
settings.ValidationType = ValidationType.Schema;  
  
XmlReader reader = XmlReader.Create("contosoBooks.xml", settings);  
  
XmlDocument document = new XmlDocument();  
document.Load(reader);  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("price", "http://www.contoso.com/books");  
  
navigator.SetTypedValue(DateTime.Now);  
```  
  
 <span data-ttu-id="42a77-132">Nell'esempio il file `contosoBooks.xml` viene considerato come input.</span><span class="sxs-lookup"><span data-stu-id="42a77-132">The example takes the `contosoBooks.xml` file as an input.</span></span>  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 <span data-ttu-id="42a77-133">Anche il file `contosoBooks.xsd` viene considerato come input.</span><span class="sxs-lookup"><span data-stu-id="42a77-133">The example also takes the `contosoBooks.xsd` as an input.</span></span>  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
#### <a name="the-effects-of-editing-strongly-typed-xml-data"></a><span data-ttu-id="42a77-134">Effetti delle modifiche ai dati XML tipizzati in modo sicuro</span><span class="sxs-lookup"><span data-stu-id="42a77-134">The Effects of Editing Strongly Typed XML Data</span></span>  
 <span data-ttu-id="42a77-135">La <xref:System.Xml.XPath.XPathNavigator> classe utilizza l'XML Schema W3C come base per la descrizione di codice XML fortemente tipizzato.</span><span class="sxs-lookup"><span data-stu-id="42a77-135">The <xref:System.Xml.XPath.XPathNavigator> class uses the W3C XML Schema as a basis for describing strongly typed XML.</span></span> <span data-ttu-id="42a77-136">Gli elementi e gli attributi possono essere annotati con informazioni sul tipo basate sulla convalida rispetto a un documento W3C XML Schema.</span><span class="sxs-lookup"><span data-stu-id="42a77-136">Elements and attributes can be annotated with type information based on validation against a W3C XML Schema document.</span></span> <span data-ttu-id="42a77-137">Gli elementi che possono contenere altri elementi o attributi sono denominati tipi complessi, mentre gli elementi che possono contenere solo contenuto testuale sono denominati tipi semplici.</span><span class="sxs-lookup"><span data-stu-id="42a77-137">Elements that can contain other elements or attributes are called complex types, while those that can only contain textual content are called simple types.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="42a77-138">Gli attributi possono disporre solo di tipi semplici.</span><span class="sxs-lookup"><span data-stu-id="42a77-138">Attributes can only have simple types.</span></span>  
  
 <span data-ttu-id="42a77-139">Un elemento o attributo può essere considerato valido per lo schema se è conforme a tutte le regole specifiche della relativa definizione del tipo.</span><span class="sxs-lookup"><span data-stu-id="42a77-139">An element or attribute can be considered to be schema-valid if it conforms to all the rules specific to its type definition.</span></span> <span data-ttu-id="42a77-140">Affinché sia valido per lo schema, un elemento di tipo semplice `xs:int` deve contenere un valore numerico compreso tra -2147483648 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="42a77-140">An element that has the simple type `xs:int` has to contain a numeric value between -2147483648 and 2147483647 to be schema-valid.</span></span> <span data-ttu-id="42a77-141">Per i tipi complessi, la validità di schema dell'elemento dipende dalla validità di schema dei relativi elementi e attributi figlio.</span><span class="sxs-lookup"><span data-stu-id="42a77-141">For complex types, the schema-validity of the element is dependent on the schema-validity of its child elements and attributes.</span></span> <span data-ttu-id="42a77-142">Pertanto, se un elemento è valido in base alla relativa definizione di tipo complesso, tutti gli elementi e gli attributi figlio sono validi in base alle proprie definizioni dei tipi.</span><span class="sxs-lookup"><span data-stu-id="42a77-142">Thus if an element is valid against its complex type definition, all its child elements and attributes are valid against their type definitions.</span></span> <span data-ttu-id="42a77-143">In modo analogo, se anche un solo elemento o attributo figlio di un elemento non è valido in base alla definizione del tipo, o se la validità è sconosciuta, l'elemento sarà non valido o di validità sconosciuta.</span><span class="sxs-lookup"><span data-stu-id="42a77-143">Similarly, if even one of the child elements or attributes of an element is invalid against its type definition, or has an unknown validity, the element is also either invalid or of unknown validity.</span></span>  
  
 <span data-ttu-id="42a77-144">Dato che la validità di un elemento dipende dalla validità degli elementi e attributi figlio, le modifiche apportate a entrambi determinano una modifica della validità dell'elemento in precedenza valido.</span><span class="sxs-lookup"><span data-stu-id="42a77-144">Given that the validity of an element is dependent on the validity of its child elements and attributes, modifications to either result in altering the validity of the element if it was previously valid.</span></span> <span data-ttu-id="42a77-145">In particolare, se gli elementi o attributi figlio di un elemento vengono inseriti, aggiornati o eliminati, la validità dell'elemento risulterà sconosciuta.</span><span class="sxs-lookup"><span data-stu-id="42a77-145">Specifically, if the child elements or attributes of an element are inserted, updated, or deleted, then the validity of the element becomes unknown.</span></span> <span data-ttu-id="42a77-146">Ciò risulterà dalla proprietà <xref:System.Xml.Schema.IXmlSchemaInfo.Validity%2A> della proprietà <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> dell'elemento impostata su <xref:System.Xml.Schema.XmlSchemaValidity.NotKnown>.</span><span class="sxs-lookup"><span data-stu-id="42a77-146">This is represented by the <xref:System.Xml.Schema.IXmlSchemaInfo.Validity%2A> property of the element's <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> property being set to <xref:System.Xml.Schema.XmlSchemaValidity.NotKnown>.</span></span> <span data-ttu-id="42a77-147">Inoltre, questo effetto si estende in modo ricorsivo verso l'alto nel documento XML, poiché anche la validità dell'elemento padre dell'elemento (e del suo elemento padre e così via) risulterà sconosciuta.</span><span class="sxs-lookup"><span data-stu-id="42a77-147">Furthermore, this effect cascades upwards recursively across the XML document, because the validity of the element's parent element (and its parent element, and so on) also becomes unknown.</span></span>  
  
 <span data-ttu-id="42a77-148">Per altre informazioni sulla convalida degli schemi e sulla classe <xref:System.Xml.XPath.XPathNavigator>, vedere [Convalida dello schema con XPathNavigator](schema-validation-using-xpathnavigator.md).</span><span class="sxs-lookup"><span data-stu-id="42a77-148">For more information about schema validation and the <xref:System.Xml.XPath.XPathNavigator> class, see [Schema Validation using XPathNavigator](schema-validation-using-xpathnavigator.md).</span></span>  
  
### <a name="modifying-attributes"></a><span data-ttu-id="42a77-149">Modifica degli attributi</span><span class="sxs-lookup"><span data-stu-id="42a77-149">Modifying Attributes</span></span>  
 <span data-ttu-id="42a77-150">I metodi <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> e <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> possono essere usati per modificare i nodi Attribute tipizzati e non tipizzati, nonché gli altri tipi di nodo elencati nella sezione "Modifica dei nodi".</span><span class="sxs-lookup"><span data-stu-id="42a77-150">The <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> and <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> methods can be used to modify untyped and typed attribute nodes as well as the other node types listed in the "Modifying Nodes" section.</span></span>  
  
 <span data-ttu-id="42a77-151">Nell'esempio seguente viene modificato il valore dell'attributo `genre` del primo elemento `book` nel file `books.xml`.</span><span class="sxs-lookup"><span data-stu-id="42a77-151">The following example changes the value of the `genre` attribute of the first `book` element in the `books.xml` file.</span></span>  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", String.Empty)  
navigator.MoveToChild("book", String.Empty)  
navigator.MoveToAttribute("genre", String.Empty)  
  
navigator.SetValue("non-fiction")  
  
navigator.MoveToRoot()  
Console.WriteLine(navigator.OuterXml)  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", String.Empty);  
navigator.MoveToChild("book", String.Empty);  
navigator.MoveToAttribute("genre", String.Empty);  
  
navigator.SetValue("non-fiction");  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
 <span data-ttu-id="42a77-152">Per altre informazioni sui metodi <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> e <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A>, vedere le sezioni "Modifica dei valori non tipizzati" e "Modifica dei valori tipizzati".</span><span class="sxs-lookup"><span data-stu-id="42a77-152">For more information about the <xref:System.Xml.XPath.XPathNavigator.SetValue%2A> and <xref:System.Xml.XPath.XPathNavigator.SetTypedValue%2A> methods, see the "Modifying Untyped Values" and "Modifying Typed Values" sections.</span></span>  
  
## <a name="innerxml-and-outerxml-properties"></a><span data-ttu-id="42a77-153">Proprietà InnerXml e OuterXml</span><span class="sxs-lookup"><span data-stu-id="42a77-153">InnerXml and OuterXml Properties</span></span>  
 <span data-ttu-id="42a77-154">Le proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> e <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> della classe <xref:System.Xml.XPath.XPathNavigator> consentono di modificare il markup XML dei nodi su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator>.</span><span class="sxs-lookup"><span data-stu-id="42a77-154">The <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> and <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> properties of the <xref:System.Xml.XPath.XPathNavigator> class change the XML markup of the nodes an <xref:System.Xml.XPath.XPathNavigator> object is currently positioned on.</span></span>  
  
 <span data-ttu-id="42a77-155">La proprietà <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> consente di modificare il markup XML dei nodi figlio su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator> con il contenuto analizzato della `string` XML specificata.</span><span class="sxs-lookup"><span data-stu-id="42a77-155">The <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> property changes the XML markup of the child nodes an <xref:System.Xml.XPath.XPathNavigator> object is currently positioned on with the parsed contents of the given XML `string`.</span></span> <span data-ttu-id="42a77-156">Allo stesso modo, la proprietà <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> consente di modificare il markup XML dei nodi figlio su cui è attualmente posizionato un oggetto <xref:System.Xml.XPath.XPathNavigator> nonché il nodo corrente stesso.</span><span class="sxs-lookup"><span data-stu-id="42a77-156">Similarly, the <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> property changes the XML markup of the child nodes an <xref:System.Xml.XPath.XPathNavigator> object is currently positioned on as well as the current node itself.</span></span>  
  
 <span data-ttu-id="42a77-157">Nell'esempio seguente viene usata la proprietà <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> per modificare il valore dell'elemento `price` e inserire un nuovo attributo `discount` sul primo elemento `book` nel file `contosoBooks.xml`.</span><span class="sxs-lookup"><span data-stu-id="42a77-157">The following example uses the <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> property to modify the value of the `price` element and insert a new `discount` attribute on the first `book` element in the `contosoBooks.xml` file.</span></span>  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("contosoBooks.xml");  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("price", "http://www.contoso.com/books")  
  
navigator.OuterXml = "<price discount=\"0\">10.99</price>"  
  
navigator.MoveToRoot()  
Console.WriteLine(navigator.OuterXml)  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("contosoBooks.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.MoveToChild("bookstore", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("price", "http://www.contoso.com/books");  
  
navigator.OuterXml = "<price discount=\"0\">10.99</price>";  
  
navigator.MoveToRoot();  
Console.WriteLine(navigator.OuterXml);  
```  
  
 <span data-ttu-id="42a77-158">Nell'esempio il file `contosoBooks.xml` viene considerato come input.</span><span class="sxs-lookup"><span data-stu-id="42a77-158">The example takes the `contosoBooks.xml` file as an input.</span></span>  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
## <a name="modifying-namespace-nodes"></a><span data-ttu-id="42a77-159">Modifica dei nodi dello spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="42a77-159">Modifying Namespace Nodes</span></span>  
 <span data-ttu-id="42a77-160">Nel DOM (Document Object Model) le dichiarazioni dello spazio dei nomi vengono considerate come attributi regolari che possono essere inseriti, aggiornati ed eliminati.</span><span class="sxs-lookup"><span data-stu-id="42a77-160">In the Document Object Model (DOM), namespace declarations are treated as if they are regular attributes that can be inserted, updated and deleted.</span></span> <span data-ttu-id="42a77-161">Nella classe <xref:System.Xml.XPath.XPathNavigator> tali operazioni sui nodi dello spazio dei nomi non sono consentite, in quanto la modifica del valore di un nodo dello spazio dei nomi può modificare a sua volta l'identità degli elementi e degli attributi nell'ambito del nodo dello spazio dei nomi, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="42a77-161">The <xref:System.Xml.XPath.XPathNavigator> class does not allow such operations on namespace nodes because altering the value of a namespace node can change the identity of the elements and attributes within the scope of the namespace node as illustrated in the following example.</span></span>  
  
```xml  
<root xmlns="http://www.contoso.com">  
    <child />  
</root>  
```  
  
 <span data-ttu-id="42a77-162">Se l'esempio precedente di codice XML viene modificato nel modo seguente, ciascun elemento del documento viene effettivamente rinominato in quanto il valore dell'URI dello spazio dei nomi di ogni singolo elemento è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="42a77-162">If the XML example above is changed in the following way, this effectively renames every element in the document because the value of each element's namespace URI is changed.</span></span>  
  
```xml  
<root xmlns="urn:contoso.com">  
    <child />  
</root>  
```  
  
 <span data-ttu-id="42a77-163">La classe <xref:System.Xml.XPath.XPathNavigator> consente l'inserimento di nodi dello spazio dei nomi che non entrino in conflitto con le dichiarazioni dello spazio dei nomi nell'ambito in cui sono stati inseriti.</span><span class="sxs-lookup"><span data-stu-id="42a77-163">Inserting namespace nodes that do not conflict with namespace declarations at the scope that they are inserted in is allowed by the <xref:System.Xml.XPath.XPathNavigator> class.</span></span> <span data-ttu-id="42a77-164">In questo caso, le dichiarazioni dello spazio dei nomi non sono dichiarate in ambiti inferiori nel documento XML e non determinano alcuna rinomina, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="42a77-164">In this case, the namespace declarations are not declared at lower scopes in the XML document and does not result in renaming as illustrated in the following example.</span></span>  
  
```xml  
<root xmlns:a="http://www.contoso.com">  
    <parent>  
        <a:child />  
    </parent>  
</root>  
```  
  
 <span data-ttu-id="42a77-165">Se l'esempio precedente di codice XML viene modificato nel modo seguente, le dichiarazioni dello spazio dei nomi vengono propagate correttamente nel documento XML nell'ambito inferiore a quello della dichiarazione dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="42a77-165">If the XML example above is changed in the following way, the namespace declarations are correctly propagated across the XML document below the scope of the other namespace declaration.</span></span>  
  
```xml  
<root xmlns:a="http://www.contoso.com">  
    <parent a:parent-id="1234" xmlns:a="http://www.contoso.com/parent-id">  
        <a:child xmlns:a="http://www.contoso.com/" />  
    </parent>  
</root>  
```  
  
 <span data-ttu-id="42a77-166">Nell'esempio precedente di codice XML, l'attributo `a:parent-id` viene inserito sull'elemento `parent` nello spazio dei nomi `http://www.contoso.com/parent-id`.</span><span class="sxs-lookup"><span data-stu-id="42a77-166">In the XML example above, the attribute `a:parent-id` is inserted on the `parent` element in the `http://www.contoso.com/parent-id` namespace.</span></span> <span data-ttu-id="42a77-167">Il metodo <xref:System.Xml.XPath.XPathNavigator.CreateAttribute%2A> viene usato per inserire l'attributo quando si trova posizionato sull'elemento `parent`.</span><span class="sxs-lookup"><span data-stu-id="42a77-167">The <xref:System.Xml.XPath.XPathNavigator.CreateAttribute%2A> method is used to insert the attribute while positioned on the `parent` element.</span></span> <span data-ttu-id="42a77-168">La dichiarazione dello spazio dei nomi `http://www.contoso.com` viene inserita automaticamente dalla classe <xref:System.Xml.XPath.XPathNavigator> per garantire la coerenza della parte restante del documento XML.</span><span class="sxs-lookup"><span data-stu-id="42a77-168">The `http://www.contoso.com` namespace declaration is automatically inserted by the <xref:System.Xml.XPath.XPathNavigator> class to preserve the consistency of the rest of the XML document.</span></span>  
  
## <a name="modifying-entity-reference-nodes"></a><span data-ttu-id="42a77-169">Modifica dei nodi dei riferimenti all'entità</span><span class="sxs-lookup"><span data-stu-id="42a77-169">Modifying Entity Reference Nodes</span></span>  
 <span data-ttu-id="42a77-170">I nodi dei riferimenti all'entità in un oggetto <xref:System.Xml.XmlDocument> sono di sola lettura e non è possibile modificarli tramite le classi <xref:System.Xml.XPath.XPathNavigator> o <xref:System.Xml.XmlNode>.</span><span class="sxs-lookup"><span data-stu-id="42a77-170">Entity reference nodes in an <xref:System.Xml.XmlDocument> object are read-only and cannot be edited using either the <xref:System.Xml.XPath.XPathNavigator> or <xref:System.Xml.XmlNode> classes.</span></span> <span data-ttu-id="42a77-171">Qualsiasi tentativo di modificare un nodo dei riferimenti all'entità determinerà un'eccezione <xref:System.InvalidOperationException>.</span><span class="sxs-lookup"><span data-stu-id="42a77-171">Any attempt to modify an entity reference node results in an <xref:System.InvalidOperationException>.</span></span>  
  
## <a name="modifying-xsinil-nodes"></a><span data-ttu-id="42a77-172">Modifica dei nodi xsi:nil</span><span class="sxs-lookup"><span data-stu-id="42a77-172">Modifying xsi:nil Nodes</span></span>  
 <span data-ttu-id="42a77-173">La raccomandazione W3C XML Schema (informazioni in lingua inglese) illustra il concetto di elemento nillable.</span><span class="sxs-lookup"><span data-stu-id="42a77-173">The W3C XML Schema recommendation introduces the concept of an element being nillable.</span></span> <span data-ttu-id="42a77-174">Quando un elemento è nillable, è possibile che l'elemento non disponga di alcun contenuto pur essendo valido.</span><span class="sxs-lookup"><span data-stu-id="42a77-174">When an element is nillable, it is possible for the element to have no content and still be valid.</span></span> <span data-ttu-id="42a77-175">Il concetto di elemento nillable è simile a quello di oggetto con valore `null`.</span><span class="sxs-lookup"><span data-stu-id="42a77-175">The concept of an element being nillable is similar to the concept of an object being `null`.</span></span> <span data-ttu-id="42a77-176">La differenza principale sta tuttavia nel fatto che un oggetto `null` non è accessibile in alcun modo, mentre un elemento `xsi:nil` continua a disporre di proprietà (gli attributi, ad esempio) a cui è possibile accedere, pur non avendo alcun contenuto (elementi figlio o testo).</span><span class="sxs-lookup"><span data-stu-id="42a77-176">The main difference is that a `null` object cannot be accessed in any way, while an `xsi:nil` element still has properties such as attributes that can be accessed, but has no content (child elements or text).</span></span> <span data-ttu-id="42a77-177">L'esistenza dell'attributo `xsi:nil` con valore `true` su un elemento di un documento XML viene usata per indicare che un elemento è privo di contenuto.</span><span class="sxs-lookup"><span data-stu-id="42a77-177">The existence of the `xsi:nil` attribute with a value of `true` on an element in an XML document is used to indicate that an element has no content.</span></span>  
  
 <span data-ttu-id="42a77-178">Se un oggetto <xref:System.Xml.XPath.XPathNavigator> viene usato per aggiungere contenuto a un elemento valido con un attributo `xsi:nil` e con un valore `true`, il valore dell'attributo `xsi:nil` viene impostato su `false`.</span><span class="sxs-lookup"><span data-stu-id="42a77-178">If an <xref:System.Xml.XPath.XPathNavigator> object is used to add content to a valid element with an `xsi:nil` attribute with a value of `true`, the value of its `xsi:nil` attribute is set to `false`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="42a77-179">Se il contenuto di un elemento con un attributo `xsi:nil` impostato su `false` viene eliminato, il valore dell'attributo non verrà modificato in `true`.</span><span class="sxs-lookup"><span data-stu-id="42a77-179">If the content of an element with an `xsi:nil` attribute set to `false` is deleted, the value of the attribute is not changed to `true`.</span></span>  
  
## <a name="saving-an-xml-document"></a><span data-ttu-id="42a77-180">Salvataggio di un documento XML</span><span class="sxs-lookup"><span data-stu-id="42a77-180">Saving an XML Document</span></span>  
 <span data-ttu-id="42a77-181">Il salvataggio delle modifiche apportate a un oggetto <xref:System.Xml.XmlDocument> come risultato dei metodi di modifica descritti in questo argomento viene eseguito usando i metodi della classe <xref:System.Xml.XmlDocument>.</span><span class="sxs-lookup"><span data-stu-id="42a77-181">Saving changes made to an <xref:System.Xml.XmlDocument> object as the result of the editing methods described in this topic is performed using the methods of the <xref:System.Xml.XmlDocument> class.</span></span> <span data-ttu-id="42a77-182">Per altre informazioni sul salvataggio delle modifiche apportate a un oggetto <xref:System.Xml.XmlDocument>, vedere [Salvataggio e scrittura di un documento](saving-and-writing-a-document.md).</span><span class="sxs-lookup"><span data-stu-id="42a77-182">For more information about saving changes made to an <xref:System.Xml.XmlDocument> object, see [Saving and Writing a Document](saving-and-writing-a-document.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="42a77-183">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="42a77-183">See also</span></span>

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [<span data-ttu-id="42a77-184">Elaborazione di dati XML con il modello di dati XPath</span><span class="sxs-lookup"><span data-stu-id="42a77-184">Process XML Data Using the XPath Data Model</span></span>](process-xml-data-using-the-xpath-data-model.md)
- [<span data-ttu-id="42a77-185">Inserimento dei dati XML utilizzando XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="42a77-185">Insert XML Data using XPathNavigator</span></span>](insert-xml-data-using-xpathnavigator.md)
- [<span data-ttu-id="42a77-186">Rimozione di dati XML con XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="42a77-186">Remove XML Data using XPathNavigator</span></span>](remove-xml-data-using-xpathnavigator.md)

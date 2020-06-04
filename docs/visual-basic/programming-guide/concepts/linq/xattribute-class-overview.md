---
title: Panoramica della classe XAttribute
ms.date: 07/20/2015
ms.assetid: 7781580a-9583-4a1b-ae1e-91c5936eb0b1
ms.openlocfilehash: 5b165044b4bea83e1a0789e3dd00367ed27b43e8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413206"
---
# <a name="xattribute-class-overview-visual-basic"></a><span data-ttu-id="3af80-102">Panoramica della classe XAttribute (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="3af80-102">XAttribute Class Overview (Visual Basic)</span></span>
<span data-ttu-id="3af80-103">Gli attributi sono coppie nome/valore associate a un elemento.</span><span class="sxs-lookup"><span data-stu-id="3af80-103">Attributes are name/value pairs that are associated with an element.</span></span> <span data-ttu-id="3af80-104">La classe <xref:System.Xml.Linq.XAttribute> rappresenta gli attributi XML.</span><span class="sxs-lookup"><span data-stu-id="3af80-104">The <xref:System.Xml.Linq.XAttribute> class represents XML attributes.</span></span>  
  
## <a name="overview"></a><span data-ttu-id="3af80-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="3af80-105">Overview</span></span>  
 <span data-ttu-id="3af80-106">Le modalità di utilizzo degli attributi in [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] sono simili a quelle degli elementi.</span><span class="sxs-lookup"><span data-stu-id="3af80-106">Working with attributes in [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] is similar to working with elements.</span></span> <span data-ttu-id="3af80-107">I relativi costruttori sono simili.</span><span class="sxs-lookup"><span data-stu-id="3af80-107">Their constructors are similar.</span></span> <span data-ttu-id="3af80-108">I metodi usati per recuperare le relative raccolte sono simili.</span><span class="sxs-lookup"><span data-stu-id="3af80-108">The methods that you use to retrieve collections of them are similar.</span></span> <span data-ttu-id="3af80-109">Un'espressione di query LINQ per una raccolta di attributi ha un aspetto molto simile a un'espressione di query LINQ per una raccolta di elementi.</span><span class="sxs-lookup"><span data-stu-id="3af80-109">A LINQ query expression for a collection of attributes looks very similar to a LINQ query expression for a collection of elements.</span></span>  
  
 <span data-ttu-id="3af80-110">L'ordine con cui gli attributi vengono aggiunti a un elemento viene mantenuto.</span><span class="sxs-lookup"><span data-stu-id="3af80-110">The order in which attributes were added to an element is preserved.</span></span> <span data-ttu-id="3af80-111">Quando si scorrono gli attributi, questi vengono visualizzati nell'ordine in cui sono stati aggiunti.</span><span class="sxs-lookup"><span data-stu-id="3af80-111">That is, when you iterate through the attributes, you see them in the same order that they were added.</span></span>  
  
## <a name="the-xattribute-constructor"></a><span data-ttu-id="3af80-112">Costruttore XAttribute</span><span class="sxs-lookup"><span data-stu-id="3af80-112">The XAttribute Constructor</span></span>  
 <span data-ttu-id="3af80-113">Il seguente costruttore della classe <xref:System.Xml.Linq.XAttribute> è quello usato più comunemente:</span><span class="sxs-lookup"><span data-stu-id="3af80-113">The following constructor of the <xref:System.Xml.Linq.XAttribute> class is the one that you will most commonly use:</span></span>  
  
|<span data-ttu-id="3af80-114">Costruttore</span><span class="sxs-lookup"><span data-stu-id="3af80-114">Constructor</span></span>|<span data-ttu-id="3af80-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3af80-115">Description</span></span>|  
|-----------------|-----------------|  
|`XAttribute(XName name, object content)`|<span data-ttu-id="3af80-116">Crea un oggetto <xref:System.Xml.Linq.XAttribute>.</span><span class="sxs-lookup"><span data-stu-id="3af80-116">Creates an <xref:System.Xml.Linq.XAttribute> object.</span></span> <span data-ttu-id="3af80-117">L'argomento `name` specifica il nome dell'attributo, mentre `content` ne specifica il contenuto.</span><span class="sxs-lookup"><span data-stu-id="3af80-117">The `name` argument specifies the name of the attribute; `content` specifies the content of the attribute.</span></span>|  
  
### <a name="creating-an-element-with-an-attribute"></a><span data-ttu-id="3af80-118">Creazione di un elemento con un attributo</span><span class="sxs-lookup"><span data-stu-id="3af80-118">Creating an Element with an Attribute</span></span>  
 <span data-ttu-id="3af80-119">Il codice seguente illustra un elemento che contiene un attributo che usa valori letterali XML in Visual Basic:</span><span class="sxs-lookup"><span data-stu-id="3af80-119">The following code shows an element that contains an attribute using XML literals in Visual Basic:</span></span>  
  
```vb  
Dim phone As XElement = <Phone Type="Home">555-555-5555</Phone>  
Console.WriteLine(phone)  
```  
  
 <span data-ttu-id="3af80-120">Nell'esempio viene prodotto l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="3af80-120">This example produces the following output:</span></span>  
  
```xml  
<Phone Type="Home">555-555-5555</Phone>  
```  
  
### <a name="functional-construction-of-attributes"></a><span data-ttu-id="3af80-121">Costruzione funzionale di attributi</span><span class="sxs-lookup"><span data-stu-id="3af80-121">Functional Construction of Attributes</span></span>  
 <span data-ttu-id="3af80-122">È possibile costruire oggetti <xref:System.Xml.Linq.XAttribute> in linea con la costruzione di oggetti <xref:System.Xml.Linq.XElement>, come descritto di seguito:</span><span class="sxs-lookup"><span data-stu-id="3af80-122">You can construct <xref:System.Xml.Linq.XAttribute> objects in-line with the construction of <xref:System.Xml.Linq.XElement> objects, as follows:</span></span>  
  
```vb  
Dim c As XElement = _  
    <Customers>  
        <Customer>  
            <Name>John Doe</Name>  
            <PhoneNumbers>  
                <Phone type="home">555-555-5555</Phone>  
                <Phone type="work">666-666-6666</Phone>  
            </PhoneNumbers>  
        </Customer>  
    </Customers>  
Console.WriteLine(c)  
```  
  
 <span data-ttu-id="3af80-123">Nell'esempio viene prodotto l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="3af80-123">This example produces the following output:</span></span>  
  
```xml  
<Customers>  
  <Customer>  
    <Name>John Doe</Name>  
    <PhoneNumbers>  
      <Phone type="home">555-555-5555</Phone>  
      <Phone type="work">666-666-6666</Phone>  
    </PhoneNumbers>  
  </Customer>  
</Customers>  
```  
  
### <a name="attributes-are-not-nodes"></a><span data-ttu-id="3af80-124">Attributi non nodi</span><span class="sxs-lookup"><span data-stu-id="3af80-124">Attributes Are Not Nodes</span></span>  
 <span data-ttu-id="3af80-125">Esistono alcune differenze tra attributi ed elementi.</span><span class="sxs-lookup"><span data-stu-id="3af80-125">There are some differences between attributes and elements.</span></span> <span data-ttu-id="3af80-126">Gli oggetti <xref:System.Xml.Linq.XAttribute> non rappresentano nodi nell'albero XML,</span><span class="sxs-lookup"><span data-stu-id="3af80-126"><xref:System.Xml.Linq.XAttribute> objects are not nodes in the XML tree.</span></span> <span data-ttu-id="3af80-127">ma sono coppie nome/valore associate a un elemento XML.</span><span class="sxs-lookup"><span data-stu-id="3af80-127">They are name/value pairs associated with an XML element.</span></span> <span data-ttu-id="3af80-128">A differenza del modello DOM (Document Object Model), questa definizione rispecchia maggiormente la struttura del codice XML.</span><span class="sxs-lookup"><span data-stu-id="3af80-128">In contrast to the Document Object Model (DOM), this more closely reflects the structure of XML.</span></span> <span data-ttu-id="3af80-129">Sebbene gli oggetti <xref:System.Xml.Linq.XAttribute> non siano effettivamente nodi dell'albero XML, le modalità di utilizzo degli oggetti <xref:System.Xml.Linq.XAttribute> sono molto simili a quelle degli oggetti <xref:System.Xml.Linq.XElement>.</span><span class="sxs-lookup"><span data-stu-id="3af80-129">Although <xref:System.Xml.Linq.XAttribute> objects are not actually nodes in the XML tree, working with <xref:System.Xml.Linq.XAttribute> objects is very similar to working with <xref:System.Xml.Linq.XElement> objects.</span></span>  
  
 <span data-ttu-id="3af80-130">Questa distinzione è di fondamentale importanza solo per gli sviluppatori che scrivono codice che riguarda gli alberi XML a livello di nodo.</span><span class="sxs-lookup"><span data-stu-id="3af80-130">This distinction is primarily important only to developers who are writing code that works with XML trees at the node level.</span></span> <span data-ttu-id="3af80-131">Non interessa quindi la maggior parte degli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="3af80-131">Many developers will not be concerned with this distinction.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3af80-132">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3af80-132">See also</span></span>

- [<span data-ttu-id="3af80-133">Panoramica della programmazione LINQ to XML (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="3af80-133">LINQ to XML Programming Overview (Visual Basic)</span></span>](linq-to-xml-programming-overview.md)

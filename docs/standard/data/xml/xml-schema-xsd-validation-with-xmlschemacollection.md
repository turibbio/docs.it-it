---
title: Convalida XSD (XML Schema) con XmlSchemaCollection
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: ad0b5717-3d32-41ad-a4d7-072c3e492b82
ms.openlocfilehash: 2ff8a8b85c3bfa594bd958a9a3688380885e0426
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290305"
---
# <a name="xml-schema-xsd-validation-with-xmlschemacollection"></a><span data-ttu-id="0de33-102">Convalida XSD (XML Schema) con XmlSchemaCollection</span><span class="sxs-lookup"><span data-stu-id="0de33-102">XML Schema (XSD) Validation with XmlSchemaCollection</span></span>
<span data-ttu-id="0de33-103">È possibile usare il tipo <xref:System.Xml.Schema.XmlSchemaCollection> per convalidare un documento XML in base a schemi XSD (XML Schema Definition Language).</span><span class="sxs-lookup"><span data-stu-id="0de33-103">You can use the <xref:System.Xml.Schema.XmlSchemaCollection> to validate an XML document against XML Schema definition language (XSD) schemas.</span></span> <span data-ttu-id="0de33-104">Il tipo <xref:System.Xml.Schema.XmlSchemaCollection> migliora le prestazioni archiviando gli schemi nella raccolta in modo che non vengano caricati in memoria ogni volta che viene eseguita la convalida.</span><span class="sxs-lookup"><span data-stu-id="0de33-104">The <xref:System.Xml.Schema.XmlSchemaCollection> improves performance by storing schemas in the collection so they are not loaded into memory each time validation occurs.</span></span> <span data-ttu-id="0de33-105">Se lo schema esiste nella raccolta di schemi, l'attributo `schemaLocation` verrà usato per cercare lo schema nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="0de33-105">If the schema exists in the schema collection, the `schemaLocation` attribute is used to look up the schema in the collection.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="0de33-106">La classe <xref:System.Xml.Schema.XmlSchemaCollection> è obsoleta ed è stata sostituita dalla classe <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="0de33-106">The <xref:System.Xml.Schema.XmlSchemaCollection> class is now obsolete and has been replaced with the <xref:System.Xml.Schema.XmlSchemaSet> class.</span></span> <span data-ttu-id="0de33-107">Per altre informazioni sulla classe <xref:System.Xml.Schema.XmlSchemaSet>, vedere [XmlSchemaSet per la compilazione di schemi](xmlschemaset-for-schema-compilation.md).</span><span class="sxs-lookup"><span data-stu-id="0de33-107">For more information about the <xref:System.Xml.Schema.XmlSchemaSet> class see, [XmlSchemaSet for Schema Compilation](xmlschemaset-for-schema-compilation.md).</span></span>  
  
 <span data-ttu-id="0de33-108">Nell'esempio seguente viene illustrato l'elemento radice di un file di dati.</span><span class="sxs-lookup"><span data-stu-id="0de33-108">The following example shows the root element of a data file.</span></span>  
  
```xml  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"  
    xmlns="urn:bookstore-schema"  
    elementFormDefault="qualified"  
    targetNamespace="urn:bookstore-schema">  
```  
  
 <span data-ttu-id="0de33-109">In questo esempio, il valore dell'attributo `targetNamespace` è `urn:bookstore-schema`, ovvero lo stesso spazio dei nomi usato quando si aggiunge lo schema all'oggetto <xref:System.Xml.Schema.XmlSchemaCollection>.</span><span class="sxs-lookup"><span data-stu-id="0de33-109">For this example, the value of the `targetNamespace` attribute is `urn:bookstore-schema`, which is the same namespace that is used when adding the schema to the <xref:System.Xml.Schema.XmlSchemaCollection>.</span></span>  
  
 <span data-ttu-id="0de33-110">Nell'esempio di codice seguente viene aggiunto uno schema XML al tipo <xref:System.Xml.Schema.XmlSchemaCollection>.</span><span class="sxs-lookup"><span data-stu-id="0de33-110">The following code example adds an XML Schema to the <xref:System.Xml.Schema.XmlSchemaCollection>.</span></span>  
  
```vb  
Dim xsc As New XmlSchemaCollection()  
' XML Schema.  
xsc.Add("urn:bookstore-schema", schema)
reader = New XmlTextReader(filename)  
vreader = New XmlValidatingReader(reader)  
vreader.Schemas.Add(xsc)  
```  
  
```csharp  
XmlSchemaCollection xsc = new XmlSchemaCollection();  
// XML Schema.  
xsc.Add("urn:bookstore-schema", schema);  
reader = new XmlTextReader (filename);  
vreader = new XmlValidatingReader (reader);  
vreader.Schemas.Add(xsc);  
```  
  
 <span data-ttu-id="0de33-111">In genere, l'attributo `targetNamespace` viene usato per aggiungere la proprietà `namespaceURI` nel metodo <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> per l'oggetto <xref:System.Xml.Schema.XmlSchemaCollection>.</span><span class="sxs-lookup"><span data-stu-id="0de33-111">The `targetNamespace` attribute is generally used when you add the `namespaceURI` property in the <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> method for the <xref:System.Xml.Schema.XmlSchemaCollection>.</span></span> <span data-ttu-id="0de33-112">È possibile specificare un riferimento null prima di aggiungere lo schema al tipo <xref:System.Xml.Schema.XmlSchemaCollection>.</span><span class="sxs-lookup"><span data-stu-id="0de33-112">You can specify a null reference before adding the schema to the <xref:System.Xml.Schema.XmlSchemaCollection>.</span></span> <span data-ttu-id="0de33-113">Per gli schemi senza uno spazio dei nomi è necessario usare una stringa vuota ("").</span><span class="sxs-lookup"><span data-stu-id="0de33-113">An empty string ("") should be used for schemas without a namespace.</span></span> <span data-ttu-id="0de33-114">Nel tipo <xref:System.Xml.Schema.XmlSchemaCollection> può essere presente solo uno schema senza uno spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="0de33-114">The <xref:System.Xml.Schema.XmlSchemaCollection> can have only one schema without a namespace.</span></span>  
  
 <span data-ttu-id="0de33-115">Nell'esempio di codice seguente viene aggiunto uno schema XML, HeadCount.xsd, al tipo <xref:System.Xml.Schema.XmlSchemaCollection> e viene eseguita la convalida di HeadCount.xml.</span><span class="sxs-lookup"><span data-stu-id="0de33-115">The following code example adds an XML Schema, HeadCount.xsd, to the <xref:System.Xml.Schema.XmlSchemaCollection> and validates HeadCount.xml.</span></span>  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Schema  
  
Namespace ValidationSample  
  
   Class Sample  
  
      Public Shared Sub Main()  
         Dim tr As New XmlTextReader("HeadCount.xml")  
         Dim vr As New XmlValidatingReader(tr)  
  
         vr.Schemas.Add("xsdHeadCount", "HeadCount.xsd")  
         vr.ValidationType = ValidationType.Schema  
         AddHandler vr.ValidationEventHandler, AddressOf ValidationHandler  
  
         While vr.Read()  
         End While  
         Console.WriteLine("Validation finished")  
      End Sub  
      ' Main  
  
      Public Shared Sub ValidationHandler(sender As Object, args As ValidationEventArgs)  
         Console.WriteLine("***Validation error")  
         Console.WriteLine("Severity:{0}", args.Severity)  
         Console.WriteLine("Message:{0}", args.Message)  
      End Sub  
      ' ValidationHandler  
   End Class  
   ' Sample  
End Namespace  
' ValidationSample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Schema;  
  
namespace ValidationSample  
{  
   class Sample  
   {  
      public static void Main()  
      {  
         XmlTextReader tr = new XmlTextReader("HeadCount.xml");  
         XmlValidatingReader vr = new XmlValidatingReader(tr);  
  
         vr.Schemas.Add("xsdHeadCount", "HeadCount.xsd");  
         vr.ValidationType = ValidationType.Schema;  
         vr.ValidationEventHandler += new ValidationEventHandler (ValidationHandler);  
  
         while(vr.Read());  
         Console.WriteLine("Validation finished");  
      }  
  
      public static void ValidationHandler(object sender, ValidationEventArgs args)  
      {  
         Console.WriteLine("***Validation error");  
         Console.WriteLine("\tSeverity:{0}", args.Severity);  
         Console.WriteLine("\tMessage  :{0}", args.Message);  
      }  
   }  
}  
```  
  
 <span data-ttu-id="0de33-116">Di seguito viene indicato il contenuto del file di input, HeadCount.xml, da convalidare.</span><span class="sxs-lookup"><span data-stu-id="0de33-116">The following outlines the contents of the input file, HeadCount.xml, to be validated.</span></span>  
  
```xml  
<!--Load HeadCount.xsd in SchemaCollection for Validation-->  
<hc:HeadCount xmlns:hc='xsdHeadCount'>  
   <Name>Waldo Pepper</Name>  
   <Name>Red Pepper</Name>  
</hc:HeadCount>  
```  
  
 <span data-ttu-id="0de33-117">Di seguito viene indicato il contenuto del file di XML Schema, HeadCount.xsd, in base al quale eseguire la convalida.</span><span class="sxs-lookup"><span data-stu-id="0de33-117">The following outlines the contents of the XML Schema file, HeadCount.xsd, to be validated against.</span></span>  
  
```xml  
<xs:schema xmlns="xsdHeadCount" targetNamespace="xsdHeadCount" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
   <xs:element name='HeadCount' type="HEADCOUNT"/>  
   <xs:complexType name="HEADCOUNT">  
      <xs:sequence>  
         <xs:element name='Name' type='xs:string' maxOccurs='unbounded'/>  
      </xs:sequence>  
      <xs:attribute name='division' type='xs:int' use='optional' default='8'/>  
   </xs:complexType>  
</xs:schema>  
```  
  
 <span data-ttu-id="0de33-118">Nell'esempio di codice seguente viene creato un <xref:System.Xml.XmlValidatingReader> che accetta un <xref:System.Xml.XmlTextReader>.</span><span class="sxs-lookup"><span data-stu-id="0de33-118">The following code example creates an <xref:System.Xml.XmlValidatingReader> that takes an <xref:System.Xml.XmlTextReader>.</span></span> <span data-ttu-id="0de33-119">Il file di input, sample4.xml, viene convalidato in base a XML Schema, sample4.xsd.</span><span class="sxs-lookup"><span data-stu-id="0de33-119">The input file, sample4.xml, is validated against the XML Schema, sample4.xsd.</span></span>  
  
```vb  
Dim tr As New XmlTextReader("sample4.xml")  
Dim vr As New XmlValidatingReader(tr)  
vr.ValidationType = ValidationType.Schema  
vr.Schemas.Add("datatypesTest", "sample4.xsd")  
AddHandler vr.ValidationEventHandler, AddressOf ValidationCallBack  
While vr.Read()  
   Console.WriteLine("NodeType: {0} NodeName: {1}", vr.NodeType, vr.Name)  
End While  
```  
  
```csharp  
XmlTextReader tr = new XmlTextReader("sample4.xml");  
XmlValidatingReader vr = new XmlValidatingReader(tr);  
vr.ValidationType = ValidationType.Schema;  
        vr.Schemas.Add("datatypesTest", "sample4.xsd");  
vr.ValidationEventHandler += new ValidationEventHandler(ValidationCallBack);  
while(vr.Read()) {  
    Console.WriteLine("NodeType: {0} NodeName: {1}", vr.NodeType, vr.Name);  
    }  
```  
  
 <span data-ttu-id="0de33-120">Di seguito viene indicato il contenuto del file di input, sample4.xml, da convalidare.</span><span class="sxs-lookup"><span data-stu-id="0de33-120">The following outlines the contents of the input file, sample4.xml, to be validated.</span></span>  
  
```xml  
<datatypes xmlns="datatypesTest">  
    <number>  
        <number_1>123</number_1>  
    </number>  
</datatypes>  
```  
  
 <span data-ttu-id="0de33-121">Di seguito viene indicato il contenuto del file di XML Schema, sample4.xsd, in base al quale eseguire la convalida.</span><span class="sxs-lookup"><span data-stu-id="0de33-121">The following outlines the contents of the XML Schema file, sample4.xsd, to be validated against.</span></span>  
  
```xml  
<xs:schema
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    xmlns:tns="datatypesTest"
    targetNamespace="datatypesTest"  
    elementFormDefault="qualified">  
  
<xs:element name = "datatypes">  
  <xs:complexType>  
    <xs:all>  
        <xs:element name="number">  
            <xs:complexType>  
                <xs:sequence>  
                    <xs:element name="number_1" type="xs:decimal" maxOccurs="unbounded"/>  
                </xs:sequence>  
            </xs:complexType>  
        </xs:element>  
    </xs:all>  
  </xs:complexType>  
</xs:element>  
</xs:schema>  
```  
  
## <a name="see-also"></a><span data-ttu-id="0de33-122">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0de33-122">See also</span></span>

- <xref:System.Xml.XmlParserContext>
- <xref:System.Xml.XmlValidatingReader.ValidationEventHandler?displayProperty=nameWithType>
- <xref:System.Xml.XmlValidatingReader.Schemas%2A?displayProperty=nameWithType>
- [<span data-ttu-id="0de33-123">Compilazione dello schema XmlSchemaCollection</span><span class="sxs-lookup"><span data-stu-id="0de33-123">XmlSchemaCollection Schema Compilation</span></span>](xmlschemacollection-schema-compilation.md)

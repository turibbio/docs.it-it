---
title: 'Procedura: Recuperare paragrafi da un documento Office Open XML'
ms.date: 07/20/2015
ms.assetid: 66053f21-9217-473c-a6f3-a0897be07756
ms.openlocfilehash: 49441da3b9a0bc43c3528a14d03aa44d8173be42
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397830"
---
# <a name="how-to-retrieve-paragraphs-from-an-office-open-xml-document-visual-basic"></a><span data-ttu-id="a0db7-102">Procedura: recuperare paragrafi da un documento Office Open XML (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="a0db7-102">How to: Retrieve Paragraphs from an Office Open XML Document (Visual Basic)</span></span>
<span data-ttu-id="a0db7-103">In questo argomento viene presentato un esempio in cui viene aperto un documento Office Open XML e viene recuperata una raccolta di tutti i relativi paragrafi.</span><span class="sxs-lookup"><span data-stu-id="a0db7-103">This topic presents an example that opens an Office Open XML document, and retrieves a collection of all of the paragraphs in the document.</span></span>  
  
 <span data-ttu-id="a0db7-104">Per ulteriori informazioni su Office Open XML, vedere il [Blog di Eric White](http://www.ericwhite.com).</span><span class="sxs-lookup"><span data-stu-id="a0db7-104">For more information on Office Open XML, see [Eric White's Blog](http://www.ericwhite.com).</span></span>  
  
## <a name="example"></a><span data-ttu-id="a0db7-105">Esempio</span><span class="sxs-lookup"><span data-stu-id="a0db7-105">Example</span></span>  
 <span data-ttu-id="a0db7-106">In questo esempio viene aperto un pacchetto Office Open XML e vengono usate le relazioni all'interno del pacchetto per trovare le parti di documento e di stile.</span><span class="sxs-lookup"><span data-stu-id="a0db7-106">This example opens an Office Open XML package, uses the relationships within the Open XML package to find the document and the style parts.</span></span> <span data-ttu-id="a0db7-107">Viene quindi eseguita una query sul documento, proiettando una raccolta di un tipo anonimo che contiene il nodo <xref:System.Xml.Linq.XElement> del paragrafo, il nome dello stile di ogni paragrafo e il testo di ogni paragrafo.</span><span class="sxs-lookup"><span data-stu-id="a0db7-107">It then queries the document, projecting a collection of an anonymous type that contains the paragraph <xref:System.Xml.Linq.XElement> node, the style name of each paragraph, and the text of each paragraph.</span></span>  
  
 <span data-ttu-id="a0db7-108">Viene usato un metodo di estensione denominato `StringConcatenate`, specificato nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="a0db7-108">The example uses an extension method named `StringConcatenate`, which is also supplied in the example.</span></span>  
  
 <span data-ttu-id="a0db7-109">Per un'esercitazione dettagliata che illustra il funzionamento di questo esempio, vedere la pagina relativa alle [trasformazioni funzionali pure di XML (Visual Basic)](pure-functional-transformations-of-xml.md).</span><span class="sxs-lookup"><span data-stu-id="a0db7-109">For a detailed tutorial that explains how this example works, see [Pure Functional Transformations of XML (Visual Basic)](pure-functional-transformations-of-xml.md).</span></span>  
  
 <span data-ttu-id="a0db7-110">In questo esempio vengono usate classi dell'assembly WindowsBase</span><span class="sxs-lookup"><span data-stu-id="a0db7-110">This example uses classes found in the WindowsBase assembly.</span></span> <span data-ttu-id="a0db7-111">e i tipi dello spazio dei nomi <xref:System.IO.Packaging?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="a0db7-111">It uses types in the <xref:System.IO.Packaging?displayProperty=nameWithType> namespace.</span></span>  
  
```vb  
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">  
  
Module Module1  
    <System.Runtime.CompilerServices.Extension()> _  
    Public Function StringConcatenate(ByVal source As IEnumerable(Of String)) As String  
        Dim sb As StringBuilder = New StringBuilder()  
        For Each s As String In source  
            sb.Append(s)  
        Next  
        Return sb.ToString()  
    End Function  
  
    <System.Runtime.CompilerServices.Extension()> _  
    Public Function StringConcatenate(Of T)(ByVal source As IEnumerable(Of T), _  
    ByVal func As Func(Of T, String)) As String  
        Dim sb As StringBuilder = New StringBuilder()  
        For Each item As T In source  
            sb.Append(func(item))  
        Next  
        Return sb.ToString()  
    End Function  
  
    <System.Runtime.CompilerServices.Extension()> _  
    Public Function StringConcatenate(Of T)(ByVal source As IEnumerable(Of T), _  
    ByVal separator As String) As String  
        Dim sb As StringBuilder = New StringBuilder()  
        For Each s As T In source  
            sb.Append(s).Append(separator)  
        Next  
        Return sb.ToString()  
    End Function  
  
    <System.Runtime.CompilerServices.Extension()> _  
    Public Function StringConcatenate(Of T)(ByVal source As IEnumerable(Of T), _  
    ByVal func As Func(Of T, String), ByVal separator As String) As String  
        Dim sb As StringBuilder = New StringBuilder()  
        For Each item As T In source  
            sb.Append(func(item)).Append(separator)  
        Next  
        Return sb.ToString()  
    End Function  
  
    Public Function ParagraphText(ByVal e As XElement) As String  
        Dim w As XNamespace = e.Name.Namespace  
        Return (e.<w:r>.<w:t>).StringConcatenate(Function(element) CStr(element))  
    End Function  
  
    ' Following function is required because Visual Basic does not support short circuit evaluation  
    Private Function GetStyleOfParagraph(ByVal styleNode As XElement, ByVal defaultStyle As String) _  
                As String  
        If (styleNode Is Nothing) Then  
            Return defaultStyle  
        Else  
            Return styleNode.@w:val  
        End If  
    End Function  
  
    Sub Main()  
        Dim fileName = "SampleDoc.docx"  
  
        Dim documentRelationshipType = _  
          "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"  
        Dim stylesRelationshipType = _  
          "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles"  
        Dim wordmlNamespace = _  
          "http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
  
        Dim xDoc As XDocument = Nothing  
        Dim styleDoc As XDocument = Nothing  
        Using wdPackage As Package = Package.Open(fileName, FileMode.Open, FileAccess.Read)  
            Dim docPackageRelationship As PackageRelationship = _  
              wdPackage _  
              .GetRelationshipsByType(documentRelationshipType) _  
              .FirstOrDefault()  
            If (docPackageRelationship IsNot Nothing) Then  
                Dim documentUri As Uri = _  
                  PackUriHelper _  
                  .ResolvePartUri(New Uri("/", UriKind.Relative), docPackageRelationship.TargetUri)  
                Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)  
  
                '  Load the document XML in the part into an XDocument instance.  
                xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()))  
  
                '  Find the styles part. There will only be one.  
                Dim styleRelation As PackageRelationship = documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()  
                If (styleRelation IsNot Nothing) Then  
                    Dim styleUri As Uri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)  
                    Dim stylePart As PackagePart = wdPackage.GetPart(styleUri)  
  
                    '  Load the style XML in the part into an XDocument instance.  
                    styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()))  
                End If  
            End If  
        End Using  
  
        Dim defaultStyle As String = _  
            ( _  
                From style In styleDoc.Root.<w:style> _  
                Where style.@w:type = "paragraph" And _  
                      style.@w:default = "1" _  
                Select style _  
            ).First().@w:styleId  
  
        ' Find all paragraphs in the document.  
        Dim paragraphs = _  
            From para In xDoc.Root.<w:body>...<w:p> _  
        Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault _  
        Select New With { _  
            .ParagraphNode = para, _  
            .StyleName = GetStyleOfParagraph(styleNode, defaultStyle) _  
        }  
  
        ' Retrieve the text of each paragraph.  
        Dim paraWithText = _  
            From para In paragraphs _  
            Select New With { _  
                .ParagraphNode = para.ParagraphNode, _  
                .StyleName = para.StyleName, _  
                .Text = ParagraphText(para.ParagraphNode) _  
            }  
  
        For Each p In paraWithText  
            Console.WriteLine("StyleName:{0} >{1}<", p.StyleName, p.Text)  
        Next  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="a0db7-112">Quando viene eseguito con il documento Open XML di esempio descritto in [creazione del documento Office Open XML di origine (Visual Basic)](creating-the-source-office-open-xml-document.md), questo esempio produce l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="a0db7-112">When run with the sample Open XML document described in [Creating the Source Office Open XML Document (Visual Basic)](creating-the-source-office-open-xml-document.md), this example produces the following output:</span></span>  
  
```console  
StyleName:Heading1 >Parsing WordprocessingML with LINQ to XML<  
StyleName:Normal ><  
StyleName:Normal >The following example prints to the console.<  
StyleName:Normal ><  
StyleName:Code >using System;<  
StyleName:Code ><  
StyleName:Code >class Program {<  
StyleName:Code >    public static void (string[] args) {<  
StyleName:Code >        Console.WriteLine("Hello World");<  
StyleName:Code >    }<  
StyleName:Code >}<  
StyleName:Normal ><  
StyleName:Normal >This example produces the following output:<  
StyleName:Normal ><  
StyleName:Code >Hello World<  
```  
  
## <a name="see-also"></a><span data-ttu-id="a0db7-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a0db7-113">See also</span></span>

- [<span data-ttu-id="a0db7-114">Tecniche di query avanzate (LINQ to XML) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="a0db7-114">Advanced Query Techniques (LINQ to XML) (Visual Basic)</span></span>](advanced-query-techniques-linq-to-xml.md)

---
title: Proiezione di XML in una forma diversa
ms.date: 07/20/2015
ms.assetid: 2da7ec97-34f7-443d-9a48-b162ac58236b
ms.openlocfilehash: 1424b88b478896854b0f094ca4ec8eba82b816b4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396363"
---
# <a name="projecting-xml-in-a-different-shape-visual-basic"></a><span data-ttu-id="bec4f-102">Proiezione di XML in una forma diversa (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="bec4f-102">Projecting XML in a Different Shape (Visual Basic)</span></span>
<span data-ttu-id="bec4f-103">In questo argomento viene illustrato un esempio di proiezione del codice XML in una forma diversa da quella del codice XML di origine.</span><span class="sxs-lookup"><span data-stu-id="bec4f-103">This topic shows an example of projecting XML that is in a different shape than the source XML.</span></span>  
  
 <span data-ttu-id="bec4f-104">Molte trasformazioni XML tipiche sono costituite da query concatenate, come nel caso di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="bec4f-104">Many typical XML transformations consist of chained queries, as in this example.</span></span> <span data-ttu-id="bec4f-105">Non è infrequente iniziare con un qualche tipo di codice XML, proiettare i risultati intermedi come raccolte di tipi anonimi o con nome e infine proiettare i risultati nuovamente nel codice XML in una forma completamente diverso rispetto al codice XML di origine.</span><span class="sxs-lookup"><span data-stu-id="bec4f-105">It is common to start with some form of XML, project intermediate results as collections of anonymous types or named types, and then finally to project the results back into XML that is in an entirely different shape than the source XML.</span></span>  
  
## <a name="example"></a><span data-ttu-id="bec4f-106">Esempio</span><span class="sxs-lookup"><span data-stu-id="bec4f-106">Example</span></span>  
 <span data-ttu-id="bec4f-107">In questo esempio viene elaborato un documento WordprocessingML, recuperandone i nodi dei paragrafi da un documento WordprocessingML.</span><span class="sxs-lookup"><span data-stu-id="bec4f-107">This example processes a WordprocessingML document, retrieving the paragraph nodes from a WordprocessingML document.</span></span> <span data-ttu-id="bec4f-108">Vengono inoltre identificati lo stile e il testo di ciascun paragrafo.</span><span class="sxs-lookup"><span data-stu-id="bec4f-108">It also identifies the style and text of each paragraph.</span></span> <span data-ttu-id="bec4f-109">Infine il codice XML viene proiettato con una forma diversa.</span><span class="sxs-lookup"><span data-stu-id="bec4f-109">Finally, the example projects XML with a different shape.</span></span> <span data-ttu-id="bec4f-110">Questo esempio si basa su esempi precedenti di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bec4f-110">This example builds on the previous examples in this tutorial.</span></span> <span data-ttu-id="bec4f-111">La nuova istruzione usata per la proiezione è indicata nei commenti del codice riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="bec4f-111">The new statement that does the projection is called out in comments in the code below.</span></span>  
  
 <span data-ttu-id="bec4f-112">Per istruzioni sulla creazione del documento di origine per questo esempio, vedere [creazione del documento Office Open XML di origine (Visual Basic)](creating-the-source-office-open-xml-document.md).</span><span class="sxs-lookup"><span data-stu-id="bec4f-112">For instructions for creating the source document for this example, see [Creating the Source Office Open XML Document (Visual Basic)](creating-the-source-office-open-xml-document.md).</span></span>  
  
 <span data-ttu-id="bec4f-113">In questo esempio vengono usate classi dell'assembly WindowsBase</span><span class="sxs-lookup"><span data-stu-id="bec4f-113">This example uses classes from the WindowsBase assembly.</span></span> <span data-ttu-id="bec4f-114">e i tipi dello spazio dei nomi <xref:System.IO.Packaging?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="bec4f-114">It uses types in the <xref:System.IO.Packaging?displayProperty=nameWithType> namespace.</span></span>  
  
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
    Private Function GetStyleOfParagraph(ByVal styleNode As XElement, _  
                                         ByVal defaultStyle As String) As String  
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
              wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault()  
            If (docPackageRelationship IsNot Nothing) Then  
                Dim documentUri As Uri = PackUriHelper.ResolvePartUri(New Uri("/", UriKind.Relative), _  
                  docPackageRelationship.TargetUri)  
                Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)  
  
                '  Load the document XML in the part into an XDocument instance.  
                xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()))  
  
                '  Find the styles part. There will only be one.  
                Dim styleRelation As PackageRelationship = _  
                  documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()  
                If (Not (styleRelation Is Nothing)) Then  
                    Dim styleUri As Uri = _  
                      PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)  
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
  
        ' Following is the new code that projects XML in a new shape  
        Dim root As XElement = _  
            <Root>  
                <%= _  
                    From p In paraWithText _  
                    Select _  
                    <Paragraph>  
                        <StyleName><%= p.StyleName %></StyleName>  
                        <Text><%= p.Text %></Text>  
                    </Paragraph> _  
                %>  
            </Root>  
  
        Console.WriteLine(root)  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="bec4f-115">Nell'esempio viene prodotto l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="bec4f-115">This example produces the following output:</span></span>  
  
```xml  
<Root>  
  <Paragraph>  
    <StyleName>Heading1</StyleName>  
    <Text>Parsing WordprocessingML with LINQ to XML</Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Normal</StyleName>  
    <Text></Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Normal</StyleName>  
    <Text>The following example prints to the console.</Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Normal</StyleName>  
    <Text></Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Code</StyleName>  
    <Text>Imports System</Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Code</StyleName>  
    <Text></Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Code</StyleName>  
    <Text>Class Program</Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Code</StyleName>  
    <Text>    Public Shared  Sub Main(ByVal args() As String)</Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Code</StyleName>  
    <Text>        Console.WriteLine("Hello World")</Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Code</StyleName>  
    <Text>    End Sub</Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Code</StyleName>  
    <Text>End Class</Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Normal</StyleName>  
    <Text></Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Normal</StyleName>  
    <Text>This example produces the following output:</Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Normal</StyleName>  
    <Text></Text>  
  </Paragraph>  
  <Paragraph>  
    <StyleName>Code</StyleName>  
    <Text>Hello World</Text>  
  </Paragraph>  
</Root>  
```  
  
## <a name="next-steps"></a><span data-ttu-id="bec4f-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bec4f-116">Next Steps</span></span>  
 <span data-ttu-id="bec4f-117">Nell'esempio successivo viene eseguita una query per individuare tutto il testo in un documento di Word:</span><span class="sxs-lookup"><span data-stu-id="bec4f-117">In the next example, you'll query to find all the text in a Word document:</span></span>  
  
- [<span data-ttu-id="bec4f-118">Ricerca di testo nei documenti di Word (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="bec4f-118">Finding Text in Word Documents (Visual Basic)</span></span>](finding-text-in-word-documents.md)  
  
## <a name="see-also"></a><span data-ttu-id="bec4f-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="bec4f-119">See also</span></span>

- [<span data-ttu-id="bec4f-120">Esercitazione: modifica del contenuto in un documento WordprocessingML (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="bec4f-120">Tutorial: Manipulating Content in a WordprocessingML Document (Visual Basic)</span></span>](tutorial-manipulating-content-in-a-wordprocessingml-document.md)

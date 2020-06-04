---
title: Recupero del testo dei paragrafi
ms.date: 07/20/2015
ms.assetid: 095fa0d9-7b1b-4cbb-9c13-e2c9d8923d31
ms.openlocfilehash: 24167ade2d0326ef9382536f79f9e45eb22c89c5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413388"
---
# <a name="retrieving-the-text-of-the-paragraphs-visual-basic"></a><span data-ttu-id="e687c-102">Recupero del testo dei paragrafi (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e687c-102">Retrieving the Text of the Paragraphs (Visual Basic)</span></span>
<span data-ttu-id="e687c-103">Questo esempio si basa sull'esempio precedente, [recuperando i paragrafi e i relativi stili (Visual Basic)](retrieving-the-paragraphs-and-their-styles.md).</span><span class="sxs-lookup"><span data-stu-id="e687c-103">This example builds on the previous example, [Retrieving the Paragraphs and Their Styles (Visual Basic)](retrieving-the-paragraphs-and-their-styles.md).</span></span> <span data-ttu-id="e687c-104">Questo nuovo esempio consente di recuperare il testo di ciascun paragrafo sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="e687c-104">This new example retrieves the text of each paragraph as a string.</span></span>  
  
 <span data-ttu-id="e687c-105">Per recuperare il testo, nell'esempio viene aggiunta un'ulteriore query che scorre la raccolta di tipi anonimi e proietta una nuova raccolta di un tipo anonimo con l'aggiunta di un nuovo membro `Text`.</span><span class="sxs-lookup"><span data-stu-id="e687c-105">To retrieve the text, this example adds an additional query that iterates through the collection of anonymous types and projects a new collection of an anonymous type with the addition of a new member, `Text`.</span></span> <span data-ttu-id="e687c-106">Viene usato l'operatore di query standard <xref:System.Linq.Enumerable.Aggregate%2A> per concatenare più stringhe in un'unica stringa.</span><span class="sxs-lookup"><span data-stu-id="e687c-106">It uses the <xref:System.Linq.Enumerable.Aggregate%2A> standard query operator to concatenate multiple strings into one string.</span></span>  
  
 <span data-ttu-id="e687c-107">Questa tecnica, che prevede dapprima la proiezione di una raccolta di un tipo anonimo e quindi l'uso di questa raccolta per la proiezione in una nuova raccolta di un tipo anonimo, costituisce un idioma comune e utile.</span><span class="sxs-lookup"><span data-stu-id="e687c-107">This technique (that is, first projecting to a collection of an anonymous type, then using this collection to project to a new collection of an anonymous type) is a common and useful idiom.</span></span> <span data-ttu-id="e687c-108">Sarebbe stato possibile scrivere la query senza la proiezione nel primo tipo anonimo,</span><span class="sxs-lookup"><span data-stu-id="e687c-108">This query could have been written without projecting to the first anonymous type.</span></span> <span data-ttu-id="e687c-109">tuttavia, a causa della valutazione lazy, tale tecnica non è più onerosa in termini di potenza di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="e687c-109">However, because of lazy evaluation, doing so does not use much additional processing power.</span></span> <span data-ttu-id="e687c-110">L'idioma crea più oggetti temporanei sull'heap, ma senza influire sostanzialmente sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e687c-110">The idiom creates more short lived objects on the heap, but this does not substantially degrade performance.</span></span>  
  
 <span data-ttu-id="e687c-111">Sarebbe naturalmente possibile scrivere una singola query che contiene la funzionalità per recuperare i paragrafi, nonché lo stile e il testo di ogni paragrafo.</span><span class="sxs-lookup"><span data-stu-id="e687c-111">Of course, it would be possible to write a single query that contains the functionality to retrieve the paragraphs, the style of each paragraph, and the text of each paragraph.</span></span> <span data-ttu-id="e687c-112">Tuttavia, è spesso utile suddividere una query più complessa in più query perché il codice risultante è più modulare e più facilmente gestibile.</span><span class="sxs-lookup"><span data-stu-id="e687c-112">However, it often is useful to break up a more complicated query into multiple queries because the resulting code is more modular and easier to maintain.</span></span> <span data-ttu-id="e687c-113">Se inoltre è necessario riutilizzare parte della query, risulta più agevole effettuare il refactoring se le query sono scritte in questo modo.</span><span class="sxs-lookup"><span data-stu-id="e687c-113">Furthermore, if you need to reuse a portion of the query, it is easier to refactor if the queries are written in this manner.</span></span>  
  
 <span data-ttu-id="e687c-114">Queste query, che vengono concatenate insieme, usano il modello di elaborazione esaminato in dettaglio nell'argomento [esercitazione: esecuzione posticipata (Visual Basic)](tutorial-deferred-execution.md).</span><span class="sxs-lookup"><span data-stu-id="e687c-114">These queries, which are chained together, use the processing model that is examined in detail in the topic [Tutorial: Deferred Execution (Visual Basic)](tutorial-deferred-execution.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="e687c-115">Esempio</span><span class="sxs-lookup"><span data-stu-id="e687c-115">Example</span></span>  
 <span data-ttu-id="e687c-116">In questo esempio viene elaborato un documento WordprocessingML, determinando il nodo dell'elemento, il nome dello stile e il testo di ciascun paragrafo.</span><span class="sxs-lookup"><span data-stu-id="e687c-116">This example processes a WordprocessingML document, determining the element node, the style name, and the text of each paragraph.</span></span> <span data-ttu-id="e687c-117">Questo esempio si basa su esempi precedenti di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e687c-117">This example builds on the previous examples in this tutorial.</span></span> <span data-ttu-id="e687c-118">La nuova query è indicata nei commenti del codice riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e687c-118">The new query is called out in comments in the code below.</span></span>  
  
 <span data-ttu-id="e687c-119">Per istruzioni sulla creazione del documento di origine per questo esempio, vedere [creazione del documento Office Open XML di origine (Visual Basic)](creating-the-source-office-open-xml-document.md).</span><span class="sxs-lookup"><span data-stu-id="e687c-119">For instructions for creating the source document for this example, see [Creating the Source Office Open XML Document (Visual Basic)](creating-the-source-office-open-xml-document.md).</span></span>  
  
 <span data-ttu-id="e687c-120">In questo esempio vengono usate classi dell'assembly WindowsBase</span><span class="sxs-lookup"><span data-stu-id="e687c-120">This example uses classes from the WindowsBase assembly.</span></span> <span data-ttu-id="e687c-121">e i tipi dello spazio dei nomi <xref:System.IO.Packaging?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="e687c-121">It uses types in the <xref:System.IO.Packaging?displayProperty=nameWithType> namespace.</span></span>  
  
```vb  
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">  
  
Module Module1  
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
                If (styleRelation IsNot Nothing) Then  
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
  
        ' Following is the new query that retrieves the text of  
        ' each paragraph.  
        Dim paraWithText = _  
            From para In paragraphs _  
            Select New With { _  
                .ParagraphNode = para.ParagraphNode, _  
                .StyleName = para.StyleName, _  
                .Text = para.ParagraphNode.<w:r>.<w:t> _  
                    .Aggregate(New StringBuilder(), _  
                               Function(s As StringBuilder, i As String) s.Append(CStr(i)), _  
                               Function(s As StringBuilder) s.ToString) _  
            }  
  
        For Each p In paraWithText  
            Console.WriteLine("StyleName:{0} >{1}<", p.StyleName, p.Text)  
        Next  
  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="e687c-122">Questo esempio produce l'output seguente quando viene applicato al documento descritto in [creazione del documento Office Open XML di origine (Visual Basic)](creating-the-source-office-open-xml-document.md).</span><span class="sxs-lookup"><span data-stu-id="e687c-122">This example produces the following output when applied to the document described in [Creating the Source Office Open XML Document (Visual Basic)](creating-the-source-office-open-xml-document.md).</span></span>  
  
```console  
StyleName:Heading1 >Parsing WordprocessingML with LINQ to XML<  
StyleName:Normal ><  
StyleName:Normal >The following example prints to the console.<  
StyleName:Normal ><  
StyleName:Code >Imports System<  
StyleName:Code ><  
StyleName:Code >Class Program<  
StyleName:Code >    Public Shared  Sub Main(ByVal args() As String)<  
StyleName:Code >        Console.WriteLine("Hello World")<  
StyleName:Code >   End Sub<  
StyleName:Code >End Class<  
StyleName:Normal ><  
StyleName:Normal >This example produces the following output:<  
StyleName:Normal ><  
StyleName:Code >Hello World<  
```  
  
## <a name="next-steps"></a><span data-ttu-id="e687c-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e687c-123">Next Steps</span></span>  
 <span data-ttu-id="e687c-124">Nell'esempio successivo viene illustrato come usare un metodo di estensione, anziché <xref:System.Linq.Enumerable.Aggregate%2A>, per concatenare più stringhe in un'unica stringa.</span><span class="sxs-lookup"><span data-stu-id="e687c-124">The next example shows how to use an extension method, instead of <xref:System.Linq.Enumerable.Aggregate%2A>, to concatenate multiple strings into a single string.</span></span>  
  
- [<span data-ttu-id="e687c-125">Refactoring tramite un metodo di estensione (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e687c-125">Refactoring Using an Extension Method (Visual Basic)</span></span>](refactoring-using-an-extension-method.md)  
  
## <a name="see-also"></a><span data-ttu-id="e687c-126">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e687c-126">See also</span></span>

- [<span data-ttu-id="e687c-127">Esercitazione: modifica del contenuto in un documento WordprocessingML (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e687c-127">Tutorial: Manipulating Content in a WordprocessingML Document (Visual Basic)</span></span>](tutorial-manipulating-content-in-a-wordprocessingml-document.md)
- [<span data-ttu-id="e687c-128">Esecuzione posticipata e valutazione lazy in LINQ to XML (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e687c-128">Deferred Execution and Lazy Evaluation in LINQ to XML (Visual Basic)</span></span>](deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)

---
title: Esempio che genera parti di documento Office Open XML
ms.date: 07/20/2015
ms.assetid: a951925b-c985-48ed-b215-2a68b58f1ae5
ms.openlocfilehash: f374967ec633dcb0dd0fab3ac77de669c65a219c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84375187"
---
# <a name="example-that-outputs-office-open-xml-document-parts-visual-basic"></a>Esempio che genera parti di documento Office Open XML (Visual Basic)
In questo argomento viene illustrato come aprire un documento Office Open XML e accedere a parti del documento.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene aperto un documento Office Open XML e le parti relative al documento e allo stile vengono visualizzate nella console.  
  
 In questo esempio vengono usate classi dell'assembly WindowsBase e i tipi dello spazio dei nomi <xref:System.IO.Packaging?displayProperty=nameWithType>.  
  
```vb  
Const fileName As String = "SampleDoc.docx"  
  
Const documentRelationshipType As String = _  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"  
Const stylesRelationshipType As String = _  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles"  
Const wordmlNamespace As String = _  
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
Dim w As XNamespace = wordmlNamespace  
  
Using wdPackage As Package = Package.Open(fileName, FileMode.Open, FileAccess.Read)  
    Dim docPackageRelationship As PackageRelationship = _  
      wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault()  
    If docPackageRelationship IsNot Nothing Then  
        Dim documentUri As Uri = PackUriHelper.ResolvePartUri(New Uri("/", UriKind.Relative), _  
          docPackageRelationship.TargetUri)  
        Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)  
  
        ' Load the document XML in the part into an XDocument instance.  
        Dim xdoc As XDocument = XDocument.Load(XmlReader.Create(documentPart.GetStream()))  
  
        Console.WriteLine("TargetUri:{0}", docPackageRelationship.TargetUri)  
        Console.WriteLine("==================================================================")  
        Console.WriteLine(xdoc.Root)  
        Console.WriteLine()  
  
        ' Find the styles part. There will only be one.  
        Dim styleRelation As PackageRelationship = _  
          documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()  
        If styleRelation IsNot Nothing Then  
            Dim styleUri As Uri = _  
              PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)  
            Dim stylePart As PackagePart = wdPackage.GetPart(styleUri)  
  
            ' Load the style XML in the part into an XDocument instance.  
            Dim styleDoc As XDocument = XDocument.Load(XmlReader.Create(stylePart.GetStream()))  
  
            Console.WriteLine("TargetUri:{0}", styleRelation.TargetUri)  
            Console.WriteLine("==================================================================")  
            Console.WriteLine(styleDoc.Root)  
            Console.WriteLine()  
        End If  
    End If  
End Using  
```  
  
## <a name="see-also"></a>Vedere anche

- [Informazioni dettagliate sui documenti WordprocessingML di Office Open XML (Visual Basic)](details-of-office-open-xml-wordprocessingml-documents.md)

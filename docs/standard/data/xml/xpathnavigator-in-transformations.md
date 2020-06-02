---
title: XPathNavigator nelle trasformazioni
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 118f97d1-7110-4d1b-b0bd-4143252c0bb0
ms.openlocfilehash: 59fb399d80e1d4d33d1a3c659d2ff74a37fd367d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84282818"
---
# <a name="xpathnavigator-in-transformations"></a>XPathNavigator nelle trasformazioni
La classe <xref:System.Xml.XPath.XPathNavigator> fornisce un accesso casuale di sola lettura ai dati ed è progettata per essere usata come input per XSLT (Extensible Stylesheet Language for Transformations). Viene implementata su <xref:System.Xml.XPath.XPathDocument>, <xref:System.Xml.XmlDataDocument> e <xref:System.Xml.XmlDocument>. <xref:System.Xml.XPath.XPathNavigator> è basato sul modello di dati W3C (World Wide Web Consortium) secondo la descrizione fornita nella sezione 5 della raccomandazione XML Path Language (XPath) (informazioni in lingua inglese).  
  
 <xref:System.Xml.XPath.XPathNavigator> definisce un modello di cursore per qualsiasi archivio e fornisce query XPath rapide e di sola lettura per qualsiasi archivio dati. <xref:System.Xml.XPath.XPathNavigator> è inoltre la classe da usare per l'esecuzione di iterazioni sui frammenti di albero risultato.  
  
 L'API consente di ottenere informazioni dal nodo corrente nell'archivio e di spostare i nodi collegati. <xref:System.Xml.XPath.XPathNavigator> è un modello di tipo cursore che esegue l'attraversamento di un archivio usando un set di metodi **Move**. <xref:System.Xml.XPath.XPathNavigator> viene sempre posizionato su un nodo. Qualsiasi metodo **Move** che abbia esito negativo lascia <xref:System.Xml.XPath.XPathNavigator> invariato.  
  
 <xref:System.Xml.XPath.XPathNavigator> è la classe da usare per l'esecuzione di iterazioni sui frammenti di albero risultato. Nell'esempio di codice seguente viene illustrata la creazione di un frammento di albero risultato all'interno di un foglio di stile, chiamando la funzione con il parametro, `fragment`, che contiene l'XML  
  
## <a name="testxsl"></a>test.xsl  
  
```xml  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
                xmlns:msxsl ="urn:schemas-microsoft-com:xslt"  
                xmlns:user="http://www.adventure-works.com"  
                version="1.0">  
  
<xsl:variable name="fragment">  
    <authorlist>  
       <author>Joe</author>  
    </authorlist>  
</xsl:variable>  
  
<msxsl:script language="C#" implements-prefix="user">  
<![CDATA[  
   string NodeFragment(XPathNavigator nav)  
   {  
      if (nav.HasChildren)  
        return nav.Value;  
      else  
        return "";  
   }  
]]>  
</msxsl:script>  
  
<xsl:template match="/">  
     <xsl:value-of select="user:NodeFragment($fragment)"/>  
</xsl:template>  
  
</xsl:stylesheet>  
```  
  
## <a name="testxml"></a>test.xml  
  
```xml  
<root>Some text</root>  
```  
  
 Nell'esempio seguente vengono usati il foglio di stile **test.xsl** e i dati di input **test.xml**.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Xsl  
Imports System.Xml.XPath  
Imports System.Text  
Public Class sample  
  
    Public Shared Sub Main()  
        Dim xslt As New XslTransform()  
        xslt.Load("test.xsl")  
  
        Dim xd As New XPathDocument("test.xml")  
  
        Dim strmTemp = New FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite)  
        xslt.Transform(xd, Nothing, strmTemp, Nothing)  
    End Sub 'Main  
End Class 'sample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Xsl;  
using System.Xml.XPath;  
using System.Text;  
  
public class sample  
{  
    public static void Main()  
    {  
        XslTransform xslt = new XslTransform();  
        xslt.Load("test.xsl");  
  
        XPathDocument xd = new XPathDocument("test.xml");  
  
        Stream strmTemp = new FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite);  
        xslt.Transform(xd, null, strmTemp, null);  
    }  
}  
```  
  
## <a name="output"></a>Output  
 Il risultato della trasformazione è riportato nel file **out.xml**:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>Joe  
```  
  
## <a name="see-also"></a>Vedere anche

- [Implementazione del processore XSLT da parte della classe XslTransform](xsltransform-class-implements-the-xslt-processor.md)

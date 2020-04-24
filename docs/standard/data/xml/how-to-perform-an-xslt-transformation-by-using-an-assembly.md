---
title: 'Procedura: Eseguire una trasformazione XSLT con un assembly'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 76ee440b-d134-4f8f-8262-b917ad6dcbf6
ms.openlocfilehash: 447cf18c7a9d24addf9d0a4ad523f46a45a5d27a
ms.sourcegitcommit: 00aa62e2f469c2272a457b04e66b4cc3c97a800b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78155975"
---
# <a name="how-to-perform-an-xslt-transformation-by-using-an-assembly"></a><span data-ttu-id="a88fe-102">Procedura: Eseguire una trasformazione XSLT con un assembly</span><span class="sxs-lookup"><span data-stu-id="a88fe-102">How to: Perform an XSLT Transformation by Using an Assembly</span></span>
<span data-ttu-id="a88fe-103">Il compilatore XSLT (xsltc.exe) consente di compilare fogli di stile XSLT e di generare un assembly.</span><span class="sxs-lookup"><span data-stu-id="a88fe-103">The XSLT compiler (xsltc.exe) compiles XSLT style sheets and generates an assembly.</span></span> <span data-ttu-id="a88fe-104">L'assembly può essere passato direttamente nel metodo <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Type%29?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="a88fe-104">The assembly can be passed directly into the <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Type%29?displayProperty=nameWithType> method.</span></span>  
  
### <a name="to-copy-the-xml-and-xslt-files-to-your-local-computer"></a><span data-ttu-id="a88fe-105">Per copiare i file XML e XSLT nel computer locale</span><span class="sxs-lookup"><span data-stu-id="a88fe-105">To copy the XML and XSLT files to your local computer</span></span>  
  
- <span data-ttu-id="a88fe-106">Copiare il file XSLT nel computer locale e denominarlo Transform.xsl.</span><span class="sxs-lookup"><span data-stu-id="a88fe-106">Copy the XSLT file to your local computer and name it Transform.xsl.</span></span>  
  
    ```xml  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
      xmlns:msxsl="urn:schemas-microsoft-com:xslt"  
      xmlns:user="urn:my-scripts">  
      <msxsl:script language="C#" implements-prefix="user">  
        <![CDATA[  
      public string discount(string price){  
        char[] trimChars = { '$' };  
        //trim leading $, convert price to type double  
        double discount_value = Convert.ToDouble(price.TrimStart(trimChars));  
        //apply 10% discount and round appropriately  
        discount_value = .9*discount_value;  
        //convert value to decimal and format as currency  
        string discount_price = discount_value.ToString("C");  
        return discount_price;  
      }  
      ]]>  
      </msxsl:script>  
      <xsl:template match="catalog">  
        <html>  
          <head></head>  
          <body>  
            <table border="1">  
              <tr>  
                <th align="left">Title</th>  
                <th align="left">Author</th>  
                <th align="left">Genre</th>  
                <th align="left">Publish Date</th>  
                <th align="left">Price</th>  
              </tr>  
              <xsl:for-each select="book">  
                <tr>  
                  <td>  
                    <xsl:value-of select="title"/>  
                  </td>  
                  <td>  
                    <xsl:value-of select="author"/>  
                  </td>  
                  <td>  
                    <xsl:value-of select="genre"/>  
                  </td>  
                  <td>  
                    <xsl:value-of select="publish_date"/>  
                  </td>  
                  <xsl:choose>  
                    <xsl:when test="genre = 'Fantasy'">  
                      <td>  
                        <xsl:value-of select="user:discount(price)"/>  
                      </td>  
                    </xsl:when>  
                    <xsl:otherwise>  
                      <td>  
                        <xsl:value-of select="price"/>  
                      </td>  
                    </xsl:otherwise>  
                  </xsl:choose>  
                </tr>  
              </xsl:for-each>  
            </table>  
          </body>  
        </html>  
      </xsl:template>  
    </xsl:stylesheet>  
    ```  
  
- <span data-ttu-id="a88fe-107">Copiare il file XML nel computer locale e denominarlo `books.xml`.</span><span class="sxs-lookup"><span data-stu-id="a88fe-107">Copy the XML file to your local computer and name it `books.xml`.</span></span>  
  
    ```xml  
    <?xml version="1.0"?>  
    <catalog>  
       <book id="bk101">  
          <author>Gambardella, Matthew</author>  
          <title>XML Developer's Guide</title>  
          <genre>Computer</genre>  
          <price>$44.95</price>  
          <publish_date>2000-10-01</publish_date>  
       </book>  
       <book id="bk102">  
          <author>Ralls, Kim</author>  
          <title>Midnight Rain</title>  
          <genre>Fantasy</genre>  
          <price>$5.95</price>  
          <publish_date>2000-12-16</publish_date>  
       </book>  
       <book id="bk103">  
          <author>Corets, Eva</author>  
          <title>Maeve Ascendant</title>  
          <genre>Fantasy</genre>  
          <price>$5.95</price>  
          <publish_date>2000-11-17</publish_date>  
       </book>  
       <book id="bk106">  
          <author>Randall, Cynthia</author>  
          <title>Lover Birds</title>  
          <genre>Romance</genre>  
          <price>$4.95</price>  
          <publish_date>2000-09-02</publish_date>  
       </book>  
       <book id="bk107">  
          <author>Thurman, Paula</author>  
          <title>Splish Splash</title>  
          <genre>Romance</genre>  
          <price>$4.95</price>  
          <publish_date>2000-11-02</publish_date>  
       </book>  
    </catalog>  
    ```  
  
### <a name="to-compile-the-style-sheet-with-the-script-enabled"></a><span data-ttu-id="a88fe-108">Per compilare il foglio di stile con lo script abilitato.</span><span class="sxs-lookup"><span data-stu-id="a88fe-108">To compile the style sheet with the script enabled.</span></span>  
  
1. <span data-ttu-id="a88fe-109">Quando si esegue il comando seguente dalla riga di comando, vengono creati due assembly denominati `Transform.dll` e `Transform_Script1.dll`. Questo è il comportamento predefinito.</span><span class="sxs-lookup"><span data-stu-id="a88fe-109">Executing the following command from the command line creates two assemblies named `Transform.dll` and `Transform_Script1.dll` (This is the default behavior.</span></span> <span data-ttu-id="a88fe-110">Se non viene specificato diversamente, il nome della classe e il nome dell'assieme vengono impostati sul nome del foglio di stile principale.</span><span class="sxs-lookup"><span data-stu-id="a88fe-110">Unless otherwise specified, the name of the class and the assembly defaults to the name of the main style sheet):</span></span>  
  
    ```console  
    xsltc /settings:script+ Transform.xsl  
    ```
  
    <span data-ttu-id="a88fe-111">Il seguente comando consente di impostare in modo esplicito il nome della classe su Transform:</span><span class="sxs-lookup"><span data-stu-id="a88fe-111">The following command explicitly sets the class name to Transform:</span></span>  
  
    ```console  
    xsltc /settings:script+ /class:Transform Transform.xsl  
    ```  
  
### <a name="to-include-the-compiled-assembly-as-a-reference-when-you-compile-your-code"></a><span data-ttu-id="a88fe-112">Per includere l'assembly compilato come riferimento quando si compila il codice</span><span class="sxs-lookup"><span data-stu-id="a88fe-112">To include the compiled assembly as a reference when you compile your code.</span></span>  
  
1. <span data-ttu-id="a88fe-113">È possibile includere un assembly in Visual Studio aggiungendo un riferimento in Esplora soluzioni o dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a88fe-113">You can include an assembly in Visual Studio by adding a reference in the Solution Explorer, or from the command line.</span></span>  
  
2. <span data-ttu-id="a88fe-114">Per la riga di comando con C#, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a88fe-114">For the command line with C#, use the following:</span></span>  
  
    ```console  
    csc myCode.cs /r:system.dll;system.xml.dll;Transform.dll  
    ```  
  
3. <span data-ttu-id="a88fe-115">Per la riga di comando con Visual Basic, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a88fe-115">For the command line with Visual Basic, use the following</span></span>  
  
    ```console  
    vbc myCode.vb /r:system.dll;system.xml.dll;Transform.dll  
    ```  
  
### <a name="to-use-the-compiled-assembly-in-your-code"></a><span data-ttu-id="a88fe-116">Per usare l'assembly compilato nel codice</span><span class="sxs-lookup"><span data-stu-id="a88fe-116">To use the compiled assembly in your code.</span></span>  
  
<span data-ttu-id="a88fe-117">Nell'esempio seguente viene illustrato come eseguire la trasformazione XSLT usando il foglio di stile compilato.</span><span class="sxs-lookup"><span data-stu-id="a88fe-117">The following example shows how to execute the XSLT transformation by using the compiled style sheet.</span></span>  
  
[!code-csharp[XslTransform_XSLTC#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XslTransform_XSLTC/CS/XslTransform_XSLTC.cs#1)]
[!code-vb[XslTransform_XSLTC#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslTransform_XSLTC/VB/XslTransform_XSLTC.vb#1)]  
  
<span data-ttu-id="a88fe-118">Per eseguire un collegamento dinamico all'assembly compilato, sostituire</span><span class="sxs-lookup"><span data-stu-id="a88fe-118">To dynamically link to the compiled assembly, replace</span></span>
  
```csharp  
xslt.Load(typeof(Transform));  
```  
  
<span data-ttu-id="a88fe-119">con</span><span class="sxs-lookup"><span data-stu-id="a88fe-119">with</span></span>  
  
```csharp
xslt.Load(System.Reflection.Assembly.Load("Transform").GetType("Transform"));  
```
  
<span data-ttu-id="a88fe-120">nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="a88fe-120">in the example above.</span></span> <span data-ttu-id="a88fe-121">Per ulteriori informazioni sul metodo assembly. Load, vedere <xref:System.Reflection.Assembly.Load%2A>.</span><span class="sxs-lookup"><span data-stu-id="a88fe-121">For more information on the Assembly.Load method, see <xref:System.Reflection.Assembly.Load%2A>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a88fe-122">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="a88fe-122">See also</span></span>

- <xref:System.Xml.Xsl.XslCompiledTransform>
- [<span data-ttu-id="a88fe-123">Compilatore XSLT (xsltc.exe)</span><span class="sxs-lookup"><span data-stu-id="a88fe-123">XSLT Compiler (xsltc.exe)</span></span>](../../../../docs/standard/data/xml/xslt-compiler-xsltc-exe.md)
- [<span data-ttu-id="a88fe-124">Trasformazioni XSLT</span><span class="sxs-lookup"><span data-stu-id="a88fe-124">XSLT Transformations</span></span>](../../../../docs/standard/data/xml/xslt-transformations.md)
- [<span data-ttu-id="a88fe-125">Compilazione dalla riga di comando con csc.exe</span><span class="sxs-lookup"><span data-stu-id="a88fe-125">Command-line Building With csc.exe</span></span>](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)

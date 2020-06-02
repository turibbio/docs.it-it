---
title: Supporto per la funzione msxsl:node-set()
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: d0cbf517-d9f6-4097-9851-4fa62903decd
ms.openlocfilehash: 747a0ff8c155f7635d5a6d2ebc76f287cf8646d4
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291448"
---
# <a name="support-for-the-msxslnode-set-function"></a><span data-ttu-id="b82a2-102">Supporto per la funzione msxsl:node-set()</span><span class="sxs-lookup"><span data-stu-id="b82a2-102">Support for the msxsl:node-set() Function</span></span>
<span data-ttu-id="b82a2-103">La funzione `msxsl:node-set` consente di convertire un frammento di albero risultato in un set di nodi.</span><span class="sxs-lookup"><span data-stu-id="b82a2-103">The `msxsl:node-set` function enables you to convert a result tree fragment into a node set.</span></span> <span data-ttu-id="b82a2-104">Il set di nodi risultante contiene sempre un nodo singolo ed è il nodo radice dell'albero.</span><span class="sxs-lookup"><span data-stu-id="b82a2-104">The resulting node set always contains a single node and is the root node of the tree.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b82a2-105">La classe <xref:System.Xml.Xsl.XslTransform> è obsoleta in .NET Framework 2.0.</span><span class="sxs-lookup"><span data-stu-id="b82a2-105">The <xref:System.Xml.Xsl.XslTransform> class is obsolete in the .NET Framework 2.0.</span></span> <span data-ttu-id="b82a2-106">È possibile eseguire le trasformazioni XSLT (Extensible Stylesheet Language for Transformations) usando la classe <xref:System.Xml.Xsl.XslCompiledTransform>.</span><span class="sxs-lookup"><span data-stu-id="b82a2-106">You can perform Extensible Stylesheet Language for Transformations (XSLT) transformations using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span> <span data-ttu-id="b82a2-107">Per altre informazioni, vedere [Utilizzo della classe XslCompiledTransform](using-the-xslcompiledtransform-class.md) e [Migrazione dalla classe XslTransform](migrating-from-the-xsltransform-class.md).</span><span class="sxs-lookup"><span data-stu-id="b82a2-107">See [Using the XslCompiledTransform Class](using-the-xslcompiledtransform-class.md) and [Migrating From the XslTransform Class](migrating-from-the-xsltransform-class.md) for more information.</span></span>  
  
 <span data-ttu-id="b82a2-108">La funzione `msxsl:node-set` consente di convertire un frammento di albero risultato in un set di nodi.</span><span class="sxs-lookup"><span data-stu-id="b82a2-108">The `msxsl:node-set` function enables you to convert a result tree fragment into a node set.</span></span> <span data-ttu-id="b82a2-109">Il set di nodi risultante contiene sempre un nodo singolo ed è il nodo radice dell'albero.</span><span class="sxs-lookup"><span data-stu-id="b82a2-109">The resulting node set always contains a single node and is the root node of the tree.</span></span>  
  
## <a name="example"></a><span data-ttu-id="b82a2-110">Esempio</span><span class="sxs-lookup"><span data-stu-id="b82a2-110">Example</span></span>  
 <span data-ttu-id="b82a2-111">Nell'esempio seguente `$var` è una variabile che rappresenta l'albero dei nodi del foglio di stile.</span><span class="sxs-lookup"><span data-stu-id="b82a2-111">In the following example, `$var` is a variable that is a node tree in the style sheet.</span></span> <span data-ttu-id="b82a2-112">L'istruzione for-each combinata con la funzione `node-set` consente all'utente di eseguire un'iterazione su questo albero come set di nodi.</span><span class="sxs-lookup"><span data-stu-id="b82a2-112">The for-each statement combined with the `node-set` function allows the user to iterate over this node tree as a node set.</span></span>  
  
## <a name="nodesetxsl"></a><span data-ttu-id="b82a2-113">nodeset.xsl</span><span class="sxs-lookup"><span data-stu-id="b82a2-113">nodeset.xsl</span></span>  
  
```xml  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"  
                xmlns:user="http://www.contoso.com"  
                version="1.0">  
    <xsl:variable name="books">  
        <book author="Michael Howard">Writing Secure Code</book>  
        <book author="Michael Kay">XSLT Reference</book>  
    </xsl:variable>  
  
    <xsl:template match="/">  
        <authors>  
            <xsl:for-each select="msxsl:node-set($books)/book">
                <author><xsl:value-of select="@author"/></author>  
            </xsl:for-each>  
        </authors>  
    </xsl:template>  
</xsl:stylesheet>  
```  
  
## <a name="output"></a><span data-ttu-id="b82a2-114">Output</span><span class="sxs-lookup"><span data-stu-id="b82a2-114">Output</span></span>  
 <span data-ttu-id="b82a2-115">Output della trasformazione:</span><span class="sxs-lookup"><span data-stu-id="b82a2-115">The output of the transformation is</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<authors><author>Michael Howard</author><author>Michael Kay</author></authors>  
```  
  
## <a name="see-also"></a><span data-ttu-id="b82a2-116">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b82a2-116">See also</span></span>

- [<span data-ttu-id="b82a2-117">Implementazione del processore XSLT da parte della classe XslTransform</span><span class="sxs-lookup"><span data-stu-id="b82a2-117">XslTransform Class Implements the XSLT Processor</span></span>](xsltransform-class-implements-the-xslt-processor.md)

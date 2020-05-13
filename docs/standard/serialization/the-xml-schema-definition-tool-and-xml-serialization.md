---
title: Strumento XML Schema Definition e serializzazione XML
description: Lo strumento XML Schema Definition genera file di classe C# o Visual Basic per uno schema XSD e genera una XML Schema da una libreria o da un file eseguibile.
ms.date: 03/30/2017
helpviewer_keywords:
- Xsd.exe
- XML serialization, XML Schema Definition tool
- XML Schema Definition tool
- serialization, XML Schema Definition tool
ms.assetid: 3c03f855-f931-47ff-bbc6-50c0367a16e4
ms.openlocfilehash: 258e66643dae64aec7280419911f5ac9193a2ada
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83380109"
---
# <a name="the-xml-schema-definition-tool-and-xml-serialization"></a><span data-ttu-id="2a7fe-103">Strumento XML Schema Definition e serializzazione XML</span><span class="sxs-lookup"><span data-stu-id="2a7fe-103">The XML Schema Definition Tool and XML Serialization</span></span>

<span data-ttu-id="2a7fe-104">Lo strumento XML Schema Definition ([xsd. exe)](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md)viene installato insieme agli strumenti .NET Framework come parte del &reg; Software Development Kit (SDK) di Windows.</span><span class="sxs-lookup"><span data-stu-id="2a7fe-104">The XML Schema Definition tool ([XML Schema Definition Tool (Xsd.exe)](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md)) is installed along with the .NET Framework tools as part of the Windows&reg; Software Development Kit (SDK).</span></span> <span data-ttu-id="2a7fe-105">Lo strumento è progettato principalmente per due scopi:</span><span class="sxs-lookup"><span data-stu-id="2a7fe-105">The tool is designed primarily for two purposes:</span></span>  
  
- <span data-ttu-id="2a7fe-106">Per generare file di classe C# o Visual Basic conformi a uno schema XML Schema Definition Language (XSD) specifico.</span><span class="sxs-lookup"><span data-stu-id="2a7fe-106">To generate either C# or Visual Basic class files that conform to a specific XML Schema definition language (XSD) schema.</span></span> <span data-ttu-id="2a7fe-107">Lo strumento prende uno schema XML come argomento e restituisce un file contenente un numero di classi che, se serializzate con <xref:System.Xml.Serialization.XmlSerializer>, risultano conformi allo schema.</span><span class="sxs-lookup"><span data-stu-id="2a7fe-107">The tool takes an XML Schema as an argument and outputs a file that contains a number of classes that, when serialized with the <xref:System.Xml.Serialization.XmlSerializer>, conform to the schema.</span></span> <span data-ttu-id="2a7fe-108">Per informazioni su come usare lo strumento per generare classi conformi a uno schema specifico, vedere [Procedura: Usare lo strumento XML Schema Definition per generare classi e documenti XML Schema](../../../docs/standard/serialization/xml-schema-def-tool-gen.md).</span><span class="sxs-lookup"><span data-stu-id="2a7fe-108">For information about how to use the tool to generate classes that conform to a specific schema, see [How to: Use the XML Schema Definition Tool to Generate Classes and XML Schema Documents](../../../docs/standard/serialization/xml-schema-def-tool-gen.md).</span></span>  
  
- <span data-ttu-id="2a7fe-109">Per generare un documento XML Schema da un file con estensione dll o exe.</span><span class="sxs-lookup"><span data-stu-id="2a7fe-109">To generate an XML Schema document from a .dll file or .exe file.</span></span> <span data-ttu-id="2a7fe-110">Per visualizzare lo schema di un set di file creati o di uno schema modificato con attributi, passare il file DLL o EXE come argomento allo strumento per generare l'XML Schema.</span><span class="sxs-lookup"><span data-stu-id="2a7fe-110">To see the schema of a set of files that you have either created or one that has been modified with attributes, pass the DLL or EXE as an argument to the tool to generate the XML schema.</span></span> <span data-ttu-id="2a7fe-111">Per informazioni su come usare lo strumento per generare un documento XML Schema da un set di classi, vedere [Procedura: Usare lo strumento XML Schema Definition per generare classi e documenti XML Schema](../../../docs/standard/serialization/xml-schema-def-tool-gen.md).</span><span class="sxs-lookup"><span data-stu-id="2a7fe-111">For information about how to use the tool to generate an XML Schema Document from a set of classes, see [How to: Use the XML Schema Definition Tool to Generate Classes and XML Schema Documents](../../../docs/standard/serialization/xml-schema-def-tool-gen.md).</span></span>  
  
<span data-ttu-id="2a7fe-112">Per ulteriori informazioni sull'utilizzo dello strumento, vedere [strumento XML Schema Definition (XSD. exe)](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md).</span><span class="sxs-lookup"><span data-stu-id="2a7fe-112">For more information about using the tool, see [XML Schema Definition Tool (Xsd.exe)](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2a7fe-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2a7fe-113">See also</span></span>

- <xref:System.Data.DataSet>
- [<span data-ttu-id="2a7fe-114">Introduzione alla serializzazione XML</span><span class="sxs-lookup"><span data-stu-id="2a7fe-114">Introducing XML Serialization</span></span>](../../../docs/standard/serialization/introducing-xml-serialization.md)
- [<span data-ttu-id="2a7fe-115">Strumento XML Schema Definition (XSD. exe)</span><span class="sxs-lookup"><span data-stu-id="2a7fe-115">XML Schema Definition Tool (Xsd.exe)</span></span>](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [<span data-ttu-id="2a7fe-116">Procedura: serializzare un oggetto</span><span class="sxs-lookup"><span data-stu-id="2a7fe-116">How to: Serialize an Object</span></span>](../../../docs/standard/serialization/how-to-serialize-an-object.md)
- [<span data-ttu-id="2a7fe-117">Procedura: Deserializzare un oggetto</span><span class="sxs-lookup"><span data-stu-id="2a7fe-117">How to: Deserialize an Object</span></span>](../../../docs/standard/serialization/how-to-deserialize-an-object.md)
- [<span data-ttu-id="2a7fe-118">Procedura: utilizzare lo strumento XML Schema Definition per generare classi e documenti di XML Schema.</span><span class="sxs-lookup"><span data-stu-id="2a7fe-118">How to: Use the XML Schema Definition Tool to Generate Classes and XML Schema Documents</span></span>](../../../docs/standard/serialization/xml-schema-def-tool-gen.md)
- <span data-ttu-id="2a7fe-119">[Supporto dell'associazione all'XML Schema](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sh1e66zd(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="2a7fe-119">[XML Schema Binding Support](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sh1e66zd(v=vs.100))</span></span>

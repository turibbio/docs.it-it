---
title: <schemaImporterExtensions> Elemento
ms.date: 03/30/2017
helpviewer_keywords:
- XML serialization, configuration
- schemaImporterExtensions element
- <schemaImporterExtensions> element
ms.assetid: 465ef2a0-f909-4ac1-9a56-0ead5c849698
ms.openlocfilehash: 5ed80ac370e34d6b62bb2b601cb7bd978228a302
ms.sourcegitcommit: 00aa62e2f469c2272a457b04e66b4cc3c97a800b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78159819"
---
# <a name="schemaimporterextensions-element"></a><span data-ttu-id="780fe-102">\<Elemento schemaImporterExtensions></span><span class="sxs-lookup"><span data-stu-id="780fe-102">\<schemaImporterExtensions> Element</span></span>
<span data-ttu-id="780fe-103">Contiene tipi utilizzati da <xref:System.Xml.Serialization.XmlSchemaImporter> per l'esecuzione del mapping dei tipi XSD ai tipi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="780fe-103">Contains types that are used by the <xref:System.Xml.Serialization.XmlSchemaImporter> for mapping of XSD types to .NET Framework types.</span></span> <span data-ttu-id="780fe-104">Per altre informazioni sui file di configurazione, vedere [Schema dei file di configurazione](../../../docs/framework/configure-apps/file-schema/index.md).</span><span class="sxs-lookup"><span data-stu-id="780fe-104">For more information about configuration files, see [Configuration File Schema](../../../docs/framework/configure-apps/file-schema/index.md).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="780fe-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="780fe-105">Syntax</span></span>  
  
```xml  
<schemaImporterExtensions>  
    <!-- Add types -->  
</schemaImporterExtensions>  
```  
  
## <a name="child-elements"></a><span data-ttu-id="780fe-106">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="780fe-106">Child Elements</span></span>  
  
|<span data-ttu-id="780fe-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="780fe-107">Element</span></span>|<span data-ttu-id="780fe-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="780fe-108">Description</span></span>|  
|-------------|-----------------|  
|[<span data-ttu-id="780fe-109">\<aggiungere> elemento per \<schemaImporterExtensions></span><span class="sxs-lookup"><span data-stu-id="780fe-109">\<add> Element for \<schemaImporterExtensions></span></span>](../../../docs/standard/serialization/add-element-for-schemaimporterextensions.md)|<span data-ttu-id="780fe-110">Aggiunge tipi usati da <xref:System.Xml.Serialization.XmlSchemaImporter> per creare i mapping.</span><span class="sxs-lookup"><span data-stu-id="780fe-110">Adds types that are used by the <xref:System.Xml.Serialization.XmlSchemaImporter> to create mappings.</span></span>|  
  
## <a name="parent-elements"></a><span data-ttu-id="780fe-111">Elementi padre</span><span class="sxs-lookup"><span data-stu-id="780fe-111">Parent Elements</span></span>  
  
|<span data-ttu-id="780fe-112">Elemento</span><span class="sxs-lookup"><span data-stu-id="780fe-112">Element</span></span>|<span data-ttu-id="780fe-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="780fe-113">Description</span></span>|  
|-------------|-----------------|  
|[<span data-ttu-id="780fe-114">\<System. XML. Serialization> elemento</span><span class="sxs-lookup"><span data-stu-id="780fe-114">\<system.xml.serialization> Element</span></span>](../../../docs/standard/serialization/system-xml-serialization-element.md)|<span data-ttu-id="780fe-115">L'elemento di primo livello per il controllo della serializzazione XML.</span><span class="sxs-lookup"><span data-stu-id="780fe-115">The top-level element for controlling XML serialization.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="780fe-116">Esempio</span><span class="sxs-lookup"><span data-stu-id="780fe-116">Example</span></span>  
 <span data-ttu-id="780fe-117">Nell'esempio di codice riportato di seguito viene illustrato come aggiungere tipi utilizzati da <xref:System.Xml.Serialization.XmlSchemaImporter> in caso di esecuzione del mapping di tipi XSD ai tipi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="780fe-117">The following code example illustrates how to add types that are used by the <xref:System.Xml.Serialization.XmlSchemaImporter> when mapping XSD types to .NET Framework types.</span></span>  
  
```xml  
<system.xml.serialization>  
    <schemaImporterExtensions>  
        <add name = "MobileCapabilities" type =
        "System.Web.Mobile.MobileCapabilities,
        System.Web.Mobile, Version - 2.0.0.0, Culture = neutral,
        PublicKeyToken = b03f5f6f11d40a3a" />  
    </schemaImporterExtensions>  
</system.xml.serialization>  
```  
  
## <a name="see-also"></a><span data-ttu-id="780fe-118">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="780fe-118">See also</span></span>

- <xref:System.Xml.Serialization.XmlSchemaImporter>
- <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>
- [<span data-ttu-id="780fe-119">Schema del file di configurazione</span><span class="sxs-lookup"><span data-stu-id="780fe-119">Configuration File Schema</span></span>](../../../docs/framework/configure-apps/file-schema/index.md)
- [<span data-ttu-id="780fe-120">\<Elemento> dateTimeSerialization</span><span class="sxs-lookup"><span data-stu-id="780fe-120">\<dateTimeSerialization> Element</span></span>](../../../docs/standard/serialization/datetimeserialization-element.md)
- [<span data-ttu-id="780fe-121">\<aggiungere> elemento per \<schemaImporterExtensions></span><span class="sxs-lookup"><span data-stu-id="780fe-121">\<add> Element for \<schemaImporterExtensions></span></span>](../../../docs/standard/serialization/add-element-for-schemaimporterextensions.md)
- [<span data-ttu-id="780fe-122">\<System. XML. Serialization> elemento</span><span class="sxs-lookup"><span data-stu-id="780fe-122">\<system.xml.serialization> Element</span></span>](../../../docs/standard/serialization/system-xml-serialization-element.md)

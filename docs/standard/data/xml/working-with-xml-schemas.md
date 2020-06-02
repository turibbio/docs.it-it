---
title: Utilizzo di schemi XML
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: bbbcc70c-bf9a-4f6a-af72-1bab5384a187
ms.openlocfilehash: f239d67d959c1f7a0bfebfaaaa49de9cf9c9a111
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84281687"
---
# <a name="working-with-xml-schemas"></a>Utilizzo di schemi XML
Per definire la struttura di un documento XML, oltre alle relazioni dei suoi elementi, i tipi di dati e i vincoli di contenuto, si usa una DTD (Document Type Definition, definizione del tipo di documento) o uno schema XSD (XML Schema Definition Language). Sebbene un documento XML venga considerato in formato corretto se soddisfa tutti i requisiti sintattici definiti dalla raccomandazione W3C (World Wide Web Consortium) Extensible Markup Language (XML) 1.0, non viene ritenuto valido a meno che non sia in formato corretto e conforme ai vincoli definiti dalla relativa DTD o dal relativo schema. Pertanto, anche se tutti i documenti XML validi sono in formato corretto, non tutti i documenti XML in formato corretto sono validi.  
  
 Per altre informazioni su XML, vedere [W3C XML 1.0 Recommendation](https://www.w3.org/TR/REC-xml/) (Consigli su W3C XML 1.0). Per altre informazioni sullo schema XML, vedere i consigli in [W3C XML Schema Part 1: Structures Recommendation](https://www.w3.org/TR/xmlschema-1/) (Schema W3C XML, parte 1: consigli sulle strutture) e [W3C XML Schema Part 2: Datatypes Recommendation](https://www.w3.org/TR/xmlschema-2/) (Schema W3C XML, parte 2: consigli sui tipi di dati).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [SOM (Schema Object Model) XML](xml-schema-object-model-som.md)  
 Viene illustrato il modello SOM (Schema Object Model) nello spazio dei nomi <xref:System.Xml.Schema?displayProperty=nameWithType>, che fornisce un set di classi che consente di leggere lo schema XSD da un file oppure di creare a livello di codice uno schema in memoria.  
  
 [XmlSchemaSet per la compilazione di schemi](xmlschemaset-for-schema-compilation.md)  
 Viene illustrata la classe <xref:System.Xml.Schema.XmlSchemaSet>, ovvero una cache in cui possono essere archiviati e convalidati gli schemi XSD.  
  
 [Convalida basata sul metodo push di XmlSchemaValidator](xmlschemavalidator-push-based-validation.md)  
 Viene illustrata la classe <xref:System.Xml.Schema.XmlSchemaValidator> che fornisce un meccanismo efficiente e a elevate prestazioni per la convalida basata sul metodo push di dati XML in base a schemi XSD.  
  
 [Inferenza di uno schema XML](inferring-an-xml-schema.md)  
 Viene illustrato come usare la classe <xref:System.Xml.Schema.XmlSchemaInference> per inferire uno schema XSD dalla struttura di un documento XML.  
  
## <a name="reference"></a>Informazioni di riferimento  
 <xref:System.Xml.Schema.XmlSchemaSet> &#124; <xref:System.Xml.Schema.XmlSchemaInference> &#124; <xref:System.Xml.XmlReader>  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Convalida di un documento XML nel DOM](validating-an-xml-document-in-the-dom.md)  
 Viene illustrato come convalidare il documento XML nel DOM (Document Object Model). È possibile convalidare il documento XML quando viene caricato nel DOM oppure convalidare un documento non convalidato in precedenza nel DOM.  
  
 [Convalida dello schema con XPathNavigator](schema-validation-using-xpathnavigator.md)  
 Viene illustrato come convalidare il documento XML esplorato e modificato usando la classe <xref:System.Xml.XPath.XPathNavigator>.

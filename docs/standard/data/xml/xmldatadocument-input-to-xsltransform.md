---
title: Input di XmlDataDocument in XslTransform
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: a0b536b6-cdb3-4a44-86c2-3b2ebc7bd4c9
ms.openlocfilehash: 5f2a7ef22eb07bb221b6a145db4453996ad8bf8c
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/07/2020
ms.locfileid: "75709855"
---
# <a name="xmldatadocument-input-to-xsltransform"></a>Input di XmlDataDocument in XslTransform
> [!NOTE]
> La classe <xref:System.Xml.Xsl.XslTransform> è obsoleta in .NET Framework 2.0. È possibile eseguire le trasformazioni XSLT (Extensible Stylesheet Language for Transformations) usando la classe <xref:System.Xml.Xsl.XslCompiledTransform>. Per altre informazioni, vedere [Utilizzo della classe XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) e [Migrazione dalla classe XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md).  
  
 Microsoft .NET Framework implementa la specifica XML DOM (Document Object Model) per offrire l'accesso ai dati in documenti XML e classi aggiuntive per scrivere, leggere e spostarsi all'interno dei documenti XML. Il tipo <xref:System.Xml.XmlDataDocument>, che si trova nello spazio dei nomi <xref:System.Xml>, fornisce un accesso relazionale ai dati poiché è in grado di sincronizzarsi con i dati relazionali nel tipo <xref:System.Data.DataSet>. È possibile visualizzare e modificare simultaneamente l'XML strutturato tramite la rappresentazione relazionale del tipo <xref:System.Data.DataSet> oppure è possibile modificare l'XML semistrutturato tramite la rappresentazione DOM del tipo <xref:System.Xml.XmlDataDocument>. Il tipo <xref:System.Xml.XmlDataDocument> supera quindi i limiti dei modelli basati sui dati XML e relazionali.  
  
 Se i dati sono archiviati in una struttura relazionale, per immetterli in una trasformazione XSLT, è possibile caricare i dati relazionali in un tipo <xref:System.Data.DataSet> e associarli al tipo  <xref:System.Xml.XmlDataDocument>. Il tipo <xref:System.Xml.XPath.XPathNavigator>, l'input per il tipo <xref:System.Xml.Xsl.XslTransform>, è implementato in un tipo <xref:System.Xml.XmlDataDocument> tramite l'interfaccia <xref:System.Xml.XPath.IXPathNavigable>. Ora è possibile eseguire trasformazioni XSLT sui dati relazionali caricandoli in un tipo <xref:System.Data.DataSet> e usando la sincronizzazione all'interno del tipo <xref:System.Xml.XmlDataDocument>.  
  
 Per altre informazioni sull'applicazione di una trasformazione ai dati relazionali, vedere [Applicazione di una trasformazione XSLT a un DataSet](../../../../docs/framework/data/adonet/dataset-datatable-dataview/applying-an-xslt-transform-to-a-dataset.md).  
  
## <a name="see-also"></a>Vedi anche

- <xref:System.Xml.XmlDataDocument>
- [Sincronizzazione di DataSet e XmlDataDocument](../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataset-and-xmldatadocument-synchronization.md)
- [Trasformazioni XSLT con la classe XslTransform](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)
- [Implementazione del processore XSLT da parte della classe XslTransform](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)
- [XPathNavigator nelle trasformazioni](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)
- [XPathNodeIterator nelle trasformazioni](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)
- [Input di XPathDocument in XslTransform](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)
- [Input di XmlDocument in XslTransform](../../../../docs/standard/data/xml/xmldocument-input-to-xsltransform.md)

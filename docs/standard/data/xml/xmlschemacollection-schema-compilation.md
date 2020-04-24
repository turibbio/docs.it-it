---
title: Compilazione dello schema XmlSchemaCollection
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 76f28770-7126-428f-9ed5-7b5ae8bad5ee
ms.openlocfilehash: af6df3729f1bd926e9a47cc5b9d9bf460c8e1225
ms.sourcegitcommit: 00aa62e2f469c2272a457b04e66b4cc3c97a800b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78159286"
---
# <a name="xmlschemacollection-schema-compilation"></a>Compilazione dello schema XmlSchemaCollection
**XmlSchemaCollection** è una cache o una libreria in cui è possibile archiviare e convalidare gli schemi XDR (XML-Data Reduced) e XSD (XML Schema Definition Language). **XmlSchemaCollection** migliora le prestazioni memorizzando nella cache gli schemi anziché accedervi da un file o un URL.  
  
> [!NOTE]
> Sebbene la classe **XmlSchemaCollection** archivi sia schemi XDR che XML Schema, tutti i metodi e le proprietà che accettano o restituiscono un oggetto **XmlSchema** supportano solo gli XML Schema.  
  
> [!IMPORTANT]
> La classe <xref:System.Xml.Schema.XmlSchemaCollection> è obsoleta ed è stata sostituita dalla classe <xref:System.Xml.Schema.XmlSchemaSet>. Per altre informazioni sulla classe <xref:System.Xml.Schema.XmlSchemaSet>, vedere [XmlSchemaSet per la compilazione di schemi](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md).  
  
## <a name="add-schemas-to-the-collection"></a>Aggiunta di schemi alla raccolta  
 Gli schemi vengono caricati nella raccolta usando il metodo **Add** di **XmlSchemaCollection** e a ogni schema viene associato un URI dello spazio dei nomi. In genere, per gli XML Schema l'URI dello spazio dei nomi è lo spazio dei nomi di destinazione per lo schema. Per gli schemi XDR, invece, l'URI dello spazio dei nomi è lo spazio dei nomi specificato quando lo schema è stato aggiunto alla raccolta.  
  
## <a name="check-for-a-schema-in-the-collection"></a>Verifica di uno schema nella raccolta  
 È possibile verificare se uno schema è presente nella raccolta usando il metodo **Contains**, che **accetta** un oggetto **XmlSchema** (solo per XML Schema) o una stringa che rappresenta l'URI dello spazio dei nomi associato allo schema (per gli schemi XDR e XML Schema).  
  
## <a name="retrieve-a-schema-from-the-collection"></a>Recupero di uno schema dalla raccolta  
 È possibile recuperare uno schema dalla raccolta usando la proprietà **Item**. Tale **proprietà** accetta una stringa che rappresenta l'URI dello spazio dei nomi associato allo schema, in genere lo spazio dei nomi di destinazione corrispondente, e restituisce un oggetto **XmlSchema**. La proprietà **Item** si applica solo a XML Schema. Per gli schemi XDR, il valore restituito è sempre un riferimento null poiché questi non dispongono di un modello a oggetti.  
  
## <a name="validate-xml-documents-using-xmlschemacollection"></a>Convalida di documenti XML mediante XmlSchemaCollection  
 È possibile convalidare un documento di istanza XML tramite **XmlSchemaCollection** creando l'oggetto **XmlSchemaCollection**, aggiungendo gli schemi alla raccolta e impostando la proprietà **Schemas** su **XmlValidatingReader** per assegnare l'oggetto **XmlSchemaCollection** creato a **XmlValidatingReader**.  
  
### <a name="improved-performance"></a>Prestazioni migliorate  
 Si consiglia, se si convalida più di un documento rispetto allo stesso schema, di usare **XmlSchemaCollection** in quanto la memorizzazione degli schemi nella cache garantisce prestazioni migliori.  
  
 Nel seguente codice di esempio viene creato un oggetto **XmlSchemaCollection**, vengono aggiunti schemi alla raccolta e viene impostata la proprietà **Schemas**.  
  
```vb  
Dim tr as XmlTextReader = new XmlTextReader("Books.xml")  
Dim vr as XmlValidatingReader = new XmlValidatingReader(tr)  
Dim xsc as XmlSchemaCollection = new XmlSchemaCollection  
xsc.Add("urn:bookstore-schema", "Books.xsd")  
vr.Schemas.Add(xsc)  
```  
  
```csharp  
XmlTextReader tr = new XmlTextReader("Books.xml");  
XmlValidatingReader vr = new XmlValidatingReader(tr);  
XmlSchemaCollection xsc = new XmlSchemaCollection();  
xsc.Add("urn:bookstore-schema", "Books.xsd");
vr.Schemas.Add(xsc);  
```  
  
## <a name="see-also"></a>Vedi anche

- [Convalida XDR con XmlSchemaCollection](../../../../docs/standard/data/xml/xdr-validation-with-xmlschemacollection.md)
- [Convalida XSD (XML Schema) con XmlSchemaCollection](../../../../docs/standard/data/xml/xml-schema-xsd-validation-with-xmlschemacollection.md)

---
title: Note sull'implementazione del supporto per il tipo XML
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 26b071f3-1261-47ef-8690-0717f5cd93c1
ms.openlocfilehash: 91a685f122ff846217ea7a8677b29df430b65363
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290279"
---
# <a name="xml-type-support-implementation-notes"></a>Note sull'implementazione del supporto per il tipo XML
In questo argomento vengono descritti alcuni dettagli sull'implementazione di cui è consigliabile essere a conoscenza.  
  
## <a name="list-mappings"></a>Mapping degli elenchi  
 I tipi <xref:System.Collections.IList>, <xref:System.Collections.ICollection>, <xref:System.Collections.IEnumerable>, **Type[]** e <xref:System.String> vengono usati per rappresentare i tipi di elenco XSD (XML Schema definition language).  
  
## <a name="union-mappings"></a>Mapping delle unioni  
 I tipi di unione vengono rappresentati usando il tipo <xref:System.Xml.Schema.XmlAtomicValue> o <xref:System.String>. Pertanto, il tipo di origine o il tipo di destinazione devono sempre essere <xref:System.String> o <xref:System.Xml.Schema.XmlAtomicValue>.  
  
 Se l'oggetto <xref:System.Xml.Schema.XmlSchemaDatatype> rappresenta un tipo di elenco, tale oggetto converte il valore della stringa di input in un elenco di uno o più oggetti. Se l'oggetto <xref:System.Xml.Schema.XmlSchemaDatatype> rappresenta un tipo di unione, viene eseguito un tentativo di analisi del valore di input come tipo membro dell'unione. Se il tentativo di analisi non viene eseguito correttamente, viene tentata la conversione con il successivo membro dell'unione e così via fino a quando la conversione non viene eseguita correttamente o non sono disponibili altri tipi di membro con cui provare. In questo caso verrà generata un'eccezione.  
  
## <a name="differences-between-clr-and-xml-data-types"></a>Differenze tra i tipi di dati CLR e XML  
 Di seguito vengono descritte alcune corrispondenze errate che si possono verificare tra i tipi di dati CLR e i tipi di dati XML e la loro eventuale gestione.  
  
> [!NOTE]
> Il prefisso `xs` viene mappato in <https://www.w3.org/2001/XMLSchema> e nell'URI dello spazio dei nomi.
  
### <a name="systemtimespan-and-xsduration"></a>System.TimeSpan e xs:duration  
 Il tipo `xs:duration` è parzialmente ordinato, poiché alcuni valori di durata sono diversi ma equivalenti. Ciò significa che per il tipo `xs:duration` il valore di 1 mese (P1M) è minore di 32 giorni (P32D), maggiore di 27 giorni (P27D) ed equivalente a 28, 29 o 30 giorni.  
  
 La classe <xref:System.TimeSpan> non supporta questo ordinamento parziale. Invece, stabilisce un numero specifico di giorni per 1 anno e 1 mese: rispettivamente 365 e 30 giorni.  
  
 Per altre informazioni sul tipo `xs:duration`, vedere la raccomandazione W3C [XML Schema Part 2: Datatypes](https://www.w3.org/TR/xmlschema-2/) (Schema XML parte 2: tipi di dati).
  
### <a name="xstime-gregorian-date-types-and-systemdatetime"></a>xs:time, tipi di date gregoriane e System.DateTime  
 Quando un valore `xs:time` è associato a un oggetto <xref:System.DateTime>, il campo <xref:System.DateTime.MinValue> viene usato per inizializzare le proprietà relative alla data dell'oggetto <xref:System.DateTime> (ad esempio, <xref:System.DateTime.Year%2A>, <xref:System.DateTime.Month%2A> e <xref:System.DateTime.Day%2A>) impostandole sul valore <xref:System.DateTime> più basso possibile.  
  
 Allo stesso modo, anche istanze di `xs:gMonth`, `xs:gDay`, `xs:gYear`, `xs:gYearMonth` e `xs:gMonthDay` vengono associate a un oggetto <xref:System.DateTime>. Le proprietà inutilizzate nell'oggetto <xref:System.DateTime> vengono inizializzate impostandole su quelle da <xref:System.DateTime.MinValue>.  
  
> [!NOTE]
> Non è possibile usare il valore <xref:System.DateTime.Year%2A?displayProperty=nameWithType> quando il contenuto è tipizzato come `xs:gMonthDay`. In questo caso il valore <xref:System.DateTime.Year%2A?displayProperty=nameWithType> è sempre impostato su 1904.  
  
### <a name="xsanyuri-and-systemuri"></a>xs:anyURI e System.Uri  
 Quando un'istanza di `xs:anyURI` che rappresenta un URI relativo viene associata a un tipo <xref:System.Uri>, l'oggetto <xref:System.Uri> non dispone di un URI di base.  
  
## <a name="see-also"></a>Vedere anche

- [Supporto di tipi di dati nelle classi System.Xml](type-support-in-the-system-xml-classes.md)

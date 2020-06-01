---
title: Panoramica degli spazi dei nomi (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 16283322-8238-4918-ab11-802ac6748eb7
ms.openlocfilehash: 010d8661afe063c06f042084f6b320acb1235ac4
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241435"
---
# <a name="namespaces-overview-linq-to-xml"></a>Panoramica degli spazi dei nomi (LINQ to XML)

Questo argomento presenta gli spazi dei nomi, la classe <xref:System.Xml.Linq.XName> e la classe <xref:System.Xml.Linq.XNamespace>.

## <a name="xml-names"></a>Nomi XML

I nomi XML sono spesso causa di complessità nella programmazione XML. Un nome XML è composto da uno spazio dei nomi XML (detto anche URI dello spazio dei nomi XML) e da un nome locale. Uno spazio dei nomi XML è simile a uno spazio dei nomi in un programma .NET. Consente infatti di qualificare in modo univoco i nomi di elementi e attributi e quindi di evitare conflitti di nomi tra le diverse parti di un documento XML. Dopo aver dichiarato uno spazio dei nomi XML, è possibile selezionare un nome locale che deve essere univoco all'interno di tale spazio dei nomi.

Un'altra peculiarità dei nomi XML è costituita dai *prefissi di spazio dei nomi* XML. Sono i prefissi XML a costituire la causa di maggior complessità dei nomi XML. I prefissi consentono di creare un collegamento per uno spazio dei nomi XML al fine di rendere il documento XML più conciso e comprensibile. Tuttavia, il significato dei prefissi XML dipende dal contesto ed è proprio questo aspetto a renderli complessi. Ad esempio, è possibile associare il prefisso XML `aw` a un unico spazio dei nomi XML in un'unica parte di un albero XML e a uno spazio dei nomi XML diverso in una parte diversa dell'albero XML.

Uno dei vantaggi dell'uso di [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] con C# è che non è necessario usare prefissi XML. Quando [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] carica o analizza un documento XML, ogni prefisso XML viene risolto nello spazio dei nomi XML corrispondente. Successivamente, quando si opera su un documento che usa spazi dei nomi, si accede quasi sempre agli spazi dei nomi tramite l'URI dello spazio dei nomi e non tramite il prefisso. Quando gli sviluppatori usano nomi XML in [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)], usano sempre nomi XML completi, ovvero costituiti da uno spazio dei nomi XML e da un nome locale. Tuttavia, quando necessario, [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] consente di usare e controllare i prefissi degli spazi dei nomi.

In [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] la classe che rappresenta i nomi XML è <xref:System.Xml.Linq.XName>. I nomi XML vengono usati frequentemente in tutta l'API di [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]. Nei casi in cui è richiesto un nome XML, sarà presente un parametro <xref:System.Xml.Linq.XName>. Solo in casi rari, tuttavia, si usa direttamente un oggetto <xref:System.Xml.Linq.XName>. <xref:System.Xml.Linq.XName> contiene una conversione implicita da stringa.

Per altre informazioni, vedere <xref:System.Xml.Linq.XNamespace> e <xref:System.Xml.Linq.XName>.

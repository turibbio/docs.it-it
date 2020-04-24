---
title: Copia di nodi esistenti da un documento all'altro
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 3caa78c1-3448-4b7b-b83c-228ee857635e
ms.openlocfilehash: 4ee3f8d280b8bf0f2de067e7529d777e62bff406
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/07/2020
ms.locfileid: "75711025"
---
# <a name="copying-existing-nodes-from-one-document-to-another"></a>Copia di nodi esistenti da un documento all'altro
Il metodo **ImportNode** è il meccanismo con il quale un nodo o un intero sottoalbero di nodi viene copiato da un oggetto **XmlDocument** a un altro. Il nodo restituito dalla chiamata è una copia del nodo dal documento di origine, inclusi i valori degli attributi, il nome del nodo, il tipo di nodo e tutti gli attributi relativi allo spazio dei nomi quali il prefisso, il nome locale e l'URI dello spazio dei nomi. Il documento di origine non viene modificato. Dopo aver importato il nodo, è necessario aggiungerlo all'albero usando uno dei metodi di inserimento dei nodi.  
  
 Quando il nodo viene associato al documento nuovo, quest'ultimo possiede il nodo, perché ogni nodo, al momento della creazione, ha un documento che lo possiede, anche se i nodi vengono creati in frammenti di documento separati. Si tratta di un requisito del modello DOM (Document Object Model) XML e viene applicato dalla progettazione della creazione della factory per la classe **XmlDocument**. Ad esempio, **CreateElement** è l'unico metodo che consente di creare nuovi nodi.  
  
 A seconda del tipo di nodo del nodo importato e del valore del parametro *deep*, vengono copiate informazioni aggiuntive. Questo metodo tenta di rispecchiare il comportamento previsto nel caso in cui un frammento di codice XML o HTML sia stato copiato da un documento all'altro, tenendo conto del fatto che per il codice XML i due documenti potrebbero avere DTD diverse.  
  
 Nella tabella seguente viene descritto il comportamento specifico di ogni tipo di nodo che è possibile importare.  
  
|Tipo di nodo|Il parametro *deep* è true|Il parametro *deep* è false|  
|---------------|------------------------------|-------------------------------|  
|XmlAttribute|<xref:System.Xml.XmlAttribute.Specified%2A> è impostato su **true** in XmlAttribute. I discendenti dell'elemento **XmlAttribute** di origine vengono importati in modo ricorsivo e i nodi risultanti vengono riassemblati per formare il sottoalbero corrispondente.|Il parametro *deep* non è applicabile ai nodi **XmlAttribute**, perché questi restano sempre associati ai nodi figlio durante l'importazione.|  
|XmlCDataSection|Copia il nodo, compresi i dati.|Copia il nodo, compresi i dati.|  
|XmlComment|Copia il nodo, compresi i dati.|Copia il nodo, compresi i dati.|  
|XmlDocumentFragment|Gli elementi discendenti del nodo di origine vengono importati in modo ricorsivo e i nodi risultanti vengono riassemblati per formare il sottoalbero corrispondente.|Viene creato un **XmlDocumentFragment** vuoto.|  
|XmlDocumentType|Copia il nodo, compresi i dati.*|Copia il nodo, compresi i dati.*|  
|XmlElement|Gli elementi discendenti dell'elemento di origine vengono importati in modo ricorsivo e i nodi risultanti vengono riassemblati per formare il sottoalbero corrispondente. **Nota:** gli attributi predefiniti non vengono copiati. Se il documento verso il quale avviene l'importazione definisce attributi predefiniti per questo nome di elemento, verranno assegnati tali attributi.|I nodi Attribute specificati dell'elemento di origine vengono importati e i nodi **XmlAttribute** generati vengono associati al nuovo elemento. I nodi discendenti non vengono copiati. **Nota:** gli attributi predefiniti non vengono copiati. Se il documento verso il quale avviene l'importazione definisce attributi predefiniti per questo nome di elemento, verranno assegnati tali attributi.|  
|XmlEntityReference|Poiché nei documenti di origine e di destinazione le entità potrebbero essere definite in modo diverso, questo metodo copia solo il nodo **XmlEntityReference**. Il testo di sostituzione non viene incluso. Se nel documento di destinazione l'entità è definita, viene assegnato il suo valore.|Poiché nei documenti di origine e di destinazione le entità potrebbero essere definite in modo diverso, questo metodo copia solo il nodo **XmlEntityReference**. Il testo di sostituzione non viene incluso. Se nel documento di destinazione l'entità è definita, viene assegnato il suo valore.|  
|XmlProcessingInstruction|Copia il valore di destinazione e dei dati dal nodo importato.|Copia il valore di destinazione e dei dati dal nodo importato.|  
|XmlText|Copia il nodo, compresi i dati.|Copia il nodo, compresi i dati.|  
|XmlSignificantWhitespace|Copia il nodo, compresi i dati.|Copia il nodo, compresi i dati.|  
|XmlWhitespace|Copia il nodo, compresi i dati.|Copia il nodo, compresi i dati.|  
|XmlDeclaration|Copia il valore di destinazione e dei dati dal nodo importato.|Copia il valore di destinazione e dei dati dal nodo importato.|  
|Tutti gli altri tipi di nodo|Questi nodi non possono essere importati.|Questi nodi non possono essere importati.|  
  
> [!NOTE]
> Sebbene sia possibile importare nodi DocumentType, un documento può disporre di un unico DocumentType. Pertanto, una volta importato il tipo di documento, prima di inserirlo nell'albero è necessario verificare che non sia presente alcun tipo di documento nel documento stesso. Per informazioni sulla rimozione dei nodi, vedere [Rimozione di nodi, contenuto e valori da un documento XML](../../../../docs/standard/data/xml/removing-nodes-content-and-values-from-an-xml-document.md).  
  
## <a name="see-also"></a>Vedi anche

- [XML DOM (Document Object Model)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)

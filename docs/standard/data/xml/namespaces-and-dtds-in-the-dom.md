---
title: Spazi dei nomi e DTD nel DOM (Document Object Model)
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 1e9b55c4-76ad-4f54-8d96-7ce4b4cf1e05
ms.openlocfilehash: 22762e3a7003d9b28a53c7b500829aaa41924c6d
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/07/2020
ms.locfileid: "75710596"
---
# <a name="namespaces-and-dtds-in-the-dom"></a>Spazi dei nomi e DTD nel DOM (Document Object Model)
Le DTD (Document Type Definition) rendono più complicato il supporto dello spazio dei nomi. Ad esempio, nel seguente codice XML sono presenti attributi predefiniti contenenti due punti nei nomi.  
  
```xml  
<!ATTLIST item x:id CDATA #IMPLIED>  
```  
  
 Di seguito sono riportate le possibili risoluzioni se il costrutto è consentito:  
  
- Il codice `x:` viene considerato come prefisso dello spazio dei nomi, ma il prefisso deve essere risolvibile usando una dichiarazione dello spazio dei nomi `xmlns:x`, che deve inoltre essere presente nella DTD. Il mapping di questo prefisso non deve essere eseguito a un elemento diverso nel documento dell'istanza.  
  
- Il codice `x:` viene considerato come prefisso dello spazio dei nomi, ma tale prefisso è sempre risolto nel contesto degli elementi dell'istanza. È pertanto possibile eseguire il mapping del prefisso a URI (Uniform Resource Identifier) diversi dello spazio dei nomi, in base all'ambito dello spazio dei nomi in cui è presente l'elemento `item`. Questo comportamento è più prevedibile rispetto alla risoluzione fornita nel punto elenco precedente, ma presenta altre implicazioni complesse poiché richiede che gli attributi predefiniti vengano materializzati.  
  
- I due punti vengono ignorati in quanto si trovano in una DTD e il nome dell'attributo è `x:y`, senza prefisso e URI dello spazio dei nomi.  
  
- I due punti nell'attributo predefinito generano un'eccezione, per indicare che i due punti nei nomi all'interno di una DTD non sono supportati. Il comportamento è prevedibile, ma implica che non sarà possibile caricare molte delle DTD pubblicate dal W3C (World Wide Web Consortium).  
  
- Quando l'utente richiede la convalida della DTD, il supporto per lo spazio dei nomi viene disattivato per l'intero documento. In tal modo è possibile caricare le DTD W3C e ottenere un comportamento prevedibile.  
  
 Il codice XML in Microsoft .NET Framework implementa la seconda opzione per garantire la massima compatibilità con le specifiche W3C.  
  
## <a name="see-also"></a>Vedi anche

- [XML DOM (Document Object Model)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)

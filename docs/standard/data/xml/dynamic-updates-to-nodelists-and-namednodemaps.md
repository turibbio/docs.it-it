---
title: Aggiornamenti dinamici di NodeLists e NamedNodeMaps
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 76c511fd-6704-4ca4-8078-860a68d898ad
ms.openlocfilehash: 0199f24e9ef8dd28f91976edd50f78399dc893ef
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84292085"
---
# <a name="dynamic-updates-to-nodelists-and-namednodemaps"></a>Aggiornamenti dinamici di NodeLists e NamedNodeMaps
Poiché in **XmlNodeList** e **XmlNamedNodeMap** è contenuto un set di nodi e il documento XML è già stato caricato in memoria e sottoposto a modifiche, il W3C (World Wide Web Consortium) stabilisce che questi oggetti contenenti set di nodi debbano essere dinamici. Vale a dire che, se il documento sottostante cambia, anche i dati di questi due oggetti cambiano di conseguenza. Se quindi un **XmlNodeList** contiene tutti gli elementi figlio di un particolare elemento (ad esempio l'elemento X), si aggiunge un ulteriore elemento, l'elemento Q, al documento sotto l'elemento X. Nell'elenco **XmlNodeList** deve essere disponibile anche il nuovo elemento Q aggiunto alla raccolta. Lo stesso vale per il contrario. Se si aggiunge un nodo a **XmlNodeList**, il documento sottostante viene anch'esso aggiornato.  
  
## <a name="see-also"></a>Vedere anche

- [XML DOM (Document Object Model)](xml-document-object-model-dom.md)

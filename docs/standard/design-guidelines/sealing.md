---
title: sealed
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- limiting extensibility
- classes [.NET Framework], sealing
- preventing customization
- sealed classes
ms.assetid: cc42267f-bb7a-427a-845e-df97408528d4
ms.openlocfilehash: a54c68efb4ac114fe0e5a5712eca877bef35c103
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290110"
---
# <a name="sealing"></a>sealed
Una delle funzionalità dei Framework orientati a oggetti è che gli sviluppatori possono estenderli e personalizzarli in modi imprevisti dalle finestre di progettazione del Framework. Questa è la potenza e il pericolo della progettazione estendibile. Quando si progetta il Framework, è quindi molto importante progettare accuratamente per l'estendibilità quando si desidera e limitare l'estendibilità quando è pericoloso.

 Un meccanismo potente che impedisce l'estendibilità è la chiusura. È possibile sigillare la classe o i singoli membri. La chiusura di una classe impedisce agli utenti di ereditare dalla classe. La chiusura di un membro impedisce agli utenti di eseguire l'override di un membro specifico.

 ❌Non bloccare le classi senza avere un motivo valido.

 La chiusura di una classe perché non è un buon motivo per considerare uno scenario di estendibilità. Gli utenti del Framework desiderano ereditare dalle classi per diversi motivi non ovvi, ad esempio l'aggiunta di pratici membri. Per esempi di motivi non evidenti che gli utenti desiderano ereditare da un tipo, vedere [classi non sealed](unsealed-classes.md) .

 Di seguito sono riportati i motivi validi per la chiusura di una classe:

- La classe è una classe statica. Vedere [progettazione di classi statiche](static-class.md).

- La classe archivia i segreti sensibili per la sicurezza nei membri protetti ereditati.

- La classe eredita molti membri virtuali e il costo di sealing singolarmente supererà i vantaggi derivanti dall'uscita dalla classe.

- La classe è un attributo che richiede una ricerca molto rapida del runtime. Gli attributi sealed hanno livelli di prestazioni leggermente più elevati rispetto a quelli non bloccati. Vedere [attributi](attributes.md).

 ❌NON dichiarare membri protetti o virtuali su tipi sealed.

 Per definizione, i tipi sealed non possono essere ereditati da. Ciò significa che i membri protetti nei tipi sealed non possono essere chiamati e che non è possibile eseguire l'override dei metodi virtuali sui tipi sealed.

 ✔️ tenere in considerazione i membri che si sostituiscono.

 I problemi che possono derivare dall'introduzione di membri virtuali (descritti in [membri virtuali](virtual-members.md)) si applicano anche alle sostituzioni, anche se a un livello leggermente inferiore. La chiusura di una sostituzione protegge da questi problemi a partire da quel punto nella gerarchia di ereditarietà.

 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti riservati.*

 *Ristampato con l'autorizzazione di Pearson Education, Inc. da [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2a edizione](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) di Krzysztof Cwalina and Brad Abrams, pubblicato il 22 ottobre 2008 da Addison-Wesley Professional nella collana Microsoft Windows Development Series.*

## <a name="see-also"></a>Vedere anche

- [Linee guida per la progettazione di Framework](index.md)
- [Progettazione finalizzata all'estensibilità](designing-for-extensibility.md)
- [Classi non sealed](unsealed-classes.md)

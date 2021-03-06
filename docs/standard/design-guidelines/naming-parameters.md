---
title: Denominazione di parametri
description: Informazioni sulle linee guida per la denominazione dei parametri. Usare, ad esempio, nomi di parametri descrittivi & la convenzione Camel, & considerare la denominazione in base al significato anziché al tipo.
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- parameters, names
- names [.NET Framework], parameters
ms.assetid: ca3c956e-725a-441b-b4e3-eab5d472f41c
ms.openlocfilehash: 54f37c4d6a0f9a6931fa69d612bf0e45bf1f2ce7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84583518"
---
# <a name="naming-parameters"></a>Denominazione di parametri
Oltre al motivo più ovvio della leggibilità, è importante seguire le linee guida per i nomi dei parametri, perché i parametri vengono visualizzati nella documentazione e nella finestra di progettazione quando gli strumenti di progettazione visivi forniscono funzionalità IntelliSense e di esplorazione delle classi.

 ✔️ utilizzare camelCasing nei nomi dei parametri.

 ✔️ utilizzare nomi di parametro descrittivi.

 ✔️ CONSIDERARE l'uso di nomi basati sul significato di un parametro anziché sul tipo del parametro.

### <a name="naming-operator-overload-parameters"></a>Denominazione dei parametri di overload degli operatori
 ✔️ utilizzare `left` e `right` per i nomi dei parametri di overload degli operatori binari se non esiste alcun significato per i parametri.

 ✔️ utilizzare `value` per i nomi dei parametri di overload dell'operatore unario se non esiste alcun significato per i parametri.

 ✔️ CONSIDERARE nomi significativi per i parametri di overload degli operatori se questa operazione aggiunge un valore significativo.

 ❌Non usare abbreviazioni o indici numerici per i nomi dei parametri di overload degli operatori.

 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti riservati.*

 *Ristampato con l'autorizzazione di Pearson Education, Inc. da [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2a edizione](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) di Krzysztof Cwalina and Brad Abrams, pubblicato il 22 ottobre 2008 da Addison-Wesley Professional nella collana Microsoft Windows Development Series.*

## <a name="see-also"></a>Vedere anche

- [Linee guida per la progettazione di Framework](index.md)
- [Linee guida per la denominazione](naming-guidelines.md)

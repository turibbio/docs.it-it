---
title: Membri protetti
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- members [.NET Framework], protected
- protected members
- classes [.NET Framework], unsealed
- classes [.NET Framework], protected members
- unsealed classes
- customizing class behavior
ms.assetid: aa0b58ee-3956-494d-ab48-471ae5db8740
ms.openlocfilehash: afcb92e48996d594fcedc5b579922b179f754b9d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286119"
---
# <a name="protected-members"></a>Membri protetti
I membri protetti da soli non forniscono alcuna estensibilità, ma possono garantire l'estendibilità tramite la sottoclasse più potente. Possono essere usati per esporre opzioni di personalizzazione avanzate senza complicare inutilmente l'interfaccia pubblica principale.

 I progettisti di Framework devono prestare attenzione ai membri protetti perché il nome "protetto" può dare un falso senso di sicurezza. Chiunque è in grado di eseguire la sottoclasse di una classe non sealed e di accedere ai membri protetti, quindi tutte le stesse procedure di codifica difensiva usate per i membri pubblici si applicano ai membri protetti.

 ✔️ CONSIGLIABILE utilizzare membri protetti per la personalizzazione avanzata.

 ✔️ Considera i membri protetti nelle classi non sealed come Public ai fini della sicurezza, della documentazione e dell'analisi della compatibilità.

 Chiunque può ereditare da una classe e accedere ai membri protetti.

 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti riservati.*

 *Ristampato con l'autorizzazione di Pearson Education, Inc. da [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2a edizione](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) di Krzysztof Cwalina and Brad Abrams, pubblicato il 22 ottobre 2008 da Addison-Wesley Professional nella collana Microsoft Windows Development Series.*

## <a name="see-also"></a>Vedere anche

- [Linee guida per la progettazione di Framework](index.md)
- [Progettazione finalizzata all'estensibilità](designing-for-extensibility.md)

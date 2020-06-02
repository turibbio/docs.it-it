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
# <a name="protected-members"></a><span data-ttu-id="021e5-102">Membri protetti</span><span class="sxs-lookup"><span data-stu-id="021e5-102">Protected Members</span></span>
<span data-ttu-id="021e5-103">I membri protetti da soli non forniscono alcuna estensibilità, ma possono garantire l'estendibilità tramite la sottoclasse più potente.</span><span class="sxs-lookup"><span data-stu-id="021e5-103">Protected members by themselves do not provide any extensibility, but they can make extensibility through subclassing more powerful.</span></span> <span data-ttu-id="021e5-104">Possono essere usati per esporre opzioni di personalizzazione avanzate senza complicare inutilmente l'interfaccia pubblica principale.</span><span class="sxs-lookup"><span data-stu-id="021e5-104">They can be used to expose advanced customization options without unnecessarily complicating the main public interface.</span></span>

 <span data-ttu-id="021e5-105">I progettisti di Framework devono prestare attenzione ai membri protetti perché il nome "protetto" può dare un falso senso di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="021e5-105">Framework designers need to be careful with protected members because the name "protected" can give a false sense of security.</span></span> <span data-ttu-id="021e5-106">Chiunque è in grado di eseguire la sottoclasse di una classe non sealed e di accedere ai membri protetti, quindi tutte le stesse procedure di codifica difensiva usate per i membri pubblici si applicano ai membri protetti.</span><span class="sxs-lookup"><span data-stu-id="021e5-106">Anyone is able to subclass an unsealed class and access protected members, and so all the same defensive coding practices used for public members apply to protected members.</span></span>

 <span data-ttu-id="021e5-107">✔️ CONSIGLIABILE utilizzare membri protetti per la personalizzazione avanzata.</span><span class="sxs-lookup"><span data-stu-id="021e5-107">✔️ CONSIDER using protected members for advanced customization.</span></span>

 <span data-ttu-id="021e5-108">✔️ Considera i membri protetti nelle classi non sealed come Public ai fini della sicurezza, della documentazione e dell'analisi della compatibilità.</span><span class="sxs-lookup"><span data-stu-id="021e5-108">✔️ DO treat protected members in unsealed classes as public for the purpose of security, documentation, and compatibility analysis.</span></span>

 <span data-ttu-id="021e5-109">Chiunque può ereditare da una classe e accedere ai membri protetti.</span><span class="sxs-lookup"><span data-stu-id="021e5-109">Anyone can inherit from a class and access the protected members.</span></span>

 <span data-ttu-id="021e5-110">*Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti riservati.*</span><span class="sxs-lookup"><span data-stu-id="021e5-110">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>

 <span data-ttu-id="021e5-111">*Ristampato con l'autorizzazione di Pearson Education, Inc. da [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2a edizione](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) di Krzysztof Cwalina and Brad Abrams, pubblicato il 22 ottobre 2008 da Addison-Wesley Professional nella collana Microsoft Windows Development Series.*</span><span class="sxs-lookup"><span data-stu-id="021e5-111">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>

## <a name="see-also"></a><span data-ttu-id="021e5-112">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="021e5-112">See also</span></span>

- [<span data-ttu-id="021e5-113">Linee guida per la progettazione di Framework</span><span class="sxs-lookup"><span data-stu-id="021e5-113">Framework Design Guidelines</span></span>](index.md)
- [<span data-ttu-id="021e5-114">Progettazione finalizzata all'estensibilità</span><span class="sxs-lookup"><span data-stu-id="021e5-114">Designing for Extensibility</span></span>](designing-for-extensibility.md)

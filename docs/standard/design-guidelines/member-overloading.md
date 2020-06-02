---
title: Overload dei membri
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- default arguments
- members [.NET Framework], overloaded
- member design guidelines [.NET Framework], overloading
- overloaded members
- signatures, members
ms.assetid: 964ba19e-8b94-4b5b-b1e3-5a0b531a0bb1
ms.openlocfilehash: 6a2cd6d4dd293a7f4a408e1ee97a125c9454be41
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289005"
---
# <a name="member-overloading"></a><span data-ttu-id="39c36-102">Overload dei membri</span><span class="sxs-lookup"><span data-stu-id="39c36-102">Member Overloading</span></span>
<span data-ttu-id="39c36-103">L'overload dei membri significa creare due o più membri dello stesso tipo che differiscono solo per il numero o il tipo di parametri, ma hanno lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="39c36-103">Member overloading means creating two or more members on the same type that differ only in the number or type of parameters but have the same name.</span></span> <span data-ttu-id="39c36-104">Nel codice seguente, ad esempio, il `WriteLine` metodo è sovraccarico:</span><span class="sxs-lookup"><span data-stu-id="39c36-104">For example, in the following, the `WriteLine` method is overloaded:</span></span>

```csharp
public static class Console {
    public void WriteLine();
    public void WriteLine(string value);
    public void WriteLine(bool value);
    ...
}
```

 <span data-ttu-id="39c36-105">Poiché solo i metodi, i costruttori e le proprietà indicizzate possono avere parametri, è possibile eseguire l'overload solo dei membri.</span><span class="sxs-lookup"><span data-stu-id="39c36-105">Because only methods, constructors, and indexed properties can have parameters, only those members can be overloaded.</span></span>

 <span data-ttu-id="39c36-106">L'overload è una delle tecniche più importanti per migliorare l'usabilità, la produttività e la leggibilità delle librerie riutilizzabili.</span><span class="sxs-lookup"><span data-stu-id="39c36-106">Overloading is one of the most important techniques for improving usability, productivity, and readability of reusable libraries.</span></span> <span data-ttu-id="39c36-107">L'overload sul numero di parametri rende possibile fornire versioni più semplici dei costruttori e dei metodi.</span><span class="sxs-lookup"><span data-stu-id="39c36-107">Overloading on the number of parameters makes it possible to provide simpler versions of constructors and methods.</span></span> <span data-ttu-id="39c36-108">L'overload del tipo di parametro consente di utilizzare lo stesso nome di membro per i membri che eseguono operazioni identiche su un set selezionato di tipi diversi.</span><span class="sxs-lookup"><span data-stu-id="39c36-108">Overloading on the parameter type makes it possible to use the same member name for members performing identical operations on a selected set of different types.</span></span>

 <span data-ttu-id="39c36-109">✔️ provare a usare nomi di parametri descrittivi per indicare l'impostazione predefinita usata dagli overload più brevi.</span><span class="sxs-lookup"><span data-stu-id="39c36-109">✔️ DO try to use descriptive parameter names to indicate the default used by shorter overloads.</span></span>

 <span data-ttu-id="39c36-110">❌EVITARE di variare arbitrariamente i nomi dei parametri negli overload.</span><span class="sxs-lookup"><span data-stu-id="39c36-110">❌ AVOID arbitrarily varying parameter names in overloads.</span></span> <span data-ttu-id="39c36-111">Se un parametro in un overload rappresenta lo stesso input di un parametro in un altro overload, i parametri devono avere lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="39c36-111">If a parameter in one overload represents the same input as a parameter in another overload, the parameters should have the same name.</span></span>

 <span data-ttu-id="39c36-112">❌EVITARE di essere incoerenti nell'ordinamento dei parametri nei membri di overload.</span><span class="sxs-lookup"><span data-stu-id="39c36-112">❌ AVOID being inconsistent in the ordering of parameters in overloaded members.</span></span> <span data-ttu-id="39c36-113">I parametri con lo stesso nome devono essere visualizzati nella stessa posizione in tutti gli overload.</span><span class="sxs-lookup"><span data-stu-id="39c36-113">Parameters with the same name should appear in the same position in all overloads.</span></span>

 <span data-ttu-id="39c36-114">✔️ effettuare solo l'overload più lungo virtuale (se è necessaria l'estendibilità).</span><span class="sxs-lookup"><span data-stu-id="39c36-114">✔️ DO make only the longest overload virtual (if extensibility is required).</span></span> <span data-ttu-id="39c36-115">Gli overload più brevi devono semplicemente eseguire una chiamata a un overload più lungo.</span><span class="sxs-lookup"><span data-stu-id="39c36-115">Shorter overloads should simply call through to a longer overload.</span></span>

 <span data-ttu-id="39c36-116">❌Non usare `ref` `out` i modificatori o per eseguire l'overload dei membri.</span><span class="sxs-lookup"><span data-stu-id="39c36-116">❌ DO NOT use `ref` or `out` modifiers to overload members.</span></span>

 <span data-ttu-id="39c36-117">Alcuni linguaggi non possono risolvere le chiamate a overload come questo.</span><span class="sxs-lookup"><span data-stu-id="39c36-117">Some languages cannot resolve calls to overloads like this.</span></span> <span data-ttu-id="39c36-118">Inoltre, questi overload in genere hanno una semantica completamente diversa e probabilmente non devono essere overload ma due metodi distinti.</span><span class="sxs-lookup"><span data-stu-id="39c36-118">In addition, such overloads usually have completely different semantics and probably should not be overloads but two separate methods instead.</span></span>

 <span data-ttu-id="39c36-119">❌NON hanno overload con parametri nella stessa posizione e tipi simili ma con semantica diversa.</span><span class="sxs-lookup"><span data-stu-id="39c36-119">❌ DO NOT have overloads with parameters at the same position and similar types yet with different semantics.</span></span>

 <span data-ttu-id="39c36-120">✔️ consentono `null` di passare per gli argomenti facoltativi.</span><span class="sxs-lookup"><span data-stu-id="39c36-120">✔️ DO  allow `null` to be passed for optional arguments.</span></span>

 <span data-ttu-id="39c36-121">✔️ utilizzare l'overload dei membri anziché definire i membri con argomenti predefiniti.</span><span class="sxs-lookup"><span data-stu-id="39c36-121">✔️ DO use member overloading rather than defining members with default arguments.</span></span>

 <span data-ttu-id="39c36-122">Gli argomenti predefiniti non sono conformi a CLS.</span><span class="sxs-lookup"><span data-stu-id="39c36-122">Default arguments are not CLS compliant.</span></span>

 <span data-ttu-id="39c36-123">*Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti riservati.*</span><span class="sxs-lookup"><span data-stu-id="39c36-123">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>

 <span data-ttu-id="39c36-124">*Ristampato con l'autorizzazione di Pearson Education, Inc. da [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2a edizione](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) di Krzysztof Cwalina and Brad Abrams, pubblicato il 22 ottobre 2008 da Addison-Wesley Professional nella collana Microsoft Windows Development Series.*</span><span class="sxs-lookup"><span data-stu-id="39c36-124">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>

## <a name="see-also"></a><span data-ttu-id="39c36-125">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="39c36-125">See also</span></span>

- [<span data-ttu-id="39c36-126">Linee guida per la progettazione di membri</span><span class="sxs-lookup"><span data-stu-id="39c36-126">Member Design Guidelines</span></span>](member.md)
- [<span data-ttu-id="39c36-127">Linee guida per la progettazione di Framework</span><span class="sxs-lookup"><span data-stu-id="39c36-127">Framework Design Guidelines</span></span>](index.md)

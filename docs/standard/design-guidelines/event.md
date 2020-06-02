---
title: Progettazione di eventi
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- pre-events
- events [.NET Framework], design guidelines
- member design guidelines, events
- event handlers [.NET Framework], event design guidelines
- post-events
- signatures, event handling
ms.assetid: 67b3c6e2-6a8f-480d-a78f-ebeeaca1b95a
ms.openlocfilehash: 852c99b1a41691911f7ae82d3b8104526811757d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289824"
---
# <a name="event-design"></a><span data-ttu-id="847e4-102">Progettazione di eventi</span><span class="sxs-lookup"><span data-stu-id="847e4-102">Event Design</span></span>
<span data-ttu-id="847e4-103">Gli eventi sono il formato di callback più comunemente usato (costrutti che consentono al Framework di effettuare chiamate nel codice utente).</span><span class="sxs-lookup"><span data-stu-id="847e4-103">Events are the most commonly used form of callbacks (constructs that allow the framework to call into user code).</span></span> <span data-ttu-id="847e4-104">Altri meccanismi di callback includono i membri che accettano delegati, membri virtuali e plug-in basati su interfaccia. i dati degli studi di usabilità indicano che la maggior parte degli sviluppatori è più comoda usando gli eventi che usano gli altri meccanismi di callback.</span><span class="sxs-lookup"><span data-stu-id="847e4-104">Other callback mechanisms include members taking delegates, virtual members, and interface-based plug-ins. Data from usability studies indicate that the majority of developers are more comfortable using events than they are using the other callback mechanisms.</span></span> <span data-ttu-id="847e4-105">Gli eventi sono perfettamente integrati con Visual Studio e molti linguaggi.</span><span class="sxs-lookup"><span data-stu-id="847e4-105">Events are nicely integrated with Visual Studio and many languages.</span></span>

 <span data-ttu-id="847e4-106">È importante notare che esistono due gruppi di eventi: eventi generati prima che uno stato del sistema venga modificato, denominati pre-eventi ed eventi generati dopo una modifica dello stato, detti post-eventi.</span><span class="sxs-lookup"><span data-stu-id="847e4-106">It is important to note that there are two groups of events: events raised before a state of the system changes, called pre-events, and events raised after a state changes, called post-events.</span></span> <span data-ttu-id="847e4-107">Un esempio di evento preliminare `Form.Closing` è, che viene generato prima della chiusura di un form.</span><span class="sxs-lookup"><span data-stu-id="847e4-107">An example of a pre-event would be `Form.Closing`, which is raised before a form is closed.</span></span> <span data-ttu-id="847e4-108">Un esempio di post-evento è `Form.Closed` , che viene generato dopo la chiusura di un form.</span><span class="sxs-lookup"><span data-stu-id="847e4-108">An example of a post-event would be `Form.Closed`, which is raised after a form is closed.</span></span>

 <span data-ttu-id="847e4-109">✔️ usare il termine "Raise" per gli eventi anziché "Fire" o "trigger".</span><span class="sxs-lookup"><span data-stu-id="847e4-109">✔️ DO use the term "raise" for events rather than "fire" or "trigger."</span></span>

 <span data-ttu-id="847e4-110">✔️ utilizzare <xref:System.EventHandler%601?displayProperty=nameWithType> anziché creare manualmente nuovi delegati da utilizzare come gestori eventi.</span><span class="sxs-lookup"><span data-stu-id="847e4-110">✔️ DO use <xref:System.EventHandler%601?displayProperty=nameWithType> instead of manually creating new delegates to be used as event handlers.</span></span>

 <span data-ttu-id="847e4-111">✔️ CONSIDERARE l'uso di una sottoclasse di <xref:System.EventArgs> come argomento dell'evento, a meno che non si sia certi che l'evento non debba mai trasferire dati al metodo di gestione degli eventi, nel qual caso è possibile usare `EventArgs` direttamente il tipo.</span><span class="sxs-lookup"><span data-stu-id="847e4-111">✔️ CONSIDER using a subclass of <xref:System.EventArgs> as the event argument, unless you are absolutely sure the event will never need to carry any data to the event handling method, in which case you can use the `EventArgs` type directly.</span></span>

 <span data-ttu-id="847e4-112">Se si invia un'API usando `EventArgs` direttamente, non sarà mai possibile aggiungere dati da trasportare con l'evento senza interruzioni della compatibilità.</span><span class="sxs-lookup"><span data-stu-id="847e4-112">If you ship an API using `EventArgs` directly, you will never be able to add any data to be carried with the event without breaking compatibility.</span></span> <span data-ttu-id="847e4-113">Se si usa una sottoclasse, anche se inizialmente completamente vuota, sarà possibile aggiungere proprietà alla sottoclasse quando necessario.</span><span class="sxs-lookup"><span data-stu-id="847e4-113">If you use a subclass, even if initially completely empty, you will be able to add properties to the subclass when needed.</span></span>

 <span data-ttu-id="847e4-114">✔️ utilizzare un metodo virtuale protetto per generare ogni evento.</span><span class="sxs-lookup"><span data-stu-id="847e4-114">✔️ DO use a protected virtual method to raise each event.</span></span> <span data-ttu-id="847e4-115">Questa operazione è applicabile solo a eventi non statici su classi non sealed, non a struct, classi sealed o eventi statici.</span><span class="sxs-lookup"><span data-stu-id="847e4-115">This is only applicable to nonstatic events on unsealed classes, not to structs, sealed classes, or static events.</span></span>

 <span data-ttu-id="847e4-116">Lo scopo del metodo è fornire un modo per una classe derivata per gestire l'evento utilizzando una sostituzione.</span><span class="sxs-lookup"><span data-stu-id="847e4-116">The purpose of the method is to provide a way for a derived class to handle the event using an override.</span></span> <span data-ttu-id="847e4-117">L'override è un modo più flessibile, più veloce e più naturale per gestire gli eventi della classe di base nelle classi derivate.</span><span class="sxs-lookup"><span data-stu-id="847e4-117">Overriding is a more flexible, faster, and more natural way to handle base class events in derived classes.</span></span> <span data-ttu-id="847e4-118">Per convenzione, il nome del metodo deve iniziare con "on" e deve essere seguito dal nome dell'evento.</span><span class="sxs-lookup"><span data-stu-id="847e4-118">By convention, the name of the method should start with "On" and be followed with the name of the event.</span></span>

 <span data-ttu-id="847e4-119">La classe derivata può scegliere di non chiamare l'implementazione di base del metodo nella relativa override.</span><span class="sxs-lookup"><span data-stu-id="847e4-119">The derived class can choose not to call the base implementation of the method in its override.</span></span> <span data-ttu-id="847e4-120">Essere preparati a questo scopo senza includere alcuna elaborazione nel metodo necessaria per il corretto funzionamento della classe base.</span><span class="sxs-lookup"><span data-stu-id="847e4-120">Be prepared for this by not including any processing in the method that is required for the base class to work correctly.</span></span>

 <span data-ttu-id="847e4-121">✔️ accettano un parametro per il metodo protetto che genera un evento.</span><span class="sxs-lookup"><span data-stu-id="847e4-121">✔️ DO take one parameter to the protected method that raises an event.</span></span>

 <span data-ttu-id="847e4-122">Il parametro deve essere denominato `e` e deve essere tipizzato come classe dell'argomento dell'evento.</span><span class="sxs-lookup"><span data-stu-id="847e4-122">The parameter should be named `e` and should be typed as the event argument class.</span></span>

 <span data-ttu-id="847e4-123">❌NON passare null come mittente durante la generazione di un evento non statico.</span><span class="sxs-lookup"><span data-stu-id="847e4-123">❌ DO NOT pass null as the sender when raising a nonstatic event.</span></span>

 <span data-ttu-id="847e4-124">✔️ passano null come mittente durante la generazione di un evento statico.</span><span class="sxs-lookup"><span data-stu-id="847e4-124">✔️ DO pass null as the sender when raising a static event.</span></span>

 <span data-ttu-id="847e4-125">❌NON passare null come parametro di dati evento durante la generazione di un evento.</span><span class="sxs-lookup"><span data-stu-id="847e4-125">❌ DO NOT pass null as the event data parameter when raising an event.</span></span>

 <span data-ttu-id="847e4-126">È necessario passare `EventArgs.Empty` se non si desidera passare dati al metodo di gestione degli eventi.</span><span class="sxs-lookup"><span data-stu-id="847e4-126">You should pass `EventArgs.Empty` if you don’t want to pass any data to the event handling method.</span></span> <span data-ttu-id="847e4-127">Gli sviluppatori si aspettano che questo parametro non sia null.</span><span class="sxs-lookup"><span data-stu-id="847e4-127">Developers expect this parameter not to be null.</span></span>

 <span data-ttu-id="847e4-128">✔️ prendere in considerazione la generazione di eventi che possono essere annullati dall'utente finale.</span><span class="sxs-lookup"><span data-stu-id="847e4-128">✔️ CONSIDER raising events that the end user can cancel.</span></span> <span data-ttu-id="847e4-129">Questo vale solo per gli eventi precedenti.</span><span class="sxs-lookup"><span data-stu-id="847e4-129">This only applies to pre-events.</span></span>

 <span data-ttu-id="847e4-130">Utilizzare <xref:System.ComponentModel.CancelEventArgs?displayProperty=nameWithType> o la relativa sottoclasse come argomento dell'evento per consentire all'utente finale di annullare gli eventi.</span><span class="sxs-lookup"><span data-stu-id="847e4-130">Use <xref:System.ComponentModel.CancelEventArgs?displayProperty=nameWithType> or its subclass as the event argument to allow the end user to cancel events.</span></span>

### <a name="custom-event-handler-design"></a><span data-ttu-id="847e4-131">Progettazione di gestori eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="847e4-131">Custom Event Handler Design</span></span>
 <span data-ttu-id="847e4-132">In alcuni casi non `EventHandler<T>` è possibile utilizzare, ad esempio quando il Framework deve funzionare con le versioni precedenti di CLR, che non supportava i generics.</span><span class="sxs-lookup"><span data-stu-id="847e4-132">There are cases in which `EventHandler<T>` cannot be used, such as when the framework needs to work with earlier versions of the CLR, which did not support Generics.</span></span> <span data-ttu-id="847e4-133">In questi casi, potrebbe essere necessario progettare e sviluppare un delegato del gestore eventi personalizzato.</span><span class="sxs-lookup"><span data-stu-id="847e4-133">In such cases, you might need to design and develop a custom event handler delegate.</span></span>

 <span data-ttu-id="847e4-134">✔️ utilizzare un tipo restituito void per i gestori eventi.</span><span class="sxs-lookup"><span data-stu-id="847e4-134">✔️ DO use a return type of void for event handlers.</span></span>

 <span data-ttu-id="847e4-135">Un gestore eventi può richiamare più metodi di gestione degli eventi, possibilmente su più oggetti.</span><span class="sxs-lookup"><span data-stu-id="847e4-135">An event handler can invoke multiple event handling methods, possibly on multiple objects.</span></span> <span data-ttu-id="847e4-136">Se i metodi di gestione degli eventi sono autorizzati a restituire un valore, saranno presenti più valori restituiti per ogni chiamata di evento.</span><span class="sxs-lookup"><span data-stu-id="847e4-136">If event handling methods were allowed to return a value, there would be multiple return values for each event invocation.</span></span>

 <span data-ttu-id="847e4-137">✔️ utilizzare `object` come tipo del primo parametro del gestore eventi e chiamarlo `sender` .</span><span class="sxs-lookup"><span data-stu-id="847e4-137">✔️ DO use `object` as the type of the first parameter of the event handler, and call it `sender`.</span></span>

 <span data-ttu-id="847e4-138">✔️ utilizzare <xref:System.EventArgs?displayProperty=nameWithType> o la relativa sottoclasse come tipo del secondo parametro del gestore eventi e chiamarlo `e` .</span><span class="sxs-lookup"><span data-stu-id="847e4-138">✔️ DO use <xref:System.EventArgs?displayProperty=nameWithType> or its subclass as the type of the second parameter of the event handler, and call it `e`.</span></span>

 <span data-ttu-id="847e4-139">❌NON avere più di due parametri sui gestori eventi.</span><span class="sxs-lookup"><span data-stu-id="847e4-139">❌ DO NOT have more than two parameters on event handlers.</span></span>

 <span data-ttu-id="847e4-140">*Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti riservati.*</span><span class="sxs-lookup"><span data-stu-id="847e4-140">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>

 <span data-ttu-id="847e4-141">*Ristampato con l'autorizzazione di Pearson Education, Inc. da [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2a edizione](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) di Krzysztof Cwalina and Brad Abrams, pubblicato il 22 ottobre 2008 da Addison-Wesley Professional nella collana Microsoft Windows Development Series.*</span><span class="sxs-lookup"><span data-stu-id="847e4-141">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>

## <a name="see-also"></a><span data-ttu-id="847e4-142">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="847e4-142">See also</span></span>

- [<span data-ttu-id="847e4-143">Linee guida per la progettazione di membri</span><span class="sxs-lookup"><span data-stu-id="847e4-143">Member Design Guidelines</span></span>](member.md)
- [<span data-ttu-id="847e4-144">Linee guida per la progettazione di Framework</span><span class="sxs-lookup"><span data-stu-id="847e4-144">Framework Design Guidelines</span></span>](index.md)

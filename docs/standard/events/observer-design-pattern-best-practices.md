---
title: Procedure consigliate per un modello di progettazione observer
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- observer design pattern [.NET Framework], best practices
- best practices [.NET Framework], observer design pattern
ms.assetid: c834760f-ddd4-417f-abb7-a059679d5b8c
ms.openlocfilehash: b4f8e568dcb6790dac1dc8fc5c969d6fa1367c4e
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288459"
---
# <a name="observer-design-pattern-best-practices"></a>Procedure consigliate per un modello di progettazione observer
In.NET Framework, il modello di progettazione osservatore è implementato come un insieme di interfacce. L'interfaccia <xref:System.IObservable%601?displayProperty=nameWithType> rappresenta il provider di dati, che è anche responsabile di fornire un'implementazione di <xref:System.IDisposable> che consenta agli osservatori di annullare la sottoscrizione di notifiche. L'interfaccia <xref:System.IObserver%601?displayProperty=nameWithType> rappresenta l'osservatore. In questo argomento vengono descritte le procedure consigliate che gli sviluppatori devono seguire per implementare il modello di progettazione osservatore usando queste interfacce.  
  
## <a name="threading"></a>Threading  
 In genere, un provider implementa il metodo <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> aggiungendo un osservatore specifico a un elenco di server di sottoscrizione, che è rappresentato da un oggetto di raccolta, e implementa il metodo <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> rimuovendo un osservatore specifico dall'elenco dei server di sottoscrizione. Un osservatore può chiamare questi metodi in qualsiasi momento. Inoltre, perché il contratto provider/osservatore non specifica chi è responsabile dell'annullamento della sottoscrizione dopo il metodo di callback <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType>, il provider e l'osservatore possono provare a rimuovere lo stesso membro dall'elenco. Grazie a questa possibilità, entrambi i metodi <xref:System.IObservable%601.Subscribe%2A> e <xref:System.IDisposable.Dispose%2A> dovrebbero essere thread-safe. In genere, ciò comporta l'uso di una [raccolta simultanea](../parallel-programming/data-structures-for-parallel-programming.md) o di un blocco. Le implementazioni che non sono thread-safe devono documentare esplicitamente che non lo sono.  
  
 Tutte le garanzie aggiuntive devono essere specificate in un livello all'inizio del contratto provider/osservatore. Gli implementatori devono indicare chiaramente quando impongono requisiti aggiuntivi per evitare confusione sul contratto di osservatore.  
  
## <a name="handling-exceptions"></a>Gestione delle eccezioni  
 A causa dell'accoppiamento debole tra un provider di dati e un osservatore, le eccezioni nel modello di progettazione osservatore sono esclusivamente informative. Ciò influisce sul modo in cui provider e osservatori gestiscono le eccezioni nel modello di progettazione osservatore.  
  
### <a name="the-provider----calling-the-onerror-method"></a>Provider: Chiamata al metodo OnError  
 Il metodo <xref:System.IObserver%601.OnError%2A> è concepito come un messaggio informativo agli osservatori, in modo analogo al metodo <xref:System.IObserver%601.OnNext%2A?displayProperty=nameWithType>. Tuttavia, il metodo <xref:System.IObserver%601.OnNext%2A> è progettato al fine di fornire a un osservare dati correnti o aggiornati, laddove il metodo <xref:System.IObserver%601.OnError%2A> è progettato per indicare che il provider non può fornire dati validi.  
  
 Il provider dovrebbe seguire queste procedure consigliate durante la gestione delle eccezioni e la chiamata del metodo <xref:System.IObserver%601.OnError%2A>:  
  
- Il provider deve gestire le proprie eccezioni in caso di requisiti specifici.  
  
- Il provider non dovrebbe aspettarsi o richiedere che gli osservatori gestiscano le eccezioni in alcun modo particolare.  
  
- Il provider dovrà chiamare il metodo <xref:System.IObserver%601.OnError%2A> quando gestisce un'eccezione che compromette la sua capacità di fornire aggiornamenti. Le informazioni su tali eccezioni possono essere passate all'osservatore. In altri casi, non è necessario notificare un'eccezione agli osservatori.  
  
 Quando il provider chiama il metodo <xref:System.IObserver%601.OnError%2A> o <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType>, non vi saranno altre notifiche e il provider potrà annullare la sottoscrizione dei relativi osservatori. Questi ultimi, tuttavia, potranno a loro volta annullare una sottoscrizione in qualsiasi momento, sia prima sia dopo aver ricevuto una notifica <xref:System.IObserver%601.OnError%2A> o <xref:System.IObserver%601.OnCompleted%2A?displayProperty=nameWithType>. Il modello di progettazione dell'osservatore non indica se il provider o l'osservatore è responsabile dell'annullamento della sottoscrizione. Quindi, è possibile che entrambi provino ad annullare la sottoscrizione. In genere, quando gli osservatori annullano l'iscrizione, vengono rimossi da una raccolta di sottoscrittori. In un'applicazione a thread singolo, l'implementazione di <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> dovrà garantire che un riferimento all'oggetto sia valido e che l'oggetto sia un membro della raccolta di sottoscrittori prima di provare a rimuoverlo. In un'applicazione multithreading, è necessario usare un oggetto di raccolta thread-safe, come ad esempio un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=nameWithType>.  
  
### <a name="the-observer----implementing-the-onerror-method"></a>Osservatore: implementazione del metodo OnError  
 Quando un osservatore riceve una notifica di errore da un provider, l'osservatore deve considerare l'eccezione come informativa e non deve eseguire alcuna operazione particolare.  
  
 L'osservatore dovrebbe seguire queste procedure consigliate durante la risposta a gestione delle eccezioni e la chiamata al metodo <xref:System.IObserver%601.OnError%2A> da un provider:  
  
- L'osservatore non deve generare eccezioni dalle implementazioni dell'interfaccia, come ad esempio <xref:System.IObserver%601.OnNext%2A> o <xref:System.IObserver%601.OnError%2A>. Tuttavia, se l'osservatore genera eccezioni, deve aspettarsi che queste eccezioni rimangano non gestite.  
  
- Per preservare lo stack di chiamate, un osservatore che intenda generare un oggetto <xref:System.Exception> che è stato passato al relativo metodo <xref:System.IObserver%601.OnError%2A> dovrà eseguire il wrapping dell'eccezione prima di generarla. A questo scopo è necessario usare un oggetto eccezione standard.  
  
## <a name="additional-best-practices"></a>Procedure consigliate aggiuntive  
 Un tentativo di annullamento della registrazione nel metodo <xref:System.IObservable%601.Subscribe%2A?displayProperty=nameWithType> può produrre un riferimento null. È quindi consigliabile evitare questa operazione.  
  
 Nonostante sia possibile associare un osservatore a più provider, il modello consigliato consiste nell'associare un'istanza di <xref:System.IObserver%601> a una sola istanza di <xref:System.IObservable%601>.  
  
## <a name="see-also"></a>Vedere anche

- [Modello di progettazione Observer](observer-design-pattern.md)
- [Procedura: implementare un Observer](how-to-implement-an-observer.md)
- [Procedura: implementare un provider](how-to-implement-a-provider.md)

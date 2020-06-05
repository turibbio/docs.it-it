---
title: Events
ms.date: 07/20/2015
helpviewer_keywords:
- events [Visual Basic], about events
- events [Visual Basic]
ms.assetid: 8fb0353a-e41b-4e23-b78f-da65db832f70
ms.openlocfilehash: c61e960078557282de39bdc30f1d614ce8a77f29
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405119"
---
# <a name="events-visual-basic"></a>Eventi (Visual Basic)
Sebbene sia possibile visualizzare un progetto di Visual Studio come una serie di procedure eseguite in una sequenza, in realtà, la maggior parte dei programmi è basata sugli eventi, ovvero il flusso di esecuzione è determinato da occorrenze esterne denominate *eventi*.  
  
 Un evento è un segnale che informa un'applicazione che si è verificato qualcosa di importante. Ad esempio, quando un utente fa clic su un controllo in un form, il form può generare un evento `Click` e chiamare una routine che gestisce l'evento. Gli eventi consentono anche le comunicazioni tra attività separate. Si supponga, ad esempio, che un'applicazione esegua un'attività di ordinamento separatamente dall'applicazione principale. Se un utente annulla l'ordinamento, l'applicazione può inviare un evento di annullamento per segnalare la necessità di interrompere il processo di ordinamento.  
  
## <a name="event-terms-and-concepts"></a>Termini e concetti relativi agli eventi  
 In questa sezione vengono descritti i termini e i concetti utilizzati con gli eventi in Visual Basic.  
  
### <a name="declaring-events"></a>Dichiarazione di eventi  
 Gli eventi vengono dichiarati all'interno di classi, strutture, moduli e interfacce tramite la parola chiave `Event`, come nell'esempio seguente:  
  
 [!code-vb[VbVbalrEvents#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#24)]  
  
### <a name="raising-events"></a>Generazione di eventi  
 Un evento può essere paragonato a un messaggio che annuncia che si è verificato qualcosa di importante. L'atto di trasmettere il messaggio viene definito *generazione* dell'evento. In Visual Basic si generano eventi con l' `RaiseEvent` istruzione, come nell'esempio seguente:  
  
 [!code-vb[VbVbalrEvents#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#25)]  
  
 Gli eventi devono essere generati nell'ambito della classe, del modulo o della struttura in cui sono dichiarati. Ad esempio, una classe derivata non può generare eventi ereditati da una classe di base.  
  
### <a name="event-senders"></a>Mittenti di eventi  
 Qualsiasi oggetto in grado di generare un evento è un *mittente di eventi*, noto anche come *origine di eventi*. I form, i controlli e gli oggetti definiti dall'utente sono alcuni esempi di mittenti di eventi.  
  
### <a name="event-handlers"></a>Gestori di eventi  
 I *gestori eventi* sono le routine chiamate quando si verifica un evento corrispondente. È possibile usare qualsiasi subroutine valida con una firma corrispondente come gestore eventi. Non è possibile usare una funzione come gestore eventi, tuttavia, perché non può restituire un valore all'origine di eventi.  
  
 Visual Basic utilizza una convenzione di denominazione standard per i gestori eventi che combina il nome del mittente dell'evento, un carattere di sottolineatura e il nome dell'evento. Ad esempio, il nome dell'evento `Click` per un pulsante denominato `button1` sarebbe `Sub button1_Click`.  
  
> [!NOTE]
> È consigliabile usare questa convenzione di denominazione durante la definizione dei gestori per gli eventi personalizzati, ma non è obbligatorio. Si può usare qualsiasi nome di subroutine valido.  
  
## <a name="associating-events-with-event-handlers"></a>Associazione di eventi a gestori eventi  
 Un gestore eventi diventa utilizzabile solo dopo averlo associato a un evento mediante l'istruzione `Handles` o `AddHandler`.  
  
### <a name="withevents-and-the-handles-clause"></a>WithEvents e clausola Handles  
 L'istruzione `WithEvents` e la clausola `Handles` offrono una modalità dichiarativa per specificare i gestori eventi. Un evento generato da un oggetto dichiarato con la parola chiave `WithEvents` può essere gestito da qualsiasi routine con un'istruzione `Handles` per tale evento, come illustrato nell'esempio seguente:  
  
 [!code-vb[VbVbalrEvents#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#1)]  
  
 L'istruzione `WithEvents` e la clausola `Handles` rappresentano spesso la scelta migliore per i gestori eventi, perché la sintassi dichiarativa che usano semplifica la scrittura del codice, la lettura e il debug per la gestione degli eventi. Tenere presenti, tuttavia, le limitazioni seguenti per l'uso delle variabili `WithEvents`:  
  
- Non è possibile usare una variabile `WithEvents` come variabile oggetto, ovvero non è possibile dichiararla come `Object`, ma è necessario specificare il nome della classe quando si dichiara la variabile.  
  
- Poiché gli eventi condivisi non sono associati a istanze di classe, non è possibile usare `WithEvents` per gestire gli eventi condivisi in modo dichiarativo. In modo analogo, non è possibile usare `WithEvents` o `Handles` per gestire gli eventi da `Structure`. In entrambi i casi, è possibile usare l'istruzione `AddHandler` per gestire tali eventi.  
  
- Non è possibile creare matrici di variabili `WithEvents`.  
  
 Le variabili `WithEvents` consentono a un unico gestore eventi di gestire uno o più tipi di evento oppure a uno o più gestori eventi di gestire lo stesso tipo di evento.  
  
 Anche se la clausola `Handles` rappresenta la modalità standard per associare un evento a un gestore eventi, è limitata all'associazione di eventi a gestori eventi in fase di compilazione.  
  
 In alcuni casi, ad esempio con gli eventi associati a form o controlli, Visual Basic estrae automaticamente un gestore eventi vuoto e lo associa a un evento. Ad esempio, quando si fa doppio clic su un pulsante di comando in un form in modalità progettazione, Visual Basic crea un gestore eventi vuoto e una `WithEvents` variabile per il pulsante di comando, come nel codice seguente:  
  
 [!code-vb[VbVbalrEvents#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#26)]  
  
### <a name="addhandler-and-removehandler"></a>AddHandler e RemoveHandler  
 L'istruzione `AddHandler` è simile alla clausola `Handles`, perché entrambe consentono di specificare un gestore eventi. Tuttavia, l'uso di `AddHandler` con `RemoveHandler` offre una maggiore flessibilità rispetto alla clausola `Handles`, perché consente di aggiungere, rimuovere e modificare dinamicamente il gestore eventi associato a un evento. Per gestire eventi condivisi o eventi da una struttura, è necessario usare `AddHandler`.  
  
 `AddHandler` accetta due argomenti: il nome di un evento da un mittente di eventi, ad esempio un controllo e un'espressione che restituisce un delegato. Non è necessario specificare in modo esplicito la classe delegata quando si usa `AddHandler`, perché l'istruzione `AddressOf` restituisce sempre un riferimento al delegato. L'esempio seguente associa un gestore eventi a un evento generato da un oggetto:  
  
 [!code-vb[VbVbalrEvents#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#28)]  
  
 `RemoveHandler`, che disconnette un evento da un gestore eventi, usa la stessa sintassi di `AddHandler`. Ad esempio:  
  
 [!code-vb[VbVbalrEvents#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#29)]  
  
 Nell'esempio seguente un gestore eventi viene associato a un evento e l'evento viene generato. Il gestore eventi intercetta l'evento e visualizza un messaggio.  
  
 Il primo gestore eventi viene quindi rimosso e all'evento viene associato un diverso gestore eventi. Quando l'evento viene generato di nuovo, viene visualizzato un messaggio diverso.  
  
 Infine, il secondo gestore eventi viene rimosso e viene generato l'evento per una terza volta. Dato che all'evento non è più associato un gestore eventi, non viene eseguita alcuna azione.  
  
 [!code-vb[VbVbalrEvents#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class2.vb#38)]  
  
## <a name="handling-events-inherited-from-a-base-class"></a>Gestione degli eventi ereditati da una classe di base  
 *Le classi derivate*, ovvero le classi che ereditano le caratteristiche da una classe di base, possono gestire gli eventi generati dalla rispettiva classe di base usando l'istruzione `Handles MyBase`.  
  
### <a name="to-handle-events-from-a-base-class"></a>Per gestire gli eventi da una classe di base  
  
- Dichiarare un gestore eventi nella classe derivata aggiungendo un'istruzione `Handles MyBase.`*nomeevento* alla riga della dichiarazione della routine del gestore eventi, dove *nomeevento* è il nome dell'evento nella classe di base che si sta gestendo. Ad esempio:  
  
     [!code-vb[VbVbalrEvents#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#12)]  
  
## <a name="related-sections"></a>Sezioni correlate  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Procedura dettagliata: dichiarazione e generazione di eventi](walkthrough-declaring-and-raising-events.md)|Descrizione dettagliata della procedura per dichiarare e generare eventi per una classe.|  
|[Procedura dettagliata: gestione di eventi](walkthrough-handling-events.md)|Illustra come scrivere una routine di gestore eventi.|  
|[Procedura: dichiarare eventi personalizzati per evitare il blocco](how-to-declare-custom-events-to-avoid-blocking.md)|Illustra come definire un evento personalizzato che consente la chiamata asincrona dei gestori eventi.|  
|[Procedura: dichiarare eventi personalizzati per proteggere la memoria](how-to-declare-custom-events-to-conserve-memory.md)|Illustra come definire un evento personalizzato che usa la memoria solo quando viene gestito l'evento.|  
|[Risoluzione dei problemi relativi ai gestori eventi ereditati in Visual Basic](troubleshooting-inherited-event-handlers.md)|Elenca i problemi comuni che si verificano con i gestori eventi nei componenti ereditati.|  
|[Events](../../../../standard/events/index.md)|Viene fornita una panoramica del modello di eventi usato in .NET Framework.|  
|[Creazione di gestori eventi in Windows Form](../../../../framework/winforms/creating-event-handlers-in-windows-forms.md)|Descrive come usare gli eventi associati agli oggetti di Windows Form.|  
|[Delegati](../delegates/index.md)|Panoramica dei delegati in Visual Basic.|

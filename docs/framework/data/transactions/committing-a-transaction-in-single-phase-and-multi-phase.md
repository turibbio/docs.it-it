---
title: Commit di una transazione in monofase e multifase
description: Informazioni su come eseguire il commit delle transazioni in una o due fasi in .NET. È necessario eseguire un commit a due fasi (2PC) se la transazione include più di una risorsa.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 694ea153-e4db-41ae-96ac-9ac66dcb69a9
ms.openlocfilehash: 2f4486998f347bf1db6d22433e6e48b553609c18
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/22/2020
ms.locfileid: "85141824"
---
# <a name="committing-a-transaction-in-single-phase-and-multi-phase"></a>Commit di una transazione in monofase e multifase
Ogni risorsa utilizzata in una transazione viene gestita dalla gestione risorse (in seguito indicato con la sigla GR), le cui azioni vengono coordinate dalla gestione transazioni (in seguito indicato con la sigla GT). Nell'argomento relativo all' [integrazione di risorse come partecipanti a una transazione](enlisting-resources-as-participants-in-a-transaction.md) viene illustrato il modo in cui una risorsa (o più risorse) può essere integrata in una transazione. Questo argomento descrive invece come coordinare il commit di una transazione fra le risorse integrate.  
  
 Al termine della transazione l'applicazione ne richiede il commit o il rollback. La gestione transazioni deve eliminare qualsiasi possibilità che si verifichino situazioni di incoerenza, come ad esempio nel caso di una transazione per cui alcuni gestori di risorse votano a favore del commit mentre altri votano a favore del rollback.  
  
 Se la transazione interessa più di una risorsa, è necessario eseguire un commit a due fasi. Il protocollo di commit a due fasi, che prevede una fase di preparazione e una fase di commit, garantisce che al termine della transazione venga eseguito coerentemente il commit oppure il rollback di tutte le modifiche apportate alle risorse. Tutti i partecipanti vengono quindi informati in merito al risultato finale. Per una descrizione dettagliata del protocollo di commit in due fasi, consultare il libro "*Transaction Processing: Concepts and Techniques (serie Morgan Kaufmann in gestione dati Systems) ISBN: 1558601902*" di Jim Gray.  
  
 Le prestazioni delle transazioni possono anche essere ottimizzate tramite il protocollo di commit monofase. Per altre informazioni, vedere [ottimizzazione tramite commit a fase singola e notifica a singola fase promuovibile](optimization-spc-and-promotable-spn.md).  
  
 Se si desidera soltanto ricevere informazioni sul risultato di una transazione senza partecipare alla votazione, è necessario essere registrati all'evento <xref:System.Transactions.Transaction.TransactionCompleted>.  
  
## <a name="two-phase-commit-2pc"></a>Protocollo 2PC  
 Nella prima fase della transazione, la gestione transazioni esegue una query su ogni risorsa allo scopo di determinare se eseguire il commit o il rollback di una transazione. Nella seconda fase della transazione, la gestione transazioni informa ogni risorsa in merito al risultato delle query eseguite, consentendo l'esecuzione delle operazioni di pulizia eventualmente necessarie.  
  
 Per poter partecipare a questo tipo di transazione, un gestore di risorse deve implementare l'interfaccia <xref:System.Transactions.IEnlistmentNotification>, che fornisce i metodi chiamati dal GT per l'invio delle notifiche durante un commit a due fasi.  Di seguito è riportato un esempio di questa implementazione.  
  
 [!code-csharp[Tx_Enlist#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/tx_enlist/cs/enlist.cs#2)]
 [!code-vb[Tx_Enlist#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/tx_enlist/vb/enlist.vb#2)]  
  
### <a name="prepare-phase-phase-1"></a>Fase di preparazione (fase 1)  
 Quando riceve dall'applicazione una richiesta di commit tramite una chiamata al metodo <xref:System.Transactions.CommittableTransaction.Commit%2A>, la gestione transazioni avvia la fase di preparazione di tutti i partecipanti integrati. A tale scopo, chiama il metodo <xref:System.Transactions.IEnlistmentNotification.Prepare%2A> su ogni risorsa integrata al fine di determinare per ognuna di esse il voto espresso in merito alla transazione.  
  
 Come illustrato nel semplice esempio seguente, il gestore di risorse che implementa l'interfaccia <xref:System.Transactions.IEnlistmentNotification> deve prima implementare il metodo <xref:System.Transactions.IEnlistmentNotification.Prepare%28System.Transactions.PreparingEnlistment%29>.  
  
```csharp
public void Prepare(PreparingEnlistment preparingEnlistment)  
{  
     Console.WriteLine("Prepare notification received");  
     //Perform work  
  
     Console.Write("reply with prepared? [Y|N] ");  
     c = Console.ReadKey();  
     Console.WriteLine();  
  
     //If work finished correctly, reply with prepared  
     if ((c.KeyChar == 'Y') || (c.KeyChar == 'y'))  
     {  
          preparingEnlistment.Prepared();  
          break;  
     }  
  
     // otherwise, do a ForceRollback  
     else if ((c.KeyChar == 'N') || (c.KeyChar == 'n'))  
     {  
          preparingEnlistment.ForceRollback();  
          break;  
     }  
}  
```  
  
 Quando il gestore di risorse durevole riceve questa chiamata, deve registrare le informazioni per il ripristino della transazione (disponibili tramite il recupero della proprietà <xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A>) nonché qualsiasi informazione necessaria al completamento della transazione in caso di commit. Non è necessario eseguire questa operazione all'interno del metodo <xref:System.Transactions.IEnlistmentNotification.Prepare%2A>, in quanto il GR può eseguirla mediante un thread di lavoro.  
  
 Dopo aver completato la fase di preparazione, il GR deve votare il commit o il rollback della transazione chiamando rispettivamente il metodo <xref:System.Transactions.PreparingEnlistment.Prepared%2A> o il metodo <xref:System.Transactions.PreparingEnlistment.ForceRollback%2A>. Si noti che la classe <xref:System.Transactions.PreparingEnlistment> eredita un metodo <xref:System.Transactions.Enlistment.Done%2A> dalla classe <xref:System.Transactions.Enlistment>. Se si chiama questo metodo sul callback <xref:System.Transactions.PreparingEnlistment> durante la fase di preparazione, il GT riceve una notifica in cui si indica che l'integrazione è di sola lettura (ovvero, i gestori di risorse possono leggere ma non aggiornare i dati protetti dalle transazioni) e il GT non informa più il GR in merito al risultato della transazione nella fase 2.  
  
 L'applicazione riceve informazioni sull'esito positivo del commit della transazione dopo che tutti i gestori di risorse votano tramite il metodo <xref:System.Transactions.PreparingEnlistment.Prepared%2A>.  
  
### <a name="commit-phase-phase-2"></a>Fase di commit (fase 2)  
 Nella seconda fase della transazione, se tutti i GR inviano al GT una conferma di esito positivo relativamente alla fase 1, ovvero se tutti i GR hanno richiamato il metodo <xref:System.Transactions.PreparingEnlistment.Prepared%2A> al termine della fase di preparazione, il GT richiama il metodo <xref:System.Transactions.IEnlistmentNotification.Commit%2A> per ogni gestore di risorse. I gestori di risorse possono quindi rendere definitive le modifiche e completare il commit.  
  
 Se almeno uno dei gestori di risorse invia una conferma di esito negativo relativamente alla fase 1, la gestione transazioni richiama il metodo <xref:System.Transactions.IEnlistmentNotification.Rollback%2A> per ogni gestore di risorse e segnala all'applicazione la non riuscita del commit.  
  
 Ne consegue che il gestore di risorse deve implementare i metodi seguenti.  
  
```csharp
public void Commit (Enlistment enlistment)  
{  
     // Do any work necessary when commit notification is received  
  
     // Declare done on the enlistment  
     enlistment.Done();  
}  
  
public void Rollback (Enlistment enlistment)  
{  
     // Do any work necessary when rollback notification is received  
  
     // Declare done on the enlistment
     enlistment.Done();
}  
```  
  
 Il GR deve eseguire tutte le operazioni necessarie per completare la transazione in base al tipo di notifica e quindi informare il GT in merito chiamando il metodo <xref:System.Transactions.Enlistment.Done%2A> sul parametro <xref:System.Transactions.Enlistment>. Queste operazioni possono essere eseguite su un thread di lavoro. Si osservi che nella fase 2 le notifiche possono presentarsi inline nello stesso thread che ha chiamato il metodo <xref:System.Transactions.PreparingEnlistment.Prepared%2A> nella fase 1. Ne consegue che, dopo la chiamata al metodo  <xref:System.Transactions.PreparingEnlistment.Prepared%2A>, non occorre eseguire alcuna operazione (ad esempio il rilascio dei blocchi) che si prevede sia stata completata prima di ricevere le notifiche della fase 2.  
  
### <a name="implementing-indoubt"></a>Implementazione di InDoubt  
 Infine, è necessario implementare il metodo <xref:System.Transactions.IEnlistmentNotification.InDoubt%2A> per il gestore di risorse volatile. Questo metodo viene chiamato se la gestione transazioni perde il contatto con uno o più partecipanti, il cui stato risulta pertanto sconosciuto. In questo caso è necessario registrare questo problema in modo che in un secondo momento sia possibile verificare se uno o più partecipanti della transazione sono rimasti in uno stato incoerente.  
  
```csharp
public void InDoubt (Enlistment enlistment)  
{  
     // log this  
     enlistment.Done();  
}  
```  
  
## <a name="single-phase-commit-optimization"></a>Ottimizzazione mediante commit monofase  
 Il protocollo di commit monofase è più efficiente in fase di esecuzione, poiché tutti gli aggiornamenti vengono eseguiti senza alcuna coordinazione esplicita. Per ulteriori informazioni su questo protocollo, vedere [Ottimizzazione mediante commit a fase singola e notifica promuovibile a una sola fase](optimization-spc-and-promotable-spn.md).  
  
## <a name="see-also"></a>Vedere anche

- [Ottimizzazione mediante commit monofase e notifica monofase promuovibile](optimization-spc-and-promotable-spn.md)
- [Integrazione di risorse come partecipanti a una transazione](enlisting-resources-as-participants-in-a-transaction.md)

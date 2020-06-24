---
title: Escalation della gestione delle transazioni
description: Informazioni sull'escalation della gestione delle transazioni in .NET, ovvero il processo di migrazione di una transazione da componenti di una gestione transazioni a un'altra.
ms.date: 03/30/2017
ms.assetid: 1e96331e-31b6-4272-bbbd-29ed1e110460
ms.openlocfilehash: a0b70f4be0f041be95b02537e06f9ec19a9b6183
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/22/2020
ms.locfileid: "85141657"
---
# <a name="transaction-management-escalation"></a>Escalation della gestione delle transazioni
In Windows è disponibile un set di servizi e moduli che costituisce una gestione transazioni. L'escalation della gestione transazioni consiste nel migrare una transazione da un componente di gestione transazioni a un altro.  
  
 Lo spazio dei nomi <xref:System.Transactions> comprende un componente di gestione transazioni finalizzato a coordinare una transazione che prevede al più un'unica risorsa durevole o più risorse volatili. La gestione transazioni offre le migliori prestazioni, in quanto esegue chiamate che riguardano esclusivamente un determinato dominio applicazione. Gli sviluppatori possono evitare di interagire direttamente con la gestione transazioni, in quanto lo spazio dei nomi <xref:System.Transactions> fornisce un'infrastruttura comune che definisce interfacce, comportamenti comuni e classi helper.  
  
 Quando si desidera fornire la transazione a un oggetto in un altro dominio applicazione (inclusi i limiti del processo e del computer) nello stesso computer, l' <xref:System.Transactions> infrastruttura esegue automaticamente l'escalation della transazione in modo che venga gestita da Microsoft Distributed Transaction Coordinator (MSDTC). L'escalation si verifica anche quando si integra un altro gestore di risorse durevoli. Dopo l'escalation, la transazione viene gestita nello stato superiore fino al suo completamento.  
  
 Fra la transazione dello spazio dei nomi <xref:System.Transactions> e la transazione MSDTC esiste un tipo intermedio di transazione reso disponibile tramite l'integrazione PSPE (Promotable Single Phase Enlistment), ovvero un altro importante meccanismo dello spazio dei nomi <xref:System.Transactions> finalizzato all'ottimizzazione delle prestazioni. L'integrazione PSPE consente a una risorsa durevole remota appartenente a un altro dominio applicazione, processo o computer di partecipare a una transazione dello spazio dei nomi <xref:System.Transactions> senza comportarne l'escalation a una transazione MSDTC. Per ulteriori informazioni su PSPE, vedere [integrazione di risorse come partecipanti a una transazione](enlisting-resources-as-participants-in-a-transaction.md).  
  
## <a name="how-escalation-is-initiated"></a>Condizioni e modalità di avvio delle escalation  
 L'escalation delle transazioni riduce le prestazioni in quanto il gestore MSDTC risiede in un processo a parte. Inoltre, l'escalation di una transazione al gestore MSDTC comporta l'invio di messaggi fra i processi. Per migliorare le prestazioni è necessario ritardare o evitare l'escalation al gestore MSDTC. È pertanto opportuno conoscere le condizioni e le modalità di avvio delle escalation.  
  
 Finché l'infrastruttura <xref:System.Transactions> gestisce risorse volatili e al massimo una risorsa durevole che supporta le notifiche monofase, la transazione resta proprietà dell'infrastruttura <xref:System.Transactions>. La gestione transazioni utilizza soltanto le risorse che risultano attive nello stesso dominio applicazione e per cui non è necessario eseguire la registrazione, ovvero la scrittura su disco del risultato della transazione. Le escalation che comportano il trasferimento della proprietà di una transazione dall'infrastruttura <xref:System.Transactions> al gestore MSDTC si verificano nei casi seguenti:  
  
- Almeno una risorsa durevole che non supporta le notifiche monofase viene integrata nella transazione.  
  
- Almeno due risorse durevoli che supportano le notifiche monofase vengono integrate nella transazione. L'integrazione di una singola connessione con SQL Server 2005, ad esempio, non comporta la promozione di una transazione. Tuttavia, ogni volta che si apre una seconda connessione a un database SQL Server 2005 che causa l'integrazione del database, l' <xref:System.Transactions> infrastruttura rileva che si tratta della seconda risorsa durevole nella transazione e ne esegue l'escalation a una transazione MSDTC.  
  
- Si verifica una richiesta di "marshalling" della transazione a un altro dominio applicazione o processo. Si consideri ad esempio il caso della serializzazione di un oggetto di transazione passato attraverso il confine di un dominio applicazione. In tal caso il sistema esegue il marshalling dell'oggetto di transazione per valore: se si tenta di passare tale oggetto attraverso il confine di un dominio applicazione (anche nello stesso processo), l'oggetto di transazione viene serializzato. È possibile passare gli oggetti di transazione effettuando una chiamata a un metodo remoto che accetta come parametro un oggetto <xref:System.Transactions.Transaction>. In alternativa, è possibile tentare di accedere a un componente remoto che supporta le transazioni. Ciò comporta la serializzazione dell'oggetto di transazione nonché un'escalation, analogamente al caso di serializzazione di una transazione passata attraverso il confine di un dominio applicazione. Ciò si verifica in quanto la transazione viene distribuita e quindi la gestione transazioni locali non è più adeguata.  
  
 Nella tabella seguente sono elencate tutte le eccezioni che possono essere generate durante un'escalation.  
  
|Tipo di eccezione|Condizione|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|Tentativo di escalation di una transazione con livello di isolamento uguale a <xref:System.Transactions.IsolationLevel.Snapshot>.|  
|<xref:System.Transactions.TransactionAbortedException>|La gestione transazioni non è disponibile.|  
|<xref:System.Transactions.TransactionException>|L'escalation non riesce e l'applicazione viene interrotta.|

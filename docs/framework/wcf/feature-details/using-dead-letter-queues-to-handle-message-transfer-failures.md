---
title: Uso di code di messaggi non recapitabili per gestire errori di trasferimento dei messaggi
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9e891c6a-d960-45ea-904f-1a00e202d61a
ms.openlocfilehash: f07397b4c10ffec4902dbde37b622978d00f5b63
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594985"
---
# <a name="using-dead-letter-queues-to-handle-message-transfer-failures"></a>Uso di code di messaggi non recapitabili per gestire errori di trasferimento dei messaggi
È possibile che i messaggi in coda non vengano recapitati. Tali messaggi con errori vengono registrati in una coda di messaggi non recapitabili. Il mancato recapito può essere dovuto a errori della rete, all'eliminazione di una coda, a una coda completa, a un errore di autenticazione o alla scadenza del tempo disponibile per il recapito.  
  
 I messaggi in coda possono rimanere nella coda per molto tempo se l'applicazione ricevente non li legge tempestivamente. Questo comportamento potrebbe non essere adatto per i messaggi a scadenza. Nell'associazione in coda la proprietà TTL (Time to Live) dei messaggi a scadenza è impostata, a indicare la durata della permanenza dei messaggi nella coda prima che scadano. I messaggi scaduti vengono inviati a una coda speciale denominata coda dei messaggi non recapitabili. I messaggi possono essere inoltre inseriti in una coda di messaggi non recapitabili per altri motivi, ad esempio se viene superata una quota della coda o se si verifica un errore di autenticazione.  
  
 In genere le applicazioni scrivono logica di compensazione per leggere i messaggi dalla coda dei messaggi non recapitabili e le motivazioni dell'errore. La logica di compensazione dipende dalla causa dell'errore. Nel caso di un errore di autenticazione, ad esempio, è possibile correggere il certificato allegato al messaggio e inviare di nuovo il messaggio. Se il messaggio non è stato recapitato a causa del raggiungimento della quota della coda di destinazione, è possibile tentare di recapitare di nuovo il messaggio nella speranza che il problema della quota sia stato risolto.  
  
 La maggior parte dei sistemi di accodamento dispongono di una coda di messaggi non recapitabili a livello di sistema nella quale vengono archiviati tutti i messaggi con errori provenienti dal sistema. In MSMQ (Accodamento messaggi) sono presenti due code di messaggi non recapitabili a livello di sistema: una coda di messaggi non recapitabili relativi a transazioni in cui sono archiviati messaggi non recapitati alla coda transazionale e una coda di messaggi non recapitabili in cui sono archiviati messaggi non recapitati alla coda non transazionale. Se due client inviano messaggi a due servizi diversi e pertanto code diverse in WCF condividono lo stesso servizio MSMQ per l'invio, è possibile che nella coda dei messaggi non recapitabili di sistema sia presente una combinazione di messaggi. Non è sempre una situazione ottimale. In molti casi (di sicurezza, ad esempio), non è opportuno che un client legga i messaggi di un altro client da una coda di messaggi non recapitabili. Una coda di messaggi non recapitabili condivisa, inoltre, impone ai client di scorrere la coda per trovare un messaggio inviato, operazione potenzialmente laboriosa in base al numero dei messaggi contenuti nella coda. Pertanto, in WCF `NetMsmqBinding` `MsmqIntegrationBinding,` e MSMQ in Windows Vista forniscono una coda di messaggi non recapitabili personalizzata (talvolta definita coda dei messaggi non recapitabili specifica dell'applicazione).  
  
 La coda di messaggi non recapitabili personalizzata fornisce l'isolamento tra client che condividono lo stesso servizio MSMQ per l'invio dei messaggi.  
  
 In Windows Server 2003 e Windows XP, Windows Communication Foundation (WCF) fornisce una coda di messaggi non recapitabili a livello di sistema per tutte le applicazioni client in coda. In Windows Vista, WCF fornisce una coda di messaggi non recapitabili per ogni applicazione client in coda.  
  
## <a name="specifying-use-of-the-dead-letter-queue"></a>Specificazione dell'utilizzo della coda dei messaggi non recapitabili  
 La coda dei messaggi non recapitabili si trova nel gestore delle code dell'applicazione mittente. Archivia messaggi scaduti o che non è stato possibile trasferire o recapitare.  
  
 L'associazione dispone delle proprietà della coda di messaggi non recapitabili seguenti:  
  
- <xref:System.ServiceModel.MsmqBindingBase.DeadLetterQueue%2A>  
  
- <xref:System.ServiceModel.MsmqBindingBase.CustomDeadLetterQueue%2A>  
  
## <a name="reading-messages-from-the-dead-letter-queue"></a>Lettura dalla coda dei messaggi non recapitabili  
 Un'applicazione che legge i messaggi da una coda di messaggi non recapitabili è simile a un servizio WCF che legge da una coda dell'applicazione, ad eccezione delle differenze minime seguenti:  
  
- Per leggere messaggi da una coda di sistema di messaggi non recapitabili relativi a transazioni, l'URI (Uniform Resource Identifier) deve presentarsi nel formato net.msmq://localhost/system$;DeadXact.  
  
- Per leggere messaggi da una coda di sistema di messaggi non recapitabili non relativi a transazioni, l'URI deve presentarsi nel formato net.msmq://localhost/system$;DeadLetter.  
  
- Per leggere i messaggi da una coda di messaggi non recapitabili personalizzata, l'URI deve avere il formato: NET. MSMQ://localhost/private/ \<*custom-dlq-name*> dove *Custom-coda DLQ-Name* è il nome della coda dei messaggi non recapitabili personalizzata.  
  
 Per ulteriori informazioni su come indirizzare le code, vedere [endpoint di servizio e indirizzamento delle code](service-endpoints-and-queue-addressing.md).  
  
 Lo stack WCF sul ricevitore corrisponde agli indirizzi su cui il servizio è in ascolto con l'indirizzo del messaggio. Se gli indirizzi corrispondono, il messaggio viene inviato. In caso contrario, il messaggio non viene inviato. Ciò può provocare problemi in caso di lettura dalla coda di messaggi non recapitabili, perché i messaggi in essa contenuti sono solitamente indirizzati al servizio, non al servizio della coda di messaggi non recapitabili. Pertanto, il servizio che legge dalla coda di messaggi non recapitabili deve installare un `ServiceBehavior` di filtro di indirizzi che indichi allo stack di far corrispondere tutti i messaggi contenuti nella coda indipendentemente dal destinatario. In particolare è necessario aggiungere un `ServiceBehavior` con il parametro <xref:System.ServiceModel.AddressFilterMode.Any> al servizio che legge messaggi dalla coda di messaggi non recapitabili.  
  
## <a name="poison-message-handling-from-the-dead-letter-queue"></a>Gestione dei messaggi non elaborabili dalla coda dei messaggi non recapitabili  
 La gestione dei messaggi non elaborabili è disponibile nelle code dei messaggi non recapitabili, ad alcune condizioni. Poiché non è possibile creare code secondarie dalle code di sistema, durante la lettura dalla coda di sistema dei messaggi non recapitabili `ReceiveErrorHandling` non può essere impostato su `Move`. Si noti che se si legge da una coda di messaggi non recapitabili personalizzata, è possibile avere code secondarie e, quindi, `Move` è una disposizione valida per il messaggio non elaborabile.  
  
 Quando `ReceiveErrorHandling` è impostato su `Reject`, durante la lettura dalla coda di messaggi non recapitabili personalizzata il messaggio non elaborabile viene inserito nella coda di sistema dei messaggi non recapitabili. Nel caso di lettura dalla coda di sistema dei messaggi non recapitabili, il messaggio viene rilasciato (eliminato). Un rifiuto da una coda di sistema di messaggi non recapitabili in MSMQ comporta il rilascio (eliminazione) del messaggio.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene descritto come creare una coda di messaggi non recapitabili e come utilizzarla per elaborare messaggi scaduti. L'esempio è basato sull'esempio in [procedura: scambiare messaggi in coda con endpoint WCF](how-to-exchange-queued-messages-with-wcf-endpoints.md). Nell'esempio seguente viene descritto come scrivere il codice client nel servizio di elaborazione ordini che utilizza una coda di messaggi non recapitabili per ogni applicazione. Nell'esempio viene inoltre mostrato come elaborare messaggi dalla coda di messaggi non recapitabili.  
  
 Il codice seguente si riferisce a un client che specifica una coda di messaggi non recapitabili per ogni applicazione.  
  
 [!code-csharp[S_DeadLetter#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_deadletter/cs/client.cs#1)]
 [!code-vb[S_DeadLetter#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_deadletter/vb/client.vb#1)]  
  
 Il codice seguente è per un file di configurazione client.  

 Il codice seguente si riferisce a un servizio che elabora messaggi da una coda di messaggi non recapitabili.  
  
 [!code-csharp[S_DeadLetter#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_deadletter/cs/dlservice.cs#3)]
 [!code-vb[S_DeadLetter#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_deadletter/vb/dlservice.vb#3)]  
  
 Il codice seguente è per il file di configurazione del servizio della coda di messaggi non recapitabili.  

## <a name="see-also"></a>Vedere anche

- [Panoramica delle code](queues-overview.md)
- [Procedura: scambiare messaggi in coda con endpoint WCF](how-to-exchange-queued-messages-with-wcf-endpoints.md)
- [Gestione dei messaggi non elaborabili](poison-message-handling.md)

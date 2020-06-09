---
title: Quote dei trasporti
ms.date: 03/30/2017
helpviewer_keywords:
- transport quotas [WCF]
ms.assetid: 3e71dd3d-f981-4d9c-9c06-ff8abb61b717
ms.openlocfilehash: fca5fbeffb560f848edda6421301785f02547d2c
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84585701"
---
# <a name="transport-quotas"></a>Quote dei trasporti
Le quote dei trasporti sono un meccanismo di criterio per stabilire quando una connessione sta utilizzando risorse eccessive. Una quota è un limite che impedisce l'utilizzo di risorse aggiuntive quando il valore della quota viene superato. Le quote dei trasporti impediscono attacchi di tipo Denial of Service (DoS) volutamente dannosi o non intenzionali.  
  
 I trasporti Windows Communication Foundation (WCF) dispongono di valori di quota predefiniti basati su un'allocazione conservativa di risorse. Questi valori predefiniti sono adatti per ambienti di sviluppo e scenari con installazioni di piccole dimensioni. Gli amministratori del servizio devono esaminare le quote dei trasporti e ottimizzare i singoli valori nel caso in cui un'installazione stia esaurendo le risorse o le connessioni vengano limitate nonostante la disponibilità di risorse aggiuntive.  
  
## <a name="types-of-transport-quotas"></a>Tipi di quote dei trasporti  
 I trasporti WCF presentano tre tipi di quote:  
  
- I *timeout* attenuano gli attacchi Denial of Service che si basano sull'associazione delle risorse per un lungo periodo di tempo.  
  
- I *limiti di allocazione della memoria* impediscono a una singola connessione di esaurire la memoria di sistema e di negare il servizio ad altre connessioni.  
  
- I *limiti delle dimensioni della raccolta* limitano l'utilizzo di risorse che allocano indirettamente memoria o sono in un approvvigionamento limitato.  
  
## <a name="transport-quota-descriptions"></a>Descrizioni delle quote dei trasporti  
 In questa sezione vengono descritte le quote di trasporto disponibili per i trasporti WCF standard: HTTP (S), TCP/IP e named pipe. I trasporti personalizzati possono esporre le proprie quote configurabili non incluse in questo elenco. Consultare la documentazione per il trasporto personalizzato e quote relative.  
  
 Ogni impostazione della quota è caratterizzata da un tipo, un valore minimo e un valore predefinito. Il valore massimo di una quota è limitato dal tipo. A causa di limitazioni dei computer, non è sempre possibile impostare una quota sul suo valore massimo.  
  
|Nome|Type|Min<br /><br /> value|Valore predefinito<br /><br /> value|Descrizione|  
|----------|----------|--------------------|-----------------------|-----------------|  
|`ChannelInitializationTimeout`|TimeSpan|1 tick|5 secondi|Tempo massimo di attesa perché una connessione invii il preambolo durante la lettura iniziale. Questi dati vengono ricevuti prima che si verifichi l'autenticazione. Questa impostazione è generalmente molto più piccola del valore della quota `ReceiveTimeout`.|  
|`CloseTimeout`|TimeSpan|0|1 min|Tempo massimo di attesa per la chiusura di una connessione prima che il trasporto generi un'eccezione.|  
|`ConnectionBufferSize`|Integer|1|8 KB|Dimensione, in byte, dei buffer di trasmissione e ricezione del trasporto sottostante. L'aumento della dimensione del buffer può migliorare la velocità effettiva in caso di invio di messaggi grandi.|  
|`IdleTimeout`|TimeSpan|0|2 min|Tempo massimo di inattività per una connessione in pool prima di essere chiusa.<br /><br /> Questa impostazione viene applicata solo a connessioni in pool.|  
|`LeaseTimeout`|TimeSpan|0|5 min|Durata massima di una connessione in pool attiva. Trascorso il periodo di tempo specificato, la connessione si chiude al termine dell'esecuzione della richiesta corrente.<br /><br /> Questa impostazione viene applicata solo a connessioni in pool.|  
|`ListenBacklog`|Integer|1|10|Numero massimo di connessioni che un listener può avere in attesa di esecuzione oltre il quale viene negata l'autorizzazione ad ulteriori connessioni a quell'endpoint.|  
|`MaxBufferPoolSize`|long|0|512 KB|Memoria massima, in byte, che il trasporto dedica al pooling di buffer dei messaggi riutilizzabili. Quando il pool non può fornire un buffer dei messaggi, ne viene allocato uno nuovo per utilizzo temporaneo.<br /><br /> Le installazioni che creano numerosi listener del canale o channel factory possono allocare grandi quantità di memoria per i pool di buffer. La riduzione delle dimensioni del buffer può ridurre considerevolmente l'utilizzo della memoria in questo scenario.|  
|`MaxBufferSize`|Integer|1|64 KB|Dimensione massima, in byte, di un buffer utilizzato per il flusso di dati. Se questa quota del trasporto non è impostata o se il trasporto non sta utilizzando l'invio nel flusso, il valore della quota corrisponde al minore tra i valori `MaxReceivedMessageSize` e <xref:System.Int32.MaxValue>.|  
|`MaxOutboundConnectionsPerEndpoint`|Integer|1|10|Numero massimo di connessioni in uscita che possono essere associate a un particolare endpoint.<br /><br /> Questa impostazione viene applicata solo a connessioni in pool.|  
|`MaxOutputDelay`|TimeSpan|0|200 ms|Tempo massimo di attesa dopo un'operazione di invio per il raggruppamento di messaggi aggiuntivi in un'unica operazione. I messaggi vengono inviati prima se il buffer del trasporto sottostante è pieno. L'invio di messaggi aggiuntivi non comporta la reimpostazione del periodo di ritardo.|  
|`MaxPendingAccepts`|Integer|1|1|Numero massimo di canali che possono attendere nel listener prima di essere accettati.<br /><br /> Esiste un intervallo di tempo tra il completamento dell'accettazione e l'avvio di una nuova accettazione. L'aumento delle dimensioni di questa raccolta consente di evitare l'eliminazione di client che si connettono durante questo intervallo.|  
|`MaxPendingConnections`|Integer|1|10|Numero massimo di connessioni che il listener può tenere in attesa di essere accettate dall'applicazione. Quando questo valore della quota viene superato, le nuove connessioni in ingresso vengono eliminate anziché restare in attesa di essere accettate.<br /><br /> Le funzionalità di connessione, ad esempio la protezione dei messaggi, possono determinare l'apertura di più connessioni da parte di un client. Gli amministratori del servizio devono tener conto delle connessioni aggiuntive durante l'impostazione di questo valore della quota.|  
|`MaxReceivedMessageSize`|long|1|64 KB|Dimensione massima, in byte, di un messaggio ricevuto, incluse le intestazioni, prima che il trasporto generi un'eccezione.|  
|`OpenTimeout`|TimeSpan|0|1 min|Tempo massimo di attesa per stabilire una connessione prima che il trasporto generi un'eccezione.|  
|`ReceiveTimeout`|TimeSpan|0|10 min|Tempo massimo di attesa per il completamento di un'operazione di lettura prima che il trasporto generi un'eccezione.|  
|`SendTimeout`|TimeSpan|0|1 min|Tempo massimo di attesa per il completamento di un'operazione di scrittura prima che il trasporto generi un'eccezione.|  
  
 Le quote del trasporto `MaxPendingConnections` e `MaxOutboundConnectionsPerEndpoint` sono combinate in un'unica quota del trasporto denominata `MaxConnections` se impostate tramite associazione o configurazione. Solo l'elemento di associazione consente di impostare questi valori di quota individualmente. La quota del trasporto `MaxConnections` è caratterizzata da valore minimo e valore predefinito uguali.  
  
## <a name="setting-transport-quotas"></a>Impostazione delle quote del trasporto  
 Le quote del trasporto sono impostate tramite l'elemento di associazione del trasporto, l'associazione del trasporto, la configurazione dell'applicazione o il criterio dell'host. In questo documento non viene esaminata l'impostazione dei trasporti tramite il criterio dell'host. Consultare la documentazione per il trasporto sottostante per scoprire le impostazioni per le quote del criterio dell'host. Nell'argomento [Configuring http and HTTPS](configuring-http-and-https.md) vengono descritte le impostazioni delle quote per il driver http. sys. Consultare la Microsoft Knowledge Base per ulteriori informazioni sulla configurazione dei limiti di Windows su connessioni HTTP, TCP/IP e named pipe.  
  
 Altri tipi di quote vengono applicati indirettamente ai trasporti. Il codificatore di messaggi utilizzato dal trasporto per trasformare un messaggio in byte può disporre di impostazioni delle quote personali. Queste quote, tuttavia, sono indipendenti dal tipo di trasporto utilizzato.  
  
### <a name="controlling-transport-quotas-from-the-binding-element"></a>Controllo delle quote del trasporto dall'elemento di associazione.  
 L'impostazione delle quote del trasporto tramite l'elemento di associazione offre la massima flessibilità per il controllo del comportamento del trasporto. Come timeout predefiniti per le operazioni di chiusura, apertura, ricezione e invio vengono utilizzati i valori specificati dall'associazione al momento della generazione di un canale.  
  
|Nome|HTTP|TCP/IP|Named pipe|  
|----------|----------|-------------|----------------|  
|`ChannelInitializationTimeout`||X|X|  
|`CloseTimeout`||||  
|`ConnectionBufferSize`||X|X|  
|`IdleTimeout`||X|X|  
|`LeaseTimeout`||X||  
|`ListenBacklog`||X||  
|`MaxBufferPoolSize`|X|X|X|  
|`MaxBufferSize`|X|X|X|  
|`MaxOutboundConnectionsPerEndpoint`||X|X|  
|`MaxOutputDelay`||X|X|  
|`MaxPendingAccepts`||X|X|  
|`MaxPendingConnections`||X|X|  
|`MaxReceivedMessageSize`|X|X|X|  
|`OpenTimeout`||||  
|`ReceiveTimeout`||||  
|`SendTimeout`||||  
  
### <a name="controlling-transport-quotas-from-the-binding"></a>Controllo delle quote del trasporto dall'associazione.  
 L'impostazione delle quote del trasporto tramite l'associazione offre un set semplificato di quote tra cui scegliere e allo stesso tempo consente l'accesso ai valori delle quote più comuni.  
  
|Nome|HTTP|TCP/IP|Named pipe|  
|----------|----------|-------------|----------------|  
|`ChannelInitializationTimeout`||||  
|`CloseTimeout`|X|X|X|  
|`ConnectionBufferSize`||||  
|`IdleTimeout`||||  
|`LeaseTimeout`||||  
|`ListenBacklog`||X||  
|`MaxBufferPoolSize`|X|X|X|  
|`MaxBufferSize`|1|X|X|  
|`MaxOutboundConnectionsPerEndpoint`||2|2|  
|`MaxOutputDelay`||||  
|`MaxPendingAccepts`||||  
|`MaxPendingConnections`||2|2|  
|`MaxReceivedMessageSize`|X|X|X|  
|`OpenTimeout`|X|X|X|  
|`ReceiveTimeout`|X|X|X|  
|`SendTimeout`|X|X|X|  
  
1. La quota del trasporto `MaxBufferSize` è disponibile solo nell'associazione `BasicHttp`. Le associazioni `WSHttp` sono valide per scenari che non supportano modalità di trasporto con flussi.  
  
2. Le quote del trasporto `MaxPendingConnections` e `MaxOutboundConnectionsPerEndpoint` sono combinate in un'unica quota denominata `MaxConnections`.  
  
### <a name="controlling-transport-quotas-from-configuration"></a>Controllo delle quote del trasporto dalla configurazione.  
 La configurazione dell'applicazione può impostare le stesse quote del trasporto utilizzate per accedere direttamente alle proprietà in un'associazione. Nei file di configurazione, il nome di una quota del trasporto inizia sempre con una lettera minuscola. La proprietà `CloseTimeout` in un'associazione corrisponde all'impostazione `closeTimeout` nella configurazione e la proprietà `MaxConnections` in un'associazione corrisponde all'impostazione `maxConnections` nella configurazione.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>
- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
- <xref:System.ServiceModel.Channels.TcpTransportBindingElement>
- <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>
- <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>
- <xref:System.ServiceModel.Channels.TransportBindingElement>

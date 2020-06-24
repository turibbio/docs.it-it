---
title: 'Procedura: creare un contratto duplex'
description: Informazioni su come creare un contratto duplex, che consente a client e server WCF di comunicare tra loro in modo indipendente. In entrambi i casi è possibile avviare chiamate all'altra.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- duplex contracts [WCF]
ms.assetid: 500a75b6-998a-47d5-8e3b-24e3aba2a434
ms.openlocfilehash: 9320e5b36b8faba3602fbe1df1b95c05dcc7fa7e
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247091"
---
# <a name="how-to-create-a-duplex-contract"></a>Procedura: creare un contratto duplex
In questo argomento vengono illustrati i passaggi di base per creare metodi che utilizzano un contratto duplex (bidirezionale). Un contratto duplex consente ai client e ai server di comunicare tra loro in modo indipendente, affinché siano entrambi in grado di effettuare chiamate all'altro. Il contratto duplex è uno dei tre modelli di messaggi disponibili per i servizi Windows Communication Foundation (WCF). Gli altri due modelli sono il modello unidirezionale e il modello request/reply. Un contratto duplex è costituito da due contratti unidirezionali tra il client e il server e non richiede che le chiamate al metodo siano correlate. Utilizzare questo tipo di contratto quando il servizio deve richiedere al client ulteriori informazioni o generare in modo esplicito eventi sul client. Per ulteriori informazioni sulla creazione di un'applicazione client per un contratto duplex, vedere [procedura: accedere ai servizi con un contratto duplex](how-to-access-services-with-a-duplex-contract.md). Per un esempio funzionante, vedere l'esempio [duplex](../samples/duplex.md) .  
  
### <a name="to-create-a-duplex-contract"></a>Per creare un contratto duplex  
  
1. Creare l'interfaccia che rappresenta il lato server del contratto duplex.  
  
2. Applicare la classe <xref:System.ServiceModel.ServiceContractAttribute> all'interfaccia.  
  
     [!code-csharp[S_WS_DualHttp#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#3)]
     [!code-vb[S_WS_DualHttp#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#3)]  
  
3. Dichiarare le firme del metodo nell'interfaccia.  
  
4. Applicare la classe <xref:System.ServiceModel.OperationContractAttribute> a ogni firma del metodo che deve essere parte del contratto pubblico.  
  
5. Creare l'interfaccia di callback che definisce il set di operazioni che il servizio può richiamare nel client.  
  
     [!code-csharp[S_WS_DualHttp#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#4)]
     [!code-vb[S_WS_DualHttp#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#4)]  
  
6. Dichiarare le firme del metodo nell'interfaccia di callback.  
  
7. Applicare la classe <xref:System.ServiceModel.OperationContractAttribute> a ogni firma del metodo che deve essere parte del contratto pubblico.  
  
8. Collegare le due interfacce in un contratto duplex impostando la proprietà <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A> nell'interfaccia primaria sul tipo dell'interfaccia di callback.  
  
### <a name="to-call-methods-on-the-client"></a>Per chiamare i metodi nel client.  
  
1. Nell'implementazione del servizio del contratto primario, dichiarare una variabile per l'interfaccia di callback.  
  
2. Impostare la variabile sul riferimento dell'oggetto restituito dal metodo <xref:System.ServiceModel.OperationContext.GetCallbackChannel%2A> della classe <xref:System.ServiceModel.OperationContext>.  
  
     [!code-csharp[S_WS_DualHttp#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#1)]
     [!code-vb[S_WS_DualHttp#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#1)]  
  
     [!code-csharp[S_WS_DualHttp#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#2)]
     [!code-vb[S_WS_DualHttp#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#2)]  
  
3. Chiamare i metodi definiti dall'interfaccia di callback.  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene illustrata la comunicazione duplex. Il contratto del servizio contiene le operazioni del servizio per spostarsi avanti e indietro. Il contratto del client contiene un'operazione del servizio per segnalare la sua posizione.  
  
 [!code-csharp[S_WS_DualHttp#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#5)]
 [!code-vb[S_WS_DualHttp#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#5)]  
  
- L'applicazione degli attributi <xref:System.ServiceModel.ServiceContractAttribute> e <xref:System.ServiceModel.OperationContractAttribute> consente di generare automaticamente le definizioni del contratto di servizio nel linguaggio di descrizione dei servizi Web (WSDL, Web Services Description Language).  
  
- Utilizzare lo [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) per recuperare il documento WSDL e (facoltativo) il codice e la configurazione di un client.  
  
- Gli endpoint che espongono servizi duplex devono essere protetti. Quando un servizio riceve un messaggio duplex, analizza l'elemento ReplyTo contenuto nel messaggio in arrivo per stabilire dove inviare la replica. Se il canale non è protetto, un client non attendibile potrebbe inviare un messaggio dannoso con un elemento ReplyTo del computer di destinazione, il che comporta un Denial of Service (DoS) del computer di destinazione. Con i messaggi request/reply normali, questo non è un problema, perché ReplyTo viene ignorato e la risposta viene inviata sul canale sul quale è arrivato il messaggio originale.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [Procedura: accedere ai servizi con un contratto duplex](how-to-access-services-with-a-duplex-contract.md)
- [Duplex](../samples/duplex.md)
- [Progettazione e implementazione di servizi](../designing-and-implementing-services.md)
- [Procedura: Definire un contratto di servizio](../how-to-define-a-wcf-service-contract.md)
- [Sessione](../samples/session.md)

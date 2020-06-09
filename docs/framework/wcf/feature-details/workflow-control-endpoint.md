---
title: Endpoint di controllo del flusso di lavoro
ms.date: 03/30/2017
ms.assetid: 1b883334-1590-4fbb-b0d6-65197efe0700
ms.openlocfilehash: 91923129235a596e4fa19a8e5982845a25db9712
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594920"
---
# <a name="workflow-control-endpoint"></a>Endpoint di controllo del flusso di lavoro
L'endpoint di controllo del flusso di lavoro consente agli sviluppatori di chiamare operazioni di controllo per controllare in remoto le istanze del flusso di lavoro ospitate utilizzando <xref:System.ServiceModel.Activities.WorkflowServiceHost>. Questa funzionalità può essere utilizzata per eseguire operazioni di controllo a livello di codice, quali la sospensione, la ripresa e la terminazione.  
  
> [!WARNING]
> Se si utilizza l'endpoint di controllo del flusso di lavoro all'interno di una transazione e il flusso di lavoro controllato contiene un' <xref:System.Activities.Statements.Persist> attività, l'istanza del flusso di lavoro si bloccherà fino al timeout della transazione.  
  
## <a name="workflow-instance-management"></a>Gestione delle istanze di flusso di lavoro  
 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] definisce un nuovo contratto denominato <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement>. Questo contratto definisce una serie di operazioni che consentono di controllare in remoto istanze del flusso di lavoro di controllo ospitate da <xref:System.ServiceModel.Activities.WorkflowServiceHost>. <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> è un endpoint standard che fornisce un'implementazione del contratto <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement>. <xref:System.ServiceModel.Activities.WorkflowControlClient> è una classe utilizzata per inviare le operazioni di controllo a <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>.  
  
 Le istanze del flusso di lavoro possono essere in uno dei seguenti stati:  
  
 Attivo  
 Lo stato di un'istanza del flusso di lavoro prima che raggiunga lo stato completato e quando non si trova nello stato sospeso. In questo stato, l'istanza del flusso di lavoro è in esecuzione ed elabora messaggi dell'applicazione.  
  
 Suspended  
 In questo stato, l'istanza del flusso di lavoro non è in esecuzione neppure se sono presenti attività non ancora in esecuzione o parzialmente in esecuzione.  
  
 Completato  
 Lo stato finale dell'istanza di un flusso di lavoro. L'istanza del flusso di lavoro non può essere in esecuzione dopo avere raggiunto lo stato completato.  
  
## <a name="iworkflowinstancemanagement"></a>IWorkflowInstanceManagement  
 L'interfaccia <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> definisce un set di operazioni di controllo con versioni sincrone e asincrone. Le versioni transazionali richiedono l'utilizzo di un'associazione in grado di riconoscere le transazioni. Nella tabella riportata di seguito vengono elencate le operazioni di controllo supportate.  
  
|Operazione di controllo|Descrizione|  
|-----------------------|-----------------|  
|Interruzione|Interrompe in modo forzato l'esecuzione dell'istanza del flusso di lavoro.|  
|Annulla|Esegue il passaggio di un'istanza del flusso di lavoro dallo stato attivo o sospeso allo stato completato.|  
|Esegui|Fornisce la possibilità di esecuzione di un'istanza del flusso di lavoro.|  
|Sospendi|Esegue il passaggio di un'istanza del flusso di lavoro dallo stato attivo allo stato sospeso.|  
|Terminazione|Esegue il passaggio di un'istanza del flusso di lavoro dallo stato attivo o sospeso allo stato completato.|  
|Unsuspend|Esegue il passaggio di un'istanza del flusso di lavoro dallo stato sospeso allo stato attivo.|  
|TransactedCancel|Esegue l'operazione Cancel in una transazione (propagata dal client o creata in locale). Se il sistema gestisce lo stato durevole dell'istanza del flusso di lavoro, quest'ultima deve essere resa persistente durante l'esecuzione di questa operazione.|  
|TransactedRun|Esegue l'operazione Run in una transazione (propagata dal client o creata in locale). Se il sistema gestisce lo stato durevole dell'istanza del flusso di lavoro, quest'ultima deve essere resa persistente durante l'esecuzione di questa operazione.|  
|TransactedSuspend|Esegue l'operazione Suspend in una transazione (propagata dal client o creata in locale). Se il sistema gestisce lo stato durevole dell'istanza del flusso di lavoro, quest'ultima deve essere resa persistente durante l'esecuzione di questa operazione.|  
|TransactedTerminate|Esegue l'operazione Terminate in una transazione (propagata dal client o creata in locale). Se il sistema gestisce lo stato durevole dell'istanza del flusso di lavoro, quest'ultima deve essere resa persistente durante l'esecuzione di questa operazione.|  
|TransactedUnsuspend|Esegue l'operazione Unsuspend in una transazione (propagata dal client o creata in locale). Se il sistema gestisce lo stato durevole dell'istanza del flusso di lavoro, quest'ultima deve essere resa persistente durante l'esecuzione di questa operazione.|  
  
 Il contratto <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> non fornisce il modo di creare una nuova istanza del flusso di lavoro, ma solo di gestire istanze del flusso di lavoro esistenti. Per ulteriori informazioni sulla creazione di una nuova istanza del flusso di lavoro in modalità remota, vedere [Estensibilità host del servizio flusso di lavoro](workflow-service-host-extensibility.md).  
  
## <a name="workflowcontrolendpoint"></a>WorkflowControlEndpoint  
 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> è un endpoint standard con un contratto fisso, <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement>. Se aggiunto a un'istanza di <xref:System.ServiceModel.Activities.WorkflowServiceHost>, questo endpoint può essere quindi utilizzato per inviare operazioni di comando a qualsiasi istanza del flusso di lavoro ospitata dall'istanza dell'host. Per altre informazioni sugli endpoint standard, vedere [endpoint standard](standard-endpoints.md).  
  
## <a name="workflowcontrolclient"></a>WorkflowControlClient  
 <xref:System.ServiceModel.Activities.WorkflowControlClient> è una classe che consente di inviare messaggi del controllo a un <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> su un <xref:System.ServiceModel.Activities.WorkflowServiceHost>. Contiene un metodo per ogni operazione supportata dal contratto <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement>, ad eccezione delle operazioni transazionali. <xref:System.ServiceModel.Activities.WorkflowControlClient> utilizza la transazione di ambiente per determinare se utilizzare un'operazione transazionale.

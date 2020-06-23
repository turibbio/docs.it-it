---
title: Configurazione semplificata per servizi WCF
description: Informazioni su come implementare e configurare un servizio e un client tipici con WCF. Il servizio comunica utilizzando un endpoint specificato in un file di configurazione.
ms.date: 03/30/2017
ms.assetid: 1e39ec25-18a3-4fdc-b6a3-9dfafbd60112
ms.openlocfilehash: 46a0c878b29de34219413a508799ddaddf507dd8
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246220"
---
# <a name="simplified-configuration-for-wcf-services"></a>Configurazione semplificata per servizi WCF
In questo esempio viene illustrato come implementare e configurare un servizio e un client tipici utilizzando Windows Communication Foundation (WCF). Questo esempio è la base per tutti gli altri esempi di tecnologia di base.  
  
 Questo servizio, che espone un endpoint per la comunicazione con il servizio, usa la configurazione semplificata in .NET Framework 4. Prima del .NET Framework 4, l'endpoint viene in genere definito in un file di configurazione (Web.config), come illustrato nell'esempio di codice di configurazione seguente.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<!-- Copyright ©) Microsoft Corporation.  All Rights Reserved. -->  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceMetadata httpGetEnabled="True"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service name="Microsoft.Samples.GettingStarted.CalculatorService"  
               behaviorConfiguration="CalculatorServiceBehavior">  
        <endpoint address="" binding="basicHttpBinding" contract="ICalculator"/>  
        <endpoint address="mex" binding="mexHttpBinding" contract="IMetadataExchange"/>  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
 In .NET Framework 4, l' `<service>` elemento è facoltativo. Quando un servizio non definisce alcun endpoint, al servizio viene aggiunto un endpoint per ogni indirizzo di base e contratto implementato. L'indirizzo di base viene aggiunto al nome del contratto per determinare l'endpoint e l'associazione è determinata dallo schema dell'indirizzo. Nell'esempio di codice seguente viene illustrato un file di configurazione semplificato. Come configurato, è possibile accedere al servizio `http://localhost/servicemodelsamples/service.svc` da un client nello stesso computer. Affinché i client presenti nei computer remoti accedano al servizio, è necessario specificare un nome di dominio completo anziché localhost. Per impostazione predefinita, il servizio non espone metadati. In quanto tale, il servizio attiva il comportamento <xref:System.ServiceModel.Description.ServiceMetadataBehavior>.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<!-- Copyright © Microsoft Corporation.  All Rights Reserved. -->  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <serviceMetadata httpGetEnabled="True"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
### <a name="to-use-this-sample"></a>Per usare questo esempio  
  
1. Assicurarsi di avere eseguito la [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Per compilare la soluzione, seguire le istruzioni riportate in [compilazione degli esempi di Windows Communication Foundation](building-the-samples.md).  
  
3. Eseguire l'esempio attenendosi ai passaggi seguenti:  
  
    1. Fare clic con il pulsante destro del mouse sul progetto di **servizio** e selezionare **Imposta come progetto di avvio**, quindi premere **CTRL + F5**.  
  
    2. Attendere l'output della console che conferma che il servizio è in esecuzione.  
  
    3. Fare clic con il pulsante destro del mouse sul progetto **client** e selezionare **Imposta come progetto di avvio**, quindi premere **CTRL + F5**.  
  
> [!IMPORTANT]
> È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente (impostazione predefinita) prima di continuare.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) ed [!INCLUDE[wf1](../../../../includes/wf1-md.md)] esempi. Questo esempio si trova nella directory seguente.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\ConfigSimplificationIn40`  
  
## <a name="see-also"></a>Vedere anche

- [Gestione](https://docs.microsoft.com/previous-versions/appfabric/ff383405(v=azure.10))
- [Configurazione semplificata](../simplified-configuration.md)

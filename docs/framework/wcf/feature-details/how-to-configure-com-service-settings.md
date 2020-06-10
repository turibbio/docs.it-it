---
title: 'Procedura: configurare le impostazioni del servizio COM+'
ms.date: 03/30/2017
helpviewer_keywords:
- COM+ [WCF], configuring service settings
ms.assetid: f42a55a8-3af8-4394-9fdd-bf12a93780eb
ms.openlocfilehash: 3fb4b31038845d223248e72d32b3e7413f2aef63
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597176"
---
# <a name="how-to-configure-com-service-settings"></a>Procedura: configurare le impostazioni del servizio COM+
Quando l'interfaccia di un'applicazione viene aggiunta o rimossa usando lo strumento di configurazione del servizio COM+, la configurazione del servizio Web viene aggiornata nel file di configurazione dell'applicazione. In modalità hosted COM+, il file Application. config si trova nella directory radice dell'applicazione (%programmi%\COMPlus Applications Applications \\ {AppID} è l'impostazione predefinita). In entrambe le modalità di hosting Web il file Web.config è posizionato nella directory vroot specificata.  
  
> [!NOTE]
> Per evitare la manomissione dei messaggi tra un client e un server è necessario firmare i messaggi. Inoltre, per evitare la diffusione di informazioni dai messaggi scambiati tra un client e un server è necessario usare la crittografia a livello di messaggio o di trasporto. Come per i servizi Windows Communication Foundation (WCF), è consigliabile usare la limitazione delle richieste per limitare il numero di chiamate simultanee, connessioni, istanze e operazioni in sospeso. Ciò consente di evitare un utilizzo eccessivo di risorse. Il comportamento della limitazione delle richieste viene specificato tramite impostazioni del file di configurazione del servizio.  
  
## <a name="example"></a>Esempio  
 Si consideri un componente che implementa l'interfaccia seguente:  
  
```csharp
[Guid("C551FBA9-E3AA-4272-8C2A-84BD8D290AC7")]  
public interface IFinances  
{  
    string Debit(string accountNo, double amount);  
    string Credit(string accountNo, double amount);  
}  
```  
  
 Se il componente viene esposto come un servizio Web, il contratto di servizio corrispondente che viene esposto, e al quale si devono conformare i client, è il seguente:  
  
```csharp
[ServiceContract(Session = true,  
Namespace = "http://tempuri.org/C551FBA9-E3AA-4272-8C2A-84BD8D290AC7",  
Name = "IFinances")]  
public interface IFinancesContract : IDisposable  
{  
    [OperationContract]  
    string Debit(string accountNo, double amount);  
    [OperationContract]  
    string Credit(string accountNo, double amount);  
}  
```  
  
> [!NOTE]
> L'IID fa parte dello spazio dei nomi iniziale per il contratto.  
  
 Le applicazioni client che usano questo servizio dovrebbero essere conformi a questo contratto, nonché usare un'associazione che sia compatibile con quella specificata nella configurazione dell'applicazione.  
  
 Nell'esempio di codice seguente viene illustrato un file di configurazione predefinito. Essendo un servizio Web Windows Communication Foundation (WCF), è conforme allo schema di configurazione del modello di servizio standard e può essere modificato in modo analogo ad altri file di configurazione dei servizi WCF.  
  
 Modifiche tipiche includono:  
  
- Modifica dell'indirizzo endpoint dal modulo ApplicationName/ComponentName/InterfaceName predefinito in un modulo maggiormente utilizzabile.  
  
- Modifica dello spazio dei nomi del servizio dal `http://tempuri.org/InterfaceID` modulo predefinito a un form più pertinente.  
  
- Modifica dell'endpoint per l'uso di un'associazione del trasporto differente.  
  
     Nel caso di un servizio COM+ ospitato, per impostazione predefinita viene usato il trasporto tramite named pipe. È comunque possibile usare un trasporto esterno al computer come TCP.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
    <system.serviceModel>  
        <bindings>  
            <netNamedPipeBinding>  
                <binding name="comNonTransactionalBinding" />  
                <binding name="comTransactionalBinding" transactionFlow="true" />  
            </netNamedPipeBinding>  
        </bindings>  
        <comContracts>  
            <comContract contract="{C551FBA9-E3AA-4272-8C2A-84BD8D290AC7}"  
                name="IFinances" namespace="http://tempuri.org/C551FBA9-E3AA-4272-8C2A-84BD8D290AC7"  
                requiresSession="true">  
                <exposedMethods>  
                    <add exposedMethod="Debit" />  
                    <add exposedMethod="Credit" />  
                </exposedMethods>  
            </comContract>  
        </comContracts>  
        <services>  
            <service name="{DCDB24CC-0B19-4534-95CD-FBBFF4D67DD9},{C942B840-AD54-4A44-B5F7-928130980AB9}">  
                <endpoint address="IFinances" binding="netNamedPipeBinding" bindingConfiguration="comNonTransactionalBinding"  
                    contract="{C551FBA9-E3AA-4272-8C2A-84BD8D290AC7}" />  
                <host>  
                    <baseAddresses>  
                        <add baseAddress="net.pipe://localhost/ServiceModelDocSampleApp/ServiceModelDocSample.esFinance" />  
                    </baseAddresses>  
                </host>  
            </service>  
        </services>  
    </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>Vedere anche

- [Integrazione con applicazioni COM+](integrating-with-com-plus-applications.md)

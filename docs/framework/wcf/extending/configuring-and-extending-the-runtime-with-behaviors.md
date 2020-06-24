---
title: Configurazione ed estensione del runtime con i comportamenti
description: Informazioni su come implementare le interfacce di comportamento nelle app WCF e aggiungerle a una descrizione o a un endpoint del servizio, a livello di codice o in un file di configurazione.
ms.date: 03/30/2017
helpviewer_keywords:
- attaching extensions using behaviors [WCF]
ms.assetid: 149b99b6-6eb6-4f45-be22-c967279677d9
ms.openlocfilehash: fc297f593b744d69cb09a33be6816fb646f88b67
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247585"
---
# <a name="configuring-and-extending-the-runtime-with-behaviors"></a>Configurazione ed estensione del runtime con i comportamenti
I comportamenti consentono di modificare il comportamento predefinito e di aggiungere estensioni personalizzate che controllano e convalidano la configurazione del servizio o modificano il comportamento in fase di esecuzione nelle applicazioni client e di servizio Windows Communication Foundation (WCF). In questo argomento vengono descritte le interfacce di comportamento e viene illustrato come implementarle e aggiungerle alla descrizione del servizio (in un'applicazione di servizio) o all'endpoint (in un'applicazione client) a livello di codice o in un file di configurazione. Per ulteriori informazioni sull'utilizzo dei comportamenti forniti dal sistema, vedere [specifica del comportamento](../specifying-service-run-time-behavior.md) in fase di esecuzione del servizio e [specifica del comportamento in fase di esecuzione del client](../specifying-client-run-time-behavior.md).  
  
## <a name="behaviors"></a>Comportamenti  
 I tipi di comportamento vengono aggiunti agli oggetti descrizione del servizio o dell'endpoint di servizio (rispettivamente sul servizio o sul client) prima che tali oggetti vengano utilizzati da Windows Communication Foundation (WCF) per creare un runtime che esegue un servizio WCF o un client WCF. Quando questi comportamenti vengono chiamati durante il processo di costruzione del runtime, saranno quindi in grado di accedere alle proprietà e ai metodi runtime che modificano il runtime costruito dal contratto, dalle associazioni e dagli indirizzi.  
  
### <a name="behavior-methods"></a>Metodi di comportamento  
 Tutti i comportamenti dispongono di un metodo `AddBindingParameters`, un metodo `ApplyDispatchBehavior`, un metodo `Validate` e un metodo `ApplyClientBehavior` con un'eccezione: poiché l'interfaccia <xref:System.ServiceModel.Description.IServiceBehavior> non può essere eseguita in un client, non implementa `ApplyClientBehavior`.  
  
- Utilizzare il metodo `AddBindingParameters` per modificare o aggiungere oggetti personalizzati in una raccolta a cui le associazioni personalizzate potranno accedere per utilizzarli quando viene costruito il runtime. Ad esempio, è in questo modo che vengono specificati i requisiti di protezione che influiscono sulla modalità di costruzione del canale, ma che non sono noti allo sviluppatore del canale.  
  
- Utilizzare il metodo `Validate` per esaminare la struttura di descrizione e l'oggetto runtime corrispondente al fine di garantirne la conformità a un set di criteri.  
  
- Utilizzare i metodi `ApplyDispatchBehavior` e `ApplyClientBehavior` per esaminare la struttura di descrizione e modificare il runtime per un particolare ambito sul servizio o sul client. È inoltre possibile inserire oggetti di estensione.  
  
    > [!NOTE]
    > Anche se in questi tre metodi viene fornita una struttura di descrizione, essa è utilizzabile solo per attività di esame. Se un albero di descrizione viene modificato, il comportamento è indefinito.  
  
 L'accesso alle proprietà che possono modificate e alle interfacce di personalizzazione che è possibile implementare avviene attraverso le classi runtime del servizio e del client. I tipi di servizio sono rappresentati dalle classi <xref:System.ServiceModel.Dispatcher.DispatchRuntime> e <xref:System.ServiceModel.Dispatcher.DispatchOperation>. I tipi di client sono rappresentati dalle classi <xref:System.ServiceModel.Dispatcher.ClientRuntime> e <xref:System.ServiceModel.Dispatcher.ClientOperation>. Le classi <xref:System.ServiceModel.Dispatcher.ClientRuntime> e <xref:System.ServiceModel.Dispatcher.DispatchRuntime> sono i punti di ingresso dell'estendibilità per accedere rispettivamente alle proprietà runtime e alle raccolte di estensioni a livello di client e del servizio. Analogamente, le classi <xref:System.ServiceModel.Dispatcher.ClientOperation> e <xref:System.ServiceModel.Dispatcher.DispatchOperation> espongono rispettivamente proprietà runtime e raccolte di estensioni dell'operazione del client e del servizio. È tuttavia possibile accedere all'oggetto runtime di ambito più ampio dall'oggetto runtime dell'operazione e viceversa se necessario.  
  
> [!NOTE]
> Per informazioni sulle proprietà di runtime e sui tipi di estensioni che è possibile usare per modificare il comportamento di esecuzione di un client, vedere [estensione dei client](extending-clients.md). Per informazioni sulle proprietà di runtime e sui tipi di estensioni che è possibile usare per modificare il comportamento di esecuzione di un dispatcher di servizi, vedere [estensione](extending-dispatchers.md)di Dispatcher.  
  
 La maggior parte degli utenti WCF non interagisce direttamente con il Runtime. usano invece costrutti di base del modello di programmazione come endpoint, contratti, Binding, indirizzi e attributi di comportamento per classi o comportamenti nei file di configurazione. Questi costrutti costituiscono la *struttura di descrizione*, ovvero la specifica completa per la costruzione di un runtime per supportare un servizio o un client descritto dalla struttura di descrizione.  
  
 In WCF sono disponibili quattro tipi di comportamento:  
  
- I comportamenti del servizio (tipi <xref:System.ServiceModel.Description.IServiceBehavior>) consentono la personalizzazione del runtime dell'intero servizio, incluso <xref:System.ServiceModel.ServiceHostBase>.  
  
- I comportamenti dell'endpoint (tipi <xref:System.ServiceModel.Description.IEndpointBehavior>) consentono la personalizzazione degli endpoint del servizio e dei relativi oggetti <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> associati.  
  
- I comportamenti del contratto (tipi <xref:System.ServiceModel.Description.IContractBehavior>) consentono la personalizzazione di entrambe le classi <xref:System.ServiceModel.Dispatcher.ClientRuntime> e <xref:System.ServiceModel.Dispatcher.DispatchRuntime> rispettivamente nelle applicazioni client e di servizi.  
  
- I comportamenti dell'operazione (tipi <xref:System.ServiceModel.Description.IOperationBehavior>) consentono la personalizzazione delle classi <xref:System.ServiceModel.Dispatcher.ClientOperation> e <xref:System.ServiceModel.Dispatcher.DispatchOperation> nel client e nel servizio.  
  
 È possibile aggiungere questi comportamenti ai vari oggetti di descrizione implementando attributi personalizzati, utilizzando file di configurazione dell'applicazione, oppure è possibile aggiungerli direttamente alla raccolta di comportamenti sull'oggetto di descrizione appropriato. Essi devono tuttavia essere aggiunti a un oggetto di descrizione del servizio o dell'endpoint del servizio prima della chiamata a <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> su <xref:System.ServiceModel.ServiceHost> o <xref:System.ServiceModel.ChannelFactory%601>.  
  
### <a name="behavior-scopes"></a>Ambiti dei comportamenti  
 Sono disponibili quattro tipi di comportamento, ognuno dei quali corrisponde a un particolare ambito di accesso runtime.  
  
#### <a name="service-behaviors"></a>Comportamenti del servizio  
 I comportamenti del servizio, che implementano l'interfaccia <xref:System.ServiceModel.Description.IServiceBehavior>, costituiscono il meccanismo principale attraverso cui è possibile modificare il runtime dell'intero servizio. Esistono tre meccanismi per aggiungere tali comportamenti a un servizio.  
  
1. Utilizzo di un attributo sulla classe del servizio.  Quando viene costruito un oggetto <xref:System.ServiceModel.ServiceHost>, l'implementazione di <xref:System.ServiceModel.ServiceHost> utilizza la riflessione per individuare il set di attributi sul tipo del servizio. Se questi attributi sono implementazioni di <xref:System.ServiceModel.Description.IServiceBehavior>, essi vengono aggiunti alla raccolta di comportamenti su <xref:System.ServiceModel.Description.ServiceDescription>. In questo modo tali comportamenti possono partecipare alla costruzione del runtime del servizio.  
  
2. Aggiunta del comportamento alla raccolta di comportamenti su <xref:System.ServiceModel.Description.ServiceDescription> a livello di codice. Per questa operazione utilizzare le righe di codice seguenti:  
  
    ```csharp
    ServiceHost host = new ServiceHost(/* Parameters */);  
    host.Description.Behaviors.Add(/* Service Behavior */);  
    ```  
  
3. Implementazione di una classe <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> personalizzata che estende la configurazione. In questo modo viene consentito l'utilizzo del comportamento del servizio dai file di configurazione dell'applicazione.  
  
 Esempi di comportamenti del servizio in WCF includono l' <xref:System.ServiceModel.ServiceBehaviorAttribute> attributo, <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> e il <xref:System.ServiceModel.Description.ServiceMetadataBehavior> comportamento.  
  
#### <a name="contract-behaviors"></a>Comportamenti del contratto  
 I comportamenti del contratto, che implementano l'interfaccia <xref:System.ServiceModel.Description.IContractBehavior>, vengono utilizzati per estendere il runtime del client e del servizio in un contratto.  
  
 Esistono due meccanismi per aggiungere tali comportamenti a un contratto.  Il primo consiste nella creazione di un attributo personalizzato da utilizzare sull'interfaccia del contratto. Quando un'interfaccia del contratto viene passata a un oggetto <xref:System.ServiceModel.ServiceHost> o <xref:System.ServiceModel.ChannelFactory%601> , WCF esamina gli attributi sull'interfaccia. Se gli attributi sono implementazioni di <xref:System.ServiceModel.Description.IContractBehavior>, essi vengono aggiunti alla raccolta di comportamenti sulla classe <xref:System.ServiceModel.Description.ContractDescription?displayProperty=nameWithType> creata per tale interfaccia.  
  
 È inoltre possibile implementare l'interfaccia <xref:System.ServiceModel.Description.IContractBehaviorAttribute?displayProperty=nameWithType> sull'attributo del comportamento del contratto personalizzato. In questo caso, il comportamento è il seguente quando applicato a:  
  
 •Un'interfaccia del contratto. In questo caso, il comportamento viene applicato a tutti i contratti di quel tipo in qualsiasi endpoint e WCF ignora il valore della <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A?displayProperty=nameWithType> Proprietà.  
  
 •Una classe del servizio. In questo caso, il comportamento viene applicato solo agli endpoint il cui contratto corrisponde al valore della proprietà <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A>.  
  
 •Una classe di callback. In questo caso, il comportamento viene applicato all'endpoint del client duplex e WCF ignora il valore della <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A> Proprietà.  
  
 Il secondo meccanismo consiste nell'aggiunta del comportamento alla raccolta di comportamenti su una classe <xref:System.ServiceModel.Description.ContractDescription>.  
  
 Esempi di comportamenti del contratto in WCF includono l' <xref:System.ServiceModel.DeliveryRequirementsAttribute?displayProperty=nameWithType> attributo. Per ulteriori informazioni e per un esempio, vedere l'argomento di riferimento.  
  
#### <a name="endpoint-behaviors"></a>Comportamenti dell'endpoint  
 I comportamenti dell'endpoint, che implementano l'interfaccia <xref:System.ServiceModel.Description.IEndpointBehavior>, costituiscono il meccanismo principale attraverso cui è possibile modificare il runtime dell'intero servizio o del client per un endpoint specifico.  
  
 Esistono due meccanismi per aggiungere tali comportamenti a un servizio.  
  
1. Aggiunta del comportamento alla proprietà <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A>.  
  
2. Implementazione di una classe <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> personalizzata che estende la configurazione.  
  
 Per ulteriori informazioni e per un esempio, vedere l'argomento di riferimento.  
  
#### <a name="operation-behaviors"></a>Comportamenti dell'operazione  
 I comportamenti dell'operazione, che implementano l'interfaccia <xref:System.ServiceModel.Description.IOperationBehavior>, vengono utilizzati per estendere il runtime del client e del servizio per ogni operazione.  
  
 Esistono due meccanismi per aggiungere tali comportamenti a un'operazione. Il primo meccanismo consiste nella creazione di un attributo personalizzato da utilizzare sul metodo che modella l'operazione. Quando un'operazione viene aggiunta a o a <xref:System.ServiceModel.ServiceHost> <xref:System.ServiceModel.ChannelFactory> , WCF aggiunge tutti <xref:System.ServiceModel.Description.IOperationBehavior> gli attributi alla raccolta dei comportamenti nell'oggetto <xref:System.ServiceModel.Description.OperationDescription> creato per l'operazione.  
  
 Il secondo meccanismo consiste nell'aggiunta diretta del comportamento alla raccolta di comportamenti su una classe <xref:System.ServiceModel.Description.OperationDescription> costruita.  
  
 Esempi di comportamenti dell'operazione in WCF includono <xref:System.ServiceModel.OperationBehaviorAttribute> e <xref:System.ServiceModel.TransactionFlowAttribute> .  
  
 Per ulteriori informazioni e per un esempio, vedere l'argomento di riferimento.  
  
### <a name="using-configuration-to-create-behaviors"></a>Utilizzo della configurazione per creare comportamenti  
 I comportamenti del servizio, dell'endpoint e del contratto possono essere progettati in modo da essere specificati nel codice o mediante attributi; ma solo i comportamenti del servizio e dell'endpoint possono essere configurati utilizzando file di configurazione dell'applicazione o Web. L'esposizione dei comportamenti mediante attributi consente agli sviluppatori di specificare un comportamento in fase di compilazione che non può essere aggiunto, rimosso o modificato a runtime. Tale sistema è spesso adatto per comportamenti che sono sempre necessari per il corretto funzionamento del servizio, ad esempio i parametri correlati alla transazione passati all'attributo <xref:System.ServiceModel.ServiceBehaviorAttribute?displayProperty=nameWithType>). L'esposizione dei comportamenti mediante la configurazione consente agli sviluppatori di lasciare la specifica e la configurazione di tali comportamenti a coloro che distribuiscono il servizio. Tale sistema è adatto per comportamenti che rappresentano componenti facoltativi o altra configurazione specifica della distribuzione, ad esempio se i metadati vengono esposti per il servizio o la particolare configurazione dell'autorizzazione per un servizio.  
  
> [!NOTE]
> È inoltre possibile utilizzare i comportamenti che supportano la configurazione per imporre criteri dell'applicazione aziendale inserendoli nel file di configurazione machine.config e bloccando tali elementi. Per una descrizione e un esempio, vedere [procedura: bloccare gli endpoint nell'organizzazione](how-to-lock-down-endpoints-in-the-enterprise.md).  
  
 Per esporre un comportamento mediante la configurazione, un sviluppatore deve creare una classe derivata di <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> e quindi registrare tale estensione nella configurazione.  
  
 Nell'esempio di codice seguente viene illustrato come un'interfaccia <xref:System.ServiceModel.Description.IEndpointBehavior> implementa <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>:  
  
```csharp
// BehaviorExtensionElement members  
public override Type BehaviorType  
{  
  get { return typeof(EndpointBehaviorMessageInspector); }  
}  
  
protected override object CreateBehavior()  
{  
  return new EndpointBehaviorMessageInspector();  
}  
```  
  
 Affinché il sistema di configurazione carichi un elemento <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> personalizzato, questo deve essere registrato come estensione. Nell'esempio di codice seguente viene illustrato il file di configurazione per il comportamento dell'endpoint precedente.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service
        name="Microsoft.WCF.Documentation.SampleService"  
        behaviorConfiguration="metadataSupport"  
      >  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost:8080/ServiceMetadata" />  
          </baseAddresses>  
        </host>  
        <endpoint  
          address="/SampleService"  
          binding="wsHttpBinding"  
          behaviorConfiguration="withMessageInspector"
          contract="Microsoft.WCF.Documentation.ISampleService"  
        />  
        <endpoint  
           address="mex"  
           binding="mexHttpBinding"  
           contract="IMetadataExchange"  
        />  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
      <behavior name="metadataSupport">  
        <serviceMetadata httpGetEnabled="true" httpGetUrl=""/>  
      </behavior>  
      </serviceBehaviors>  
      <endpointBehaviors>  
        <behavior name="withMessageInspector">  
          <endpointMessageInspector />  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <extensions>  
      <behaviorExtensions>  
        <add
          name="endpointMessageInspector"  
          type="Microsoft.WCF.Documentation.EndpointBehaviorMessageInspector, HostApplication, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null"  
        />  
      </behaviorExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
```  
  
 Dove `Microsoft.WCF.Documentation.EndpointBehaviorMessageInspector` è il tipo di estensione di comportamento e `HostApplication` è il nome dell'assembly in cui è stata compilata tale classe.  
  
### <a name="evaluation-order"></a>Ordine di valutazione  
 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> e <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> sono responsabili della compilazione del runtime in base al modello di programmazione e alla descrizione. I comportamenti, come descritto in precedenza, contribuiscono a tale processo di compilazione a livello del servizio, dell'endpoint, del contratto e dell'operazione.  
  
 <xref:System.ServiceModel.ServiceHost> applica i comportamenti nell'ordine seguente:  
  
1. Service  
  
2. Contratto  
  
3. Endpoint  
  
4. Operazione  
  
 All'interno di una raccolta di comportamenti non è garantito alcun ordine.  
  
 <xref:System.ServiceModel.ChannelFactory%601> applica i comportamenti nell'ordine seguente:  
  
1. Contratto  
  
2. Endpoint  
  
3. Operazione  
  
 Anche in questo caso, all'interno di una raccolta di comportamenti non è garantito alcun ordine.  
  
### <a name="adding-behaviors-programmatically"></a>Aggiunta di comportamenti a livello di codice  
 Le proprietà di <xref:System.ServiceModel.Description.ServiceDescription?displayProperty=nameWithType> nell'applicazione del servizio non devono essere modificate successivamente al metodo <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A?displayProperty=nameWithType> su <xref:System.ServiceModel.ServiceHostBase?displayProperty=nameWithType>. Alcuni membri, come la proprietà <xref:System.ServiceModel.ServiceHostBase.Credentials%2A?displayProperty=nameWithType> e i metodi `AddServiceEndpoint` su <xref:System.ServiceModel.ServiceHostBase> e <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType>, generano un'eccezione se vengono modificati dopo questo punto. Altri consentono la modifica, ma il risultato è indefinito.  
  
 Analogamente, sul client i valori <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType> non devono essere modificati dopo la chiamata a <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A> su <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType>. La proprietà <xref:System.ServiceModel.ChannelFactory.Credentials%2A?displayProperty=nameWithType> genera un'eccezione se viene modificata dopo questo punto, ma è possibile modificare senza errore gli altri valori della descrizione client. Il risultato è tuttavia indefinito.  
  
 Per il servizio o per il client, è consigliabile modificare la descrizione prima di chiamare <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A?displayProperty=nameWithType>.  
  
### <a name="inheritance-rules-for-behavior-attributes"></a>Regole di ereditarietà per gli attributi di comportamento  
 Tutti i quattro tipi di comportamento possono essere popolati utilizzando attributi, ovvero i comportamenti del servizio e i comportamenti del contratto. Poiché gli attributi vengono definiti su oggetti gestiti e membri e gli oggetti gestiti e i membri supportano l'ereditarietà, è necessario definire il funzionamento degli attributi di comportamento nel contesto di ereditarietà.  
  
 A livello generale, la regola prevede che per un particolare ambito (ad esempio un servizio, un contratto o un'operazione) vengono applicati tutti gli attributi di comportamento nella gerarchia di ereditarietà dell'ambito. Se sono presenti due attributi di comportamento dello stesso tipo, viene utilizzato solo il tipo più derivato.  
  
#### <a name="service-behaviors"></a>Comportamenti del servizio  
 Per una determinata classe del servizio, vengono applicati tutti gli attributi di comportamento del servizio sulla classe e sugli elementi padre della classe. Se lo stesso tipo di attributo viene applicato in più posizioni nella gerarchia di ereditarietà, viene utilizzato il tipo più derivato.  
  
```csharp  
[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Multiple)]  
[AspNetCompatibilityRequirementsAttribute(  
    AspNetCompatibilityRequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]  
public class A { /* … */ }  
  
[ServiceBehavior(InstanceContextMode = InstanceContextMode.Single)]  
public class B : A { /* … */}  
```  
  
 Ad esempio, nel caso precedente, il servizio B finisce con una modalità <xref:System.ServiceModel.InstanceContextMode> paria <xref:System.ServiceModel.InstanceContextMode.Single>, una modalità <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode> pari a <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed> e una modalità <xref:System.ServiceModel.ConcurrencyMode> pari a <xref:System.ServiceModel.ConcurrencyMode.Single>. <xref:System.ServiceModel.ConcurrencyMode> è <xref:System.ServiceModel.ConcurrencyMode.Single>, poiché l'attributo <xref:System.ServiceModel.ServiceBehaviorAttribute> sul servizio B è "più derivato" di quello sul servizio A.  
  
#### <a name="contract-behaviors"></a>Comportamenti del contratto  
 Per un determinato contratto, vengono applicati tutti gli attributi di comportamento del contratto sull'interfaccia e sugli elementi padre dell'interfaccia. Se lo stesso tipo di attributo viene applicato in più posizioni nella gerarchia di ereditarietà, viene utilizzato il tipo più derivato.  
  
#### <a name="operation-behaviors"></a>Comportamenti dell'operazione  
 Se una determinata operazione non esegue l'override di un'operazione astratta o virtuale esistente, non viene applicata alcuna regola di ereditarietà.  
  
 Se un'operazione esegue l'override di un'operazione esistente, vengono applicati tutti gli attributi di comportamento dell'operazione sull'operazione e sugli elementi padre dell'operazione.  Se lo stesso tipo di attributo viene applicato in più posizioni nella gerarchia di ereditarietà, viene utilizzato il tipo più derivato.

---
title: Trasporto UDP
ms.date: 03/30/2017
ms.assetid: 738705de-ad3e-40e0-b363-90305bddb140
ms.openlocfilehash: 3eb7116199cfb23d965918247b74af04d671e79b
ms.sourcegitcommit: 839777281a281684a7e2906dccb3acd7f6a32023
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82141147"
---
# <a name="transport-udp"></a>Trasporto UDP
Nell'esempio di trasporto UDP viene illustrato come implementare unicast e multicast UDP come trasporto WCF (Custom Windows Communication Foundation). Nell'esempio viene descritta la procedura consigliata per la creazione di un trasporto personalizzato in WCF, utilizzando il Framework del canale e le procedure consigliate WCF seguenti. I passaggi per creare un trasporto personalizzato sono i seguenti:  
  
1. Decidere quale [modello di scambio dei messaggi](#MessageExchangePatterns) del canale (IOutputChannel, IInputChannel, IDuplexChannel, IRequestChannel o IReplyChannel) è supportato da ChannelFactory e ChannelListener. Quindi decidere se si supporteranno le variazioni con sessione di tali interfacce.  
  
2. Creare una channel factory e un listener di canale che supportano il modello di scambio dei messaggi.  
  
3. Assicurarsi che eventuali eccezioni specifiche della rete vengano normalizzate nella classe derivata appropriata di <xref:System.ServiceModel.CommunicationException>.  
  
4. Aggiungere un [ \<elemento>di associazione](../../configure-apps/file-schema/wcf/bindings.md) che aggiunge il trasporto personalizzato a uno stack di canali. Per ulteriori informazioni, vedere [aggiunta di un elemento di associazione](#AddingABindingElement).  
  
5. Aggiungere una sezione di estensione degli elementi di associazione per esporre il nuovo elemento di associazione al sistema di configurazione.  
  
6. Aggiungere le estensioni dei metadati per comunicare le funzionalità agli altri endpoint.  
  
7. Aggiungere un'associazione che preconfigura uno stack di elementi di associazione secondo un profilo ben definito. Per ulteriori informazioni, vedere [aggiunta di un'associazione standard](#AddingAStandardBinding).  
  
8. Aggiungere una sezione dell'associazione e un elemento di configurazione dell'associazione per esporre l'associazione al sistema di configurazione. Per ulteriori informazioni, vedere [aggiunta del supporto](#AddingConfigurationSupport)per la configurazione.  
  
<a name="MessageExchangePatterns"></a>
## <a name="message-exchange-patterns"></a>Modelli di scambio dei messaggi  
 Per scrivere un trasporto personalizzato, è necessario innanzitutto stabilire quali modelli di scambio dei messaggi (o MEP, Message Exchange Pattern) sono necessari per il trasporto. Sono disponibili tre modelli di scambio dei messaggi:  
  
- Datagramma (IInputChannel/IOutputChannel)  
  
     Quando si utilizza un modello datagramma, un client invia un messaggio utilizzando uno scambio di tipo "fire and forget". Tale scambio richiede una conferma fuori banda di recapito con esito positivo. Il messaggio potrebbe infatti andare perso durante il transito e non raggiungere mai il servizio. Se l'operazione di invio viene completata correttamente sul lato client, non c'è garanzia che l'endpoint remoto abbia ricevuto il messaggio. Il datagramma è un componente fondamentale per i messaggi, poiché sulla sua base è possibile compilare protocolli propri, tra cui protocolli affidabili e protocolli sicuri. I canali del datagramma del client implementano l'interfaccia <xref:System.ServiceModel.Channels.IOutputChannel>, mentre i canali del datagramma del servizio implementano l'interfaccia <xref:System.ServiceModel.Channels.IInputChannel>.  
  
- Richiesta-risposta (IRequestChannel/IReplyChannel)  
  
     In questo modello di scambio, viene inviato un messaggio e viene ricevuta una risposta. Il modello è costituito da coppie richiesta-risposta. Esempi di chiamate richiesta-risposta sono le chiamate RPC (Remote Procedure Call, chiamata a procedura remota) e le richieste GETs del browser. Questo modello è anche noto come half-duplex. In tale modello, i canali client implementano l'interfaccia <xref:System.ServiceModel.Channels.IRequestChannel>, mentre i canali del servizio implementano l'interfaccia <xref:System.ServiceModel.Channels.IReplyChannel>.  
  
- Duplex (IDuplexChannel)  
  
     Il modello di scambio duplex consente l'invio di un numero arbitrario di messaggi da parte di un client e la ricezione in qualsiasi ordine. Tale modello è simile a una conversazione telefonica, in cui ogni parola pronunciata è un messaggio. Poiché in questo modello i due lati possono entrambi inviare e ricevere messaggi, l'interfaccia implementata dai canali client e del servizio è <xref:System.ServiceModel.Channels.IDuplexChannel>.  
  
 Ognuno di questi modelli può inoltre supportare sessioni. La funzionalità aggiuntiva fornita da un canale con supporto della sessione è che correla tutti i messaggi inviati e ricevuti su un canale. Il modello richiesta-risposta è una sessione autonoma a due messaggi, poiché la richiesta e la risposta sono correlate. Il modello request/response che supporta sessioni implica invece che tutte le coppie request/response nel canale siano correlate le une alle altre. Gli dà un totale di sei modelli tra cui scegliere: Datagramma, Richiesta-risposta, Duplex, Datagramma con sessioni, Richiesta-Risposta con sessioni e Duplex con sessioni.  
  
> [!NOTE]
> Per il trasporto UDP, l'unico modello di scambio dei messaggi supportato è il datagramma, poiché il protocollo UPD è di tipo "fire and forget".  
  
### <a name="the-icommunicationobject-and-the-wcf-object-lifecycle"></a>Ciclo di vita di  ICommunicationObject e dell'oggetto WCF  
 WCF dispone di una macchina a stati comune utilizzata per gestire il ciclo di vita di <xref:System.ServiceModel.Channels.IChannel>oggetti <xref:System.ServiceModel.Channels.IChannelFactory>quali, <xref:System.ServiceModel.Channels.IChannelListener> e utilizzati per la comunicazione. Ci sono cinque stati in cui questi oggetti di comunicazione possono esistere. Questi stati sono rappresentati dall'enumerazione <xref:System.ServiceModel.CommunicationState> e sono elencati di seguito:  
  
- Creato: questo è lo stato di un oggetto <xref:System.ServiceModel.ICommunicationObject> quando viene creato come istanza. In questo stato non può aver luogo alcun input o output (I/O).  
  
- Apertura: gli oggetti passano a questo stato quando viene chiamato il metodo <xref:System.ServiceModel.ICommunicationObject.Open%2A>. In questa fase le proprietà diventano immutabili e l'input/output può iniziare. Tale transizione è valida solo dallo stato Creato.  
  
- Aperto: gli oggetti passano a questo stato al termine del processo di apertura. Tale transizione è valida solo dallo stato Apertura. In questa fase, l'oggetto è pienamente utilizzabile per il trasferimento.  
  
- Chiusura: gli oggetti passano a questo stato quando viene chiamato il metodo <xref:System.ServiceModel.ICommunicationObject.Close%2A> per un arresto normale. Tale transizione è valida solo dallo stato Aperto.  
  
- Chiuso: gli oggetti con stato Chiuso nono sono più utilizzabili. In generale, la configurazione è ancora accessibile per essere esaminata, ma non può verificarsi nessuna comunicazione. Questo stato è equivalente all'eliminazione.  
  
- Non riuscito: nello stato Non riuscito, gli oggetti sono accessibili per essere esaminati ma non sono più utilizzabili. Quando si verifica un errore irreversibile, l'oggetto passa a questo stato. L'unica transizione valida da questo stato è nello `Closed` stato.  
  
 Ci sono eventi che generano per ogni passaggio di stato. Il metodo <xref:System.ServiceModel.ICommunicationObject.Abort%2A> può essere chiamato in ogni momento, esso fa in modo che l'oggetto passi immediatamente allo stato Chiuso. Una chiamata al metodo <xref:System.ServiceModel.ICommunicationObject.Abort%2A> termina qualsiasi lavoro non finito.  
  
<a name="ChannelAndChannelListener"></a>
## <a name="channel-factory-and-channel-listener"></a>Channel factory e listener del canale  
 Il passaggio successivo per scrivere un trasporto TCP personalizzato consiste nel creare un'implementazione di <xref:System.ServiceModel.Channels.IChannelFactory> per i canali client e di <xref:System.ServiceModel.Channels.IChannelListener> per i canali del servizio. Il livello del canale usa un modello della factory per costruire canali. WCF fornisce helper della classe di base per questo processo.  
  
- La classe <xref:System.ServiceModel.Channels.CommunicationObject> implementa <xref:System.ServiceModel.ICommunicationObject> e attiva la macchina a stati precedentemente descritta nel passaggio 2.

- La <xref:System.ServiceModel.Channels.ChannelManagerBase> classe implementa <xref:System.ServiceModel.Channels.CommunicationObject> e fornisce una classe base unificata per <xref:System.ServiceModel.Channels.ChannelFactoryBase> e <xref:System.ServiceModel.Channels.ChannelListenerBase>. La classe <xref:System.ServiceModel.Channels.ChannelManagerBase> opera unitamente alla classe <xref:System.ServiceModel.Channels.ChannelBase>, una classe di base che implementa l'interfaccia <xref:System.ServiceModel.Channels.IChannel>.  
  
- La <xref:System.ServiceModel.Channels.ChannelFactoryBase> classe implementa <xref:System.ServiceModel.Channels.ChannelManagerBase> e <xref:System.ServiceModel.Channels.IChannelFactory> e consolida gli `CreateChannel` overload in un unico `OnCreateChannel` metodo astratto.  
  
- La <xref:System.ServiceModel.Channels.ChannelListenerBase> classe implementa <xref:System.ServiceModel.Channels.IChannelListener>. Si occupa della gestione dello stato di base.  
  
 In questo esempio, l'implementazione della factory è contenuta in UdpChannelFactory.cs e l'implementazione del listener è contenuta in UdpChannelListener.cs. Le implementazioni di <xref:System.ServiceModel.Channels.IChannel> sono in UdpOutputChannel.cs e UdpInputChannel.cs.  
  
### <a name="the-udp-channel-factory"></a>Channel factory UDP  
 `UdpChannelFactory` deriva da <xref:System.ServiceModel.Channels.ChannelFactoryBase>. L'esempio esegue l'override di <xref:System.ServiceModel.Channels.ChannelFactoryBase.GetProperty%2A> per fornire accesso alla versione del messaggio del codificatore di messaggi. L'esempio esegue inoltre l'override di <xref:System.ServiceModel.Channels.ChannelFactoryBase.OnClose%2A> per chiudere l'istanza di <xref:System.ServiceModel.Channels.BufferManager> quando la macchina a stati esegue la transizione.  
  
#### <a name="the-udp-output-channel"></a>Canale di output UDP  
 `UdpOutputChannel` implementa <xref:System.ServiceModel.Channels.IOutputChannel>. Il costruttore convalida gli argomenti e costruisce un oggetto <xref:System.Net.EndPoint> di destinazione basato sull'elemento <xref:System.ServiceModel.EndpointAddress> che viene passato.  
  
```csharp
this.socket = new Socket(this.remoteEndPoint.AddressFamily, SocketType.Dgram, ProtocolType.Udp);  
```  
  
 Il canale può essere chiuso normalmente o in modo anomalo. Se il canale viene chiuso normalmente, il socket viene chiuso e viene eseguita una chiamata al metodo `OnClose` della classe di base. Se viene generata un'eccezione, l'infrastruttura chiama `Abort` per verificare che il canale sia pulito.  
  
```csharp
this.socket.Close(0);  
```  
  
 Vengono quindi `Send()` implementati `BeginSend()` / `EndSend()`e. In questo modo si ottengono due sezioni principali. Prima serializzare il messaggio in una matrice di byte.  
  
```csharp
ArraySegment<byte> messageBuffer = EncodeMessage(message);  
```  
  
 Inviare quindi i dati risultanti sulla rete.  
  
```csharp
this.socket.SendTo(messageBuffer.Array, messageBuffer.Offset, messageBuffer.Count, SocketFlags.None, this.remoteEndPoint);  
```  
  
### <a name="the-udpchannellistener"></a>Listener canale UDP  
 L' `UdpChannelListener` oggetto implementato dall'esempio deriva dalla <xref:System.ServiceModel.Channels.ChannelListenerBase> classe. Utilizza un solo socket UDP per ricevere datagrammi. Il metodo `OnOpen` riceve dati utilizzando il socket UDP in un ciclo asincrono. I dati vengono quindi convertiti in messaggi utilizzando il sistema di codifica messaggi:  
  
```csharp
message = MessageEncoderFactory.Encoder.ReadMessage(new ArraySegment<byte>(buffer, 0, count), bufferManager);  
```  
  
 Poiché lo stesso canale del datagramma rappresenta messaggi in arrivo da un certo numero di origini, `UdpChannelListener` è un listener singleton. Esiste al massimo un elemento attivo <xref:System.ServiceModel.Channels.IChannel> associato a questo listener alla volta. Nell'esempio ne viene generato un altro solo se un canale restituito dal metodo `AcceptChannel` viene successivamente eliminato. Quando un messaggio viene ricevuto, viene accodato in questo canale singleton.  
  
#### <a name="udpinputchannel"></a>UdpInputChannel  
 La `UdpInputChannel` classe implementa `IInputChannel`. È composta da una coda di messaggi in arrivo popolata dal socket di `UdpChannelListener`. La coda di questi messaggi viene annullata dal metodo `IInputChannel.Receive`.  
  
<a name="AddingABindingElement"></a>
## <a name="adding-a-binding-element"></a>Aggiunta di un elemento di associazione.  
 Ora che le factory e i canali sono compilati, devono essere esposti al runtime di ServiceModel tramite un'associazione. Un'associazione è una raccolta di elementi di associazione che rappresentano lo stack di comunicazione associato a un indirizzo del servizio. Ogni elemento dello stack è rappresentato da un [ \<elemento binding>](../../configure-apps/file-schema/wcf/bindings.md) .  
  
 Nell'esempio, l'elemento di associazione è `UdpTransportBindingElement`, che deriva dalla classe <xref:System.ServiceModel.Channels.TransportBindingElement>. Esso esegue l'override dei metodi seguenti per compilare le factory associate all'associazione.  
  
```csharp
public IChannelFactory<TChannel> BuildChannelFactory<TChannel>(BindingContext context)  
{  
    return (IChannelFactory<TChannel>)(object)new UdpChannelFactory(this, context);  
}  
  
public IChannelListener<TChannel> BuildChannelListener<TChannel>(BindingContext context)  
{  
    return (IChannelListener<TChannel>)(object)new UdpChannelListener(this, context);  
}  
```  
  
 Contiene inoltre membri per duplicare `BindingElement` e restituire lo schema (soap.udp).  
  
## <a name="adding-metadata-support-for-a-transport-binding-element"></a>Aggiunta del supporto dei metadati per un elemento di associazione del trasporto  
 Per essere integrato in un sistema di metadati, il trasporto deve supportare sia l'importazione che l'esportazione di un criterio. In questo modo è possibile generare client dell'associazione tramite lo [strumento ServiceModel Metadata Utility Tool (Svcutil. exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  
  
### <a name="adding-wsdl-support"></a>Aggiunta di supporto WSDL  
 L'elemento di associazione del trasporto in un'associazione è responsabile dell'esportazione e importazione delle informazioni di indirizzamento nei metadati. Quando si utilizza un'associazione SOAP, l'elemento di associazione del trasporto deve esportare anche un URI di trasporto corretto nei metadati.  
  
#### <a name="wsdl-export"></a>Esportazione WSDL  
 Per esportare informazioni di indirizzamento, `UdpTransportBindingElement` implementa l'interfaccia `IWsdlExportExtension`. Il metodo `ExportEndpoint` aggiunge le informazioni di indirizzamento corrette alla porta WSDL.  
  
```csharp
if (context.WsdlPort != null)  
{  
    AddAddressToWsdlPort(context.WsdlPort, context.Endpoint.Address, encodingBindingElement.MessageVersion.Addressing);  
}  
```  
  
 L'implementazione di `UdpTransportBindingElement` del metodo `ExportEndpoint` esporta anche un URI di trasporto quando l'endpoint utilizza un'associazione SOAP.  
  
```csharp
WsdlNS.SoapBinding soapBinding = GetSoapBinding(context, exporter);  
if (soapBinding != null)  
{  
    soapBinding.Transport = UdpPolicyStrings.UdpNamespace;  
}  
```  
  
#### <a name="wsdl-import"></a>Importazione WSDL  
 Per estendere il sistema di importazione WSDL in modo da gestire l'importazione degli indirizzi, aggiungere la configurazione seguente al file di configurazione per Svcutil.exe, come illustrato nel file Svcutil.exe.config:  
  
```xml
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <policyImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 Quando si esegue Svcutil.exe, esistono due opzioni per ottenere che Svcutil.exe carichi le estensioni di importazione WSDL:  
  
1. Puntare Svcutil. exe al file di configurazione usando/SvcutilConfig:\<file>.  
  
2. Aggiungere la sezione di configurazione a Svcutil.exe.config nella stessa directory di Svcutil.exe.  
  
 Il tipo `UdpBindingElementImporter` implementa l'interfaccia `IWsdlImportExtension`. Il metodo `ImportEndpoint` importa l'indirizzo dalla porta WSDL.  
  
```csharp
BindingElementCollection bindingElements = context.Endpoint.Binding.CreateBindingElements();  
TransportBindingElement transportBindingElement = bindingElements.Find<TransportBindingElement>();  
if (transportBindingElement is UdpTransportBindingElement)  
{  
    ImportAddress(context);  
}  
```  
  
### <a name="adding-policy-support"></a>Aggiunta del supporto dei criteri  
 L'elemento di associazione personalizzato è in grado di esportare asserzioni di criteri nell'associazione WSDL affinché un endpoint del servizio esprima le funzionalità di quell'elemento di associazione.  
  
#### <a name="policy-export"></a>Esportazione di criteri  
 Il `UdpTransportBindingElement` tipo implementa `IPolicyExportExtension` per aggiungere il supporto per l'esportazione dei criteri. Di conseguenza, `System.ServiceModel.MetadataExporter` include `UdpTransportBindingElement` nella generazione del criterio per qualsiasi associazione in cui è incluso.  
  
 In `IPolicyExportExtension.ExportPolicy`, aggiungere un'asserzione per UDP e un'altra asserzione se il canale è in modalità multicast. Ciò è dovuto al fatto che la modalità multicast influisce sul modo in cui viene costruito lo stack di comunicazione, pertanto deve essere coordinato tra entrambi i lati.  
  
```csharp
ICollection<XmlElement> bindingAssertions = context.GetBindingAssertions();  
XmlDocument xmlDocument = new XmlDocument();  
bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.TransportAssertion, UdpPolicyStrings.UdpNamespace));  
if (Multicast)  
{  
    bindingAssertions.Add(xmlDocument.CreateElement(
        UdpPolicyStrings.Prefix,
        UdpPolicyStrings.MulticastAssertion,
        UdpPolicyStrings.UdpNamespace));  
}  
```  
  
 Dato che gli elementi di associazione di trasporto personalizzati sono responsabili della gestione dell'indirizzamento, l'implementazione di `IPolicyExportExtension` in `UdpTransportBindingElement` deve gestire anche l'esportazione delle asserzioni di criteri di WS-Addressing appropriate per indicare la versione di WS-Addressing utilizzata.  
  
```csharp
AddWSAddressingAssertion(context, encodingBindingElement.MessageVersion.Addressing);  
```  
  
#### <a name="policy-import"></a>Importazione di criteri  
 Per estendere il sistema di importazione dei criteri, aggiungere la configurazione seguente al file di configurazione per Svcutil.exe, come illustrato nel file Svcutil.exe.config:  
  
```xml
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <policyImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 Implementare quindi `IPolicyImporterExtension` dalla classe registrata (`UdpBindingElementImporter`). In `ImportPolicy()`, esaminare le asserzioni nello spazio dei nomi appropriato ed elaborare quelle per generare il trasporto e controllare se è multicast. Rimuovere inoltre dall'elenco delle asserzioni di associazione quelle gestite dall'importatore. Anche in questo caso, quando si esegue Svcutil.exe esistono due opzioni per l'integrazione:  
  
1. Puntare Svcutil. exe al file di configurazione usando/SvcutilConfig:\<file>.  
  
2. Aggiungere la sezione di configurazione a Svcutil.exe.config nella stessa directory di Svcutil.exe.  
  
<a name="AddingAStandardBinding"></a>
## <a name="adding-a-standard-binding"></a>Aggiunta di un elemento di associazione standard  
 L'elemento di associazione è utilizzabile nei due modi seguenti:  
  
- Tramite un'associazione personalizzata: un'associazione personalizzata consente all'utente di creare associazioni basate su un set arbitrario di elementi di associazione.  
  
- Utilizzando un'associazione fornita dal sistema che includa l'elemento di associazione. In `BasicHttpBinding`WCF sono disponibili diverse associazioni definite dal sistema, ad esempio, `NetTcpBinding`e. `WsHttpBinding` Ognuna di queste associazioni è associata a un profilo ben definito.  
  
 L'esempio implementa il profilo di associazione in `SampleProfileUdpBinding`, che deriva dalla classe <xref:System.ServiceModel.Channels.Binding>. `SampleProfileUdpBinding` contiene fino a quattro elementi di associazione al suo interno: `UdpTransportBindingElement`, `TextMessageEncodingBindingElement CompositeDuplexBindingElement` e `ReliableSessionBindingElement`.  
  
```csharp
public override BindingElementCollection CreateBindingElements()  
{
    BindingElementCollection bindingElements = new BindingElementCollection();  
    if (ReliableSessionEnabled)  
    {  
        bindingElements.Add(session);  
        bindingElements.Add(compositeDuplex);  
    }  
    bindingElements.Add(encoding);  
    bindingElements.Add(transport);  
    return bindingElements.Clone();  
}  
```  
  
### <a name="adding-a-custom-standard-binding-importer"></a>Aggiunta di un importatore di associazione standard personalizzato  
 Per impostazione predefinita, Svcutil.exe e il tipo `WsdlImporter` riconoscono e importano associazioni fornite dal sistema. In caso contrario, l'associazione viene importata come istanza `CustomBinding`. Per consentire a Svcutil.exe e a `WsdlImporter` di importare `SampleProfileUdpBinding`, `UdpBindingElementImporter` funge anche da importatore di associazione standard personalizzato.  
  
 Un importatore di associazione standard personalizzato implementa il metodo `ImportEndpoint` nell'interfaccia `IWsdlImportExtension` per esaminare l'istanza `CustomBinding` importata dai metadati per controllare se poteva essere generata da un'associazione standard specifica.  
  
```csharp
if (context.Endpoint.Binding is CustomBinding)  
{  
    Binding binding;  
    if (transportBindingElement is UdpTransportBindingElement)  
    {  
        //if TryCreate is true, the CustomBinding will be replace by a SampleProfileUdpBinding in the  
        //generated config file for better typed generation.  
        if (SampleProfileUdpBinding.TryCreate(bindingElements, out binding))  
        {  
            binding.Name = context.Endpoint.Binding.Name;  
            binding.Namespace = context.Endpoint.Binding.Namespace;  
            context.Endpoint.Binding = binding;  
        }  
    }  
}  
```  
  
 In genere, l'implementazione di un importatore dell'associazione standard personalizzato implica il controllo delle proprietà degli elementi di associazione importati per verificare che siano cambiate solo le proprietà che avrebbero potuto essere impostate dall'associazione standard e che tutte le altre siano rimaste sulle impostazioni predefinite. Una strategia di base per l'implementazione di un importatore dell'associazione standard consiste nel creare un'istanza dell'associazione standard, propagare le proprietà dagli elementi di associazione all'istanza dell'associazione standard supportata dall'associazione standard e nel confrontare gli elementi di associazione dall'associazione standard con gli elementi di associazione importati.  
  
<a name="AddingConfigurationSupport"></a>
## <a name="adding-configuration-support"></a>Aggiunta del supporto di configurazione  
 Per esporre il trasporto tramite configurazione si devono implementare due sezioni di configurazione. La prima è una classe `BindingElementExtensionElement` per `UdpTransportBindingElement`. Serve per fare in modo che le implementazioni di `CustomBinding` possano fare riferimento all'elemento di associazione. La seconda è una `Configuration` per `SampleProfileUdpBinding`.  
  
### <a name="binding-element-extension-element"></a>Elemento di estensione dell'elemento di associazione  
 La sezione `UdpTransportElement` è una classe `BindingElementExtensionElement` che espone `UdpTransportBindingElement` al sistema di configurazione. Con alcuni override di base, vengono definiti il nome della sezione di configurazione, il tipo dell'elemento di associazione e come creare l'elemento di associazione. Gli utenti possono quindi registrare la sezione di estensione in un file di configurazione come illustrato nel codice seguente.  
  
```xml
<configuration>  
  <system.serviceModel>  
    <extensions>  
      <bindingElementExtensions>  
        <add name="udpTransport" type="Microsoft.ServiceModel.Samples.UdpTransportElement, UdpTransport" />  
      </bindingElementExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
```  
  
 È possibile fare riferimento all'estensione da associazioni personalizzate per utilizzare UDP come trasporto.  
  
```xml
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <customBinding>  
       <binding configurationName="UdpCustomBinding">  
         <udpTransport/>  
       </binding>  
      </customBinding>  
    </bindings>  
  </system.serviceModel>  
</configuration>  
```  
  
### <a name="binding-section"></a>Sezione dell'associazione  
 La sezione `SampleProfileUdpBindingCollectionElement` è una classe `StandardBindingCollectionElement` che espone `SampleProfileUdpBinding` al sistema di configurazione. La maggior parte dell'implementazione viene delegata a `SampleProfileUdpBindingConfigurationElement` che deriva da `StandardBindingElement`. `SampleProfileUdpBindingConfigurationElement` Dispone di proprietà che corrispondono alle proprietà in `SampleProfileUdpBinding`e alle funzioni di cui eseguire il `ConfigurationElement` mapping dall'associazione. Infine, viene eseguito l'override del metodo `OnApplyConfiguration` in `SampleProfileUdpBinding`, come illustrato nell'esempio di codice seguente.  
  
```csharp
protected override void OnApplyConfiguration(string configurationName)  
{  
    if (binding == null)
        throw new ArgumentNullException("binding");

    if (binding.GetType() != typeof(SampleProfileUdpBinding))
    {
        throw new ArgumentException(string.Format(CultureInfo.CurrentCulture,
            "Invalid type for binding. Expected type: {0}. Type passed in: {1}.",
            typeof(SampleProfileUdpBinding).AssemblyQualifiedName,
            binding.GetType().AssemblyQualifiedName));
    }
    SampleProfileUdpBinding udpBinding = (SampleProfileUdpBinding)binding;

    udpBinding.OrderedSession = this.OrderedSession;
    udpBinding.ReliableSessionEnabled = this.ReliableSessionEnabled;
    udpBinding.SessionInactivityTimeout = this.SessionInactivityTimeout;
    if (this.ClientBaseAddress != null)
        udpBinding.ClientBaseAddress = ClientBaseAddress;
}
```  
  
 Per registrare questo gestore nel sistema di configurazione, aggiungere la sezione seguente al file di configurazione pertinente.  
  
```xml
<configuration>  
  <configSections>  
     <sectionGroup name="system.serviceModel">  
        <sectionGroup name="bindings">  
          <section name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport" />  
        </sectionGroup>  
     </sectionGroup>  
  </configSections>  
</configuration>  
```  
  
 È possibile farvi riferimento dalla sezione di configurazione modello servizi.  
  
```xml
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint configurationName="calculator"  
                address="soap.udp://localhost:8001/"
                bindingConfiguration="CalculatorServer"  
                binding="sampleProfileUdpBinding"
                contract= "Microsoft.ServiceModel.Samples.ICalculatorContract">  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="the-udp-test-service-and-client"></a>UDP Test Service e client  
 Il codice di test per l'utilizzo di questo trasporto di esempio è disponibile nelle directory UdpTestService e UdpTestClient. Il codice servizio è costituito da due test. Il primo imposta associazioni ed endpoint tramite codice e l'altro lo fa tramite configurazione. Entrambi i test utilizzano due endpoint. Un endpoint usa la `SampleUdpProfileBinding` [ \<>con ReliableSession](https://docs.microsoft.com/previous-versions/ms731375(v=vs.90)) impostato su. `true` L'altro endpoint utilizza un'associazione personalizzata con `UdpTransportBindingElement`. Equivale a usare `SampleUdpProfileBinding` with [ \<ReliableSession>](https://docs.microsoft.com/previous-versions/ms731375(v=vs.90)) impostato su. `false` Entrambi i test creano un servizio, aggiungono un endpoint per ogni associazione, aprono il servizio e quindi aspettano che l'utente prema INVIO prima di chiudere il servizio.  
  
 Quando si avvia l'applicazione per testare il servizio, l'output sarà come segue:  
  
```console
Testing Udp From Code.  
Service is started from code...  
Press <ENTER> to terminate the service and start service from config...  
```  
  
 È quindi possibile eseguire l'applicazione per testare il client sugli endpoint pubblicati. L'applicazione per testare il client crea un client per ogni endpoint e invia cinque messaggi a ogni endpoint. Di seguito è riportato l'output del client.  
  
```console
Testing Udp From Imported Files Generated By SvcUtil.  
0  
3  
6  
9  
12  
Press <ENTER> to complete test.  
```  
  
 Di seguito è riportato l'output completo del servizio.  
  
```console
Service is started from code...  
Press <ENTER> to terminate the service and start service from config...  
Hello, world!  
Hello, world!  
Hello, world!  
Hello, world!  
Hello, world!  
   adding 0 + 0  
   adding 1 + 2  
   adding 2 + 4  
   adding 3 + 6  
   adding 4 + 8  
```  
  
 Per eseguire l'applicazione client su endpoint pubblicati utilizzando la configurazione, premere INVIO nel servizio e quindi eseguire nuovamente il client di prova. Nel servizio, si dovrebbe vedere l'output seguente.  
  
```console
Testing Udp From Config.  
Service is started from config...  
Press <ENTER> to terminate the service and exit...  
```  
  
 Una nuova esecuzione del client restituisce gli stessi risultati.  
  
 Per rigenerare il codice client e la configurazione tramite Svcutil.exe, avviare l'applicazione di servizio e quindi eseguire il seguente Svcutil.exe dalla directory radice dell'esempio.  
  
```console
svcutil http://localhost:8000/udpsample/ /reference:UdpTransport\bin\UdpTransport.dll /svcutilConfig:svcutil.exe.config  
```  
  
 Notare che Svcutil.exe non genera la configurazione di estensione di associazione per `SampleProfileUdpBinding`, quindi è necessario aggiungerla manualmente.  
  
```xml
<configuration>  
  <system.serviceModel>
    <extensions>  
      <!-- This was added manually because svcutil.exe does not add this extension to the file -->  
      <bindingExtensions>  
        <add name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport" />  
      </bindingExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Per impostare, compilare ed eseguire l'esempio  
  
1. Per compilare la soluzione, seguire le istruzioni riportate in [compilazione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
2. Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
3. Fare riferimento alla sezione precedente "UDP Test Service e client".  
  
> [!IMPORTANT]
> È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente (impostazione predefinita) prima di continuare.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ed esempi. Questo esempio si trova nella directory seguente.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Transport\Udp`

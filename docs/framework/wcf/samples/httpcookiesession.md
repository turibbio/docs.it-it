---
title: HttpCookieSession
ms.date: 03/30/2017
ms.assetid: 101cb624-8303-448a-a3af-933247c1e109
ms.openlocfilehash: 8dba147ace7ada221b5d274cd233e4b9618835d9
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84585130"
---
# <a name="httpcookiesession"></a>HttpCookieSession
In questo esempio viene illustrato come compilare un canale di protocollo personalizzato per utilizzare cookie HTTP per la gestione della sessione. Questo canale consente la comunicazione tra i servizi Windows Communication Foundation (WCF) e i client ASMX o tra i client WCF e i servizi ASMX.  
  
 Quando un client chiama un metodo Web in un servizio Web ASMX basato sulla sessione, il motore ASP.NET esegue le operazioni seguenti:  
  
- Genera un ID univoco (ID sessione).  
  
- Genera l'oggetto sessione e lo associa all'ID univoco.  
  
- Aggiunge l'ID univoco a un'intestazione della risposta HTTP Set-Cookie e la invia al client.  
  
- Identifica il client su chiamate successive in base all'ID di sessione inviato.  
  
 Il client include questo ID di sessione nelle richieste successive al server. Il server utilizza l'ID di sessione dal client per caricare l'oggetto sessione appropriato per il contesto HTTP corrente.  
  
> [!IMPORTANT]
> È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente (impostazione predefinita) prima di continuare.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) ed [!INCLUDE[wf1](../../../../includes/wf1-md.md)] esempi. Questo esempio si trova nella directory seguente.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Channels\HttpCookieSession`  
  
## <a name="httpcookiesession-channel-message-exchange-pattern"></a>Modello di scambio messaggi sul canale HttpCookieSession  
 In questo esempio vengono abilitate sessioni per gli scenari simili ad ASMX. Nella parte inferiore dello stack dei canali, è presente il trasporto HTTP che supporta <xref:System.ServiceModel.Channels.IRequestChannel> e <xref:System.ServiceModel.Channels.IReplyChannel>. È il processo del canale a fornire le sessioni ai livelli più elevati dello stack dei canali. L'esempio implementa due canali (<xref:System.ServiceModel.Channels.IRequestSessionChannel> e <xref:System.ServiceModel.Channels.IReplySessionChannel>) che supportano le sessioni.  
  
## <a name="service-channel"></a>Canale del servizio  
 Nell'esempio viene fornito un canale del servizio nella classe `HttpCookieReplySessionChannelListener`. Questa classe implementa l'interfaccia <xref:System.ServiceModel.Channels.IChannelListener> e converte il canale <xref:System.ServiceModel.Channels.IReplyChannel> da una posizione inferiore nello stack dei canali a un'interfaccia <xref:System.ServiceModel.Channels.IReplySessionChannel>. Questo processo può essere suddiviso nelle parti seguenti:  
  
- Quando il listener del canale è aperto, accetta un canale interno dal listener interno. Poiché il listener interno è un listener del datagramma e la durata di un canale accettato è separata dalla durata del listener, è possibile chiudere il listener interno e utilizzare solo il canale interno  
  
    ```csharp  
                this.innerChannelListener.Open(timeoutHelper.RemainingTime());  
    this.innerChannel = this.innerChannelListener.AcceptChannel(timeoutHelper.RemainingTime());  
    this.innerChannel.Open(timeoutHelper.RemainingTime());  
    this.innerChannelListener.Close(timeoutHelper.RemainingTime());  
    ```  
  
- Quando il processo aperto viene completato, si imposta un ciclo di messaggi per ricevere messaggi dal canale interno.  
  
    ```csharp  
    IAsyncResult result = BeginInnerReceiveRequest();  
    if (result != null && result.CompletedSynchronously)  
    {  
       // do not block the user thread  
       this.completeReceiveCallback ??= new WaitCallback(CompleteReceiveCallback);
       ThreadPool.QueueUserWorkItem(this.completeReceiveCallback, result);  
    }  
    ```  
  
- Quando arriva un messaggio, il canale del servizio esamina l'identificatore di sessione ed esegue il demultiplexing al canale della sessione appropriato. Il listener del canale gestisce un dizionario che esegue il mapping degli identificatori di sessione alle istanze del canale della sessione.  
  
    ```csharp  
    Dictionary<string, IReplySessionChannel> channelMapping;  
    ```  
  
 La `HttpCookieReplySessionChannel` classe implementa <xref:System.ServiceModel.Channels.IReplySessionChannel> . I livelli più elevati dello stack dei canali chiamano il metodo <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A> per leggere le richieste per la sessione. Ogni canale della sessione ha una coda di messaggi privata in cui vengono inseriti messaggi dal canale del servizio.  
  
```csharp  
InputQueue<RequestContext> requestQueue;  
```  
  
 Se qualcuno chiama il metodo <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A> e non sono presenti messaggi nella coda di messaggi, il canale attende per un determinato periodo di tempo prima di spegnersi. Questa operazione consente di pulire i canali della sessione creati per i client non WCF.  
  
 Si utilizza `channelMapping` per tenere traccia di `ReplySessionChannels` e non si chiude il `innerChannel` sottostante fino a quando tutti i canali accettati non sono stati chiusi. In questo modo `HttpCookieReplySessionChannel` può essere attivo oltre la durata di `HttpCookieReplySessionChannelListener`. Non è inoltre necessario preoccuparsi che il listener venga sottoposto a procedure di garbage collection perché i canali accettati conservano un riferimento al listener tramite il callback di `OnClosed`.  
  
## <a name="client-channel"></a>Canale del client  
 Il canale del client corrispondente è incluso nella classe `HttpCookieSessionChannelFactory`. Durante la creazione del canale, la channel factory esegue il wrapping del canale della richiesta interno con una classe `HttpCookieRequestSessionChannel`. La classe `HttpCookieRequestSessionChannel` inoltra le chiamate al canale della richiesta sottostante. Quando il client chiude il proxy, `HttpCookieRequestSessionChannel` invia un messaggio al servizio nel quale viene indicato che il canale sta per essere chiuso. In questo modo, lo stack dei canali del servizio può arrestare normalmente il canale della sessione in uso.  
  
## <a name="binding-and-binding-element"></a>Associazioni ed elementi di associazione  
 Dopo aver creato i canali del servizio e del client, il passaggio successivo consiste nell'integrarli nel runtime WCF. I canali vengono esposti a WCF tramite associazioni ed elementi di associazione. Un'associazione è costituita da uno o più elementi di associazione. WCF offre diverse associazioni definite dal sistema. ad esempio, BasicHttpBinding o WSHttpBinding. La classe `HttpCookieSessionBindingElement` contiene l'implementazione per l'elemento di associazione. Esegue l'override del listener del canale e dei metodi di creazione della channel factory per creare le istanze del listener del canale o della channel factory necessarie.  
  
 Nell'esempio vengono utilizzate asserzioni di criteri per la descrizione del servizio. In questo modo, nell'esempio i requisiti del canale possono essere pubblicati negli altri client che possono utilizzare il servizio. Ad esempio, questo elemento di associazione pubblica le asserzioni di criteri per segnalare ai client potenziali che supporta le sessioni. Poiché nell'esempio viene abilitata la proprietà `ExchangeTerminateMessage` nella configurazione dell'elemento di associazione, vengono aggiunte le asserzioni necessarie per mostrare che il servizio supporta un'azione di scambio messaggi aggiuntiva per terminare la conversazione della sessione. I client possono quindi utilizzare questa azione. Nel codice WSDL seguente vengono mostrate le asserzioni di criteri create da `HttpCookieSessionBindingElement`.  
  
```xml  
<wsp:Policy wsu:Id="HttpCookieSessionBinding_IWcfCookieSessionService_policy" xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy" xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
<wsp:ExactlyOne>  
<wsp:All>  
<wspe:Utf816FFFECharacterEncoding xmlns:wspe="http://schemas.xmlsoap.org/ws/2004/09/policy/encoding"/>  
<mhsc:httpSessionCookie xmlns:mhsc="http://samples.microsoft.com/wcf/mhsc/policy"/>  
</wsp:All>  
</wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
 La classe `HttpCookieSessionBinding` è un'associazione fornita dal sistema che utilizza l'elemento di associazione descritto in precedenza.  
  
## <a name="adding-the-channel-to-the-configuration-system"></a>Aggiunta del canale al sistema di configurazione  
 Nell'esempio vengono fornite due classi che espongono il canale di esempio tramite la configurazione. La prima è una classe <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> per `HttpCookieSessionBindingElement`. La maggior parte dell'implementazione viene delegata a `HttpCookieSessionBindingConfigurationElement` che deriva da <xref:System.ServiceModel.Configuration.StandardBindingElement>. La classe `HttpCookieSessionBindingConfigurationElement` dispone di proprietà che corrispondono alle proprietà di `HttpCookieSessionBindingElement`.  
  
### <a name="binding-element-extension-section"></a>Sezione di estensione dell'elemento di associazione  
 La sezione `HttpCookieSessionBindingElementSection` è una classe <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> che espone `HttpCookieSessionBindingElement` al sistema di configurazione. Con alcuni override, vengono definiti il nome della sezione di configurazione, il tipo dell'elemento di associazione e come creare l'elemento di associazione. È quindi possibile registrare la sezione di estensione in un file di configurazione come segue:  
  
```xml  
<configuration>
    <system.serviceModel>
      <extensions>
        <bindingElementExtensions>
          <add name="httpCookieSession"
               type=  
"Microsoft.ServiceModel.Samples.HttpCookieSessionBindingElementElement,
                    HttpCookieSessionExtension, Version=1.0.0.0,
                    Culture=neutral, PublicKeyToken=null"/>  
        </bindingElementExtensions >  
      </extensions>  
  
      <bindings>  
      <customBinding>  
        <binding name="allowCookiesBinding">  
          <textMessageEncoding messageVersion="Soap11WSAddressing10" />  
          <httpCookieSession sessionTimeout="10" exchangeTerminateMessage="true" />  
          <httpTransport allowCookies="true" />  
        </binding>  
      </customBinding>  
      </bindings>
    </system.serviceModel>
</configuration>  
```  
  
## <a name="test-code"></a>Codice di test  
 Il codice di test per l'utilizzo di questo trasporto di esempio è disponibile nelle directory Client e Service. È costituito da due test: un test usa un'associazione con `allowCookies` impostato `true` su nel client. mentre il secondo test abilita l'arresto esplicito (mediante l'arresto dello scambio di messaggi) sull'associazione.  
  
 Quando si esegue l'esempio, verrà visualizzato l'output seguente:  
  
```console  
Simple binding:  
AddItem(10000,2): ItemCount=2  
AddItem(10550,5): ItemCount=7  
RemoveItem(10550,2): ItemCount=5  
Items  
10000, 2  
10550, 3  
Smart binding:  
AddItem(10000,2): ItemCount=2  
AddItem(10550,5): ItemCount=7  
RemoveItem(10550,2): ItemCount=5  
Items  
10000, 2  
10550, 3  
  
Press <ENTER> to terminate client.  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Per impostare, compilare ed eseguire l'esempio  
  
1. Installare ASP.NET 4,0 usando il comando seguente.  
  
    ```console  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. Assicurarsi di avere eseguito la [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).  
  
3. Per compilare la soluzione, seguire le istruzioni riportate in [compilazione degli esempi di Windows Communication Foundation](building-the-samples.md).  
  
4. Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [esecuzione degli esempi di Windows Communication Foundation](running-the-samples.md).  

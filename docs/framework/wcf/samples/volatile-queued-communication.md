---
title: Comunicazione volatile in coda
ms.date: 03/30/2017
ms.assetid: 0d012f64-51c7-41d0-8e18-c756f658ee3d
ms.openlocfilehash: a9f7e8a96fd293c7f87cc19846a42a42f28de288
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602343"
---
# <a name="volatile-queued-communication"></a>Comunicazione volatile in coda

In questo esempio viene illustrato come eseguire la comunicazione volatile in coda sul trasporto dell'accodamento messaggi (MSMQ). Nell'esempio viene utilizzato <xref:System.ServiceModel.NetMsmqBinding>. Il servizio, in questo caso, è un'applicazione console indipendente che consente di osservare il servizio che riceve messaggi in coda.

> [!NOTE]
> La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.

Nella comunicazione in coda, il client comunica al servizio usando una coda. Più precisamente, il client invia messaggi a una coda. Il servizio riceve messaggi dalla coda. Di conseguenza, per comunicare mediante una coda il servizio e il client non devono essere in esecuzione contemporaneamente.

Quando si invia un messaggio senza garanzie, MSMQ esegue tutti i tentativi possibili per recapitare il messaggio, mentre se si utilizzano le garanzie "una sola volta" MSMQ assicura che il messaggio venga recapitato oppure, se ciò non è possibile, notifica all'utente che il messaggio non può essere recapitato.

In alcuni scenari può essere necessario inviare un messaggio volatile senza garanzia su una coda, ad esempio quando il recapito tempestivo ha la priorità rispetto all'eventualità di perdere i messaggi. Se il gestore delle code si arresta in modo anomalo, i messaggi volatili andranno persi. Pertanto se il gestore delle code si arresta in modo anomalo, la coda non transazionale utilizzata per archiviare i messaggi volatili resta attiva ma i messaggi stessi vengono persi perché non sono archiviati sul disco.

> [!NOTE]
> Non è possibile inviare messaggi volatili senza garanzie all'interno dell'ambito di una transazione utilizzando MSMQ. È necessario creare anche una coda non transazionale per inviare messaggi volatili.

Il contratto di servizio in questo esempio è `IStockTicker` che definisce servizi unidirezionali particolarmente indicati per l'utilizzo con l'accodamento.

```csharp
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]
public interface IStockTicker
{
    [OperationContract(IsOneWay = true)]
    void StockTick(string symbol, float price);
}
```

L'operazione del servizio visualizza il simbolo e il prezzo del ticket delle azioni, come illustrato nel codice di esempio seguente:

```csharp
public class StockTickerService : IStockTicker
{
    public void StockTick(string symbol, float price)
    {
        Console.WriteLine("Stock Tick {0}:{1} ", symbol, price);
     }
     …
}
```

Il servizio è indipendente. Quando si usa il trasporto MSMQ, la coda usata deve essere creata in anticipo. Questa operazione può essere eseguita manualmente o mediante il codice. In questo esempio, il servizio contiene il codice necessario per verificare l'esistenza della coda e crearla, se necessario. Il nome della coda viene letto dal file di configurazione. L'indirizzo di base viene utilizzato dallo [strumento ServiceModel Metadata Utility Tool (Svcutil. exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) per generare il proxy per il servizio.

```csharp
// Host the service within this EXE console application.
public static void Main()
{
    // Get MSMQ queue name from app settings in configuration.
    string queueName = ConfigurationManager.AppSettings["queueName"];

    // Create the transacted MSMQ queue if necessary.
    if (!MessageQueue.Exists(queueName))
        MessageQueue.Create(queueName);

    // Create a ServiceHost for the StockTickerService type.
    using (ServiceHost serviceHost = new ServiceHost(typeof(StockTickerService)))
    {
        // Open the ServiceHost to create listeners and start listening for messages.
        serviceHost.Open();

        // The service can now be accessed.
        Console.WriteLine("The service is ready.");
        Console.WriteLine("Press <ENTER> to terminate service.");
        Console.WriteLine();
        Console.ReadLine();

        // Close the ServiceHost to shutdown the service.
        serviceHost.Close();
    }
}
```

Il nome della coda MSMQ è specificato nella sezione appSettings del file di configurazione. L'endpoint per il servizio è definito nella sezione system.serviceModel del file di configurazione e specifica l'associazione `netMsmqBinding`.

> [!NOTE]
> Nel nome della coda viene usato un punto (.) per il computer locale e il separatore barra rovesciata nel percorso quando la coda viene creata usando <xref:System.Messaging>. L'indirizzo dell'endpoint Windows Communication Foundation (WCF) specifica uno schema net. MSMQ:, utilizza "localhost" per il computer locale e le barre nel percorso.

Anche le garanzie e la durabilità o volatilità dei messaggi sono specificate nella configurazione.

```xml
<appSettings>
  <!-- use appSetting to configure MSMQ queue name -->
  <add key="queueName" value=".\private$\ServiceModelSamplesVolatile" />
</appSettings>

<system.serviceModel>
  <services>
    <service name="Microsoft.ServiceModel.Samples.StockTickerService"
             behaviorConfiguration="CalculatorServiceBehavior">
    ...
      <!-- Define NetMsmqEndpoint -->
      <endpoint address="net.msmq://localhost/private/ServiceModelSamplesVolatile"
                binding="netMsmqBinding"
                bindingConfiguration="volatileBinding"
                contract="Microsoft.ServiceModel.Samples.IStockTicker" />
    ...
    </service>
  </services>

  <bindings>
    <netMsmqBinding>
      <binding name="volatileBinding"
             durable="false"
           exactlyOnce="false"/>
    </netMsmqBinding>
  </bindings>
  ...
</system.serviceModel>
```

Poiché nell'esempio vengono inviati messaggi in coda utilizzando una coda non transazionale, i messaggi sottoposti a transazione non possono essere inviati alla coda.

```csharp
// Create a client.
Random r = new Random(137);

StockTickerClient client = new StockTickerClient();

float price = 43.23F;
for (int i = 0; i < 10; i++)
{
    float increment = 0.01f * (r.Next(10));
    client.StockTick("zzz" + i, price + increment);
}

//Closing the client gracefully cleans up resources.
client.Close();
```

Quando si esegue l'esempio, le attività del client e del servizio vengono visualizzate nelle finestre della console del servizio e del client. È possibile osservare il servizio che riceve i messaggi dal client. Premere INVIO in tutte le finestre della console per arrestare il servizio e il client. Notare che essendo usato l'accodamento, non è necessario che client e servizio siano in esecuzione contemporaneamente. È possibile eseguire il client, arrestarlo e quindi avviare il servizio e riceve comunque i messaggi.

```console
The service is ready.
Press <ENTER> to terminate service.

Stock Tick zzz0:43.25
Stock Tick zzz1:43.23
Stock Tick zzz2:43.28
Stock Tick zzz3:43.3
Stock Tick zzz4:43.23
Stock Tick zzz5:43.25
Stock Tick zzz6:43.25
Stock Tick zzz7:43.24
Stock Tick zzz8:43.32
Stock Tick zzz9:43.3
```

### <a name="to-set-up-build-and-run-the-sample"></a>Per impostare, compilare ed eseguire l'esempio

1. Assicurarsi di avere eseguito la [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).

2. Per compilare l'edizione in C# o Visual Basic .NET della soluzione, seguire le istruzioni in [Building the Windows Communication Foundation Samples](building-the-samples.md).

3. Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [esecuzione degli esempi di Windows Communication Foundation](running-the-samples.md).

Per impostazione predefinita con l'associazione <xref:System.ServiceModel.NetMsmqBinding>, la sicurezza del trasporto è abilitata. Esistono due proprietà pertinenti per la sicurezza del trasporto MSMQ <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> e, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> `.` per impostazione predefinita, la modalità di autenticazione è impostata su `Windows` e il livello di protezione è impostato su `Sign` . Affinché MSMQ fornisca la funzionalità di autenticazione e firma, è necessario che faccia parte di un dominio e che sia installata l'opzione di integrazione di Active Directory per MSMQ. Se si esegue questo esempio in un computer che non soddisfà questi criteri si riceve un errore.

### <a name="to-run-the-sample-on-a-computer-joined-to-a-workgroup-or-without-active-directory-integration"></a>Per eseguire l'esempio in un computer appartenente a un gruppo di lavoro o privo di integrazione con Active Directory

1. Se il computer non appartiene a un dominio o non è installato con l'integrazione di Active Directory, disattivare la sicurezza del trasporto impostando la modalità di autenticazione e il livello di protezione su `None` come illustrato nel codice di configurazione seguente:

    ```xml
    <system.serviceModel>
        <services>
          <service name="Microsoft.ServiceModel.Samples.StockTickerService"
                   behaviorConfiguration="StockTickerServiceBehavior">
            <host>
              <baseAddresses>
                <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>
              </baseAddresses>
            </host>

            <!-- Define NetMsmqEndpoint -->
            <endpoint address="net.msmq://localhost/private/ServiceModelSamplesVolatile"
                      binding="netMsmqBinding"
                      bindingConfiguration="volatileBinding"
                      contract="Microsoft.ServiceModel.Samples.IStockTicker" />
            <!-- the mex endpoint is exposed at http://localhost:8000/ServiceModelSamples/service/mex -->
            <endpoint address="mex"
                      binding="mexHttpBinding"
                      contract="IMetadataExchange" />

          </service>
        </services>

        <bindings>
          <netMsmqBinding>
            <binding name="volatileBinding"
                  durable="false"
                  exactlyOnce="false">
              <security mode="None" />
            </binding>
          </netMsmqBinding>
        </bindings>

        <behaviors>
          <serviceBehaviors>
            <behavior name="StockTickerServiceBehavior">
              <serviceMetadata httpGetEnabled="True"/>
            </behavior>
          </serviceBehaviors>
        </behaviors>

      </system.serviceModel>
    ```

2. Assicurarsi di modificare la configurazione sul server e sul client prima di eseguire l'esempio.

    > [!NOTE]
    > L'impostazione di `security mode` su `None` è equivalente all'impostazione di <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>, <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> e della sicurezza `Message` su `None`.

> [!IMPORTANT]
> È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente (impostazione predefinita) prima di continuare.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) ed [!INCLUDE[wf1](../../../../includes/wf1-md.md)] esempi. Questo esempio si trova nella directory seguente.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\Volatile`

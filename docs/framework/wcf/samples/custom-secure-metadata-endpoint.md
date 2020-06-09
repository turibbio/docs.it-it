---
title: Endpoint di metadati protetto personalizzato
ms.date: 03/30/2017
ms.assetid: 9e369e99-ea4a-49ff-aed2-9fdf61091a48
ms.openlocfilehash: 6e392f396b62ad2a3d3cda6e7d6ff31f186f0964
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84592437"
---
# <a name="custom-secure-metadata-endpoint"></a>Endpoint di metadati protetto personalizzato
In questo esempio viene illustrato come implementare un servizio con un endpoint di metadati protetto che utilizza una delle associazioni di scambio non di metadati e come configurare [lo strumento ServiceModel Metadata Utility Tool (Svcutil. exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) o i client per recuperare i metadati da tale endpoint di metadati. Per l'esposizione di endpoint di metadati sono disponibili due associazioni fornite dal sistema, cioè mexHttpBinding e mexHttpsBinding. L'associazione mexHttpBinding viene utilizzata per esporre un endpoint di metadati tramite HTTP in modo non protetto. L'associazione mexHttpsBinding viene utilizzata per esporre un endpoint di metadati tramite HTTPS in modo protetto. In questo esempio viene illustrato come esporre un endpoint di metadati protetto tramite <xref:System.ServiceModel.WSHttpBinding>. Procedere in questo modo quando si desidera modificare le impostazioni di sicurezza sull'associazione senza utilizzare HTTPS. Se si utilizza mexHttpsBinding, l'endpoint di metadati sarà protetto, ma non sarà in alcun modo possibile modificare le impostazioni dell'associazione.  
  
> [!NOTE]
> La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
## <a name="service"></a>Service  
 Il servizio di questo esempio è dotato di due endpoint. L'endpoint dell'applicazione invia al contratto `ICalculator` un `WSHttpBinding` con la `ReliableSession` attivata e la sicurezza dei `Message` che utilizza certificati. L'endpoint di metadati utilizza inoltre `WSHttpBinding`, con le stesse impostazioni di sicurezza ma senza `ReliableSession`. La configurazione pertinente è la seguente:  
  
```xml  
<services>
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
             behaviorConfiguration="CalculatorServiceBehavior">  
     <!-- use base address provided by host -->  
     <endpoint address=""  
       binding="wsHttpBinding"  
       bindingConfiguration="Binding2"  
       contract="Microsoft.ServiceModel.Samples.ICalculator" />  
     <endpoint address="mex"  
       binding="wsHttpBinding"  
       bindingConfiguration="Binding1"  
       contract="IMetadataExchange" />  
     </service>  
 </services>  
 <bindings>  
   <wsHttpBinding>  
     <binding name="Binding1">  
       <security mode="Message">  
         <message clientCredentialType="Certificate" />  
       </security>  
     </binding>  
     <binding name="Binding2">  
       <reliableSession inactivityTimeout="00:01:00" enabled="true" />  
       <security mode="Message">  
         <message clientCredentialType="Certificate" />  
       </security>  
     </binding>  
   </wsHttpBinding>  
 </bindings>  
```  
  
 In molti degli altri esempi, l'endpoint di metadati utilizza il `mexHttpBinding` predefinito, che non è protetto. Qui i metadati sono protetti utilizzando `WSHttpBinding` con sicurezza dei `Message`. Affinché i client di metadati possano recuperare questi metadati, è necessario che siano configurati con un'associazione corrispondente. Nell'esempio viene illustrato l'utilizzo di due di questi client.  
  
 Il primo client utilizza Svcutil.exe per recuperare i metadati e generare il codice del client e la configurazione in fase di progettazione. Il servizio utilizza un'associazione non predefinita per i metadati, quindi lo strumento Svcutil.exe deve essere specificamente configurato in modo da ottenere i metadati dal servizio che utilizza quell'associazione.  
  
 Il secondo client utilizza il `MetadataResolver` per recuperare dinamicamente i metadati per un contratto noto e richiamare quindi le operazioni sul client generato dinamicamente.  
  
## <a name="svcutil-client"></a>Client Svcutil  
 Quando si utilizza l'associazione predefinita per ospitare l'endpoint `IMetadataExchange`, è possibile eseguire Svcutil.exe con l'indirizzo di quell'endpoint:  
  
```console  
svcutil http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 e funziona. Ma in questo esempio, il server utilizza un endpoint non predefinito per ospitare i metadati. È quindi necessario richiedere a Svcutil.exe di utilizzare l'associazione corretta. Questa operazione può essere eseguita utilizzando un file Svcutil.exe.config.  
  
 Il file Svcutil.exe.config sembra un file di configurazione client normale. Le uniche differenze sono il nome e il contratto dell'endpoint:  
  
```xml  
<endpoint name="http"  
          binding="wsHttpBinding"  
          bindingConfiguration="Binding1"  
          behaviorConfiguration="ClientCertificateBehavior"  
          contract="IMetadataExchange" />  
```  
  
 Il nome dell'endpoint deve essere il nome dello schema dell'indirizzo in cui vengono ospitati i metadati e il contratto dell'endpoint deve essere `IMetadataExchange`. In questo modo, quando viene eseguito Svcutil.exe con una riga di comando simile alla seguente:  
  
```console  
svcutil http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 viene cercato l'endpoint denominato "http" e il contratto `IMetadataExchange` per configurare l'associazione e il comportamento dello scambio di comunicazione con l'endpoint di metadati. Il resto del file Svcutil.exe.config nell'esempio specifica la configurazione di associazione e le credenziali del comportamento per fare corrispondere la configurazione del server all'endpoint di metadati.  
  
 Perché Svcutil.exe selezioni la configurazione in Svcutil.exe.config, Svcutil.exe deve trovarsi nella stessa directory del file di configurazione. Di conseguenza, è necessario copiare Svcutil.exe dal percorso di installazione alla directory che contiene il file Svcutil.exe.config. Da tale directory, eseguire il comando seguente:  
  
```console  
.\svcutil.exe http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 Il carattere ". \\ " garantisce che venga eseguita la copia di Svcutil. exe in questa directory (quella con un file Svcutil. exe. config corrispondente).  
  
## <a name="metadataresolver-client"></a>Client di MetadataResolver  
 Se il client conosce il contratto e come comunicare con i metadati in fase di progettazione, può scoprire dinamicamente l'associazione e indirizzo degli endpoint dell'applicazione utilizzando `MetadataResolver`. In questo esempio di client viene illustrata questa operazione, oltre a come configurare l'associazione e le credenziali utilizzate dal `MetadataResolver` creando e configurando un `MetadataExchangeClient`.  
  
 Le stesse informazioni sull'associazione e sul certificato visualizzate in Svcutil.exe.config possono essere specificate in modo imperativo nel `MetadataExchangeClient`:  
  
```csharp  
// Specify the Metadata Exchange binding and its security mode  
WSHttpBinding mexBinding = new WSHttpBinding(SecurityMode.Message);  
mexBinding.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;  
  
// Create a MetadataExchangeClient for retrieving metadata, and set the // certificate details  
MetadataExchangeClient mexClient = new MetadataExchangeClient(mexBinding);  
mexClient.SoapCredentials.ClientCertificate.SetCertificate(    StoreLocation.CurrentUser, StoreName.My,  
    X509FindType.FindBySubjectName, "client.com");  
mexClient.SoapCredentials.ServiceCertificate.Authentication.CertificateValidationMode = X509CertificateValidationMode.PeerOrChainTrust;  
mexClient.SoapCredentials.ServiceCertificate.SetDefaultCertificate(    StoreLocation.CurrentUser, StoreName.TrustedPeople,  
    X509FindType.FindBySubjectName, "localhost");  
```  
  
 Una volta configurato il `mexClient`, è possibile enumerare i contratti desiderati e utilizzare `MetadataResolver` per recuperare un elenco di endpoint con quei contratti:  
  
```csharp  
// The contract we want to fetch metadata for  
Collection<ContractDescription> contracts = new Collection<ContractDescription>();  
ContractDescription contract = ContractDescription.GetContract(typeof(ICalculator));  
contracts.Add(contract);  
// Find endpoints for that contract  
EndpointAddress mexAddress = new EndpointAddress(ConfigurationManager.AppSettings["mexAddress"]);  
ServiceEndpointCollection endpoints = MetadataResolver.Resolve(contracts, mexAddress, mexClient);  
```  
  
 Infine, è possibile utilizzare le informazioni da quegli endpoint per inizializzare l'associazione e l'indirizzo di una `ChannelFactory` utilizzata per creare canali per comunicare con gli endpoint dell'applicazione.  
  
```csharp  
ChannelFactory<ICalculator> cf = new ChannelFactory<ICalculator>(endpoint.Binding, endpoint.Address);  
```  
  
 Il punto importante di questo esempio di client è di dimostrare che, se si utilizza `MetadataResolver` ed è necessario specificare associazioni o comportamenti personalizzati per la comunicazione di scambio di metadati, è possibile utilizzare un `MetadataExchangeClient` per specificare quelle impostazioni personalizzate.  
  
#### <a name="to-set-up-and-build-the-sample"></a>Per impostare e compilare l'esempio  
  
1. Assicurarsi di avere eseguito la [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Per compilare la soluzione, seguire le istruzioni riportate in [compilazione degli esempi di Windows Communication Foundation](building-the-samples.md).  
  
#### <a name="to-run-the-sample-on-the-same-machine"></a>Per eseguire l'esempio sullo stesso computer  
  
1. Eseguire Setup.bat dalla cartella di installazione dell'esempio. In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio. Si noti che Setup. bat utilizza lo strumento FindPrivateKey. exe, che viene installato eseguendo setupCertTool. bat dalla [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Eseguire l'applicazione client da \MetadataResolverClient\bin o \SvcutilClient\bin. L'attività del client viene visualizzata nella finestra dell'applicazione console.  
  
3. Se il client e il servizio non sono in grado di comunicare, vedere [Suggerimenti per la risoluzione dei problemi per gli esempi di WCF](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).  
  
4. Rimuovere i certificati eseguendo Cleanup.bat una volta completato l'esempio. Negli altri esempi relativi alla sicurezza vengono usati gli stessi certificati.  
  
#### <a name="to-run-the-sample-across-machines"></a>Per eseguire l'esempio tra più computer  
  
1. Eseguire `setup.bat service` sul server. Quando `setup.bat` si esegue con l' `service` argomento viene creato un certificato del servizio con il nome di dominio completo del computer e il certificato del servizio viene esportato in un file denominato Service. cer.  
  
2. Modificare Web.config sul server per riflettere il nome del nuovo certificato, Ovvero modificare l' `findValue` attributo nell' [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md) elemento con il nome di dominio completo del computer.  
  
3. Copiare il file Service.cer dalla directory del servizio alla directory del client sul computer client.  
  
4. Eseguire `setup.bat client` sul client. Quando `setup.bat` si esegue con l' `client` argomento viene creato un certificato client denominato client.com e il certificato client viene esportato in un file denominato client. cer.  
  
5. Nel file App.config del `MetadataResolverClient` sul computer client, modificare il valore dell'indirizzo dell'endpoint mex in modo che corrisponda al nuovo indirizzo del servizio. Tale operazione viene eseguita sostituendo localhost con il nome di dominio completo del server. Modificare inoltre l'occorrenza di "localhost" nel file metadataResolverClient.cs al nuovo nome del certificato del servizio (il nome di dominio completo del server). Eseguire la stessa operazione per il file App.config del progetto SvcutilClient.  
  
6. Copiare il file Client.cer dalla directory del client nella directory del servizio sul server.  
  
7. Eseguire `ImportServiceCert.bat` sul client. In questo modo viene importato il certificato del servizio dal file Service.cer nell'archivio CurrentUser - TrustedPeople.  
  
8. Eseguire `ImportClientCert.bat` sul server. In questo modo il certificato client viene importato dal file Client.cer nell'archivio LocalMachine - TrustedPeople.  
  
9. Compilare il progetto di servizio in Visual Studio sul computer server e selezionare la pagina della Guida in un browser Web per verificare che sia in esecuzione.  
  
10. Eseguire MetadataResolverClient o SvcutilClient da VS sul computer client.  
  
    1. Se il client e il servizio non sono in grado di comunicare, vedere [Suggerimenti per la risoluzione dei problemi per gli esempi di WCF](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).  
  
#### <a name="to-clean-up-after-the-sample"></a>Per eseguire la pulizia dopo l'esempio  
  
- Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio.  
  
    > [!NOTE]
    > Questo script non rimuove i certificati del servizio su un client quando si esegue questo esempio tra più computer. Se sono stati eseguiti esempi Windows Communication Foundation (WCF) che usano certificati tra computer, assicurarsi di cancellare i certificati del servizio installati nell'archivio CurrentUser-TrustedPeople. A tale scopo, utilizzare il comando seguente: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`. Ad esempio: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.  
  
> [!IMPORTANT]
> È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente (impostazione predefinita) prima di continuare.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) ed [!INCLUDE[wf1](../../../../includes/wf1-md.md)] esempi. Questo esempio si trova nella directory seguente.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Metadata\CustomMexEndpoint`  

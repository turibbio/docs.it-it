---
title: Validator del certificato X.509
ms.date: 03/30/2017
ms.assetid: 3b042379-02c4-4395-b927-e57c842fd3e0
ms.openlocfilehash: ba73381bb6211dcbd1ddad1457f9ae8611008d43
ms.sourcegitcommit: 839777281a281684a7e2906dccb3acd7f6a32023
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82141205"
---
# <a name="x509-certificate-validator"></a>Validator del certificato X.509

In questo esempio viene illustrato come implementare un validator del certificato X.509 personalizzato. Questo processo è utile nei casi in cui nessuna delle convalide incorporate del certificato X.509 è appropriata ai requisiti dell'applicazione. In questo esempio viene mostrato un servizio che dispone di un validator personalizzato che accetta certificati autocertificati. Il client utilizza tale certificato per l'autenticazione nel servizio.

Nota: poiché chiunque può costruire un certificato autocertificato, il validator personalizzato utilizzato dal servizio è meno affidabile del comportamento predefinito fornito da ChainTrust X509CertificateValidationMode. Le implicazioni di sicurezza di questa scelta devono essere considerate attentamente prima di utilizzare questa logica di convalida nel codice di produzione.

In sintesi, nell'esempio viene illustrato in che modo eseguire le operazioni seguenti:

- Il client può essere autenticato tramite un certificato X.509.

- Il server convalida le credenziali client a fronte di un validator X509CertificateValidator personalizzato.

- Il server viene autenticato tramite il certificato X.509 del server.

Il servizio espone un singolo endpoint per la comunicazione con il servizio, definito utilizzando il file di configurazione app. config. L'endpoint è costituito da un indirizzo, un'associazione e un contratto. L'associazione viene configurata con `wsHttpBinding` uno standard che usa `WSSecurity` per impostazione predefinita e l'autenticazione del certificato client. Il comportamento del servizio specifica la modalità personalizzata per la convalida dei certificati X.509 client insieme al tipo di classe del validator. Il comportamento specifica inoltre il certificato server mediante l'elemento serviceCertificate. Il certificato del server deve contenere lo stesso valore per l' `SubjectName` oggetto `findValue` nel [ \<>ServiceCertificate ](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md).

```xml
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceModel.Samples.CalculatorService"
               behaviorConfiguration="CalculatorServiceBehavior">
        <!-- use host/baseAddresses to configure base address -->
        <!-- provided by host -->
        <host>
          <baseAddresses>
            <add baseAddress =
                "http://localhost:8001/servicemodelsamples/service" />
          </baseAddresses>
        </host>
        <!-- use base address specified above, provide one endpoint -->
        <endpoint address="certificate"
               binding="wsHttpBinding"
               bindingConfiguration="Binding"
               contract="Microsoft.ServiceModel.Samples.ICalculator" />
      </service>
    </services>
    <bindings>
      <wsHttpBinding>
        <!-- X509 certificate binding -->
        <binding name="Binding">
          <security mode="Message">
            <message clientCredentialType="Certificate" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceDebug includeExceptionDetailInFaults ="true"/>
          <serviceCredentials>
            <!-- The serviceCredentials behavior allows one -->
            <!-- to specify authentication constraints on -->
            <!-- client certificates. -->
            <clientCertificate>
              <!-- Setting the certificateValidationMode to -->
              <!-- Custom means that if the custom -->
              <!-- X509CertificateValidator does NOT throw -->
              <!-- an exception, then the provided certificate -->
              <!-- will be trusted without performing any -->
              <!-- validation beyond that performed by the custom -->
              <!-- validator. The security implications of this -->
              <!-- setting should be carefully considered before -->
              <!-- using Custom in production code. -->
              <authentication
                 certificateValidationMode="Custom"
                 customCertificateValidatorType =
"Microsoft.ServiceModel.Samples.CustomX509CertificateValidator, service" />
            </clientCertificate>
            <!-- The serviceCredentials behavior allows one to -->
            <!-- define a service certificate. -->
            <!-- A service certificate is used by a client to -->
            <!-- authenticate the service and provide message -->
            <!-- protection. This configuration references the -->
            <!-- "localhost" certificate installed during the setup -->
            <!-- instructions. -->
            <serviceCertificate findValue="localhost"
                 storeLocation="LocalMachine"
                 storeName="My" x509FindType="FindBySubjectName" />
          </serviceCredentials>
        </behavior>
      </serviceBehaviors>
    </behaviors>
      </system.serviceModel>
```

La configurazione dell'endpoint client è costituita da un nome di configurazione, un indirizzo assoluto per l'endpoint del servizio, l'associazione e il contratto. L'associazione client viene configurata con la modalità e il `clientCredentialType` del messaggio appropriati.

```xml
<system.serviceModel>
    <client>
      <!-- X509 certificate based endpoint -->
      <endpoint name="Certificate"
        address=
        "http://localhost:8001/servicemodelsamples/service/certificate"
                binding="wsHttpBinding"
                bindingConfiguration="Binding"
                behaviorConfiguration="ClientCertificateBehavior"
                contract="Microsoft.ServiceModel.Samples.ICalculator">
      </endpoint>
    </client>
    <bindings>
        <wsHttpBinding>
            <!-- X509 certificate binding -->
            <binding name="Binding">
                <security mode="Message">
                    <message clientCredentialType="Certificate" />
               </security>
            </binding>
       </wsHttpBinding>
    </bindings>
    <behaviors>
      <endpointBehaviors>
        <behavior name="ClientCertificateBehavior">
          <clientCredentials>
            <serviceCertificate>
              <!-- Setting the certificateValidationMode to -->
              <!-- PeerOrChainTrust means that if the certificate -->
              <!-- is in the user's Trusted People store, then it -->
              <!-- is trusted without performing a validation of -->
              <!-- the certificate's issuer chain. -->
              <!-- This setting is used here for convenience so -->
              <!-- that the sample can be run without having to -->
              <!-- have certificates issued by a certification -->
              <!-- authority (CA). This setting is less secure -->
              <!-- than the default, ChainTrust. The security -->
              <!-- implications of this setting should be -->
              <!-- carefully considered before using -->
              <!-- PeerOrChainTrust in production code.-->
              <authentication
                  certificateValidationMode="PeerOrChainTrust" />
            </serviceCertificate>
          </clientCredentials>
        </behavior>
      </endpointBehaviors>
    </behaviors>
  </system.serviceModel>
```

L'implementazione client imposta il certificato client da utilizzare.

```csharp
// Create a client with Certificate endpoint configuration
CalculatorClient client = new CalculatorClient("Certificate");
try
{
    client.ClientCredentials.ClientCertificate.SetCertificate(StoreLocation.CurrentUser, StoreName.My, X509FindType.FindBySubjectName, "test1");

    // Call the Add service operation.
    double value1 = 100.00D;
    double value2 = 15.99D;
    double result = client.Add(value1, value2);
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);

    // Call the Subtract service operation.
    value1 = 145.00D;
    value2 = 76.54D;
    result = client.Subtract(value1, value2);
    Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);

    // Call the Multiply service operation.
    value1 = 9.00D;
    value2 = 81.25D;
    result = client.Multiply(value1, value2);
    Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);

    // Call the Divide service operation.
    value1 = 22.00D;
    value2 = 7.00D;
    result = client.Divide(value1, value2);
    Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);
    client.Close();
}
catch (TimeoutException e)
{
    Console.WriteLine("Call timed out : {0}", e.Message);
    client.Abort();
}
catch (CommunicationException e)
{
    Console.WriteLine("Call failed : {0}", e.Message);
    client.Abort();
}
catch (Exception e)
{
    Console.WriteLine("Call failed : {0}", e.Message);
    client.Abort();
}
```

In questo esempio viene utilizzato un X509CertificateValidator personalizzato per convalidare i certificati. In questo esempio viene implementato CustomX509CertificateValidator, derivato da <xref:System.IdentityModel.Selectors.X509CertificateValidator>. Per ulteriori informazioni, vedere la documentazione relativa a <xref:System.IdentityModel.Selectors.X509CertificateValidator>. In questo particolare esempio il validator personalizzato implementa il metodo Validate per accettare qualsiasi certificato X.509 che è autocertificata, come mostrato nel codice seguente.

```csharp
public class CustomX509CertificateValidator : X509CertificateValidator
{
  public override void Validate ( X509Certificate2 certificate )
  {
   // Only accept self-issued certificates
   if (certificate.Subject != certificate.Issuer)
     throw new Exception("Certificate is not self-issued");
   }
}
```

 Quando il validator è stato implementato nel codice del servizio, l'host del servizio deve essere informato dell'istanza del validator da utilizzare. Questa operazione viene eseguita tramite il codice seguente.

```csharp
serviceHost.Credentials.ClientCertificate.Authentication.CertificateValidationMode = X509CertificateValidationMode.Custom;
serviceHost.Credentials.ClientCertificate.Authentication.CustomCertificateValidator = new CustomX509CertificateValidator();
```

 In alternativa, è possibile eseguire la stessa operazione nella configurazione come segue.

```xml
<behaviors>
    <serviceBehaviors>
     <behavior name="CalculatorServiceBehavior">
       ...
   <serviceCredentials>
    <!--The serviceCredentials behavior allows one to specify -->
    <!--authentication constraints on client certificates.-->
    <clientCertificate>
    <!-- Setting the certificateValidationMode to Custom means -->
    <!--that if the custom X509CertificateValidator does NOT -->
    <!--throw an exception, then the provided certificate will -->
    <!--be trusted without performing any validation beyond that -->
    <!--performed by the custom validator. The security -->
    <!--implications of this setting should be carefully -->
    <!--considered before using Custom in production code. -->
    <authentication certificateValidationMode="Custom"
       customCertificateValidatorType =
"Microsoft.ServiceModel.Samples. CustomX509CertificateValidator, service" />
   </clientCertificate>
   </serviceCredentials>
   ...
  </behavior>
 </serviceBehaviors>
</behaviors>
```

Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client. Il client deve chiamare correttamente tutti i metodi. Premere INVIO nella finestra del client per arrestare il client.

## <a name="setup-batch-file"></a>File batch di installazione

Il file batch Setup.bat incluso in questo esempio consente di configurare il server con i certificati attinenti per eseguire un'applicazione indipendente che richiede la sicurezza server basata su certificato. Questo file batch deve essere modificato per funzionare tra computer diversi o nel caso in cui non sia ospitato.

Di seguito viene fornita una breve panoramica delle varie sezioni dei file batch in modo che possano essere modificate per l'esecuzione nella configurazione appropriata.

- Creazione del certificato server:

     Le righe seguenti del file batch Setup.bat creano il certificato server da usare. La variabile %SERVER_NAME% specifica il nome del server. Modificare questa variabile per specificare nome del server. Il valore predefinito è localhost.

    ```bash
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

- Installazione del certificato server nell'archivio certificati attendibili del client:

     Le righe seguenti nel file batch Setup.bat copiano il certificato server nell'archivio di persone attendibile del client. Questo passaggio è necessario poiché i certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema client. Se è già disponibile un certificato con radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il passaggio del popolamento dell'archivio certificati client con il certificato server non è necessario.

    ```bash
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

- Creazione del certificato del client:

     Le righe seguenti del file batch Setup.bat creano il certificato client da utilizzare. La variabile %USER_NAME% specifica il nome del client. Questo valore è impostato su "test1" perché questo è il nome cercato dal codice client. Se si modifica il valore di % USER_NAME% è necessario modificare il valore corrispondente nel file di origine Client.cs e ricompilare il client.

     Il certificato viene memorizzato nell'archivio personale nel percorso di archivio CurrentUser.

    ```bash
    echo ************
    echo Client cert setup starting
    echo %USER_NAME%
    echo ************
    echo making client cert
    echo ************
    makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%USER_NAME% -sky exchange -pe
    ```

- Installazione del certificato client nell'archivio certificati attendibili del server:

     Le righe seguenti nel file batch Setup.bat copiano il certificato client nell'archivio delle persone attendibile. Questo passaggio è necessario poiché i certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema server. Se è già disponibile un certificato che è impostato come radice in un certificato radice attendibile, ad esempio un certificato rilasciato da Microsoft, il passaggio della popolazione dell'archivio certificati server con il certificato client non è necessario.

    ```bash
    certmgr.exe -add -r CurrentUser -s My -c -n %USER_NAME% -r LocalMachine -s TrustedPeople
    ```

#### <a name="to-set-up-and-build-the-sample"></a>Per impostare e compilare l'esempio

1. Per compilare la soluzione, seguire le istruzioni riportate in [compilazione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).

2. Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni indicate di seguito.

#### <a name="to-run-the-sample-on-the-same-computer"></a>Per eseguire l'esempio nello stesso computer

1. Eseguire Setup. bat dalla cartella di installazione dell'esempio all'interno di un prompt dei comandi di Visual Studio 2012 aperto con privilegi di amministratore. In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.

    > [!IMPORTANT]
    > Il file batch Setup. bat è progettato per essere eseguito da un prompt dei comandi di Visual Studio 2012. La variabile di ambiente PATH impostata nel prompt dei comandi di Visual Studio 2012 punta alla directory che contiene i file eseguibili richiesti dallo script Setup. bat.

2. Avviare Service.exe da service\bin.

3. Avviare Client.exe da \client\bin. L'attività del client viene visualizzata nella finestra dell'applicazione console.

4. Se il client e il servizio non sono in grado di comunicare, vedere [Suggerimenti per la risoluzione dei problemi per gli esempi di WCF](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).

#### <a name="to-run-the-sample-across-computers"></a>Per eseguire l'esempio tra più computer

1. Creare una directory sul computer del servizio.

2. Copiare i file del programma del servizio da \service\bin alla directory virtuale nel computer del servizio. Copiare inoltre i file Setup.bat, Cleanup.bat,GetComputerName.vbs e ImportClientCert.bat nel computer del servizio.

3. Creare una directory sul client del servizio per i file binari del client.

4. Copiare i file di programma del client nella directory del client sul computer relativo e i file Setup.bat, Cleanup.bat e ImportServiceCert.bat nel client.

5. Sul server, eseguire `setup.bat service` in un prompt dei comandi per gli sviluppatori per Visual Studio aperto con privilegi di amministratore. Quando `setup.bat` si esegue `service` con l'argomento viene creato un certificato del servizio con il nome di dominio completo del computer e il certificato del servizio viene esportato in un file denominato Service. cer.

6. Modificare Service. exe. config per riflettere il nuovo nome del certificato (nell' `findValue` attributo in [ \<ServiceCertificate>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)), che corrisponde al nome di dominio completo del computer. Modificare anche il nome del computer nell' \<elemento Service>\</baseAddresses> da localhost al nome completo del computer del servizio.

7. Copiare il file Service.cer dalla directory del servizio nella directory del client sul computer relativo.

8. Sul client, eseguire `setup.bat client` in un prompt dei comandi per gli sviluppatori per Visual Studio aperto con privilegi di amministratore. Quando si esegue `setup.bat` con l'argomento `client` viene creato un certificato client denominato client.com che viene esportato in un file denominato Client.cer.

9. Nel file Client.exe.config presente nel computer client modificare il valore dell'indirizzo della definizione dell'endpoint in base al nuovo indirizzo del servizio. Tale operazione viene eseguita sostituendo localhost con il nome di dominio completo del server.

10. Copiare il file Client.cer dalla directory del client nella directory del servizio sul server.

11. Sul client, eseguire ImportServiceCert. bat in un Prompt dei comandi per gli sviluppatori per Visual Studio aperto con privilegi di amministratore. In questo modo viene importato il certificato del servizio dal file Service.cer nell'archivio CurrentUser - TrustedPeople.

12. Sul server, eseguire ImportClientCert. bat in un Prompt dei comandi per gli sviluppatori per Visual Studio aperto con privilegi di amministratore. In questo modo viene importato il certificato del client dal file Client.cer nell'archivio LocalMachine - TrustedPeople.

13. Sul computer server avviare Service.exe dalla finestra del prompt dei comandi.

14. Sul computer client avviare Client.exe da una finestra del prompt dei comandi. Se il client e il servizio non sono in grado di comunicare, vedere [Suggerimenti per la risoluzione dei problemi per gli esempi di WCF](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).

#### <a name="to-clean-up-after-the-sample"></a>Per eseguire la pulizia dopo l'esempio

1. Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio. In questo modo i certificati server e client vengono rimossi dall'archivio certificati.

> [!NOTE]
> Questo script non rimuove i certificati del servizio da un client quando si esegue l'esempio tra più computer. Se sono stati eseguiti esempi Windows Communication Foundation (WCF) che usano certificati tra computer, assicurarsi di cancellare i certificati del servizio installati nell'archivio CurrentUser-TrustedPeople. Per eseguire questa operazione, usare il seguente comando: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` Ad esempio: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.

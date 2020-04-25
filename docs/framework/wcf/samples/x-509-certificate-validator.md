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
# <a name="x509-certificate-validator"></a><span data-ttu-id="bac2a-102">Validator del certificato X.509</span><span class="sxs-lookup"><span data-stu-id="bac2a-102">X.509 Certificate Validator</span></span>

<span data-ttu-id="bac2a-103">In questo esempio viene illustrato come implementare un validator del certificato X.509 personalizzato.</span><span class="sxs-lookup"><span data-stu-id="bac2a-103">This sample demonstrates how to implement a custom X.509 Certificate Validator.</span></span> <span data-ttu-id="bac2a-104">Questo processo è utile nei casi in cui nessuna delle convalide incorporate del certificato X.509 è appropriata ai requisiti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bac2a-104">This is useful in cases where none of the built-in X.509 Certificate Validation modes is appropriate for the requirements of the application.</span></span> <span data-ttu-id="bac2a-105">In questo esempio viene mostrato un servizio che dispone di un validator personalizzato che accetta certificati autocertificati.</span><span class="sxs-lookup"><span data-stu-id="bac2a-105">This sample shows a service that has a custom validator that accepts self-issued certificates.</span></span> <span data-ttu-id="bac2a-106">Il client utilizza tale certificato per l'autenticazione nel servizio.</span><span class="sxs-lookup"><span data-stu-id="bac2a-106">The client uses such a certificate to authenticate to the service.</span></span>

<span data-ttu-id="bac2a-107">Nota: poiché chiunque può costruire un certificato autocertificato, il validator personalizzato utilizzato dal servizio è meno affidabile del comportamento predefinito fornito da ChainTrust X509CertificateValidationMode.</span><span class="sxs-lookup"><span data-stu-id="bac2a-107">Note: As anyone can construct a self-issued certificate the custom validator used by the service is less secure than the default behavior provided by the ChainTrust X509CertificateValidationMode.</span></span> <span data-ttu-id="bac2a-108">Le implicazioni di sicurezza di questa scelta devono essere considerate attentamente prima di utilizzare questa logica di convalida nel codice di produzione.</span><span class="sxs-lookup"><span data-stu-id="bac2a-108">The security implications of this should be carefully considered before using this validation logic in production code.</span></span>

<span data-ttu-id="bac2a-109">In sintesi, nell'esempio viene illustrato in che modo eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bac2a-109">In summary this sample demonstrates how:</span></span>

- <span data-ttu-id="bac2a-110">Il client può essere autenticato tramite un certificato X.509.</span><span class="sxs-lookup"><span data-stu-id="bac2a-110">The client can be authenticated using an X.509 certificate.</span></span>

- <span data-ttu-id="bac2a-111">Il server convalida le credenziali client a fronte di un validator X509CertificateValidator personalizzato.</span><span class="sxs-lookup"><span data-stu-id="bac2a-111">The server validates the client credentials against a custom X509CertificateValidator.</span></span>

- <span data-ttu-id="bac2a-112">Il server viene autenticato tramite il certificato X.509 del server.</span><span class="sxs-lookup"><span data-stu-id="bac2a-112">The server is authenticated using the server's X.509 certificate.</span></span>

<span data-ttu-id="bac2a-113">Il servizio espone un singolo endpoint per la comunicazione con il servizio, definito utilizzando il file di configurazione app. config. L'endpoint è costituito da un indirizzo, un'associazione e un contratto.</span><span class="sxs-lookup"><span data-stu-id="bac2a-113">The service exposes a single endpoint for communicating with the service, defined using the configuration file App.config. The endpoint consists of an address, a binding, and a contract.</span></span> <span data-ttu-id="bac2a-114">L'associazione viene configurata con `wsHttpBinding` uno standard che usa `WSSecurity` per impostazione predefinita e l'autenticazione del certificato client.</span><span class="sxs-lookup"><span data-stu-id="bac2a-114">The binding is configured with a standard `wsHttpBinding` that defaults to using `WSSecurity` and client certificate authentication.</span></span> <span data-ttu-id="bac2a-115">Il comportamento del servizio specifica la modalità personalizzata per la convalida dei certificati X.509 client insieme al tipo di classe del validator.</span><span class="sxs-lookup"><span data-stu-id="bac2a-115">The service behavior specifies the Custom mode for validating client X.509 certificates along with the type of the validator class.</span></span> <span data-ttu-id="bac2a-116">Il comportamento specifica inoltre il certificato server mediante l'elemento serviceCertificate.</span><span class="sxs-lookup"><span data-stu-id="bac2a-116">The behavior also specifies the server certificate using the serviceCertificate element.</span></span> <span data-ttu-id="bac2a-117">Il certificato del server deve contenere lo stesso valore per l' `SubjectName` oggetto `findValue` nel [ \<>ServiceCertificate ](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md).</span><span class="sxs-lookup"><span data-stu-id="bac2a-117">The server certificate has to contain the same value for the `SubjectName` as the `findValue` in the [\<serviceCertificate>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md).</span></span>

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

<span data-ttu-id="bac2a-118">La configurazione dell'endpoint client è costituita da un nome di configurazione, un indirizzo assoluto per l'endpoint del servizio, l'associazione e il contratto.</span><span class="sxs-lookup"><span data-stu-id="bac2a-118">The client endpoint configuration consists of a configuration name, an absolute address for the service endpoint, the binding, and the contract.</span></span> <span data-ttu-id="bac2a-119">L'associazione client viene configurata con la modalità e il `clientCredentialType` del messaggio appropriati.</span><span class="sxs-lookup"><span data-stu-id="bac2a-119">The client binding is configured with the appropriate mode and message `clientCredentialType`.</span></span>

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

<span data-ttu-id="bac2a-120">L'implementazione client imposta il certificato client da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="bac2a-120">The client implementation sets the client certificate to use.</span></span>

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

<span data-ttu-id="bac2a-121">In questo esempio viene utilizzato un X509CertificateValidator personalizzato per convalidare i certificati.</span><span class="sxs-lookup"><span data-stu-id="bac2a-121">This sample uses a custom X509CertificateValidator to validate certificates.</span></span> <span data-ttu-id="bac2a-122">In questo esempio viene implementato CustomX509CertificateValidator, derivato da <xref:System.IdentityModel.Selectors.X509CertificateValidator>.</span><span class="sxs-lookup"><span data-stu-id="bac2a-122">The sample implements CustomX509CertificateValidator, derived from <xref:System.IdentityModel.Selectors.X509CertificateValidator>.</span></span> <span data-ttu-id="bac2a-123">Per ulteriori informazioni, vedere la documentazione relativa a <xref:System.IdentityModel.Selectors.X509CertificateValidator>.</span><span class="sxs-lookup"><span data-stu-id="bac2a-123">See documentation about <xref:System.IdentityModel.Selectors.X509CertificateValidator> for more information.</span></span> <span data-ttu-id="bac2a-124">In questo particolare esempio il validator personalizzato implementa il metodo Validate per accettare qualsiasi certificato X.509 che è autocertificata, come mostrato nel codice seguente.</span><span class="sxs-lookup"><span data-stu-id="bac2a-124">This particular custom validator sample implements the Validate method to accept any X.509 certificate that is self-issued as shown in the following code.</span></span>

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

 <span data-ttu-id="bac2a-125">Quando il validator è stato implementato nel codice del servizio, l'host del servizio deve essere informato dell'istanza del validator da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="bac2a-125">Once the validator is implemented in service code, the service host must be informed about the validator instance to use.</span></span> <span data-ttu-id="bac2a-126">Questa operazione viene eseguita tramite il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="bac2a-126">This is done using the following code.</span></span>

```csharp
serviceHost.Credentials.ClientCertificate.Authentication.CertificateValidationMode = X509CertificateValidationMode.Custom;
serviceHost.Credentials.ClientCertificate.Authentication.CustomCertificateValidator = new CustomX509CertificateValidator();
```

 <span data-ttu-id="bac2a-127">In alternativa, è possibile eseguire la stessa operazione nella configurazione come segue.</span><span class="sxs-lookup"><span data-stu-id="bac2a-127">Or you can do the same thing in configuration as follows.</span></span>

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

<span data-ttu-id="bac2a-128">Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.</span><span class="sxs-lookup"><span data-stu-id="bac2a-128">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="bac2a-129">Il client deve chiamare correttamente tutti i metodi.</span><span class="sxs-lookup"><span data-stu-id="bac2a-129">The client should successfully call all the methods.</span></span> <span data-ttu-id="bac2a-130">Premere INVIO nella finestra del client per arrestare il client.</span><span class="sxs-lookup"><span data-stu-id="bac2a-130">Press ENTER in the client window to shut down the client.</span></span>

## <a name="setup-batch-file"></a><span data-ttu-id="bac2a-131">File batch di installazione</span><span class="sxs-lookup"><span data-stu-id="bac2a-131">Setup Batch File</span></span>

<span data-ttu-id="bac2a-132">Il file batch Setup.bat incluso in questo esempio consente di configurare il server con i certificati attinenti per eseguire un'applicazione indipendente che richiede la sicurezza server basata su certificato.</span><span class="sxs-lookup"><span data-stu-id="bac2a-132">The Setup.bat batch file included with this sample allows you to configure the server with relevant certificates to run a self-hosted application that requires server certificate-based security.</span></span> <span data-ttu-id="bac2a-133">Questo file batch deve essere modificato per funzionare tra computer diversi o nel caso in cui non sia ospitato.</span><span class="sxs-lookup"><span data-stu-id="bac2a-133">This batch file must be modified to work across computers or to work in a non-hosted case.</span></span>

<span data-ttu-id="bac2a-134">Di seguito viene fornita una breve panoramica delle varie sezioni dei file batch in modo che possano essere modificate per l'esecuzione nella configurazione appropriata.</span><span class="sxs-lookup"><span data-stu-id="bac2a-134">The following provides a brief overview of the different sections of the batch files so that they can be modified to run in the appropriate configuration:</span></span>

- <span data-ttu-id="bac2a-135">Creazione del certificato server:</span><span class="sxs-lookup"><span data-stu-id="bac2a-135">Creating the server certificate:</span></span>

     <span data-ttu-id="bac2a-136">Le righe seguenti del file batch Setup.bat creano il certificato server da usare.</span><span class="sxs-lookup"><span data-stu-id="bac2a-136">The following lines from the Setup.bat batch file create the server certificate to be used.</span></span> <span data-ttu-id="bac2a-137">La variabile %SERVER_NAME% specifica il nome del server.</span><span class="sxs-lookup"><span data-stu-id="bac2a-137">The %SERVER_NAME% variable specifies the server name.</span></span> <span data-ttu-id="bac2a-138">Modificare questa variabile per specificare nome del server.</span><span class="sxs-lookup"><span data-stu-id="bac2a-138">Change this variable to specify your own server name.</span></span> <span data-ttu-id="bac2a-139">Il valore predefinito è localhost.</span><span class="sxs-lookup"><span data-stu-id="bac2a-139">The default value is localhost.</span></span>

    ```bash
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

- <span data-ttu-id="bac2a-140">Installazione del certificato server nell'archivio certificati attendibili del client:</span><span class="sxs-lookup"><span data-stu-id="bac2a-140">Installing the server certificate into client's trusted certificate store:</span></span>

     <span data-ttu-id="bac2a-141">Le righe seguenti nel file batch Setup.bat copiano il certificato server nell'archivio di persone attendibile del client.</span><span class="sxs-lookup"><span data-stu-id="bac2a-141">The following lines in the Setup.bat batch file copy the server certificate into the client trusted people store.</span></span> <span data-ttu-id="bac2a-142">Questo passaggio è necessario poiché i certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema client.</span><span class="sxs-lookup"><span data-stu-id="bac2a-142">This step is required since certificates generated by Makecert.exe are not implicitly trusted by the client system.</span></span> <span data-ttu-id="bac2a-143">Se è già disponibile un certificato con radice in un certificato radice client attendibile, ad esempio un certificato rilasciato da Microsoft, il passaggio del popolamento dell'archivio certificati client con il certificato server non è necessario.</span><span class="sxs-lookup"><span data-stu-id="bac2a-143">If you already have a certificate that is rooted in a client trusted root certificate—for example, a Microsoft issued certificate—this step of populating the client certificate store with the server certificate is not required.</span></span>

    ```bash
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

- <span data-ttu-id="bac2a-144">Creazione del certificato del client:</span><span class="sxs-lookup"><span data-stu-id="bac2a-144">Creating the client certificate:</span></span>

     <span data-ttu-id="bac2a-145">Le righe seguenti del file batch Setup.bat creano il certificato client da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="bac2a-145">The following lines from the Setup.bat batch file create the client certificate to be used.</span></span> <span data-ttu-id="bac2a-146">La variabile %USER_NAME% specifica il nome del client.</span><span class="sxs-lookup"><span data-stu-id="bac2a-146">The %USER_NAME% variable specifies the client name.</span></span> <span data-ttu-id="bac2a-147">Questo valore è impostato su "test1" perché questo è il nome cercato dal codice client.</span><span class="sxs-lookup"><span data-stu-id="bac2a-147">This value is set to "test1" because this is the name the client code looks for.</span></span> <span data-ttu-id="bac2a-148">Se si modifica il valore di % USER_NAME% è necessario modificare il valore corrispondente nel file di origine Client.cs e ricompilare il client.</span><span class="sxs-lookup"><span data-stu-id="bac2a-148">If you change the value of %USER_NAME% you must change the corresponding value in the Client.cs source file and rebuild the client.</span></span>

     <span data-ttu-id="bac2a-149">Il certificato viene memorizzato nell'archivio personale nel percorso di archivio CurrentUser.</span><span class="sxs-lookup"><span data-stu-id="bac2a-149">The certificate is stored in My (Personal) store under the CurrentUser store location.</span></span>

    ```bash
    echo ************
    echo Client cert setup starting
    echo %USER_NAME%
    echo ************
    echo making client cert
    echo ************
    makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%USER_NAME% -sky exchange -pe
    ```

- <span data-ttu-id="bac2a-150">Installazione del certificato client nell'archivio certificati attendibili del server:</span><span class="sxs-lookup"><span data-stu-id="bac2a-150">Installing the client certificate into server's trusted certificate store:</span></span>

     <span data-ttu-id="bac2a-151">Le righe seguenti nel file batch Setup.bat copiano il certificato client nell'archivio delle persone attendibile.</span><span class="sxs-lookup"><span data-stu-id="bac2a-151">The following lines in the Setup.bat batch file copy the client certificate into the trusted people store.</span></span> <span data-ttu-id="bac2a-152">Questo passaggio è necessario poiché i certificati generati da Makecert.exe non sono considerati implicitamente attendibili dal sistema server.</span><span class="sxs-lookup"><span data-stu-id="bac2a-152">This step is required because certificates generated by Makecert.exe are not implicitly trusted by the server system.</span></span> <span data-ttu-id="bac2a-153">Se è già disponibile un certificato che è impostato come radice in un certificato radice attendibile, ad esempio un certificato rilasciato da Microsoft, il passaggio della popolazione dell'archivio certificati server con il certificato client non è necessario.</span><span class="sxs-lookup"><span data-stu-id="bac2a-153">If you already have a certificate that is rooted in a trusted root certificate—for example, a Microsoft issued certificate—this step of populating the server certificate store with the client certificate is not required.</span></span>

    ```bash
    certmgr.exe -add -r CurrentUser -s My -c -n %USER_NAME% -r LocalMachine -s TrustedPeople
    ```

#### <a name="to-set-up-and-build-the-sample"></a><span data-ttu-id="bac2a-154">Per impostare e compilare l'esempio</span><span class="sxs-lookup"><span data-stu-id="bac2a-154">To set up and build the sample</span></span>

1. <span data-ttu-id="bac2a-155">Per compilare la soluzione, seguire le istruzioni riportate in [compilazione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bac2a-155">To build the solution, follow the instructions in [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).</span></span>

2. <span data-ttu-id="bac2a-156">Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni indicate di seguito.</span><span class="sxs-lookup"><span data-stu-id="bac2a-156">To run the sample in a single- or cross-computer configuration, use the following instructions.</span></span>

#### <a name="to-run-the-sample-on-the-same-computer"></a><span data-ttu-id="bac2a-157">Per eseguire l'esempio nello stesso computer</span><span class="sxs-lookup"><span data-stu-id="bac2a-157">To run the sample on the same computer</span></span>

1. <span data-ttu-id="bac2a-158">Eseguire Setup. bat dalla cartella di installazione dell'esempio all'interno di un prompt dei comandi di Visual Studio 2012 aperto con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="bac2a-158">Run Setup.bat from the sample install folder inside a Visual Studio 2012 command prompt opened with administrator privileges.</span></span> <span data-ttu-id="bac2a-159">In questo modo vengono installati tutti i certificati necessari per l'esecuzione dell'esempio.</span><span class="sxs-lookup"><span data-stu-id="bac2a-159">This installs all the certificates required for running the sample.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bac2a-160">Il file batch Setup. bat è progettato per essere eseguito da un prompt dei comandi di Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="bac2a-160">The Setup.bat batch file is designed to be run from a Visual Studio 2012 Command Prompt.</span></span> <span data-ttu-id="bac2a-161">La variabile di ambiente PATH impostata nel prompt dei comandi di Visual Studio 2012 punta alla directory che contiene i file eseguibili richiesti dallo script Setup. bat.</span><span class="sxs-lookup"><span data-stu-id="bac2a-161">The PATH environment variable set within the Visual Studio 2012 Command Prompt points to the directory that contains executables required by the Setup.bat script.</span></span>

2. <span data-ttu-id="bac2a-162">Avviare Service.exe da service\bin.</span><span class="sxs-lookup"><span data-stu-id="bac2a-162">Launch Service.exe from service\bin.</span></span>

3. <span data-ttu-id="bac2a-163">Avviare Client.exe da \client\bin.</span><span class="sxs-lookup"><span data-stu-id="bac2a-163">Launch Client.exe from \client\bin.</span></span> <span data-ttu-id="bac2a-164">L'attività del client viene visualizzata nella finestra dell'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="bac2a-164">Client activity is displayed on the client console application.</span></span>

4. <span data-ttu-id="bac2a-165">Se il client e il servizio non sono in grado di comunicare, vedere [Suggerimenti per la risoluzione dei problemi per gli esempi di WCF](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span><span class="sxs-lookup"><span data-stu-id="bac2a-165">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>

#### <a name="to-run-the-sample-across-computers"></a><span data-ttu-id="bac2a-166">Per eseguire l'esempio tra più computer</span><span class="sxs-lookup"><span data-stu-id="bac2a-166">To run the sample across computers</span></span>

1. <span data-ttu-id="bac2a-167">Creare una directory sul computer del servizio.</span><span class="sxs-lookup"><span data-stu-id="bac2a-167">Create a directory on the service computer.</span></span>

2. <span data-ttu-id="bac2a-168">Copiare i file del programma del servizio da \service\bin alla directory virtuale nel computer del servizio.</span><span class="sxs-lookup"><span data-stu-id="bac2a-168">Copy the service program files from \service\bin to the virtual directory on the service computer.</span></span> <span data-ttu-id="bac2a-169">Copiare inoltre i file Setup.bat, Cleanup.bat,GetComputerName.vbs e ImportClientCert.bat nel computer del servizio.</span><span class="sxs-lookup"><span data-stu-id="bac2a-169">Also copy the Setup.bat, Cleanup.bat, GetComputerName.vbs and ImportClientCert.bat files to the service computer.</span></span>

3. <span data-ttu-id="bac2a-170">Creare una directory sul client del servizio per i file binari del client.</span><span class="sxs-lookup"><span data-stu-id="bac2a-170">Create a directory on the client computer for the client binaries.</span></span>

4. <span data-ttu-id="bac2a-171">Copiare i file di programma del client nella directory del client sul computer relativo</span><span class="sxs-lookup"><span data-stu-id="bac2a-171">Copy the client program files to the client directory on the client computer.</span></span> <span data-ttu-id="bac2a-172">e i file Setup.bat, Cleanup.bat e ImportServiceCert.bat nel client.</span><span class="sxs-lookup"><span data-stu-id="bac2a-172">Also copy the Setup.bat, Cleanup.bat, and ImportServiceCert.bat files to the client.</span></span>

5. <span data-ttu-id="bac2a-173">Sul server, eseguire `setup.bat service` in un prompt dei comandi per gli sviluppatori per Visual Studio aperto con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="bac2a-173">On the server, run `setup.bat service` in a Developer Command Prompt for Visual Studio opened with administrator privileges.</span></span> <span data-ttu-id="bac2a-174">Quando `setup.bat` si esegue `service` con l'argomento viene creato un certificato del servizio con il nome di dominio completo del computer e il certificato del servizio viene esportato in un file denominato Service. cer.</span><span class="sxs-lookup"><span data-stu-id="bac2a-174">Running `setup.bat` with the `service` argument creates a service certificate with the fully-qualified domain name of the computer and exports the service certificate to a file named Service.cer.</span></span>

6. <span data-ttu-id="bac2a-175">Modificare Service. exe. config per riflettere il nuovo nome del certificato (nell' `findValue` attributo in [ \<ServiceCertificate>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)), che corrisponde al nome di dominio completo del computer.</span><span class="sxs-lookup"><span data-stu-id="bac2a-175">Edit Service.exe.config to reflect the new certificate name (in the `findValue` attribute in the [\<serviceCertificate>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)) which is the same as the fully-qualified domain name of the computer.</span></span> <span data-ttu-id="bac2a-176">Modificare anche il nome del computer nell' \<elemento Service>\</baseAddresses> da localhost al nome completo del computer del servizio.</span><span class="sxs-lookup"><span data-stu-id="bac2a-176">Also change the computer name in the \<service>/\<baseAddresses> element from localhost to fully qualified name of your service computer.</span></span>

7. <span data-ttu-id="bac2a-177">Copiare il file Service.cer dalla directory del servizio nella directory del client sul computer relativo.</span><span class="sxs-lookup"><span data-stu-id="bac2a-177">Copy the Service.cer file from the service directory to the client directory on the client computer.</span></span>

8. <span data-ttu-id="bac2a-178">Sul client, eseguire `setup.bat client` in un prompt dei comandi per gli sviluppatori per Visual Studio aperto con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="bac2a-178">On the client, run `setup.bat client` in a Developer Command Prompt for Visual Studio opened with administrator privileges.</span></span> <span data-ttu-id="bac2a-179">Quando si esegue `setup.bat` con l'argomento `client` viene creato un certificato client denominato client.com che viene esportato in un file denominato Client.cer.</span><span class="sxs-lookup"><span data-stu-id="bac2a-179">Running `setup.bat` with the `client` argument creates a client certificate named client.com and exports the client certificate to a file named Client.cer.</span></span>

9. <span data-ttu-id="bac2a-180">Nel file Client.exe.config presente nel computer client modificare il valore dell'indirizzo della definizione dell'endpoint in base al nuovo indirizzo del servizio.</span><span class="sxs-lookup"><span data-stu-id="bac2a-180">In the Client.exe.config file on the client computer, change the address value of the endpoint to match the new address of your service.</span></span> <span data-ttu-id="bac2a-181">Tale operazione viene eseguita sostituendo localhost con il nome di dominio completo del server.</span><span class="sxs-lookup"><span data-stu-id="bac2a-181">Do this by replacing localhost with the fully-qualified domain name of the server.</span></span>

10. <span data-ttu-id="bac2a-182">Copiare il file Client.cer dalla directory del client nella directory del servizio sul server.</span><span class="sxs-lookup"><span data-stu-id="bac2a-182">Copy the Client.cer file from the client directory to the service directory on the server.</span></span>

11. <span data-ttu-id="bac2a-183">Sul client, eseguire ImportServiceCert. bat in un Prompt dei comandi per gli sviluppatori per Visual Studio aperto con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="bac2a-183">On the client, run ImportServiceCert.bat in a Developer Command Prompt for Visual Studio opened with administrator privileges.</span></span> <span data-ttu-id="bac2a-184">In questo modo viene importato il certificato del servizio dal file Service.cer nell'archivio CurrentUser - TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="bac2a-184">This imports the service certificate from the Service.cer file into the CurrentUser - TrustedPeople store.</span></span>

12. <span data-ttu-id="bac2a-185">Sul server, eseguire ImportClientCert. bat in un Prompt dei comandi per gli sviluppatori per Visual Studio aperto con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="bac2a-185">On the server, run ImportClientCert.bat in a Developer Command Prompt for Visual Studio opened with administrator privileges.</span></span> <span data-ttu-id="bac2a-186">In questo modo viene importato il certificato del client dal file Client.cer nell'archivio LocalMachine - TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="bac2a-186">This imports the client certificate from the Client.cer file into the LocalMachine - TrustedPeople store.</span></span>

13. <span data-ttu-id="bac2a-187">Sul computer server avviare Service.exe dalla finestra del prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="bac2a-187">On the server computer, launch Service.exe from the command prompt window.</span></span>

14. <span data-ttu-id="bac2a-188">Sul computer client avviare Client.exe da una finestra del prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="bac2a-188">On the client computer, launch Client.exe from a command prompt window.</span></span> <span data-ttu-id="bac2a-189">Se il client e il servizio non sono in grado di comunicare, vedere [Suggerimenti per la risoluzione dei problemi per gli esempi di WCF](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span><span class="sxs-lookup"><span data-stu-id="bac2a-189">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>

#### <a name="to-clean-up-after-the-sample"></a><span data-ttu-id="bac2a-190">Per eseguire la pulizia dopo l'esempio</span><span class="sxs-lookup"><span data-stu-id="bac2a-190">To clean up after the sample</span></span>

1. <span data-ttu-id="bac2a-191">Eseguire Cleanup.bat nella cartella degli esempi una volta completato l'esempio.</span><span class="sxs-lookup"><span data-stu-id="bac2a-191">Run Cleanup.bat in the samples folder once you have finished running the sample.</span></span> <span data-ttu-id="bac2a-192">In questo modo i certificati server e client vengono rimossi dall'archivio certificati.</span><span class="sxs-lookup"><span data-stu-id="bac2a-192">This removes the server and client certificates from the certificate store.</span></span>

> [!NOTE]
> <span data-ttu-id="bac2a-193">Questo script non rimuove i certificati del servizio da un client quando si esegue l'esempio tra più computer.</span><span class="sxs-lookup"><span data-stu-id="bac2a-193">This script does not remove service certificates on a client when running this sample across computers.</span></span> <span data-ttu-id="bac2a-194">Se sono stati eseguiti esempi Windows Communication Foundation (WCF) che usano certificati tra computer, assicurarsi di cancellare i certificati del servizio installati nell'archivio CurrentUser-TrustedPeople.</span><span class="sxs-lookup"><span data-stu-id="bac2a-194">If you have run Windows Communication Foundation (WCF) samples that use certificates across computers, be sure to clear the service certificates that have been installed in the CurrentUser - TrustedPeople store.</span></span> <span data-ttu-id="bac2a-195">Per eseguire questa operazione, usare il seguente comando: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` Ad esempio: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="bac2a-195">To do this, use the following command: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` For example: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.</span></span>

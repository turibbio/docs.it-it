---
title: Blocco della sicurezza delle informazioni personali
ms.date: 03/30/2017
ms.assetid: c44fb338-9527-4dd0-8607-b8787d15acb4
ms.openlocfilehash: 64c07825f0756b029781e173eb2098711cdbe60a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600477"
---
# <a name="pii-security-lockdown"></a><span data-ttu-id="c2684-102">Blocco della sicurezza delle informazioni personali</span><span class="sxs-lookup"><span data-stu-id="c2684-102">PII Security Lockdown</span></span>
<span data-ttu-id="c2684-103">In questo esempio viene illustrato come controllare diverse funzionalità correlate alla sicurezza di un servizio Windows Communication Foundation (WCF) tramite:</span><span class="sxs-lookup"><span data-stu-id="c2684-103">This sample demonstrates how to control several security-related features of a Windows Communication Foundation (WCF) service by:</span></span>  
  
- <span data-ttu-id="c2684-104">Crittografando informazioni riservate nel file di configurazione di un servizio.</span><span class="sxs-lookup"><span data-stu-id="c2684-104">Encrypting sensitive information in a service's configuration file.</span></span>  
  
- <span data-ttu-id="c2684-105">Bloccando gli elementi nel file di configurazione in modo che le sottodirectory annidate del servizio non possano eseguire l'override delle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="c2684-105">Locking elements in the configuration file so that nested service subdirectories cannot override settings.</span></span>  
  
- <span data-ttu-id="c2684-106">Controllando la registrazione delle informazioni personali (PII) nei log di traccia e dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="c2684-106">Controlling the logging of Personally Identifiable Information (PII) in trace and message logs.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="c2684-107">È possibile che gli esempi siano già installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="c2684-107">The samples may already be installed on your computer.</span></span> <span data-ttu-id="c2684-108">Verificare la directory seguente (impostazione predefinita) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="c2684-108">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="c2684-109">Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) ed [!INCLUDE[wf1](../../../../includes/wf1-md.md)] esempi.</span><span class="sxs-lookup"><span data-stu-id="c2684-109">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="c2684-110">Questo esempio si trova nella directory seguente.</span><span class="sxs-lookup"><span data-stu-id="c2684-110">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\SecurityLockdown`  
  
## <a name="discussion"></a><span data-ttu-id="c2684-111">Discussione</span><span class="sxs-lookup"><span data-stu-id="c2684-111">Discussion</span></span>  
 <span data-ttu-id="c2684-112">Queste funzionalità possono essere usate separatamente o tutte insieme per controllare gli aspetti della sicurezza di un servizio.</span><span class="sxs-lookup"><span data-stu-id="c2684-112">Each of these features can be used separately or together to control aspects of a service's security.</span></span> <span data-ttu-id="c2684-113">Non si tratta di una guida definitiva per la protezione di un servizio WCF.</span><span class="sxs-lookup"><span data-stu-id="c2684-113">This is not a definitive guide to securing a WCF service.</span></span>  
  
 <span data-ttu-id="c2684-114">I file di configurazione di .NET Framework possono contenere informazioni riservate, ad esempio stringhe di connessione per connettersi ai database.</span><span class="sxs-lookup"><span data-stu-id="c2684-114">The .NET Framework configuration files can contain sensitive information such as connection strings to connect to databases.</span></span> <span data-ttu-id="c2684-115">Negli scenari condivisi, ospitati da Web, potrebbe essere auspicabile crittografare queste informazioni nel file di configurazione per un servizio, in modo che i dati contenuti all'interno del file di configurazione siano protetti dagli osservatori esterni.</span><span class="sxs-lookup"><span data-stu-id="c2684-115">In shared, Web-hosted scenarios it may be desirable to encrypt this information in the configuration file for a service so that the data contained within the configuration file is resistant to casual viewing.</span></span> <span data-ttu-id="c2684-116">Nella versione 2.0 e successive di .NET Framework è possibile crittografare parti del file di configurazione usando la DPAPI (Windows Data Protection API) o il provider di crittografia RSA.</span><span class="sxs-lookup"><span data-stu-id="c2684-116">.NET Framework 2.0 and later has the ability to encrypt portions of the configuration file using the Windows Data Protection application programming interface (DPAPI) or the RSA Cryptographic provider.</span></span> <span data-ttu-id="c2684-117">L'aspnet_regiis.exe che usa DPAPI o RSA è in grado di crittografare parti selezionate di un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c2684-117">The aspnet_regiis.exe using the DPAPI or RSA can encrypt select portions of a configuration file.</span></span>  
  
 <span data-ttu-id="c2684-118">Negli scenari ospitati da Web è possibile che alcuni servizi siano all'interno di sottodirectory di altri servizi.</span><span class="sxs-lookup"><span data-stu-id="c2684-118">In Web-hosted scenarios it is possible to have services in subdirectories of other services.</span></span> <span data-ttu-id="c2684-119">La semantica predefinita per determinare i valori di configurazione consente ai file di configurazione che si trovano nelle directory annidate di eseguire l'override dei valori di configurazione della directory padre.</span><span class="sxs-lookup"><span data-stu-id="c2684-119">The default semantic for determining configuration values allows configuration files in the nested directories to override the configuration values in the parent directory.</span></span> <span data-ttu-id="c2684-120">In alcune situazioni questo può essere inaccettabile per molteplici ragioni.</span><span class="sxs-lookup"><span data-stu-id="c2684-120">In certain situations this may be undesirable for a variety of reasons.</span></span> <span data-ttu-id="c2684-121">La configurazione del servizio WCF supporta il blocco dei valori di configurazione in modo che la configurazione annidata generi eccezioni quando viene eseguito un servizio annidato utilizzando valori di configurazione sottoposti a override.</span><span class="sxs-lookup"><span data-stu-id="c2684-121">WCF service configuration supports the locking of configuration values so that nested configuration generates exceptions when a nested service is run using overridden configuration values.</span></span>  
  
 <span data-ttu-id="c2684-122">In questo esempio viene illustrato come controllare la registrazione di informazioni personali nei registri di traccia e dei messaggi, come il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="c2684-122">This sample demonstrates how to control the logging of known Personally Identifiable Information (PII) in trace and message logs, such as username and password.</span></span> <span data-ttu-id="c2684-123">Per impostazione predefinita, la registrazione di informazioni personali note è disattivata. Tuttavia in alcune situazioni la registrazione delle informazioni personali può essere importante per eseguire il debug di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c2684-123">By default, logging of known PII is disabled however in certain situations logging of PII can be important in debugging an application.</span></span> <span data-ttu-id="c2684-124">Questo esempio è basato sul [Introduzione](getting-started-sample.md).</span><span class="sxs-lookup"><span data-stu-id="c2684-124">This sample is based on the [Getting Started](getting-started-sample.md).</span></span> <span data-ttu-id="c2684-125">Questo esempio usa inoltre la registrazione di traccia e dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="c2684-125">In addition, this sample uses tracing and message logging.</span></span> <span data-ttu-id="c2684-126">Per ulteriori informazioni, vedere l'esempio [traccia e registrazione dei messaggi](tracing-and-message-logging.md) .</span><span class="sxs-lookup"><span data-stu-id="c2684-126">For more information, see the [Tracing and Message Logging](tracing-and-message-logging.md) sample.</span></span>  
  
## <a name="encrypting-configuration-file-elements"></a><span data-ttu-id="c2684-127">Crittografia degli elementi del file di configurazione</span><span class="sxs-lookup"><span data-stu-id="c2684-127">Encrypting Configuration File Elements</span></span>  
 <span data-ttu-id="c2684-128">Per motivi di sicurezza in un ambiente di hosting Web condiviso, potrebbe essere auspicabile crittografare alcuni elementi di configurazione, ad esempio le stringhe di connessione al database che potrebbero contenere informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="c2684-128">For security purposes in a shared Web-hosting environment, it may be desirable to encrypt certain configuration elements, such as database connection strings that may contain sensitive information.</span></span> <span data-ttu-id="c2684-129">Un elemento di configurazione può essere crittografato utilizzando lo strumento aspnet_regiis. exe disponibile nella cartella .NET Framework ad esempio,%WINDIR%\Microsoft.NET\Framework\v4.0.20728.</span><span class="sxs-lookup"><span data-stu-id="c2684-129">A configuration element may be encrypted using the aspnet_regiis.exe tool found in the .NET Framework folder For example, %WINDIR%\Microsoft.NET\Framework\v4.0.20728.</span></span>  
  
#### <a name="to-encrypt-the-values-in-the-appsettings-section-in-webconfig-for-the-sample"></a><span data-ttu-id="c2684-130">Per crittografare i valori nella sezione appSettings di Web.config per l'esempio</span><span class="sxs-lookup"><span data-stu-id="c2684-130">To encrypt the values in the appSettings section in Web.config for the sample</span></span>  
  
1. <span data-ttu-id="c2684-131">Aprire un prompt dei comandi utilizzando Start->Esegui....</span><span class="sxs-lookup"><span data-stu-id="c2684-131">Open a command prompt by using Start->Run….</span></span> <span data-ttu-id="c2684-132">Digitare `cmd` e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2684-132">Type in `cmd` and click **OK**.</span></span>  
  
2. <span data-ttu-id="c2684-133">Spostarsi alla directory .NET Framework corrente eseguendo il comando seguente: `cd %WINDIR%\Microsoft.NET\Framework\v4.0.20728`.</span><span class="sxs-lookup"><span data-stu-id="c2684-133">Navigate to the current .NET Framework directory by issuing the following command: `cd %WINDIR%\Microsoft.NET\Framework\v4.0.20728`.</span></span>  
  
3. <span data-ttu-id="c2684-134">Crittografare le impostazioni di configurazione appSettings nella cartella Web.config eseguendo il comando seguente: `aspnet_regiis -pe "appSettings" -app "/servicemodelsamples" -prov "DataProtectionConfigurationProvider"`.</span><span class="sxs-lookup"><span data-stu-id="c2684-134">Encrypt the appSettings configuration settings in the Web.config folder by issuing the following command: `aspnet_regiis -pe "appSettings" -app "/servicemodelsamples" -prov "DataProtectionConfigurationProvider"`.</span></span>  
  
 <span data-ttu-id="c2684-135">Per altre informazioni sulla crittografia delle sezioni dei file di configurazione, vedere la pagina relativa alla procedura di configurazione di DPAPI in ASP.NET ([compilazione di applicazioni ASP.NET sicure: autenticazione, autorizzazione e comunicazione protetta](https://docs.microsoft.com/previous-versions/msp-n-p/ff649248(v=pandp.10))) e una procedura per la configurazione di rsa in ASP.NET ([procedura: crittografare le sezioni di configurazione in ASP.NET 2,0 usando RSA](https://docs.microsoft.com/previous-versions/msp-n-p/ff650304(v=pandp.10))).</span><span class="sxs-lookup"><span data-stu-id="c2684-135">More information about encrypting sections of configuration files can be found by reading a how-to on DPAPI in ASP.NET configuration ([Building Secure ASP.NET Applications: Authentication, Authorization, and Secure Communication](https://docs.microsoft.com/previous-versions/msp-n-p/ff649248(v=pandp.10))) and a how-to on RSA in ASP.NET configuration ([How To: Encrypt Configuration Sections in ASP.NET 2.0 Using RSA](https://docs.microsoft.com/previous-versions/msp-n-p/ff650304(v=pandp.10))).</span></span>  
  
## <a name="locking-configuration-file-elements"></a><span data-ttu-id="c2684-136">Blocco degli elementi del file di configurazione</span><span class="sxs-lookup"><span data-stu-id="c2684-136">Locking configuration file elements</span></span>  
 <span data-ttu-id="c2684-137">Negli scenari ospitati da Web è possibile che alcuni servizi siano all'interno di sottodirectory di altri servizi.</span><span class="sxs-lookup"><span data-stu-id="c2684-137">In Web-hosted scenarios, it is possible to have services in subdirectories of services.</span></span> <span data-ttu-id="c2684-138">In queste situazioni, i valori di configurazione per il servizio nella sottodirectory vengono calcolati esaminando i valori in Machine.config e unendoli successivamente con i file Web.config delle directory padre, facendo scorrere verso il basso l'albero di directory e unendo infine il file Web.config alla directory che contiene il servizio.</span><span class="sxs-lookup"><span data-stu-id="c2684-138">In these situations, configuration values for the service in the subdirectory are calculated by examining values in Machine.config and successively merging with any Web.config files in parent directories moving down the directory tree and finally merging the Web.config file in the directory that contains the service.</span></span> <span data-ttu-id="c2684-139">Il comportamento predefinito della maggior parte degli elementi di configurazione è di consentire che i file di configurazione presenti nelle sottodirectory eseguano l'override dei valori impostati nelle directory padre.</span><span class="sxs-lookup"><span data-stu-id="c2684-139">The default behavior for most configuration elements is to allow configuration files in subdirectories to override the values set in parent directories.</span></span> <span data-ttu-id="c2684-140">In alcune situazioni potrebbe essere auspicabile impedire che i file di configurazione presenti nelle sottodirectory eseguano l'override dei valori impostati nella configurazione della directory padre.</span><span class="sxs-lookup"><span data-stu-id="c2684-140">In certain situations it may be desirable to prevent configuration files in subdirectories from overriding values set in parent directory configuration.</span></span>  
  
 <span data-ttu-id="c2684-141">.NET Framework fornisce un modo per bloccare gli elementi del file di configurazione in modo che le configurazioni che eseguono l'override degli elementi di configurazione bloccati generino eccezioni in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c2684-141">The .NET Framework provides a way to lock configuration file elements so that configurations that override locked configuration elements throw run-time exceptions.</span></span>  
  
 <span data-ttu-id="c2684-142">Un elemento di configurazione può essere bloccato specificando l'attributo `lockItem` per un nodo nel file di configurazione. Per bloccare ad esempio il nodo CalculatorServiceBehavior nel file di configurazione in modo che i servizi calcolatrice nei file di configurazione annidati non possano modificare il comportamento, è possibile usare la configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="c2684-142">A configuration element can be locked by specifying the `lockItem` attribute for a node in the configuration file, for example, to lock the CalculatorServiceBehavior node in the configuration file so that calculator services in nested configuration files cannot change the behavior, the following configuration can be used.</span></span>  
  
```xml  
<configuration>  
   <system.serviceModel>  
      <behaviors>
          <serviceBehaviors>
             <behavior name="CalculatorServiceBehavior" lockItem="true">
               <serviceMetadata httpGetEnabled="True"/>
               <serviceDebug includeExceptionDetailInFaults="False" />
             </behavior>
          </serviceBehaviors>
       </behaviors>
    </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="c2684-143">Il blocco degli elementi di configurazione può essere eseguito a livello più specifico.</span><span class="sxs-lookup"><span data-stu-id="c2684-143">Locking of configuration elements can be more specific.</span></span> <span data-ttu-id="c2684-144">È possibile specificare un elenco di elementi come valore per gli oggetti `lockElements` per bloccare un set di elementi all'interno di una raccolta di sottoelementi.</span><span class="sxs-lookup"><span data-stu-id="c2684-144">A list of elements can be specified as the value to the `lockElements` to lock a set of elements within a collection of sub-elements.</span></span> <span data-ttu-id="c2684-145">È possibile specificare un elenco di attributi come valore agli `lockAttributes` per bloccare un gruppo di attributi all'interno di un elemento.</span><span class="sxs-lookup"><span data-stu-id="c2684-145">A list of attributes can be specified as the value to the `lockAttributes` to lock a set of attributes within an element.</span></span> <span data-ttu-id="c2684-146">È possibile bloccare un'intera raccolta di elementi o di attributi, eccetto un elenco selezionato, specificando gli `lockAllElementsExcept` o gli attributi `lockAllAttributesExcept` su un nodo.</span><span class="sxs-lookup"><span data-stu-id="c2684-146">An entire collection of elements or attributes can be locked except for a specified list by specifying the `lockAllElementsExcept` or `lockAllAttributesExcept` attributes on a node.</span></span>  
  
## <a name="pii-logging-configuration"></a><span data-ttu-id="c2684-147">Configurazione della registrazione di informazioni personali</span><span class="sxs-lookup"><span data-stu-id="c2684-147">PII Logging Configuration</span></span>  
 <span data-ttu-id="c2684-148">La registrazione di informazioni personali viene controllata da due opzioni: un'impostazione a livello di computer situata in Machine.config che consente a un amministratore del computer di autorizzare o negare la registrazione di informazioni personali e un'impostazione dell'applicazione che consente a un amministratore dell'applicazione di modificare le autorizzazioni di registrazione di informazioni personali per ogni origine nei file Web.config o App.config.</span><span class="sxs-lookup"><span data-stu-id="c2684-148">Logging of PII is controlled by two switches: a computer-wide setting found in Machine.config that allows a computer administrator to permit or deny logging of PII and an application setting that allows an application administrator to toggle logging of PII for each source in a Web.config or App.config file.</span></span>  
  
 <span data-ttu-id="c2684-149">L'impostazione a livello di computer viene controllata impostando `enableLoggingKnownPii` su `true` o `false` , nell' `machineSettings` elemento in Machine. config. Il codice seguente, ad esempio, consente alle applicazioni di attivare la registrazione delle informazioni personali.</span><span class="sxs-lookup"><span data-stu-id="c2684-149">The computer-wide setting is controlled by setting `enableLoggingKnownPii` to `true` or `false`, in the `machineSettings` element in Machine.config. For example, the following allows applications to turn on logging of PII.</span></span>  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <machineSettings enableLoggingKnownPii="true" />  
    </system.serviceModel>  
</configuration>  
```  
  
> [!NOTE]
> <span data-ttu-id="c2684-150">Il file Machine.config ha un percorso predefinito: %WINDIR%\Microsoft.NET\Framework\v2.0.50727\CONFIG.</span><span class="sxs-lookup"><span data-stu-id="c2684-150">The Machine.config file has a default location: %WINDIR%\Microsoft.NET\Framework\v2.0.50727\CONFIG.</span></span>  
  
 <span data-ttu-id="c2684-151">Se l'attributo `enableLoggingKnownPii` non è presente in Machine.config, la registrazione delle informazioni personali non è consentita.</span><span class="sxs-lookup"><span data-stu-id="c2684-151">If the `enableLoggingKnownPii` attribute is not present in Machine.config, logging of PII is not allowed.</span></span>  
  
 <span data-ttu-id="c2684-152">È possibile abilitare la registrazione delle informazioni personali in un'applicazione impostando l'attributo `logKnownPii` dell'elemento di origine su `true` o `false` nei file Web.config o App.config.</span><span class="sxs-lookup"><span data-stu-id="c2684-152">Enabling logging of PII for an application is done by setting the `logKnownPii` attribute of the source element to `true` or `false` in the Web.config or App.config file.</span></span> <span data-ttu-id="c2684-153">Ad esempio, gli elementi seguenti abilitano la registrazione delle informazioni personali per la registrazione di traccia e dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="c2684-153">For example, the following enables logging of PII for both message logging and trace logging.</span></span>  
  
```xml  
<configuration>  
    <system.diagnostics>  
        <sources>  
            <source name="System.ServiceModel.MessageLogging" logKnownPii="true">  
                <listeners>
                ...
                </listeners>  
            </source>  
            <source name="System.ServiceModel" switchValue="Verbose, ActivityTracing">  
            <listeners>  
        ...
            </listeners>  
            </source>  
        </sources>  
    </system.diagnostics>  
</configuration>  
```  
  
 <span data-ttu-id="c2684-154">Se l'attributo `logKnownPii` non è stato specificato, le informazioni personali non vengono registrate.</span><span class="sxs-lookup"><span data-stu-id="c2684-154">If the `logKnownPii` attribute is not specified, then PII is not logged.</span></span>  
  
 <span data-ttu-id="c2684-155">Le informazioni personali vengono registrate solo se `enableLoggingKnownPii` è impostato su `true` e `logKnownPii` è impostato su `true`.</span><span class="sxs-lookup"><span data-stu-id="c2684-155">PII is only logged if both `enableLoggingKnownPii` is set to `true`, and `logKnownPii` is set to `true`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c2684-156">System.Diagnostics ignora tutti gli attributi di tutte le origini tranne la prima elencata nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c2684-156">System.Diagnostics ignores all attributes on all sources except the first one listed in the configuration file.</span></span> <span data-ttu-id="c2684-157">Aggiungendo l'attributo `logKnownPii` alla seconda origine nel file di configurazione non ha alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="c2684-157">Adding the `logKnownPii` attribute to the second source in the configuration file has no effect.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="c2684-158">Per eseguire questo esempio, comporta la modifica manuale di Machine. config. Prestare attenzione quando si modifica machine. config come valori non corretti o la sintassi potrebbe impedire l'esecuzione di tutte le applicazioni .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c2684-158">To run this sample involves manual modification of Machine.config. Care should be taken when modifying Machine.config as incorrect values or syntax may prevent all .NET Framework applications from running.</span></span>  
  
 <span data-ttu-id="c2684-159">È inoltre possibile crittografare gli elementi del file di configurazione usando DPAPI e RSA.</span><span class="sxs-lookup"><span data-stu-id="c2684-159">It is also possible to encrypt configuration file elements using DPAPI and RSA.</span></span> <span data-ttu-id="c2684-160">Per ulteriori informazioni, vedere i seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="c2684-160">For more information, see the following links:</span></span>  
  
- <span data-ttu-id="c2684-161">[Come compilare applicazioni ASP.NET protette: autenticazione, autorizzazione e comunicazioni protette (la pagina potrebbe essere in inglese)](https://docs.microsoft.com/previous-versions/msp-n-p/ff649248(v=pandp.10))</span><span class="sxs-lookup"><span data-stu-id="c2684-161">[Building Secure ASP.NET Applications: Authentication, Authorization, and Secure Communication](https://docs.microsoft.com/previous-versions/msp-n-p/ff649248(v=pandp.10))</span></span>  
  
- <span data-ttu-id="c2684-162">[Procedura: crittografare le sezioni di configurazione in ASP.NET 2.0 utilizzando RSA](https://docs.microsoft.com/previous-versions/msp-n-p/ff650304(v=pandp.10))</span><span class="sxs-lookup"><span data-stu-id="c2684-162">[How To: Encrypt Configuration Sections in ASP.NET 2.0 Using RSA](https://docs.microsoft.com/previous-versions/msp-n-p/ff650304(v=pandp.10))</span></span>  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="c2684-163">Per impostare, compilare ed eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="c2684-163">To set up, build and run the sample</span></span>  
  
1. <span data-ttu-id="c2684-164">Assicurarsi di avere eseguito la [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c2684-164">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="c2684-165">Modificare Machine.config per impostare l'attributo `enableLoggingKnownPii` su `true`, aggiungendo i nodi padre se necessario.</span><span class="sxs-lookup"><span data-stu-id="c2684-165">Edit Machine.config to set the `enableLoggingKnownPii` attribute to `true`, adding the parent nodes if necessary.</span></span>  
  
3. <span data-ttu-id="c2684-166">Per compilare l'edizione in C# o Visual Basic .NET della soluzione, seguire le istruzioni in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c2684-166">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
4. <span data-ttu-id="c2684-167">Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [esecuzione degli esempi di Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c2684-167">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
#### <a name="to-clean-up-the-sample"></a><span data-ttu-id="c2684-168">Per eseguire la pulizia dell'esempio</span><span class="sxs-lookup"><span data-stu-id="c2684-168">To clean up the sample</span></span>  
  
1. <span data-ttu-id="c2684-169">Modificare Machine.config per impostare l'attributo `enableLoggingKnownPii` su `false`.</span><span class="sxs-lookup"><span data-stu-id="c2684-169">Edit Machine.config to set the `enableLoggingKnownPii` attribute to `false`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c2684-170">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c2684-170">See also</span></span>

- <span data-ttu-id="c2684-171">[Monitoraggio](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="c2684-171">[AppFabric Monitoring Samples](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))</span></span>

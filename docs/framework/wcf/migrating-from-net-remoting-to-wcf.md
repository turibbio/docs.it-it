---
title: Migrazione da .NET Remoting a WCF
description: Informazioni su come eseguire la migrazione di un'applicazione che utilizza .NET Remoting per utilizzare WCF. In WCF è possibile eseguire diversi scenari comuni di comunicazione remota.
ms.date: 03/30/2017
ms.assetid: 16902a42-ef80-40e9-8c4c-90e61ddfdfe5
ms.openlocfilehash: f6f526db09806008314980b71233b208d25359fc
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246155"
---
# <a name="migrating-from-net-remoting-to-wcf"></a><span data-ttu-id="aa628-104">Migrazione da .NET Remoting a WCF</span><span class="sxs-lookup"><span data-stu-id="aa628-104">Migrating from .NET Remoting to WCF</span></span>
<span data-ttu-id="aa628-105">In questo articolo viene descritto come eseguire la migrazione di un'applicazione che usa Servizi remoti .NET per l'uso di Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="aa628-105">This article describes how to migrate an application that uses .NET Remoting to use Windows Communication Foundation (WCF).</span></span> <span data-ttu-id="aa628-106">Vengono confrontati concetti simili tra questi prodotti e quindi viene descritto come realizzare diversi scenari comuni di Servizi remoti .NET in WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-106">It compares similar concepts between these products and then describes how to accomplish several common Remoting scenarios in WCF.</span></span>  
  
 <span data-ttu-id="aa628-107">Servizi remoti .NET è un prodotto legacy supportato solo per la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="aa628-107">.NET Remoting is a legacy product that is supported only for backward compatibility.</span></span> <span data-ttu-id="aa628-108">Non è sicuro in ambienti ad attendibilità mista poiché non è in grado di mantenere livelli di attendibilità distinti tra il client e il server.</span><span class="sxs-lookup"><span data-stu-id="aa628-108">It is not secure across mixed-trust environments because it cannot maintain the separate trust levels between client and server.</span></span> <span data-ttu-id="aa628-109">Ad esempio, è consigliabile non esporre mai un endpoint Servizi remoti .NET a Internet o a client non attendibili.</span><span class="sxs-lookup"><span data-stu-id="aa628-109">For example, you should never expose a .NET Remoting endpoint to the Internet or to untrusted clients.</span></span> <span data-ttu-id="aa628-110">Si consiglia di eseguire la migrazione delle applicazioni Servizi remoti .NET esistenti a tecnologie più recenti e sicure.</span><span class="sxs-lookup"><span data-stu-id="aa628-110">We recommend existing Remoting applications be migrated to newer and more secure technologies.</span></span> <span data-ttu-id="aa628-111">Se la progettazione dell'applicazione usa solo HTTP ed è RESTful, è consigliabile l'API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="aa628-111">If the application’s design uses only HTTP and is RESTful, we recommend ASP.NET Web API.</span></span> <span data-ttu-id="aa628-112">Per altre informazioni, vedere l'API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="aa628-112">For more information, see ASP.NET Web API.</span></span> <span data-ttu-id="aa628-113">Se l'applicazione è basata su SOAP o richiede protocolli diversi da HTTP, come ad esempio TCP, è consigliabile WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-113">If the application is based on SOAP or requires non-Http protocols such as TCP, we recommend WCF.</span></span>  

## <a name="comparing-net-remoting-to-wcf"></a><span data-ttu-id="aa628-114">Confronto tra Servizi remoti .NET e WCF</span><span class="sxs-lookup"><span data-stu-id="aa628-114">Comparing .NET Remoting to WCF</span></span>  
 <span data-ttu-id="aa628-115">In questa sezione vengono confrontati i componenti di base di Servizi remoti .NET con gli equivalenti di WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-115">This section compares the basic building blocks of .NET Remoting with their WCF equivalents.</span></span> <span data-ttu-id="aa628-116">Questi blocchi predefiniti vengono usati in un secondo momento per creare alcuni scenari client-server comuni in WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-116">We will use these building blocks later to create some common client-server scenarios in WCF.</span></span> <span data-ttu-id="aa628-117">Nel grafico seguente sono riepilogate le analogie e le differenze principali tra .NET Remoting e WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-117">The following chart summarizes the main similarities and differences between .NET Remoting and WCF.</span></span>  
  
||<span data-ttu-id="aa628-118">Servizi remoti .NET</span><span class="sxs-lookup"><span data-stu-id="aa628-118">.NET Remoting</span></span>|<span data-ttu-id="aa628-119">WCF</span><span class="sxs-lookup"><span data-stu-id="aa628-119">WCF</span></span>|  
|-|-------------------|---------|  
|<span data-ttu-id="aa628-120">Tipo di server</span><span class="sxs-lookup"><span data-stu-id="aa628-120">Server type</span></span>|<span data-ttu-id="aa628-121">Sottoclasse MarshalByRefObject</span><span class="sxs-lookup"><span data-stu-id="aa628-121">Subclass MarshalByRefObject</span></span>|<span data-ttu-id="aa628-122">Contrassegno con l'attributo [ServiceContract]</span><span class="sxs-lookup"><span data-stu-id="aa628-122">Mark with [ServiceContract] attribute</span></span>|  
|<span data-ttu-id="aa628-123">Operazioni di servizio</span><span class="sxs-lookup"><span data-stu-id="aa628-123">Service operations</span></span>|<span data-ttu-id="aa628-124">Metodi pubblici nel tipo di server</span><span class="sxs-lookup"><span data-stu-id="aa628-124">Public methods on server type</span></span>|<span data-ttu-id="aa628-125">Contrassegno con l'attributo [OperationContract]</span><span class="sxs-lookup"><span data-stu-id="aa628-125">Mark with [OperationContract] attribute</span></span>|  
|<span data-ttu-id="aa628-126">Serializzazione</span><span class="sxs-lookup"><span data-stu-id="aa628-126">Serialization</span></span>|<span data-ttu-id="aa628-127">ISerializable o [Serializable]</span><span class="sxs-lookup"><span data-stu-id="aa628-127">ISerializable or [Serializable]</span></span>|<span data-ttu-id="aa628-128">DataContractSerializer o XmlSerializer</span><span class="sxs-lookup"><span data-stu-id="aa628-128">DataContractSerializer or XmlSerializer</span></span>|  
|<span data-ttu-id="aa628-129">Oggetti passati</span><span class="sxs-lookup"><span data-stu-id="aa628-129">Objects passed</span></span>|<span data-ttu-id="aa628-130">In base al valore o in base al riferimento</span><span class="sxs-lookup"><span data-stu-id="aa628-130">By-value or by-reference</span></span>|<span data-ttu-id="aa628-131">Solo in base al valore</span><span class="sxs-lookup"><span data-stu-id="aa628-131">By-value only</span></span>|  
|<span data-ttu-id="aa628-132">Errori/eccezioni</span><span class="sxs-lookup"><span data-stu-id="aa628-132">Errors/exceptions</span></span>|<span data-ttu-id="aa628-133">Qualsiasi eccezione serializzabile</span><span class="sxs-lookup"><span data-stu-id="aa628-133">Any serializable exception</span></span>|<span data-ttu-id="aa628-134">FaultContract\<TDetail></span><span class="sxs-lookup"><span data-stu-id="aa628-134">FaultContract\<TDetail></span></span>|  
|<span data-ttu-id="aa628-135">Oggetti proxy client</span><span class="sxs-lookup"><span data-stu-id="aa628-135">Client proxy objects</span></span>|<span data-ttu-id="aa628-136">Proxy trasparenti fortemente tipizzati vengono creati automaticamente da MarshalByRefObjects</span><span class="sxs-lookup"><span data-stu-id="aa628-136">Strongly typed transparent proxies are created automatically from MarshalByRefObjects</span></span>|<span data-ttu-id="aa628-137">I proxy fortemente tipizzati vengono generati su richiesta con ChannelFactory\<TChannel></span><span class="sxs-lookup"><span data-stu-id="aa628-137">Strongly typed proxies are generated on-demand using ChannelFactory\<TChannel></span></span>|  
|<span data-ttu-id="aa628-138">Piattaforma richiesta</span><span class="sxs-lookup"><span data-stu-id="aa628-138">Platform required</span></span>|<span data-ttu-id="aa628-139">Sia il client che il server devono usare un sistema operativo Microsoft e .NET</span><span class="sxs-lookup"><span data-stu-id="aa628-139">Both client and server must use Microsoft OS and .NET</span></span>|<span data-ttu-id="aa628-140">Multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="aa628-140">Cross-platform</span></span>|  
|<span data-ttu-id="aa628-141">Formato dei messaggi</span><span class="sxs-lookup"><span data-stu-id="aa628-141">Message format</span></span>|<span data-ttu-id="aa628-142">Private</span><span class="sxs-lookup"><span data-stu-id="aa628-142">Private</span></span>|<span data-ttu-id="aa628-143">Standard di settore (SOAP, WS-\* e così via)</span><span class="sxs-lookup"><span data-stu-id="aa628-143">Industry standards (SOAP, WS-\*, etc.)</span></span>|  
  
### <a name="server-implementation-comparison"></a><span data-ttu-id="aa628-144">Confronto dell'implementazione server</span><span class="sxs-lookup"><span data-stu-id="aa628-144">Server Implementation Comparison</span></span>  
  
#### <a name="creating-a-server-in-net-remoting"></a><span data-ttu-id="aa628-145">Creazione di un server in Servizi remoti .NET</span><span class="sxs-lookup"><span data-stu-id="aa628-145">Creating a Server in .NET Remoting</span></span>  
 <span data-ttu-id="aa628-146">I tipi di server di Servizi remoti .NET devono derivare da MarshalByRefObject e definire i metodi che il client può chiamare, nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="aa628-146">.NET Remoting server types must derive from MarshalByRefObject and define methods the client can call, like the following:</span></span>  
  
```csharp
public class RemotingServer : MarshalByRefObject  
{  
    public Customer GetCustomer(int customerId) { … }  
}  
```  
  
 <span data-ttu-id="aa628-147">I metodi pubblici di questo tipo di server diventano il contratto pubblico disponibile per i client.</span><span class="sxs-lookup"><span data-stu-id="aa628-147">The public methods of this server type become the public contract available to clients.</span></span>  <span data-ttu-id="aa628-148">Non vi è alcuna separazione tra l'interfaccia pubblica del server e la relativa implementazione: un solo tipo le gestisce entrambe.</span><span class="sxs-lookup"><span data-stu-id="aa628-148">There is no separation between the server’s public interface and its implementation – one type handles both.</span></span>  
  
 <span data-ttu-id="aa628-149">Dopo aver definito il tipo di server, questo può essere reso disponibile ai client, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="aa628-149">Once the server type has been defined, it can be made available to clients, like in the following example:</span></span>  
  
```csharp
TcpChannel channel = new TcpChannel(8080);  
ChannelServices.RegisterChannel(channel, ensureSecurity : true);  
RemotingConfiguration.RegisterWellKnownServiceType(  
    typeof(RemotingServer),
    "RemotingServer",
    WellKnownObjectMode.Singleton);  
Console.WriteLine("RemotingServer is running.  Press ENTER to terminate...");  
Console.ReadLine();  
```  
  
 <span data-ttu-id="aa628-150">Esistono diversi modi per rendere disponibile il tipo di Servizi remoti .NET come server, incluso l'uso di file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa628-150">There are many ways to make the Remoting type available as a server, including using configuration files.</span></span> <span data-ttu-id="aa628-151">Questo è solo un esempio.</span><span class="sxs-lookup"><span data-stu-id="aa628-151">This is just one example.</span></span>  
  
#### <a name="creating-a-server-in-wcf"></a><span data-ttu-id="aa628-152">Creazione di un server in WCF</span><span class="sxs-lookup"><span data-stu-id="aa628-152">Creating a Server in WCF</span></span>  
 <span data-ttu-id="aa628-153">Il passaggio equivalente in WCF prevede la creazione di due tipi: il "contratto di servizio" pubblico e l'implementazione concreta.</span><span class="sxs-lookup"><span data-stu-id="aa628-153">The equivalent step in WCF involves creating two types -- the public "service contract" and the concrete implementation.</span></span> <span data-ttu-id="aa628-154">Il primo viene dichiarato come un'interfaccia contrassegnata con [ServiceContract].</span><span class="sxs-lookup"><span data-stu-id="aa628-154">The first is declared as an interface marked with [ServiceContract].</span></span> <span data-ttu-id="aa628-155">I metodi disponibili per i client sono contrassegnati con [OperationContract]:</span><span class="sxs-lookup"><span data-stu-id="aa628-155">Methods available to clients are marked with [OperationContract]:</span></span>  
  
```csharp
[ServiceContract]  
public interface IWCFServer  
{  
    [OperationContract]  
    Customer GetCustomer(int customerId);  
}  
```  
  
 <span data-ttu-id="aa628-156">L'implementazione del server è definita in una classe concreta distinta, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="aa628-156">The server’s implementation is defined in a separate concrete class, like in the following example:</span></span>  
  
```csharp
public class WCFServer : IWCFServer  
{  
    public Customer GetCustomer(int customerId) { … }  
}  
```  
  
 <span data-ttu-id="aa628-157">Dopo aver definito questi tipi, il server WCF può essere reso disponibile ai client, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="aa628-157">Once these types have been defined, the WCF server can be made available to clients, like in the following example:</span></span>  
  
```csharp
NetTcpBinding binding = new NetTcpBinding();  
Uri baseAddress = new Uri("net.tcp://localhost:8000/wcfserver");  
  
using (ServiceHost serviceHost = new ServiceHost(typeof(WCFServer), baseAddress))  
{  
    serviceHost.AddServiceEndpoint(typeof(IWCFServer), binding, baseAddress);  
    serviceHost.Open();  
  
    Console.WriteLine($"The WCF server is ready at {baseAddress}.");
    Console.WriteLine("Press <ENTER> to terminate service...");  
    Console.WriteLine();  
    Console.ReadLine();  
}  
```  
  
> [!NOTE]
> <span data-ttu-id="aa628-158">Viene usato TCP in entrambi gli esempi per mantenerli quanto più simili possibile.</span><span class="sxs-lookup"><span data-stu-id="aa628-158">TCP is used in both examples to keep them as similar as possible.</span></span> <span data-ttu-id="aa628-159">Per esempi relativi all'uso di HTTP, fare riferimento alle procedure dettagliate per gli scenari, disponibili più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="aa628-159">Refer to the scenario walk-throughs later in this topic for examples using HTTP.</span></span>  
  
 <span data-ttu-id="aa628-160">Esistono diversi modi per configurare e ospitare servizi WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-160">There are many ways to configure and to host WCF services.</span></span> <span data-ttu-id="aa628-161">Questo è solo un esempio, basato su un approccio "self-hosted".</span><span class="sxs-lookup"><span data-stu-id="aa628-161">This is just one example, known as "self-hosted".</span></span> <span data-ttu-id="aa628-162">Per altre informazioni, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa628-162">For more information, see the following topics:</span></span>  
  
- [<span data-ttu-id="aa628-163">Procedura: Definire un contratto di servizio</span><span class="sxs-lookup"><span data-stu-id="aa628-163">How to: Define a Service Contract</span></span>](how-to-define-a-wcf-service-contract.md)  
  
- [<span data-ttu-id="aa628-164">Configurazione dei servizi tramite file di configurazione</span><span class="sxs-lookup"><span data-stu-id="aa628-164">Configuring Services Using Configuration Files</span></span>](configuring-services-using-configuration-files.md)  
  
- [<span data-ttu-id="aa628-165">Servizi di hosting</span><span class="sxs-lookup"><span data-stu-id="aa628-165">Hosting Services</span></span>](hosting-services.md)  
  
### <a name="client-implementation-comparison"></a><span data-ttu-id="aa628-166">Confronto dell'implementazione client</span><span class="sxs-lookup"><span data-stu-id="aa628-166">Client Implementation Comparison</span></span>  
  
#### <a name="creating-a-client-in-net-remoting"></a><span data-ttu-id="aa628-167">Creazione di un client in Servizi remoti .NET</span><span class="sxs-lookup"><span data-stu-id="aa628-167">Creating a Client in .NET Remoting</span></span>  
 <span data-ttu-id="aa628-168">Una volta che è stato reso disponibile un oggetto server Servizi remoti .NET, questo può essere usato dai client, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="aa628-168">Once a .NET Remoting server object has been made available, it can be consumed by clients, like in the following example:</span></span>  
  
```csharp
TcpChannel channel = new TcpChannel();  
ChannelServices.RegisterChannel(channel, ensureSecurity : true);  
RemotingServer server = (RemotingServer)Activator.GetObject(  
                            typeof(RemotingServer),
                            "tcp://localhost:8080/RemotingServer");  
  
RemotingCustomer customer = server.GetCustomer(42);  
Console.WriteLine($"Customer {customer.FirstName} {customer.LastName} received.");
```  
  
 <span data-ttu-id="aa628-169">L'istanza RemotingServer restituita da Activator.GetObject() è denominata "proxy trasparente".</span><span class="sxs-lookup"><span data-stu-id="aa628-169">The RemotingServer instance returned from Activator.GetObject() is known as a "transparent proxy."</span></span> <span data-ttu-id="aa628-170">Implementa l'API pubblica per il tipo RemotingServer sul client, ma tutti i metodi chiamano l'oggetto server in esecuzione in un altro processo o computer.</span><span class="sxs-lookup"><span data-stu-id="aa628-170">It implements the public API for the RemotingServer type on the client, but all the methods call the server object running in a different process or machine.</span></span>  
  
#### <a name="creating-a-client-in-wcf"></a><span data-ttu-id="aa628-171">Creazione di un client in WCF</span><span class="sxs-lookup"><span data-stu-id="aa628-171">Creating a Client in WCF</span></span>  
 <span data-ttu-id="aa628-172">Il passaggio equivalente in WCF prevede l'uso di una channel factory per creare il proxy in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="aa628-172">The equivalent step in WCF involves using a channel factory to create the proxy explicitly.</span></span> <span data-ttu-id="aa628-173">Analogamente a Servizi remoti .NET, l'oggetto proxy può essere usato per richiamare operazioni sul server, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="aa628-173">Like Remoting, the proxy object can be used to invoke operations on the server, like in the following example:</span></span>  
  
```csharp
NetTcpBinding binding = new NetTcpBinding();  
String url = "net.tcp://localhost:8000/wcfserver";  
EndpointAddress address = new EndpointAddress(url);  
ChannelFactory<IWCFServer> channelFactory =
    new ChannelFactory<IWCFServer>(binding, address);  
IWCFServer server = channelFactory.CreateChannel();  
  
Customer customer = server.GetCustomer(42);  
Console.WriteLine($"  Customer {customer.FirstName} {customer.LastName} received.");
```  
  
 <span data-ttu-id="aa628-174">In questo esempio viene illustrata la programmazione a livello di canale perché è molto simile all'esempio relativo a Servizi remoti .NET.</span><span class="sxs-lookup"><span data-stu-id="aa628-174">This example shows programming at the channel level because it is most similar to the Remoting example.</span></span> <span data-ttu-id="aa628-175">È disponibile anche l'approccio **Aggiungi riferimento al servizio** in Visual Studio che genera codice per semplificare la programmazione client.</span><span class="sxs-lookup"><span data-stu-id="aa628-175">Also available is the **Add Service Reference** approach in Visual Studio that generates code to simplify client programming.</span></span> <span data-ttu-id="aa628-176">Per altre informazioni, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa628-176">For more information, see the following topics:</span></span>  
  
- [<span data-ttu-id="aa628-177">Programmazione a livello di canale client</span><span class="sxs-lookup"><span data-stu-id="aa628-177">Client Channel-Level Programming</span></span>](./extending/client-channel-level-programming.md)  
  
- [<span data-ttu-id="aa628-178">Procedura: aggiungere, aggiornare o rimuovere un riferimento al servizio</span><span class="sxs-lookup"><span data-stu-id="aa628-178">How to: Add, Update, or Remove a Service Reference</span></span>](/visualstudio/data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference)  
  
### <a name="serialization-usage"></a><span data-ttu-id="aa628-179">Uso della serializzazione</span><span class="sxs-lookup"><span data-stu-id="aa628-179">Serialization Usage</span></span>  
 <span data-ttu-id="aa628-180">Sia Servizi remoti .NET che WCF usano la serializzazione per l'invio di oggetti tra il client e il server, ma vi sono tre importanti differenze:</span><span class="sxs-lookup"><span data-stu-id="aa628-180">Both .NET Remoting and WCF use serialization to send objects between client and server, but they differ in these important ways:</span></span>  
  
1. <span data-ttu-id="aa628-181">Vengono usati serializzatori e convenzioni differenti per indicare gli elementi da serializzare.</span><span class="sxs-lookup"><span data-stu-id="aa628-181">They use different serializers and conventions to indicate what to serialize.</span></span>  
  
2. <span data-ttu-id="aa628-182">Servizi remoti .NET supporta la serializzazione "in base al riferimento", che consente l'accesso a proprietà o metodi su un livello per l'esecuzione di codice su un altro livello, ovvero attraverso i limiti di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="aa628-182">.NET Remoting supports "by reference" serialization that allows method or property access on one tier to execute code on the other tier, which is across security boundaries.</span></span> <span data-ttu-id="aa628-183">Questa funzionalità espone vulnerabilità di sicurezza e rappresenta uno dei motivi principali per cui gli endpoint Servizi remoti .NET non devono mai essere esposti a client non attendibili.</span><span class="sxs-lookup"><span data-stu-id="aa628-183">This capability exposes security vulnerabilities and is one of the main reasons why Remoting endpoints should never be exposed to untrusted clients.</span></span>  
  
3. <span data-ttu-id="aa628-184">La serializzazione usata da Servizi remoti .NET è di tipo opt-out (vengono esclusi in modo esplicito gli elementi da non serializzare), mentre la serializzazione di WCF è di tipo opt-in (vengono contrassegnati in modo esplicito i membri da serializzare).</span><span class="sxs-lookup"><span data-stu-id="aa628-184">Serialization used by Remoting is opt-out (explicitly exclude what not to serialize) and WCF serialization is opt-in (explicitly mark which members to serialize).</span></span>  
  
#### <a name="serialization-in-net-remoting"></a><span data-ttu-id="aa628-185">Serializzazione in Servizi remoti .NET</span><span class="sxs-lookup"><span data-stu-id="aa628-185">Serialization in .NET Remoting</span></span>  
 <span data-ttu-id="aa628-186">Servizi remoti .NET supporta due modi per serializzare e deserializzare gli oggetti tra client e server:</span><span class="sxs-lookup"><span data-stu-id="aa628-186">.NET Remoting supports two ways to serialize and deserialize objects between the client and server:</span></span>  
  
- <span data-ttu-id="aa628-187">*Per valore* : i valori dell'oggetto vengono serializzati attraverso i limiti del livello e viene creata una nuova istanza dell'oggetto nell'altro livello.</span><span class="sxs-lookup"><span data-stu-id="aa628-187">*By value* – the values of the object are serialized across tier boundaries, and a new instance of that object is created on the other tier.</span></span> <span data-ttu-id="aa628-188">Tutte le chiamate a metodi o proprietà della nuova istanza sono in esecuzione solo in locale e non influiscono sull'oggetto o sul livello originale.</span><span class="sxs-lookup"><span data-stu-id="aa628-188">Any calls to methods or properties of that new instance execute only locally and do not affect the original object or tier.</span></span>  
  
- <span data-ttu-id="aa628-189">*Per riferimento* : un "riferimento a un oggetto" speciale viene serializzato attraverso i limiti del livello.</span><span class="sxs-lookup"><span data-stu-id="aa628-189">*By reference* – a special "object reference" is serialized across tier boundaries.</span></span> <span data-ttu-id="aa628-190">Quando un livello interagisce con metodi o proprietà di tale oggetto, comunica con l'oggetto originale nel livello originale.</span><span class="sxs-lookup"><span data-stu-id="aa628-190">When one tier interacts with methods or properties of that object, it communicates back to the original object on the original tier.</span></span> <span data-ttu-id="aa628-191">Il flusso degli oggetti in base al riferimento può avvenire in entrambe le direzioni: dal server al client o dal client al server.</span><span class="sxs-lookup"><span data-stu-id="aa628-191">By-reference objects can flow in either direction – server to client, or client to server.</span></span>  
  
 <span data-ttu-id="aa628-192">I tipi in base al valore in Servizi remoti .NET sono contrassegnati con l'attributo [Serializable] o implementano ISerializable, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="aa628-192">By-value types in Remoting are marked with the [Serializable] attribute or implement ISerializable, like in the following example:</span></span>  
  
```csharp
[Serializable]  
public class RemotingCustomer  
{  
    public string FirstName { get; set; }  
    public string LastName { get; set; }  
    public int CustomerId { get; set; }  
}  
```  
  
 <span data-ttu-id="aa628-193">I tipi in base al riferimento derivano dalla classe MarshalByRefObject, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="aa628-193">By-reference types derive from the MarshalByRefObject class, like in the following example:</span></span>  
  
```csharp
public class RemotingCustomerReference : MarshalByRefObject  
{  
    public string FirstName { get; set; }  
    public string LastName { get; set; }  
    public int CustomerId { get; set; }  
}  
```  
  
 <span data-ttu-id="aa628-194">È estremamente importante comprendere le implicazioni degli oggetti in base al riferimento di Servizi remoti .NET.</span><span class="sxs-lookup"><span data-stu-id="aa628-194">It is extremely important to understand the implications of Remoting’s by-reference objects.</span></span> <span data-ttu-id="aa628-195">Se un livello (client o server) invia un oggetto in base al riferimento all'altro livello, tutte le chiamate di metodi vengono eseguite nel livello proprietario dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="aa628-195">If either tier (client or server) sends a by-reference object to the other tier, all method calls execute back on the tier owning the object.</span></span> <span data-ttu-id="aa628-196">Ad esempio, un client che esegue la chiamata di metodi su un oggetto in base al riferimento restituito dal server eseguirà il codice sul server.</span><span class="sxs-lookup"><span data-stu-id="aa628-196">For example, a client calling methods on a by-reference object returned by the server will execute code on the server.</span></span> <span data-ttu-id="aa628-197">Analogamente, un server che esegue la chiamata di metodi su un oggetto in base al riferimento fornito dal client eseguirà il codice sul client.</span><span class="sxs-lookup"><span data-stu-id="aa628-197">Similarly, a server calling methods on a by-reference object provided by the client will execute code back on the client.</span></span> <span data-ttu-id="aa628-198">Per questo motivo, l'uso di Servizi remoti .NET è consigliabile solo all'interno di ambienti completamente attendibili.</span><span class="sxs-lookup"><span data-stu-id="aa628-198">For this reason, the use of .NET Remoting is recommended only within fully-trusted environments.</span></span> <span data-ttu-id="aa628-199">L'esposizione di un endpoint Servizi remoti .NET pubblico a client non attendibili renderà vulnerabile agli attacchi un server Servizi remoti .NET.</span><span class="sxs-lookup"><span data-stu-id="aa628-199">Exposing a public .NET Remoting endpoint to untrusted clients will make a Remoting server vulnerable to attack.</span></span>  
  
#### <a name="serialization-in-wcf"></a><span data-ttu-id="aa628-200">Serializzazione in WCF</span><span class="sxs-lookup"><span data-stu-id="aa628-200">Serialization in WCF</span></span>  
 <span data-ttu-id="aa628-201">WCF supporta solo la serializzazione in base al valore.</span><span class="sxs-lookup"><span data-stu-id="aa628-201">WCF supports only by-value serialization.</span></span> <span data-ttu-id="aa628-202">Il modo più comune per definire un tipo per lo scambio tra client e server è simile a quello riportato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="aa628-202">The most common way to define a type to exchange between client and server is like in the following example:</span></span>  
  
```csharp
[DataContract]  
public class WCFCustomer  
{  
    [DataMember]  
    public string FirstName { get; set; }  
  
    [DataMember]  
    public string LastName { get; set; }  
  
    [DataMember]  
    public int CustomerId { get; set; }  
}  
```  
  
 <span data-ttu-id="aa628-203">L'attributo [DataContract] identifica questo tipo come serializzabile e deserializzabile tra client e server.</span><span class="sxs-lookup"><span data-stu-id="aa628-203">The [DataContract] attribute identifies this type as one that can be serialized and deserialized between client and server.</span></span> <span data-ttu-id="aa628-204">L'attributo [DataMember] identifica le singole proprietà o i singoli campi da serializzare.</span><span class="sxs-lookup"><span data-stu-id="aa628-204">The [DataMember] attribute identifies the individual properties or fields to serialize.</span></span>  
  
 <span data-ttu-id="aa628-205">Quando WCF invia un oggetto tra i livelli, serializza solo i valori e crea una nuova istanza dell'oggetto nell'altro livello.</span><span class="sxs-lookup"><span data-stu-id="aa628-205">When WCF sends an object across tiers, it serializes only the values and creates a new instance of the object on the other tier.</span></span> <span data-ttu-id="aa628-206">Tutte le interazioni con i valori dell'oggetto avvengono solo in locale: non comunicano con l'altro livello come nel caso degli oggetti in base al riferimento di Servizi remoti .NET.</span><span class="sxs-lookup"><span data-stu-id="aa628-206">Any interactions with the values of the object occur only locally – they do not communicate with the other tier the way .NET Remoting by-reference objects do.</span></span> <span data-ttu-id="aa628-207">Per ulteriori informazioni, vedere [serializzazione e deserializzazione](./feature-details/serialization-and-deserialization.md).</span><span class="sxs-lookup"><span data-stu-id="aa628-207">For more information, see [Serialization and Deserialization](./feature-details/serialization-and-deserialization.md).</span></span>  
  
### <a name="exception-handling-capabilities"></a><span data-ttu-id="aa628-208">Funzionalità di gestione delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="aa628-208">Exception Handling Capabilities</span></span>  
  
#### <a name="exceptions-in-net-remoting"></a><span data-ttu-id="aa628-209">Eccezioni in Servizi remoti .NET</span><span class="sxs-lookup"><span data-stu-id="aa628-209">Exceptions in .NET Remoting</span></span>  
 <span data-ttu-id="aa628-210">Le eccezioni generate da un server Servizi remoti .NET vengono serializzate, inviate al client e generate in locale sul client come qualsiasi altra eccezione.</span><span class="sxs-lookup"><span data-stu-id="aa628-210">Exceptions thrown by a Remoting server are serialized, sent to the client, and thrown locally on the client like any other exception.</span></span> <span data-ttu-id="aa628-211">È possibile creare eccezioni personalizzate assegnando una sottoclasse al tipo Exception e contrassegnandolo con [Serializable].</span><span class="sxs-lookup"><span data-stu-id="aa628-211">Custom exceptions can be created by sub-classing the Exception type and marking it with [Serializable].</span></span>   <span data-ttu-id="aa628-212">La maggior parte delle eccezioni del framework sono già contrassegnate in questo modo, pertanto possono essere generate dal server, serializzate e generate nuovamente sul client.</span><span class="sxs-lookup"><span data-stu-id="aa628-212">Most framework exceptions are already marked in this way, allowing most to be thrown by the server, serialized, and re-thrown on the client.</span></span> <span data-ttu-id="aa628-213">Benché questa progettazione sia utile in fase di sviluppo, è possibile che informazioni sul lato server vengano inavvertitamente rivelate al client.</span><span class="sxs-lookup"><span data-stu-id="aa628-213">Though this design is convenient during development, server-side information can inadvertently be disclosed to the client.</span></span> <span data-ttu-id="aa628-214">Questo è uno dei diversi motivi per cui Servizi remoti .NET deve essere usato solo in ambienti completamente attendibili.</span><span class="sxs-lookup"><span data-stu-id="aa628-214">This is one of many reasons Remoting should be used only in fully-trusted environments.</span></span>  
  
#### <a name="exceptions-and-faults-in-wcf"></a><span data-ttu-id="aa628-215">Eccezioni ed errori in WCF</span><span class="sxs-lookup"><span data-stu-id="aa628-215">Exceptions and Faults in WCF</span></span>  
 <span data-ttu-id="aa628-216">WCF non consente la restituzione di tipi di eccezione arbitrari dal server al client, poiché ciò potrebbe causare la divulgazione accidentale di informazioni.</span><span class="sxs-lookup"><span data-stu-id="aa628-216">WCF does not allow arbitrary exception types to be returned from the server to the client because it could lead to inadvertent information disclosure.</span></span> <span data-ttu-id="aa628-217">Se un'operazione del servizio genera un'eccezione imprevista, questo determina la generazione di una FaultException generica sul client.</span><span class="sxs-lookup"><span data-stu-id="aa628-217">If a service operation throws an unexpected exception, it causes a general purpose FaultException to be thrown on the client.</span></span> <span data-ttu-id="aa628-218">Tale eccezione non include informazioni sul motivo del problema o sulla posizione in cui si è verificato e per alcune applicazioni è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="aa628-218">This exception does not carry any information why or where the problem occurred, and for some applications this is sufficient.</span></span> <span data-ttu-id="aa628-219">Le applicazioni che devono comunicare al client informazioni più dettagliate sugli errori possono eseguire questa operazione definendo un contratto di errore.</span><span class="sxs-lookup"><span data-stu-id="aa628-219">Applications that need to communicate richer error information to the client do this by defining a fault contract.</span></span>  
  
 <span data-ttu-id="aa628-220">A tale scopo, creare innanzitutto un tipo [DataContract] per fornire le informazioni sull'errore.</span><span class="sxs-lookup"><span data-stu-id="aa628-220">To do this, first create a [DataContract] type to carry the fault information.</span></span>  
  
```csharp
[DataContract]  
public class CustomerServiceFault  
{  
    [DataMember]  
    public string ErrorMessage { get; set; }  
  
    [DataMember]  
    public int CustomerId {get;set;}  
}  
```  
  
 <span data-ttu-id="aa628-221">Specificare il contratto di errore da usare per ogni operazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="aa628-221">Specify the fault contract to use for each service operation.</span></span>  
  
```csharp
[ServiceContract]  
public interface IWCFServer  
{  
    [OperationContract]  
    [FaultContract(typeof(CustomerServiceFault))]  
    Customer GetCustomer(int customerId);  
}  
```  
  
 <span data-ttu-id="aa628-222">Il server segnala le condizioni di errore generando una FaultException.</span><span class="sxs-lookup"><span data-stu-id="aa628-222">The server reports error conditions by throwing a FaultException.</span></span>  
  
```csharp
throw new FaultException<CustomerServiceFault>(  
    new CustomerServiceFault() {
        CustomerId = customerId,
        ErrorMessage = "Illegal customer Id"
    });  
```  
  
 <span data-ttu-id="aa628-223">Ogni volta che il client effettua una richiesta al server, può intercettare gli errori come normali eccezioni.</span><span class="sxs-lookup"><span data-stu-id="aa628-223">And whenever the client makes a request to the server, it can catch faults as normal exceptions.</span></span>  
  
```csharp
try  
{  
    Customer customer = server.GetCustomer(-1);  
}  
catch (FaultException<CustomerServiceFault> fault)  
{  
    Console.WriteLine($"Fault received: {fault.Detail.ErrorMessage}");
}  
```  
  
 <span data-ttu-id="aa628-224">Per altre informazioni sui contratti di errore, vedere <xref:System.ServiceModel.FaultException>.</span><span class="sxs-lookup"><span data-stu-id="aa628-224">For more information about fault contracts, see <xref:System.ServiceModel.FaultException>.</span></span>  
  
### <a name="security-considerations"></a><span data-ttu-id="aa628-225">Considerazioni relative alla sicurezza</span><span class="sxs-lookup"><span data-stu-id="aa628-225">Security Considerations</span></span>  
  
#### <a name="security-in-net-remoting"></a><span data-ttu-id="aa628-226">Sicurezza in Servizi remoti .NET</span><span class="sxs-lookup"><span data-stu-id="aa628-226">Security in .NET Remoting</span></span>  
 <span data-ttu-id="aa628-227">Alcuni canali di Servizi remoti .NET supportano funzionalità di sicurezza quali l'autenticazione e la crittografia a livello di canale (IPC e TCP).</span><span class="sxs-lookup"><span data-stu-id="aa628-227">Some .NET Remoting channels support security features such as authentication and encryption at the channel layer (IPC and TCP).</span></span> <span data-ttu-id="aa628-228">Il canale HTTP si basa su Internet Information Services (IIS) sia per l'autenticazione che per la crittografia.</span><span class="sxs-lookup"><span data-stu-id="aa628-228">The HTTP channel relies on Internet Information Services (IIS) for both authentication and encryption.</span></span> <span data-ttu-id="aa628-229">Nonostante questo supporto, è necessario considerare Servizi remoti .NET un protocollo di comunicazione non sicuro e usarlo solo all'interno di ambienti completamente attendibili.</span><span class="sxs-lookup"><span data-stu-id="aa628-229">Despite this support, you should consider .NET Remoting an unsecure communication protocol and use it only within fully-trusted environments.</span></span> <span data-ttu-id="aa628-230">Non esporre mai un endpoint Servizi remoti .NET pubblico a Internet o a client non attendibili.</span><span class="sxs-lookup"><span data-stu-id="aa628-230">Never expose a public Remoting endpoint to the Internet or untrusted clients.</span></span>  
  
#### <a name="security-in-wcf"></a><span data-ttu-id="aa628-231">Sicurezza in WCF</span><span class="sxs-lookup"><span data-stu-id="aa628-231">Security in WCF</span></span>  
 <span data-ttu-id="aa628-232">WCF è stato progettato tenendo conto della sicurezza, in parte per risolvere i tipi di vulnerabilità che sono presenti in Servizi remoti .NET.</span><span class="sxs-lookup"><span data-stu-id="aa628-232">WCF was designed with security in mind, in part to address the kinds of vulnerabilities found in .NET Remoting.</span></span> <span data-ttu-id="aa628-233">WCF garantisce la sicurezza sia a livello di trasporto che di messaggi e offre numerose opzioni per l'autenticazione, l'autorizzazione, la crittografia e così via.</span><span class="sxs-lookup"><span data-stu-id="aa628-233">WCF offers security at both the transport and message level, and offers many options for authentication, authorization, encryption, and so on.</span></span> <span data-ttu-id="aa628-234">Per altre informazioni, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa628-234">For more information, see the following topics:</span></span>  
  
- [<span data-ttu-id="aa628-235">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="aa628-235">Security</span></span>](./feature-details/security.md)  
  
- [<span data-ttu-id="aa628-236">Guida alla sicurezza di WCF</span><span class="sxs-lookup"><span data-stu-id="aa628-236">WCF Security Guidance</span></span>](./feature-details/security-guidance-and-best-practices.md)  
  
## <a name="migrating-to-wcf"></a><span data-ttu-id="aa628-237">Migrazione a WCF</span><span class="sxs-lookup"><span data-stu-id="aa628-237">Migrating to WCF</span></span>  
  
### <a name="why-migrate-from-remoting-to-wcf"></a><span data-ttu-id="aa628-238">Perché eseguire la migrazione da Servizi remoti .NET a WCF?</span><span class="sxs-lookup"><span data-stu-id="aa628-238">Why Migrate from Remoting to WCF?</span></span>  
  
- <span data-ttu-id="aa628-239">**Servizi remoti .NET è un prodotto legacy.**</span><span class="sxs-lookup"><span data-stu-id="aa628-239">**.NET Remoting is a legacy product.**</span></span> <span data-ttu-id="aa628-240">Come descritto in [.NET Remoting](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507%28v=vs.100%29), viene considerato un prodotto legacy e non è consigliato per il nuovo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="aa628-240">As described in [.NET Remoting](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507%28v=vs.100%29), it is considered a legacy product and is not recommended for new development.</span></span> <span data-ttu-id="aa628-241">Per le applicazioni nuove ed esistenti sono consigliati WCF o l'API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="aa628-241">WCF or ASP.NET Web API are recommended for new and existing applications.</span></span>  
  
- <span data-ttu-id="aa628-242">**WCF usa standard multipiattaforma.**</span><span class="sxs-lookup"><span data-stu-id="aa628-242">**WCF uses cross-platform standards.**</span></span> <span data-ttu-id="aa628-243">WCF è stato progettato tenendo conto dell'interoperabilità tra le piattaforme e supporta numerosi standard di settore (SOAP, WS-Security, WS-Trust e così via).</span><span class="sxs-lookup"><span data-stu-id="aa628-243">WCF was designed with cross-platform interoperability in mind and supports many industry standards (SOAP, WS-Security, WS-Trust, etc.).</span></span> <span data-ttu-id="aa628-244">Un servizio WCF può interagire con client in esecuzione in sistemi operativi diversi da Windows.</span><span class="sxs-lookup"><span data-stu-id="aa628-244">A WCF service can interoperate with clients running on operating systems other than Windows.</span></span> <span data-ttu-id="aa628-245">La comunicazione remota è stata progettata principalmente per gli ambienti in cui le applicazioni server e client vengono eseguite utilizzando .NET Framework in un sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="aa628-245">Remoting was designed primarily for environments where both the server and client applications run using .NET Framework on a Windows operating system.</span></span>
  
- <span data-ttu-id="aa628-246">**WCF dispone di funzionalità di sicurezza incorporate.**</span><span class="sxs-lookup"><span data-stu-id="aa628-246">**WCF has built-in security.**</span></span> <span data-ttu-id="aa628-247">WCF è stato progettato tenendo conto della sicurezza e offre molte opzioni per l'autenticazione, la sicurezza a livello di trasporto, la sicurezza a livello di messaggio e così via. La comunicazione remota è stata progettata per semplificare l'interoperabilità delle applicazioni, ma non è stata progettata per essere protetta in ambienti non attendibili.</span><span class="sxs-lookup"><span data-stu-id="aa628-247">WCF was designed with security in mind and offers many options for authentication, transport level security, message level security, etc. Remoting was designed to make it easy for applications to interoperate but was not designed to be secure in non-trusted environments.</span></span> <span data-ttu-id="aa628-248">WCF è stato progettato per l'uso sia in ambienti attendibili che non attendibili.</span><span class="sxs-lookup"><span data-stu-id="aa628-248">WCF was designed to work in both trusted and non-trusted environments.</span></span>  
  
### <a name="migration-recommendations"></a><span data-ttu-id="aa628-249">Suggerimenti sulla migrazione</span><span class="sxs-lookup"><span data-stu-id="aa628-249">Migration Recommendations</span></span>  
 <span data-ttu-id="aa628-250">Di seguito sono riportate le procedure consigliate per la migrazione da Servizi remoti .NET a WCF:</span><span class="sxs-lookup"><span data-stu-id="aa628-250">The following are the recommended steps to migrate from .NET Remoting to WCF:</span></span>  
  
- <span data-ttu-id="aa628-251">**Creare il contratto di servizio.**</span><span class="sxs-lookup"><span data-stu-id="aa628-251">**Create the service contract.**</span></span> <span data-ttu-id="aa628-252">Definire i tipi di interfaccia di servizio e contrassegnarli con l'attributo [ServiceContract]. Contrassegnare tutti i metodi che i client saranno autorizzati a chiamare con [OperationContract].</span><span class="sxs-lookup"><span data-stu-id="aa628-252">Define your service interface types, and mark them with the [ServiceContract] attribute.Mark all the methods the clients will be allowed to call with [OperationContract].</span></span>  
  
- <span data-ttu-id="aa628-253">**Creare il contratto dati.**</span><span class="sxs-lookup"><span data-stu-id="aa628-253">**Create the data contract.**</span></span> <span data-ttu-id="aa628-254">Definire i tipi di dati che verranno scambiati tra il server e il client e contrassegnarli con l'attributo [DataContract].</span><span class="sxs-lookup"><span data-stu-id="aa628-254">Define the data types that will be exchanged between server and client, and mark them with the [DataContract] attribute.</span></span> <span data-ttu-id="aa628-255">Contrassegnare tutti i campi e le proprietà che il client sarà autorizzato a usare con [DataMember].</span><span class="sxs-lookup"><span data-stu-id="aa628-255">Mark all the fields and properties the client will be allowed to use with [DataMember].</span></span>  
  
- <span data-ttu-id="aa628-256">**Creare il contratto di errore (facoltativo).**</span><span class="sxs-lookup"><span data-stu-id="aa628-256">**Create the fault contract (optional).**</span></span> <span data-ttu-id="aa628-257">Creare i tipi che verranno scambiati tra il server e il client quando si verificano errori.</span><span class="sxs-lookup"><span data-stu-id="aa628-257">Create the types that will be exchanged between server and client when errors are encountered.</span></span> <span data-ttu-id="aa628-258">Contrassegnare questi tipi con [DataContract] e [DataMember] per renderli serializzabili.</span><span class="sxs-lookup"><span data-stu-id="aa628-258">Mark these types with [DataContract] and [DataMember] to make them serializable.</span></span> <span data-ttu-id="aa628-259">Contrassegnare inoltre con [FaultContract] tutte le operazioni di servizio contrassegnate con [OperationContract] per indicare quali errori possono restituire.</span><span class="sxs-lookup"><span data-stu-id="aa628-259">For all service operations you marked with [OperationContract], also mark them with [FaultContract] to indicate which errors they may return.</span></span>  
  
- <span data-ttu-id="aa628-260">**Configurare e ospitare il servizio.**</span><span class="sxs-lookup"><span data-stu-id="aa628-260">**Configure and host the service.**</span></span> <span data-ttu-id="aa628-261">Dopo aver creato il contratto di servizio, il passaggio successivo consiste nel configurare un'associazione per esporre il servizio in un endpoint.</span><span class="sxs-lookup"><span data-stu-id="aa628-261">Once the service contract has been created, the next step is to configure a binding to expose the service at an endpoint.</span></span> <span data-ttu-id="aa628-262">Per ulteriori informazioni, vedere [endpoint: indirizzi, associazioni e contratti](./feature-details/endpoints-addresses-bindings-and-contracts.md).</span><span class="sxs-lookup"><span data-stu-id="aa628-262">For more information, see [Endpoints: Addresses, Bindings, and Contracts](./feature-details/endpoints-addresses-bindings-and-contracts.md).</span></span>  
  
 <span data-ttu-id="aa628-263">Una volta che è stata eseguita la migrazione a WCF di un'applicazione Servizi remoti .NET, è comunque importante rimuovere le dipendenze da Servizi remoti .NET.</span><span class="sxs-lookup"><span data-stu-id="aa628-263">Once a Remoting application has been migrated to WCF, it is still important to remove dependencies on .NET Remoting.</span></span> <span data-ttu-id="aa628-264">Questo garantisce che eventuali vulnerabilità di Servizi remoti .NET vengano rimosse dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aa628-264">This ensures that any Remoting vulnerabilities are removed from the application.</span></span> <span data-ttu-id="aa628-265">Tali passaggi sono:</span><span class="sxs-lookup"><span data-stu-id="aa628-265">These steps include the following:</span></span>  
  
- <span data-ttu-id="aa628-266">**Interrompere l'uso di MarshalByRefObject.**</span><span class="sxs-lookup"><span data-stu-id="aa628-266">**Discontinue use of MarshalByRefObject.**</span></span> <span data-ttu-id="aa628-267">Il tipo MarshalByRefObject esiste solo per Servizi remoti .NET e non viene usato da WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-267">The MarshalByRefObject type exists only for Remoting and is not used by WCF.</span></span> <span data-ttu-id="aa628-268">Tutti i tipi di applicazioni che usano la sottoclasse MarshalByRefObject devono essere rimossi o modificati.</span><span class="sxs-lookup"><span data-stu-id="aa628-268">Any application types that sub-class MarshalByRefObject should be removed or changed.</span></span>  
  
- <span data-ttu-id="aa628-269">**Interrompere l'uso di [Serializable] e ISerializable.**</span><span class="sxs-lookup"><span data-stu-id="aa628-269">**Discontinue use of [Serializable] and ISerializable.**</span></span> <span data-ttu-id="aa628-270">L'attributo [Serializable] e l'interfaccia ISerializable erano originariamente concepiti per la serializzazione di tipi all'interno di ambienti attendibili e vengono usati da Servizi remoti .NET.</span><span class="sxs-lookup"><span data-stu-id="aa628-270">The [Serializable] attribute and ISerializable interface were originally designed to serialize types within trusted environments, and they are used by Remoting.</span></span> <span data-ttu-id="aa628-271">La serializzazione di WCF si basa sui tipi contrassegnati con [DataContract] e [DataMember].</span><span class="sxs-lookup"><span data-stu-id="aa628-271">WCF serialization relies on types being marked with [DataContract] and [DataMember].</span></span> <span data-ttu-id="aa628-272">I tipi di dati usati da un'applicazione devono essere modificati in modo da usare [DataContract] invece di ISerializable o [Serializable].</span><span class="sxs-lookup"><span data-stu-id="aa628-272">Data types used by an application should be modified to use [DataContract] and not to use ISerializable or [Serializable].</span></span>  
  
### <a name="migration-scenarios"></a><span data-ttu-id="aa628-273">Scenari di migrazione</span><span class="sxs-lookup"><span data-stu-id="aa628-273">Migration Scenarios</span></span>  
 <span data-ttu-id="aa628-274">Verrà ora descritto come realizzare in WCF i seguenti scenari comuni di Servizi remoti .NET:</span><span class="sxs-lookup"><span data-stu-id="aa628-274">Now let’s see how to accomplish the following common Remoting scenarios in WCF:</span></span>  
  
1. <span data-ttu-id="aa628-275">Il server restituisce al client un oggetto in base al valore</span><span class="sxs-lookup"><span data-stu-id="aa628-275">Server returns an object by-value to the client</span></span>  
  
2. <span data-ttu-id="aa628-276">Il server restituisce al client un oggetto in base al riferimento</span><span class="sxs-lookup"><span data-stu-id="aa628-276">Server returns an object by-reference to the client</span></span>  
  
3. <span data-ttu-id="aa628-277">Il client invia al server un oggetto in base al valore</span><span class="sxs-lookup"><span data-stu-id="aa628-277">Client sends an object by-value to the server</span></span>  
  
> [!NOTE]
> <span data-ttu-id="aa628-278">L'invio di un oggetto in base al riferimento dal client al server non è consentito in WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-278">Sending an object by-reference from the client to the server is not allowed in WCF.</span></span>  
  
 <span data-ttu-id="aa628-279">Ai fini dei presenti scenari, si presuppone che le interfacce iniziali per Servizi remoti .NET siano analoghe a quelle illustrate nel seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="aa628-279">When reading through these scenarios, assume our baseline interfaces for .NET Remoting look like the following example.</span></span> <span data-ttu-id="aa628-280">L'implementazione di Servizi remoti .NET non è importante in questo caso, perché si vuole solo illustrare come usare WCF per implementare una funzionalità equivalente.</span><span class="sxs-lookup"><span data-stu-id="aa628-280">The .NET Remoting implementation is not important here because we want to illustrate only how to use WCF to implement equivalent functionality.</span></span>  
  
```csharp
public class RemotingServer : MarshalByRefObject  
{  
    // Demonstrates server returning object by-value  
    public Customer GetCustomer(int customerId) {…}  
  
    // Demonstrates server returning object by-reference  
    public CustomerReference GetCustomerReference(int customerId) {…}  
  
    // Demonstrates client passing object to server by-value  
    public bool UpdateCustomer(Customer customer) {…}  
}  
```  
  
#### <a name="scenario-1-service-returns-an-object-by-value"></a><span data-ttu-id="aa628-281">Scenario 1: il server restituisce un oggetto in base al valore</span><span class="sxs-lookup"><span data-stu-id="aa628-281">Scenario 1: Service Returns an Object by Value</span></span>  
 <span data-ttu-id="aa628-282">In questo scenario viene illustrato un server che restituisce al client un oggetto in base al valore.</span><span class="sxs-lookup"><span data-stu-id="aa628-282">This scenario demonstrates a server returning an object to the client by value.</span></span> <span data-ttu-id="aa628-283">Poiché WCF restituisce sempre gli oggetti dal server in base al valore, la procedura seguente descrive semplicemente come compilare un normale servizio WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-283">WCF always returns objects from the server by value, so the following steps simply describe how to build a normal WCF service.</span></span>  
  
1. <span data-ttu-id="aa628-284">Per iniziare, definire un'interfaccia pubblica per il servizio WCF e contrassegnarla con l'attributo [ServiceContract].</span><span class="sxs-lookup"><span data-stu-id="aa628-284">Start by defining a public interface for the WCF service and mark it with the [ServiceContract] attribute.</span></span> <span data-ttu-id="aa628-285">Viene usato [OperationContract] per identificare i metodi sul lato server che verranno chiamati dal client.</span><span class="sxs-lookup"><span data-stu-id="aa628-285">We use [OperationContract] to identify the server-side methods our client will call.</span></span>  
  
   ```csharp
   [ServiceContract]  
   public interface ICustomerService  
   {  
       [OperationContract]  
       Customer GetCustomer(int customerId);  
  
       [OperationContract]  
       bool UpdateCustomer(Customer customer);  
   }  
   ```  
  
2. <span data-ttu-id="aa628-286">Il passaggio successivo consiste nel creare il contratto dati per questo servizio.</span><span class="sxs-lookup"><span data-stu-id="aa628-286">The next step is to create the data contract for this service.</span></span> <span data-ttu-id="aa628-287">Tale operazione viene eseguita creando classi (non interfacce) contrassegnate con l'attributo [DataContract].</span><span class="sxs-lookup"><span data-stu-id="aa628-287">We do this by creating classes (not interfaces) marked with the [DataContract] attribute.</span></span> <span data-ttu-id="aa628-288">Le singole proprietà o i singoli campi che devono essere visibili sia per il client che per il server sono contrassegnati con [DataMember].</span><span class="sxs-lookup"><span data-stu-id="aa628-288">The individual properties or fields we want visible to both client and server are marked with [DataMember].</span></span> <span data-ttu-id="aa628-289">Se si vuole che i tipi derivati siano consentiti, è necessario usare l'attributo [KnownType] per identificarli.</span><span class="sxs-lookup"><span data-stu-id="aa628-289">If we want derived types to be allowed, we must use the [KnownType] attribute to identify them.</span></span> <span data-ttu-id="aa628-290">Gli unici tipi di cui WCF consentirà la serializzazione o la deserializzazione per questo servizio sono quelli nell'interfaccia del servizio e questi "tipi noti".</span><span class="sxs-lookup"><span data-stu-id="aa628-290">The only types WCF will allow to be serialized or deserialized for this service are those in the service interface and these "known types".</span></span> <span data-ttu-id="aa628-291">Ogni tentativo di scambiare qualsiasi altro tipo non incluso in questo elenco verrà rifiutato.</span><span class="sxs-lookup"><span data-stu-id="aa628-291">Attempting to exchange any other type not in this list will be rejected.</span></span>  
  
   ```csharp
   [DataContract]  
   [KnownType(typeof(PremiumCustomer))]  
   public class Customer  
   {  
       [DataMember]  
       public string FirstName { get; set; }  
  
       [DataMember]  
       public string LastName { get; set; }  
  
       [DataMember]  
       public int CustomerId { get; set; }  
   }  
  
   [DataContract]  
   public class PremiumCustomer : Customer
   {  
       [DataMember]  
       public int AccountId { get; set; }  
   }  
   ```  
  
3. <span data-ttu-id="aa628-292">È quindi necessario fornire l'implementazione per l'interfaccia del servizio.</span><span class="sxs-lookup"><span data-stu-id="aa628-292">Next, we provide the implementation for the service interface.</span></span>  
  
   ```csharp  
   public class CustomerService : ICustomerService  
   {  
       public Customer GetCustomer(int customerId)  
       {  
           // read from database  
       }  
  
       public bool UpdateCustomer(Customer customer)  
       {  
           // write to database  
       }  
   }  
   ```  
  
4. <span data-ttu-id="aa628-293">Per eseguire il servizio WCF, è necessario dichiarare un endpoint che esponga tale interfaccia del servizio in un URL specifico tramite un'associazione WCF specifica.</span><span class="sxs-lookup"><span data-stu-id="aa628-293">To run the WCF service, we need to declare an endpoint that exposes that service interface at a specific URL using a specific WCF binding.</span></span> <span data-ttu-id="aa628-294">Questa operazione viene in genere eseguita aggiungendo le sezioni seguenti al file web.config del progetto server.</span><span class="sxs-lookup"><span data-stu-id="aa628-294">This is typically done by adding the following sections to the server project’s web.config file.</span></span>  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <service name="Server.CustomerService">  
            <endpoint address="http://localhost:8083/CustomerService"  
                      binding="basicHttpBinding"  
                      contract="Shared.ICustomerService" />  
          </service>  
        </services>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
5. <span data-ttu-id="aa628-295">Il servizio WCF può quindi essere avviato con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="aa628-295">The WCF service can then be started with the following code:</span></span>  
  
   ```csharp
   ServiceHost customerServiceHost = new ServiceHost(typeof(CustomerService));  
       customerServiceHost.Open();  
   ```  
  
     <span data-ttu-id="aa628-296">Quando questo ServiceHost viene avviato, usa il file web.config per stabilire il contratto, l'associazione e l'endpoint appropriati.</span><span class="sxs-lookup"><span data-stu-id="aa628-296">When this ServiceHost is started, it uses the web.config file to establish the proper contract, binding and endpoint.</span></span> <span data-ttu-id="aa628-297">Per ulteriori informazioni sui file di configurazione, vedere configurazione [dei servizi tramite file di configurazione](./configuring-services-using-configuration-files.md).</span><span class="sxs-lookup"><span data-stu-id="aa628-297">For more information about configuration files, see [Configuring Services Using Configuration Files](./configuring-services-using-configuration-files.md).</span></span> <span data-ttu-id="aa628-298">Questo tipo di avvio del server è noto come self-hosting.</span><span class="sxs-lookup"><span data-stu-id="aa628-298">This style of starting the server is known as self-hosting.</span></span> <span data-ttu-id="aa628-299">Per ulteriori informazioni sulle altre opzioni per l'hosting dei servizi WCF, vedere [Hosting Services](./hosting-services.md).</span><span class="sxs-lookup"><span data-stu-id="aa628-299">To learn more about other choices for hosting WCF services, see [Hosting Services](./hosting-services.md).</span></span>  
  
6. <span data-ttu-id="aa628-300">Il file app.config del progetto client deve dichiarare le informazioni di associazione corrispondenti per l'endpoint del servizio.</span><span class="sxs-lookup"><span data-stu-id="aa628-300">The client project’s app.config must declare matching binding information for the service’s endpoint.</span></span> <span data-ttu-id="aa628-301">Il modo più semplice per eseguire questa operazione in Visual Studio consiste nell'usare **Aggiungi riferimento al servizio**, che aggiornerà automaticamente il file di app.config.</span><span class="sxs-lookup"><span data-stu-id="aa628-301">The easiest way to do this in Visual Studio is to use **Add Service Reference**, which will automatically update the app.config file.</span></span> <span data-ttu-id="aa628-302">In alternativa, è possibile apportare le stesse modifiche manualmente.</span><span class="sxs-lookup"><span data-stu-id="aa628-302">Alternatively, these same changes can be added manually.</span></span>  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
        <client>  
          <endpoint name="customerservice"  
                    address="http://localhost:8083/CustomerService"  
                    binding="basicHttpBinding"  
                    contract="Shared.ICustomerService"/>  
        </client>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
     <span data-ttu-id="aa628-303">Per ulteriori informazioni sull'utilizzo di **Aggiungi riferimento al servizio**, vedere [procedura: aggiungere, aggiornare o rimuovere un riferimento al servizio](/visualstudio/data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference).</span><span class="sxs-lookup"><span data-stu-id="aa628-303">For more information about using **Add Service Reference**, see [How to: Add, Update, or Remove a Service Reference](/visualstudio/data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference).</span></span>  
  
7. <span data-ttu-id="aa628-304">A questo punto è possibile chiamare il servizio WCF dal client.</span><span class="sxs-lookup"><span data-stu-id="aa628-304">Now we can call the WCF service from the client.</span></span> <span data-ttu-id="aa628-305">È possibile eseguire tale operazione creando una channel factory per il servizio, richiedendole un canale e chiamando direttamente il metodo desiderato su tale canale.</span><span class="sxs-lookup"><span data-stu-id="aa628-305">We do this by creating a channel factory for that service, asking it for a channel, and directly calling the method we want on that channel.</span></span> <span data-ttu-id="aa628-306">Ciò è possibile perché il canale implementa l'interfaccia del servizio e gestisce automaticamente la logica di richiesta/risposta sottostante.</span><span class="sxs-lookup"><span data-stu-id="aa628-306">We can do this because the channel implements the service’s interface and handles the underlying request/reply logic for us.</span></span> <span data-ttu-id="aa628-307">Il valore restituito dalla chiamata del metodo è la copia deserializzata della risposta del server.</span><span class="sxs-lookup"><span data-stu-id="aa628-307">The return value from that method call is the deserialized copy of the server’s response.</span></span>  
  
   ```csharp
   ChannelFactory<ICustomerService> factory =  
       new ChannelFactory<ICustomerService>("customerservice");  
   ICustomerService service = factory.CreateChannel();  
   Customer customer = service.GetCustomer(42);  
   Console.WriteLine($"  Customer {customer.FirstName} {customer.LastName} received.");
   ```  
  
 <span data-ttu-id="aa628-308">Gli oggetti restituiti da WCF dal server al client sono sempre in base al valore.</span><span class="sxs-lookup"><span data-stu-id="aa628-308">Objects returned by WCF from the server to the client are always by value.</span></span> <span data-ttu-id="aa628-309">Gli oggetti sono copie deserializzate dei dati inviati dal server.</span><span class="sxs-lookup"><span data-stu-id="aa628-309">The objects are deserialized copies of the data sent by the server.</span></span> <span data-ttu-id="aa628-310">Il client può chiamare metodi su queste copie locali senza rischiare di richiamare codice server tramite callback.</span><span class="sxs-lookup"><span data-stu-id="aa628-310">The client can call methods on these local copies without any danger of invoking server code through callbacks.</span></span>  
  
#### <a name="scenario-2-server-returns-an-object-by-reference"></a><span data-ttu-id="aa628-311">Scenario 2: il server restituisce un oggetto in base al riferimento</span><span class="sxs-lookup"><span data-stu-id="aa628-311">Scenario 2: Server Returns an Object By Reference</span></span>  
 <span data-ttu-id="aa628-312">In questo scenario viene illustrato un server che fornisce al client un oggetto in base al riferimento.</span><span class="sxs-lookup"><span data-stu-id="aa628-312">This scenario demonstrates the server providing an object to the client by reference.</span></span> <span data-ttu-id="aa628-313">In Servizi remoti .NET questa operazione viene gestita automaticamente per qualsiasi tipo derivato da MarshalByRefObject, che è serializzato in base al riferimento.</span><span class="sxs-lookup"><span data-stu-id="aa628-313">In .NET Remoting, this is handled automatically for any type derived from MarshalByRefObject, which is serialized by-reference.</span></span> <span data-ttu-id="aa628-314">Un esempio di questo scenario consiste nel consentire a più client di disporre di oggetti con sessione indipendenti sul lato server.</span><span class="sxs-lookup"><span data-stu-id="aa628-314">An example of this scenario is allowing multiple clients to have independent sessionful server-side objects.</span></span> <span data-ttu-id="aa628-315">Come accennato in precedenza, gli oggetti restituiti da un servizio WCF sono sempre in base al valore, pertanto non esiste un equivalente diretto di un oggetto in base al riferimento. Tuttavia, è possibile ottenere un risultato analogo a una semantica in base al riferimento usando un oggetto <xref:System.ServiceModel.EndpointAddress10>.</span><span class="sxs-lookup"><span data-stu-id="aa628-315">As previously mentioned, objects returned by a WCF service are always by value, so there is no direct equivalent of a by-reference object, but it is possible to achieve something similar to by-reference semantics using an <xref:System.ServiceModel.EndpointAddress10> object.</span></span> <span data-ttu-id="aa628-316">Questo è un oggetto serializzabile in base al valore che può essere usato dal client per ottenere un oggetto in base al riferimento con sessione sul server.</span><span class="sxs-lookup"><span data-stu-id="aa628-316">This is a serializable by-value object that can be used by the client to obtain a sessionful by-reference object on the server.</span></span> <span data-ttu-id="aa628-317">Ciò rende possibile lo scenario relativo a più client con oggetti con sessione indipendenti sul lato server.</span><span class="sxs-lookup"><span data-stu-id="aa628-317">This enables the scenario of having multiple clients with independent sessionful server-side objects.</span></span>  
  
1. <span data-ttu-id="aa628-318">Innanzitutto, è necessario definire un contratto di servizio WCF che corrisponde all'oggetto con sessione stesso.</span><span class="sxs-lookup"><span data-stu-id="aa628-318">First, we need to define a WCF service contract that corresponds to the sessionful object itself.</span></span>  
  
   ```csharp
   [ServiceContract(SessionMode = SessionMode.Allowed)]  
       public interface ISessionBoundObject  
       {  
           [OperationContract]  
           string GetCurrentValue();  
  
           [OperationContract]  
           void SetCurrentValue(string value);  
       }  
   ```  
  
    > [!TIP]
    > <span data-ttu-id="aa628-319">Si noti che l'oggetto con sessione è contrassegnato con [ServiceContract], che lo rende una normale interfaccia del servizio WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-319">Notice that the sessionful object is marked with [ServiceContract], making it a normal WCF service interface.</span></span> <span data-ttu-id="aa628-320">L'impostazione della proprietà SessionMode indica che sarà un servizio con sessione.</span><span class="sxs-lookup"><span data-stu-id="aa628-320">Setting the SessionMode property indicates it will be a sessionful service.</span></span> <span data-ttu-id="aa628-321">In WCF una sessione è un modo per correlare più messaggi inviati tra due endpoint.</span><span class="sxs-lookup"><span data-stu-id="aa628-321">In WCF, a session is a way of correlating multiple messages sent between two endpoints.</span></span> <span data-ttu-id="aa628-322">Ciò significa che, una volta che un client ottiene una connessione al servizio, verrà stabilita una sessione tra il client e il server.</span><span class="sxs-lookup"><span data-stu-id="aa628-322">This means that once a client obtains a connection to this service, a session will be established between the client and the server.</span></span> <span data-ttu-id="aa628-323">Il client userà una singola istanza univoca dell'oggetto sul lato server per tutte le proprie interazioni all'interno di questa singola sessione.</span><span class="sxs-lookup"><span data-stu-id="aa628-323">The client will use a single unique instance of the server-side object for all its interactions within this single session.</span></span>  
  
2. <span data-ttu-id="aa628-324">È quindi necessario fornire l'implementazione di questa interfaccia del servizio.</span><span class="sxs-lookup"><span data-stu-id="aa628-324">Next, we need to provide the implementation of this service interface.</span></span> <span data-ttu-id="aa628-325">Denotandola con [ServiceBehavior] e impostando InstanceContextMode, è possibile indicare a WCF che si vuole usare un'istanza univoca di questo tipo per ciascuna sessione.</span><span class="sxs-lookup"><span data-stu-id="aa628-325">By denoting it with [ServiceBehavior] and setting the InstanceContextMode, we tell WCF we want to use a unique instance of this type for an each session.</span></span>  
  
   ```csharp
   [ServiceBehavior(InstanceContextMode = InstanceContextMode.PerSession)]  
       public class MySessionBoundObject : ISessionBoundObject  
       {  
           private string _value;  
  
           public string GetCurrentValue()  
           {  
               return _value;  
           }  
  
           public void SetCurrentValue(string val)  
           {  
               _value = val;  
           }  
  
       }  
   ```  
  
3. <span data-ttu-id="aa628-326">A questo punto è necessario un modo per ottenere un'istanza di questo oggetto con sessione.</span><span class="sxs-lookup"><span data-stu-id="aa628-326">Now we need a way to obtain an instance of this sessionful object.</span></span> <span data-ttu-id="aa628-327">A tale scopo, è possibile creare un'altra interfaccia di servizio WCF che restituisce un oggetto EndpointAddress10.</span><span class="sxs-lookup"><span data-stu-id="aa628-327">We do this by creating another WCF service interface that returns an EndpointAddress10 object.</span></span> <span data-ttu-id="aa628-328">Si tratta di una forma serializzabile di un endpoint che il client può usare per creare l'oggetto con sessione.</span><span class="sxs-lookup"><span data-stu-id="aa628-328">This is a serializable form of an endpoint that the client can use to create the sessionful object.</span></span>  
  
   ```csharp
   [ServiceContract]  
       public interface ISessionBoundFactory  
       {  
           [OperationContract]  
           EndpointAddress10 GetInstanceAddress();  
       }  
   ```  
  
     <span data-ttu-id="aa628-329">È quindi possibile implementare il servizio WCF:</span><span class="sxs-lookup"><span data-stu-id="aa628-329">And we implement this WCF service:</span></span>  
  
   ```csharp
   public class SessionBoundFactory : ISessionBoundFactory  
       {  
           public static ChannelFactory<ISessionBoundObject> _factory =
               new ChannelFactory<ISessionBoundObject>("sessionbound");  

           public SessionBoundFactory()  
           {  
           }  
  
           public EndpointAddress10 GetInstanceAddress()  
           {  
               IClientChannel channel = (IClientChannel)_factory.CreateChannel();  
               return EndpointAddress10.FromEndpointAddress(channel.RemoteAddress);  
           }  
       }  
   ```  
  
     <span data-ttu-id="aa628-330">Questa implementazione mantiene una channel factory singleton per creare oggetti con sessione.</span><span class="sxs-lookup"><span data-stu-id="aa628-330">This implementation maintains a singleton channel factory to create sessionful objects.</span></span> <span data-ttu-id="aa628-331">Quando viene chiamato GetInstanceAddress(), questo crea un canale e un oggetto EndpointAddress10 che fa riferimento in modo efficace all'indirizzo remoto associato a questo canale.</span><span class="sxs-lookup"><span data-stu-id="aa628-331">When GetInstanceAddress() is called, it creates a channel and creates an EndpointAddress10 object that effectively points to the remote address associated with this channel.</span></span> <span data-ttu-id="aa628-332">EndpointAddress10 è semplicemente un tipo di dati che può essere restituito al client in base al valore.</span><span class="sxs-lookup"><span data-stu-id="aa628-332">EndpointAddress10 is simply a data type that can be returned to the client by-value.</span></span>  
  
4. <span data-ttu-id="aa628-333">È necessario modificare il file di configurazione del server eseguendo le due operazioni seguenti, come illustrato nell'esempio riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="aa628-333">We need to modify the server’s configuration file by doing the following two things as shown in the example below:</span></span>  
  
    1. <span data-ttu-id="aa628-334">Dichiarare una \<client> sezione che descrive l'endpoint per l'oggetto con sessione.</span><span class="sxs-lookup"><span data-stu-id="aa628-334">Declare a \<client> section that describes the endpoint for the sessionful object.</span></span> <span data-ttu-id="aa628-335">Questa operazione è necessaria perché il server opera anche come client in questa situazione.</span><span class="sxs-lookup"><span data-stu-id="aa628-335">This is necessary because the server also acts as a client in this situation.</span></span>  
  
    2. <span data-ttu-id="aa628-336">Dichiarare gli endpoint per la factory e l'oggetto con sessione.</span><span class="sxs-lookup"><span data-stu-id="aa628-336">Declare endpoints for the factory and sessionful object.</span></span> <span data-ttu-id="aa628-337">Ciò è necessario per consentire al client di comunicare con gli endpoint del servizio per acquisire l'EndpointAddress10 e per creare il canale con sessione.</span><span class="sxs-lookup"><span data-stu-id="aa628-337">This is necessary to allow the client to communicate with the service endpoints to acquire the EndpointAddress10 and to create the sessionful channel.</span></span>  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
         <client>  
          <endpoint name="sessionbound"  
                    address="net.tcp://localhost:8081/SessionBoundObject"  
                    binding="netTcpBinding"  
                    contract="Shared.ISessionBoundObject"/>  
        </client>  
        <services>  
          <service name="Server.CustomerService">  
            <endpoint address="http://localhost:8083/CustomerService"  
                      binding="basicHttpBinding"  
                      contract="Shared.ICustomerService" />  
          </service>  
          <service name="Server.MySessionBoundObject">  
            <endpoint address="net.tcp://localhost:8081/SessionBoundObject"  
                      binding="netTcpBinding"  
                      contract="Shared.ISessionBoundObject" />  
          </service>  
          <service name="Server.SessionBoundFactory">  
            <endpoint address="net.tcp://localhost:8081/SessionBoundFactory"  
                      binding="netTcpBinding"  
                      contract="Shared.ISessionBoundFactory" />  
          </service>  
        </services>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
     <span data-ttu-id="aa628-338">È quindi possibile avviare questi servizi:</span><span class="sxs-lookup"><span data-stu-id="aa628-338">And then we can start these services:</span></span>  
  
   ```csharp
   ServiceHost factoryHost = new ServiceHost(typeof(SessionBoundFactory));  
   factoryHost.Open();  
  
   ServiceHost sessionHost = new ServiceHost(typeof(MySessionBoundObject));  
   sessionHost.Open();  
   ```  
  
5. <span data-ttu-id="aa628-339">Il client può essere configurato dichiarando questi stessi endpoint nel file app.config del progetto.</span><span class="sxs-lookup"><span data-stu-id="aa628-339">We configure the client by declaring these same endpoints in its project’s app.config file.</span></span>  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
        <client>  
          <endpoint name="customerservice"  
                    address="http://localhost:8083/CustomerService"  
                    binding="basicHttpBinding"  
                    contract="Shared.ICustomerService"/>  
          <endpoint name="sessionbound"  
                    address="net.tcp://localhost:8081/SessionBoundObject"  
                    binding="netTcpBinding"  
                    contract="Shared.ISessionBoundObject"/>  
          <endpoint name="factory"  
                    address="net.tcp://localhost:8081/SessionBoundFactory"  
                    binding="netTcpBinding"  
                    contract="Shared.ISessionBoundFactory"/>  
        </client>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
6. <span data-ttu-id="aa628-340">Per creare e usare questo oggetto con sessione, il client deve eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="aa628-340">In order to create and use this sessionful object, the client must do the following steps:</span></span>  
  
    1. <span data-ttu-id="aa628-341">Creare un canale per il servizio ISessionBoundFactory.</span><span class="sxs-lookup"><span data-stu-id="aa628-341">Create a channel to the ISessionBoundFactory service.</span></span>  
  
    2. <span data-ttu-id="aa628-342">Usare tale canale per richiamare il servizio in modo da ottenere un EndpointAddress10.</span><span class="sxs-lookup"><span data-stu-id="aa628-342">Use that channel to invoke that service to obtain an EndpointAddress10.</span></span>  
  
    3. <span data-ttu-id="aa628-343">Usare l'EndpointAddress10 per creare un canale in modo da ottenere un oggetto con sessione.</span><span class="sxs-lookup"><span data-stu-id="aa628-343">Use the EndpointAddress10 to create a channel to obtain a sessionful object.</span></span>  
  
    4. <span data-ttu-id="aa628-344">Interagire con l'oggetto con sessione per verificare che rimanga la stessa istanza fra diverse chiamate.</span><span class="sxs-lookup"><span data-stu-id="aa628-344">Interact with the sessionful object to demonstrate it remains the same instance across multiple calls.</span></span>  
  
   ```csharp
   ChannelFactory<ISessionBoundFactory> channelFactory =
       new ChannelFactory<ISessionBoundFactory>("factory");  
   ISessionBoundFactory sessionFactory = channelFactory.CreateChannel();  
  
   EndpointAddress10 address1 = sessionFactory.GetInstanceAddress();  
   EndpointAddress10 address2 = sessionFactory.GetInstanceAddress();  
  
   ChannelFactory<ISessionBoundObject> sessionObjectFactory1 =
       new ChannelFactory<ISessionBoundObject>(new NetTcpBinding(),
                                               address1.ToEndpointAddress());  
   ChannelFactory<ISessionBoundObject> sessionObjectFactory2 =
       new ChannelFactory<ISessionBoundObject>(new NetTcpBinding(),
                                               address2.ToEndpointAddress());  
  
   ISessionBoundObject sessionInstance1 = sessionObjectFactory1.CreateChannel();  
   ISessionBoundObject sessionInstance2 = sessionObjectFactory2.CreateChannel();  
  
   sessionInstance1.SetCurrentValue("Hello");  
   sessionInstance2.SetCurrentValue("World");  
  
   if (sessionInstance1.GetCurrentValue() == "Hello" &&  
       sessionInstance2.GetCurrentValue() == "World")  
   {  
       Console.WriteLine("sessionful server object works as expected");  
   }  
   ```  
  
 <span data-ttu-id="aa628-345">WCF restituisce sempre oggetti in base al valore, ma è possibile supportare l'equivalente di una semantica in base al riferimento mediante l'uso di EndpointAddress10.</span><span class="sxs-lookup"><span data-stu-id="aa628-345">WCF always returns objects by value, but it is possible to support the equivalent of by-reference semantics through the use of EndpointAddress10.</span></span> <span data-ttu-id="aa628-346">Ciò consente al client di richiedere un'istanza del servizio WCF con sessione, dopodiché può interagire con tale istanza come qualsiasi altro servizio WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-346">This permits the client to request a sessionful WCF service instance, after which it can interact with it like any other WCF service.</span></span>  
  
#### <a name="scenario-3-client-sends-server-a-by-value-instance"></a><span data-ttu-id="aa628-347">Scenario 3: il client invia al server un'istanza in base al valore</span><span class="sxs-lookup"><span data-stu-id="aa628-347">Scenario 3: Client Sends Server a By-Value Instance</span></span>  
 <span data-ttu-id="aa628-348">In questo scenario viene illustrato un client che invia al server un'istanza di oggetto non primitiva in base al valore.</span><span class="sxs-lookup"><span data-stu-id="aa628-348">This scenario demonstrates the client sending a non-primitive object instance to the server by value.</span></span> <span data-ttu-id="aa628-349">Poiché WCF invia solo oggetti in base al valore, in questo scenario viene illustrato il normale uso di WCF.</span><span class="sxs-lookup"><span data-stu-id="aa628-349">Because WCF only sends objects by value, this scenario demonstrates normal WCF usage.</span></span>  
  
1. <span data-ttu-id="aa628-350">Usare lo stesso servizio WCF dello scenario 1.</span><span class="sxs-lookup"><span data-stu-id="aa628-350">Use the same WCF Service from Scenario 1.</span></span>  
  
2. <span data-ttu-id="aa628-351">Usare il client per creare un nuovo oggetto in base al valore (Customer), creare un canale per comunicare con il servizio ICustomerService e inviare l'oggetto a tale canale.</span><span class="sxs-lookup"><span data-stu-id="aa628-351">Use the client to create a new by-value object (Customer), create a channel to communicate with the ICustomerService service, and send the object to it.</span></span>  
  
   ```csharp
   ChannelFactory<ICustomerService> factory =  
       new ChannelFactory<ICustomerService>("customerservice");  
   ICustomerService service = factory.CreateChannel();  
   PremiumCustomer customer = new PremiumCustomer {
   FirstName = "Bob",
   LastName = "Jones",
   CustomerId = 43,
   AccountId = 99};  
   bool success = service.UpdateCustomer(customer);  
   Console.WriteLine($"  Server returned {success}.");
   ```  
  
     <span data-ttu-id="aa628-352">L'oggetto Customer verrà serializzato e inviato al server, dove sarà deserializzato in una nuova copia di tale oggetto.</span><span class="sxs-lookup"><span data-stu-id="aa628-352">The customer object will be serialized, and sent to the server, where it is deserialized into a new copy of that object.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="aa628-353">Questo codice illustra inoltre l'invio di un tipo derivato (PremiumCustomer).</span><span class="sxs-lookup"><span data-stu-id="aa628-353">This code also illustrates sending a derived type (PremiumCustomer).</span></span> <span data-ttu-id="aa628-354">L'interfaccia del servizio prevede un oggetto Customer, ma l'attributo [KnownType] nella classe Customer indicava che anche PremiumCustomer era consentito.</span><span class="sxs-lookup"><span data-stu-id="aa628-354">The service interface expects a Customer object, but the [KnownType] attribute on the Customer class indicated PremiumCustomer was also allowed.</span></span> <span data-ttu-id="aa628-355">In WCF qualunque tentativo di serializzare o deserializzare qualsiasi altro tipo tramite questa interfaccia di servizio non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="aa628-355">WCF will fail any attempt to serialize or deserialize any other type through this service interface.</span></span>  
  
 <span data-ttu-id="aa628-356">I normali scambi di dati in WCF sono in base al valore.</span><span class="sxs-lookup"><span data-stu-id="aa628-356">Normal WCF exchanges of data are by value.</span></span> <span data-ttu-id="aa628-357">Ciò garantisce che la chiamata di metodi su uno di questi oggetti di dati venga eseguita solo in locale: non verrà richiamato codice su un altro livello.</span><span class="sxs-lookup"><span data-stu-id="aa628-357">This guarantees that invoking methods on one of these data objects executes only locally – it will not invoke code on the other tier.</span></span> <span data-ttu-id="aa628-358">Sebbene sia possibile ottenere qualcosa come gli oggetti per riferimento restituiti *dal* server, non è possibile che un client passi un oggetto per riferimento *al* server.</span><span class="sxs-lookup"><span data-stu-id="aa628-358">While it is possible to achieve something like by-reference objects returned *from* the server, it is not possible for a client to pass a by-reference object *to* the server.</span></span> <span data-ttu-id="aa628-359">Uno scenario che richiede una conversazione tra il client e il server può essere realizzato in WCF usando un servizio duplex.</span><span class="sxs-lookup"><span data-stu-id="aa628-359">A scenario that requires a conversation back and forth between client and server can be achieved in WCF using a duplex service.</span></span> <span data-ttu-id="aa628-360">Per ulteriori informazioni, vedere [servizi duplex](./feature-details/duplex-services.md).</span><span class="sxs-lookup"><span data-stu-id="aa628-360">For more information, see [Duplex Services](./feature-details/duplex-services.md).</span></span>  
  
## <a name="summary"></a><span data-ttu-id="aa628-361">Summary</span><span class="sxs-lookup"><span data-stu-id="aa628-361">Summary</span></span>  
 <span data-ttu-id="aa628-362">Servizi remoti .NET è un framework di comunicazione destinato all'uso solo all'interno di ambienti completamente attendibili.</span><span class="sxs-lookup"><span data-stu-id="aa628-362">.NET Remoting is a communication framework intended to be used only within fully-trusted environments.</span></span> <span data-ttu-id="aa628-363">Si tratta di un prodotto legacy e supportato solo per la compatibilità con le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="aa628-363">It is a legacy product and supported only for backward compatibility.</span></span> <span data-ttu-id="aa628-364">Non deve essere usato per creare nuove applicazioni.</span><span class="sxs-lookup"><span data-stu-id="aa628-364">It should not be used to build new applications.</span></span> <span data-ttu-id="aa628-365">Al contrario, WCF è stato progettato prestando particolare attenzione alla sicurezza ed è consigliato per le applicazioni nuove ed esistenti.</span><span class="sxs-lookup"><span data-stu-id="aa628-365">Conversely, WCF was designed with security in mind and is recommended for new and existing applications.</span></span> <span data-ttu-id="aa628-366">Microsoft consiglia di eseguire la migrazione delle applicazioni Servizi remoti .NET esistenti per l'uso di WCF o dell'API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="aa628-366">Microsoft recommends that existing Remoting applications be migrated to use WCF or ASP.NET Web API instead.</span></span>

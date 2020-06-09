---
title: 'Procedura: scegliere tra richieste HTTP POST e HTTP GET per gli endpoint ASP.NET AJAX'
ms.date: 03/30/2017
ms.assetid: b47de82a-4c92-4af6-bceb-a5cb8bb8ede9
ms.openlocfilehash: 15d7ad43ce9120e97aba9119aff6a6c1a19f301f
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596916"
---
# <a name="how-to-choose-between-http-post-and-http-get-requests-for-aspnet-ajax-endpoints"></a><span data-ttu-id="ecb87-102">Procedura: scegliere tra richieste HTTP POST e HTTP GET per gli endpoint ASP.NET AJAX</span><span class="sxs-lookup"><span data-stu-id="ecb87-102">How to: Choose between HTTP POST and HTTP GET requests for ASP.NET AJAX Endpoints</span></span>

<span data-ttu-id="ecb87-103">Windows Communication Foundation (WCF) consente di creare un servizio che espone un endpoint abilitato per AJAX ASP.NET che può essere chiamato da JavaScript su un sito Web client.</span><span class="sxs-lookup"><span data-stu-id="ecb87-103">Windows Communication Foundation (WCF) allows you to create a service that exposes an ASP.NET AJAX-enabled endpoint that can be called from JavaScript on a client Web site.</span></span> <span data-ttu-id="ecb87-104">Le procedure di base per la compilazione di tali servizi sono illustrate in [procedura: usare la configurazione per aggiungere un endpoint ASP.NET AJAX](how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md) e [procedura: aggiungere un endpoint ASP.NET AJAX senza usare la configurazione](how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="ecb87-104">The basic procedures for building such services is discussed in [How to: Use Configuration to Add an ASP.NET AJAX Endpoint](how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md) and [How to: Add an ASP.NET AJAX Endpoint Without Using Configuration](how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md).</span></span>  
  
 <span data-ttu-id="ecb87-105">ASP.NET AJAX supporta operazioni che usano verbi HTTP POST e HTTP GET, con HTTP POST come impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ecb87-105">ASP.NET AJAX supports operations that use the HTTP POST and HTTP GET verbs, with HTTP POST being the default.</span></span> <span data-ttu-id="ecb87-106">Quando si crea un'operazione che non ha effetti collaterali e restituisce dati che non vengono mai modificati o vengono modificati solo di rado, usare HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="ecb87-106">When creating an operation that has no side effects and returns data that rarely or never changes, use HTTP GET instead.</span></span> <span data-ttu-id="ecb87-107">I risultati delle operazioni GET possono essere memorizzati nella cache, il che significa che più chiamate alla stessa operazione possono produrre una sola richiesta al servizio.</span><span class="sxs-lookup"><span data-stu-id="ecb87-107">Results of GET operations can be cached, which means that multiple calls to the same operation may result in only one request to your service.</span></span> <span data-ttu-id="ecb87-108">La memorizzazione nella cache non viene eseguita da WCF, ma può essere eseguita a qualsiasi livello (nel browser di un utente, in un server proxy e in altri livelli). La memorizzazione nella cache è vantaggiosa se si desidera aumentare le prestazioni del servizio, ma potrebbe non essere accettabile se i dati vengono modificati di frequente o se l'operazione esegue un'azione.</span><span class="sxs-lookup"><span data-stu-id="ecb87-108">The caching is not done by WCF but can take place at any level (in a user's browser, on a proxy server, and other levels.) Caching is advantageous if you want to increase service performance, but may not be acceptable if data changes frequently or if the operation performs some action.</span></span>  
  
 <span data-ttu-id="ecb87-109">Ad esempio, se si sta progettando un servizio per gestire il catalogo musicale di un utente, un'operazione che ricerca l'artista in base al titolo di un album trae vantaggio dall'utilizzo di GET, ma un'operazione che aggiunge un album alla raccolta personale dell'utente deve usare POST.</span><span class="sxs-lookup"><span data-stu-id="ecb87-109">For example, if you are designing service to manage a user's music library, an operation that looks up the artist based on an album's title benefits from using GET, but an operation that adds an album to the user's personal collection must use POST.</span></span>  
  
 <span data-ttu-id="ecb87-110">Per controllare la durata della cache, usare il tipo <xref:System.ServiceModel.Web.OutgoingWebResponseContext>.</span><span class="sxs-lookup"><span data-stu-id="ecb87-110">To control the lifetime of the cache, use the <xref:System.ServiceModel.Web.OutgoingWebResponseContext> type.</span></span> <span data-ttu-id="ecb87-111">Ad esempio, quando si progetta un servizio che restituisce previsioni meteorologiche aggiornate ogni ora, si utilizzerà GET limitando però la durata della cache a massimo un'ora, per impedire agli utenti del servizio di accedere a dati non aggiornati.</span><span class="sxs-lookup"><span data-stu-id="ecb87-111">For example, when designing a service that returns weather forecasts updated hourly, you would use GET but limit the cache duration to an hour or less to prevent the users of the service from accessing stale data.</span></span>  
  
 <span data-ttu-id="ecb87-112">Quando si usano servizi da una pagina ASP.NET AJAX che usano il controllo Script Manager, non c'è alcuna differenza se l'operazione usa GET o POST, il meccanismo di gestione degli script assicura che venga emesso il tipo di richiesta corretto.</span><span class="sxs-lookup"><span data-stu-id="ecb87-112">When using services from an ASP.NET AJAX page that use the Script Manager control, it makes no difference whether the operation uses GET or POST - the script manager mechanism ensures that the correct request type is issued.</span></span>  
  
 <span data-ttu-id="ecb87-113">Le operazioni HTTP GET usano qualsiasi parametro di input supportato dalle operazioni POST, inclusi i tipi di contratto dati complessi.</span><span class="sxs-lookup"><span data-stu-id="ecb87-113">HTTP GET operations use any input parameters supported by POST operations, including complex data contract types.</span></span> <span data-ttu-id="ecb87-114">Tuttavia, nella maggior parte dei casi è consigliabile evitare di usare troppi parametri o parametri troppo complessi nelle operazioni GET, per non ridurre l'efficienza della memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="ecb87-114">However, in most cases it is recommended to avoid too many parameters or parameters that are too complex in GET operations because it reduces caching efficiency.</span></span>  
  
 <span data-ttu-id="ecb87-115">In questo argomento viene illustrato come scegliere tra GET e POST aggiungendo gli attributi <xref:System.ServiceModel.Web.WebGetAttribute> o <xref:System.ServiceModel.Web.WebInvokeAttribute> alle operazioni pertinenti nel contratto di servizio.</span><span class="sxs-lookup"><span data-stu-id="ecb87-115">This topic demonstrates how to select between GET and POST by adding the <xref:System.ServiceModel.Web.WebGetAttribute> or <xref:System.ServiceModel.Web.WebInvokeAttribute> attributes to the relevant operations in the service contract.</span></span> <span data-ttu-id="ecb87-116">Gli altri passaggi (per implementare, configurare e ospitare il servizio) necessari per eseguire il servizio sono simili a quelli usati da qualsiasi servizio ASP.NET AJAX in WCF.</span><span class="sxs-lookup"><span data-stu-id="ecb87-116">The other steps (to implement, configure and host the service) that are required to get the service running are similar to those used by any ASP.NET AJAX service in WCF.</span></span>  
  
 <span data-ttu-id="ecb87-117">Un'operazione contrassegnata da <xref:System.ServiceModel.Web.WebGetAttribute> usa sempre una richiesta GET.</span><span class="sxs-lookup"><span data-stu-id="ecb87-117">An operation marked with the <xref:System.ServiceModel.Web.WebGetAttribute> always uses a GET request.</span></span> <span data-ttu-id="ecb87-118">Un'operazione contrassegnata da <xref:System.ServiceModel.Web.WebInvokeAttribute> o non contrassegnata da nessuno dei due attributi, usa una richiesta POST.</span><span class="sxs-lookup"><span data-stu-id="ecb87-118">An operation marked with the <xref:System.ServiceModel.Web.WebInvokeAttribute>, or not marked with any of the two attributes, uses a POST request.</span></span> <span data-ttu-id="ecb87-119"><xref:System.ServiceModel.Web.WebInvokeAttribute> consente di usare altri verbi HTTP, diversi da GET e POST, quali PUT e DELETE, tramite la proprietà <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A>.</span><span class="sxs-lookup"><span data-stu-id="ecb87-119">The <xref:System.ServiceModel.Web.WebInvokeAttribute> allows the use of other HTTP verbs, other than GET and POST (such as PUT and DELETE) through the <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A> property.</span></span> <span data-ttu-id="ecb87-120">Tuttavia, questi verbi non sono supportati da ASP.NET AJAX.</span><span class="sxs-lookup"><span data-stu-id="ecb87-120">However, these verbs are not supported by ASP.NET AJAX.</span></span> <span data-ttu-id="ecb87-121">Se si intende usare il servizio da pagine ASP.NET che usano il controllo Script Manager, non usare la proprietà <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A>.</span><span class="sxs-lookup"><span data-stu-id="ecb87-121">If you intend to use the service from ASP.NET pages using the Script Manager control, do not use the <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A> property.</span></span>  
  
 <span data-ttu-id="ecb87-122">Per un esempio funzionante di cambio da ottenere, vedere l'esempio di [servizio AJAX di base](../samples/basic-ajax-service.md) .</span><span class="sxs-lookup"><span data-stu-id="ecb87-122">For a working example of switching to GET, see the [Basic AJAX Service](../samples/basic-ajax-service.md) sample.</span></span>  
  
 <span data-ttu-id="ecb87-123">Per un esempio che usa POST, vedere l'esempio di [servizio AJAX con http post](../samples/ajax-service-using-http-post.md) .</span><span class="sxs-lookup"><span data-stu-id="ecb87-123">For a sample that uses POST, see the [AJAX Service Using HTTP POST](../samples/ajax-service-using-http-post.md) sample.</span></span>  
  
## <a name="to-create-a-wcf-service-that-responds-to-http-get-or-http-post-requests"></a><span data-ttu-id="ecb87-124">Per creare un servizio WCF che risponde a richieste HTTP GET o HTTP POST</span><span class="sxs-lookup"><span data-stu-id="ecb87-124">To create a WCF service that responds to HTTP GET or HTTP POST requests</span></span>
  
1. <span data-ttu-id="ecb87-125">Definire un contratto di servizio WCF di base con un'interfaccia contrassegnata con l' <xref:System.ServiceModel.ServiceContractAttribute> attributo.</span><span class="sxs-lookup"><span data-stu-id="ecb87-125">Define a basic WCF service contract with an interface marked with the <xref:System.ServiceModel.ServiceContractAttribute> attribute.</span></span> <span data-ttu-id="ecb87-126">Contrassegnare ogni operazione con <xref:System.ServiceModel.OperationContractAttribute>.</span><span class="sxs-lookup"><span data-stu-id="ecb87-126">Mark each operation with the <xref:System.ServiceModel.OperationContractAttribute>.</span></span> <span data-ttu-id="ecb87-127">Aggiungere l'attributo <xref:System.ServiceModel.Web.WebGetAttribute> per stabilire che un'operazione deve rispondere a richieste HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="ecb87-127">Add the <xref:System.ServiceModel.Web.WebGetAttribute> attribute to stipulate that an operation should respond to HTTP GET requests.</span></span> <span data-ttu-id="ecb87-128">È inoltre possibile aggiungere l'attributo <xref:System.ServiceModel.Web.WebInvokeAttribute> per specificare esplicitamente HTTP POST o non specificare alcun attributo e scegliere quindi HTTP POST per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ecb87-128">You can also add the <xref:System.ServiceModel.Web.WebInvokeAttribute> attribute to explicitly specify HTTP POST, or not specify an attribute, which defaults to HTTP POST.</span></span>
  
    ```csharp
    [ServiceContract]  
    public interface IMusicService  
    {  
        //This operation uses a GET method.  
        [OperationContract]  
        [WebGet]  
        string LookUpArtist(string album);  
  
        //This operation will use a POST method.  
        [OperationContract]  
        [WebInvoke]  
        void AddAlbum(string user, string album);  
  
        //This operation will use POST method by default  
        //since nothing else is explicitly specified.  
        [OperationContract]  
        string[] GetAlbums(string user);  
  
        //Other operations omitted…  
  
    }  
    ```  
  
2. <span data-ttu-id="ecb87-129">Implementare il contratto di servizio `IMusicService` con `MusicService`.</span><span class="sxs-lookup"><span data-stu-id="ecb87-129">Implement the `IMusicService` service contract with a `MusicService`.</span></span>
  
    ```csharp
    public class MusicService : IMusicService  
    {  
        public void AddAlbum(string user, string album)  
        {  
            //Add implementation here.  
        }  
  
         //Other operations omitted…  
    }  
    ```  
  
3. <span data-ttu-id="ecb87-130">Creare un nuovo file denominato "file del servizio" con estensione svc nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ecb87-130">Create a new file named service with a .svc extension in the application.</span></span> <span data-ttu-id="ecb87-131">Modificare questo file aggiungendo le informazioni della direttiva [ \@ ServiceHost](../../configure-apps/file-schema/wcf-directive/servicehost.md) appropriate per il servizio.</span><span class="sxs-lookup"><span data-stu-id="ecb87-131">Edit this file by adding the appropriate [\@ServiceHost](../../configure-apps/file-schema/wcf-directive/servicehost.md) directive information for the service.</span></span> <span data-ttu-id="ecb87-132">Consente di specificare che deve <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> essere utilizzato nella direttiva [ \@ ServiceHost](../../configure-apps/file-schema/wcf-directive/servicehost.md) per configurare automaticamente un endpoint ASP.NET AJAX.</span><span class="sxs-lookup"><span data-stu-id="ecb87-132">Specify that the <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> is to be used in the [\@ServiceHost](../../configure-apps/file-schema/wcf-directive/servicehost.md) directive to automatically configure an ASP.NET AJAX endpoint.</span></span>  
  
    ```
    <%@ServiceHost
        language=c#
        Debug="true"
        Service="Microsoft.Ajax.Samples.MusicService"  
        Factory=System.ServiceModel.Activation.WebScriptServiceHostFactory  
    %>  
    ```  
  
## <a name="to-call-the-service"></a><span data-ttu-id="ecb87-133">Per chiamare il servizio</span><span class="sxs-lookup"><span data-stu-id="ecb87-133">To call the service</span></span>  
  
1. <span data-ttu-id="ecb87-134">È possibile testare le operazioni GET del servizio senza alcun codice client, usando il browser.</span><span class="sxs-lookup"><span data-stu-id="ecb87-134">You can test your service's GET operations without any client code, by using the browser.</span></span> <span data-ttu-id="ecb87-135">Se, ad esempio, il servizio è configurato in corrispondenza dell' `http://example.com/service.svc` Indirizzo, digitando `http://example.com/service.svc/LookUpArtist?album=SomeAlbum` nella barra degli indirizzi del browser viene richiamato il servizio e la risposta viene scaricata o visualizzata.</span><span class="sxs-lookup"><span data-stu-id="ecb87-135">For example, if your service is configured at the `http://example.com/service.svc` address, then typing `http://example.com/service.svc/LookUpArtist?album=SomeAlbum` into the browser address bar invokes the service and causes the response to be downloaded or displayed.</span></span>
  
2. <span data-ttu-id="ecb87-136">È possibile usare servizi con operazioni GET esattamente come qualsiasi altro servizio ASP.NET AJAX, immettendo l'URL del servizio nella raccolta degli script del controllo Script Manager ASP.NET AJAX.</span><span class="sxs-lookup"><span data-stu-id="ecb87-136">You can use services with GET operations in the same way as any other ASP.NET AJAX services - by entering the service URL into the Scripts collection of the ASP.NET AJAX Script Manager control.</span></span> <span data-ttu-id="ecb87-137">Per un esempio, vedere [servizio AJAX di base](../samples/basic-ajax-service.md).</span><span class="sxs-lookup"><span data-stu-id="ecb87-137">For an example, see the [Basic AJAX Service](../samples/basic-ajax-service.md).</span></span>
  
## <a name="see-also"></a><span data-ttu-id="ecb87-138">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ecb87-138">See also</span></span>

- [<span data-ttu-id="ecb87-139">Creazione di servizi WCF per ASP.NET AJAX</span><span class="sxs-lookup"><span data-stu-id="ecb87-139">Creating WCF Services for ASP.NET AJAX</span></span>](creating-wcf-services-for-aspnet-ajax.md)
- [<span data-ttu-id="ecb87-140">Procedura: eseguire la migrazione di servizi Web ASP.NET compatibili AJAX a WCF</span><span class="sxs-lookup"><span data-stu-id="ecb87-140">How to: Migrate AJAX-Enabled ASP.NET Web Services to WCF</span></span>](how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)

---
title: Monitoraggio dell’integrità
description: Esplorare un approccio per implementare il monitoraggio dell'integrità.
ms.date: 03/02/2020
ms.openlocfilehash: 88354ae0ae59dbfbe40dbe1b25320f8f93d042ce
ms.sourcegitcommit: e3cbf26d67f7e9286c7108a2752804050762d02d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/09/2020
ms.locfileid: "80988856"
---
# <a name="health-monitoring"></a><span data-ttu-id="fba6f-103">Monitoraggio dell’integrità</span><span class="sxs-lookup"><span data-stu-id="fba6f-103">Health monitoring</span></span>

<span data-ttu-id="fba6f-104">Il monitoraggio dell'integrità consente di ottenere quasi in tempo reale informazioni sullo stato di contenitori e microservizi.</span><span class="sxs-lookup"><span data-stu-id="fba6f-104">Health monitoring can allow near-real-time information about the state of your containers and microservices.</span></span> <span data-ttu-id="fba6f-105">Il monitoraggio dell'integrità è fondamentale per vari aspetti dei microservizi operativi ed è particolarmente importante quando gli agenti di orchestrazione eseguono aggiornamenti parziali dell'applicazione in fasi, come illustrato più avanti.</span><span class="sxs-lookup"><span data-stu-id="fba6f-105">Health monitoring is critical to multiple aspects of operating microservices and is especially important when orchestrators perform partial application upgrades in phases, as explained later.</span></span>

<span data-ttu-id="fba6f-106">Le applicazioni basate su microservizi usano spesso heartbeat o controlli di integrità per consentire ai monitor di prestazioni, alle utilità di pianificazione e agli agenti di orchestrazione di tenere traccia dei numerosi servizi.</span><span class="sxs-lookup"><span data-stu-id="fba6f-106">Microservices-based applications often use heartbeats or health checks to enable their performance monitors, schedulers, and orchestrators to keep track of the multitude of services.</span></span> <span data-ttu-id="fba6f-107">Se i servizi non possono inviare una sorta di segnale "Sono attivo", su richiesta o in base a una pianificazione, l'applicazione potrebbe essere in grado di affrontare rischi quando si distribuiscono gli aggiornamenti oppure potrebbe semplicemente rilevare gli errori troppo tardi e non essere in grado di arrestare gli errori a catena che possono verificarsi gravi interruzioni.</span><span class="sxs-lookup"><span data-stu-id="fba6f-107">If services cannot send some sort of "I'm alive" signal, either on demand or on a schedule, your application might face risks when you deploy updates, or it might just detect failures too late and not be able to stop cascading failures that can end up in major outages.</span></span>

<span data-ttu-id="fba6f-108">Nel modello tipico, i servizi inviano report sul proprio stato e queste informazioni vengono aggregate per fornire una visualizzazione complessiva dello stato di integrità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fba6f-108">In the typical model, services send reports about their status, and that information is aggregated to provide an overall view of the state of health of your application.</span></span> <span data-ttu-id="fba6f-109">Se si usa un agente di orchestrazione, è possibile fornire informazioni sull'integrità al cluster dell'agente di orchestrazione, in modo che il cluster possa agire di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="fba6f-109">If you're using an orchestrator, you can provide health information to your orchestrator's cluster, so that the cluster can act accordingly.</span></span> <span data-ttu-id="fba6f-110">Investendo sulla creazione di report sull'integrità di alta qualità personalizzati per l'applicazione, è possibile rilevare e risolvere molto più facilmente i problemi dell'applicazione in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fba6f-110">If you invest in high-quality health reporting that's customized for your application, you can detect and fix issues for your running application much more easily.</span></span>

## <a name="implement-health-checks-in-aspnet-core-services"></a><span data-ttu-id="fba6f-111">Implementare i controlli di integrità nei servizi ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="fba6f-111">Implement health checks in ASP.NET Core services</span></span>

<span data-ttu-id="fba6f-112">Quando si sviluppa un'applicazione Web o un microservizio ASP.NET Core, è possibile utilizzare la funzionalità di controllo dell'integrità incorporata rilasciata in ASP .NET Core 2.2 ([Microsoft.Extensions.Diagnostics.HealthChecks](https://www.nuget.org/packages/Microsoft.Extensions.Diagnostics.HealthChecks)).</span><span class="sxs-lookup"><span data-stu-id="fba6f-112">When developing an ASP.NET Core microservice or web application, you can use the built-in health checks feature that was released in ASP .NET Core 2.2 ([Microsoft.Extensions.Diagnostics.HealthChecks](https://www.nuget.org/packages/Microsoft.Extensions.Diagnostics.HealthChecks)).</span></span> <span data-ttu-id="fba6f-113">Come molte delle funzionalità di ASP.NET Core, i controlli di integrità includono un set di servizi e un middleware.</span><span class="sxs-lookup"><span data-stu-id="fba6f-113">Like many ASP.NET Core features, health checks come with a set of services and a middleware.</span></span>

<span data-ttu-id="fba6f-114">I servizi e il middleware per i controlli di integrità sono facili da usare e offrono funzionalità che consentono di accertarsi del corretto funzionamento di qualsiasi risorsa esterna necessaria per l'applicazione (ad esempio un database di SQL Server o un API remota).</span><span class="sxs-lookup"><span data-stu-id="fba6f-114">Health check services and middleware are easy to use and provide capabilities that let you validate if any external resource needed for your application (like a SQL Server database or a remote API) is working properly.</span></span> <span data-ttu-id="fba6f-115">Quando si usa questa funzionalità, è possibile anche decidere cosa si intende per integrità della risorsa, come illustrato più avanti.</span><span class="sxs-lookup"><span data-stu-id="fba6f-115">When you use this feature, you can also decide what it means that the resource is healthy, as we explain later.</span></span>

<span data-ttu-id="fba6f-116">Per usare questa funzionalità in modo efficace, è prima necessario configurare i servizi nei microservizi.</span><span class="sxs-lookup"><span data-stu-id="fba6f-116">To use this feature effectively, you need to first configure services in your microservices.</span></span> <span data-ttu-id="fba6f-117">In secondo luogo, è necessaria un'applicazione front-end che esegua query per i report sull'integrità.</span><span class="sxs-lookup"><span data-stu-id="fba6f-117">Second, you need a front-end application that queries for the health reports.</span></span> <span data-ttu-id="fba6f-118">Tale applicazione front-end potrebbe essere un'applicazione di creazione di report personalizzata oppure un agente di orchestrazione in grado di agire in base agli stati di integrità.</span><span class="sxs-lookup"><span data-stu-id="fba6f-118">That front-end application could be a custom reporting application, or it could be an orchestrator itself that can react accordingly to the health states.</span></span>

### <a name="use-the-healthchecks-feature-in-your-back-end-aspnet-microservices"></a><span data-ttu-id="fba6f-119">Usare la funzionalità HealthChecks nei microservizi ASP.NET di back-end</span><span class="sxs-lookup"><span data-stu-id="fba6f-119">Use the HealthChecks feature in your back-end ASP.NET microservices</span></span>

<span data-ttu-id="fba6f-120">In questa sezione verrà illustrato come implementare la funzionalità HealthChecks in un esempio ASP.NETapplicazione API Web Core 3.1 quando si usa il pacchetto [Microsoft.Extensions.Diagnostics.HealthChecks.](https://www.nuget.org/packages/Microsoft.Extensions.Diagnostics.HealthChecks)</span><span class="sxs-lookup"><span data-stu-id="fba6f-120">In this section, you'll learn how to implement the HealthChecks feature in a sample ASP.NET Core 3.1 Web API application when using the [Microsoft.Extensions.Diagnostics.HealthChecks](https://www.nuget.org/packages/Microsoft.Extensions.Diagnostics.HealthChecks) package.</span></span> <span data-ttu-id="fba6f-121">L'implementazione di questa funzionalità in un microservizi su larga scala come eShopOnContainers è illustrata nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="fba6f-121">The Implementation of this feature in a large-scale microservices like the eShopOnContainers is explained in the next section.</span></span>

<span data-ttu-id="fba6f-122">Per iniziare, è necessario definire gli elementi che costituiscono uno stato integro per ogni microservizio.</span><span class="sxs-lookup"><span data-stu-id="fba6f-122">To begin, you need to define what constitutes a healthy status for each microservice.</span></span> <span data-ttu-id="fba6f-123">Nell'applicazione di esempio viene definito che il microservizio è integro se la relativa API è accessibile tramite HTTP e il relativo database SQL Server è disponibile anche.</span><span class="sxs-lookup"><span data-stu-id="fba6f-123">In the sample application, we define the microservice is healthy if its API is accessible via HTTP and its related SQL Server database is also available.</span></span>

<span data-ttu-id="fba6f-124">In .NET Core 3.1, con le API incorporate, è possibile configurare i servizi, aggiungere un controllo di integrità per il microservizio e il relativo database SQL Server dipendente nel modo seguente:In .NET Core 3.1, with the built-in APIs, you can configure the services, add a Health Check for the microservice and its dependent SQL Server database in this way:</span><span class="sxs-lookup"><span data-stu-id="fba6f-124">In .NET Core 3.1, with the built-in APIs, you can configure the services, add a Health Check for the microservice and its dependent SQL Server database in this way:</span></span>

```csharp
// Startup.cs from .NET Core 3.1 Web API sample
//
public void ConfigureServices(IServiceCollection services)
{
    //...
    // Registers required services for health checks
    services.AddHealthChecks()
        // Add a health check for a SQL Server database
        .AddCheck(
            "OrderingDB-check",
            new SqlConnectionHealthCheck(Configuration["ConnectionString"]),
            HealthStatus.Unhealthy,
            new string[] { "orderingdb" });
}
```

<span data-ttu-id="fba6f-125">Nel codice precedente, `services.AddHealthChecks()` il metodo configura un controllo HTTP di base che restituisce un codice di stato **200** con "Integro".</span><span class="sxs-lookup"><span data-stu-id="fba6f-125">In the previous code, the `services.AddHealthChecks()` method configures a basic HTTP check that returns a status code **200** with "Healthy".</span></span>  <span data-ttu-id="fba6f-126">Inoltre, `AddCheck()` il metodo di `SqlConnectionHealthCheck` estensione configura un personalizzato che controlla l'integrità del database SQL correlato.</span><span class="sxs-lookup"><span data-stu-id="fba6f-126">Further, the `AddCheck()` extension method configures a custom `SqlConnectionHealthCheck` that checks the related SQL Database's health.</span></span>

<span data-ttu-id="fba6f-127">Il metodo `AddCheck()` aggiunge un nuovo controllo di integrità con un nome specificato e l'implementazione del tipo `IHealthCheck`.</span><span class="sxs-lookup"><span data-stu-id="fba6f-127">The `AddCheck()` method adds a new health check with a specified name and the implementation of type `IHealthCheck`.</span></span> <span data-ttu-id="fba6f-128">È possibile aggiungere più controlli di integrità usando il metodo AddCheck, in modo che un microservizio non fornisca uno stato "integro" fino a quando tutti i controlli non sono integri.</span><span class="sxs-lookup"><span data-stu-id="fba6f-128">You can add multiple Health Checks using AddCheck method, so a microservice won't provide a "healthy" status until all its checks are healthy.</span></span>

<span data-ttu-id="fba6f-129">`SqlConnectionHealthCheck` è una classe personalizzata che implementa `IHealthCheck`, che accetta una stringa di connessione come parametro di costruttore ed esegue una query semplice per verificare se la connessione al database SQL ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="fba6f-129">`SqlConnectionHealthCheck` is a custom class that implements `IHealthCheck`, which takes a connection string as a constructor parameter and executes a simple query to check if the connection to the SQL database is successful.</span></span> <span data-ttu-id="fba6f-130">Restituisce `HealthCheckResult.Healthy()` se la query è stata eseguita correttamente e `FailureStatus` con l'eccezione effettiva in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="fba6f-130">It returns `HealthCheckResult.Healthy()` if the query was executed successfully and a `FailureStatus` with the actual exception when it fails.</span></span>

```csharp
// Sample SQL Connection Health Check
public class SqlConnectionHealthCheck : IHealthCheck
{
    private static readonly string DefaultTestQuery = "Select 1";

    public string ConnectionString { get; }

    public string TestQuery { get; }

    public SqlConnectionHealthCheck(string connectionString)
        : this(connectionString, testQuery: DefaultTestQuery)
    {
    }

    public SqlConnectionHealthCheck(string connectionString, string testQuery)
    {
        ConnectionString = connectionString ?? throw new ArgumentNullException(nameof(connectionString));
        TestQuery = testQuery;
    }

    public async Task<HealthCheckResult> CheckHealthAsync(HealthCheckContext context, CancellationToken cancellationToken = default(CancellationToken))
    {
        using (var connection = new SqlConnection(ConnectionString))
        {
            try
            {
                await connection.OpenAsync(cancellationToken);

                if (TestQuery != null)
                {
                    var command = connection.CreateCommand();
                    command.CommandText = TestQuery;

                    await command.ExecuteNonQueryAsync(cancellationToken);
                }
            }
            catch (DbException ex)
            {
                return new HealthCheckResult(status: context.Registration.FailureStatus, exception: ex);
            }
        }

        return HealthCheckResult.Healthy();
    }
}
```

<span data-ttu-id="fba6f-131">Si noti che nel codice precedente, `Select 1` è la query usata per controllare l'integrità del database.</span><span class="sxs-lookup"><span data-stu-id="fba6f-131">Note that in the previous code, `Select 1` is the query used to check the Health of the database.</span></span> <span data-ttu-id="fba6f-132">Per monitorare la disponibilità dei microservizi, gli agenti di orchestrazione come Kubernetes eseguono periodicamente controlli di integrità inviando richieste per testare i microservizi.</span><span class="sxs-lookup"><span data-stu-id="fba6f-132">To monitor the availability of your microservices, orchestrators like Kubernetes periodically perform health checks by sending requests to test the microservices.</span></span> <span data-ttu-id="fba6f-133">È importante mantenere efficienti le query sul database in modo che queste operazioni siano veloci e non determinino un maggiore utilizzo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="fba6f-133">It's important to keep your database queries efficient so that these operations are quick and don’t result in a higher utilization of resources.</span></span>

<span data-ttu-id="fba6f-134">Infine, aggiungere un middleware che risponde `/hc`al percorso URL :</span><span class="sxs-lookup"><span data-stu-id="fba6f-134">Finally, add a middleware that responds to the url path `/hc`:</span></span>

```csharp
// Startup.cs from .NET Core 3.1 Web Api sample
//
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    //…
    app.UseEndpoints(endpoints =>
    {
        //...
        endpoints.MapHealthChecks("/hc");
        //...
    });
    //…
}
```

<span data-ttu-id="fba6f-135">Quando l'endpoint `<yourmicroservice>/hc` viene richiamato, esegue tutti i controlli di integrità configurati nel metodo `AddHealthChecks()` nella classe di avvio e visualizza il risultato.</span><span class="sxs-lookup"><span data-stu-id="fba6f-135">When the endpoint `<yourmicroservice>/hc` is invoked, it runs all the health checks that are configured in the `AddHealthChecks()` method in the Startup class and shows the result.</span></span>

### <a name="healthchecks-implementation-in-eshoponcontainers"></a><span data-ttu-id="fba6f-136">Implementazione di HealthChecks in eShopOnContainers</span><span class="sxs-lookup"><span data-stu-id="fba6f-136">HealthChecks implementation in eShopOnContainers</span></span>

<span data-ttu-id="fba6f-137">I microservizi in eShopOnContainers si basano su più servizi per eseguire le attività.</span><span class="sxs-lookup"><span data-stu-id="fba6f-137">Microservices in eShopOnContainers rely on multiple services to perform its task.</span></span> <span data-ttu-id="fba6f-138">Ad esempio, il microservizio `Catalog.API` da eShopOnContainers dipende da molti servizi, ad esempio Archiviazione BLOB di Azure, SQL Server e RabbitMQ.</span><span class="sxs-lookup"><span data-stu-id="fba6f-138">For example, the `Catalog.API` microservice from eShopOnContainers depends on many services, such as Azure Blob Storage, SQL Server, and RabbitMQ.</span></span> <span data-ttu-id="fba6f-139">Pertanto, include diversi controlli di integrità aggiunti con il metodo `AddCheck()`.</span><span class="sxs-lookup"><span data-stu-id="fba6f-139">Therefore, it has several health checks added using the `AddCheck()` method.</span></span> <span data-ttu-id="fba6f-140">Per ogni servizio dipendente, è necessario aggiungere un'implementazione personalizzata `IHealthCheck` che definisce il rispettivo stato di integrità.</span><span class="sxs-lookup"><span data-stu-id="fba6f-140">For every dependent service, a custom `IHealthCheck` implementation that defines its respective health status would need to be added.</span></span>

<span data-ttu-id="fba6f-141">Il progetto open source [AspNetCore.Diagnostics.HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks) risolve questo problema fornendo implementazioni di controllo dell'integrità personalizzate per ognuno di questi servizi aziendali, che si basano su .NET Core 3.1.</span><span class="sxs-lookup"><span data-stu-id="fba6f-141">The open-source project [AspNetCore.Diagnostics.HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks) solves this problem by providing custom health check implementations for each of these enterprise services, that are built on top of .NET Core 3.1.</span></span> <span data-ttu-id="fba6f-142">Ogni controllo di integrità è disponibile come singolo pacchetto NuGet che può essere facilmente aggiunto al progetto.</span><span class="sxs-lookup"><span data-stu-id="fba6f-142">Each health check is available as an individual NuGet package that can be easily added to the project.</span></span> <span data-ttu-id="fba6f-143">eShopOnContainers li utilizza ampiamente in tutti i suoi microservizi.</span><span class="sxs-lookup"><span data-stu-id="fba6f-143">eShopOnContainers uses them extensively in all its microservices.</span></span>

<span data-ttu-id="fba6f-144">Ad esempio, nel microservizio `Catalog.API` sono stati aggiunti i pacchetti NuGet seguenti:</span><span class="sxs-lookup"><span data-stu-id="fba6f-144">For instance, in the `Catalog.API` microservice, the following NuGet packages were added:</span></span>

![Screenshot dei pacchetti AspNetCore.Diagnostics.HealthChecks NuGet.](./media/monitor-app-health/aspnet-core-diagnostics-health-checks.png)

<span data-ttu-id="fba6f-146">**Figura 8-7**.</span><span class="sxs-lookup"><span data-stu-id="fba6f-146">**Figure 8-7**.</span></span> <span data-ttu-id="fba6f-147">Controlli di integrità personalizzati implementati in Catalog.API tramite AspNetCore.Diagnostics.HealthChecks</span><span class="sxs-lookup"><span data-stu-id="fba6f-147">Custom Health Checks implemented in Catalog.API using AspNetCore.Diagnostics.HealthChecks</span></span>

<span data-ttu-id="fba6f-148">Nel codice seguente, vengono aggiunte le implementazioni dei controlli di integrità per ogni servizio dipendente e quindi viene configurato il middleware:</span><span class="sxs-lookup"><span data-stu-id="fba6f-148">In the following code, the health check implementations are added for each dependent service and then the middleware is configured:</span></span>

```csharp
// Startup.cs from Catalog.api microservice
//
public static IServiceCollection AddCustomHealthCheck(this IServiceCollection services, IConfiguration configuration)
{
    var accountName = configuration.GetValue<string>("AzureStorageAccountName");
    var accountKey = configuration.GetValue<string>("AzureStorageAccountKey");

    var hcBuilder = services.AddHealthChecks();

    hcBuilder
        .AddSqlServer(
            configuration["ConnectionString"],
            name: "CatalogDB-check",
            tags: new string[] { "catalogdb" });

    if (!string.IsNullOrEmpty(accountName) && !string.IsNullOrEmpty(accountKey))
    {
        hcBuilder
            .AddAzureBlobStorage(
                $"DefaultEndpointsProtocol=https;AccountName={accountName};AccountKey={accountKey};EndpointSuffix=core.windows.net",
                name: "catalog-storage-check",
                tags: new string[] { "catalogstorage" });
    }
    if (configuration.GetValue<bool>("AzureServiceBusEnabled"))
    {
        hcBuilder
            .AddAzureServiceBusTopic(
                configuration["EventBusConnection"],
                topicName: "eshop_event_bus",
                name: "catalog-servicebus-check",
                tags: new string[] { "servicebus" });
    }
    else
    {
        hcBuilder
            .AddRabbitMQ(
                $"amqp://{configuration["EventBusConnection"]}",
                name: "catalog-rabbitmqbus-check",
                tags: new string[] { "rabbitmqbus" });
    }

    return services;
}
```

<span data-ttu-id="fba6f-149">Infine, aggiungere il middleware HealthCheck per l'ascolto dell'endpoint "/hc":</span><span class="sxs-lookup"><span data-stu-id="fba6f-149">Finally, add the HealthCheck middleware to listen to “/hc” endpoint:</span></span>

```csharp
// HealthCheck middleware
app.UseHealthChecks("/hc", new HealthCheckOptions()
{
    Predicate = _ => true,
    ResponseWriter = UIResponseWriter.WriteHealthCheckUIResponse
});
}
```

### <a name="query-your-microservices-to-report-about-their-health-status"></a><span data-ttu-id="fba6f-150">Eseguire query sui microservizi per creare report sullo stato di integrità</span><span class="sxs-lookup"><span data-stu-id="fba6f-150">Query your microservices to report about their health status</span></span>

<span data-ttu-id="fba6f-151">Dopo aver configurato i controlli di integrità come descritto in questo articolo, quando il microservizio è in esecuzione in Docker è possibile verificarne l'integrità direttamente da un browser.</span><span class="sxs-lookup"><span data-stu-id="fba6f-151">When you've configured health checks as described in this article and you have the microservice running in Docker, you can directly check from a browser if it's healthy.</span></span> <span data-ttu-id="fba6f-152">È necessario pubblicare la porta del contenitore nell'host Docker in modo da poter accedere al contenitore tramite l'IP dell'host Docker o tramite `localhost`, come illustrato nella Figura 8-8.</span><span class="sxs-lookup"><span data-stu-id="fba6f-152">You have to publish the container port in the Docker host, so you can access the container through the external Docker host IP or through `localhost`, as shown in figure 8-8.</span></span>

![Screenshot della risposta JSON restituita da un controllo di integrità.](./media/monitor-app-health/health-check-json-response.png)

<span data-ttu-id="fba6f-154">**Figura 8-8**.</span><span class="sxs-lookup"><span data-stu-id="fba6f-154">**Figure 8-8**.</span></span> <span data-ttu-id="fba6f-155">Verifica dello stato di integrità di un singolo servizio da un browser</span><span class="sxs-lookup"><span data-stu-id="fba6f-155">Checking health status of a single service from a browser</span></span>

<span data-ttu-id="fba6f-156">In questo test, si può notare che il microservizio `Catalog.API` (in esecuzione sulla porta 5101) è integro e restituisce lo stato HTTP 200 e le informazioni sullo stato in JSON.</span><span class="sxs-lookup"><span data-stu-id="fba6f-156">In that test, you can see that the `Catalog.API` microservice (running on port 5101) is healthy, returning HTTP status 200 and status information in JSON.</span></span> <span data-ttu-id="fba6f-157">Il servizio ha controllato anche l'integrità della propria dipendenza dal database SQL Server e di RabbitMQ, quindi il controllo di integrità è risultato integro.</span><span class="sxs-lookup"><span data-stu-id="fba6f-157">The service also checked the health of its SQL Server database dependency and RabbitMQ, so the health check reported itself as healthy.</span></span>

## <a name="use-watchdogs"></a><span data-ttu-id="fba6f-158">Usare watchdog</span><span class="sxs-lookup"><span data-stu-id="fba6f-158">Use watchdogs</span></span>

<span data-ttu-id="fba6f-159">Un watchdog è un servizio separato in grado di controllare l'integrità e il carico tra servizi e segnalare l'integrità dei microservizi eseguendo una query con la libreria `HealthChecks` introdotta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fba6f-159">A watchdog is a separate service that can watch health and load across services, and report health about the microservices by querying with the `HealthChecks` library introduced earlier.</span></span> <span data-ttu-id="fba6f-160">Questo consente di evitare errori che non verrebbero rilevati visualizzando un singolo servizio.</span><span class="sxs-lookup"><span data-stu-id="fba6f-160">This can help prevent errors that would not be detected based on the view of a single service.</span></span> <span data-ttu-id="fba6f-161">I watchdog sono una buona posizione in cui ospitare codice in grado di eseguire interventi correttivi per condizioni note senza bisogno di azioni da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="fba6f-161">Watchdogs also are a good place to host code that can perform remediation actions for known conditions without user interaction.</span></span>

<span data-ttu-id="fba6f-162">L'esempio eShopOnContainers contiene una pagina Web che visualizza report di esempio sul controllo di integrità, come illustrato nella figura 8-9.</span><span class="sxs-lookup"><span data-stu-id="fba6f-162">The eShopOnContainers sample contains a web page that displays sample health check reports, as shown in Figure 8-9.</span></span> <span data-ttu-id="fba6f-163">Questo è il tipo watchdog più semplice possibile, poiché si limita a visualizzare lo stato dei microservizi e delle applicazioni Web in eShopOnContainers.</span><span class="sxs-lookup"><span data-stu-id="fba6f-163">This is the simplest watchdog you could have since it only shows the state of the microservices and web applications in eShopOnContainers.</span></span> <span data-ttu-id="fba6f-164">In genere un watchdog esegue anche azioni quando rileva stati non integri.</span><span class="sxs-lookup"><span data-stu-id="fba6f-164">Usually a watchdog also takes actions when it detects unhealthy states.</span></span>

<span data-ttu-id="fba6f-165">Per fortuna [AspNetCore.Diagnostics.HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks) fornisce anche il pacchetto NuGet [AspNetCore.HealthChecks.UI](https://www.nuget.org/packages/AspNetCore.HealthChecks.UI/) che può essere usato per visualizzare i risultati dei controlli di integrità dagli URI configurati.</span><span class="sxs-lookup"><span data-stu-id="fba6f-165">Fortunately, [AspNetCore.Diagnostics.HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks) also provides [AspNetCore.HealthChecks.UI](https://www.nuget.org/packages/AspNetCore.HealthChecks.UI/) NuGet package that can be used to display the health check results from the configured URIs.</span></span>

![Screenshot degli stati di integrità eShopOnContainers dei controlli di integrità.](./media/monitor-app-health/health-check-status-ui.png)

<span data-ttu-id="fba6f-167">**Figura 8-9**.</span><span class="sxs-lookup"><span data-stu-id="fba6f-167">**Figure 8-9**.</span></span> <span data-ttu-id="fba6f-168">Report di controllo di integrità di esempio in eShopOnContainers</span><span class="sxs-lookup"><span data-stu-id="fba6f-168">Sample health check report in eShopOnContainers</span></span>

<span data-ttu-id="fba6f-169">In sintesi, questo servizio watchdog esegue una query sull'endpoint "/hc" di ogni microservizio.</span><span class="sxs-lookup"><span data-stu-id="fba6f-169">In summary, this watchdog service queries each microservice's "/hc" endpoint.</span></span> <span data-ttu-id="fba6f-170">In tal modo verranno eseguiti tutti i controlli di integrità definiti al suo interno e verrà restituito uno stato di integrità globale in base a tutti i controlli.</span><span class="sxs-lookup"><span data-stu-id="fba6f-170">This will execute all the health checks defined within it and return an overall health state depending on all those checks.</span></span> <span data-ttu-id="fba6f-171">L'utilizzo di HealthChecksUI è facile con poche voci di configurazione e due righe di codice che devono essere aggiunte nel file Startup.cs del servizio watchdog.</span><span class="sxs-lookup"><span data-stu-id="fba6f-171">The HealthChecksUI is easy to consume with a few configuration entries and two lines of code that needs to be added into the Startup.cs of the watchdog service.</span></span>

<span data-ttu-id="fba6f-172">File di configurazione di esempio per l'interfaccia utente dei controlli di integrità:</span><span class="sxs-lookup"><span data-stu-id="fba6f-172">Sample configuration file for health check UI:</span></span>

```json
// Configuration
{
  "HealthChecks-UI": {
    "HealthChecks": [
      {
        "Name": "Ordering HTTP Check",
        "Uri": "http://localhost:5102/hc"
      },
      {
        "Name": "Ordering HTTP Background Check",
        "Uri": "http://localhost:5111/hc"
      },
      //...
    ]}
}
```

<span data-ttu-id="fba6f-173">File Startup.cs con aggiunta di HealthChecksUI:</span><span class="sxs-lookup"><span data-stu-id="fba6f-173">Startup.cs file that adds HealthChecksUI:</span></span>

```csharp
// Startup.cs from WebStatus(Watch Dog) service
//
public void ConfigureServices(IServiceCollection services)
{
    //…
    // Registers required services for health checks
    services.AddHealthChecksUI();
}
//…
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    //…
    app.UseHealthChecksUI(config=> config.UIPath = "/hc-ui");
    //…
}
```

## <a name="health-checks-when-using-orchestrators"></a><span data-ttu-id="fba6f-174">Controlli di integrità quando si usano agenti di orchestrazione</span><span class="sxs-lookup"><span data-stu-id="fba6f-174">Health checks when using orchestrators</span></span>

<span data-ttu-id="fba6f-175">Per monitorare la disponibilità dei microservizi, gli agenti di orchestrazione come Kubernetes e Service Fabric eseguono periodicamente controlli di integrità, inviando richieste di esecuzione di test sui microservizi.</span><span class="sxs-lookup"><span data-stu-id="fba6f-175">To monitor the availability of your microservices, orchestrators like Kubernetes and Service Fabric periodically perform health checks by sending requests to test the microservices.</span></span> <span data-ttu-id="fba6f-176">Quando un agente di orchestrazione determina che un servizio o contenitore non è integro, interrompe il routing delle richieste a tale istanza.</span><span class="sxs-lookup"><span data-stu-id="fba6f-176">When an orchestrator determines that a service/container is unhealthy, it stops routing requests to that instance.</span></span> <span data-ttu-id="fba6f-177">In genere crea anche una nuova istanza di tale contenitore.</span><span class="sxs-lookup"><span data-stu-id="fba6f-177">It also usually creates a new instance of that container.</span></span>

<span data-ttu-id="fba6f-178">Ad esempio, gran parte degli agenti di orchestrazione può usare controlli di integrità per gestire le distribuzioni senza tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="fba6f-178">For instance, most orchestrators can use health checks to manage zero-downtime deployments.</span></span> <span data-ttu-id="fba6f-179">Solo quando lo stato di un servizio o contenitore diventa integro, l'agente di orchestrazione avvierà il routing del traffico alle istanze del servizio o contenitore.</span><span class="sxs-lookup"><span data-stu-id="fba6f-179">Only when the status of a service/container changes to healthy will the orchestrator start routing traffic to service/container instances.</span></span>

<span data-ttu-id="fba6f-180">Il monitoraggio dell'integrità è particolarmente importante quando un agente di orchestrazione esegue l'aggiornamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fba6f-180">Health monitoring is especially important when an orchestrator performs an application upgrade.</span></span> <span data-ttu-id="fba6f-181">Alcuni agenti di orchestrazione (ad esempio Azure Service Fabric) aggiornano i servizi in fasi, ad esempio aggiornano un quinto della superficie di cluster per ogni aggiornamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fba6f-181">Some orchestrators (like Azure Service Fabric) update services in phases—for example, they might update one-fifth of the cluster surface for each application upgrade.</span></span> <span data-ttu-id="fba6f-182">Il set di nodi che viene aggiornato allo stesso tempo è detto *dominio di aggiornamento*.</span><span class="sxs-lookup"><span data-stu-id="fba6f-182">The set of nodes that's upgraded at the same time is referred to as an *upgrade domain*.</span></span> <span data-ttu-id="fba6f-183">Quando un dominio di aggiornamento risulta aggiornato ed è disponibile agli utenti, deve superare i controlli di integrità prima che la distribuzione passi al dominio di aggiornamento successivo.</span><span class="sxs-lookup"><span data-stu-id="fba6f-183">After each upgrade domain has been upgraded and is available to users, that upgrade domain must pass health checks before the deployment moves to the next upgrade domain.</span></span>

<span data-ttu-id="fba6f-184">Un altro aspetto dell'integrità del servizio è dato dalla creazione di report sulle metriche del servizio.</span><span class="sxs-lookup"><span data-stu-id="fba6f-184">Another aspect of service health is reporting metrics from the service.</span></span> <span data-ttu-id="fba6f-185">Si tratta di una funzionalità avanzata del modello di integrità di alcuni agenti di orchestrazione, ad esempio Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fba6f-185">This is an advanced capability of the health model of some orchestrators, like Service Fabric.</span></span> <span data-ttu-id="fba6f-186">Le metriche sono importanti quando si usa un agente di orchestrazione perché vengono usate per bilanciare l'utilizzo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="fba6f-186">Metrics are important when using an orchestrator because they are used to balance resource usage.</span></span> <span data-ttu-id="fba6f-187">Possono anche essere usate come un indicatore dell'integrità del sistema.</span><span class="sxs-lookup"><span data-stu-id="fba6f-187">Metrics also can be an indicator of system health.</span></span> <span data-ttu-id="fba6f-188">Ad esempio, un'applicazione potrebbe disporre di molti microservizi e ogni istanza potrebbe segnalare una metrica di richieste al secondo (RPS).</span><span class="sxs-lookup"><span data-stu-id="fba6f-188">For example, you might have an application that has many microservices, and each instance reports a requests-per-second (RPS) metric.</span></span> <span data-ttu-id="fba6f-189">Se un servizio usa più risorse (memoria, processore e così via) di un altro servizio, l'agente di orchestrazione potrebbe spostare le istanze del servizio all'interno del cluster per tentare di mantenere uniforme l'utilizzo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="fba6f-189">If one service is using more resources (memory, processor, etc.) than another service, the orchestrator could move service instances around in the cluster to try to maintain even resource utilization.</span></span>

<span data-ttu-id="fba6f-190">Si noti che Azure Service Fabric fornisce il proprio [modello di monitoraggio dell'integrità](/azure/service-fabric/service-fabric-health-introduction), più avanzato rispetto ai semplici controlli di integrità.</span><span class="sxs-lookup"><span data-stu-id="fba6f-190">Note that Azure Service Fabric provides its own [Health Monitoring model](/azure/service-fabric/service-fabric-health-introduction), which is more advanced than simple health checks.</span></span>

## <a name="advanced-monitoring-visualization-analysis-and-alerts"></a><span data-ttu-id="fba6f-191">Monitoraggio avanzato: visualizzazione, analisi e avvisi</span><span class="sxs-lookup"><span data-stu-id="fba6f-191">Advanced monitoring: visualization, analysis, and alerts</span></span>

<span data-ttu-id="fba6f-192">L'ultima parte del monitoraggio consiste nel visualizzare il flusso di eventi, creare report sulle prestazioni dei servizi e avvisare in caso di problemi.</span><span class="sxs-lookup"><span data-stu-id="fba6f-192">The final part of monitoring is visualizing the event stream, reporting on service performance, and alerting when an issue is detected.</span></span> <span data-ttu-id="fba6f-193">È possibile usare soluzioni diverse per questo aspetto del monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="fba6f-193">You can use different solutions for this aspect of monitoring.</span></span>

<span data-ttu-id="fba6f-194">È possibile usare semplici applicazioni personalizzate che visualizzano lo stato dei servizi, ad esempio la pagina personalizzata visualizzata nella spiegazione di [AspNetCore.Diagnostics.HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks).</span><span class="sxs-lookup"><span data-stu-id="fba6f-194">You can use simple custom applications showing the state of your services, like the custom page shown when explaining the [AspNetCore.Diagnostics.HealthChecks](https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks).</span></span> <span data-ttu-id="fba6f-195">In alternativa è possibile usare strumenti più avanzati come [Monitoraggio di Azure](https://azure.microsoft.com/services/monitor/) per la generazione di avvisi in base al flusso di eventi.</span><span class="sxs-lookup"><span data-stu-id="fba6f-195">Or you could use more advanced tools like [Azure Monitor](https://azure.microsoft.com/services/monitor/) to raise alerts based on the stream of events.</span></span>

<span data-ttu-id="fba6f-196">Infine, se si archiviano tutti i flussi di eventi, per visualizzare i dati è possibile usare Microsoft Power BI o una soluzione alternativa quale Kibana o Splunk.</span><span class="sxs-lookup"><span data-stu-id="fba6f-196">Finally, if you're storing all the event streams, you can use Microsoft Power BI or other solutions like Kibana or Splunk to visualize the data.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fba6f-197">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fba6f-197">Additional resources</span></span>

- <span data-ttu-id="fba6f-198">**HealthChecks and HealthChecks UI for ASP.NET Core** </span><span class="sxs-lookup"><span data-stu-id="fba6f-198">**HealthChecks and HealthChecks UI for ASP.NET Core** </span></span>\
  <https://github.com/Xabaril/AspNetCore.Diagnostics.HealthChecks>

- <span data-ttu-id="fba6f-199">**Introduzione al monitoraggio dell'integrità di Service FabricIntroduction to Service Fabric health monitoring** </span><span class="sxs-lookup"><span data-stu-id="fba6f-199">**Introduction to Service Fabric health monitoring** </span></span>\
  [https://docs.microsoft.com/azure/service-fabric/service-fabric-health-introduction](/azure/service-fabric/service-fabric-health-introduction)

- <span data-ttu-id="fba6f-200">**Monitoraggio di AzureAzure Monitor** </span><span class="sxs-lookup"><span data-stu-id="fba6f-200">**Azure Monitor** </span></span>\
  <https://azure.microsoft.com/services/monitor/>

>[!div class="step-by-step"]
><span data-ttu-id="fba6f-201">[Successivo](implement-circuit-breaker-pattern.md)
>[precedente](../secure-net-microservices-web-applications/index.md)</span><span class="sxs-lookup"><span data-stu-id="fba6f-201">[Previous](implement-circuit-breaker-pattern.md)
[Next](../secure-net-microservices-web-applications/index.md)</span></span>

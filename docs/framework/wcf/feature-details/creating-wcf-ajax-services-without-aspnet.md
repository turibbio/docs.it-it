---
title: Creazione di servizi WCF AJAX senza ASP.NET
ms.date: 03/30/2017
ms.assetid: ba4a7d1b-e277-4978-9f62-37684e6dc934
ms.openlocfilehash: b5f0f730f90227dcccc7e5ebf533d80a28f6e6eb
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599295"
---
# <a name="creating-wcf-ajax-services-without-aspnet"></a><span data-ttu-id="90d58-102">Creazione di servizi WCF AJAX senza ASP.NET</span><span class="sxs-lookup"><span data-stu-id="90d58-102">Creating WCF AJAX Services without ASP.NET</span></span>
<span data-ttu-id="90d58-103">È possibile accedere ai servizi AJAX Windows Communication Foundation (WCF) da qualsiasi pagina Web abilitata per JavaScript, senza la necessità di ASP.NET AJAX.</span><span class="sxs-lookup"><span data-stu-id="90d58-103">Windows Communication Foundation (WCF) AJAX services can be accessed from any JavaScript-enabled Web page, without requiring ASP.NET AJAX.</span></span> <span data-ttu-id="90d58-104">In questo argomento viene descritto come creare un servizio WCF di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="90d58-104">This topic describes how to create such a WCF service.</span></span>  
  
 <span data-ttu-id="90d58-105">Per istruzioni sull'utilizzo di WCF con ASP.NET AJAX, vedere [creazione di servizi WCF per ASP.NET AJAX](creating-wcf-services-for-aspnet-ajax.md).</span><span class="sxs-lookup"><span data-stu-id="90d58-105">For instructions on using WCF with ASP.NET AJAX, see [Creating WCF Services for ASP.NET AJAX](creating-wcf-services-for-aspnet-ajax.md).</span></span>  
  
 <span data-ttu-id="90d58-106">La creazione di un servizio AJAX WCF è costituita da tre parti:</span><span class="sxs-lookup"><span data-stu-id="90d58-106">There are three parts to a creating a WCF AJAX service:</span></span>  
  
- <span data-ttu-id="90d58-107">Creazione di un endpoint AJAX a cui sia possibile accedere dal browser.</span><span class="sxs-lookup"><span data-stu-id="90d58-107">Creating an AJAX endpoint that can be accessed from the browser.</span></span>  
  
- <span data-ttu-id="90d58-108">Creazione di un contratto di servizio compatibile con AJAX.</span><span class="sxs-lookup"><span data-stu-id="90d58-108">Creating an AJAX-compatible service contract.</span></span>  
  
- <span data-ttu-id="90d58-109">Accesso ai servizi WCF AJAX.</span><span class="sxs-lookup"><span data-stu-id="90d58-109">Accessing WCF AJAX services.</span></span>  
  
## <a name="creating-an-ajax-endpoint"></a><span data-ttu-id="90d58-110">Creazione di un endpoint AJAX</span><span class="sxs-lookup"><span data-stu-id="90d58-110">Creating an AJAX Endpoint</span></span>  
 <span data-ttu-id="90d58-111">Il modo più semplice per abilitare il supporto AJAX in un servizio WCF consiste nell'usare nel <xref:System.ServiceModel.Activation.WebServiceHostFactory> file con estensione svc associato al servizio, come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="90d58-111">The most basic way to enable AJAX support in a WCF service is to use the <xref:System.ServiceModel.Activation.WebServiceHostFactory> in the .svc file associated with the service, as in the following example.</span></span>  
  
```text
<%ServiceHost
    language=c#  
    Debug="true"  
    Service="Microsoft.Ajax.Samples.CityService"  
    Factory=System.ServiceModel.Activation.WebServiceHostFactory  
%>  
```  
  
 <span data-ttu-id="90d58-112">In alternativa, è anche possibile usare la configurazione per aggiungere un endpoint AJAX.</span><span class="sxs-lookup"><span data-stu-id="90d58-112">Alternatively, you can also use configuration to add an AJAX endpoint.</span></span> <span data-ttu-id="90d58-113">Usare <xref:System.ServiceModel.WebHttpBinding> sull'endpoint del servizio e configurare tale endpoint con <xref:System.ServiceModel.Description.WebHttpBehavior>, come illustrato nel frammento di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="90d58-113">Use the <xref:System.ServiceModel.WebHttpBinding> on the service endpoint and configure that endpoint with the <xref:System.ServiceModel.Description.WebHttpBehavior> as shown in the following code snippet.</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="AjaxBehavior">  
          <webHttp/>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <services>  
      <service name="Microsoft.Ajax.Samples.CityService">  
        <endpoint
          address="ajaxEndpoint"  
          behaviorConfiguration="AjaxBehavior"  
          binding="webHttpBinding"  
          contract="Microsoft.Ajax.Samples.ICityService" />  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="90d58-114">Per un esempio funzionante, vedere il [servizio AJAX con JSON e XML](../samples/ajax-service-with-json-and-xml-sample.md).</span><span class="sxs-lookup"><span data-stu-id="90d58-114">For a working example, see the [AJAX Service with JSON and XML](../samples/ajax-service-with-json-and-xml-sample.md).</span></span>  
  
## <a name="creating-an-ajax-compatible-service-contract"></a><span data-ttu-id="90d58-115">Creazione di un contratto di servizio compatibile con AJAX</span><span class="sxs-lookup"><span data-stu-id="90d58-115">Creating an AJAX-Compatible Service Contract</span></span>  
 <span data-ttu-id="90d58-116">Per impostazione predefinita, i contratti di servizio esposti su un endpoint AJAX restituiscono dati in formato XML.</span><span class="sxs-lookup"><span data-stu-id="90d58-116">By default, service contracts exposed over an AJAX endpoint return data in the XML format.</span></span> <span data-ttu-id="90d58-117">Inoltre, le operazioni del servizio sono accessibili, per impostazione predefinita, tramite richieste HTTP POST agli URL che includono l'indirizzo endpoint seguito dal nome dell'operazione, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="90d58-117">Also, by default service operations are accessible through HTTP POST requests to URLs that include the endpoint address followed by the operation name, as shown in the following example.</span></span>  
  
```csharp
[OperationContract]  
string[] GetCities(string firstLetters);  
```  
  
 <span data-ttu-id="90d58-118">Questa operazione è accessibile tramite HTTP POST a `http://serviceaddress/endpointaddress/GetCities` e restituisce un messaggio XML.</span><span class="sxs-lookup"><span data-stu-id="90d58-118">This operation is accessible using an HTTP POST to `http://serviceaddress/endpointaddress/GetCities` and return an XML message.</span></span>  
  
 <span data-ttu-id="90d58-119">È possibile usare il Modello di programmazione Web completo per personalizzare questi aspetti di base.</span><span class="sxs-lookup"><span data-stu-id="90d58-119">You can use the full Web Programming Model to customize these basic aspects.</span></span> <span data-ttu-id="90d58-120">Ad esempio, è possibile usare gli attributi <xref:System.ServiceModel.Web.WebGetAttribute> o <xref:System.ServiceModel.Web.WebInvokeAttribute> per controllare il verbo HTTP al quale risponde l'operazione o usare la proprietà `UriTemplate` di questi rispettivi attributi per specificare gli URI personalizzati.</span><span class="sxs-lookup"><span data-stu-id="90d58-120">For example, you can use the <xref:System.ServiceModel.Web.WebGetAttribute> or <xref:System.ServiceModel.Web.WebInvokeAttribute> attributes to control the HTTP verb to which the operation responds or use the `UriTemplate` property of these respective attributes to specify custom URIs.</span></span> <span data-ttu-id="90d58-121">Per ulteriori informazioni, vedere l'argomento relativo al [modello di programmazione HTTP Web WCF](wcf-web-http-programming-model.md) .</span><span class="sxs-lookup"><span data-stu-id="90d58-121">For more information, see the [WCF Web HTTP Programming Model](wcf-web-http-programming-model.md) topic.</span></span>  
  
 <span data-ttu-id="90d58-122">Nei servizi AJAX viene spesso usato il formato dati JSON.</span><span class="sxs-lookup"><span data-stu-id="90d58-122">The JSON data format is often used in AJAX services.</span></span> <span data-ttu-id="90d58-123">Per creare un'operazione che restituisce JSON invece di XML, impostare la proprietà <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A> (o <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A>) su <xref:System.ServiceModel.Web.WebMessageFormat.Json>.</span><span class="sxs-lookup"><span data-stu-id="90d58-123">To create an operation that returns JSON instead of XML, set the <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A> (or the <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A>) property to <xref:System.ServiceModel.Web.WebMessageFormat.Json>.</span></span> <span data-ttu-id="90d58-124">L'argomento relativo alla [serializzazione JSON autonoma](stand-alone-json-serialization.md) illustra come eseguire il mapping di tipi .NET e di contratti dati incorporati a JSON.</span><span class="sxs-lookup"><span data-stu-id="90d58-124">The [Stand-Alone JSON Serialization](stand-alone-json-serialization.md) topic shows how built-in .NET types and data contract types map to JSON.</span></span>  
  
 <span data-ttu-id="90d58-125">In genere, le richieste e le risposte JSON sono costituite da un solo elemento.</span><span class="sxs-lookup"><span data-stu-id="90d58-125">Normally, JSON requests and responses consist of just one item.</span></span> <span data-ttu-id="90d58-126">Nell'operazione `GetCities` precedente, la richiesta assomiglia all'istruzione seguente.</span><span class="sxs-lookup"><span data-stu-id="90d58-126">For the preceding `GetCities` operation, the request resembles the following statement.</span></span>  
  
```json
"na"  
```  
  
 <span data-ttu-id="90d58-127">La risposta a questa richiesta è simile all'istruzione seguente.</span><span class="sxs-lookup"><span data-stu-id="90d58-127">The response to that request resembles the following statement.</span></span>  
  
```json
["Nairobi", "Naples", "Nashville"]  
```  
  
 <span data-ttu-id="90d58-128">Se l'operazione accetta un parametro aggiuntivo, lo stile della richiesta deve essere "incapsulato", per eseguire il wrapping di entrambi parametri in un solo oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="90d58-128">If the operation takes an extra parameter, the request style must be wrapped to wrap both parameters in a single JSON object.</span></span> <span data-ttu-id="90d58-129">Un esempio di questo stile di messaggio JSON è riportato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="90d58-129">An example of this style JSON message is in the following example.</span></span>  
  
```json  
{"firstLetters": "na", "maxNumber": 2}  
```  
  
 <span data-ttu-id="90d58-130">Il contratto seguente accetta questo messaggio.</span><span class="sxs-lookup"><span data-stu-id="90d58-130">The following contract accepts this message.</span></span>  
  
```csharp
[WebInvoke(BodyStyle=WebMessageBodyStyle.WrappedRequest, ResponseFormat=WebMessageFormat.Json)]  
[OperationContract]  
string[] GetCities(string firstLetters, int maxNumber);  
```  
  
## <a name="accessing-ajax-services"></a><span data-ttu-id="90d58-131">Accesso ai servizi AJAX.</span><span class="sxs-lookup"><span data-stu-id="90d58-131">Accessing AJAX Services</span></span>  
 <span data-ttu-id="90d58-132">Gli endpoint WCF AJAX accettano sempre richieste JSON e XML.</span><span class="sxs-lookup"><span data-stu-id="90d58-132">WCF AJAX endpoints always accept both JSON and XML requests.</span></span>  
  
 <span data-ttu-id="90d58-133">Le richieste HTTP POST con un tipo di contenuto "application/json" vengono considerate JSON e quelle con tipo di contenuto che indica XML (ad esempio "Text/XML") vengono trattate come XML.</span><span class="sxs-lookup"><span data-stu-id="90d58-133">HTTP POST requests with a content-type of "application/json" are treated as JSON, and those with content-type that indicate XML (for example, "text/xml") are treated as XML.</span></span>  
  
 <span data-ttu-id="90d58-134">Le richieste HTTP GET contengono tutti i parametri di richiesta presenti nell'URL stesso.</span><span class="sxs-lookup"><span data-stu-id="90d58-134">HTTP GET requests contain all the request parameters in the URL itself.</span></span>  
  
 <span data-ttu-id="90d58-135">Spetta all'utente decidere come creare la richiesta HTTP per l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="90d58-135">It is up to the user to decide how to create the HTTP request to the endpoint.</span></span> <span data-ttu-id="90d58-136">Inoltre, l'utente ha il pieno controllo sulla costruzione del codice JSON che forma il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="90d58-136">Also, the user has full control over constructing the JSON that forms the body of the request.</span></span> <span data-ttu-id="90d58-137">Per un esempio di creazione di una richiesta da JavaScript, vedere il [servizio AJAX con JSON e XML](../samples/ajax-service-with-json-and-xml-sample.md).</span><span class="sxs-lookup"><span data-stu-id="90d58-137">For an example of creating a request from JavaScript, see the [AJAX Service with JSON and XML](../samples/ajax-service-with-json-and-xml-sample.md).</span></span>

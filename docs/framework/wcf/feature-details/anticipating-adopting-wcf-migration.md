---
title: "Preparazione all'adozione di Windows Communication Foundation: facilitazione dell'integrazione futura"
ms.date: 03/30/2017
ms.assetid: f49664d9-e9e0-425c-a259-93f0a569d01b
ms.openlocfilehash: b43f509bd49ebe89d7ed0be4c37b3ed179aaeb8c
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84576499"
---
# <a name="anticipating-adopting-the-windows-communication-foundation-easing-future-migration"></a><span data-ttu-id="0cf59-102">Preparazione all'adozione di Windows Communication Foundation: facilitazione dell'integrazione futura</span><span class="sxs-lookup"><span data-stu-id="0cf59-102">Anticipating Adopting the Windows Communication Foundation: Easing Future Migration</span></span>
<span data-ttu-id="0cf59-103">Per garantire una migrazione futura più semplice delle nuove applicazioni ASP.NET a WCF, seguire le indicazioni precedenti, nonché i consigli seguenti.</span><span class="sxs-lookup"><span data-stu-id="0cf59-103">To ensure an easier future migration of new ASP.NET applications to WCF, follow the preceding recommendations as well as the following recommendations.</span></span>  
  
## <a name="protocols"></a><span data-ttu-id="0cf59-104">Protocolli</span><span class="sxs-lookup"><span data-stu-id="0cf59-104">Protocols</span></span>  
 <span data-ttu-id="0cf59-105">Disattivare il supporto di ASP.NET 2.0 per SOAP 1.2:</span><span class="sxs-lookup"><span data-stu-id="0cf59-105">Disable ASP.NET 2.0’s support for SOAP 1.2:</span></span>  
  
```xml  
<configuration>  
     <system.web>  
      <webServices >  
          <protocols>  
           <remove name="HttpSoap12"/>  
          </protocols>
      </webServices>  
     </system.web>
</configuration>  
```  
  
 <span data-ttu-id="0cf59-106">Questa operazione è consigliabile perché WCF richiede che i messaggi conformi a diversi protocolli, come SOAP 1,1 e SOAP 1,2, vengano usati con endpoint diversi.</span><span class="sxs-lookup"><span data-stu-id="0cf59-106">Doing so is advisable because WCF requires messages conforming to different protocols, like SOAP 1.1 and SOAP 1.2, to go by using different endpoints.</span></span> <span data-ttu-id="0cf59-107">Se un servizio Web ASP.NET 2,0 è configurato per supportare sia SOAP 1,1 che SOAP 1,2, ovvero la configurazione predefinita, non è possibile eseguirne la migrazione in un singolo endpoint WCF con l'indirizzo originale che sarebbe certamente compatibile con tutti i client esistenti del servizio Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0cf59-107">If an ASP.NET 2.0 Web service is configured to support both SOAP 1.1 and SOAP 1.2, which is the default configuration, then it cannot be migrated forward to a single WCF endpoint at the original address that would be certainly be compatible with all of the ASP.NET Web service’s existing clients.</span></span> <span data-ttu-id="0cf59-108">La scelta di SOAP 1.2 anziché la versione 1.1 restringerà inoltre sensibilmente il numero di clienti del servizio.</span><span class="sxs-lookup"><span data-stu-id="0cf59-108">Also choosing SOAP 1.2 instead of 1.1 will more severely restrict the clientele of the service.</span></span>  
  
## <a name="service-development"></a><span data-ttu-id="0cf59-109">Sviluppo del servizio</span><span class="sxs-lookup"><span data-stu-id="0cf59-109">Service Development</span></span>  
 <span data-ttu-id="0cf59-110">WCF consente di definire i contratti di servizio applicando <xref:System.ServiceModel.ServiceContractAttribute> a interfacce o a classi.</span><span class="sxs-lookup"><span data-stu-id="0cf59-110">WCF allows you to define service contracts by applying the <xref:System.ServiceModel.ServiceContractAttribute> either to interfaces or to classes.</span></span> <span data-ttu-id="0cf59-111">È consigliabile applicare l'attributo a un'interfaccia piuttosto che a una classe perché in questo modo viene creata una definizione di contratto che può essere implementata in vari modi da un numero qualsiasi di classi.</span><span class="sxs-lookup"><span data-stu-id="0cf59-111">It is recommended to apply the attribute to an interface rather than to a class, because doing so creates a definition of a contract that can be variously implemented by any number of classes.</span></span> <span data-ttu-id="0cf59-112">ASP.NET supporta l'opzione relativa all'applicazione dell'attributo <xref:System.Web.Services.WebService> a interfacce e classi.</span><span class="sxs-lookup"><span data-stu-id="0cf59-112">ASP.NET 2.0 supports the option of applying the <xref:System.Web.Services.WebService> attribute to interfaces as well as classes.</span></span> <span data-ttu-id="0cf59-113">Tuttavia, come già menzionato, ASP.NET 2.0 presenta un difetto a causa del quale il parametro Namespace dell'attributo <xref:System.Web.Services.WebService> non produce alcun effetto quando l'attributo viene applicato a un'interfaccia anziché a una classe.</span><span class="sxs-lookup"><span data-stu-id="0cf59-113">However, as mentioned already, there is a defect in ASP.NET 2.0, by which the Namespace parameter of the <xref:System.Web.Services.WebService> attribute has no effect when that attribute is applied to an interface rather than a class.</span></span> <span data-ttu-id="0cf59-114">Poiché è generalmente consigliabile modificare lo spazio dei nomi di un servizio dal valore predefinito, `http://tempuri.org` , usando il parametro Namespace dell' <xref:System.Web.Services.WebService> attributo, è necessario continuare a definire i servizi Web ASP.NET applicando l' <xref:System.ServiceModel.ServiceContractAttribute> attributo alle interfacce o alle classi.</span><span class="sxs-lookup"><span data-stu-id="0cf59-114">Since it is generally advisable to modify the namespace of a service from the default value, `http://tempuri.org`, using the Namespace parameter of the <xref:System.Web.Services.WebService> attribute, one should continue defining ASP.NET Web Services by applying the <xref:System.ServiceModel.ServiceContractAttribute> attribute either to interfaces or to classes.</span></span>  
  
- <span data-ttu-id="0cf59-115">Usare meno codice possibile nei metodi mediante i quali vengono definite queste interfacce.</span><span class="sxs-lookup"><span data-stu-id="0cf59-115">Have as little code as possible in the methods by which those interfaces are defined.</span></span> <span data-ttu-id="0cf59-116">Fare in modo che deleghino il lavoro ad altre classi.</span><span class="sxs-lookup"><span data-stu-id="0cf59-116">Have them delegate their work to other classes.</span></span> <span data-ttu-id="0cf59-117">I nuovi tipi di servizio WCF possono quindi delegare il lavoro sostanziale a tali classi.</span><span class="sxs-lookup"><span data-stu-id="0cf59-117">New WCF service types could then also delegate their substantive work to those classes.</span></span>  
  
- <span data-ttu-id="0cf59-118">Fornire nomi espliciti per le operazioni di un servizio usando il parametro `MessageName` di <xref:System.Web.Services.WebMethodAttribute>.</span><span class="sxs-lookup"><span data-stu-id="0cf59-118">Provide explicit names for the operations of a service using the `MessageName` parameter of the <xref:System.Web.Services.WebMethodAttribute>.</span></span>  
  
    ```csharp  
    [WebMethod(MessageName="ExplicitName")]  
    string Echo(string input);  
    ```  
  
     <span data-ttu-id="0cf59-119">Questa operazione è importante, perché i nomi predefiniti per le operazioni in ASP.NET sono diversi da quelli predefiniti forniti da WCF.</span><span class="sxs-lookup"><span data-stu-id="0cf59-119">Doing so is important, because the default names for operations in ASP.NET are different from the default names supplied by WCF.</span></span> <span data-ttu-id="0cf59-120">Fornendo nomi espliciti non è necessario basarsi su quelli predefiniti.</span><span class="sxs-lookup"><span data-stu-id="0cf59-120">By providing explicit names, you avoid relying on the default ones.</span></span>  
  
- <span data-ttu-id="0cf59-121">Non implementano le operazioni del servizio Web ASP.NET con metodi polimorfici perché WCF non supporta l'implementazione di operazioni con metodi polimorfici.</span><span class="sxs-lookup"><span data-stu-id="0cf59-121">Do not implement ASP.NET Web service operations with polymorphic methods, because WCF does not support implementing operations with polymorphic methods.</span></span>  
  
- <span data-ttu-id="0cf59-122">Usare <xref:System.Web.Services.Protocols.SoapDocumentMethodAttribute> per fornire valori espliciti per le intestazioni HTTP SOAPAction mediante le quali le richieste HTTP verranno indirizzate ai metodi.</span><span class="sxs-lookup"><span data-stu-id="0cf59-122">Use the <xref:System.Web.Services.Protocols.SoapDocumentMethodAttribute> to provide explicit values for the SOAPAction HTTP headers by which HTTP requests will be routed to methods.</span></span>  
  
    ```csharp  
    [WebMethod]  
    [SoapDocumentMethod(RequestElementName="ExplicitAction")]  
    string Echo(string input);  
    ```  
  
     <span data-ttu-id="0cf59-123">L'adozione di questo approccio elude la necessità di basarsi sui valori SOAPAction predefiniti utilizzati da ASP.NET e WCF.</span><span class="sxs-lookup"><span data-stu-id="0cf59-123">Taking this approach will circumvent having to rely on the default SOAPAction values used by ASP.NET and WCF being the same.</span></span>  
  
- <span data-ttu-id="0cf59-124">Evitare l'uso di estensioni SOAP.</span><span class="sxs-lookup"><span data-stu-id="0cf59-124">Avoid using SOAP extensions.</span></span> <span data-ttu-id="0cf59-125">Se sono necessarie estensioni SOAP, determinare se lo scopo per il quale vengono considerate è una funzionalità già fornita da WCF.</span><span class="sxs-lookup"><span data-stu-id="0cf59-125">If SOAP extensions are required, then determine whether the purpose for which they are being considered is a feature that is already provided by WCF.</span></span> <span data-ttu-id="0cf59-126">In caso contrario, riconsiderare la scelta di non adottare immediatamente WCF.</span><span class="sxs-lookup"><span data-stu-id="0cf59-126">If that is indeed the case, then reconsider the choice to not adopt WCF right away.</span></span>  
  
## <a name="state-management"></a><span data-ttu-id="0cf59-127">Gestione dello stato</span><span class="sxs-lookup"><span data-stu-id="0cf59-127">State Management</span></span>  
 <span data-ttu-id="0cf59-128">Evitare di dover gestire lo stato nei servizi.</span><span class="sxs-lookup"><span data-stu-id="0cf59-128">Avoid having to maintain state in services.</span></span> <span data-ttu-id="0cf59-129">Non solo la gestione dello stato tende a compromettere la scalabilità di un'applicazione, ma i meccanismi di gestione dello stato di ASP.NET e WCF sono molto diversi, sebbene WCF supporti i meccanismi ASP.NET in modalità di compatibilità ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0cf59-129">Not only does maintaining state tend to compromise the scalability of an application, but the state management mechanisms of ASP.NET and WCF are very different, although WCF does support the ASP.NET mechanisms in ASP.NET compatibility mode.</span></span>  
  
## <a name="exception-handling"></a><span data-ttu-id="0cf59-130">Gestione delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="0cf59-130">Exception Handling</span></span>  
 <span data-ttu-id="0cf59-131">Nella progettazione delle strutture dei tipi di dati da inviare e ricevere da un servizio, progettare anche strutture che rappresentino i vari tipi di eccezioni che potrebbero verificarsi all'interno di un servizio che si desidera trasmettere a un client.</span><span class="sxs-lookup"><span data-stu-id="0cf59-131">In designing the structures of the data types to be sent and received by a service, also design structures to represent the various types of exceptions that might occur within a service that one might wish to convey to a client.</span></span>  
  
```csharp  
[Serializable]  
[XmlRoot(Namespace="ExplicitNamespace", IsNullable=true)]  
public partial class AnticipatedException
{
    private string anticipatedExceptionInformationField;  

    public string AnticipatedExceptionInformation
    {  
        get {
            return this.anticipatedExceptionInformationField;  
        }  
        set {  
            this.anticipatedExceptionInformationField = value;  
        }  
    }  
}  
```  
  
 <span data-ttu-id="0cf59-132">Impostare queste classi in modo che siano in grado di serializzarsi in XML:</span><span class="sxs-lookup"><span data-stu-id="0cf59-132">Give such classes the ability to serialize themselves to XML:</span></span>  
  
```csharp  
public XmlNode ToXML()  
{  
     XmlSerializer serializer = new XmlSerializer(  
      typeof(AnticipatedException));  
     MemoryStream memoryStream = new MemoryStream();  
     XmlTextWriter writer = new XmlTextWriter(  
     memoryStream, UnicodeEncoding.UTF8);  
     serializer.Serialize(writer, this);  
     XmlDocument document = new XmlDocument();  
     document.LoadXml(new string(  
     UnicodeEncoding.UTF8.GetChars(  
     memoryStream.GetBuffer())).Trim());  
    return document.DocumentElement;  
}  
```  
  
 <span data-ttu-id="0cf59-133">Le classi potranno quindi essere usate per fornire i dettagli per le istanze <xref:System.Web.Services.Protocols.SoapException> generate in modo esplicito:</span><span class="sxs-lookup"><span data-stu-id="0cf59-133">The classes can then be used to provide the details for explicitly thrown <xref:System.Web.Services.Protocols.SoapException> instances:</span></span>  
  
```csharp  
AnticipatedException exception = new AnticipatedException();  
exception.AnticipatedExceptionInformation = "…";  
throw new SoapException(  
     "Fault occurred",  
     SoapException.ClientFaultCode,  
     Context.Request.Url.AbsoluteUri,  
     exception.ToXML());  
```  
  
 <span data-ttu-id="0cf59-134">Queste classi di eccezioni saranno immediatamente riutilizzabili con la <xref:System.ServiceModel.FaultException%601> classe WCF per generare un nuovo`FaultException<AnticipatedException>(anticipatedException);`</span><span class="sxs-lookup"><span data-stu-id="0cf59-134">These exception classes will be readily reusable with the WCF <xref:System.ServiceModel.FaultException%601> class to throw a new `FaultException<AnticipatedException>(anticipatedException);`</span></span>  
  
## <a name="security"></a><span data-ttu-id="0cf59-135">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="0cf59-135">Security</span></span>  
 <span data-ttu-id="0cf59-136">Di seguito sono riportati alcuni consigli sulla protezione.</span><span class="sxs-lookup"><span data-stu-id="0cf59-136">The following are some security recommendations.</span></span>  
  
- <span data-ttu-id="0cf59-137">Evitare di utilizzare i profili ASP.NET 2,0, in quanto l'utilizzo di tali profili limita l'utilizzo della modalità di integrazione ASP.NET se è stata eseguita la migrazione del servizio in WCF.</span><span class="sxs-lookup"><span data-stu-id="0cf59-137">Avoid using ASP.NET 2.0 Profiles, as using them would restrict the use of ASP.NET Integration Mode if the service was migrated to WCF.</span></span>  
  
- <span data-ttu-id="0cf59-138">Evitare di utilizzare gli ACL per controllare l'accesso ai servizi, perché i servizi Web di ASP.NET supportano gli ACL tramite Internet Information Services (IIS), WCF non, perché i servizi Web ASP.NET dipendono da IIS per l'hosting e WCF non deve necessariamente essere ospitato in IIS.</span><span class="sxs-lookup"><span data-stu-id="0cf59-138">Avoid using ACLs to control access to services, as ASP.NET Web services supports ACLs using Internet Information Services (IIS), WCF does not—because ASP.NET Web services depend on IIS for hosting, and WCF does not necessarily have to be hosted in IIS.</span></span>  
  
- <span data-ttu-id="0cf59-139">Prendere in considerazione l'uso dei provider di ruoli di ASP.NET 2.0 per l'autorizzazione dell'accesso alle risorse di un servizio.</span><span class="sxs-lookup"><span data-stu-id="0cf59-139">Do consider using ASP.NET 2.0 Role Providers for authorizing access to the resources of a service.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0cf59-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0cf59-140">See also</span></span>

- [<span data-ttu-id="0cf59-141">Preparazione all'adozione di Windows Communication Foundation: facilitare l'integrazione futura</span><span class="sxs-lookup"><span data-stu-id="0cf59-141">Anticipating Adopting the Windows Communication Foundation: Easing Future Integration</span></span>](anticipating-adopting-the-wcf-easing-future-integration.md)

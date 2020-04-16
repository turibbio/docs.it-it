---
title: Indirizzamento
ms.date: 03/30/2017
ms.assetid: d438e6f2-d0f3-43aa-b259-b51b5bda2e64
ms.openlocfilehash: 55bb30ba3df80e41986b1337f8732dd8ad3231ff
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463762"
---
# <a name="addressing"></a><span data-ttu-id="cf1a0-102">Indirizzamento</span><span class="sxs-lookup"><span data-stu-id="cf1a0-102">Addressing</span></span>
<span data-ttu-id="cf1a0-103">Nell'esempio relativo all'Indirizzamento vengono illustrati i vari aspetti e le funzionalità degli indirizzi endpoint.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-103">The Addressing sample demonstrates various aspects and features of endpoint addresses.</span></span> <span data-ttu-id="cf1a0-104">L'esempio è basato sulla [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).</span><span class="sxs-lookup"><span data-stu-id="cf1a0-104">The sample is based on the [Getting Started](../../../../docs/framework/wcf/samples/getting-started-sample.md).</span></span> <span data-ttu-id="cf1a0-105">In questo esempio, il servizio è indipendente.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-105">In this sample the service is self-hosted.</span></span> <span data-ttu-id="cf1a0-106">Sia il client che il servizio sono applicazioni console.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-106">Both the service and the client are console applications.</span></span> <span data-ttu-id="cf1a0-107">Il servizio definisce più endpoint usando una combinazione di indirizzi endpoint relativi e assoluti.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-107">The service defines multiple endpoints using a combination of relative and absolute endpoint addresses.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="cf1a0-108">La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-108">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="cf1a0-109">Il file di configurazione del servizio specifica un indirizzo di base e quattro endpoint.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-109">The service configuration file specifies a base address and four endpoints.</span></span> <span data-ttu-id="cf1a0-110">L'indirizzo di base viene specificato usando l'elemento Add, in service/host/baseAddresses, come illustrato nell'esempio di configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-110">The base address is specified using the add element, under service/host/baseAddresses as demonstrated in the following sample configuration.</span></span>  
  
```xml  
<service name="Microsoft.ServiceModel.Samples.CalculatorService"  
         behaviorConfiguration="CalculatorServiceBehavior">  
  <host>  
    <baseAddresses>  
      <add baseAddress="http://localhost:8000/ServiceModelSamples/service" />  
    </baseAddresses>  
  </host>  
</service>  
```  
  
 <span data-ttu-id="cf1a0-111">La prima definizione dell'endpoint descritta nell'esempio di configurazione seguente specifica un indirizzo relativo, che indica che l'indirizzo endpoint è una combinazione dell'indirizzo di base e dell'indirizzo relativo, in base alle regole di composizione URI.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-111">The first endpoint definition shown in the following sample configuration specifies a relative address, which means the endpoint address is a combination of the base address and the relative address following the rules of URI composition.</span></span>  
  
```xml
<!-- Empty relative address specified:   
     use the base address provided by the host. -->  
<!-- The endpoint address is  
     http://localhost:8000/ServiceModelSamples/service. -->  
<endpoint address=""  
          binding="wsHttpBinding"  
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
 <span data-ttu-id="cf1a0-112">In questo caso, l'indirizzo relativo è vuoto (""), pertanto l'indirizzo endpoint corrisponde all'indirizzo di base.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-112">In this case, the relative address is empty (""), so the endpoint address is the same as the base address.</span></span> <span data-ttu-id="cf1a0-113">L'indirizzo endpoint `http://localhost:8000/servicemodelsamples/service`effettivo è .</span><span class="sxs-lookup"><span data-stu-id="cf1a0-113">The actual endpoint address is `http://localhost:8000/servicemodelsamples/service`.</span></span>
  
 <span data-ttu-id="cf1a0-114">Anche la seconda definizione dell'endpoint specifica un indirizzo relativo, come illustrato nell'esempio di configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-114">The second endpoint definition also specifies a relative address, as shown in the following sample configuration.</span></span>  
  
```xml  
<!-- The relative address specified: use the base address -->  
<!-- provided by the host + path. The endpoint address is -->  
<!-- http://localhost:8000/servicemodelsamples/service/test. -->  
<endpoint address="/test"  
          binding="wsHttpBinding"  
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
 <span data-ttu-id="cf1a0-115">L'indirizzo relativo, "test", viene accodato all'indirizzo di base.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-115">The relative address, "test", is appended to the base address.</span></span> <span data-ttu-id="cf1a0-116">L'indirizzo endpoint `http://localhost:8000/servicemodelsamples/service/test`effettivo è .</span><span class="sxs-lookup"><span data-stu-id="cf1a0-116">The actual endpoint address is `http://localhost:8000/servicemodelsamples/service/test`.</span></span>
  
 <span data-ttu-id="cf1a0-117">La terza definizione dell'endpoint specifica un indirizzo assoluto, come illustrato nell'esempio di configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-117">The third endpoint definition specifies an absolute address, as shown in the following sample configuration.</span></span>  
  
```xml  
<endpoint address="http://localhost:8001/hello/servicemodelsamples"  
          binding="wsHttpBinding"  
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
 <span data-ttu-id="cf1a0-118">L'indirizzo di base non ha alcun ruolo nell'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-118">The base address plays no role in the address.</span></span> <span data-ttu-id="cf1a0-119">L'indirizzo endpoint `http://localhost:8001/hello/servicemodelsamples`effettivo è .</span><span class="sxs-lookup"><span data-stu-id="cf1a0-119">The actual endpoint address is `http://localhost:8001/hello/servicemodelsamples`.</span></span>
  
 <span data-ttu-id="cf1a0-120">Il quarto indirizzo endpoint specifica un indirizzo assoluto e un trasporto diverso, cioè TCP.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-120">The fourth endpoint address specifies an absolute address and a different transport—TCP.</span></span> <span data-ttu-id="cf1a0-121">L'indirizzo di base non ha alcun ruolo nell'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-121">The base address plays no role in the address.</span></span> <span data-ttu-id="cf1a0-122">L'indirizzo endpoint `net.tcp://localhost:9000/servicemodelsamples/service`effettivo è .</span><span class="sxs-lookup"><span data-stu-id="cf1a0-122">The actual endpoint address is `net.tcp://localhost:9000/servicemodelsamples/service`.</span></span>
  
```xml  
<!-- The absolute address specified, different transport: -->  
<!-- use the specified address, and ignore the base address. -->  
<!-- The endpoint address is -->  
<!-- net.tcp://localhost:9000/servicemodelsamples/service. -->  
<endpoint address=  
          "net.tcp://localhost:9000/servicemodelsamples/service"  
          binding="netTcpBinding"  
          contract="Microsoft.ServiceModel.Samples.ICalculator" />  
```  
  
 <span data-ttu-id="cf1a0-123">Il client accede a uno dei quattro endpoint del servizio, ma tutti e quattro vengono definiti nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-123">The client accesses just one of the four service endpoints, but all four are defined in its configuration file.</span></span> <span data-ttu-id="cf1a0-124">Il client seleziona un endpoint quando crea l'oggetto `CalculatorProxy`.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-124">The client selects an endpoint when it creates the `CalculatorProxy` object.</span></span> <span data-ttu-id="cf1a0-125">Modificando il nome della configurazione da `CalculatorEndpoint1` a `CalculatorEndpoint4`, è possibile verificare il funzionamento di ognuno degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-125">By changing the configuration name from `CalculatorEndpoint1` through `CalculatorEndpoint4`, you can exercise each of the endpoints.</span></span>  
  
 <span data-ttu-id="cf1a0-126">Quando si esegue l'esempio, il servizio enumera l'indirizzo, il nome dell'associazione e il nome del contratto per ognuno degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-126">When you run the sample, the service enumerates the address, binding name and contract name for each of its endpoints.</span></span> <span data-ttu-id="cf1a0-127">Per ServiceHost, l'endpoint di scambio di metadati (MEX) è solo un altro endpoint, per cui viene incluso nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-127">The metadata exchange (MEX) endpoint is just another endpoint from the ServiceHost's perspective so it shows up in the list.</span></span>  
  
```console  
Service endpoints:  
Endpoint - address:  http://localhost:8000/ServiceModelSamples/service  
           binding:  WSHttpBinding  
           contract: ICalculator  
Endpoint - address:  http://localhost:8000/ServiceModelSamples/service/test  
           binding:  WSHttpBinding  
           contract: ICalculator  
Endpoint - address:  http://localhost:8001/hello/servicemodelsamples  
           binding:  WSHttpBinding  
           contract: ICalculator  
Endpoint - address:  net.tcp://localhost:9000/servicemodelsamples/service  
           binding:  NetTcpBinding  
           contract: ICalculator  
Endpoint - address:  http://localhost:8000/ServiceModelSamples/service/mex  
           binding:  MetadataExchangeHttpBinding  
           contract: IMetadataExchange  
  
The service is ready.  
Press <ENTER> to terminate service.  
```  
  
 <span data-ttu-id="cf1a0-128">Quando si esegue il client, le richieste e le risposte dell'operazione vengono visualizzate nelle finestre della console client e del servizio.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-128">When you run the client, the operation requests and responses are displayed in both the service and client console windows.</span></span> <span data-ttu-id="cf1a0-129">Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-129">Press ENTER in each console window to shut down the service and client.</span></span>  
  
```console  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="cf1a0-130">Per impostare, compilare ed eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="cf1a0-130">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="cf1a0-131">Assicurarsi di aver eseguito la procedura di [installazione una tantera per Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cf1a0-131">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="cf1a0-132">Per compilare l'edizione in C# o Visual Basic .NET della soluzione, seguire le istruzioni in [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cf1a0-132">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="cf1a0-133">Per eseguire l'esempio in una configurazione su un singolo o più computer, seguire le istruzioni in Esecuzione di [Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cf1a0-133">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/running-the-samples.md).</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="cf1a0-134">Se si usa Svcutil.exe per rigenerare la configurazione di questo esempio, assicurarsi di modificare il nome dell'endpoint nella configurazione client in modo che corrisponda al codice client.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-134">If you use Svcutil.exe to regenerate the configuration for this sample, be sure to modify the endpoint name in the client configuration to match the client code.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="cf1a0-135">È possibile che gli esempi siano già installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-135">The samples may already be installed on your machine.</span></span> <span data-ttu-id="cf1a0-136">Verificare la directory seguente (impostazione predefinita) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-136">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="cf1a0-137">Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) e Windows Workflow Foundation (WF) Esempi per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti gli esempi e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="cf1a0-137">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="cf1a0-138">Questo esempio si trova nella directory seguente.</span><span class="sxs-lookup"><span data-stu-id="cf1a0-138">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Addressing`  

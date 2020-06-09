---
title: Trasporto dell'associazione personalizzata e codifica
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6c0b353d-79ee-4e61-b348-be49ad0e9a16
ms.openlocfilehash: 3b3a0f1b52afce495ca41a426ebc9e57314d8254
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84592528"
---
# <a name="custom-binding-transport-and-encoding"></a><span data-ttu-id="d568f-102">Trasporto dell'associazione personalizzata e codifica</span><span class="sxs-lookup"><span data-stu-id="d568f-102">Custom Binding Transport and Encoding</span></span>
<span data-ttu-id="d568f-103">Un'associazione personalizzata viene definita da un elenco ordinato di elementi di associazione discreti.</span><span class="sxs-lookup"><span data-stu-id="d568f-103">A custom binding is defined by an ordered list of discrete binding elements.</span></span> <span data-ttu-id="d568f-104">Questo esempio illustra come configurare un'associazione personalizzata con vari elementi di codifica di trasporto e messaggio.</span><span class="sxs-lookup"><span data-stu-id="d568f-104">This sample demonstrates how to configure a custom binding with various transport and message encoding elements.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="d568f-105">La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="d568f-105">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="d568f-106">Questo esempio è basato sull' [host indipendente](self-host.md)ed è stato modificato per configurare tre endpoint per supportare i trasporti HTTP, TCP e NamedPipe con binding personalizzati.</span><span class="sxs-lookup"><span data-stu-id="d568f-106">This sample is based on the [Self-Host](self-host.md), and has been modified to configure three endpoints to support HTTP, TCP, and NamedPipe transports with custom bindings.</span></span> <span data-ttu-id="d568f-107">La configurazione del client viene modificata in modo simile e il codice del client modificato per comunicare con ognuno dei tre endpoint.</span><span class="sxs-lookup"><span data-stu-id="d568f-107">The client configuration was similarly modified, and the client code changed to communicate with each of the three endpoints.</span></span>  
  
 <span data-ttu-id="d568f-108">L'esempio illustra come configurare un'associazione personalizzata che supporta una particolare codifica di trasporto e messaggio.</span><span class="sxs-lookup"><span data-stu-id="d568f-108">The sample demonstrates a how to configure a custom binding that supports a particular transport and message encoding.</span></span> <span data-ttu-id="d568f-109">Ciò viene effettuato configurando un trasporto e un messaggio che codificano per l'elemento `binding`.</span><span class="sxs-lookup"><span data-stu-id="d568f-109">This is accomplished by configuring a transport and a message encoding for the `binding` element.</span></span> <span data-ttu-id="d568f-110">L'ordinamento degli elementi di associazione è importante per la definizione di un'associazione personalizzata, perché ogni rappresenta un livello nello stack dei canali (vedere [binding personalizzati](../extending/custom-bindings.md)).</span><span class="sxs-lookup"><span data-stu-id="d568f-110">The ordering of binding elements is important in defining a custom binding, because each represents a layer in the channel stack (see [Custom Bindings](../extending/custom-bindings.md)).</span></span> <span data-ttu-id="d568f-111">Questo esempio configura tre associazioni personalizzate: un trasporto HTTP con codifica di testo, un trasporto TCP con codifica di testo e un trasporto di NamedPipe con codifica binaria.</span><span class="sxs-lookup"><span data-stu-id="d568f-111">This sample configures three custom bindings: an HTTP transport with text encoding, a TCP transport with text encoding, and a NamedPipe transport with a binary encoding.</span></span>  
  
 <span data-ttu-id="d568f-112">La configurazione del servizio definisce l'associazione personalizzata nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="d568f-112">The service configuration defines the custom bindings as follows:</span></span>  
  
```xml  
<bindings>  
    <customBinding>  
        <binding name="HttpBinding" >  
            <textMessageEncoding
                messageVersion="Soap12Addressing10"/>  
            <httpTransport />  
        </binding>  
        <binding name="TcpBinding" >  
            <textMessageEncoding />  
            <tcpTransport />  
        </binding>  
        <binding name="NamedPipeBinding" >  
            <binaryMessageEncoding />  
            <namedPipeTransport />  
        </binding>  
    </customBinding>  
</bindings>  
```  
  
 <span data-ttu-id="d568f-113">Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client e del servizio.</span><span class="sxs-lookup"><span data-stu-id="d568f-113">When you run the sample, the operation requests and responses are displayed in both the service and client console window.</span></span> <span data-ttu-id="d568f-114">Il client comunica con ognuno dei tre endpoint, accedendo prima a HTTP, quindi a TCP e finalmente a NamedPipe.</span><span class="sxs-lookup"><span data-stu-id="d568f-114">The client communicates with each of the three endpoints, accessing first HTTP, then TCP, and finally NamedPipe.</span></span> <span data-ttu-id="d568f-115">Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.</span><span class="sxs-lookup"><span data-stu-id="d568f-115">Press ENTER in each console window to shut down the service and client.</span></span>  
  
 <span data-ttu-id="d568f-116">L'associazione `namedPipeTransport` non supporta operazioni da computer a computer.</span><span class="sxs-lookup"><span data-stu-id="d568f-116">The `namedPipeTransport` binding does not support machine-to-machine operations.</span></span> <span data-ttu-id="d568f-117">Viene utilizzata solo per la comunicazione sullo stesso computer.</span><span class="sxs-lookup"><span data-stu-id="d568f-117">It is used only for communication on the same machine.</span></span> <span data-ttu-id="d568f-118">Pertanto, quando si esegue l'esempio in un scenario a più computer, impostare come commento le righe seguenti nel file contenente il codice client:</span><span class="sxs-lookup"><span data-stu-id="d568f-118">Therefore, when running the sample in a cross-machine scenario, comment out the following lines in the client code file:</span></span>  
  
```csharp  
CalculatorClient client = new CalculatorClient("default");  
Console.WriteLine("Communicate with named pipe endpoint.");  
// Call operations.  
DoCalculations(client);  
//Closing the client gracefully closes the connection and cleans up resources  
client.Close();  
```  
  
```vb  
Dim client As New CalculatorClient("default")  
Console.WriteLine("Communicate with named pipe endpoint.")  
' call operations  
DoCalculations(client)  
'Closing the client gracefully closes the connection and cleans up resources  
client.Close()  
```  
  
> [!NOTE]
> <span data-ttu-id="d568f-119">Se si usa Svcutil.exe per rigenerare la configurazione di questo esempio, assicurarsi di modificare il nome dell'endpoint nella configurazione client in modo che corrisponda al codice client.</span><span class="sxs-lookup"><span data-stu-id="d568f-119">If you use Svcutil.exe to regenerate the configuration for this sample, be sure to modify the endpoint name in the client configuration to match the client code.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="d568f-120">Per impostare, compilare ed eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="d568f-120">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="d568f-121">Assicurarsi di avere eseguito la [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d568f-121">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="d568f-122">Per compilare l'edizione C#, C++ o Visual Basic .NET della soluzione, seguire le istruzioni in [compilazione degli esempi di Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d568f-122">To build the C#, C++, or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="d568f-123">Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [esecuzione degli esempi di Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d568f-123">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="d568f-124">È possibile che gli esempi siano già installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="d568f-124">The samples may already be installed on your machine.</span></span> <span data-ttu-id="d568f-125">Verificare la directory seguente (impostazione predefinita) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="d568f-125">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="d568f-126">Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) ed [!INCLUDE[wf1](../../../../includes/wf1-md.md)] esempi.</span><span class="sxs-lookup"><span data-stu-id="d568f-126">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="d568f-127">Questo esempio si trova nella directory seguente.</span><span class="sxs-lookup"><span data-stu-id="d568f-127">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Custom\Transport`  

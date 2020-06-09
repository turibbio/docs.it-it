---
title: CustomChannelsTester
ms.date: 03/30/2017
ms.assetid: ee1fa307-98b1-4647-8860-2e9217ba6082
ms.openlocfilehash: 9123167e0f97592592765f7b4a4aa768064fc173
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596604"
---
# <a name="customchannelstester"></a><span data-ttu-id="0c386-102">CustomChannelsTester</span><span class="sxs-lookup"><span data-stu-id="0c386-102">CustomChannelsTester</span></span>
<span data-ttu-id="0c386-103">`CustomChannelsTester` è uno strumento che può essere usato per testare le implementazioni del canale personalizzato in un set di contratti di servizio predefiniti.</span><span class="sxs-lookup"><span data-stu-id="0c386-103">The `CustomChannelsTester` is a tool that you can use to test your custom channel implementations against a set of predefined service contracts.</span></span> <span data-ttu-id="0c386-104">È possibile selezionare il set di contratti di servizio e passarlo allo strumento usando un file XML.</span><span class="sxs-lookup"><span data-stu-id="0c386-104">You can select the set of service contracts and pass it to the tool using an XML file.</span></span> <span data-ttu-id="0c386-105">Lo strumento genera quindi il servizio e il client che esercitano le implementazioni del canale personalizzate durante lo scambio di messaggi.</span><span class="sxs-lookup"><span data-stu-id="0c386-105">The tool then generates the service and client that exercises your custom channel implementations during message exchange.</span></span>  
  
### <a name="to-build-the-tool"></a><span data-ttu-id="0c386-106">Per compilare lo strumento</span><span class="sxs-lookup"><span data-stu-id="0c386-106">To build the tool</span></span>  
  
1. <span data-ttu-id="0c386-107">Per compilare la soluzione, seguire le istruzioni riportate in [compilazione degli esempi di Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0c386-107">To build the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
2. <span data-ttu-id="0c386-108">La compilazione della soluzione genera tre file: CustomChannelsTester.exe, TestSpec.xml e SampleRun.cmd.</span><span class="sxs-lookup"><span data-stu-id="0c386-108">Building the solution generates three files: CustomChannelsTester.exe, TestSpec.xml and SampleRun.cmd.</span></span> <span data-ttu-id="0c386-109">Il file SampleRun. cmd include una riga di comando di esempio che illustra come usare questo strumento per testare l'esempio [Transport: UDP](transport-udp.md) .</span><span class="sxs-lookup"><span data-stu-id="0c386-109">The file SampleRun.cmd has a sample command line that shows how to use this tool to test the [Transport: UDP](transport-udp.md) sample.</span></span>  
  
### <a name="to-run-the-tool"></a><span data-ttu-id="0c386-110">Per eseguire lo strumento</span><span class="sxs-lookup"><span data-stu-id="0c386-110">To run the tool</span></span>  
  
- <span data-ttu-id="0c386-111">Al prompt dei comandi digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0c386-111">At the command prompt type the following command:</span></span>  
  
    ```console  
    CustomChannelsTester.exe /binding:YourCustomBindngName /dll:TheAssemblyWhereThisTypeisDefined /testspec:XmlFileNameWhichContainsTestOptions  
    ```  
  
     <span data-ttu-id="0c386-112">L'utilizzo dell'opzione `/binding` è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="0c386-112">Using the `/binding` option is required.</span></span>  
  
     <span data-ttu-id="0c386-113">`/dll`è obbligatorio se "binding" non è un'associazione fornita dal sistema fornita da Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="0c386-113">`/dll` is required if "binding" is not a system-provided binding provided by Windows Communication Foundation (WCF).</span></span>  
  
     <span data-ttu-id="0c386-114">`/testspec` è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="0c386-114">`/testspec` is optional.</span></span>  
  
     <span data-ttu-id="0c386-115">Crea server e client basati sulle specifiche del test e sull'associazione.</span><span class="sxs-lookup"><span data-stu-id="0c386-115">This creates server and clients based on the test specifications and the binding.</span></span>  
  
     <span data-ttu-id="0c386-116">Esegue il client e il server e restituisce i risultati.</span><span class="sxs-lookup"><span data-stu-id="0c386-116">Executes the client and server and returns the results.</span></span>  
  
     <span data-ttu-id="0c386-117">Di seguito è riportato l'esempio XML della descrizione delle specifiche del test (testspec.xml):</span><span class="sxs-lookup"><span data-stu-id="0c386-117">The following is the sample XML for the description of the test specifications (testspec.xml):</span></span>  
  
    ```xml  
    <TestSpec xmlns="http://WCF/TestSpec" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" >  
    <ServiceContract>  
    <!-- Test a contract which has oneway / twoway operations. If you set ExpandAll = true, both types of contracts are tested -->    <IsOneWay ExpandAll="true">true</IsOneWay>  
    <!-- Test a contract with Asynchronous / Synchronous Operations-->  
        <IsAsync>false</IsAsync>
    <!-- Test a sessionful / sessionless contract-->
        <IsSession ExpandAll="true">true</IsSession>  
    <!-- If the Service Contract includes a CallBack Contract-->
        <IsCallBack ExpandAll="true">true</IsCallBack>  
    </ServiceContract>  
    <TestDetails>  
    <!-- Name of the machine that runs the server - required if you want to run the test crossmachine-->  
        <ServerName>ReplaceThisWithTheServerMachineName</ServerName>  
    <!-- Port Number - Optional-->  
        <Port>8000</Port>  
    <!--URI for the callBack address for the client. The client will receive the messages from the server on this address in case of a CallBack Contract-->  
        <ClientCallBackAddress/>
    <!-- Duration (in sec) after the server has started, it times out - optional(default = 300sec) -->  
        <ServerTimeout>300</ServerTimeout>  
    <!-- Duration (in sec) before the Client initializes -optional(default = 60sec) -->  
        <ClientTimeout>60</ClientTimeout>  
    <!-- Number of clients for each service - optional(default = 1) -->  
        <NumberOfClients>1</NumberOfClients>  
    <!-- Number of messages each client sends to the service - optional(default = 1) -->  
        <MessagesPerClient>1</MessagesPerClient>  
    </TestDetails>  
    </TestSpec>  
    ```  

---
title: Integrazione di componenti transazionali di Enterprise Services
ms.date: 03/30/2017
ms.assetid: 05dab277-b8b2-48cf-b40c-826be128b175
ms.openlocfilehash: 1c4fabfadb113c79b216fa10ff80b551ba0f9716
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596851"
---
# <a name="integrating-enterprise-services-transactional-components"></a><span data-ttu-id="1b38b-102">Integrazione di componenti transazionali di Enterprise Services</span><span class="sxs-lookup"><span data-stu-id="1b38b-102">Integrating Enterprise Services Transactional Components</span></span>

<span data-ttu-id="1b38b-103">Windows Communication Foundation (WCF) fornisce un meccanismo automatico per l'integrazione con Enterprise Services. vedere [integrazione con applicazioni com+](integrating-with-com-plus-applications.md).</span><span class="sxs-lookup"><span data-stu-id="1b38b-103">Windows Communication Foundation (WCF) provides an automatic mechanism for integrating with Enterprise Services (see [Integrating with COM+ Applications](integrating-with-com-plus-applications.md)).</span></span> <span data-ttu-id="1b38b-104">Può tuttavia essere necessario disporre della flessibilità di sviluppare servizi che utilizzano internamente componenti transazionali ospitati all'interno di Enterprise Services.</span><span class="sxs-lookup"><span data-stu-id="1b38b-104">However, you may want the flexibility to develop services that internally use transactional components hosted within Enterprise Services.</span></span> <span data-ttu-id="1b38b-105">Poiché la funzionalità transazioni WCF è basata sull' <xref:System.Transactions> infrastruttura di, il processo di integrazione di Enterprise Services con WCF è identico a quello per la specifica dell'interoperabilità tra <xref:System.Transactions> e Enterprise Services, come descritto in [interoperabilità con le transazioni di Enterprise Services e com+](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.0/ms229974(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="1b38b-105">Because the WCF Transactions feature is built on the <xref:System.Transactions> infrastructure, the process for integrating Enterprise Services with WCF is identical to that for specifying interoperability between <xref:System.Transactions> and Enterprise Services, as outlined in [Interoperability with Enterprise Services and COM+ Transactions](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.0/ms229974(v=vs.85)).</span></span>  
  
 <span data-ttu-id="1b38b-106">Per fornire il livello desiderato di interoperabilità tra la transazione propagata in ingresso e la transazione in contesto COM+, l'implementazione del servizio deve creare un'istanza della classe <xref:System.Transactions.TransactionScope> e deve utilizzare il valore appropriato ricavato dall'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption>.</span><span class="sxs-lookup"><span data-stu-id="1b38b-106">To provide the desired level of interoperability between the incoming flowed transaction and the COM+ context transaction, the service implementation must create a <xref:System.Transactions.TransactionScope> instance and use the appropriate value from the <xref:System.Transactions.EnterpriseServicesInteropOption> enumeration.</span></span>  
  
## <a name="integrating-enterprise-services-with-a-service-operation"></a><span data-ttu-id="1b38b-107">Integrazione di Enterprise Services con un'operazione del servizio</span><span class="sxs-lookup"><span data-stu-id="1b38b-107">Integrating Enterprise Services with a Service Operation</span></span>  
 <span data-ttu-id="1b38b-108">Nel codice seguente viene illustrata un'operazione, con propagazione transazionale Allowed, che crea una classe <xref:System.Transactions.TransactionScope> con l'opzione <xref:System.Transactions.EnterpriseServicesInteropOption.Full>.</span><span class="sxs-lookup"><span data-stu-id="1b38b-108">The following code demonstrates an operation, with Allowed transaction flow, that creates a <xref:System.Transactions.TransactionScope> with the <xref:System.Transactions.EnterpriseServicesInteropOption.Full> option.</span></span> <span data-ttu-id="1b38b-109">In questo scenario vengono applicate le condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b38b-109">The following conditions apply in this scenario:</span></span>  
  
- <span data-ttu-id="1b38b-110">Se il client propaga una transazione, l'operazione, inclusa la chiamata al componente Enterprise Services, viene eseguita all'interno dell'ambito di tale transazione.</span><span class="sxs-lookup"><span data-stu-id="1b38b-110">If the client flows a transaction, the operation, including the call to the Enterprise Services component, is executed within the scope of that transaction.</span></span> <span data-ttu-id="1b38b-111">L'utilizzo di <xref:System.Transactions.EnterpriseServicesInteropOption.Full> garantisce la sincronizzazione della transazione con il contesto <xref:System.EnterpriseServices>, il che significa che la transazione di ambiente per <xref:System.Transactions> e <xref:System.EnterpriseServices> è la stessa.</span><span class="sxs-lookup"><span data-stu-id="1b38b-111">Using <xref:System.Transactions.EnterpriseServicesInteropOption.Full> ensures that the transaction is synchronized with the <xref:System.EnterpriseServices> context, which means that the ambient transaction for <xref:System.Transactions> and the <xref:System.EnterpriseServices> is the same.</span></span>  
  
- <span data-ttu-id="1b38b-112">Se il client non propaga una transazione, l'impostazione di <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> su `true` crea un nuovo ambito di transazione per l'operazione.</span><span class="sxs-lookup"><span data-stu-id="1b38b-112">If the client does not flow a transaction, setting <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> to `true` creates a new transaction scope for the operation.</span></span> <span data-ttu-id="1b38b-113">Analogamente, l'utilizzo di <xref:System.Transactions.EnterpriseServicesInteropOption.Full> garantisce che la transazione dell'operazione sia la stessa transazione utilizzata all'interno del contesto del componente <xref:System.EnterpriseServices>.</span><span class="sxs-lookup"><span data-stu-id="1b38b-113">Similarly, using <xref:System.Transactions.EnterpriseServicesInteropOption.Full> ensures that the operation’s transaction is the same as the transaction used inside the <xref:System.EnterpriseServices> component's context.</span></span>  
  
 <span data-ttu-id="1b38b-114">Eventuali chiamate aggiuntive al metodo avvengono anch'esse nell'ambito della stessa transazione dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="1b38b-114">Any additional method calls also occur within the scope of the same operation’s transaction.</span></span>  
  
```csharp
[ServiceContract()]  
public interface ICustomerServiceContract  
{  
   [OperationContract]  
   [TransactionFlow(TransactionFlowOption.Allowed)]  
   void UpdateCustomerNameOperation(int customerID, string newCustomerName);  
}  
  
[ServiceBehavior(TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable)]  
public class CustomerService : ICustomerServiceContract  
{  
   [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
   public void UpdateCustomerNameOperation(int customerID, string newCustomerName)  
   {  
   // Create a transaction scope with full ES interop  
      using (TransactionScope ts = new TransactionScope(  
                     TransactionScopeOption.Required,  
                     new TransactionOptions(),  
                     EnterpriseServicesInteropOption.Full))  
      {  
         // Create an Enterprise Services component  
         // Call UpdateCustomer method on an Enterprise Services
         // component
  
         // Call UpdateOtherCustomerData method on an Enterprise
         // Services component
         ts.Complete();  
      }  
  
      // Do UpdateAdditionalData on an non-Enterprise Services  
      // component  
   }  
}  
```  
  
 <span data-ttu-id="1b38b-115">Se non è necessaria alcuna sincronizzazione tra la transazione corrente di un'operazione e le chiamate ai componenti Enterprise Services transazionali, utilizzare l'opzione <xref:System.Transactions.EnterpriseServicesInteropOption.None> quando si crea l'istanza di <xref:System.Transactions.TransactionScope>.</span><span class="sxs-lookup"><span data-stu-id="1b38b-115">If no synchronization is required between an operation’s current transaction and calls to transactional Enterprise Services components, then use the <xref:System.Transactions.EnterpriseServicesInteropOption.None> option when instantiating the <xref:System.Transactions.TransactionScope> instance.</span></span>  
  
## <a name="integrating-enterprise-services-with-a-client"></a><span data-ttu-id="1b38b-116">Integrazione di Enterprise Services con un client</span><span class="sxs-lookup"><span data-stu-id="1b38b-116">Integrating Enterprise Services with a Client</span></span>  
 <span data-ttu-id="1b38b-117">Nell'esempio seguente viene illustrato il codice client utilizzando un'istanza della classe <xref:System.Transactions.TransactionScope> con l'impostazione <xref:System.Transactions.EnterpriseServicesInteropOption.Full></span><span class="sxs-lookup"><span data-stu-id="1b38b-117">The following code demonstrates client code using a <xref:System.Transactions.TransactionScope> instance with the <xref:System.Transactions.EnterpriseServicesInteropOption.Full> setting.</span></span> <span data-ttu-id="1b38b-118">In questo scenario, le chiamate alle operazioni del servizio che supportano la propagazione transazionale avvengono nell'ambito della stessa transazione delle chiamate ai componenti Enterprise Services.</span><span class="sxs-lookup"><span data-stu-id="1b38b-118">In this scenario, calls to service operations that support transaction flow occur within the scope of the same transaction as the calls to Enterprise Services components.</span></span>  
  
```csharp
static void Main()  
{  
    // Create a client  
    CalculatorClient client = new CalculatorClient();  
  
    // Create a transaction scope with full ES interop  
    using (TransactionScope ts = new TransactionScope(  
          TransactionScopeOption.Required,  
          new TransactionOptions(),  
          EnterpriseServicesInteropOption.Full))  
    {  
        // Call Add calculator service operation  
  
        // Create an Enterprise Services component  
  
        // Call UpdateCustomer method on an Enterprise Services
        // component
  
        ts.Complete();  
    }  
  
    // Closing the client gracefully closes the connection and
    // cleans up resources  
    client.Close();  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="1b38b-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1b38b-119">See also</span></span>

- [<span data-ttu-id="1b38b-120">Integrazione con applicazioni COM+</span><span class="sxs-lookup"><span data-stu-id="1b38b-120">Integrating with COM+ Applications</span></span>](integrating-with-com-plus-applications.md)
- [<span data-ttu-id="1b38b-121">Integrazione con applicazioni COM</span><span class="sxs-lookup"><span data-stu-id="1b38b-121">Integrating with COM Applications</span></span>](integrating-with-com-applications.md)

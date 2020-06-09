---
title: Esempio della guida introduttiva
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- basic samples [WCF], getting started
ms.assetid: 967a3d94-0261-49ff-b85a-20bb07f1af20
ms.openlocfilehash: fc4a7e9acb15f77140732638b2982dd4a9dae9ce
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84575186"
---
# <a name="getting-started-sample"></a>Esempio della guida introduttiva

Nell'esempio Introduzione viene illustrato come implementare un servizio tipico e un client tipico utilizzando Windows Communication Foundation (WCF). Questo esempio è la base per tutti gli altri esempi di tecnologia di base.

> [!NOTE]
> La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.

> [!IMPORTANT]
> È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente (impostazione predefinita) prima di continuare.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) ed [!INCLUDE[wf1](../../../../includes/wf1-md.md)] esempi. Questo esempio si trova nella directory seguente.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\GettingStarted\GettingStarted`

Il servizio descrive le operazioni che esegue in un contratto di servizio che espone pubblicamente come metadati. Il servizio contiene inoltre il codice per implementare le operazioni.

Il client contiene una definizione del contratto di servizio e una classe proxy per accedere al servizio. Il codice proxy viene generato dai metadati del servizio mediante lo [strumento ServiceModel Metadata Utility Tool (Svcutil. exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md).

In Windows Vista, il servizio è ospitato nel servizio Attivazione Windows (WAS). In Windows XP e Windows Server 2003, è ospitato da Internet Information Services (IIS) e ASP.NET. Ospitare un servizio in IIS o WAS consente l'attivazione automatica del servizio quando si esegue l'accesso per la prima volta.

> [!NOTE]
> Se si preferisce iniziare a usare un esempio che ospita il servizio in un'applicazione console anziché IIS, vedere l'esempio [self-host](self-host.md) .

Il servizio e il client specificano i dettagli di accesso nelle impostazioni del file di configurazione, dettagli che forniscono flessibilità al momento della distribuzione. Questi dettagli comprendono una definizione dell'endpoint che specifica un indirizzo, un'associazione e un contratto. L'associazione specifica i dettagli di trasporto e di sicurezza per la modalità di accesso al servizio.

Il servizio configura un comportamento in fase di esecuzione per pubblicare i metadati.

Il servizio implementa un contratto che definisce un modello di comunicazione richiesta/risposta. Il contratto è definito dall'interfaccia `ICalculator` che espone operazioni matematiche (somma, sottrazione, moltiplicazione e divisione). Il client esegue richieste a un'operazione matematica specificata e il servizio risponde fornendo il risultato. Il servizio implementa un contratto `ICalculator` definito nel codice seguente.

```vb
' Define a service contract.
    <ServiceContract(Namespace:="http://Microsoft.Samples.GettingStarted")>
     Public Interface ICalculator
        <OperationContract()>
        Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double
        <OperationContract()>
        Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double
        <OperationContract()>
        Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double
        <OperationContract()>
        Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double
    End Interface
```

```csharp
// Define a service contract.
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    [OperationContract]
    double Subtract(double n1, double n2);
    [OperationContract]
    double Multiply(double n1, double n2);
    [OperationContract]
    double Divide(double n1, double n2);
}
```

L'implementazione del servizio calcola e restituisce il risultato appropriato, come illustrato nell'esempio di codice seguente.

```vb
' Service class which implements the service contract.
Public Class CalculatorService
Implements ICalculator
Public Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Add
Return n1 + n2
End Function

Public Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Subtract
Return n1 - n2
End Function

Public Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Multiply
Return n1 * n2
End Function

Public Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Divide
Return n1 / n2
End Function
End Class
```

```csharp
// Service class that implements the service contract.
public class CalculatorService : ICalculator
{
    public double Add(double n1, double n2)
    {
        return n1 + n2;
    }
    public double Subtract(double n1, double n2)
    {
        return n1 - n2;
    }
    public double Multiply(double n1, double n2)
    {
        return n1 * n2;
    }
    public double Divide(double n1, double n2)
    {
        return n1 / n2;
    }
}
```

Il servizio espone un endpoint per comunicare con il servizio che viene definito mediante un file di configurazione (Web.config), come illustrato nella configurazione di esempio seguente.

```xaml
<services>
    <service
        name="Microsoft.ServiceModel.Samples.CalculatorService"
        behaviorConfiguration="CalculatorServiceBehavior">
        <!-- ICalculator is exposed at the base address provided by
         host: http://localhost/servicemodelsamples/service.svc.  -->
       <endpoint address=""
              binding="wsHttpBinding"
              contract="Microsoft.ServiceModel.Samples.ICalculator" />
       ...
    </service>
</services>
```

Il servizio espone l'endpoint dell'indirizzo di base fornito dall'host IIS o WAS. L'associazione è configurata con una classe <xref:System.ServiceModel.WSHttpBinding> standard che fornisce comunicazione HTTP e protocolli del servizio Web standard per l'indirizzamento e la sicurezza. Il contratto rappresenta il `ICalculator` implementato dal servizio.

Come configurato, è possibile accedere al servizio `http://localhost/servicemodelsamples/service.svc` da un client nello stesso computer. Affinché i client presenti nei computer remoti accedano al servizio, è necessario specificare un nome di dominio completo anziché localhost.

Per impostazione predefinita il framework non espone metadati. Di conseguenza, il servizio attiva <xref:System.ServiceModel.Description.ServiceMetadataBehavior> ed espone un endpoint di scambio di metadati (MEX) in `http://localhost/servicemodelsamples/service.svc/mex` . Nella configurazione seguente viene illustrata questa evenienza.

```xaml
<system.serviceModel>
  <services>
    <service
        name="Microsoft.ServiceModel.Samples.CalculatorService"
        behaviorConfiguration="CalculatorServiceBehavior">
      ...
      <!-- the mex endpoint is exposed at
       http://localhost/servicemodelsamples/service.svc/mex -->
      <endpoint address="mex"
                binding="mexHttpBinding"
                contract="IMetadataExchange" />
    </service>
  </services>

  <!--For debugging purposes set the includeExceptionDetailInFaults
   attribute to true-->
  <behaviors>
    <serviceBehaviors>
      <behavior name="CalculatorServiceBehavior">
        <serviceMetadata httpGetEnabled="True"/>
        <serviceDebug includeExceptionDetailInFaults="False" />
      </behavior>
    </serviceBehaviors>
  </behaviors>
</system.serviceModel>
```

Il client comunica utilizzando un tipo di contratto specificato utilizzando una classe client generata dallo [strumento ServiceModel Metadata Utility Tool (Svcutil. exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md). Questo client generato è contenuto nel file generatedClient.cs o generatedClient.vb. Questa utilità recupera metadati per un servizio specificato e genera un client che viene utilizzato dall'applicazione client per comunicare utilizzando un tipo di contratto specificato. Il servizio ospitato deve essere disponibile per generare il codice client, perché il servizio viene utilizzato per recuperare i metadati aggiornati.

 Eseguire il comando seguente dal prompt dei comandi SDK nella directory del client per generare il proxy tipizzato:

```console
svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /out:generatedClient.cs
```

Per generare il client in Visual Basic, immettere il codice seguente nel prompt dei comandi SDK:

`Svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /l:vb /out:generatedClient.vb`

Utilizzando il client generato, il client può accedere a un endpoint del servizio specificato configurando l'indirizzo e l'associazione appropriati. Analogamente al servizio, il client utilizza un file di configurazione (App.config) per specificare l'endpoint con il quale desidera comunicare. La configurazione dell'endpoint client è costituita da un indirizzo assoluto per l'endpoint del servizio, l'associazione e il contratto, come illustrato nell'esempio seguente.

```xaml
<client>
     <endpoint
         address="http://localhost/servicemodelsamples/service.svc"
         binding="wsHttpBinding"
         contract=" Microsoft.ServiceModel.Samples.ICalculator" />
</client>
```

L'implementazione del client crea un'istanza del client e utilizza l'interfaccia tipizzata per avviare la comunicazione con il servizio, come illustrato nell'esempio di codice seguente.

```vb
' Create a client
Dim client As New CalculatorClient()

' Call the Add service operation.
            Dim value1 = 100.0R
            Dim value2 = 15.99R
            Dim result = client.Add(value1, value2)
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result)

' Call the Subtract service operation.
value1 = 145.00R
value2 = 76.54R
result = client.Subtract(value1, value2)
Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result)

' Call the Multiply service operation.
value1 = 9.00R
value2 = 81.25R
result = client.Multiply(value1, value2)
Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result)

' Call the Divide service operation.
value1 = 22.00R
value2 = 7.00R
result = client.Divide(value1, value2)
Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result)

'Closing the client gracefully closes the connection and cleans up resources
```

```csharp
// Create a client.
CalculatorClient client = new CalculatorClient();

// Call the Add service operation.
double value1 = 100.00D;
double value2 = 15.99D;
double result = client.Add(value1, value2);
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);

// Call the Subtract service operation.
value1 = 145.00D;
value2 = 76.54D;
result = client.Subtract(value1, value2);
Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);

// Call the Multiply service operation.
value1 = 9.00D;
value2 = 81.25D;
result = client.Multiply(value1, value2);
Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);

// Call the Divide service operation.
value1 = 22.00D;
value2 = 7.00D;
result = client.Divide(value1, value2);
Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);

//Closing the client releases all communication resources.
client.Close();
```

Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client. Premere INVIO nella finestra del client per arrestare il client.

```output
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714

Press <ENTER> to terminate client.
```

Nell'esempio della guida introduttiva viene illustrata la modalità standard per creare un servizio e un client. L'altra build di [base](basic-sample.md) di questo esempio per illustrare le funzionalità specifiche del prodotto.

### <a name="to-set-up-build-and-run-the-sample"></a>Per impostare, compilare ed eseguire l'esempio

1. Assicurarsi di avere eseguito la [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).

2. Per compilare l'edizione in C# o Visual Basic .NET della soluzione, seguire le istruzioni in [Building the Windows Communication Foundation Samples](building-the-samples.md).

3. Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [esecuzione degli esempi di Windows Communication Foundation](running-the-samples.md).

## <a name="see-also"></a>Vedere anche

- [Procedura: ospitare un servizio WCF in un'applicazione gestita](../how-to-host-a-wcf-service-in-a-managed-application.md)
- [Procedura: ospitare un servizio WCF in IIS](../feature-details/how-to-host-a-wcf-service-in-iis.md)

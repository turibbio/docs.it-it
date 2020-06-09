---
title: Eccezioni previste
ms.date: 03/30/2017
ms.assetid: 299a6987-ae6b-43c6-987f-12b034b583ae
ms.openlocfilehash: d8e3c024eb69fe22ec27f3e3697bc4fc7b4ee121
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600529"
---
# <a name="expected-exceptions"></a>Eccezioni previste
In questo esempio viene illustrato come rilevare le eccezioni previste quando si utilizza un client tipizzato. Questo esempio si basa sul [Introduzione](getting-started-sample.md) che implementa un servizio di calcolatrice. In questo esempio, il client è un'applicazione console (.exe) e il servizio è ospitato da Internet Information Services (IIS).  
  
> [!NOTE]
> La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 In questo esempio viene illustrata l'intercettazione e la gestione di due tipi di eccezione previsti che devono essere gestiti da programmi specifici, ovvero `TimeoutException` e `CommunicationException`.  
  
 Le eccezioni generate dai metodi di comunicazione su un client Windows Communication Foundation (WCF) sono previste o impreviste. Le eccezioni impreviste includono gli errori irreversibili come `OutOfMemoryException` e gli errori di programmazione come `ArgumentNullException` o `InvalidOperationException`. Non esiste in genere un modo utile per gestire gli errori imprevisti, quindi in genere non è consigliabile intercettarli quando si chiama un metodo di comunicazione client WCF.  
  
 Le eccezioni previste dai metodi di comunicazione su un client WCF includono `TimeoutException` , `CommunicationException` e qualsiasi classe derivata di `CommunicationException` . Che indicano un problema durante la comunicazione che può essere gestito in modo sicuro interrompendo il client WCF e segnalando un errore di comunicazione. Perché fattori esterni possono provocare questi errori in qualsiasi applicazione, le eccezioni devono essere rilevate da applicazioni specifiche e deve essere eseguito il ripristino quando si verificano.  
  
 Un client può generare numerose classi derivate di `CommunicationException`. In alcuni casi, le applicazioni rilevano anche alcune di queste eccezioni per una gestione speciale, ma lasciano che le altre vengano gestite come `CommunicationException`. Questo processo può essere portato a termine rilevando prima il tipo di eccezione più specifico e quindi `CommunicationException` in una clausola di rilevamento successiva.  
  
 Il codice che chiama un metodo di comunicazione client deve rilevare `TimeoutException` e `CommunicationException`. Un modo per gestire tali errori consiste nell'interrompere il client e riportare l'errore di comunicazione.  
  
```csharp
try  
{  
    ...  
    double result = client.Add(value1, value2);  
    ...  
    client.Close();  
}  
catch (TimeoutException exception)  
{  
    Console.WriteLine("Got {0}", exception.GetType());  
    client.Abort();  
}  
catch (CommunicationException exception)  
{  
    Console.WriteLine("Got {0}", exception.GetType());  
    client.Abort();  
}  
```  
  
 In seguito a un'eccezione prevista, il client può essere utilizzabile o non esserlo. Per determinare se il client può ancora essere utilizzato, verificare che la proprietà `State` sia impostata su `CommunicationState`.Opened. Se è aperto, può essere ancora utilizzato. In caso contrario è necessario interrompere il client e rilasciare tutti i riferimenti attinenti.  
  
> [!CAUTION]
> È possibile osservare che i client che dispongono di una sessione spesso possono più essere utilizzati dopo un'eccezione, mentre i client privi di una sessione spesso possono ancora essere utilizzati dopo un'eccezione. Tuttavia, nessuno di questi comportamenti è garantito, pertanto se si desidera continuare a utilizzare il client dopo un'eccezione, l'applicazione dovere controllare la proprietà `State` per verificare che il client sia ancora aperto.  
  
 Quando si esegue l'esempio, le risposte e le eccezioni dell'operazione vengono visualizzate nella finestra della console client.  
  
 Il processo client esegue due scenari, ognuno dei quali tenta di chiamare `Add` seguito da `Divide`. Il primo scenario simula un problema di rete interrompendo il client prima di effettuare la chiamata a `Divide`. Il secondo scenario provoca una condizione di timeout impostando un valore di timeout troppo breve per consentire il completamento del metodo. L'output previsto dal processo client è:  
  
```output
Add(100,15.99) = 115.99  
Simulated network problem occurs...  
Got System.ServiceModel.CommunicationObjectAbortedException  
Add(100,15.99) = 115.99  
Set timeout too short for method to complete...  
Got System.TimeoutException  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Per impostare, compilare ed eseguire l'esempio  
  
1. Assicurarsi di avere eseguito la [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Per compilare l'edizione in C# o Visual Basic .NET della soluzione, seguire le istruzioni in [Building the Windows Communication Foundation Samples](building-the-samples.md).  
  
3. Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [esecuzione degli esempi di Windows Communication Foundation](running-the-samples.md).  
  
> [!IMPORTANT]
> È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente (impostazione predefinita) prima di continuare.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) ed [!INCLUDE[wf1](../../../../includes/wf1-md.md)] esempi. Questo esempio si trova nella directory seguente.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\ExpectedExceptions`  

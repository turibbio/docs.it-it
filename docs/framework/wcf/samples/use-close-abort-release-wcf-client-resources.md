---
title: Usare Chiudi e Interrompi per rilasciare risorse client WCF
description: Dispose può avere esito negativo e generare eccezioni in caso di errore di rete. Questo può causare un comportamento indesiderato. In alternativa, usare Chiudi e Interrompi per rilasciare le risorse client quando la rete non è riuscita.
ms.date: 11/12/2018
ms.assetid: aff82a8d-933d-4bdc-b0c2-c2f7527204fb
ms.openlocfilehash: b338b760f461d7b773f43dd1f5e6dbce98f9e15a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599919"
---
# <a name="close-and-abort-release-resources-safely-when-network-connections-have-dropped"></a>Chiudi e Interrompi le risorse di rilascio in modo sicuro quando le connessioni di rete

In questo esempio viene illustrato l'utilizzo dei `Close` `Abort` metodi e per pulire le risorse quando si utilizza un client tipizzato. L' `using` istruzione genera eccezioni quando la connessione di rete non è affidabile. Questo esempio si basa sul [Introduzione](getting-started-sample.md) che implementa un servizio di calcolatrice. In questo esempio, il client è un'applicazione console (.exe) e il servizio è ospitato da Internet Information Services (IIS).

> [!NOTE]
> La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.

In questo esempio vengono illustrati due dei problemi comuni che si verificano in caso di utilizzo dell'istruzione "using" di C# con i client tipizzati e il codice che pulisce correttamente le eccezioni.

L'istruzione "using" di C# genera una chiamata a `Dispose`(). Questo corrisponde a `Close`(), che può generare eccezioni quando si verifica un errore di rete. Poiché la chiamata a `Dispose`() si verifica implicitamente alla parentesi graffa di chiusura del blocco "using", è probabile che l'origine delle eccezioni non venga rilevata da chi scrive il codice e da chi lo legge. Questa situazione può causare errori dell'applicazione.

Il primo problema, illustrato nel metodo `DemonstrateProblemUsingCanThrow` è che la parentesi graffa di chiusura genera un'eccezione e il codice dopo che la parentesi graffa di chiusura non viene eseguito:

```csharp
using (CalculatorClient client = new CalculatorClient())
{
    ...
} // <-- this line might throw
Console.WriteLine("Hope this code wasn't important, because it might not happen.");
```

Anche se non vengono generate eccezioni nel blocco "using" o se tutte le eccezioni all'interno del blocco "using" vengono rilevate, `Console.WriteLine` potrebbe non verificarsi visto che la chiamata `Dispose`() implicita potrebbe generare un'eccezione alla parentesi graffa di chiusura.

Il secondo problema, illustrato nel metodo `DemonstrateProblemUsingCanThrowAndMask` deriva da un'altra implicazione della parentesi graffa di chiusura che genera un'eccezione:

```csharp
using (CalculatorClient client = new CalculatorClient())
{
    ...
    throw new ApplicationException("Hope this exception was not important, because "+
                                   "it might be masked by the Close exception.");
} // <-- this line might throw an exception.
```

Poiché `Dispose`() si verifica in un blocco "finally", `ApplicationException` non viene mai visualizzato al di fuori del blocco "using" se si verifica un errore in `Dispose`(). Se il codice esterno deve essere in grado di rilevare quando si verifica `ApplicationException`, si potrebbero verificare problemi se il costrutto "using" maschera questa eccezione.

Nell'esempio viene infine illustrato come pulire correttamente le eccezioni che si verificano in `DemonstrateCleanupWithExceptions`. Questa operazione utilizza un blocco try/catch per segnalare gli errori e chiamare `Abort`. Per ulteriori informazioni sull'intercettazione delle eccezioni dalle chiamate client, vedere l'esempio di [eccezioni previste](expected-exceptions.md) .

```csharp
try
{
    ...
    client.Close();
}
catch (CommunicationException e)
{
    ...
    client.Abort();
}
catch (TimeoutException e)
{
    ...
    client.Abort();
}
catch (Exception e)
{
    ...
    client.Abort();
    throw;
}
```

> [!NOTE]
> Istruzione using e ServiceHost: molte applicazioni indipendenti non fanno altro che ospitare un servizio e ServiceHost.Close raramente genera un'eccezione, pertanto tali applicazioni possono utilizzare in modo sicuro l'istruzione using con ServiceHost. Tuttavia, è consigliabile prendere in considerazione che ServiceHost.Close può generare un'eccezione `CommunicationException`, pertanto se l'applicazione è ancora in esecuzione dopo avere chiuso ServiceHost, è necessario evitare di usare l'istruzione using e seguire il modello fornito in precedenza.

Quando si esegue l'esempio, le risposte e le eccezioni dell'operazione vengono visualizzate nella finestra della console client.

Il processo client esegue tre scenari, ognuno dei quali tenta di chiamare `Divide`. Nel primo scenario viene descritto il codice ignorato a causa di un'eccezione da `Dispose`(). Nel secondo scenario viene illustrata un'eccezione importante mascherata a causa di un'eccezione da `Dispose`(). Nel terzo scenario viene illustrato come eseguire correttamente la pulizia.

L'output previsto dal processo client è:

```console
=
= Demonstrating problem:  closing brace of using statement can throw.
=
Got System.ServiceModel.CommunicationException from Divide.
Got System.ServiceModel.Security.MessageSecurityException
=
= Demonstrating problem:  closing brace of using statement can mask other Exceptions.
=
Got System.ServiceModel.CommunicationException from Divide.
Got System.ServiceModel.Security.MessageSecurityException
=
= Demonstrating cleanup with Exceptions.
=
Calling client.Add(0.0, 0.0);
        client.Add(0.0, 0.0); returned 0
Calling client.Divide(0.0, 0.0);
Got System.ServiceModel.CommunicationException from Divide.

Press <ENTER> to terminate client.
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
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\UsingUsing`

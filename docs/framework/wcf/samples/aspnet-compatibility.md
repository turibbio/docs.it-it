---
title: Compatibilità con ASP.NET
ms.date: 03/30/2017
ms.assetid: c8b51f1e-c096-4c42-ad99-0519887bbbc5
ms.openlocfilehash: 23930e0756d3fbefc28a8f650b5a056106145a50
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594712"
---
# <a name="aspnet-compatibility"></a>Compatibilità con ASP.NET

In questo esempio viene illustrato come abilitare la modalità di compatibilità ASP.NET in Windows Communication Foundation (WCF). I servizi in esecuzione in modalità di compatibilità ASP.NET partecipano completamente alla pipeline dell'applicazione ASP.NET e possono usare le funzionalità di ASP.NET, ad esempio l'autorizzazione file/URL, lo stato della sessione e la <xref:System.Web.HttpContext> classe. La <xref:System.Web.HttpContext> classe consente l'accesso a cookie, sessioni e altre funzionalità ASP.NET. Questa modalità richiede che le associazioni usino il trasporto HTTP e che il servizio stesso debba essere ospitato in IIS.

In questo esempio, il client è un'applicazione console (un file eseguibile) e il servizio è ospitato da Internet Information Services (IIS).

> [!NOTE]
> La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.

Per l'esecuzione di questo esempio è necessario un pool di applicazioni .NET Framework 4. Per creare un nuovo pool di applicazioni o modificare il pool di applicazioni predefinito, attenersi alla procedura seguente.

1. Aprire il **Pannello di controllo**.  Aprire l'applet **strumenti di amministrazione** sotto l'intestazione **sistema e sicurezza** . Aprire l'applet **gestione Internet Information Services (IIS)** .

2. Espandere TreeView nel riquadro **connessioni** . Selezionare il nodo **pool di applicazioni** .

3. Per impostare il pool di applicazioni predefinito per l'utilizzo di .NET Framework 4 (che potrebbe causare problemi di incompatibilità con i siti esistenti), fare clic con il pulsante destro del mouse sull'elemento dell'elenco **DefaultAppPool** e selezionare **impostazioni di base.** Impostare il pull della **versione di .NET Framework** su **.NET Framework v 4.0.30128** (o versioni successive).

4. Per creare un nuovo pool di applicazioni che usi .NET Framework 4 (per mantenere la compatibilità per altre applicazioni), fare clic con il pulsante destro del mouse sul nodo **pool di applicazioni** e scegliere **Aggiungi pool di applicazioni.** Assegnare un nome al nuovo pool di applicazioni e impostare il pull della **versione di .NET Framework** su **.NET Framework v 4.0.30128** (o versioni successive). Dopo aver eseguito la procedura di installazione riportata di seguito, fare clic con il pulsante destro del mouse sull'applicazione **servicemodelsamples** e scegliere **Gestisci applicazione**, **Impostazioni avanzate.** Impostare il **pool di applicazioni** sul nuovo pool di applicazioni.

> [!IMPORTANT]
> È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente (impostazione predefinita) prima di continuare.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) ed [!INCLUDE[wf1](../../../../includes/wf1-md.md)] esempi. Questo esempio si trova nella directory seguente.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebHost\ASPNetCompatibility`

Questo esempio è basato sul [Introduzione](getting-started-sample.md), che implementa un servizio di calcolatrice. Il contratto `ICalculator` è stato modificato al contratto `ICalculatorSession` per consentire l'esecuzione di un set di operazioni mantenendo il risultato della sessione.

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface ICalculatorSession
{
    [OperationContract]
    void Clear();
    [OperationContract]
    void AddTo(double n);
    [OperationContract]
    void SubtractFrom(double n);
    [OperationContract]
    void MultiplyBy(double n);
    [OperationContract]
    void DivideBy(double n);
    [OperationContract]
    double Result();
}
```

Usando questa funzionalità il servizio mantiene lo stato di ogni client, mentre vengono chiamate più operazioni del servizio per eseguire un calcolo. Il client può recuperare il risultato corrente chiamando `Result` e può azzerare il risultato chiamando `Clear`.

Il servizio usa la sessione ASP.NET per archiviare il risultato per ogni sessione client. Questo consente al servizio di mantenere il risultato della sessione per ogni client, su più chiamate al servizio.

> [!NOTE]
> Lo stato della sessione ASP.NET e le sessioni WCF sono molto diversi. Per informazioni dettagliate sulle sessioni WCF, vedere la [sessione](session.md) .

Il servizio ha una dipendenza intima dallo stato della sessione ASP.NET e richiede la modalità di compatibilità ASP.NET per funzionare correttamente. Questi requisiti vengono espressi in modo dichiarativo applicando l'attributo `AspNetCompatibilityRequirements`.

```csharp
[AspNetCompatibilityRequirements(RequirementsMode =
                       AspNetCompatibilityRequirementsMode.Required)]
public class CalculatorService : ICalculatorSession
{
    double Result
    {  // store result in AspNet Session
       get {
          if (HttpContext.Current.Session["Result"] != null)
             return (double)HttpContext.Current.Session["Result"];
          return 0.0D;
       }
       set
       {
          HttpContext.Current.Session["Result"] = value;
       }
    }
    public void Clear()
    {
        Result = 0.0D;
    }
    public void AddTo(double n)
    {
        Result += n;
    }
    public void SubtractFrom(double n)
    {
        Result -= n;
    }
    public void MultiplyBy(double n)
    {
        Result *= n;
    }
    public void DivideBy(double n)
    {
        Result /= n;
    }
    public double Result()
    {
        return Result;
    }
}
```

Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client. Premere INVIO nella finestra del client per arrestare il client.

```console
0, + 100, - 50, * 17.65, / 2 = 441.25
Press <ENTER> to terminate client.
```

### <a name="to-set-up-build-and-run-the-sample"></a>Per impostare, compilare ed eseguire l'esempio

1. Assicurarsi di avere eseguito la [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).

2. Per compilare l'edizione in C# o Visual Basic .NET della soluzione, seguire le istruzioni in [Building the Windows Communication Foundation Samples](building-the-samples.md).

3. Una volta compilata la soluzione, eseguire Setup. bat per configurare l'applicazione ServiceModelSamples in IIS 7,0. La directory ServiceModelSamples dovrebbe ora essere visualizzata come applicazione IIS 7,0.

4. Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [esecuzione degli esempi di Windows Communication Foundation](running-the-samples.md).

## <a name="see-also"></a>Vedere anche

- [Hosting e salvataggio permanente](https://docs.microsoft.com/previous-versions/appfabric/ff383418(v=azure.10))

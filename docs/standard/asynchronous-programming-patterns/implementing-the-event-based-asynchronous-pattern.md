---
title: Implementazione del modello asincrono basato su eventi
description: Informazioni su come implementare il modello asincrono basato su eventi (EAP) in .NET. EAP è un modo standard per creare un pacchetto di una classe con funzionalità asincrone.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- components [.NET Framework], asynchronous
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: 43402d19-8d30-426d-8785-1a4478233bfa
ms.openlocfilehash: 9ffb2e2f426e2d2d97998a89a3e8d306de4f29ca
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84583661"
---
# <a name="implementing-the-event-based-asynchronous-pattern"></a>Implementazione del modello asincrono basato su eventi

In caso di scrittura di una classe con alcune operazioni che possono causare ritardi notevoli, è consigliabile assegnare la funzionalità asincrona implementando [Cenni preliminari sul modello asincrono basato su eventi](event-based-asynchronous-pattern-overview.md).

Il modello asincrono basato su eventi offre un modo standardizzato per aggiungere funzionalità asincrone a una classe. Se implementata con classi helper come <xref:System.ComponentModel.AsyncOperationManager>, la classe funzionerà con qualsiasi modello di applicazione, tra cui ASP.NET, applicazioni console e Windows Forms Application.

Per un esempio che implementa il modello asincrono basato su eventi, vedere [Procedura: Implementare un componente che supporta il modello asincrono basato su eventi](component-that-supports-the-event-based-asynchronous-pattern.md).

Per operazioni asincrone semplici, può risultare idoneo il componente <xref:System.ComponentModel.BackgroundWorker>. Per altre informazioni su <xref:System.ComponentModel.BackgroundWorker>, vedere [Procedura: eseguire un'operazione in background](../../framework/winforms/controls/how-to-run-an-operation-in-the-background.md).

L'elenco seguente descrive le funzionalità del modello asincrono basato su eventi affrontate in questo argomento.

- Opportunità per implementare il modello asincrono basato su eventi

- Denominazione di metodi asincroni

- Supporto facoltativo dell'annullamento

- Supporto facoltativo della proprietà IsBusy

- Supporto facoltativo per la generazione di report sullo stato di avanzamento

- Supporto facoltativo per la restituzione di risultati incrementali

- Gestione dei parametri Out e Ref nei metodi

## <a name="opportunities-for-implementing-the-event-based-asynchronous-pattern"></a>Opportunità per implementare il modello asincrono basato su eventi

Valutare l'implementazione del modello asincrono basato su eventi quando:

- I client della classe non richiedono che siano disponibili oggetti <xref:System.Threading.WaitHandle> e <xref:System.IAsyncResult> per le operazioni asincrone, quindi il polling e il metodo <xref:System.Threading.WaitHandle.WaitAll%2A> o <xref:System.Threading.WaitHandle.WaitAny%2A> devono essere compilati dal client.

- Si desidera che le operazioni asincrone vengano gestite dal client con il modello noto di evento/delegato.

Qualsiasi operazione è un candidato per un'implementazione asincrona, ma è opportuno considerare quelle con lunghe latenze previste. Sono particolarmente indicate le operazioni in cui i client chiamano un metodo e ricevono una notifica al completamento, senza richiedere ulteriori interventi. Rientrano in questa condizione anche le operazioni con esecuzione continua,che inviano notifiche periodiche ai client sullo stato di avanzamento, sui risultati incrementali o sulle modifiche di stato.

Per altre informazioni sui casi in cui supportare il modello asincrono basato su eventi, vedere [Quando implementare il modello asincrono basato su eventi](deciding-when-to-implement-the-event-based-asynchronous-pattern.md).

## <a name="naming-asynchronous-methods"></a>Denominazione di metodi asincroni

Per ogni metodo *MethodName* sincrono per il quale si desidera specificare una controparte asincrona:

Definire un metodo**Async** _MethodName_che:

- Restituisce `void`.

- Accetta gli stessi parametri del metodo *MethodName*.

- Accetta più chiamate.

Definire facoltativamente un overload**Async** di _MethodName_, identico a _MethodName_**Async**, ma con un parametro con valori di oggetto aggiuntivo denominato `userState` . Seguire questa procedura se si intende gestire più chiamate simultanee del metodo, nel qual caso il valore `userState` verrà recapitato nuovamente a tutti i gestori eventi per distinguere le chiamate del metodo. È anche possibile scegliere questa opzione come posizione in cui archiviare lo stato utente per un successivo recupero.

Per ogni firma del metodo**Async** _MethodName_separato:

1. Definire l'evento seguente nella stessa classe del metodo:

    ```vb
    Public Event MethodNameCompleted As MethodNameCompletedEventHandler
    ```

    ```csharp
    public event MethodNameCompletedEventHandler MethodNameCompleted;
    ```

2. Definire il delegato seguente e <xref:System.ComponentModel.AsyncCompletedEventArgs>. che verranno probabilmente definiti all'esterno della classe, ma nello stesso spazio dei nomi.

    ```vb
    Public Delegate Sub MethodNameCompletedEventHandler( _
        ByVal sender As Object, _
        ByVal e As MethodNameCompletedEventArgs)

    Public Class MethodNameCompletedEventArgs
        Inherits System.ComponentModel.AsyncCompletedEventArgs
    Public ReadOnly Property Result() As MyReturnType
    End Property
    ```

    ```csharp
    public delegate void MethodNameCompletedEventHandler(object sender,
        MethodNameCompletedEventArgs e);

    public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs
    {
        public MyReturnType Result { get; }
    }
    ```

    - Assicurarsi che la classe _MethodName_**CompletedEventArgs** esponga i relativi membri come proprietà di sola lettura e non come campi, poiché i campi impediscono Data Binding.

    - Non definire alcuna classe derivata da <xref:System.ComponentModel.AsyncCompletedEventArgs> per i metodi che non producono risultati. Usare semplicemente un'istanza di <xref:System.ComponentModel.AsyncCompletedEventArgs>.

      > [!NOTE]
      > È perfettamente accettabile, quando possibile e appropriato, riutilizzare il delegato e i tipi <xref:System.ComponentModel.AsyncCompletedEventArgs>. In questo caso, la denominazione non sarà coerente con il nome del metodo, perché un delegato e un oggetto <xref:System.ComponentModel.AsyncCompletedEventArgs> specifici non saranno associati a un singolo metodo.

## <a name="optionally-support-cancellation"></a>Supporto facoltativo dell'annullamento

Se la classe supporta l'annullamento delle operazioni asincrone, l'annullamento dovrebbe essere esposto al client come descritto di seguito. Si noti che è necessario raggiungere due decisioni prima di definire il supporto dell'annullamento:

- La classe, incluse eventuali aggiunte future previste, include una sola operazione asincrona che supporta l'annullamento?

- Le operazioni asincrone che supportano l'annullamento supportano più operazioni in sospeso? In altre termini, il metodo**Async** _Method_accetta un `userState` parametro e consente più chiamate prima di attendere il completamento di qualsiasi?

Usare le risposte a queste due domande nella tabella seguente per determinare la firma per il metodo di annullamento scelto.

### <a name="visual-basic"></a>Visual Basic

||Più operazioni simultanee supportate|Una sola operazione alla volta|
|------|------------------------------------------------|----------------------------------|
|Una operazione asincrona nell'intera classe|`Sub MethodNameAsyncCancel(ByVal userState As Object)`|`Sub MethodNameAsyncCancel()`|
|Più operazioni asincrone nella classe|`Sub CancelAsync(ByVal userState As Object)`|`Sub CancelAsync()`|

### <a name="c"></a>C\#

||Più operazioni simultanee supportate|Una sola operazione alla volta|
|------|------------------------------------------------|----------------------------------|
|Una operazione asincrona nell'intera classe|`void MethodNameAsyncCancel(object userState);`|`void MethodNameAsyncCancel();`|
|Più operazioni asincrone nella classe|`void CancelAsync(object userState);`|`void CancelAsync();`|

Se si definisce il metodo `CancelAsync(object userState)`, i client devono scegliere con cautela i valori di stato per permettere la distinzione tra tutti i metodi asincroni chiamati sull'oggetto e non solo tra tutte le chiamate di un singolo metodo asincrono.

La decisione di denominare la versione single-Async-Operation _MethodName_**AsyncCancel** si basa sulla possibilità di individuare più facilmente il metodo in un ambiente di progettazione come IntelliSense di Visual Studio. Questo raggruppa i membri correlati e li distingue dagli altri membri che non hanno a che fare con funzionalità asincrone. Se si prevede che potrebbero essere aggiunte altre operazioni asincrone nelle versioni successive, è preferibile definire `CancelAsync`.

Non definire più metodi della tabella precedente nella stessa classe. Non avrebbe senso e creerebbe confusione nell'interfaccia della classe con un numero eccessivo di metodi.

Questi metodi vengono in genere restituiti immediatamente e l'esito dell'operazione di annullamento non è garantito. Nel gestore eventi per l'evento _MethodName_**Completed** , l'oggetto _NomeMetodo_**CompletedEventArgs** contiene un `Cancelled` campo, che i client possono usare per determinare se si è verificato l'annullamento.

Rispettare la semantica di annullamento descritta in [Suggerimenti per l'implementazione del modello asincrono basato su eventi](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).

## <a name="optionally-support-the-isbusy-property"></a>Supporto facoltativo della proprietà IsBusy

Se la classe non supporta più chiamate simultanee, è consigliabile esporre una proprietà `IsBusy`. Ciò consente agli sviluppatori di determinare se un metodo**Async** _MethodName_è in esecuzione senza intercettare un'eccezione dal metodo**Async** _MethodName_.

Rispettare la semantica di `IsBusy` descritta in [Suggerimenti per l'implementazione del modello asincrono basato su eventi](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).

## <a name="optionally-provide-support-for-progress-reporting"></a>Supporto facoltativo per la generazione di report sullo stato di avanzamento

È spesso utile che un'operazione asincrona generi un report sullo stato di avanzamento durante il funzionamento. Il modello asincrono basato su eventi offre linee guida a tale scopo.

- Definire facoltativamente un evento che verrà generato dall'operazione asincrona e chiamato sul thread appropriato. L'oggetto <xref:System.ComponentModel.ProgressChangedEventArgs> supporta un indicatore di stato con valori interi compresi tra 0 e 100.

- Denominare l'evento come indicato di seguito:

  - `ProgressChanged` se la classe dispone di più operazioni asincrone (o presumibilmente aumenterà per includere più operazioni asincrone nelle versioni future);

  - _MethodName_**ProgressChanged** se la classe dispone di una singola operazione asincrona.

  Questa scelta di denominazione è paragonabile a quella eseguita per il metodo di annullamento, come descritto nella sezione Supporto facoltativo dell'annullamento.

Questo evento deve usare la firma del delegato <xref:System.ComponentModel.ProgressChangedEventHandler> e la classe <xref:System.ComponentModel.ProgressChangedEventArgs>. In alternativa, se è possibile fornire un indicatore di stato più specifico per il dominio (ad esempio, byte letti e byte totali per un'operazione di download), è consigliabile definire una classe derivata di <xref:System.ComponentModel.ProgressChangedEventArgs>.

Si noti che per la classe è presente un solo `ProgressChanged` evento o _MethodName_**ProgressChanged** , indipendentemente dal numero di metodi asincroni supportati. Si prevede che i client usino l' `userState` oggetto passato ai metodi async _MethodName_**Async** per distinguere tra gli aggiornamenti dello stato di avanzamento in più operazioni simultanee.

In alcuni casi, più operazioni potrebbero supportare lo stato di avanzamento e restituire singolarmente un indicatore diverso. In questo caso, un singolo evento `ProgressChanged` non è appropriato ed è opportuno scegliere di supportare più eventi `ProgressChanged`. In questo caso usare un modello di denominazione di _MethodName_**ProgressChanged** per ogni metodo**Async** _MethodName_.

Rispettare la semantica della generazione di report sullo stato di avanzamento descritta in [Suggerimenti per l'implementazione del modello asincrono basato su eventi](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).

## <a name="optionally-provide-support-for-returning-incremental-results"></a>Supporto facoltativo per la restituzione di risultati incrementali

A volte un'operazione asincrona può restituire risultati incrementali prima del completamento. Per supportare questo scenario sono disponibili numerose opzioni. Di seguito sono riportati alcuni esempi.

### <a name="single-operation-class"></a>Classe con singola operazione

Se la classe supporta solo una singola operazione asincrona e tale operazione è in grado di restituire risultati incrementali:

- Estendere il <xref:System.ComponentModel.ProgressChangedEventArgs> tipo per includere i dati del risultato incrementale e definire un evento _MethodName_**ProgressChanged** con i dati estesi.

- Generare questo evento _MethodName_**ProgressChanged** quando è presente un risultato incrementale da segnalare.

Questa soluzione si applica in modo specifico a una classe con singola operazione asincrona poiché non si verificano problemi con lo stesso evento che si verifica per restituire i risultati incrementali in "tutte le operazioni", come fa l'evento _MethodName_**ProgressChanged** .

### <a name="multiple-operation-class-with-homogeneous-incremental-results"></a>Classe con più operazioni con risultati incrementali omogenei

In questo caso, la classe supporta più metodi asincroni, ognuno dei quali è in grado di restituire risultati incrementali che avranno tutti lo stesso tipo di dati.

Seguire il modello descritto in precedenza per le classi con singola operazione, poiché la stessa struttura di <xref:System.EventArgs> è applicabile a tutti i risultati incrementali. Definire un `ProgressChanged` evento anziché un evento _MethodName_**ProgressChanged** , poiché si applica a più metodi asincroni.

### <a name="multiple-operation-class-with-heterogeneous-incremental-results"></a>Classe con più operazioni con risultati incrementali eterogenei

Se la classe supporta più metodi asincroni, ognuno dei quali restituisce un tipo diverso di dati, è consigliabile:

- Separare il report dei risultati incrementali dal report sullo stato di avanzamento.

- Definire un evento _MethodName_**ProgressChanged** separato con appropriato <xref:System.EventArgs> per ogni metodo asincrono per gestire i dati dei risultati incrementali del metodo.

Chiamare il gestore eventi sul thread appropriato, come descritto in [Suggerimenti per l'implementazione del modello asincrono basato su eventi](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).

## <a name="handling-out-and-ref-parameters-in-methods"></a>Gestione dei parametri Out e Ref nei metodi

Sebbene l'uso di `out` e `ref` sia, in generale, sconsigliato in .NET Framework, ecco le regole da seguire quando sono presenti:

Dato un metodo *MethodName* sincrono:

- `out`i parametri per *MethodName* non devono far parte di _MethodName_**Async**. Devono invece far parte di _MethodName_**CompletedEventArgs** con lo stesso nome del relativo parametro equivalente in *MethodName* (a meno che non esista un nome più appropriato).

- `ref`i parametri per *MethodName* devono essere visualizzati come parte di _MethodName_**Async**e come parte di _MethodName_**CompletedEventArgs** con lo stesso nome del relativo parametro equivalente in *MethodName* (a meno che non esista un nome più appropriato).

Si consideri ad esempio di avere una situazione simile alla seguente:

```vb
Public Function MethodName(ByVal arg1 As String, ByRef arg2 As String, ByRef arg3 As String) As Integer
```

```csharp
public int MethodName(string arg1, ref string arg2, out string arg3);
```

Il metodo asincrono e la relativa classe <xref:System.ComponentModel.AsyncCompletedEventArgs> avranno un aspetto simile al seguente:

```vb
Public Sub MethodNameAsync(ByVal arg1 As String, ByVal arg2 As String)

Public Class MethodNameCompletedEventArgs
    Inherits System.ComponentModel.AsyncCompletedEventArgs
    Public ReadOnly Property Result() As Integer
    End Property
    Public ReadOnly Property Arg2() As String
    End Property
    Public ReadOnly Property Arg3() As String
    End Property
End Class
```

```csharp
public void MethodNameAsync(string arg1, string arg2);

public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs
{
    public int Result { get; };
    public string Arg2 { get; };
    public string Arg3 { get; };
}
```

## <a name="see-also"></a>Vedere anche

- <xref:System.ComponentModel.ProgressChangedEventArgs>
- <xref:System.ComponentModel.AsyncCompletedEventArgs>
- [Procedura: implementare un componente che supporta il modello asincrono basato su eventi](component-that-supports-the-event-based-asynchronous-pattern.md)
- [Procedura: Eseguire un'operazione in background](../../framework/winforms/controls/how-to-run-an-operation-in-the-background.md)
- [Procedura: implementare un form che utilizza un'operazione in background](../../framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)
- [Quando implementare il modello asincrono basato su eventi](deciding-when-to-implement-the-event-based-asynchronous-pattern.md)
- [Suggerimenti per l'implementazione del modello asincrono basato su eventi](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)
- [Event-based Asynchronous Pattern (EAP)](event-based-asynchronous-pattern-eap.md) (Modello asincrono basato su eventi, EAP)

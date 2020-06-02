---
title: Sicurezza e race condition
'description:': Describes pitfalls to avoid around security holes exploited by race conditions, including dispose methods, constructors, cached objects, and finalizers.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [.NET Framework], race conditions
- race conditions
- secure coding, race conditions
- code security, race conditions
ms.assetid: ea3edb80-b2e8-4e85-bfed-311b20cb59b6
ms.openlocfilehash: 715bf240a5f7f44ba3f914ad6788631074aa41b2
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291019"
---
# <a name="security-and-race-conditions"></a>Sicurezza e race condition
Un'altra area di interesse è la possibilità di buchi di sicurezza sfruttati da race condition. Questa situazione può verificarsi in diversi modi. Gli argomenti secondari che seguono illustrano alcune delle principali insidie che lo sviluppatore deve evitare.  
  
## <a name="race-conditions-in-the-dispose-method"></a>Race condition nel metodo Dispose  
 Se il metodo **Dispose** di una classe (per altre informazioni, vedere [Garbage Collection](../garbage-collection/index.md)) non è sincronizzato, è possibile che il codice di pulitura all'interno di **Dispose** possa essere eseguito più di una volta, come illustrato nell'esempio seguente.  
  
```vb  
Sub Dispose()  
    If Not (myObj Is Nothing) Then  
       Cleanup(myObj)  
       myObj = Nothing  
    End If  
End Sub  
```  
  
```csharp  
void Dispose()
{  
    if (myObj != null)
    {  
        Cleanup(myObj);  
        myObj = null;  
    }  
}  
```  
  
 Poiché questa implementazione di **Dispose** non è sincronizzata, è possibile che `Cleanup` venga chiamata dal primo thread e quindi da un secondo thread prima che `_myObj` venga impostato su **null**. Se questo è un problema di sicurezza, dipende da cosa accade quando `Cleanup` viene eseguito il codice. Un problema importante con le implementazioni **Dispose** non sincronizzate prevede l'uso di handle di risorsa, ad esempio i file. L'eliminazione non corretta può causare l'uso di un handle errato, che spesso genera vulnerabilità di sicurezza.  
  
## <a name="race-conditions-in-constructors"></a>Race condition nei costruttori  
 In alcune applicazioni, è possibile che altri thread accedano ai membri della classe prima che i costruttori della classe vengano eseguiti completamente. È necessario esaminare tutti i costruttori di classe per assicurarsi che non vi siano problemi di sicurezza, se necessario, o sincronizzare i thread, se necessario.  
  
## <a name="race-conditions-with-cached-objects"></a>Race condition con oggetti memorizzati nella cache  
 Il codice che memorizza nella cache le informazioni di sicurezza o utilizza l'operazione di [asserzione](../../framework/misc/using-the-assert-method.md) di sicurezza dall'accesso di codice potrebbe essere vulnerabile alle race condition se altre parti della classe non sono sincronizzate in modo appropriato, come illustrato nell'esempio seguente.  
  
```vb  
Sub SomeSecureFunction()  
    If SomeDemandPasses() Then  
        fCallersOk = True  
        DoOtherWork()  
        fCallersOk = False  
    End If  
End Sub  
  
Sub DoOtherWork()  
    If fCallersOK Then  
        DoSomethingTrusted()  
    Else  
        DemandSomething()  
        DoSomethingTrusted()  
    End If  
End Sub  
```  
  
```csharp  
void SomeSecureFunction()
{  
    if (SomeDemandPasses())
    {  
        fCallersOk = true;  
        DoOtherWork();  
        fCallersOk = false;  
    }  
}  
void DoOtherWork()
{  
    if (fCallersOK)
    {  
        DoSomethingTrusted();  
    }  
    else
    {  
        DemandSomething();  
        DoSomethingTrusted();  
    }  
}  
```  
  
 Se sono presenti altri percorsi `DoOtherWork` che possono essere chiamati da un altro thread con lo stesso oggetto, un chiamante non attendibile può superare una richiesta.  
  
 Se il codice memorizza nella cache le informazioni di sicurezza, assicurarsi di esaminarle per questa vulnerabilità.  
  
## <a name="race-conditions-in-finalizers"></a>Race condition nei finalizzatori  
 Le race condition possono verificarsi anche in un oggetto che fa riferimento a una risorsa statica o non gestita che quindi libera nel finalizzatore. Se più oggetti condividono una risorsa che viene modificata nel finalizzatore di una classe, gli oggetti devono sincronizzare tutti gli accessi a tale risorsa.  
  
## <a name="see-also"></a>Vedere anche

- [Linee guida per la generazione di codice sicuro](secure-coding-guidelines.md)

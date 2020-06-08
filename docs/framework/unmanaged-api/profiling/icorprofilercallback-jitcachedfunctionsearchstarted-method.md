---
title: Metodo ICorProfilerCallback::JITCachedFunctionSearchStarted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCachedFunctionSearchStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCachedFunctionSearchStarted
helpviewer_keywords:
- JITCachedFunctionSearchStarted method [.NET Framework profiling]
- ICorProfilerCallback::JITCachedFunctionSearchStarted method [.NET Framework profiling]
ms.assetid: 5cba642c-0d80-48ee-889d-198c5044d821
topic_type:
- apiref
ms.openlocfilehash: d8f4a04abea0bd5eb9bf38629a8fcaf76479bcc9
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500057"
---
# <a name="icorprofilercallbackjitcachedfunctionsearchstarted-method"></a>Metodo ICorProfilerCallback::JITCachedFunctionSearchStarted
Notifica al profiler che è stata avviata una ricerca per una funzione compilata in precedenza utilizzando il generatore di immagini native (NGen. exe).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT JITCachedFunctionSearchStarted(  
    [in]  FunctionID functionId,  
    [out] BOOL *pbUseCachedFunction);  
```  
  
## <a name="parameters"></a>Parametri

- `functionId`

  \[in] ID della funzione per la quale viene eseguita la ricerca.

- `pbUseCachedFunction`

  \[out] `true` se il motore di esecuzione deve usare la versione memorizzata nella cache di una funzione (se disponibile); in caso contrario, `false` . Se il valore è `false` , il motore di esecuzione compila la funzione in modalità JIT anziché usare una versione non compilata tramite JIT.

## <a name="remarks"></a>Osservazioni  
 Nella versione .NET Framework 2,0, i `JITCachedFunctionSearchStarted` callback del [metodo e ICorProfilerCallback:: JITCachedFunctionSearchFinished](icorprofilercallback-jitcachedfunctionsearchfinished-method.md) non verranno eseguiti per tutte le funzioni nelle immagini NGen normali. Solo le immagini NGen ottimizzate per un profilo genereranno callback per tutte le funzioni nell'immagine. Tuttavia, a causa dell'overhead aggiuntivo, un profiler deve richiedere immagini NGen ottimizzate per il profiler solo se intende usare questi callback per forzare la compilazione di una funzione JIT (just-in-Time). In caso contrario, il profiler deve usare una strategia Lazy per raccogliere informazioni sulle funzioni.  
  
 I profiler devono supportare i casi in cui più thread di un'applicazione profilata chiamano contemporaneamente lo stesso metodo. Ad esempio, il thread A chiama `JITCachedFunctionSearchStarted` e il profiler risponde impostando *PBUSECACHEDFUNCTION*su false per forzare la compilazione JIT. Il thread A chiama quindi [ICorProfilerCallback:: JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md) e [ICorProfilerCallback:: JITCompilationFinished](icorprofilercallback-jitcompilationfinished-method.md).  
  
 Ora il thread B chiama `JITCachedFunctionSearchStarted` per la stessa funzione. Anche se il profiler ha dichiarato l'intenzione di compilare in modo JIT la funzione, il profiler riceve il secondo callback perché il thread B invia il callback prima che il profiler abbia risposto alla chiamata del thread a `JITCachedFunctionSearchStarted` . L'ordine in cui i thread effettuano chiamate dipende dalla modalità di pianificazione dei thread.  
  
 Quando il profiler riceve callback duplicati, deve impostare il valore a cui fa riferimento lo `pbUseCachedFunction` stesso valore per tutti i callback duplicati. Ovvero, quando `JITCachedFunctionSearchStarted` viene chiamato più volte con lo stesso `functionId` valore, il profiler deve rispondere allo stesso ogni volta.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorProf.idl, CorProf.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfaccia ICorProfilerCallback](icorprofilercallback-interface.md)

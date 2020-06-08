---
title: Metodo ICorProfilerInfo3::SetEnterLeaveFunctionHooks3WithInfo
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.SetEnterLeaveFunctionHooks3WithInfo Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::SetEnterLeaveFunctionHooks3WithInfo
helpviewer_keywords:
- SetEnterLeaveFunctionHooks3WithInfo method [.NET Framework profiling]
- ICorProfilerInfo3::SetEnterLeaveFunctionHooks3WithInfo method [.NET Framework profiling]
ms.assetid: ca8ea534-e441-47b8-be85-466410988c0a
topic_type:
- apiref
ms.openlocfilehash: d40cb424306535cc502d930dd61e6a1e254667da
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496178"
---
# <a name="icorprofilerinfo3setenterleavefunctionhooks3withinfo-method"></a>Metodo ICorProfilerInfo3::SetEnterLeaveFunctionHooks3WithInfo
Specifica le funzioni implementate dal profiler che verranno chiamate sugli hook [FunctionEnter3WithInfo](functionenter3withinfo-function.md), [FunctionLeave3WithInfo](functionleave3withinfo-function.md)e [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md) delle funzioni gestite.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT SetEnterLeaveFunctionHooks3WithInfo(  
            [in] FunctionEnter3WithInfo    *pFuncEnter3,  
            [in] FunctionLeave3withInfo    *pFuncLeave3,  
            [in] FunctionTailcall3WithInfo *pFuncTailcall3);  
```  
  
## <a name="parameters"></a>Parametri  
 `pFuncEnter3`  
 in Puntatore all'implementazione da utilizzare come `FunctionEnter3WithInfo` callback.  
  
 `pFuncLeave3`  
 in Puntatore all'implementazione da utilizzare come `FunctionLeave3WithInfo` callback.  
  
 `pFuncTailcall3`  
 in Puntatore all'implementazione da utilizzare come `FunctionTailcall3WithInfo` callback.  
  
## <a name="remarks"></a>Osservazioni  
 Gli hook [FunctionEnter3WithInfo](functionenter3withinfo-function.md), [FunctionLeave3WithInfo](functionleave3withinfo-function.md)e [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md) forniscono stack frame e l'ispezione degli argomenti. Per accedere a tali informazioni, `COR_PRF_ENABLE_FUNCTION_ARGS` `COR_PRF_ENABLE_FUNCTION_RETVAL` è necessario impostare i flag, e/o `COR_PRF_ENABLE_FRAME_INFO` . Il profiler può usare il metodo [ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md) per impostare i flag di evento e quindi usare il `SetEnterLeaveFunctionHooks3WithInfo` metodo per registrare l'implementazione di questa funzione.  
  
 Solo un set di callback può essere attivo alla volta e la versione più recente ha la precedenza. Se pertanto un profiler chiama sia [SetEnterLeaveFunctionHooks2](icorprofilerinfo2-setenterleavefunctionhooks2-method.md) che `SetEnterLeaveFunctionHooks3WithInfo` , `SetEnterLeaveFunctionHooks3WithInfo` viene utilizzato.  
  
 Il `SetEnterLeaveFunctionHooks3WithInfo` metodo può essere chiamato solo dal callback [ICorProfilerCallback:: Initialize](icorprofilercallback-initialize-method.md) del profiler.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorProf.idl, CorProf.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [SetEnterLeaveFunctionHooks3](icorprofilerinfo3-setenterleavefunctionhooks3-method.md)
- [FunctionEnter3](functionenter3-function.md)
- [FunctionLeave3](functionleave3-function.md)
- [FunctionTailcall3](functiontailcall3-function.md)
- [FunctionEnter3WithInfo](functionenter3withinfo-function.md)
- [FunctionLeave3WithInfo](functionleave3withinfo-function.md)
- [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)
- [Funzioni statiche globali di profilatura](profiling-global-static-functions.md)
- [Interfaccia ICorProfilerInfo3](icorprofilerinfo3-interface.md)
- [Interfacce di profilatura](profiling-interfaces.md)
- [Profilatura](index.md)

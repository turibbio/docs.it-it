---
title: Metodo ICorProfilerInfo::GetILToNativeMapping
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetILToNativeMapping
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetILToNativeMapping
helpviewer_keywords:
- GetILToNativeMapping method, ICorProfilerInfo interface [.NET Framework profiling]
- ICorProfilerInfo::GetILToNativeMapping method [.NET Framework profiling]
ms.assetid: 6a5431ef-22fb-4e53-bac5-703986297eb1
topic_type:
- apiref
ms.openlocfilehash: b3c0bee44bf49c7966b8fefcfe6460c6255375c5
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502990"
---
# <a name="icorprofilerinfogetiltonativemapping-method"></a>Metodo ICorProfilerInfo::GetILToNativeMapping
Ottiene una mappa dagli offset MSIL (Microsoft Intermediate Language) agli offset nativi per il codice contenuto nella funzione specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT GetILToNativeMapping(  
    [in] FunctionID functionId,  
    [in] ULONG32 cMap,  
    [out] ULONG32 *pcMap,  
    [out, size_is(cMap), length_is(*pcMap)]  
        COR_DEBUG_IL_TO_NATIVE_MAP map[]);  
```  
  
## <a name="parameters"></a>Parametri  
 `functionId`  
 [in] ID della funzione che contiene il codice.  
  
 `cMap`  
 [in] Dimensione massima della matrice `map`.  
  
 `pcMap`  
 [out] Numero complessivo di strutture COR_DEBUG_IL_TO_NATIVE_MAP disponibili.  
  
 `map`  
 [out] Matrice di strutture `COR_DEBUG_IL_TO_NATIVE_MAP`, ognuna delle quali specifica gli offset. Dopo il completamento del metodo `GetILToNativeMapping`, `map` conterrà alcune o tutte le strutture `COR_DEBUG_IL_TO_NATIVE_MAP`.  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo `GetILToNativeMapping` restituisce una matrice di strutture `COR_DEBUG_IL_TO_NATIVE_MAP`. Per indicare che determinati intervalli di istruzioni native corrispondono a aree speciali di codice (ad esempio, il prologo), una voce nella matrice può avere il `ilOffset` campo impostato su un valore dell'enumerazione [CorDebugIlToNativeMappingTypes](../debugging/cordebugiltonativemappingtypes-enumeration.md) .  
  
 Dopo il completamento del metodo `GetILToNativeMapping`, è necessario verificare che il buffer `map` sia abbastanza grande per contenere tutte le strutture `COR_DEBUG_IL_TO_NATIVE_MAP`. A tale scopo, confrontare il valore di `cMap` con il valore del parametro `pcMap`. Se il valore `pcMap`, moltiplicato per la dimensione di una struttura `COR_DEBUG_IL_TO_NATIVE_MAP`, è superiore a `cMap`, allocare un buffer `map` più grande, aggiornare `cMap` con la nuova dimensione e chiamare nuovamente `GetILToNativeMapping`.  
  
 In alternativa, è possibile chiamare innanzitutto `GetILToNativeMapping` con un buffer `map` di lunghezza zero per ottenere le dimensioni del buffer corrette. È quindi possibile impostare le dimensioni del buffer sul valore restituito nel parametro `pcMap` e chiamare nuovamente `GetILToNativeMapping`.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorProf.idl, CorProf.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfaccia ICorProfilerInfo](icorprofilerinfo-interface.md)
- [Metodo GetILToNativeMapping2](icorprofilerinfo4-getiltonativemapping2-method.md)
- [Interfacce di profilatura](profiling-interfaces.md)
- [Profilatura](index.md)

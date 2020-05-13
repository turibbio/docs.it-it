---
title: Metodo ICorDebugProcess5::EnumerateHeap
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.EnumerateHeap
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnumerateHeap
helpviewer_keywords:
- EnumerateHeap method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::EnumerateHeap method [.NET Framework debugging]
ms.assetid: b0192104-6073-4089-a4df-dc29ee033074
topic_type:
- apiref
ms.openlocfilehash: 9386c77cc98df17d797d5886e1603ffc4824b6dc
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83205242"
---
# <a name="icordebugprocess5enumerateheap-method"></a>Metodo ICorDebugProcess5::EnumerateHeap
Ottiene un enumeratore per gli oggetti nell'heap gestito.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT EnumerateHeap(  
    [out] ICorDebugHeapEnum **ppObjects  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `ppObject`  
 out Puntatore all'indirizzo di un oggetto interfaccia [ICorDebugHeapEnum](icordebugheapenum-interface.md) che è un enumeratore per gli oggetti che risiedono nell'heap gestito.  
  
## <a name="remarks"></a>Osservazioni  
 Prima di chiamare il `ICorDebugProcess5::EnumerateHeap` metodo, è necessario chiamare il metodo [ICorDebugProcess5:: GetGCHeapInformation](icordebugprocess5-getgcheapinformation-method.md) ed esaminare il valore del `areGCStructuresValid` campo dell'oggetto [COR_HEAPINFO](cor-heapinfo-structure.md) restituito per assicurarsi che l'heap Garbage Collection nello stato corrente sia enumerabile. Inoltre, `ICorDebugProcess5::EnumerateHeap` restituisce `E_FAIL` se ci si connette troppo presto alla durata del processo, prima dell'allocazione della memoria per l'heap gestito.  
  
 L'oggetto interfaccia [ICorDebugHeapEnum](icordebugheapenum-interface.md) è un enumeratore standard derivato dall'interfaccia ICorDebugEnum che consente di enumerare [COR_HEAPOBJECT](cor-heapobject-structure.md) oggetti. Questo metodo popola l'oggetto raccolta [ICorDebugHeapEnum](icordebugheapenum-interface.md) con [COR_HEAPOBJECT](cor-heapobject-structure.md) istanze che forniscono informazioni su tutti gli oggetti. La raccolta può includere anche [COR_HEAPOBJECT](cor-heapobject-structure.md) istanze che forniscono informazioni sugli oggetti che non sono radice da alcun oggetto, ma che non sono stati ancora raccolti dall'Garbage Collector.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, CorDebug.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfaccia ICorDebugProcess5](icordebugprocess5-interface.md)
- [Interfacce di debug](debugging-interfaces.md)

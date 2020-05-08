---
title: Metodo ICorDebugEval::CreateValue
ms.date: 03/30/2017
api_name:
- ICorDebugEval.CreateValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::CreateValue
helpviewer_keywords:
- ICorDebugEval::CreateValue method [.NET Framework debugging]
- CreateValue method [.NET Framework debugging]
ms.assetid: 9a1c0b47-6f10-4fcb-844a-4ab2d7990140
topic_type:
- apiref
ms.openlocfilehash: 55888786fdd8ff2b1d5610a74ee729db0d4fcfde
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976252"
---
# <a name="icordebugevalcreatevalue-method"></a>Metodo ICorDebugEval::CreateValue
Crea un valore del tipo specificato, con un valore iniziale pari a zero o null.  
  
 Questo metodo è obsoleto nella versione .NET Framework 2,0. Usare invece [ICorDebugEval2:: CreateValueForType](icordebugeval2-createvaluefortype-method.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT CreateValue (  
    [in] CorElementType     elementType,  
    [in] ICorDebugClass     *pElementClass,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `elementType`  
 in Valore dell'enumerazione [CorElementType](../metadata/corelementtype-enumeration.md) che specifica il tipo del valore.  
  
 `pElementClass`  
 in Puntatore a un oggetto [ICorDebugClass](icordebugclass-interface.md) che specifica la classe del valore, se il tipo non è un tipo primitivo.  
  
 `ppValue`  
 out Puntatore all'indirizzo di un oggetto "ICorDebugValue" che rappresenta il valore.  
  
## <a name="remarks"></a>Osservazioni  
 `CreateValue`Crea un `ICorDebugValue` oggetto del tipo specificato per l'utilizzo esclusivo in una valutazione di funzione. Questo oggetto valore può essere utilizzato per passare le costanti utente come parametri.  
  
 Se il tipo del valore è un tipo primitivo, il valore iniziale è zero o null. Usare [ICorDebugGenericValue:: SetValue](icordebuggenericvalue-setvalue-method.md) per impostare il valore di un tipo primitivo.  
  
 Se il valore di `elementType` è ELEMENT_TYPE_CLASS, viene visualizzato un valore "ICorDebugReferenceValue" (restituito `ppValue`in) che rappresenta il riferimento all'oggetto null. È possibile utilizzare questo oggetto per passare valori null a una valutazione di funzione con parametri di riferimento a un oggetto. Non è possibile impostare `ICorDebugValue` su nulla; rimane sempre null.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, CorDebug.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:** 1,1, 1,0  
  
## <a name="see-also"></a>Vedere anche

- [Metodo CreateValueForType](icordebugeval2-createvaluefortype-method.md)
- [Interfaccia ICorDebugEval](icordebugeval-interface.md)

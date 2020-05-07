---
title: Metodo ICorDebugClass::GetStaticFieldValue
ms.date: 03/30/2017
api_name:
- ICorDebugClass.GetStaticFieldValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass::GetStaticFieldValue
helpviewer_keywords:
- GetStaticFieldValue method, ICorDebugClass interface [.NET Framework debugging]
- ICorDebugClass::GetStaticFieldValue method [.NET Framework debugging]
ms.assetid: 56e718b4-fabd-418b-a5b3-3cc33c745683
topic_type:
- apiref
ms.openlocfilehash: d4a254853256e1a1440f5588418b94e39eabcc9a
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894102"
---
# <a name="icordebugclassgetstaticfieldvalue-method"></a>Metodo ICorDebugClass::GetStaticFieldValue
Ottiene il valore del campo statico specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT GetStaticFieldValue (  
    [in]  mdFieldDef         fieldDef,  
    [in]  ICorDebugFrame     *pFrame,  
    [out] ICorDebugValue     **ppValue  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `fieldDef`  
 in Token di `Def` campo che fa riferimento al campo da recuperare.  
  
 `pFrame`  
 in Puntatore a un oggetto ICorDebugFrame che rappresenta il frame da usare per evitare ambiguità tra il thread, il contesto o gli elementi statici del dominio dell'applicazione.  
  
 Se il campo statico è relativo a un thread, a un contesto o a un dominio dell'applicazione, il frame determinerà il valore appropriato.  
  
 `ppValue`  
 out Puntatore all'indirizzo di un oggetto ICorDebugValue che rappresenta il valore del campo statico.  
  
## <a name="remarks"></a>Osservazioni  
 Per i tipi con parametri, il valore di un campo statico è relativo alla particolare creazione di istanza. Se pertanto il costruttore della classe accetta parametri di tipo <xref:System.Type>, chiamare [ICorDebugType:: GetStaticFieldValue](icordebugtype-getstaticfieldvalue-method.md) anziché `ICorDebugClass::GetStaticFieldValue`.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, CorDebug.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

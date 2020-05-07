---
title: Metodo ICorDebugClass2::SetJMCStatus
ms.date: 03/30/2017
api_name:
- ICorDebugClass2.SetJMCStatus
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass2::SetJMCStatus
helpviewer_keywords:
- ICorDebugClass2::SetJMCStatus method [.NET Framework debugging]
- SetJMCStatus method, ICorDebugClass2 interface [.NET Framework debugging]
ms.assetid: 077e6c7f-f857-480c-bebb-76ee1de4e8fc
topic_type:
- apiref
ms.openlocfilehash: 9fb2f960098e970b4d3d9f0be499f4d9fda6558e
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82893900"
---
# <a name="icordebugclass2setjmcstatus-method"></a>Metodo ICorDebugClass2::SetJMCStatus
Per ogni metodo della classe, imposta un valore che indica se il metodo è codice definito dall'utente.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT SetJMCStatus (  
    [in] BOOL   bIsJustMyCode  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `bIsJustMyCode`  
 in Impostare su `true` per indicare che il metodo è codice definito dall'utente; in caso contrario, `false`impostare su.  
  
## <a name="remarks"></a>Osservazioni  
 Un stepper (Just-My-Code) ignorerà il codice non definito dall'utente. Il codice definito dall'utente deve essere un subset del codice di cui è possibile eseguire il debug.  
  
 `SetJMCStatus`Restituisce un valore HRESULT di S_FALSE se non è possibile impostare il valore per qualsiasi metodo, anche se il valore viene impostato correttamente per tutti gli altri metodi.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, CorDebug.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]

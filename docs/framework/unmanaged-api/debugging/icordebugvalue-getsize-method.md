---
title: Metodo ICorDebugValue::GetSize
ms.date: 03/30/2017
api_name:
- ICorDebugValue.GetSize
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValue::GetSize
helpviewer_keywords:
- GetSize method, ICorDebugValue interface [.NET Framework debugging]
- ICorDebugValue::GetSize method [.NET Framework debugging]
ms.assetid: 445a9ee3-e050-4f3a-931a-96b0efb00110
topic_type:
- apiref
ms.openlocfilehash: 9ff7128f55236ae4d0c3a9067a279c496cfb6798
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396746"
---
# <a name="icordebugvaluegetsize-method"></a>Metodo ICorDebugValue::GetSize
Ottiene le dimensioni in byte di questo oggetto "ICorDebugValue".  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT GetSize (  
    [out] ULONG32   *pSize  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `pSize`  
 out Dimensione, in byte, di questo oggetto valore.  
  
## <a name="remarks"></a>Commenti  
 Se il tipo del valore è un tipo di riferimento, questo metodo restituisce le dimensioni del puntatore anziché le dimensioni dell'oggetto.  
  
 Il `ICorDebugValue::GetSize` metodo restituisce `COR_E_OVERFLOW` per oggetti di dimensioni maggiori di 4 GB su piattaforme a 64 bit. Usare invece il metodo [ICorDebugValue3:: GetSize64](icordebugvalue3-getsize64-method.md) per gli oggetti con dimensioni maggiori di 4 GB.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, CorDebug.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vedi anche

- [Metodo GetSize64](icordebugvalue3-getsize64-method.md)

---
title: Metodo ICorDebugNativeFrame2::IsChild
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame2.IsChild Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame2::IsChild
helpviewer_keywords:
- IsChild method [.NET Framework debugging]
- ICorDebugNativeFrame2::IsChild method [.NET Framework debugging]
ms.assetid: 9e2aae09-49cb-4fbd-81e5-e29cd864a88b
topic_type:
- apiref
ms.openlocfilehash: 759ba7bd46f8231143e743aa5ffcabffeb99c3b6
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83205104"
---
# <a name="icordebugnativeframe2ischild-method"></a>Metodo ICorDebugNativeFrame2::IsChild
Determina se il frame corrente è un frame figlio.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT IsChild([out] BOOL * pIsChild);  
```  
  
## <a name="parameters"></a>Parametri  
 `pIsChild`  
 out Valore booleano che specifica se il frame corrente è un frame figlio.  
  
## <a name="return-value"></a>Valore restituito  
 Questo metodo restituisce gli specifici HRESULT seguenti, nonché gli errori di HRESULT che indicano la mancata riuscita del metodo.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|Stato figlio restituito correttamente.|  
|E_FAIL|Non è stato possibile restituire lo stato figlio.|  
|E_INVALIDARG|`pIsChild` è null.|  
  
## <a name="exceptions"></a>Eccezioni  
  
## <a name="remarks"></a>Osservazioni  
 Il `IsChild` metodo restituisce `true` se l'oggetto frame su cui si chiama il metodo è un elemento figlio di un altro frame. In tal caso, utilizzare il metodo [IsMatchingParentFrame](icordebugnativeframe2-ismatchingparentframe-method.md) per verificare se un frame è il relativo elemento padre.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, CorDebug.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfaccia ICorDebugNativeFrame2](icordebugnativeframe2-interface.md)
- [Interfacce di debug](debugging-interfaces.md)
- [Debug](index.md)

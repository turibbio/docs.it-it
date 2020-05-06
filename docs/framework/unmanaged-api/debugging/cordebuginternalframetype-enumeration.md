---
title: Enumerazione CorDebugInternalFrameType
ms.date: 03/30/2017
api_name:
- CorDebugInternalFrameType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugInternalFrameType
helpviewer_keywords:
- CorDebugInternalFrameType enumeration [.NET Framework debugging]
ms.assetid: e4412dc2-c338-4cfb-94d8-f682095dd2b1
topic_type:
- apiref
ms.openlocfilehash: 4a65a98ee04c3870dae2f49b3da2a8e72b1ffae4
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795833"
---
# <a name="cordebuginternalframetype-enumeration"></a>Enumerazione CorDebugInternalFrameType
Identifica il tipo di stack frame. Questa enumerazione viene utilizzata dal metodo [ICorDebugInternalFrame:: GetFrameType](icordebuginternalframe-getframetype-method.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
typedef enum CorDebugInternalFrameType {  
  
    STUBFRAME_NONE                 = 0x00000000,  
    STUBFRAME_M2U                  = 0x00000001,  
    STUBFRAME_U2M                  = 0x00000002,  
    STUBFRAME_APPDOMAIN_TRANSITION = 0x00000003,  
    STUBFRAME_LIGHTWEIGHT_FUNCTION = 0x00000004,  
    STUBFRAME_FUNC_EVAL            = 0x00000005,  
    STUBFRAME_INTERNALCALL         = 0x00000006,  
    STUBFRAME_CLASS_INIT           = 0x00000007,  
    STUBFRAME_EXCEPTION            = 0x00000008,  
    STUBFRAME_SECURITY             = 0x00000009,  
    STUBFRAME_JIT_COMPILATION     = 0x0000000a,  
} CorDebugInternalFrameType;  
```  
  
## <a name="members"></a>Members  
  
|Membro|Description|  
|------------|-----------------|  
|`STUBFRAME_NONE`|Valore null. Il `ICorDebugInternalFrame::GetFrameType` metodo non restituisce mai questo valore.|  
|`STUBFRAME_M2U`|Frame dello stub gestito da gestito a non gestito.|  
|`STUBFRAME_U2M`|Frame stub non gestito.|  
|`STUBFRAME_APPDOMAIN_TRANSITION`|Transizione tra domini dell'applicazione.|  
|`STUBFRAME_LIGHTWEIGHT_FUNCTION`|Una chiamata al metodo Lightweight.|  
|`STUBFRAME_FUNC_EVAL`|Inizio della valutazione della funzione.|  
|`STUBFRAME_INTERNALCALL`|Una chiamata interna all'Common Language Runtime.|  
|`STUBFRAME_CLASS_INIT`|Inizio dell'inizializzazione di una classe.|  
|`STUBFRAME_EXCEPTION`|Eccezione generata.|  
|`STUBFRAME_SECURITY`|Frame utilizzato per la sicurezza dall'accesso di codice.|  
|`STUBFRAME_JIT_COMPILATION`|Il Runtime sta eseguendo la compilazione JIT di un metodo.|  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, CorDebug.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Enumerazioni di debug](debugging-enumerations.md)

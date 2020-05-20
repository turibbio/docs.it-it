---
title: Struttura USER_THREAD
ms.date: 03/30/2017
api_name:
- USER_THREAD
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- USER_THREAD
helpviewer_keywords:
- USER_THREAD structure [.NET Framework debugging]
ms.assetid: a57c7d71-c4b0-41f9-a964-0c5ee84a3124
topic_type:
- apiref
ms.openlocfilehash: 5144feab742bc5dac36563d701d81a699d0bb2f3
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83609443"
---
# <a name="user_thread-structure"></a>Struttura USER_THREAD
Fornisce informazioni a un debugger relativo a un thread. Per ulteriori informazioni, vedere il metodo [INotifySource2:: SetNotifyFilter](inotifysource2-setnotifyfilter-method.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
typedef struct tagUSER_THREAD  
{  
    BYTE    *pSidBuffer;  
    DWORD   dwSidLen;  
    DWORD   dwTid;  
} USER_THREAD;  
```  
  
## <a name="members"></a>Membri  
  
|Membro|Description|  
|------------|-----------------|  
|`pSidBuffer`|Indirizzo del buffer del thread.|  
|`dwSidLen`|Lunghezza del buffer del thread, in byte.|  
|`dwTid`|ID thread.|  
  
## <a name="requirements"></a>Requisiti  
 **Intestazione:** ProtocolNotify2. idl  
  
## <a name="see-also"></a>Vedere anche

- [Metodo SetNotifyFilter](inotifysource2-setnotifyfilter-method.md)
- [Strutture dell'archivio simboli di diagnostica](diagnostics-symbol-store-structures.md)

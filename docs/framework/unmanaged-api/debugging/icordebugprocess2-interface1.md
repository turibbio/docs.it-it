---
title: Interfaccia ICorDebugProcess2
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2
helpviewer_keywords:
- ICorDebugProcess2 interface [.NET Framework debugging]
ms.assetid: 73332138-5fea-441f-b893-61af87d45a42
topic_type:
- apiref
ms.openlocfilehash: 1a57b7ceb6da961fba1f0d6e8e0ba1aa88ca0541
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213491"
---
# <a name="icordebugprocess2-interface"></a>Interfaccia ICorDebugProcess2
Estensione logica dell'interfaccia ICorDebugProcess, che rappresenta un processo che esegue codice gestito.  
  
## <a name="methods"></a>Metodi  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[Metodo ClearUnmanagedBreakpoint](icordebugprocess2-clearunmanagedbreakpoint-method.md)|Rimuove un punto di interruzione in corrispondenza dell'offset specificato impostato da una chiamata precedente a `ICorDebugProcess2::SetUnmanagedBreakpoint` .|  
|[Metodo GetDesiredNGENCompilerFlags](icordebugprocess2-getdesiredngencompilerflags-method.md)|Ottiene i flag che devono essere impostati per il Common Language Runtime (CLR) per caricare l'immagine nel processo a cui fa riferimento questo oggetto `ICorDebugProcess2` .|  
|[Metodo GetReferenceValueFromGCHandle](icordebugprocess2-getreferencevaluefromgchandle-method.md)|Ottiene un puntatore di riferimento all'oggetto gestito specificato con un handle Garbage Collection.|  
|[Metodo GetThreadForTaskID](icordebugprocess2-getthreadfortaskid-method.md)|Ottiene il thread su cui è in esecuzione l'attività con l'identificatore specificato.|  
|[Metodo GetVersion](icordebugprocess2-getversion-method.md)|Ottiene la versione di CLR su cui è in esecuzione il processo di cui è in corso il debug.|  
|[Metodo SetDesiredNGENCompilerFlags](icordebugprocess2-setdesiredngencompilerflags-method.md)|Imposta i flag necessari per il compilatore JIT (just-in-Time) per caricare un'immagine nel processo di cui è in corso il debug.|  
|[Metodo SetUnmanagedBreakpoint](icordebugprocess2-setunmanagedbreakpoint-method.md)|Imposta un punto di interruzione non gestito in corrispondenza dell'offset dell'immagine nativa specificato.|  
  
## <a name="remarks"></a>Osservazioni  
  
> [!NOTE]
> Questa interfaccia non supporta la chiamata in modalità remota, tra computer o tra processi.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, CorDebug.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfacce di debug](debugging-interfaces.md)

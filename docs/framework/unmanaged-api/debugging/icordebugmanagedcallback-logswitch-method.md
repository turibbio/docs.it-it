---
title: Metodo ICorDebugManagedCallback::LogSwitch
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.LogSwitch
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::LogSwitch
helpviewer_keywords:
- LogSwitch method [.NET Framework debugging]
- ICorDebugManagedCallback::LogSwitch method [.NET Framework debugging]
ms.assetid: 0ac59d27-783f-4a87-b7a8-baa3ccc54582
topic_type:
- apiref
ms.openlocfilehash: f095bc0272e0e6f16467b9758d5e392d371139dd
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212685"
---
# <a name="icordebugmanagedcallbacklogswitch-method"></a><span data-ttu-id="36ba3-102">Metodo ICorDebugManagedCallback::LogSwitch</span><span class="sxs-lookup"><span data-stu-id="36ba3-102">ICorDebugManagedCallback::LogSwitch Method</span></span>
<span data-ttu-id="36ba3-103">Notifica al debugger che un thread gestito di Common Language Runtime (CLR) ha chiamato un metodo nella <xref:System.Diagnostics.Switch> classe per creare, modificare o eliminare un'opzione di debug/traccia.</span><span class="sxs-lookup"><span data-stu-id="36ba3-103">Notifies the debugger that a common language runtime (CLR) managed thread has called a method in the <xref:System.Diagnostics.Switch> class to create, modify, or delete a debugging/tracing switch.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="36ba3-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="36ba3-104">Syntax</span></span>  
  
```cpp  
HRESULT LogSwitch (  
    [in] ICorDebugAppDomain  *pAppDomain,  
    [in] ICorDebugThread     *pThread,  
    [in] LONG                 lLevel,  
    [in] ULONG                ulReason,  
    [in] WCHAR               *pLogSwitchName,  
    [in] WCHAR               *pParentName);  
```  
  
## <a name="parameters"></a><span data-ttu-id="36ba3-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="36ba3-105">Parameters</span></span>  
 `PAppDomain`  
 <span data-ttu-id="36ba3-106">in Puntatore a un oggetto ICorDebugAppDomain che rappresenta il dominio applicazione contenente il thread gestito che ha creato, modificato o eliminato un'opzione di debug/traccia.</span><span class="sxs-lookup"><span data-stu-id="36ba3-106">[in] A pointer to an ICorDebugAppDomain object that represents the application domain containing the managed thread that created, modified, or deleted a debugging/tracing switch.</span></span>  
  
 `pThread`  
 <span data-ttu-id="36ba3-107">in Puntatore a un oggetto ICorDebugThread che rappresenta il thread gestito.</span><span class="sxs-lookup"><span data-stu-id="36ba3-107">[in] A pointer to an ICorDebugThread object that represents the managed thread.</span></span>  
  
 `lLevel`  
 <span data-ttu-id="36ba3-108">in Valore che indica il livello di gravità del messaggio descrittivo che è stato scritto nel log eventi.</span><span class="sxs-lookup"><span data-stu-id="36ba3-108">[in] A value that indicates the severity level of the descriptive message that was written to the event log.</span></span>  
  
 `ulReason`  
 <span data-ttu-id="36ba3-109">in Valore dell'enumerazione [LogSwitchCallReason](logswitchcallreason-enumeration.md) che indica l'operazione eseguita sull'opzione di debug/traccia.</span><span class="sxs-lookup"><span data-stu-id="36ba3-109">[in] A value of the [LogSwitchCallReason](logswitchcallreason-enumeration.md) enumeration that indicates the operation performed on the debugging/tracing switch.</span></span>  
  
 `pLogSwitchName`  
 <span data-ttu-id="36ba3-110">in Puntatore al nome dell'opzione di debug/traccia.</span><span class="sxs-lookup"><span data-stu-id="36ba3-110">[in] A pointer to the name of the debugging/tracing switch.</span></span>  
  
 `pParentName`  
 <span data-ttu-id="36ba3-111">in Puntatore al nome dell'elemento padre dell'opzione di debug/traccia.</span><span class="sxs-lookup"><span data-stu-id="36ba3-111">[in] A pointer to the name of the parent of the debugging/tracing switch.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="36ba3-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="36ba3-112">Requirements</span></span>  
 <span data-ttu-id="36ba3-113">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="36ba3-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="36ba3-114">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="36ba3-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="36ba3-115">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="36ba3-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="36ba3-116">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="36ba3-116">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="36ba3-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="36ba3-117">See also</span></span>

- [<span data-ttu-id="36ba3-118">Interfaccia ICorDebugManagedCallback</span><span class="sxs-lookup"><span data-stu-id="36ba3-118">ICorDebugManagedCallback Interface</span></span>](icordebugmanagedcallback-interface.md)

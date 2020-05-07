---
title: Interfaccia ICorDebugController
ms.date: 03/30/2017
api_name:
- ICorDebugController
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController
helpviewer_keywords:
- ICorDebugController interface [.NET Framework debugging]
ms.assetid: dbb1c4dc-269a-459b-ab1d-6c70788782ce
topic_type:
- apiref
ms.openlocfilehash: e494bbb24e8f2245593e7945625e72e70ae1dde5
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82892764"
---
# <a name="icordebugcontroller-interface"></a><span data-ttu-id="ef0f6-102">Interfaccia ICorDebugController</span><span class="sxs-lookup"><span data-stu-id="ef0f6-102">ICorDebugController Interface</span></span>

<span data-ttu-id="ef0f6-103">Rappresenta un ambito, ossia <xref:System.Diagnostics.Process> o <xref:System.AppDomain>, in cui è possibile controllare il contesto di esecuzione del codice.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-103">Represents a scope, either a <xref:System.Diagnostics.Process> or an <xref:System.AppDomain>, in which code execution context can be controlled.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="ef0f6-104">Metodi</span><span class="sxs-lookup"><span data-stu-id="ef0f6-104">Methods</span></span>  
  
|<span data-ttu-id="ef0f6-105">Metodo</span><span class="sxs-lookup"><span data-stu-id="ef0f6-105">Method</span></span>|<span data-ttu-id="ef0f6-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ef0f6-106">Description</span></span>|  
|------------|-----------------|  
|`ICorDebugController::CanCommitChanges`|<span data-ttu-id="ef0f6-107">Questo metodo è obsoleto.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-107">This method is obsolete.</span></span>|  
|`ICorDebugController::CommitChanges`|<span data-ttu-id="ef0f6-108">Questo metodo è obsoleto.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-108">This method is obsolete.</span></span>|  
|[<span data-ttu-id="ef0f6-109">Metodo Continue</span><span class="sxs-lookup"><span data-stu-id="ef0f6-109">Continue Method</span></span>](icordebugcontroller-continue-method.md)|<span data-ttu-id="ef0f6-110">Riprende l'esecuzione di thread gestiti dopo una chiamata a [ICorDebugController:: Stop](icordebugcontroller-stop-method.md).</span><span class="sxs-lookup"><span data-stu-id="ef0f6-110">Resumes execution of managed threads after a call to [ICorDebugController::Stop](icordebugcontroller-stop-method.md).</span></span>|  
|[<span data-ttu-id="ef0f6-111">Metodo Detach</span><span class="sxs-lookup"><span data-stu-id="ef0f6-111">Detach Method</span></span>](icordebugcontroller-detach-method.md)|<span data-ttu-id="ef0f6-112">Scollega il debugger dal dominio del processo o dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-112">Detaches the debugger from the process or application domain.</span></span>|  
|[<span data-ttu-id="ef0f6-113">Metodo EnumerateThreads</span><span class="sxs-lookup"><span data-stu-id="ef0f6-113">EnumerateThreads Method</span></span>](icordebugcontroller-enumeratethreads-method.md)|<span data-ttu-id="ef0f6-114">Ottiene un enumeratore per i thread gestiti attivi nel processo.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-114">Gets an enumerator for the active managed threads in the process.</span></span>|  
|[<span data-ttu-id="ef0f6-115">Metodo HasQueuedCallbacks</span><span class="sxs-lookup"><span data-stu-id="ef0f6-115">HasQueuedCallbacks Method</span></span>](icordebugcontroller-hasqueuedcallbacks-method.md)|<span data-ttu-id="ef0f6-116">Ottiene un valore che indica se i callback gestiti sono attualmente in coda per il thread specificato.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-116">Gets a value that indicates whether any managed callbacks are currently queued for the specified thread.</span></span>|  
|[<span data-ttu-id="ef0f6-117">Metodo IsRunning</span><span class="sxs-lookup"><span data-stu-id="ef0f6-117">IsRunning Method</span></span>](icordebugcontroller-isrunning-method.md)|<span data-ttu-id="ef0f6-118">Ottiene un valore che indica se i thread del processo sono attualmente in esecuzione liberamente.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-118">Gets a value that indicates whether the threads in the process are currently running freely.</span></span>|  
|[<span data-ttu-id="ef0f6-119">Metodo SetAllThreadsDebugState</span><span class="sxs-lookup"><span data-stu-id="ef0f6-119">SetAllThreadsDebugState Method</span></span>](icordebugcontroller-setallthreadsdebugstate-method.md)|<span data-ttu-id="ef0f6-120">Imposta lo stato di debug di tutti i thread gestiti nel processo.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-120">Sets the debug state of all managed threads in the process.</span></span>|  
|[<span data-ttu-id="ef0f6-121">Metodo Stop</span><span class="sxs-lookup"><span data-stu-id="ef0f6-121">Stop Method</span></span>](icordebugcontroller-stop-method.md)|<span data-ttu-id="ef0f6-122">Esegue un arresto cooperativo su tutti i thread che eseguono codice gestito nel processo.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-122">Performs a cooperative stop on all threads that are running managed code in the process.</span></span>|  
|[<span data-ttu-id="ef0f6-123">Metodo Terminate</span><span class="sxs-lookup"><span data-stu-id="ef0f6-123">Terminate Method</span></span>](icordebugcontroller-terminate-method.md)|<span data-ttu-id="ef0f6-124">Termina il processo con il codice di uscita specificato.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-124">Terminates the process with the specified exit code.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="ef0f6-125">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="ef0f6-125">Remarks</span></span>  
 <span data-ttu-id="ef0f6-126">Se `ICorDebugController` controlla un processo, l'ambito include tutti i thread del processo.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-126">If `ICorDebugController` is controlling a process, the scope includes all threads of the process.</span></span> <span data-ttu-id="ef0f6-127">Se `ICorDebugController` controlla un dominio applicazione, l'ambito include solo i thread di quel particolare dominio applicazione.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-127">If `ICorDebugController` is controlling an application domain, the scope includes only the threads of that particular application domain.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ef0f6-128">Questa interfaccia non supporta la chiamata in modalità remota, tra computer o tra processi.</span><span class="sxs-lookup"><span data-stu-id="ef0f6-128">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ef0f6-129">Requisiti</span><span class="sxs-lookup"><span data-stu-id="ef0f6-129">Requirements</span></span>  
 <span data-ttu-id="ef0f6-130">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ef0f6-130">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ef0f6-131">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="ef0f6-131">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="ef0f6-132">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="ef0f6-132">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ef0f6-133">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ef0f6-133">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ef0f6-134">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ef0f6-134">See also</span></span>

- [<span data-ttu-id="ef0f6-135">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="ef0f6-135">Debugging Interfaces</span></span>](debugging-interfaces.md)

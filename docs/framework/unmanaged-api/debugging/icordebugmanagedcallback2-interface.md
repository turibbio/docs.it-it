---
title: Interfaccia ICorDebugManagedCallback2
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2
helpviewer_keywords:
- ICorDebugManagedCallback2 interface [.NET Framework debugging]
ms.assetid: cf7b7cfa-1c4b-4d8c-be70-4f9ed15a788b
topic_type:
- apiref
ms.openlocfilehash: b00be90316598e458f01f6cd440d0ad0a2e79c50
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212360"
---
# <a name="icordebugmanagedcallback2-interface"></a><span data-ttu-id="0866f-102">Interfaccia ICorDebugManagedCallback2</span><span class="sxs-lookup"><span data-stu-id="0866f-102">ICorDebugManagedCallback2 Interface</span></span>
<span data-ttu-id="0866f-103">Fornisce metodi che supportano la gestione delle eccezioni del debugger e assistenti al debug gestito.</span><span class="sxs-lookup"><span data-stu-id="0866f-103">Provides methods to support debugger exception handling and managed debugging assistants (MDAs).</span></span> <span data-ttu-id="0866f-104">`ICorDebugManagedCallback2`è un'estensione logica dell'interfaccia [ICorDebugManagedCallback](icordebugmanagedcallback-interface.md) .</span><span class="sxs-lookup"><span data-stu-id="0866f-104">`ICorDebugManagedCallback2` is a logical extension of the [ICorDebugManagedCallback](icordebugmanagedcallback-interface.md) interface.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="0866f-105">Metodi</span><span class="sxs-lookup"><span data-stu-id="0866f-105">Methods</span></span>  
  
|<span data-ttu-id="0866f-106">Metodo</span><span class="sxs-lookup"><span data-stu-id="0866f-106">Method</span></span>|<span data-ttu-id="0866f-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0866f-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="0866f-108">Metodo ChangeConnection</span><span class="sxs-lookup"><span data-stu-id="0866f-108">ChangeConnection Method</span></span>](icordebugmanagedcallback2-changeconnection-method.md)|<span data-ttu-id="0866f-109">Notifica al debugger che è stato modificato il set di attività associato alla connessione specificata.</span><span class="sxs-lookup"><span data-stu-id="0866f-109">Notifies the debugger that the set of tasks associated with the specified connection has changed.</span></span>|  
|[<span data-ttu-id="0866f-110">Metodo CreateConnection</span><span class="sxs-lookup"><span data-stu-id="0866f-110">CreateConnection Method</span></span>](icordebugmanagedcallback2-createconnection-method.md)|<span data-ttu-id="0866f-111">Notifica al debugger che è stata creata una nuova connessione.</span><span class="sxs-lookup"><span data-stu-id="0866f-111">Notifies the debugger that a new connection has been created.</span></span>|  
|[<span data-ttu-id="0866f-112">Metodo DestroyConnection</span><span class="sxs-lookup"><span data-stu-id="0866f-112">DestroyConnection Method</span></span>](icordebugmanagedcallback2-destroyconnection-method.md)|<span data-ttu-id="0866f-113">Notifica al debugger che la connessione specificata è stata terminata.</span><span class="sxs-lookup"><span data-stu-id="0866f-113">Notifies the debugger that the specified connection has been terminated.</span></span>|  
|[<span data-ttu-id="0866f-114">Metodo Exception</span><span class="sxs-lookup"><span data-stu-id="0866f-114">Exception Method</span></span>](icordebugmanagedcallback2-exception-method.md)|<span data-ttu-id="0866f-115">Notifica al debugger che è stata avviata una ricerca di un gestore di eccezioni.</span><span class="sxs-lookup"><span data-stu-id="0866f-115">Notifies the debugger that a search for an exception handler has started.</span></span>|  
|[<span data-ttu-id="0866f-116">Metodo ExceptionUnwind</span><span class="sxs-lookup"><span data-stu-id="0866f-116">ExceptionUnwind Method</span></span>](icordebugmanagedcallback2-exceptionunwind-method.md)|<span data-ttu-id="0866f-117">Fornisce una notifica di stato durante il processo di rimozione dell'eccezione.</span><span class="sxs-lookup"><span data-stu-id="0866f-117">Provides a status notification during the exception unwinding process.</span></span>|  
|[<span data-ttu-id="0866f-118">Metodo FunctionRemapComplete</span><span class="sxs-lookup"><span data-stu-id="0866f-118">FunctionRemapComplete Method</span></span>](icordebugmanagedcallback2-functionremapcomplete-method.md)|<span data-ttu-id="0866f-119">Notifica al debugger che l'esecuzione del codice è cambiata a una nuova versione di una funzione modificata.</span><span class="sxs-lookup"><span data-stu-id="0866f-119">Notifies the debugger that code execution has switched to a new version of an edited function.</span></span>|  
|[<span data-ttu-id="0866f-120">Metodo FunctionRemapOpportunity</span><span class="sxs-lookup"><span data-stu-id="0866f-120">FunctionRemapOpportunity Method</span></span>](icordebugmanagedcallback2-functionremapopportunity-method.md)|<span data-ttu-id="0866f-121">Notifica al debugger che l'esecuzione del codice ha raggiunto un punto di sequenza in una versione precedente di una funzione modificata.</span><span class="sxs-lookup"><span data-stu-id="0866f-121">Notifies the debugger that code execution has reached a sequence point in an older version of an edited function.</span></span>|  
|[<span data-ttu-id="0866f-122">Metodo MDANotification</span><span class="sxs-lookup"><span data-stu-id="0866f-122">MDANotification Method</span></span>](icordebugmanagedcallback2-mdanotification-method.md)|<span data-ttu-id="0866f-123">Fornisce la notifica che l'esecuzione del codice ha rilevato un messaggio assistente al debug gestito (MDA).</span><span class="sxs-lookup"><span data-stu-id="0866f-123">Provides notification that code execution has encountered a managed debugging assistant (MDA) message.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="0866f-124">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="0866f-124">Remarks</span></span>  
 <span data-ttu-id="0866f-125">L' `ICorDebugManagedCallback2` interfaccia estende l' `ICorDebugManagedCallback` interfaccia per gestire i nuovi eventi di debug introdotti nella versione .NET Framework 2,0.</span><span class="sxs-lookup"><span data-stu-id="0866f-125">The `ICorDebugManagedCallback2` interface extends the `ICorDebugManagedCallback` interface to handle new debug events introduced in the .NET Framework version 2.0.</span></span>  
  
 <span data-ttu-id="0866f-126">Un debugger deve implementare `ICorDebugManagedCallback2` se esegue il debug di applicazioni .NET Framework 2,0.</span><span class="sxs-lookup"><span data-stu-id="0866f-126">A debugger must implement `ICorDebugManagedCallback2` if it is debugging .NET Framework 2.0 applications.</span></span> <span data-ttu-id="0866f-127">Un'istanza di `ICorDebugManagedCallback` o `ICorDebugManagedCallback2` viene passata come oggetto callback a [ICorDebug:: SetManagedHandler](icordebug-setmanagedhandler-method.md).</span><span class="sxs-lookup"><span data-stu-id="0866f-127">An instance of `ICorDebugManagedCallback` or `ICorDebugManagedCallback2` is passed as the callback object to [ICorDebug::SetManagedHandler](icordebug-setmanagedhandler-method.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="0866f-128">Questa interfaccia non supporta la chiamata in modalità remota, tra computer o tra processi.</span><span class="sxs-lookup"><span data-stu-id="0866f-128">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="0866f-129">Requisiti</span><span class="sxs-lookup"><span data-stu-id="0866f-129">Requirements</span></span>  
 <span data-ttu-id="0866f-130">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="0866f-130">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="0866f-131">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="0866f-131">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="0866f-132">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="0866f-132">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="0866f-133">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="0866f-133">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0866f-134">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0866f-134">See also</span></span>

- [<span data-ttu-id="0866f-135">Diagnostica degli errori tramite gli assistenti al debug gestito</span><span class="sxs-lookup"><span data-stu-id="0866f-135">Diagnosing Errors with Managed Debugging Assistants</span></span>](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
- [<span data-ttu-id="0866f-136">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="0866f-136">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="0866f-137">Interfaccia ICorDebugManagedCallback</span><span class="sxs-lookup"><span data-stu-id="0866f-137">ICorDebugManagedCallback Interface</span></span>](icordebugmanagedcallback-interface.md)

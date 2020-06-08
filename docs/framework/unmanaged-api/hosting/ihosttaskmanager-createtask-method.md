---
title: Metodo IHostTaskManager::CreateTask
ms.date: 03/30/2017
api_name:
- IHostTaskManager.CreateTask
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::CreateTask
helpviewer_keywords:
- CreateTask method, IHostTaskManager interface [.NET Framework hosting]
- IHostTaskManager::CreateTask method [.NET Framework hosting]
ms.assetid: a6f8ad36-61e1-42b0-9db2-add575646d18
topic_type:
- apiref
ms.openlocfilehash: 4037ffe63d8ebfca67cbd0b3293d36be7481b1bd
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501417"
---
# <a name="ihosttaskmanagercreatetask-method"></a><span data-ttu-id="e6026-102">Metodo IHostTaskManager::CreateTask</span><span class="sxs-lookup"><span data-stu-id="e6026-102">IHostTaskManager::CreateTask Method</span></span>
<span data-ttu-id="e6026-103">Richiede che l'host crei una nuova attività.</span><span class="sxs-lookup"><span data-stu-id="e6026-103">Requests that the host create a new task.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e6026-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="e6026-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateTask (  
    [in]  DWORD stacksize,
    [in]  LPTHREAD_START_ROUTINE pStartAddress,  
    [in]  PVOID pParameter,  
    [out] IHostTask **ppTask  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e6026-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="e6026-105">Parameters</span></span>  
 `stacksize`  
 <span data-ttu-id="e6026-106">in Dimensioni richieste, in byte, dello stack richiesto o 0 (zero) per le dimensioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="e6026-106">[in] The requested size, in bytes, of the requested stack, or 0 (zero) for the default size.</span></span>  
  
 `pStartAddress`  
 <span data-ttu-id="e6026-107">in Puntatore alla funzione che deve essere eseguita dall'attività.</span><span class="sxs-lookup"><span data-stu-id="e6026-107">[in] A pointer to the function the task is to execute.</span></span>  
  
 `pParameter`  
 <span data-ttu-id="e6026-108">in Puntatore ai dati utente da passare alla funzione oppure null se la funzione non accetta parametri.</span><span class="sxs-lookup"><span data-stu-id="e6026-108">[in] A pointer to the user data to be passed to the function, or null if the function takes no parameters.</span></span>  
  
 `ppTask`  
 <span data-ttu-id="e6026-109">out Puntatore all'indirizzo di un'istanza di [IHostTask](ihosttask-interface.md) creato dall'host oppure null se non è possibile creare l'attività.</span><span class="sxs-lookup"><span data-stu-id="e6026-109">[out] A pointer to the address of an [IHostTask](ihosttask-interface.md) instance created by the host, or null if the task cannot be created.</span></span> <span data-ttu-id="e6026-110">L'attività rimane in stato sospeso fino a quando non viene avviata in modo esplicito da una chiamata a [IHostTask:: Start](ihosttask-start-method.md).</span><span class="sxs-lookup"><span data-stu-id="e6026-110">The task remains in a suspended state until it is explicitly started by a call to [IHostTask::Start](ihosttask-start-method.md).</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="e6026-111">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="e6026-111">Return Value</span></span>  
  
|<span data-ttu-id="e6026-112">HRESULT</span><span class="sxs-lookup"><span data-stu-id="e6026-112">HRESULT</span></span>|<span data-ttu-id="e6026-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e6026-113">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="e6026-114">S_OK</span><span class="sxs-lookup"><span data-stu-id="e6026-114">S_OK</span></span>|<span data-ttu-id="e6026-115">`CreateTask`la restituzione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="e6026-115">`CreateTask` returned successfully.</span></span>|  
|<span data-ttu-id="e6026-116">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="e6026-116">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="e6026-117">Il Common Language Runtime (CLR) non è stato caricato in un processo oppure CLR si trova in uno stato in cui non è possibile eseguire codice gestito o elaborare la chiamata correttamente.</span><span class="sxs-lookup"><span data-stu-id="e6026-117">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="e6026-118">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="e6026-118">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="e6026-119">Timeout della chiamata.</span><span class="sxs-lookup"><span data-stu-id="e6026-119">The call timed out.</span></span>|  
|<span data-ttu-id="e6026-120">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="e6026-120">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="e6026-121">Il chiamante non è il proprietario del blocco.</span><span class="sxs-lookup"><span data-stu-id="e6026-121">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="e6026-122">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="e6026-122">HOST_E_ABANDONED</span></span>|<span data-ttu-id="e6026-123">Un evento è stato annullato mentre un thread bloccato o Fiber era in attesa su di esso.</span><span class="sxs-lookup"><span data-stu-id="e6026-123">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="e6026-124">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="e6026-124">E_FAIL</span></span>|<span data-ttu-id="e6026-125">Si è verificato un errore irreversibile sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="e6026-125">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="e6026-126">Quando un metodo restituisce E_FAIL, CLR non è più utilizzabile all'interno del processo.</span><span class="sxs-lookup"><span data-stu-id="e6026-126">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="e6026-127">Le chiamate successive ai metodi di hosting restituiscono HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="e6026-127">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="e6026-128">E_OUTOFMEMORY</span><span class="sxs-lookup"><span data-stu-id="e6026-128">E_OUTOFMEMORY</span></span>|<span data-ttu-id="e6026-129">Memoria insufficiente per creare l'attività richiesta.</span><span class="sxs-lookup"><span data-stu-id="e6026-129">Not enough memory was available to create the requested task.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e6026-130">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="e6026-130">Remarks</span></span>  
 <span data-ttu-id="e6026-131">CLR chiama `CreateTask` per richiedere che l'host crei una nuova attività.</span><span class="sxs-lookup"><span data-stu-id="e6026-131">The CLR calls `CreateTask` to request that the host create a new task.</span></span> <span data-ttu-id="e6026-132">L'host restituisce un puntatore a interfaccia a un' `IHostTask` istanza di.</span><span class="sxs-lookup"><span data-stu-id="e6026-132">The host returns an interface pointer to an `IHostTask` instance.</span></span> <span data-ttu-id="e6026-133">L'attività restituita deve rimanere sospesa fino a quando non viene avviata in modo esplicito da una chiamata a `IHostTask::Start` .</span><span class="sxs-lookup"><span data-stu-id="e6026-133">The returned task must remain suspended until it is explicitly started by a call to `IHostTask::Start`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e6026-134">Requisiti</span><span class="sxs-lookup"><span data-stu-id="e6026-134">Requirements</span></span>  
 <span data-ttu-id="e6026-135">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e6026-135">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e6026-136">**Intestazione:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="e6026-136">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="e6026-137">**Libreria:** Incluso come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="e6026-137">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="e6026-138">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e6026-138">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e6026-139">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e6026-139">See also</span></span>

- [<span data-ttu-id="e6026-140">Interfaccia ICLRTask</span><span class="sxs-lookup"><span data-stu-id="e6026-140">ICLRTask Interface</span></span>](iclrtask-interface.md)
- [<span data-ttu-id="e6026-141">Interfaccia ICLRTaskManager</span><span class="sxs-lookup"><span data-stu-id="e6026-141">ICLRTaskManager Interface</span></span>](iclrtaskmanager-interface.md)
- [<span data-ttu-id="e6026-142">Interfaccia IHostTask</span><span class="sxs-lookup"><span data-stu-id="e6026-142">IHostTask Interface</span></span>](ihosttask-interface.md)
- [<span data-ttu-id="e6026-143">Interfaccia IHostTaskManager</span><span class="sxs-lookup"><span data-stu-id="e6026-143">IHostTaskManager Interface</span></span>](ihosttaskmanager-interface.md)

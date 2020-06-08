---
title: Enumerazione COR_PRF_SUSPEND_REASON
ms.date: 03/30/2017
api_name:
- COR_PRF_SUSPEND_REASON
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_SUSPEND_REASON
helpviewer_keywords:
- COR_PRF_SUSPEND_REASON enumeration [.NET Framework profiling]
ms.assetid: 75594833-bed3-47b2-a426-b75c5fe6fbcf
topic_type:
- apiref
ms.openlocfilehash: fdbcbb2da8f449b9275d820763c2a94cca86cd1e
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500754"
---
# <a name="cor_prf_suspend_reason-enumeration"></a><span data-ttu-id="411da-102">Enumerazione COR_PRF_SUSPEND_REASON</span><span class="sxs-lookup"><span data-stu-id="411da-102">COR_PRF_SUSPEND_REASON Enumeration</span></span>
<span data-ttu-id="411da-103">Indica il motivo della sospensione del runtime.</span><span class="sxs-lookup"><span data-stu-id="411da-103">Indicates the reason that the runtime is suspended.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="411da-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="411da-104">Syntax</span></span>  
  
```cpp  
typedef enum {  
    COR_PRF_SUSPEND_OTHER                   = 0x00,  
    COR_PRF_SUSPEND_FOR_GC                  = 0x01,  
    COR_PRF_SUSPEND_FOR_APPDOMAIN_SHUTDOWN  = 0x02,  
    COR_PRF_SUSPEND_FOR_CODE_PITCHING       = 0x03,  
    COR_PRF_SUSPEND_FOR_SHUTDOWN            = 0x04,  
    COR_PRF_SUSPEND_FOR_INPROC_DEBUGGER     = 0x06,  
    COR_PRF_SUSPEND_FOR_GC_PREP             = 0x07,    COR_PRF_SUSPEND_FOR_REJIT               = 8  
} COR_PRF_SUSPEND_REASON;  
```  
  
## <a name="members"></a><span data-ttu-id="411da-105">Membri</span><span class="sxs-lookup"><span data-stu-id="411da-105">Members</span></span>  
  
|<span data-ttu-id="411da-106">Membro</span><span class="sxs-lookup"><span data-stu-id="411da-106">Member</span></span>|<span data-ttu-id="411da-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="411da-107">Description</span></span>|  
|------------|-----------------|  
|`COR_PRF_FIELD_SUSPEND_OTHER`|<span data-ttu-id="411da-108">Il runtime viene sospeso per un motivo non specificato.</span><span class="sxs-lookup"><span data-stu-id="411da-108">The runtime is suspended for an unspecified reason.</span></span>|  
|`COR_PRF_FIELD_SUSPEND_FOR_GC`|<span data-ttu-id="411da-109">Il runtime viene sospeso per servire una richiesta Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="411da-109">The runtime is suspended to service a garbage collection request.</span></span><br /><br /> <span data-ttu-id="411da-110">I callback correlati a Garbage Collection si verificano tra i callback [ICorProfilerCallback:: RuntimeSuspendFinished](icorprofilercallback-runtimesuspendfinished-method.md) e [ICorProfilerCallback:: RuntimeResumeStarted](icorprofilercallback-runtimeresumestarted-method.md) .</span><span class="sxs-lookup"><span data-stu-id="411da-110">The garbage collection-related callbacks occur between the [ICorProfilerCallback::RuntimeSuspendFinished](icorprofilercallback-runtimesuspendfinished-method.md) and [ICorProfilerCallback::RuntimeResumeStarted](icorprofilercallback-runtimeresumestarted-method.md) callbacks.</span></span>|  
|`COR_PRF_FIELD_SUSPEND_FOR_APPDOMAIN_SHUTDOWN`|<span data-ttu-id="411da-111">Il runtime viene sospeso in modo che un `AppDomain` possa essere arrestato.</span><span class="sxs-lookup"><span data-stu-id="411da-111">The runtime is suspended so that an `AppDomain` can be shut down.</span></span><br /><br /> <span data-ttu-id="411da-112">Durante la sospensione del runtime, il runtime determinerà quali thread si trovano nell'oggetto `AppDomain` da arrestare e impostarli su Interrompi al riavvio.</span><span class="sxs-lookup"><span data-stu-id="411da-112">While the runtime is suspended, the runtime will determine which threads are in the `AppDomain` that is being shut down and set them to abort when they resume.</span></span> <span data-ttu-id="411da-113">Non sono presenti `AppDomain` callback specifici durante questa sospensione.</span><span class="sxs-lookup"><span data-stu-id="411da-113">There are no `AppDomain`-specific callbacks during this suspension.</span></span>|  
|`COR_PRF_FIELD_SUSPEND_FOR_CODE_PITCHING`|<span data-ttu-id="411da-114">Il runtime viene sospeso in modo che possa verificarsi il pitching del codice.</span><span class="sxs-lookup"><span data-stu-id="411da-114">The runtime is suspended so that code pitching can occur.</span></span><br /><br /> <span data-ttu-id="411da-115">Il pitching del codice si verifica solo quando il compilatore JIT (just-in-Time) è attivo con la funzionalità di pitching del codice abilitata.</span><span class="sxs-lookup"><span data-stu-id="411da-115">Code pitching ensues only when the just-in-time (JIT) compiler is active with code pitching enabled.</span></span> <span data-ttu-id="411da-116">I callback di pitching del codice si verificano tra i `ICorProfilerCallback::RuntimeSuspendFinished` `ICorProfilerCallback::RuntimeResumeStarted` callback e.</span><span class="sxs-lookup"><span data-stu-id="411da-116">Code pitching callbacks occur between the `ICorProfilerCallback::RuntimeSuspendFinished` and `ICorProfilerCallback::RuntimeResumeStarted` callbacks.</span></span> <span data-ttu-id="411da-117">**Nota:**  CLR JIT non esegue il pitch delle funzioni nella .NET Framework versione 2,0, pertanto questo valore non viene usato in 2,0.</span><span class="sxs-lookup"><span data-stu-id="411da-117">**Note:**  The CLR JIT does not pitch functions in the .NET Framework version 2.0, so this value is not used in 2.0.</span></span>|  
|`COR_PRF_FIELD_SUSPEND_FOR_SHUTDOWN`|<span data-ttu-id="411da-118">Il runtime viene sospeso in modo che sia possibile arrestarlo.</span><span class="sxs-lookup"><span data-stu-id="411da-118">The runtime is suspended so that it can shut down.</span></span> <span data-ttu-id="411da-119">Per completare l'operazione, è necessario sospendere tutti i thread.</span><span class="sxs-lookup"><span data-stu-id="411da-119">It must suspend all threads to complete the operation.</span></span>|  
|`COR_PRF_FIELD_SUSPEND_FOR_INPROC_DEBUGGER`|<span data-ttu-id="411da-120">Il runtime è sospeso per il debug in-process.</span><span class="sxs-lookup"><span data-stu-id="411da-120">The runtime is suspended for in-process debugging.</span></span>|  
|`COR_PRF_FIELD_SUSPEND_FOR_GC_PREP`|<span data-ttu-id="411da-121">Il runtime viene sospeso per prepararsi a una Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="411da-121">The runtime is suspended to prepare for a garbage collection.</span></span>|  
|`COR_PRF_SUSPEND_FOR_REJIT`|<span data-ttu-id="411da-122">Il runtime è sospeso per la ricompilazione JIT.</span><span class="sxs-lookup"><span data-stu-id="411da-122">The runtime is suspended for JIT recompilation.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="411da-123">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="411da-123">Remarks</span></span>  
 <span data-ttu-id="411da-124">È possibile continuare l'esecuzione di tutti i thread di runtime presenti nel codice non gestito fino a quando non tentano di immettere nuovamente il runtime, quindi verranno sospesi fino al riavvio del runtime.</span><span class="sxs-lookup"><span data-stu-id="411da-124">All runtime threads that are in unmanaged code are permitted to continue running until they try to re-enter the runtime, at which point they will also be suspended until the runtime resumes.</span></span> <span data-ttu-id="411da-125">Questo vale anche per i nuovi thread che entrano in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="411da-125">This also applies to new threads that enter the runtime.</span></span> <span data-ttu-id="411da-126">Tutti i thread all'interno della fase di esecuzione vengono sospesi immediatamente se sono nel codice interrompibili o vengono richiesti per la sospensione quando raggiungono il codice interrompibili.</span><span class="sxs-lookup"><span data-stu-id="411da-126">All threads within the runtime are either suspended immediately if they are in interruptible code, or asked to suspend when they do reach interruptible code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="411da-127">Requisiti</span><span class="sxs-lookup"><span data-stu-id="411da-127">Requirements</span></span>  
 <span data-ttu-id="411da-128">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="411da-128">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="411da-129">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="411da-129">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="411da-130">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="411da-130">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="411da-131">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="411da-131">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="411da-132">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="411da-132">See also</span></span>

- [<span data-ttu-id="411da-133">Enumerazioni di profilatura</span><span class="sxs-lookup"><span data-stu-id="411da-133">Profiling Enumerations</span></span>](profiling-enumerations.md)

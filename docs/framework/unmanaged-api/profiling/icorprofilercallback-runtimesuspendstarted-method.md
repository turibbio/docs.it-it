---
title: Metodo ICorProfilerCallback::RuntimeSuspendStarted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RuntimeSuspendStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RuntimeSuspendStarted
helpviewer_keywords:
- ICorProfilerCallback::RuntimeSuspendStarted method [.NET Framework profiling]
- RuntimeSuspendStarted method [.NET Framework profiling]
ms.assetid: c8461cac-e31b-4efa-ad2c-26598173eb96
topic_type:
- apiref
ms.openlocfilehash: cc01254d9604ce39c964c7d78059ef4087483c77
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503224"
---
# <a name="icorprofilercallbackruntimesuspendstarted-method"></a><span data-ttu-id="b1ef7-102">Metodo ICorProfilerCallback::RuntimeSuspendStarted</span><span class="sxs-lookup"><span data-stu-id="b1ef7-102">ICorProfilerCallback::RuntimeSuspendStarted Method</span></span>
<span data-ttu-id="b1ef7-103">Notifica al profiler che il Runtime sta per sospendere tutti i thread runtime.</span><span class="sxs-lookup"><span data-stu-id="b1ef7-103">Notifies the profiler that the runtime is about to suspend all runtime threads.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b1ef7-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b1ef7-104">Syntax</span></span>  
  
```cpp  
HRESULT RuntimeSuspendStarted(  
    [in] COR_PRF_SUSPEND_REASON suspendReason);  
```  
  
## <a name="parameters"></a><span data-ttu-id="b1ef7-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="b1ef7-105">Parameters</span></span>  
 `suspendReason`  
 <span data-ttu-id="b1ef7-106">in Valore dell'enumerazione [COR_PRF_SUSPEND_REASON](cor-prf-suspend-reason-enumeration.md) che indica il motivo della sospensione.</span><span class="sxs-lookup"><span data-stu-id="b1ef7-106">[in] A value of the [COR_PRF_SUSPEND_REASON](cor-prf-suspend-reason-enumeration.md) enumeration that indicates the reason for the suspension.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b1ef7-107">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="b1ef7-107">Remarks</span></span>  
 <span data-ttu-id="b1ef7-108">Tutti i thread runtime presenti nel codice non gestito possono continuare l'esecuzione fino a quando non tentano di immettere nuovamente il Runtime.</span><span class="sxs-lookup"><span data-stu-id="b1ef7-108">All runtime threads that are in unmanaged code are allowed to continue running until they try to re-enter the runtime.</span></span> <span data-ttu-id="b1ef7-109">A questo punto verranno sospesi anche fino al riavvio del runtime.</span><span class="sxs-lookup"><span data-stu-id="b1ef7-109">At that point they will also be suspended until the runtime resumes.</span></span> <span data-ttu-id="b1ef7-110">Questo vale anche per i nuovi thread che entrano in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b1ef7-110">This also applies to new threads that enter the runtime.</span></span> <span data-ttu-id="b1ef7-111">Tutti i thread in fase di esecuzione vengono sospesi immediatamente se sono già presenti nel codice interrompibili o viene richiesto di sospenderli quando raggiungono il codice interrompibili.</span><span class="sxs-lookup"><span data-stu-id="b1ef7-111">All threads in the runtime are either suspended immediately if they are already in interruptible code, or they are asked to suspend when they reach interruptible code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b1ef7-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="b1ef7-112">Requirements</span></span>  
 <span data-ttu-id="b1ef7-113">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b1ef7-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b1ef7-114">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="b1ef7-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="b1ef7-115">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="b1ef7-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="b1ef7-116">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b1ef7-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b1ef7-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b1ef7-117">See also</span></span>

- [<span data-ttu-id="b1ef7-118">Interfaccia ICorProfilerCallback</span><span class="sxs-lookup"><span data-stu-id="b1ef7-118">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="b1ef7-119">Metodo RuntimeSuspendAborted</span><span class="sxs-lookup"><span data-stu-id="b1ef7-119">RuntimeSuspendAborted Method</span></span>](icorprofilercallback-runtimesuspendaborted-method.md)
- [<span data-ttu-id="b1ef7-120">Metodo RuntimeSuspendFinished</span><span class="sxs-lookup"><span data-stu-id="b1ef7-120">RuntimeSuspendFinished Method</span></span>](icorprofilercallback-runtimesuspendfinished-method.md)

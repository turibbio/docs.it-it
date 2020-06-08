---
title: Metodo ICorProfilerCallback::ThreadCreated
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ThreadCreated
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ThreadCreated
helpviewer_keywords:
- ICorProfilerCallback::ThreadCreated method [.NET Framework profiling]
- ThreadCreated method [.NET Framework profiling]
ms.assetid: cca0f799-09b8-4689-a33c-6d6537943a9b
topic_type:
- apiref
ms.openlocfilehash: 25a4b101388bfc0151ba7c9c52da6561d48f806b
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503159"
---
# <a name="icorprofilercallbackthreadcreated-method"></a><span data-ttu-id="7e539-102">Metodo ICorProfilerCallback::ThreadCreated</span><span class="sxs-lookup"><span data-stu-id="7e539-102">ICorProfilerCallback::ThreadCreated Method</span></span>
<span data-ttu-id="7e539-103">Notifica al profiler che è stato creato un thread.</span><span class="sxs-lookup"><span data-stu-id="7e539-103">Notifies the profiler that a thread has been created.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7e539-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="7e539-104">Syntax</span></span>  
  
```cpp  
HRESULT ThreadCreated(  
    [in] ThreadID threadId);
```  
  
## <a name="parameters"></a><span data-ttu-id="7e539-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="7e539-105">Parameters</span></span>  
 `threadId`  
 <span data-ttu-id="7e539-106">in ID del thread che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="7e539-106">[in] The ID of the thread that has been created.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="7e539-107">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="7e539-107">Remarks</span></span>  
 <span data-ttu-id="7e539-108">Il `threadId` valore è immediatamente valido.</span><span class="sxs-lookup"><span data-stu-id="7e539-108">The `threadId` value is immediately valid.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7e539-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="7e539-109">Requirements</span></span>  
 <span data-ttu-id="7e539-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7e539-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7e539-111">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="7e539-111">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="7e539-112">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="7e539-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="7e539-113">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7e539-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7e539-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7e539-114">See also</span></span>

- [<span data-ttu-id="7e539-115">Interfaccia ICorProfilerCallback</span><span class="sxs-lookup"><span data-stu-id="7e539-115">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="7e539-116">Metodo ThreadDestroyed</span><span class="sxs-lookup"><span data-stu-id="7e539-116">ThreadDestroyed Method</span></span>](icorprofilercallback-threaddestroyed-method.md)

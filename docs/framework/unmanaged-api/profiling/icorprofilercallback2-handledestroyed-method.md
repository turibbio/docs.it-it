---
title: Metodo ICorProfilerCallback2::HandleDestroyed
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.HandleDestroyed
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::HandleDestroyed
helpviewer_keywords:
- ICorProfilerCallback2::HandleDestroyed method [.NET Framework profiling]
- HandleDestroyed method [.NET Framework profiling]
ms.assetid: ab4f4bbd-40c7-4667-bfde-60cd73803110
topic_type:
- apiref
ms.openlocfilehash: d7a4f7d08e6d8698dbb58c4c2d111a47d0ccc8db
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499779"
---
# <a name="icorprofilercallback2handledestroyed-method"></a><span data-ttu-id="d8b1e-102">Metodo ICorProfilerCallback2::HandleDestroyed</span><span class="sxs-lookup"><span data-stu-id="d8b1e-102">ICorProfilerCallback2::HandleDestroyed Method</span></span>
<span data-ttu-id="d8b1e-103">Notifica all'Code Profiler che un handle di Garbage Collection è stato eliminato definitivamente.</span><span class="sxs-lookup"><span data-stu-id="d8b1e-103">Notifies the code profiler that a garbage collection handle has been destroyed.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d8b1e-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="d8b1e-104">Syntax</span></span>  
  
```cpp  
HRESULT HandleDestroyed(  
    [in] GCHandleID handleId);  
```  
  
## <a name="parameters"></a><span data-ttu-id="d8b1e-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="d8b1e-105">Parameters</span></span>  
 `handleId`  
 <span data-ttu-id="d8b1e-106">in ID dell'handle per la Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="d8b1e-106">[in] The ID of the handle for the garbage collection.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d8b1e-107">Requisiti</span><span class="sxs-lookup"><span data-stu-id="d8b1e-107">Requirements</span></span>  
 <span data-ttu-id="d8b1e-108">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="d8b1e-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d8b1e-109">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="d8b1e-109">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="d8b1e-110">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d8b1e-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d8b1e-111">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d8b1e-111">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d8b1e-112">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d8b1e-112">See also</span></span>

- [<span data-ttu-id="d8b1e-113">Interfaccia ICorProfilerCallback</span><span class="sxs-lookup"><span data-stu-id="d8b1e-113">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="d8b1e-114">Interfaccia ICorProfilerCallback2</span><span class="sxs-lookup"><span data-stu-id="d8b1e-114">ICorProfilerCallback2 Interface</span></span>](icorprofilercallback2-interface.md)

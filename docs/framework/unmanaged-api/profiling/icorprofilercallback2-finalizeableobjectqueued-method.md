---
title: Metodo ICorProfilerCallback2::FinalizeableObjectQueued
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.FinalizeableObjectQueued
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::FinalizeableObjectQueued
helpviewer_keywords:
- FinalizeableObjectQueued method [.NET Framework profiling]
- ICorProfilerCallback2::FinalizeableObjectQueued method [.NET Framework profiling]
ms.assetid: 92d76893-683c-475d-9996-5bff03cdb10f
topic_type:
- apiref
ms.openlocfilehash: e2e01c396a67614464e3d4ca50de992388961463
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499823"
---
# <a name="icorprofilercallback2finalizeableobjectqueued-method"></a><span data-ttu-id="3fa91-102">Metodo ICorProfilerCallback2::FinalizeableObjectQueued</span><span class="sxs-lookup"><span data-stu-id="3fa91-102">ICorProfilerCallback2::FinalizeableObjectQueued Method</span></span>
<span data-ttu-id="3fa91-103">Notifica all'Code Profiler che un oggetto con un finalizzatore è stato accodato al thread del finalizzatore per l'esecuzione del relativo `Finalize` metodo.</span><span class="sxs-lookup"><span data-stu-id="3fa91-103">Notifies the code profiler that an object with a finalizer has been queued to the finalizer thread for execution of its `Finalize` method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3fa91-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="3fa91-104">Syntax</span></span>  
  
```cpp  
HRESULT FinalizeableObjectQueued(  
    [in] DWORD finalizerFlags,  
    [in] ObjectID objectID);  
```  
  
## <a name="parameters"></a><span data-ttu-id="3fa91-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="3fa91-105">Parameters</span></span>  
 `finalizerFlags`  
 <span data-ttu-id="3fa91-106">in Valore dell'enumerazione [COR_PRF_FINALIZER_FLAGS](cor-prf-finalizer-flags-enumeration.md) che descrive gli aspetti del finalizzatore.</span><span class="sxs-lookup"><span data-stu-id="3fa91-106">[in] A value of the [COR_PRF_FINALIZER_FLAGS](cor-prf-finalizer-flags-enumeration.md) enumeration that describes aspects of the finalizer.</span></span>  
  
 `objectID`  
 <span data-ttu-id="3fa91-107">in ID dell'oggetto che è stato accodato.</span><span class="sxs-lookup"><span data-stu-id="3fa91-107">[in] The ID of the object that has been queued.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3fa91-108">Requisiti</span><span class="sxs-lookup"><span data-stu-id="3fa91-108">Requirements</span></span>  
 <span data-ttu-id="3fa91-109">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3fa91-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3fa91-110">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="3fa91-110">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="3fa91-111">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="3fa91-111">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3fa91-112">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3fa91-112">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3fa91-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3fa91-113">See also</span></span>

- [<span data-ttu-id="3fa91-114">Interfaccia ICorProfilerCallback</span><span class="sxs-lookup"><span data-stu-id="3fa91-114">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="3fa91-115">Interfaccia ICorProfilerCallback2</span><span class="sxs-lookup"><span data-stu-id="3fa91-115">ICorProfilerCallback2 Interface</span></span>](icorprofilercallback2-interface.md)

---
title: Metodo ICorProfilerCallback::AssemblyLoadStarted
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AssemblyLoadStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AssemblyLoadStarted
helpviewer_keywords:
- ICorProfilerCallback::AssemblyLoadStarted method [.NET Framework profiling]
- AssemblyLoadStarted method [.NET Framework profiling]
ms.assetid: 67e8209d-a0ca-4118-a6e6-c1ee0abc2221
topic_type:
- apiref
ms.openlocfilehash: df172edb97a82ae3bf2d46c8be6ea05d5445a09a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500429"
---
# <a name="icorprofilercallbackassemblyloadstarted-method"></a><span data-ttu-id="259e5-102">Metodo ICorProfilerCallback::AssemblyLoadStarted</span><span class="sxs-lookup"><span data-stu-id="259e5-102">ICorProfilerCallback::AssemblyLoadStarted Method</span></span>
<span data-ttu-id="259e5-103">Notifica al profiler che è in corso il caricamento di un assembly.</span><span class="sxs-lookup"><span data-stu-id="259e5-103">Notifies the profiler that an assembly is being loaded.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="259e5-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="259e5-104">Syntax</span></span>  
  
```cpp  
HRESULT AssemblyLoadStarted(  
    [in] AssemblyID assemblyId);  
```  
  
## <a name="parameters"></a><span data-ttu-id="259e5-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="259e5-105">Parameters</span></span>

- `assemblyId`

  <span data-ttu-id="259e5-106">\[in] identifica l'assembly da caricare.</span><span class="sxs-lookup"><span data-stu-id="259e5-106">\[in] Identifies the assembly that is being loaded.</span></span>

## <a name="remarks"></a><span data-ttu-id="259e5-107">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="259e5-107">Remarks</span></span>  
 <span data-ttu-id="259e5-108">Il valore di `assemblyId` non è valido per una richiesta di informazioni fino a quando non viene chiamato il metodo [ICorProfilerCallback:: AssemblyLoadFinished](icorprofilercallback-assemblyloadfinished-method.md) .</span><span class="sxs-lookup"><span data-stu-id="259e5-108">The value of `assemblyId` is not valid for an information request until the [ICorProfilerCallback::AssemblyLoadFinished](icorprofilercallback-assemblyloadfinished-method.md) method is called.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="259e5-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="259e5-109">Requirements</span></span>  
 <span data-ttu-id="259e5-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="259e5-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="259e5-111">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="259e5-111">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="259e5-112">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="259e5-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="259e5-113">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="259e5-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="259e5-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="259e5-114">See also</span></span>

- [<span data-ttu-id="259e5-115">Interfaccia ICorProfilerCallback</span><span class="sxs-lookup"><span data-stu-id="259e5-115">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)

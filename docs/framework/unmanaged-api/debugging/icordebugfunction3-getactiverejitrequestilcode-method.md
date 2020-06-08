---
title: Metodo ICorDebugFunction3::GetActiveReJitRequestILCode
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugFunction3.GetActiveReJitRequestILCode
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 88584574-ade5-45b2-9778-489ed5c4dd7f
topic_type:
- apiref
ms.openlocfilehash: db9ce146da1d6fee8db32a0be43903eaa61e52de
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501755"
---
# <a name="icordebugfunction3getactiverejitrequestilcode-method"></a><span data-ttu-id="d9d3e-102">Metodo ICorDebugFunction3::GetActiveReJitRequestILCode</span><span class="sxs-lookup"><span data-stu-id="d9d3e-102">ICorDebugFunction3::GetActiveReJitRequestILCode Method</span></span>
<span data-ttu-id="d9d3e-103">[Supportato in .NET Framework 4.5.2 e versioni successive]</span><span class="sxs-lookup"><span data-stu-id="d9d3e-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="d9d3e-104">Ottiene un puntatore a interfaccia a un [ICorDebugILCode](icordebugilcode-interface.md) che contiene il il da una richiesta ReJIT attiva.</span><span class="sxs-lookup"><span data-stu-id="d9d3e-104">Gets an interface pointer to an [ICorDebugILCode](icordebugilcode-interface.md) that contains the IL from an active ReJIT request.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d9d3e-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="d9d3e-105">Syntax</span></span>  
  
```cpp
HRESULT GetActiveReJitRequestILCode(  
   ICorDebugILCode **ppReJitedILCode  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="d9d3e-106">Parametri</span><span class="sxs-lookup"><span data-stu-id="d9d3e-106">Parameters</span></span>  
 `ppReJitedILCode`  
 <span data-ttu-id="d9d3e-107">Puntatore al linguaggio intermedio (IL) da una richiesta ReJIT attiva.</span><span class="sxs-lookup"><span data-stu-id="d9d3e-107">A pointer to the IL from an active ReJIT request.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="d9d3e-108">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="d9d3e-108">Remarks</span></span>  
 <span data-ttu-id="d9d3e-109">Se il metodo rappresentato da questo oggetto `ICorDebugFunction3` ha una richiesta ReJIT attiva, `ppReJitedILCode` restituisce un puntatore al relativo linguaggio intermedio.</span><span class="sxs-lookup"><span data-stu-id="d9d3e-109">If the method represented by this `ICorDebugFunction3` object has an active ReJIT request, `ppReJitedILCode` returns a pointer to its IL.</span></span> <span data-ttu-id="d9d3e-110">Se non sono presenti richieste attive, ovvero un caso comune, `ppReJitedILCode` è **null**.</span><span class="sxs-lookup"><span data-stu-id="d9d3e-110">If there is no active request, which is a common case, then `ppReJitedILCode` is **null**.</span></span>  
  
 <span data-ttu-id="d9d3e-111">Una richiesta ReJIT diventa attiva subito dopo la restituzione dell'esecuzione dalla chiamata al metodo [ICorProfilerCallback4:: GetReJITParameters](../profiling/icorprofilercallback4-getrejitparameters-method.md) .</span><span class="sxs-lookup"><span data-stu-id="d9d3e-111">A ReJIT request becomes active just after execution returns from the [ICorProfilerCallback4::GetReJITParameters](../profiling/icorprofilercallback4-getrejitparameters-method.md) method call.</span></span> <span data-ttu-id="d9d3e-112">È possibile che non sia stata ancora sottoposta a compilazione JIT e i thread possono essere ancora in esecuzione nella versione originale del codice.</span><span class="sxs-lookup"><span data-stu-id="d9d3e-112">It may not yet be JIT-compiled, and threads may still be executing in the original version of the code.</span></span> <span data-ttu-id="d9d3e-113">Una richiesta ReJIT diventa inattiva durante la chiamata del profiler al metodo [ICorProfilerInfo4:: RequestRevert](../profiling/icorprofilerinfo4-requestrevert-method.md) .</span><span class="sxs-lookup"><span data-stu-id="d9d3e-113">A ReJIT request becomes inactive during the profiler's call to the [ICorProfilerInfo4::RequestRevert](../profiling/icorprofilerinfo4-requestrevert-method.md) method.</span></span> <span data-ttu-id="d9d3e-114">Anche dopo il ripristino del linguaggio intermedio, un thread può essere ancora in esecuzione nel codice ReJIT.</span><span class="sxs-lookup"><span data-stu-id="d9d3e-114">Even after the IL is reverted, a thread can still be executing in the JIT-recompiled (ReJIT) code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d9d3e-115">Requisiti</span><span class="sxs-lookup"><span data-stu-id="d9d3e-115">Requirements</span></span>  
 <span data-ttu-id="d9d3e-116">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="d9d3e-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d9d3e-117">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="d9d3e-117">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="d9d3e-118">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d9d3e-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d9d3e-119">**Versioni .NET Framework:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d9d3e-119">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d9d3e-120">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d9d3e-120">See also</span></span>

- [<span data-ttu-id="d9d3e-121">Interfaccia ICorDebugFunction3</span><span class="sxs-lookup"><span data-stu-id="d9d3e-121">ICorDebugFunction3 Interface</span></span>](icordebugfunction3-interface.md)
- [<span data-ttu-id="d9d3e-122">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="d9d3e-122">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="d9d3e-123">ReJIT: Guida alle procedure</span><span class="sxs-lookup"><span data-stu-id="d9d3e-123">ReJIT: A How-To Guide</span></span>](https://docs.microsoft.com/archive/blogs/davbr/rejit-a-how-to-guide)

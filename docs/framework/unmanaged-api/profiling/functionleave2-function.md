---
title: Funzione FunctionLeave2
ms.date: 03/30/2017
api_name:
- FunctionLeave2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionLeave2
helpviewer_keywords:
- FunctionLeave2 function [.NET Framework profiling]
ms.assetid: 8cdac941-8b94-4497-b874-4e571785f3fe
topic_type:
- apiref
ms.openlocfilehash: a2a3d58e0631fceab96c32f9d86fef25973fed84
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500663"
---
# <a name="functionleave2-function"></a><span data-ttu-id="9bdf0-102">Funzione FunctionLeave2</span><span class="sxs-lookup"><span data-stu-id="9bdf0-102">FunctionLeave2 Function</span></span>
<span data-ttu-id="9bdf0-103">Notifica al profiler che una funzione sta per tornare al chiamante e fornisce informazioni sull'stack frame e sul valore restituito della funzione.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-103">Notifies the profiler that a function is about to return to the caller and provides information about the stack frame and function return value.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9bdf0-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="9bdf0-104">Syntax</span></span>  
  
```cpp  
void __stdcall FunctionLeave2 (  
    [in]  FunctionID                        funcId,  
    [in]  UINT_PTR                          clientData,  
    [in]  COR_PRF_FRAME_INFO                func,  
    [in]  COR_PRF_FUNCTION_ARGUMENT_RANGE  *retvalRange  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="9bdf0-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="9bdf0-105">Parameters</span></span>

- `funcId`

  <span data-ttu-id="9bdf0-106">\[in] identificatore della funzione che restituisce.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-106">\[in] The identifier of the function that is returning.</span></span>

- `clientData`

  <span data-ttu-id="9bdf0-107">\[in] identificatore della funzione di cui è stato eseguito il mapping, specificato in precedenza dal profiler tramite la funzione [FunctionIDMapper](functionidmapper-function.md) .</span><span class="sxs-lookup"><span data-stu-id="9bdf0-107">\[in] The remapped function identifier, which the profiler previously specified via the [FunctionIDMapper](functionidmapper-function.md) function.</span></span>

- `func`

  <span data-ttu-id="9bdf0-108">\[in] `COR_PRF_FRAME_INFO` valore che punta alle informazioni relative all'stack frame.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-108">\[in] A `COR_PRF_FRAME_INFO` value that points to information about the stack frame.</span></span>

  <span data-ttu-id="9bdf0-109">Il profiler deve considerarlo come un handle opaco che può essere passato di nuovo al motore di esecuzione nel metodo [ICorProfilerInfo2:: GetFunctionInfo2](icorprofilerinfo2-getfunctioninfo2-method.md) .</span><span class="sxs-lookup"><span data-stu-id="9bdf0-109">The profiler should treat this as an opaque handle that can be passed back to the execution engine in the [ICorProfilerInfo2::GetFunctionInfo2](icorprofilerinfo2-getfunctioninfo2-method.md) method.</span></span>  
  
- `retvalRange`

  <span data-ttu-id="9bdf0-110">\[in] puntatore a una struttura [COR_PRF_FUNCTION_ARGUMENT_RANGE](cor-prf-function-argument-range-structure.md) che specifica la posizione di memoria del valore restituito della funzione.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-110">\[in] A pointer to a [COR_PRF_FUNCTION_ARGUMENT_RANGE](cor-prf-function-argument-range-structure.md) structure that specifies the memory location of the function's return value.</span></span>

  <span data-ttu-id="9bdf0-111">Per accedere alle informazioni sul valore restituito, `COR_PRF_ENABLE_FUNCTION_RETVAL` è necessario impostare il flag.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-111">In order to access return value information, the `COR_PRF_ENABLE_FUNCTION_RETVAL` flag must be set.</span></span> <span data-ttu-id="9bdf0-112">Il profiler può usare il metodo [ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md) per impostare i flag di evento.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-112">The profiler can use the [ICorProfilerInfo::SetEventMask](icorprofilerinfo-seteventmask-method.md) method to set the event flags.</span></span>

## <a name="remarks"></a><span data-ttu-id="9bdf0-113">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="9bdf0-113">Remarks</span></span>  
 <span data-ttu-id="9bdf0-114">I valori dei `func` parametri e `retvalRange` non sono validi dopo la `FunctionLeave2` restituzione della funzione perché i valori possono essere modificati o eliminati.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-114">The values of the `func` and `retvalRange` parameters are not valid after the `FunctionLeave2` function returns because the values may change or be destroyed.</span></span>  
  
 <span data-ttu-id="9bdf0-115">La `FunctionLeave2` funzione è un callback. è necessario implementarla.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-115">The `FunctionLeave2` function is a callback; you must implement it.</span></span> <span data-ttu-id="9bdf0-116">L'implementazione deve usare l' `__declspec` `naked` attributo della classe di archiviazione ().</span><span class="sxs-lookup"><span data-stu-id="9bdf0-116">The implementation must use the `__declspec`(`naked`) storage-class attribute.</span></span>  
  
 <span data-ttu-id="9bdf0-117">Il motore di esecuzione non salva i registri prima di chiamare questa funzione.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-117">The execution engine does not save any registers before calling this function.</span></span>  
  
- <span data-ttu-id="9bdf0-118">In ingresso è necessario salvare tutti i registri utilizzati, inclusi quelli nell'unità a virgola mobile (FPU).</span><span class="sxs-lookup"><span data-stu-id="9bdf0-118">On entry, you must save all registers that you use, including those in the floating-point unit (FPU).</span></span>  
  
- <span data-ttu-id="9bdf0-119">All'uscita è necessario ripristinare lo stack scegliendo tutti i parametri di cui è stato eseguito il push dal chiamante.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-119">On exit, you must restore the stack by popping off all the parameters that were pushed by its caller.</span></span>  
  
 <span data-ttu-id="9bdf0-120">L'implementazione di `FunctionLeave2` non deve essere bloccata perché ritarderà Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-120">The implementation of `FunctionLeave2` should not block because it will delay garbage collection.</span></span> <span data-ttu-id="9bdf0-121">L'implementazione non deve tentare un Garbage Collection perché lo stack potrebbe non essere in uno stato descrittivo Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-121">The implementation should not attempt a garbage collection because the stack may not be in a garbage collection-friendly state.</span></span> <span data-ttu-id="9bdf0-122">Se viene effettuato un tentativo di Garbage Collection, il runtime si bloccherà fino a quando non viene `FunctionLeave2` restituito.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-122">If a garbage collection is attempted, the runtime will block until `FunctionLeave2` returns.</span></span>  
  
 <span data-ttu-id="9bdf0-123">Inoltre, la `FunctionLeave2` funzione non deve chiamare nel codice gestito o in alcun modo causare un'allocazione managed memory.</span><span class="sxs-lookup"><span data-stu-id="9bdf0-123">Also, the `FunctionLeave2` function must not call into managed code or in any way cause a managed memory allocation.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9bdf0-124">Requisiti</span><span class="sxs-lookup"><span data-stu-id="9bdf0-124">Requirements</span></span>  
 <span data-ttu-id="9bdf0-125">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="9bdf0-125">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9bdf0-126">**Intestazione:** CorProf. idl</span><span class="sxs-lookup"><span data-stu-id="9bdf0-126">**Header:** CorProf.idl</span></span>  
  
 <span data-ttu-id="9bdf0-127">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="9bdf0-127">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="9bdf0-128">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9bdf0-128">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9bdf0-129">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9bdf0-129">See also</span></span>

- [<span data-ttu-id="9bdf0-130">Funzione FunctionEnter2</span><span class="sxs-lookup"><span data-stu-id="9bdf0-130">FunctionEnter2 Function</span></span>](functionenter2-function.md)
- [<span data-ttu-id="9bdf0-131">Funzione FunctionTailcall2</span><span class="sxs-lookup"><span data-stu-id="9bdf0-131">FunctionTailcall2 Function</span></span>](functiontailcall2-function.md)
- [<span data-ttu-id="9bdf0-132">Metodo SetEnterLeaveFunctionHooks2</span><span class="sxs-lookup"><span data-stu-id="9bdf0-132">SetEnterLeaveFunctionHooks2 Method</span></span>](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [<span data-ttu-id="9bdf0-133">Funzioni statiche globali di profilatura</span><span class="sxs-lookup"><span data-stu-id="9bdf0-133">Profiling Global Static Functions</span></span>](profiling-global-static-functions.md)

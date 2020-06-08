---
title: Funzione FunctionIDMapper
ms.date: 03/30/2017
api_name:
- FunctionIDMapper
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionIDMapper
helpviewer_keywords:
- FunctionIDMapper function [.NET Framework profiling]
ms.assetid: b8205b60-1893-4303-8cff-7ac5a00892aa
topic_type:
- apiref
ms.openlocfilehash: afc818dfe625bfc329ceb1660539eb119702a90d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500676"
---
# <a name="functionidmapper-function"></a><span data-ttu-id="fe35b-102">Funzione FunctionIDMapper</span><span class="sxs-lookup"><span data-stu-id="fe35b-102">FunctionIDMapper Function</span></span>
<span data-ttu-id="fe35b-103">Notifica al profiler che l'identificatore specificato di una funzione può essere rimappato a un ID alternativo da usare nei callback [FunctionEnter2](functionenter2-function.md), [FunctionLeave2](functionleave2-function.md)e [FunctionTailcall2](functiontailcall2-function.md) per tale funzione.</span><span class="sxs-lookup"><span data-stu-id="fe35b-103">Notifies the profiler that the given identifier of a function may be remapped to an alternative ID to be used in the [FunctionEnter2](functionenter2-function.md), [FunctionLeave2](functionleave2-function.md), and [FunctionTailcall2](functiontailcall2-function.md) callbacks for that function.</span></span> <span data-ttu-id="fe35b-104">`FunctionIDMapper` consente inoltre al profiler di indicare se vuole ricevere i callback per tale funzione.</span><span class="sxs-lookup"><span data-stu-id="fe35b-104">`FunctionIDMapper` also enables the profiler to indicate whether it wants to receive callbacks for that function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fe35b-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="fe35b-105">Syntax</span></span>  
  
```cpp  
UINT_PTR __stdcall FunctionIDMapper (  
    [in]  FunctionID  funcId,
    [out] BOOL       *pbHookFunction  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="fe35b-106">Parametri</span><span class="sxs-lookup"><span data-stu-id="fe35b-106">Parameters</span></span>

- `funcId`

  <span data-ttu-id="fe35b-107">\[in] identificatore di funzione di cui eseguire il mapping.</span><span class="sxs-lookup"><span data-stu-id="fe35b-107">\[in] The function identifier to be remapped.</span></span>

- `pbHookFunction`

  <span data-ttu-id="fe35b-108">\[out] puntatore a un valore che il profiler imposta su `true` se desidera ricevere i `FunctionEnter2` `FunctionLeave2` callback, e `FunctionTailcall2` ; in caso contrario, imposta questo valore su `false` .</span><span class="sxs-lookup"><span data-stu-id="fe35b-108">\[out] A pointer to a value that the profiler sets to `true` if it wants to receive `FunctionEnter2`, `FunctionLeave2`, and `FunctionTailcall2` callbacks; otherwise, it sets this value to `false`.</span></span>

## <a name="return-value"></a><span data-ttu-id="fe35b-109">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fe35b-109">Return Value</span></span>  
 <span data-ttu-id="fe35b-110">Il profiler restituisce un valore che il motore di esecuzione usa come identificatore alternativo della funzione.</span><span class="sxs-lookup"><span data-stu-id="fe35b-110">The profiler returns a value that the execution engine uses as an alternative function identifier.</span></span> <span data-ttu-id="fe35b-111">Il valore restituito non può essere null a meno che non sia restituito `false` in `pbHookFunction`.</span><span class="sxs-lookup"><span data-stu-id="fe35b-111">The return value cannot be null unless `false` is returned in `pbHookFunction`.</span></span> <span data-ttu-id="fe35b-112">In caso contrario, un valore restituito null produrrà risultati imprevedibili, inclusa la possibilità di arrestare il processo.</span><span class="sxs-lookup"><span data-stu-id="fe35b-112">Otherwise, a null return value will produce unpredictable results, including possibly halting the process.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="fe35b-113">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="fe35b-113">Remarks</span></span>  
 <span data-ttu-id="fe35b-114">La `FunctionIDMapper` funzione è un callback.</span><span class="sxs-lookup"><span data-stu-id="fe35b-114">The `FunctionIDMapper` function is a callback.</span></span> <span data-ttu-id="fe35b-115">Viene implementato dal profiler per eseguire il mapping di un ID funzione a un altro identificatore più utile per il profiler.</span><span class="sxs-lookup"><span data-stu-id="fe35b-115">It is implemented by the profiler to remap a function ID to some other identifier that is more useful for the profiler.</span></span> <span data-ttu-id="fe35b-116">`FunctionIDMapper`Restituisce l'ID alternativo da usare per una determinata funzione.</span><span class="sxs-lookup"><span data-stu-id="fe35b-116">The `FunctionIDMapper` returns the alternate ID to be used for any given function.</span></span> <span data-ttu-id="fe35b-117">Il motore di esecuzione rispetta quindi la richiesta del profiler passando questo ID alternativo, oltre all'ID funzione tradizionale, al profiler nel `clientData` parametro degli `FunctionEnter2` `FunctionLeave2` Hook, e `FunctionTailcall2` per identificare la funzione per cui viene chiamato il gancio.</span><span class="sxs-lookup"><span data-stu-id="fe35b-117">The execution engine then honors the profiler's request by passing this alternate ID, in addition to the traditional function ID, back to the profiler in the `clientData` parameter of the `FunctionEnter2`, `FunctionLeave2`, and `FunctionTailcall2` hooks, to identify the function for which the hook is being called.</span></span>  
  
 <span data-ttu-id="fe35b-118">È possibile usare il metodo [ICorProfilerInfo:: SetFunctionIDMapper](icorprofilerinfo-setfunctionidmapper-method.md) per specificare l'implementazione della `FunctionIDMapper` funzione.</span><span class="sxs-lookup"><span data-stu-id="fe35b-118">You can use the [ICorProfilerInfo::SetFunctionIDMapper](icorprofilerinfo-setfunctionidmapper-method.md) method to specify the implementation of the `FunctionIDMapper` function.</span></span> <span data-ttu-id="fe35b-119">È possibile chiamare il `ICorProfilerInfo::SetFunctionIDMapper` metodo solo una volta e si consiglia di eseguire questa operazione nel callback [ICorProfilerCallback:: Initialize](icorprofilercallback-initialize-method.md) .</span><span class="sxs-lookup"><span data-stu-id="fe35b-119">You can call the `ICorProfilerInfo::SetFunctionIDMapper` method only once, and we recommend that you do so in the [ICorProfilerCallback::Initialize](icorprofilercallback-initialize-method.md) callback.</span></span>  
  
 <span data-ttu-id="fe35b-120">Per impostazione predefinita, si presuppone che un profiler che imposta il flag di COR_PRF_MONITOR_ENTERLEAVE usando [ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md)e che imposta hook tramite [ICorProfilerInfo:: SetEnterLeaveFunctionHooks](icorprofilerinfo-setenterleavefunctionhooks-method.md) o [ICorProfilerInfo2:: SetEnterLeaveFunctionHooks2](icorprofilerinfo2-setenterleavefunctionhooks2-method.md), debba ricevere i `FunctionEnter2` `FunctionLeave2` callback, e `FunctionTailcall2` per ogni funzione.</span><span class="sxs-lookup"><span data-stu-id="fe35b-120">By default, it is assumed that a profiler that sets the COR_PRF_MONITOR_ENTERLEAVE flag by using [ICorProfilerInfo::SetEventMask](icorprofilerinfo-seteventmask-method.md), and which sets hooks via [ICorProfilerInfo::SetEnterLeaveFunctionHooks](icorprofilerinfo-setenterleavefunctionhooks-method.md) or [ICorProfilerInfo2::SetEnterLeaveFunctionHooks2](icorprofilerinfo2-setenterleavefunctionhooks2-method.md), should receive the `FunctionEnter2`, `FunctionLeave2`, and `FunctionTailcall2` callbacks for every function.</span></span> <span data-ttu-id="fe35b-121">Tuttavia, i profiler possono implementare `FunctionIDMapper` in modo selettivo per evitare di ricevere questi callback per determinate funzioni impostando `pbHookFunction` su `false` .</span><span class="sxs-lookup"><span data-stu-id="fe35b-121">However, profilers may implement `FunctionIDMapper` to selectively avoid receiving these callbacks for certain functions by setting `pbHookFunction` to `false`.</span></span>  
  
 <span data-ttu-id="fe35b-122">I profiler devono essere tolleranti nei casi in cui più thread di un'applicazione profilata chiamano simultaneamente lo stesso metodo o funzione.</span><span class="sxs-lookup"><span data-stu-id="fe35b-122">Profilers should be tolerant of cases where multiple threads of a profiled application are calling the same method/function simultaneously.</span></span> <span data-ttu-id="fe35b-123">In questi casi, il profiler può ricevere più `FunctionIDMapper` callback per lo stesso `FunctionID` .</span><span class="sxs-lookup"><span data-stu-id="fe35b-123">In such cases, the profiler may receive multiple `FunctionIDMapper` callbacks for the same `FunctionID`.</span></span> <span data-ttu-id="fe35b-124">Il profiler deve essere determinato per restituire gli stessi valori da questo callback quando viene chiamato più volte con lo stesso `FunctionID` .</span><span class="sxs-lookup"><span data-stu-id="fe35b-124">The profiler should be certain to return the same values from this callback when it is called multiple times with the same `FunctionID`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="fe35b-125">Requisiti</span><span class="sxs-lookup"><span data-stu-id="fe35b-125">Requirements</span></span>  
 <span data-ttu-id="fe35b-126">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="fe35b-126">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="fe35b-127">**Intestazione:** CorProf. idl</span><span class="sxs-lookup"><span data-stu-id="fe35b-127">**Header:** CorProf.idl</span></span>  
  
 <span data-ttu-id="fe35b-128">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="fe35b-128">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="fe35b-129">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="fe35b-129">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fe35b-130">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="fe35b-130">See also</span></span>

- [<span data-ttu-id="fe35b-131">Metodo SetFunctionIDMapper</span><span class="sxs-lookup"><span data-stu-id="fe35b-131">SetFunctionIDMapper Method</span></span>](icorprofilerinfo-setfunctionidmapper-method.md)
- [<span data-ttu-id="fe35b-132">Funzione FunctionIDMapper2</span><span class="sxs-lookup"><span data-stu-id="fe35b-132">FunctionIDMapper2 Function</span></span>](functionidmapper2-function.md)
- [<span data-ttu-id="fe35b-133">Funzione FunctionEnter2</span><span class="sxs-lookup"><span data-stu-id="fe35b-133">FunctionEnter2 Function</span></span>](functionenter2-function.md)
- [<span data-ttu-id="fe35b-134">Funzione FunctionLeave2</span><span class="sxs-lookup"><span data-stu-id="fe35b-134">FunctionLeave2 Function</span></span>](functionleave2-function.md)
- [<span data-ttu-id="fe35b-135">Funzione FunctionTailcall2</span><span class="sxs-lookup"><span data-stu-id="fe35b-135">FunctionTailcall2 Function</span></span>](functiontailcall2-function.md)
- [<span data-ttu-id="fe35b-136">Funzioni statiche globali di profilatura</span><span class="sxs-lookup"><span data-stu-id="fe35b-136">Profiling Global Static Functions</span></span>](profiling-global-static-functions.md)

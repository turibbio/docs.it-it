---
title: Metodo ICorProfilerInfo4::GetFunctionFromIP2
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.GetFunctionFromIP2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::GetFunctionFromIP2
helpviewer_keywords:
- ICorProfilerInfo4::GetFunctionFromIP2 method [.NET Framework profiling]
- GetFunctionFromIP2 method, ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: 46ff70f4-13e9-40a0-802a-0a40abcfc6a0
topic_type:
- apiref
ms.openlocfilehash: ea66474e809b3813faceef79a69dd8a639a72a3b
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502795"
---
# <a name="icorprofilerinfo4getfunctionfromip2-method"></a><span data-ttu-id="ca6c0-102">Metodo ICorProfilerInfo4::GetFunctionFromIP2</span><span class="sxs-lookup"><span data-stu-id="ca6c0-102">ICorProfilerInfo4::GetFunctionFromIP2 Method</span></span>
<span data-ttu-id="ca6c0-103">Esegue il mapping di un puntatore all'istruzione di codice gestito alla versione di una funzione ricompilata in JIT.</span><span class="sxs-lookup"><span data-stu-id="ca6c0-103">Maps a managed code instruction pointer to the JIT-recompiled version of a function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ca6c0-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="ca6c0-104">Syntax</span></span>  
  
```cpp  
HRESULT GetFunctionFromIP2(  
    [in]  LPCBYTE    ip,  
    [out] FunctionID *pFunctionId,  
    [out] ReJITID *pReJitId);  
```  
  
## <a name="parameters"></a><span data-ttu-id="ca6c0-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="ca6c0-105">Parameters</span></span>  
 `ip`  
 <span data-ttu-id="ca6c0-106">in Puntatore all'istruzione nel codice gestito.</span><span class="sxs-lookup"><span data-stu-id="ca6c0-106">[in] The instruction pointer in managed code.</span></span>  
  
 `pFunctionId`  
 <span data-ttu-id="ca6c0-107">out ID funzione.</span><span class="sxs-lookup"><span data-stu-id="ca6c0-107">[out] The function ID.</span></span>  
  
 `pReJitId`  
 <span data-ttu-id="ca6c0-108">out Identità della versione ricompilata in JIT della funzione.</span><span class="sxs-lookup"><span data-stu-id="ca6c0-108">[out] The identity of the JIT-recompiled version of the function.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="ca6c0-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="ca6c0-109">Remarks</span></span>  
 <span data-ttu-id="ca6c0-110">`GetFunctionFromIP2`è simile a `GetFunctionFromIP` , ad eccezione del fatto che ottiene l'ID ricompilato JIT anziché l'ID funzione della funzione che contiene l'indirizzo IP specificato.</span><span class="sxs-lookup"><span data-stu-id="ca6c0-110">`GetFunctionFromIP2` is similar to `GetFunctionFromIP`, except that it gets the JIT-recompiled ID instead of the function ID of the function that contains the specified IP address.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ca6c0-111">`GetFunctionFromIP2`può attivare un Garbage Collection, mentre `GetFunctionFromIP` non lo è.</span><span class="sxs-lookup"><span data-stu-id="ca6c0-111">`GetFunctionFromIP2` can trigger a garbage collection, whereas `GetFunctionFromIP` will not.</span></span>  <span data-ttu-id="ca6c0-112">Per ulteriori informazioni, vedere [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT](corprof-e-unsupported-call-sequence-hresult.md).</span><span class="sxs-lookup"><span data-stu-id="ca6c0-112">For more information, see [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT](corprof-e-unsupported-call-sequence-hresult.md).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ca6c0-113">Requisiti</span><span class="sxs-lookup"><span data-stu-id="ca6c0-113">Requirements</span></span>  
 <span data-ttu-id="ca6c0-114">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ca6c0-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ca6c0-115">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="ca6c0-115">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="ca6c0-116">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="ca6c0-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ca6c0-117">**Versioni .NET Framework:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ca6c0-117">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ca6c0-118">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ca6c0-118">See also</span></span>

- [<span data-ttu-id="ca6c0-119">Interfaccia ICorProfilerInfo</span><span class="sxs-lookup"><span data-stu-id="ca6c0-119">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)

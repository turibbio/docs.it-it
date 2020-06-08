---
title: Metodo ICorProfilerInfo3::GetThreadStaticAddress2
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetThreadStaticAddress2 Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetThreadStaticAddress2
helpviewer_keywords:
- ICorProfilerInfo3::GetThreadStaticAddress2 method [.NET Framework profiling]
- GetThreadStaticAddress2 method [.NET Framework profiling]
ms.assetid: a9608861-ae64-4467-8a73-be05ad34beac
topic_type:
- apiref
ms.openlocfilehash: a27e7ca156ca138078215a65486ac4b965c6a93d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496334"
---
# <a name="icorprofilerinfo3getthreadstaticaddress2-method"></a><span data-ttu-id="73734-102">Metodo ICorProfilerInfo3::GetThreadStaticAddress2</span><span class="sxs-lookup"><span data-stu-id="73734-102">ICorProfilerInfo3::GetThreadStaticAddress2 Method</span></span>
<span data-ttu-id="73734-103">Ottiene l'indirizzo del campo statico a livello di thread specificato che è nell'ambito del dominio dell'applicazione e del thread specificati.</span><span class="sxs-lookup"><span data-stu-id="73734-103">Gets the address of the specified thread-static field that is in the scope of the specified thread and application domain.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="73734-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="73734-104">Syntax</span></span>  
  
```cpp  
HRESULT GetThreadStaticAddress2(  
                [in] ClassID classId,  
                [in] mdFieldDef fieldToken,  
                [in] AppDomainID appDomainId,  
                [in] ThreadID threadId,  
                [out] void **ppAddress);  
```  
  
## <a name="parameters"></a><span data-ttu-id="73734-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="73734-105">Parameters</span></span>  
 `classId`  
 <span data-ttu-id="73734-106">in ID della classe che contiene il campo statico di thread richiesto.</span><span class="sxs-lookup"><span data-stu-id="73734-106">[in] The ID of the class that contains the requested thread-static field.</span></span>  
  
 `fieldToken`  
 <span data-ttu-id="73734-107">in Token di metadati per il campo statico di thread richiesto.</span><span class="sxs-lookup"><span data-stu-id="73734-107">[in] The metadata token for the requested thread-static field.</span></span>  
  
 `appDomainId`  
 <span data-ttu-id="73734-108">[in] ID del dominio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="73734-108">[in] The ID of the application domain.</span></span>  
  
 `threadId`  
 <span data-ttu-id="73734-109">in ID del thread che rappresenta l'ambito per il campo statico richiesto.</span><span class="sxs-lookup"><span data-stu-id="73734-109">[in] The ID of the thread that is the scope for the requested static field.</span></span>  
  
 `ppAddress`  
 <span data-ttu-id="73734-110">out Puntatore all'indirizzo del campo statico che si trova all'interno del thread specificato.</span><span class="sxs-lookup"><span data-stu-id="73734-110">[out] A pointer to the address of the static field that is within the specified thread.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="73734-111">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="73734-111">Remarks</span></span>  
 <span data-ttu-id="73734-112">Il `GetThreadStaticAddress2` metodo può restituire uno dei seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="73734-112">The `GetThreadStaticAddress2` method may return one of the following:</span></span>  
  
- <span data-ttu-id="73734-113">CORPROF_E_DATAINCOMPLETE HRESULT se al campo statico specificato non è stato assegnato un indirizzo nel contesto specificato.</span><span class="sxs-lookup"><span data-stu-id="73734-113">A CORPROF_E_DATAINCOMPLETE HRESULT if the given static field has not been assigned an address in the specified context.</span></span>  
  
- <span data-ttu-id="73734-114">Indirizzi degli oggetti che possono trovarsi nell'heap Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="73734-114">The addresses of objects that may be in the garbage collection heap.</span></span> <span data-ttu-id="73734-115">Questi indirizzi potrebbero non essere più validi dopo Garbage Collection, quindi, dopo Garbage Collection, i profiler non devono presupporre che siano validi.</span><span class="sxs-lookup"><span data-stu-id="73734-115">These addresses may become invalid after garbage collection, so after garbage collection, profilers should not assume that they are valid.</span></span>  
  
 <span data-ttu-id="73734-116">Prima che il costruttore della classe di una classe venga completato, `GetThreadStaticAddress2` restituirà CORPROF_E_DATAINCOMPLETE per tutti i campi statici, anche se alcuni dei campi statici potrebbero essere già inizializzati e la radice Garbage Collection oggetti.</span><span class="sxs-lookup"><span data-stu-id="73734-116">Before a class’s class constructor is completed, `GetThreadStaticAddress2` will return CORPROF_E_DATAINCOMPLETE for all its static fields, although some of the static fields may already be initialized and rooting garbage collection objects.</span></span>  
  
 <span data-ttu-id="73734-117">Il metodo [ICorProfilerInfo2:: GetThreadStaticAddress](icorprofilerinfo2-getthreadstaticaddress-method.md) è simile al `GetThreadStaticAddress2` metodo, ma non accetta un argomento del dominio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="73734-117">The [ICorProfilerInfo2::GetThreadStaticAddress](icorprofilerinfo2-getthreadstaticaddress-method.md) method is similar to the `GetThreadStaticAddress2` method, but does not accept an application domain argument.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="73734-118">Requisiti</span><span class="sxs-lookup"><span data-stu-id="73734-118">Requirements</span></span>  
 <span data-ttu-id="73734-119">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="73734-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="73734-120">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="73734-120">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="73734-121">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="73734-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="73734-122">**Versioni .NET Framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="73734-122">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="73734-123">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="73734-123">See also</span></span>

- [<span data-ttu-id="73734-124">Interfaccia ICorProfilerInfo3</span><span class="sxs-lookup"><span data-stu-id="73734-124">ICorProfilerInfo3 Interface</span></span>](icorprofilerinfo3-interface.md)
- [<span data-ttu-id="73734-125">Interfacce di profilatura</span><span class="sxs-lookup"><span data-stu-id="73734-125">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="73734-126">Profilatura</span><span class="sxs-lookup"><span data-stu-id="73734-126">Profiling</span></span>](index.md)

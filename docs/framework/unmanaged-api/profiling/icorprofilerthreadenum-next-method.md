---
title: Metodo ICorProfilerThreadEnum::Next
ms.date: 03/30/2017
api_name:
- ICorProfilerThreadEnum.Next
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerThreadEnum::Next
helpviewer_keywords:
- ICorProfilerThreadEnum::Next method [.NET Framework profiling]
- Next method, ICorProfilerThreadEnum interface [.NET Framework profiling]
ms.assetid: f3535279-3c63-41a2-ab0e-a129dc5a01e8
topic_type:
- apiref
ms.openlocfilehash: 37d1acfa70a1a2b2c18fb34fb5d6024f3b61e2ab
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494345"
---
# <a name="icorprofilerthreadenumnext-method"></a><span data-ttu-id="afde8-102">Metodo ICorProfilerThreadEnum::Next</span><span class="sxs-lookup"><span data-stu-id="afde8-102">ICorProfilerThreadEnum::Next Method</span></span>
<span data-ttu-id="afde8-103">Ottiene il numero specificato di thread contigui da una raccolta sequenziale di moduli, a partire dalla posizione corrente dell'enumeratore nella sequenza.</span><span class="sxs-lookup"><span data-stu-id="afde8-103">Gets the specified number of contiguous threads from a sequential collection of threads, starting at the enumerator's current position in the sequence.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="afde8-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="afde8-104">Syntax</span></span>  
  
```cpp  
HRESULT Next (    [in]  ULONG      celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
                    ThreadID ids[],  
    [out] ULONG *   pceltFetched  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="afde8-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="afde8-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="afde8-106">[in] Numero di thread da recuperare.</span><span class="sxs-lookup"><span data-stu-id="afde8-106">[in] The number of threads to retrieve.</span></span>  
  
 `ids`  
 <span data-ttu-id="afde8-107">[out] Matrice di valori `ThreadID`, ognuno dei quali rappresenta un thread recuperato.</span><span class="sxs-lookup"><span data-stu-id="afde8-107">[out] An array of `ThreadID` values, each of which represents a retrieved thread.</span></span>  
  
 `pceltFetched`  
 <span data-ttu-id="afde8-108">[out] Puntatore al numero di thread effettivamente restituiti nella matrice `ids`.</span><span class="sxs-lookup"><span data-stu-id="afde8-108">[out] A pointer to the number of threads actually returned in the `ids` array.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="afde8-109">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="afde8-109">Return Value</span></span>  
 <span data-ttu-id="afde8-110">Questo metodo restituisce gli specifici HRESULT seguenti, nonché gli errori di HRESULT che indicano la mancata riuscita del metodo.</span><span class="sxs-lookup"><span data-stu-id="afde8-110">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="afde8-111">HRESULT</span><span class="sxs-lookup"><span data-stu-id="afde8-111">HRESULT</span></span>|<span data-ttu-id="afde8-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="afde8-112">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="afde8-113">S_OK</span><span class="sxs-lookup"><span data-stu-id="afde8-113">S_OK</span></span>|<span data-ttu-id="afde8-114">Sono stati restituiti `celt` elementi.</span><span class="sxs-lookup"><span data-stu-id="afde8-114">`celt` elements were returned.</span></span>|  
|<span data-ttu-id="afde8-115">S_FALSE</span><span class="sxs-lookup"><span data-stu-id="afde8-115">S_FALSE</span></span>|<span data-ttu-id="afde8-116">Sono stati restituiti meno di `celt` elementi, il che indica che l'enumerazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="afde8-116">Fewer than `celt` elements were returned, which indicates that the enumeration is complete.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="afde8-117">Requisiti</span><span class="sxs-lookup"><span data-stu-id="afde8-117">Requirements</span></span>  
 <span data-ttu-id="afde8-118">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="afde8-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="afde8-119">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="afde8-119">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="afde8-120">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="afde8-120">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="afde8-121">**Versioni .NET Framework:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="afde8-121">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="afde8-122">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="afde8-122">See also</span></span>

- [<span data-ttu-id="afde8-123">Interfaccia ICorProfilerThreadEnum</span><span class="sxs-lookup"><span data-stu-id="afde8-123">ICorProfilerThreadEnum Interface</span></span>](icorprofilerthreadenum-interface.md)
- [<span data-ttu-id="afde8-124">Interfacce di profilatura</span><span class="sxs-lookup"><span data-stu-id="afde8-124">Profiling Interfaces</span></span>](profiling-interfaces.md)

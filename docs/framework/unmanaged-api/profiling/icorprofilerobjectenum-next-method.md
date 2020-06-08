---
title: Metodo ICorProfilerObjectEnum::Next
ms.date: 03/30/2017
api_name:
- ICorProfilerObjectEnum.Next
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerObjectEnum::Next
helpviewer_keywords:
- Next method, ICorProfilerObjectEnum interface [.NET Framework profiling]
- ICorProfilerObjectEnum::Next method [.NET Framework profiling]
ms.assetid: b420433c-5ebe-4986-bba1-97902e6db819
topic_type:
- apiref
ms.openlocfilehash: 850f05520e4146b5016bb574f02aa800dfcaaf32
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494579"
---
# <a name="icorprofilerobjectenumnext-method"></a><span data-ttu-id="7a92f-102">Metodo ICorProfilerObjectEnum::Next</span><span class="sxs-lookup"><span data-stu-id="7a92f-102">ICorProfilerObjectEnum::Next Method</span></span>
<span data-ttu-id="7a92f-103">Ottiene il numero specificato di oggetti contigui da una raccolta sequenziale di oggetti, a partire dalla posizione corrente dell'enumeratore nella sequenza.</span><span class="sxs-lookup"><span data-stu-id="7a92f-103">Gets the specified number of contiguous objects from a sequential collection of objects, starting at the enumerator's current position in the sequence.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7a92f-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="7a92f-104">Syntax</span></span>  
  
```cpp  
HRESULT Next (  
    [in] ULONG                    celt,  
    [out, size_is(celt), length_is(*pceltFetched)]
        ObjectID                  objects[],  
    [out] ULONG                   *pceltFetched  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="7a92f-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="7a92f-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="7a92f-106">[in] Numero di oggetti da recuperare.</span><span class="sxs-lookup"><span data-stu-id="7a92f-106">[in] The number of objects to be retrieved.</span></span>  
  
 `objects`  
 <span data-ttu-id="7a92f-107">out Matrice di `ObjectID` valori, ognuno dei quali rappresenta un oggetto recuperato.</span><span class="sxs-lookup"><span data-stu-id="7a92f-107">[out] An array of `ObjectID` values, each of which represents a retrieved object.</span></span>  
  
 `pceltFetched`  
 <span data-ttu-id="7a92f-108">[out] Puntatore al numero di elementi effettivamente restituiti nella matrice `objects`.</span><span class="sxs-lookup"><span data-stu-id="7a92f-108">[out] A pointer to the number of elements actually returned in the `objects` array.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7a92f-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="7a92f-109">Requirements</span></span>  
 <span data-ttu-id="7a92f-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7a92f-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7a92f-111">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="7a92f-111">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="7a92f-112">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="7a92f-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="7a92f-113">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7a92f-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7a92f-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7a92f-114">See also</span></span>

- [<span data-ttu-id="7a92f-115">Interfaccia ICorProfilerObjectEnum</span><span class="sxs-lookup"><span data-stu-id="7a92f-115">ICorProfilerObjectEnum Interface</span></span>](icorprofilerobjectenum-interface.md)

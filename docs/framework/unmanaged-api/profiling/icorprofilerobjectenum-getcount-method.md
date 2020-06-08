---
title: Metodo ICorProfilerObjectEnum::GetCount
ms.date: 03/30/2017
api_name:
- ICorProfilerObjectEnum.GetCount
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerObjectEnum::GetCount
helpviewer_keywords:
- ICorProfilerObjectEnum::GetCount method [.NET Framework profiling]
- GetCount method, ICorProfilerObjectEnum interface [.NET Framework profiling]
ms.assetid: 166b0761-ed80-4ccd-9973-dc20e61bf8fa
topic_type:
- apiref
ms.openlocfilehash: 4c867a9e263f022fc6f8d90a883562e2560ad1b2
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494657"
---
# <a name="icorprofilerobjectenumgetcount-method"></a><span data-ttu-id="debef-102">Metodo ICorProfilerObjectEnum::GetCount</span><span class="sxs-lookup"><span data-stu-id="debef-102">ICorProfilerObjectEnum::GetCount Method</span></span>
<span data-ttu-id="debef-103">Ottiene il numero totale di oggetti bloccati nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="debef-103">Gets the total number of frozen objects in the collection.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="debef-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="debef-104">Syntax</span></span>  
  
```cpp  
HRESULT GetCount (  
    [out] ULONG   *pcelt  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="debef-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="debef-105">Parameters</span></span>  
 `pcelt`  
 <span data-ttu-id="debef-106">out Puntatore al numero di oggetti bloccati nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="debef-106">[out] A pointer to the number of frozen objects in the collection.</span></span>  
  
 <span data-ttu-id="debef-107">Questo metodo restituirà sempre zero in .NET Framework versione 3,5 Service Pack 1 (SP1) e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="debef-107">This method will always return zero in the .NET Framework version 3.5 Service Pack 1 (SP1) and later versions.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="debef-108">Requisiti</span><span class="sxs-lookup"><span data-stu-id="debef-108">Requirements</span></span>  
 <span data-ttu-id="debef-109">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="debef-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="debef-110">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="debef-110">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="debef-111">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="debef-111">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="debef-112">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="debef-112">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="debef-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="debef-113">See also</span></span>

- [<span data-ttu-id="debef-114">Interfaccia ICorProfilerObjectEnum</span><span class="sxs-lookup"><span data-stu-id="debef-114">ICorProfilerObjectEnum Interface</span></span>](icorprofilerobjectenum-interface.md)

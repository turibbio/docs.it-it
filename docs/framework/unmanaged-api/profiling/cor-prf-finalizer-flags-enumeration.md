---
title: Enumerazione COR_PRF_FINALIZER_FLAGS
ms.date: 03/30/2017
api_name:
- COR_PRF_FINALIZER_FLAGS
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_FINALIZER_FLAGS
helpviewer_keywords:
- COR_PRF_FINALIZER_FLAGS enumeration [.NET Framework profiling]
ms.assetid: 297d7721-3911-4f36-9e34-d9da0c33e22a
topic_type:
- apiref
ms.openlocfilehash: b273faafd7abb86ace58bb5c24473406af3ce20e
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500973"
---
# <a name="cor_prf_finalizer_flags-enumeration"></a><span data-ttu-id="dd35b-102">Enumerazione COR_PRF_FINALIZER_FLAGS</span><span class="sxs-lookup"><span data-stu-id="dd35b-102">COR_PRF_FINALIZER_FLAGS Enumeration</span></span>
<span data-ttu-id="dd35b-103">Descrive il finalizzatore per un oggetto.</span><span class="sxs-lookup"><span data-stu-id="dd35b-103">Describes the finalizer for an object.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="dd35b-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="dd35b-104">Syntax</span></span>  
  
```cpp  
typedef enum {  
    COR_PRF_FINALIZER_CRITICAL = 0x1  
} COR_PRF_FINALIZER_FLAGS;  
```  
  
## <a name="members"></a><span data-ttu-id="dd35b-105">Membri</span><span class="sxs-lookup"><span data-stu-id="dd35b-105">Members</span></span>  
  
|<span data-ttu-id="dd35b-106">Membro</span><span class="sxs-lookup"><span data-stu-id="dd35b-106">Member</span></span>|<span data-ttu-id="dd35b-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="dd35b-107">Description</span></span>|  
|------------|-----------------|  
|`COR_PRF_FINALIZER_CRITICAL`|<span data-ttu-id="dd35b-108">Il finalizzatore è di importanza critica.</span><span class="sxs-lookup"><span data-stu-id="dd35b-108">The finalizer is critical.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="dd35b-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="dd35b-109">Remarks</span></span>  
 <span data-ttu-id="dd35b-110">L' `COR_PRF_FINALIZER_FLAGS` enumerazione viene utilizzata dal metodo [ICorProfilerCallback2:: FinalizeableObjectQueued](icorprofilercallback2-finalizeableobjectqueued-method.md) per descrivere il finalizzatore per un oggetto.</span><span class="sxs-lookup"><span data-stu-id="dd35b-110">The `COR_PRF_FINALIZER_FLAGS` enumeration is used by the [ICorProfilerCallback2::FinalizeableObjectQueued](icorprofilercallback2-finalizeableobjectqueued-method.md) method to describe the finalizer for an object.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="dd35b-111">Requisiti</span><span class="sxs-lookup"><span data-stu-id="dd35b-111">Requirements</span></span>  
 <span data-ttu-id="dd35b-112">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="dd35b-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="dd35b-113">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="dd35b-113">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="dd35b-114">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="dd35b-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="dd35b-115">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="dd35b-115">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="dd35b-116">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dd35b-116">See also</span></span>

- [<span data-ttu-id="dd35b-117">Enumerazioni di profilatura</span><span class="sxs-lookup"><span data-stu-id="dd35b-117">Profiling Enumerations</span></span>](profiling-enumerations.md)

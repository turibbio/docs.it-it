---
title: Enumerazione CorDebugUnmappedStop
ms.date: 03/30/2017
api_name:
- CorDebugUnmappedStop
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugUnmappedStop
helpviewer_keywords:
- CorDebugUnmappedStop enumeration [.NET Framework debugging]
ms.assetid: a684f7d7-d0c2-4690-b721-639e613f11f8
topic_type:
- apiref
ms.openlocfilehash: 772f1f0dee260ad3752b2f89e5fbe0d6bc27b87b
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795651"
---
# <a name="cordebugunmappedstop-enumeration"></a><span data-ttu-id="e9d80-102">Enumerazione CorDebugUnmappedStop</span><span class="sxs-lookup"><span data-stu-id="e9d80-102">CorDebugUnmappedStop Enumeration</span></span>
<span data-ttu-id="e9d80-103">Specifica il tipo di codice non mappato che può attivare un arresto nell'esecuzione del codice da parte del gestore di istruzioni.</span><span class="sxs-lookup"><span data-stu-id="e9d80-103">Specifies the type of unmapped code that can trigger a halt in code execution by the stepper.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e9d80-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="e9d80-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDebugUnmappedStop {  
    STOP_NONE               = 0x0,  
    STOP_PROLOG             = 0x01,  
    STOP_EPILOG             = 0x02,  
    STOP_NO_MAPPING_INFO    = 0x04,  
    STOP_OTHER_UNMAPPED     = 0x08,  
    STOP_UNMANAGED          = 0x10,  
    STOP_ALL                = 0xffff,  
} CorDebugUnmappedStop;  
```  
  
## <a name="members"></a><span data-ttu-id="e9d80-105">Members</span><span class="sxs-lookup"><span data-stu-id="e9d80-105">Members</span></span>  
  
|<span data-ttu-id="e9d80-106">Membro</span><span class="sxs-lookup"><span data-stu-id="e9d80-106">Member</span></span>|<span data-ttu-id="e9d80-107">Description</span><span class="sxs-lookup"><span data-stu-id="e9d80-107">Description</span></span>|  
|------------|-----------------|  
|`STOP_NONE`|<span data-ttu-id="e9d80-108">Non arrestare in alcun tipo di codice non mappato.</span><span class="sxs-lookup"><span data-stu-id="e9d80-108">Do not stop in any type of unmapped code.</span></span>|  
|`STOP_PROLOG`|<span data-ttu-id="e9d80-109">Arresta nel codice di prologo.</span><span class="sxs-lookup"><span data-stu-id="e9d80-109">Stop in prolog code.</span></span>|  
|`STOP_EPILOG`|<span data-ttu-id="e9d80-110">Arresta nel codice di epilogo.</span><span class="sxs-lookup"><span data-stu-id="e9d80-110">Stop in epilog code.</span></span>|  
|`STOP_NO_MAPPING_INFO`|<span data-ttu-id="e9d80-111">Arresta nel codice senza informazioni di mapping.</span><span class="sxs-lookup"><span data-stu-id="e9d80-111">Stop in code that has no mapping information.</span></span>|  
|`STOP_OTHER_UNMAPPED`|<span data-ttu-id="e9d80-112">Arrestarsi in codice non mappato che non rientra nel prologo, in epilogo, senza mapping-Information o nella categoria non gestita.</span><span class="sxs-lookup"><span data-stu-id="e9d80-112">Stop in unmapped code that does not fit into the prolog, epilog, no-mapping-information, or unmanaged category.</span></span>|  
|`STOP_UNMANAGED`|<span data-ttu-id="e9d80-113">Arresta nel codice non gestito.</span><span class="sxs-lookup"><span data-stu-id="e9d80-113">Stop in unmanaged code.</span></span> <span data-ttu-id="e9d80-114">Questo valore è valido solo con il debug di interoperabilità.</span><span class="sxs-lookup"><span data-stu-id="e9d80-114">This value is valid only with interop debugging.</span></span>|  
|`STOP_ALL`|<span data-ttu-id="e9d80-115">Arresta in tutti i tipi di codice non mappato.</span><span class="sxs-lookup"><span data-stu-id="e9d80-115">Stop in all types of unmapped code.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e9d80-116">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="e9d80-116">Remarks</span></span>  
 <span data-ttu-id="e9d80-117">Usare il metodo [ICorDebugStepper:: SetUnmappedStopMask](icordebugstepper-setunmappedstopmask-method.md) per impostare i flag che specificano il codice di cui non è stato eseguito il mapping in cui il gestore di stepper si arresterà.</span><span class="sxs-lookup"><span data-stu-id="e9d80-117">Use the [ICorDebugStepper::SetUnmappedStopMask](icordebugstepper-setunmappedstopmask-method.md) method to set the flags that specify the unmapped code in which the stepper will stop.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e9d80-118">Requisiti</span><span class="sxs-lookup"><span data-stu-id="e9d80-118">Requirements</span></span>  
 <span data-ttu-id="e9d80-119">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e9d80-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e9d80-120">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="e9d80-120">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="e9d80-121">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e9d80-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e9d80-122">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e9d80-122">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e9d80-123">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e9d80-123">See also</span></span>

- [<span data-ttu-id="e9d80-124">Enumerazioni di debug</span><span class="sxs-lookup"><span data-stu-id="e9d80-124">Debugging Enumerations</span></span>](debugging-enumerations.md)

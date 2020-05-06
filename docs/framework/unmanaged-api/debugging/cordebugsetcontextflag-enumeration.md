---
title: Enumerazione CorDebugSetContextFlag
ms.date: 03/30/2017
api_name:
- CorDebugSetContextFlag
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugSetContextFlag
helpviewer_keywords:
- CorDebugSetContextFlag enumeration [.NET Framework debugging]
ms.assetid: b30280bb-fe75-44ed-8589-bcff081fae44
topic_type:
- apiref
ms.openlocfilehash: a3214fc4e52918716f183720c7c616b1fff74bdb
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795677"
---
# <a name="cordebugsetcontextflag-enumeration"></a><span data-ttu-id="6ee6a-102">Enumerazione CorDebugSetContextFlag</span><span class="sxs-lookup"><span data-stu-id="6ee6a-102">CorDebugSetContextFlag Enumeration</span></span>
<span data-ttu-id="6ee6a-103">Indica se il contesto proviene dal frame attivo (o foglia) sullo stack o se è stato calcolato dalla rimozione da un altro frame.</span><span class="sxs-lookup"><span data-stu-id="6ee6a-103">Indicates whether the context is from the active (or leaf) frame on the stack or has been computed by unwinding from another frame.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6ee6a-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="6ee6a-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDebugSetContextFlag  
{  
   SET_CONTEXT_FLAG_ACTIVE_FRAME = 1  
   SET_CONTEXT_FLAG_UNWIND_FRAME = 2  
}  CorDebugSetContextFlag;  
```  
  
## <a name="members"></a><span data-ttu-id="6ee6a-105">Members</span><span class="sxs-lookup"><span data-stu-id="6ee6a-105">Members</span></span>  
  
|<span data-ttu-id="6ee6a-106">Membro</span><span class="sxs-lookup"><span data-stu-id="6ee6a-106">Member</span></span>|<span data-ttu-id="6ee6a-107">Description</span><span class="sxs-lookup"><span data-stu-id="6ee6a-107">Description</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="6ee6a-108">SET_CONTEXT_FLAG_ACTIVE_FRAME</span><span class="sxs-lookup"><span data-stu-id="6ee6a-108">SET_CONTEXT_FLAG_ACTIVE_FRAME</span></span>|<span data-ttu-id="6ee6a-109">Il contesto è il contesto attivo del thread.</span><span class="sxs-lookup"><span data-stu-id="6ee6a-109">The context is the thread’s active context.</span></span>|  
|<span data-ttu-id="6ee6a-110">SET_CONTEXT_FLAG_UNWIND_FRAME</span><span class="sxs-lookup"><span data-stu-id="6ee6a-110">SET_CONTEXT_FLAG_UNWIND_FRAME</span></span>|<span data-ttu-id="6ee6a-111">Il contesto è stato calcolato dalla rimozione da un altro frame.</span><span class="sxs-lookup"><span data-stu-id="6ee6a-111">The context has been computed by unwinding from another frame.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="6ee6a-112">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="6ee6a-112">Remarks</span></span>  
 <span data-ttu-id="6ee6a-113">`CorDebugSetContextFlag`fornisce i valori utilizzati dal metodo [ICorDebugStackWalk:: secontext](icordebugstackwalk-setcontext-method.md) .</span><span class="sxs-lookup"><span data-stu-id="6ee6a-113">`CorDebugSetContextFlag` provides values that are used by the [ICorDebugStackWalk::SetContext](icordebugstackwalk-setcontext-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6ee6a-114">Requisiti</span><span class="sxs-lookup"><span data-stu-id="6ee6a-114">Requirements</span></span>  
 <span data-ttu-id="6ee6a-115">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="6ee6a-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6ee6a-116">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="6ee6a-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="6ee6a-117">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="6ee6a-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="6ee6a-118">**Versioni .NET Framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6ee6a-118">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6ee6a-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="6ee6a-119">See also</span></span>

- [<span data-ttu-id="6ee6a-120">Enumerazioni di debug</span><span class="sxs-lookup"><span data-stu-id="6ee6a-120">Debugging Enumerations</span></span>](debugging-enumerations.md)
- [<span data-ttu-id="6ee6a-121">Debug</span><span class="sxs-lookup"><span data-stu-id="6ee6a-121">Debugging</span></span>](index.md)

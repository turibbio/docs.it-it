---
title: Enumerazione CorDebugExceptionCallbackType
ms.date: 03/30/2017
api_name:
- CorDebugExceptionCallbackType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugExceptionCallbackType
helpviewer_keywords:
- CorDebugExceptionCallbackType enumeration [.NET Framework debugging]
ms.assetid: 4d946ad4-3c19-42cb-bec9-8633325ba769
topic_type:
- apiref
ms.openlocfilehash: d5cdb8c6740970f6a7469be8c763961bf76d6ecc
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795939"
---
# <a name="cordebugexceptioncallbacktype-enumeration"></a><span data-ttu-id="d7727-102">Enumerazione CorDebugExceptionCallbackType</span><span class="sxs-lookup"><span data-stu-id="d7727-102">CorDebugExceptionCallbackType Enumeration</span></span>
<span data-ttu-id="d7727-103">Indica il tipo di callback eseguito da un evento [ICorDebugManagedCallback2:: Exception](icordebugmanagedcallback2-exception-method.md) .</span><span class="sxs-lookup"><span data-stu-id="d7727-103">Indicates the type of callback that is made from an [ICorDebugManagedCallback2::Exception](icordebugmanagedcallback2-exception-method.md) event.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d7727-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="d7727-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDebugExceptionCallbackType {  
    DEBUG_EXCEPTION_FIRST_CHANCE         = 1,  
    DEBUG_EXCEPTION_USER_FIRST_CHANCE    = 2,  
    DEBUG_EXCEPTION_CATCH_HANDLER_FOUND  = 3,  
    DEBUG_EXCEPTION_UNHANDLED            = 4  
} CorDebugExceptionCallbackType;  
```  
  
## <a name="members"></a><span data-ttu-id="d7727-105">Members</span><span class="sxs-lookup"><span data-stu-id="d7727-105">Members</span></span>  
  
|<span data-ttu-id="d7727-106">Membro</span><span class="sxs-lookup"><span data-stu-id="d7727-106">Member</span></span>|<span data-ttu-id="d7727-107">Description</span><span class="sxs-lookup"><span data-stu-id="d7727-107">Description</span></span>|  
|------------|-----------------|  
|`DEBUG_EXCEPTION_FIRST_CHANCE`|<span data-ttu-id="d7727-108">È stata generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="d7727-108">An exception was thrown.</span></span>|  
|`DEBUG_EXCEPTION_USER_FIRST_CHANCE`|<span data-ttu-id="d7727-109">L'eccezione Windup il codice utente immesso.</span><span class="sxs-lookup"><span data-stu-id="d7727-109">The exception windup process entered user code.</span></span>|  
|`DEBUG_EXCEPTION_CATCH_HANDLER_FOUND`|<span data-ttu-id="d7727-110">Il processo Windup dell'eccezione ha `catch` rilevato un blocco nel codice utente.</span><span class="sxs-lookup"><span data-stu-id="d7727-110">The exception windup process found a `catch` block in user code.</span></span>|  
|`DEBUG_EXCEPTION_UNHANDLED`|<span data-ttu-id="d7727-111">L'eccezione non è stata gestita.</span><span class="sxs-lookup"><span data-stu-id="d7727-111">The exception was not handled.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="d7727-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="d7727-112">Requirements</span></span>  
 <span data-ttu-id="d7727-113">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="d7727-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d7727-114">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="d7727-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="d7727-115">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d7727-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d7727-116">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d7727-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d7727-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d7727-117">See also</span></span>

- [<span data-ttu-id="d7727-118">Enumerazioni di debug</span><span class="sxs-lookup"><span data-stu-id="d7727-118">Debugging Enumerations</span></span>](debugging-enumerations.md)

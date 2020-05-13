---
title: Interfaccia ICorDebugThread3
ms.date: 03/30/2017
api_name:
- ICorDebugThread3
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread3
helpviewer_keywords:
- ICorDebugThread3 interface [.NET Framework debugging]
ms.assetid: eb2860ef-06cb-4968-a6c3-6d048ecda2a4
topic_type:
- apiref
ms.openlocfilehash: dc556dfb59e999ed9b7fc5f35c603dc26c35f314
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378713"
---
# <a name="icordebugthread3-interface"></a><span data-ttu-id="a2068-102">Interfaccia ICorDebugThread3</span><span class="sxs-lookup"><span data-stu-id="a2068-102">ICorDebugThread3 Interface</span></span>
<span data-ttu-id="a2068-103">Fornisce il punto di ingresso per [ICorDebugStackWalk](icordebugstackwalk-interface.md) e le interfacce corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="a2068-103">Provides the entry point to the [ICorDebugStackWalk](icordebugstackwalk-interface.md) and corresponding interfaces.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="a2068-104">Metodi</span><span class="sxs-lookup"><span data-stu-id="a2068-104">Methods</span></span>  
  
|<span data-ttu-id="a2068-105">Metodo</span><span class="sxs-lookup"><span data-stu-id="a2068-105">Method</span></span>|<span data-ttu-id="a2068-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a2068-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="a2068-107">Metodo CreateStackWalk</span><span class="sxs-lookup"><span data-stu-id="a2068-107">CreateStackWalk Method</span></span>](icordebugthread3-createstackwalk-method.md)|<span data-ttu-id="a2068-108">Crea un oggetto [ICorDebugStackWalk](icordebugstackwalk-interface.md) per il thread il cui stack si vuole rimuovere.</span><span class="sxs-lookup"><span data-stu-id="a2068-108">Creates an [ICorDebugStackWalk](icordebugstackwalk-interface.md) object for the thread whose stack you want to unwind.</span></span>|  
|[<span data-ttu-id="a2068-109">Metodo GetActiveInternalFrames</span><span class="sxs-lookup"><span data-stu-id="a2068-109">GetActiveInternalFrames Method</span></span>](icordebugthread3-getactiveinternalframes-method.md)|<span data-ttu-id="a2068-110">Restituisce una matrice di frame interni (oggetti[ICorDebugInternalFrame2](icordebuginternalframe2-interface.md) ) nello stack.</span><span class="sxs-lookup"><span data-stu-id="a2068-110">Returns an array of internal frames ([ICorDebugInternalFrame2](icordebuginternalframe2-interface.md) objects) on the stack.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="a2068-111">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="a2068-111">Remarks</span></span>  
 <span data-ttu-id="a2068-112">`ICorDebugThread3`è un'estensione logica dell'interfaccia ICorDebugThread.</span><span class="sxs-lookup"><span data-stu-id="a2068-112">`ICorDebugThread3` is a logical extension to the ICorDebugThread interface.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="a2068-113">Questa interfaccia non supporta la chiamata in modalità remota, tra computer o tra processi.</span><span class="sxs-lookup"><span data-stu-id="a2068-113">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a2068-114">Requisiti</span><span class="sxs-lookup"><span data-stu-id="a2068-114">Requirements</span></span>  
 <span data-ttu-id="a2068-115">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a2068-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a2068-116">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="a2068-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a2068-117">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a2068-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a2068-118">**Versioni .NET Framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a2068-118">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a2068-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a2068-119">See also</span></span>

- [<span data-ttu-id="a2068-120">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="a2068-120">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="a2068-121">Debug</span><span class="sxs-lookup"><span data-stu-id="a2068-121">Debugging</span></span>](index.md)

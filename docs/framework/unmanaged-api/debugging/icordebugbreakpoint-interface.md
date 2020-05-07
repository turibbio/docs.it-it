---
title: Interfaccia ICorDebugBreakpoint
ms.date: 03/30/2017
api_name:
- ICorDebugBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBreakpoint
helpviewer_keywords:
- ICorDebugBreakpoint interface [.NET Framework debugging]
ms.assetid: aa5ad3d7-e1bb-42af-99bc-471224e3bcaa
topic_type:
- apiref
ms.openlocfilehash: b92c3d3328c657762ed002155ef4947a9292b19e
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894737"
---
# <a name="icordebugbreakpoint-interface"></a><span data-ttu-id="e6b0f-102">Interfaccia ICorDebugBreakpoint</span><span class="sxs-lookup"><span data-stu-id="e6b0f-102">ICorDebugBreakpoint Interface</span></span>

<span data-ttu-id="e6b0f-103">Rappresenta un punto di interruzione in una funzione o un punto di controllo su un valore.</span><span class="sxs-lookup"><span data-stu-id="e6b0f-103">Represents a breakpoint in a function, or a watch point on a value.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="e6b0f-104">Metodi</span><span class="sxs-lookup"><span data-stu-id="e6b0f-104">Methods</span></span>  
  
|<span data-ttu-id="e6b0f-105">Metodo</span><span class="sxs-lookup"><span data-stu-id="e6b0f-105">Method</span></span>|<span data-ttu-id="e6b0f-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e6b0f-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="e6b0f-107">Metodo Activate</span><span class="sxs-lookup"><span data-stu-id="e6b0f-107">Activate Method</span></span>](icordebugbreakpoint-activate-method.md)|<span data-ttu-id="e6b0f-108">Imposta lo stato attivo di questo `ICorDebugBreakpoint`oggetto.</span><span class="sxs-lookup"><span data-stu-id="e6b0f-108">Sets the active state of this `ICorDebugBreakpoint`.</span></span>|  
|[<span data-ttu-id="e6b0f-109">Metodo IsActive</span><span class="sxs-lookup"><span data-stu-id="e6b0f-109">IsActive Method</span></span>](icordebugbreakpoint-isactive-method.md)|<span data-ttu-id="e6b0f-110">Ottiene un valore che indica se l' `ICorDebugBreakpoint` oggetto è attivo.</span><span class="sxs-lookup"><span data-stu-id="e6b0f-110">Gets a value that indicates whether this `ICorDebugBreakpoint` is active.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e6b0f-111">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="e6b0f-111">Remarks</span></span>  
 <span data-ttu-id="e6b0f-112">I punti di interruzione non supportano direttamente le espressioni condizionali.</span><span class="sxs-lookup"><span data-stu-id="e6b0f-112">Breakpoints do not directly support conditional expressions.</span></span> <span data-ttu-id="e6b0f-113">Se si desidera una funzionalità di `ICorDebugBreakpoint`questo tipo, un debugger deve implementarlo oltre a.</span><span class="sxs-lookup"><span data-stu-id="e6b0f-113">If such functionality is desired, a debugger must implement it on top of `ICorDebugBreakpoint`.</span></span>  
  
 <span data-ttu-id="e6b0f-114">L'interfaccia ICorDebugFunctionBreakpoint si `ICorDebugBreakpoint` estende per supportare i punti di interruzione all'interno di funzioni.</span><span class="sxs-lookup"><span data-stu-id="e6b0f-114">The ICorDebugFunctionBreakpoint interface extends `ICorDebugBreakpoint` to support breakpoints within functions.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e6b0f-115">Questa interfaccia non supporta la chiamata in modalità remota, tra computer o tra processi.</span><span class="sxs-lookup"><span data-stu-id="e6b0f-115">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e6b0f-116">Requisiti</span><span class="sxs-lookup"><span data-stu-id="e6b0f-116">Requirements</span></span>  
 <span data-ttu-id="e6b0f-117">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e6b0f-117">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e6b0f-118">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="e6b0f-118">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="e6b0f-119">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e6b0f-119">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e6b0f-120">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e6b0f-120">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e6b0f-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e6b0f-121">See also</span></span>

- [<span data-ttu-id="e6b0f-122">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="e6b0f-122">Debugging Interfaces</span></span>](debugging-interfaces.md)

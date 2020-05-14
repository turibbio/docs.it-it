---
title: Interfaccia ICorDebugVariableHomeEnum
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHomeEnum
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHomeEnum
helpviewer_keywords:
- ICorDebugVariableHomeEnum interface [.NET Framework debugging]
ms.assetid: c312ae6d-c8dc-48d6-9f1e-ead515c88fdf
topic_type:
- apiref
ms.openlocfilehash: d5962de8cc2762f6ecf4864c5255da0fe83918e4
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396523"
---
# <a name="icordebugvariablehomeenum-interface"></a><span data-ttu-id="5e82d-102">Interfaccia ICorDebugVariableHomeEnum</span><span class="sxs-lookup"><span data-stu-id="5e82d-102">ICorDebugVariableHomeEnum Interface</span></span>
<span data-ttu-id="5e82d-103">Fornisce un enumeratore per le variabili e gli argomenti locali in una funzione.</span><span class="sxs-lookup"><span data-stu-id="5e82d-103">Provides an enumerator to the local variables and arguments in a function.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="5e82d-104">Metodi</span><span class="sxs-lookup"><span data-stu-id="5e82d-104">Methods</span></span>  
  
|<span data-ttu-id="5e82d-105">Metodo</span><span class="sxs-lookup"><span data-stu-id="5e82d-105">Method</span></span>|<span data-ttu-id="5e82d-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5e82d-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="5e82d-107">Metodo Next</span><span class="sxs-lookup"><span data-stu-id="5e82d-107">Next Method</span></span>](icordebugvariablehomeenum-next-method.md)|<span data-ttu-id="5e82d-108">Ottiene il numero specificato di istanze di [ICorDebugVariableHome](icordebugvariablehome-interface.md) che contengono informazioni sulle variabili e gli argomenti locali in una funzione.</span><span class="sxs-lookup"><span data-stu-id="5e82d-108">Gets the specified number of [ICorDebugVariableHome](icordebugvariablehome-interface.md) instances that contain information about the local variables and arguments in a function.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="5e82d-109">Commenti</span><span class="sxs-lookup"><span data-stu-id="5e82d-109">Remarks</span></span>  
 <span data-ttu-id="5e82d-110">L' `ICorDebugVariableHomeEnum` interfaccia implementa l'interfaccia ICorDebugEnum.</span><span class="sxs-lookup"><span data-stu-id="5e82d-110">The `ICorDebugVariableHomeEnum` interface implements the ICorDebugEnum interface.</span></span>  
  
 <span data-ttu-id="5e82d-111">Un' `ICorDebugVariableHomeEnum` istanza viene popolata con istanze [ICorDebugVariableHome](icordebugvariablehome-interface.md) chiamando il metodo [interfacce icordebugcode4:: EnumerateVariableHomes](icordebugcode4-enumeratevariablehomes-method.md) .</span><span class="sxs-lookup"><span data-stu-id="5e82d-111">An `ICorDebugVariableHomeEnum` instance is populated with [ICorDebugVariableHome](icordebugvariablehome-interface.md) instances by calling the [ICorDebugCode4::EnumerateVariableHomes](icordebugcode4-enumeratevariablehomes-method.md) method.</span></span> <span data-ttu-id="5e82d-112">Ogni istanza di [ICorDebugVariableHome](icordebugvariablehome-interface.md) nell'insieme rappresenta una variabile o un argomento locale in una funzione.</span><span class="sxs-lookup"><span data-stu-id="5e82d-112">Each [ICorDebugVariableHome](icordebugvariablehome-interface.md) instance in the collection represents a local variable or argument in a function.</span></span> <span data-ttu-id="5e82d-113">Gli oggetti [ICorDebugVariableHome](icordebugvariablehome-interface.md) della raccolta possono essere enumerati chiamando il metodo [ICorDebugVariableHomeEnum:: Next](icordebugvariablehomeenum-next-method.md) .</span><span class="sxs-lookup"><span data-stu-id="5e82d-113">The  [ICorDebugVariableHome](icordebugvariablehome-interface.md) objects in the collection can be enumerated by calling the [ICorDebugVariableHomeEnum::Next](icordebugvariablehomeenum-next-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="5e82d-114">Requisiti</span><span class="sxs-lookup"><span data-stu-id="5e82d-114">Requirements</span></span>  
 <span data-ttu-id="5e82d-115">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="5e82d-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5e82d-116">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="5e82d-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="5e82d-117">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="5e82d-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="5e82d-118">**Versioni .NET Framework:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="5e82d-118">**.NET Framework Versions:** [!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5e82d-119">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="5e82d-119">See also</span></span>

- [<span data-ttu-id="5e82d-120">Interfaccia ICorDebugVariableHome</span><span class="sxs-lookup"><span data-stu-id="5e82d-120">ICorDebugVariableHome Interface</span></span>](icordebugvariablehome-interface.md)
- [<span data-ttu-id="5e82d-121">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="5e82d-121">Debugging Interfaces</span></span>](debugging-interfaces.md)

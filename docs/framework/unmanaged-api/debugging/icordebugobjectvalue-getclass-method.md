---
title: Metodo ICorDebugObjectValue::GetClass
ms.date: 03/30/2017
api_name:
- ICorDebugObjectValue.GetClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugObjectValue::GetClass
helpviewer_keywords:
- ICorDebugObjectValue::GetClass method [.NET Framework debugging]
- GetClass method, ICorDebugObjectValue interface [.NET Framework debugging]
ms.assetid: 5be25292-8357-445f-a09b-f997c0de761c
topic_type:
- apiref
ms.openlocfilehash: b0e8fd162ccc1cfc944fb870f493febfe2e5ef42
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207674"
---
# <a name="icordebugobjectvaluegetclass-method"></a><span data-ttu-id="ba7f8-102">Metodo ICorDebugObjectValue::GetClass</span><span class="sxs-lookup"><span data-stu-id="ba7f8-102">ICorDebugObjectValue::GetClass Method</span></span>
<span data-ttu-id="ba7f8-103">Ottiene la classe del valore di questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="ba7f8-103">Gets the class of this object value.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ba7f8-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="ba7f8-104">Syntax</span></span>  
  
```cpp  
HRESULT GetClass (  
    [out] ICorDebugClass     **ppClass  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="ba7f8-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="ba7f8-105">Parameters</span></span>  
 `ppClass`  
 <span data-ttu-id="ba7f8-106">out Puntatore all'indirizzo di un oggetto "ICorDebugClass" che rappresenta la classe del valore dell'oggetto rappresentato da questo oggetto "ICorDebugObjectValue".</span><span class="sxs-lookup"><span data-stu-id="ba7f8-106">[out] A pointer to the address of an "ICorDebugClass" object that represents the class of the object value represented by this "ICorDebugObjectValue" object.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="ba7f8-107">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="ba7f8-107">Remarks</span></span>  
 <span data-ttu-id="ba7f8-108">I `GetClass` metodi e [ICorDebugValue:: GetType](icordebugvalue-gettype-method.md) restituiscono tutti informazioni sul tipo di un valore. entrambi sono sostituiti dai generics-Aware [ICorDebugValue2:: GetExactType](icordebugvalue2-getexacttype-method.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-108">The `GetClass` and [ICorDebugValue::GetType](icordebugvalue-gettype-method.md) methods each return information about the type of a value; they are both superseded by the generics-aware [ICorDebugValue2::GetExactType](icordebugvalue2-getexacttype-method.md).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ba7f8-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="ba7f8-109">Requirements</span></span>  
 <span data-ttu-id="ba7f8-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f8-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ba7f8-111">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="ba7f8-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="ba7f8-112">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="ba7f8-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ba7f8-113">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ba7f8-113">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ba7f8-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ba7f8-114">See also</span></span>

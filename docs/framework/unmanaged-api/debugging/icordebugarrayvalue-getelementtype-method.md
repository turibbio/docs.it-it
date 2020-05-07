---
title: Metodo ICorDebugArrayValue::GetElementType
ms.date: 03/30/2017
api_name:
- ICorDebugArrayValue.GetElementType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugArrayValue::GetElementType
helpviewer_keywords:
- ICorDebugArrayValue::GetElementType method [.NET Framework debugging]
- GetElementType method [.NET Framework debugging]
ms.assetid: ed71961e-ae9b-4dfc-9554-06637696d697
topic_type:
- apiref
ms.openlocfilehash: 8b5a6f4447730ebc6e4b23d3cd06df85b2d7fee6
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895000"
---
# <a name="icordebugarrayvaluegetelementtype-method"></a><span data-ttu-id="ab98b-102">Metodo ICorDebugArrayValue::GetElementType</span><span class="sxs-lookup"><span data-stu-id="ab98b-102">ICorDebugArrayValue::GetElementType Method</span></span>
<span data-ttu-id="ab98b-103">Ottiene un valore che indica il tipo semplice degli elementi nella matrice.</span><span class="sxs-lookup"><span data-stu-id="ab98b-103">Gets a value that indicates the simple type of the elements in the array.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ab98b-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="ab98b-104">Syntax</span></span>  
  
```cpp  
HRESULT GetElementType (  
    [out] CorElementType  *pType  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="ab98b-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="ab98b-105">Parameters</span></span>  
 `pType`  
 <span data-ttu-id="ab98b-106">out Puntatore a un valore dell'enumerazione CorElementType che indica il tipo.</span><span class="sxs-lookup"><span data-stu-id="ab98b-106">[out] A pointer to a value of the CorElementType enumeration that indicates the type.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ab98b-107">Requisiti</span><span class="sxs-lookup"><span data-stu-id="ab98b-107">Requirements</span></span>  
 <span data-ttu-id="ab98b-108">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ab98b-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ab98b-109">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="ab98b-109">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="ab98b-110">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="ab98b-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ab98b-111">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ab98b-111">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>

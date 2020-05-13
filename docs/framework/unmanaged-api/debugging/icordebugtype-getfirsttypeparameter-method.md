---
title: Metodo ICorDebugType::GetFirstTypeParameter
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetFirstTypeParameter
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetFirstTypeParameter
helpviewer_keywords:
- ICorDebugType::GetFirstTypeParameter method [.NET Framework debugging]
- GetFirstTypeParameter method [.NET Framework debugging]
ms.assetid: 35bb594f-af6a-4349-83fe-e98702674e03
topic_type:
- apiref
ms.openlocfilehash: da0097daea183c76f97f0b1966b313e1cb5a557b
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379944"
---
# <a name="icordebugtypegetfirsttypeparameter-method"></a><span data-ttu-id="2efc0-102">Metodo ICorDebugType::GetFirstTypeParameter</span><span class="sxs-lookup"><span data-stu-id="2efc0-102">ICorDebugType::GetFirstTypeParameter Method</span></span>
<span data-ttu-id="2efc0-103">Ottiene un puntatore a interfaccia a un oggetto ICorDebugType che rappresenta il primo <xref:System.Type> parametro del tipo rappresentato da questo oggetto `ICorDebugType` .</span><span class="sxs-lookup"><span data-stu-id="2efc0-103">Gets an interface pointer to an ICorDebugType that represents the first <xref:System.Type> parameter of the type represented by this `ICorDebugType`.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2efc0-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="2efc0-104">Syntax</span></span>  
  
```cpp  
HRESULT GetFirstTypeParameter (  
    [out] ICorDebugType   **value  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="2efc0-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="2efc0-105">Parameters</span></span>  
 `value`  
 <span data-ttu-id="2efc0-106">out Puntatore all'indirizzo di un `ICorDebugType` oggetto che rappresenta il primo parametro.</span><span class="sxs-lookup"><span data-stu-id="2efc0-106">[out] A pointer to the address of an `ICorDebugType` object that represents the first parameter.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="2efc0-107">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="2efc0-107">Remarks</span></span>  
 <span data-ttu-id="2efc0-108">`GetFirstTypeParameter`può essere chiamato nei casi in cui le informazioni aggiuntive sul tipo includono al massimo un parametro di tipo.</span><span class="sxs-lookup"><span data-stu-id="2efc0-108">`GetFirstTypeParameter` can be called in cases where the additional information about the type involves, at most, one type parameter.</span></span> <span data-ttu-id="2efc0-109">In particolare, può essere utilizzata se il tipo è un ELEMENT_TYPE_ARRAY, ELEMENT_TYPE_SZARRAY, ELEMENT_TYPE_BYREF o ELEMENT_TYPE_PTR, come indicato dal metodo [ICorDebugType:: GetType](icordebugtype-gettype-method.md) .</span><span class="sxs-lookup"><span data-stu-id="2efc0-109">In particular, it can be used if the type is an ELEMENT_TYPE_ARRAY, ELEMENT_TYPE_SZARRAY, ELEMENT_TYPE_BYREF, or ELEMENT_TYPE_PTR, as indicated by the [ICorDebugType::GetType](icordebugtype-gettype-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2efc0-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="2efc0-110">Requirements</span></span>  
 <span data-ttu-id="2efc0-111">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="2efc0-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2efc0-112">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="2efc0-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="2efc0-113">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="2efc0-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="2efc0-114">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2efc0-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>

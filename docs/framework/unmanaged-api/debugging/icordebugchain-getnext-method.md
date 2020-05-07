---
title: Metodo ICorDebugChain::GetNext
ms.date: 03/30/2017
api_name:
- ICorDebugChain.GetNext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::GetNext
helpviewer_keywords:
- GetNext method [.NET Framework debugging]
- ICorDebugChain::GetNext method [.NET Framework debugging]
ms.assetid: 8d9744a5-e08b-4ab2-9855-5c22711cc1e6
topic_type:
- apiref
ms.openlocfilehash: 47a90ed63ae217cb150f392ad9196f8d0d5764e3
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894636"
---
# <a name="icordebugchaingetnext-method"></a><span data-ttu-id="d82c4-102">Metodo ICorDebugChain::GetNext</span><span class="sxs-lookup"><span data-stu-id="d82c4-102">ICorDebugChain::GetNext Method</span></span>
<span data-ttu-id="d82c4-103">Ottiene la catena di frame successiva per il thread.</span><span class="sxs-lookup"><span data-stu-id="d82c4-103">Gets the next chain of frames for the thread.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d82c4-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="d82c4-104">Syntax</span></span>  
  
```cpp  
HRESULT GetNext (  
    [out] ICorDebugChain     **ppChain  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="d82c4-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="d82c4-105">Parameters</span></span>  
 `ppChain`  
 <span data-ttu-id="d82c4-106">out Puntatore all'indirizzo di un oggetto ICorDebugChain che rappresenta la catena di frame successiva per il thread.</span><span class="sxs-lookup"><span data-stu-id="d82c4-106">[out] A pointer to the address of an ICorDebugChain object that represents the next chain of frames for the thread.</span></span> <span data-ttu-id="d82c4-107">Se questa catena è l'ultima catena, `ppChain` è null.</span><span class="sxs-lookup"><span data-stu-id="d82c4-107">If this chain is the last chain, `ppChain` is null.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d82c4-108">Requisiti</span><span class="sxs-lookup"><span data-stu-id="d82c4-108">Requirements</span></span>  
 <span data-ttu-id="d82c4-109">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="d82c4-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d82c4-110">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="d82c4-110">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="d82c4-111">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d82c4-111">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d82c4-112">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d82c4-112">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>

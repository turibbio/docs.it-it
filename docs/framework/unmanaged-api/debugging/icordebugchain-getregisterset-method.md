---
title: Metodo ICorDebugChain::GetRegisterSet
ms.date: 03/30/2017
api_name:
- ICorDebugChain.GetRegisterSet
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::GetRegisterSet
helpviewer_keywords:
- ICorDebugChain::GetRegisterSet method [.NET Framework debugging]
- GetRegisterSet method, ICorDebugChain interface [.NET Framework debugging]
ms.assetid: bc4288b6-3331-4ae3-990d-e1d6e62ecb67
topic_type:
- apiref
ms.openlocfilehash: 75cc729a3d0ffa7ac67b29be2defb84b05cc6bb0
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894469"
---
# <a name="icordebugchaingetregisterset-method"></a><span data-ttu-id="281b9-102">Metodo ICorDebugChain::GetRegisterSet</span><span class="sxs-lookup"><span data-stu-id="281b9-102">ICorDebugChain::GetRegisterSet Method</span></span>
<span data-ttu-id="281b9-103">Ottiene il set di registri per la parte attiva della catena.</span><span class="sxs-lookup"><span data-stu-id="281b9-103">Gets the register set for the active part of this chain.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="281b9-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="281b9-104">Syntax</span></span>  
  
```cpp  
HRESULT GetRegisterSet (  
    [out] ICorDebugRegisterSet **ppRegisters  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="281b9-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="281b9-105">Parameters</span></span>  
 `ppRegisters`  
 <span data-ttu-id="281b9-106">out Puntatore all'indirizzo di un oggetto [ICorDebugRegisterSet](icordebugregisterset-interface.md) che rappresenta il set di registri per la parte attiva della catena.</span><span class="sxs-lookup"><span data-stu-id="281b9-106">[out] A pointer to the address of an [ICorDebugRegisterSet](icordebugregisterset-interface.md) object that represents the register set for the active part of this chain.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="281b9-107">Requisiti</span><span class="sxs-lookup"><span data-stu-id="281b9-107">Requirements</span></span>  
 <span data-ttu-id="281b9-108">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="281b9-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="281b9-109">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="281b9-109">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="281b9-110">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="281b9-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="281b9-111">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="281b9-111">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>

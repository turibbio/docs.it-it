---
title: Metodo ICorDebugAssembly2::IsFullyTrusted
ms.date: 03/30/2017
api_name:
- ICorDebugAssembly2.IsFullyTrusted
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAssembly2::IsFullyTrusted
helpviewer_keywords:
- ICorDebugAssembly2::IsFullyTrusted method [.NET Framework debugging]
- IsFullyTrusted method [.NET Framework debugging]
ms.assetid: 26cbd27d-12bf-444a-8197-ccd14d37dda3
topic_type:
- apiref
ms.openlocfilehash: dd82709064fe7f7d912d93f4b3f0248769f02b9e
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894892"
---
# <a name="icordebugassembly2isfullytrusted-method"></a><span data-ttu-id="663c7-102">Metodo ICorDebugAssembly2::IsFullyTrusted</span><span class="sxs-lookup"><span data-stu-id="663c7-102">ICorDebugAssembly2::IsFullyTrusted Method</span></span>
<span data-ttu-id="663c7-103">Ottiene un valore che indica se all'assembly è stata concessa l'attendibilità totale dal sistema di sicurezza del runtime.</span><span class="sxs-lookup"><span data-stu-id="663c7-103">Gets a value that indicates whether the assembly has been granted full trust by the runtime security system.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="663c7-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="663c7-104">Syntax</span></span>  
  
```cpp  
HRESULT IsFullyTrusted(  
    [out] BOOL *pbFullyTrusted  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="663c7-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="663c7-105">Parameters</span></span>  
 `pbFullyTrusted`  
 <span data-ttu-id="663c7-106">out `true` se all'assembly è stata concessa l'attendibilità totale dal sistema di sicurezza di runtime; in caso `false`contrario,.</span><span class="sxs-lookup"><span data-stu-id="663c7-106">[out] `true` if the assembly has been granted full trust by the runtime security system; otherwise, `false`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="663c7-107">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="663c7-107">Remarks</span></span>  
 <span data-ttu-id="663c7-108">Questo metodo restituisce un valore HRESULT di CORDBG_E_NOTREADY se i criteri di sicurezza per l'assembly non sono stati ancora risolti, ovvero se non è stato ancora eseguito alcun codice nell'assembly.</span><span class="sxs-lookup"><span data-stu-id="663c7-108">This method returns an HRESULT of CORDBG_E_NOTREADY if the security policy for the assembly has not yet been resolved, that is, if no code in the assembly has been run yet.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="663c7-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="663c7-109">Requirements</span></span>  
 <span data-ttu-id="663c7-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="663c7-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="663c7-111">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="663c7-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="663c7-112">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="663c7-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="663c7-113">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="663c7-113">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>

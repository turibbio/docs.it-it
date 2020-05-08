---
title: Metodo ICorDebugAppDomainEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomainEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomainEnum::Next method
helpviewer_keywords:
- ICorDebugAppDomainEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugAppDomainEnum interface [.NET Framework debugging]
ms.assetid: b8d1def7-0ebc-4314-a3a2-fd36a75973e7
topic_type:
- apiref
ms.openlocfilehash: 17bf4c92b1e1347a8fe790c8df5937de0f95df4d
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895077"
---
# <a name="icordebugappdomainenumnext-method"></a><span data-ttu-id="83e34-102">Metodo ICorDebugAppDomainEnum::Next</span><span class="sxs-lookup"><span data-stu-id="83e34-102">ICorDebugAppDomainEnum::Next Method</span></span>
<span data-ttu-id="83e34-103">Ottiene il numero specificato di domini applicazione dalla raccolta, a partire dalla posizione corrente del cursore.</span><span class="sxs-lookup"><span data-stu-id="83e34-103">Gets the specified number of application domains from the collection, starting at the current cursor position.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="83e34-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="83e34-104">Syntax</span></span>  
  
```cpp  
HRESULT Next (  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
                           ICorDebugAppDomain *values[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="83e34-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="83e34-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="83e34-106">in Numero di domini applicazione da recuperare.</span><span class="sxs-lookup"><span data-stu-id="83e34-106">[in] The number of application domains to be retrieved.</span></span>  
  
 `values`  
 <span data-ttu-id="83e34-107">out Matrice di puntatori, ciascuno dei quali punta a un oggetto ICorDebugAppDomain che rappresenta un dominio applicazione.</span><span class="sxs-lookup"><span data-stu-id="83e34-107">[out] An array of pointers, each of which points to an ICorDebugAppDomain object that represents an application domain.</span></span>  
  
 `pceltFetched`  
 <span data-ttu-id="83e34-108">out Puntatore al numero di domini applicazione effettivamente restituiti.</span><span class="sxs-lookup"><span data-stu-id="83e34-108">[out] A pointer to the number of application domains actually returned.</span></span> <span data-ttu-id="83e34-109">Questo valore può essere null se `celt` è uno.</span><span class="sxs-lookup"><span data-stu-id="83e34-109">This value may be null if `celt` is one.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="83e34-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="83e34-110">Requirements</span></span>  
 <span data-ttu-id="83e34-111">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="83e34-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="83e34-112">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="83e34-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="83e34-113">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="83e34-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="83e34-114">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="83e34-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>

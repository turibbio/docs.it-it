---
title: Metodo ICorThreadpool::CorQueueUserWorkItem
ms.date: 03/30/2017
api_name:
- ICorThreadpool.CorQueueUserWorkItem
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorQueueUserWorkItem
helpviewer_keywords:
- ICorThreadpool::CorQueueUserWorkItem method [.NET Framework hosting]
- CorQueueUserWorkItem method [.NET Framework hosting]
ms.assetid: 29ac7898-a7c7-433e-8f79-cd5237e0bab8
topic_type:
- apiref
ms.openlocfilehash: 5500f2b84f00e039cbc3f669b49be467789955f0
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762734"
---
# <a name="icorthreadpoolcorqueueuserworkitem-method"></a><span data-ttu-id="78f73-102">Metodo ICorThreadpool::CorQueueUserWorkItem</span><span class="sxs-lookup"><span data-stu-id="78f73-102">ICorThreadpool::CorQueueUserWorkItem Method</span></span>
<span data-ttu-id="78f73-103">Questo metodo supporta l'infrastruttura .NET Framework e non può essere utilizzato direttamente dal codice.</span><span class="sxs-lookup"><span data-stu-id="78f73-103">This method supports the .NET Framework infrastructure and is not intended to be used directly from your code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="78f73-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="78f73-104">Syntax</span></span>  
  
```cpp  
HRESULT CorQueueUserWorkItem (  
    [in] LPTHREAD_START_ROUTINE Function,  
    [in] PVOID                  Context,  
    [in] BOOL                   executeOnlyOnce,  
    [out] BOOL*                 result  
);  
```  
  
## <a name="requirements"></a><span data-ttu-id="78f73-105">Requisiti</span><span class="sxs-lookup"><span data-stu-id="78f73-105">Requirements</span></span>  
 <span data-ttu-id="78f73-106">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="78f73-106">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="78f73-107">**Intestazione:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="78f73-107">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="78f73-108">**Libreria:** Incluso come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="78f73-108">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="78f73-109">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="78f73-109">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="78f73-110">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="78f73-110">See also</span></span>

- [<span data-ttu-id="78f73-111">Interfaccia ICorThreadpool</span><span class="sxs-lookup"><span data-stu-id="78f73-111">ICorThreadpool Interface</span></span>](icorthreadpool-interface.md)

---
title: Funzione _EFN_GetManagedObjectName
ms.date: 03/30/2017
api_name:
- _EFN_GetManagedObjectName
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- _EFN_GetManagedObjectName
helpviewer_keywords:
- _EFN_GetManagedObjectName function [.NET Framework debugging]
ms.assetid: 6e7c6bee-7ced-495f-bf6c-2a5f0c716f7e
topic_type:
- apiref
ms.openlocfilehash: 708ac2e407bf6f87dbe314a0e87cdd16f45b2bcf
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860749"
---
# <a name="_efn_getmanagedobjectname-function"></a><span data-ttu-id="f61a7-102">\_AAPN\_GetManagedObjectName-funzione</span><span class="sxs-lookup"><span data-stu-id="f61a7-102">\_EFN\_GetManagedObjectName Function</span></span>
<span data-ttu-id="f61a7-103">Ottiene il nome di un tipo utilizzando il puntatore all'oggetto gestito fornito.</span><span class="sxs-lookup"><span data-stu-id="f61a7-103">Gets the name of a type using the provided managed object pointer.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f61a7-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="f61a7-104">Syntax</span></span>  
  
```cpp  
HRESULT _EFN_GetManagedObjectName(  
    [in]  PDEBUG_CLIENT  Client,  
    [in]  ULONG64        objAddr,  
    [out] __out_ecount(cbName) PSTR szName,  
    [out] ULONG          cbName  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="f61a7-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="f61a7-105">Parameters</span></span>  
 `Client`  
 <span data-ttu-id="f61a7-106">in Puntatore al client di debug.</span><span class="sxs-lookup"><span data-stu-id="f61a7-106">[in] A pointer to the debug client.</span></span>  
  
 `objAddr`  
 <span data-ttu-id="f61a7-107">in Puntatore A un oggetto gestito.</span><span class="sxs-lookup"><span data-stu-id="f61a7-107">[in] A managed object pointer.</span></span>  
  
 <span data-ttu-id="f61a7-108">szName</span><span class="sxs-lookup"><span data-stu-id="f61a7-108">szName</span></span>  
 <span data-ttu-id="f61a7-109">out Nome del tipo.</span><span class="sxs-lookup"><span data-stu-id="f61a7-109">[out] The name of the type.</span></span>  
  
 `cbName`  
 <span data-ttu-id="f61a7-110">out Numero di caratteri disponibili nel buffer di stringa.</span><span class="sxs-lookup"><span data-stu-id="f61a7-110">[out] The number of characters available in the string buffer.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="f61a7-111">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="f61a7-111">Remarks</span></span>  
 <span data-ttu-id="f61a7-112">Se nel thread non è attualmente presente codice gestito, la funzione restituisce HRESULT SOS_E_NOMANAGEDCODE con un valore della funzione messaggi 0XA0 e un codice di errore 0x1000.</span><span class="sxs-lookup"><span data-stu-id="f61a7-112">If there is no managed code on the thread currently in context, the function returns HRESULT SOS_E_NOMANAGEDCODE with a facility value of 0xa0 and an error code of 0x1000.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f61a7-113">Requisiti</span><span class="sxs-lookup"><span data-stu-id="f61a7-113">Requirements</span></span>  
 <span data-ttu-id="f61a7-114">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="f61a7-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f61a7-115">**Intestazione:** SOS_Stacktrace. h</span><span class="sxs-lookup"><span data-stu-id="f61a7-115">**Header:** SOS_Stacktrace.h</span></span>  
  
 <span data-ttu-id="f61a7-116">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f61a7-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f61a7-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f61a7-117">See also</span></span>

- [<span data-ttu-id="f61a7-118">Funzioni statiche globali di debug</span><span class="sxs-lookup"><span data-stu-id="f61a7-118">Debugging Global Static Functions</span></span>](debugging-global-static-functions.md)

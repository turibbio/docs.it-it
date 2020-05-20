---
title: Metodo ICorPublishProcessEnum::Next
ms.date: 03/30/2017
api_name:
- ICorPublishProcessEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishProcessEnum::Next
helpviewer_keywords:
- ICorPublishProcessEnum::Next method [.NET Framework debugging]
- Next method, ICorPublishProcessEnum interface [.NET Framework debugging]
ms.assetid: 6c399f37-1e38-4ca1-b70d-8ae41f7228b7
topic_type:
- apiref
ms.openlocfilehash: b3bb1857075f857f62ec92ac6a2876a49655c70e
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421059"
---
# <a name="icorpublishprocessenumnext-method"></a><span data-ttu-id="b114f-102">Metodo ICorPublishProcessEnum::Next</span><span class="sxs-lookup"><span data-stu-id="b114f-102">ICorPublishProcessEnum::Next Method</span></span>
<span data-ttu-id="b114f-103">Ottiene il numero specificato di processi dalla raccolta, a partire dalla posizione corrente del cursore.</span><span class="sxs-lookup"><span data-stu-id="b114f-103">Gets the specified number of processes from the collection, starting at the current cursor position.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b114f-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b114f-104">Syntax</span></span>  
  
```cpp  
HRESULT Next (  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorPublishProcess **objects,  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="b114f-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="b114f-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="b114f-106">in Numero di processi da recuperare.</span><span class="sxs-lookup"><span data-stu-id="b114f-106">[in] The number of processes to be retrieved.</span></span>  
  
 `objects`  
 <span data-ttu-id="b114f-107">out Puntatore alla matrice di oggetti [ICorPublishProcess](icorpublishprocess-interface.md) recuperati, ognuno dei quali rappresenta un processo.</span><span class="sxs-lookup"><span data-stu-id="b114f-107">[out] A pointer to the array of retrieved [ICorPublishProcess](icorpublishprocess-interface.md) objects, each of which represents a process.</span></span>  
  
 `pceltFetched`  
 <span data-ttu-id="b114f-108">out Puntatore al numero di processi effettivamente restituiti.</span><span class="sxs-lookup"><span data-stu-id="b114f-108">[out] Pointer to the number of processes actually returned.</span></span> <span data-ttu-id="b114f-109">Questo valore può essere null se `celt` è uno.</span><span class="sxs-lookup"><span data-stu-id="b114f-109">This value may be null if `celt` is one.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b114f-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="b114f-110">Requirements</span></span>  
 <span data-ttu-id="b114f-111">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b114f-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b114f-112">**Intestazione:** CorPub. idl, CorPub. h</span><span class="sxs-lookup"><span data-stu-id="b114f-112">**Header:** CorPub.idl, CorPub.h</span></span>  
  
 <span data-ttu-id="b114f-113">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="b114f-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="b114f-114">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b114f-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b114f-115">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b114f-115">See also</span></span>

- [<span data-ttu-id="b114f-116">Interfaccia ICorPublishProcessEnum</span><span class="sxs-lookup"><span data-stu-id="b114f-116">ICorPublishProcessEnum Interface</span></span>](icorpublishprocessenum-interface.md)

---
title: Metodo ICorDebugGCReferenceEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugGCReferenceEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugGCReferenceEnum::Next
helpviewer_keywords:
- Next method, ICorDebugGCReferenceEnum interface [.NET Framework debugging]
- ICorDebugGCReferenceEnum::Next method [.NET Framework debugging]
ms.assetid: 91b1345c-a94f-4ef8-9696-3823d06c6d05
topic_type:
- apiref
ms.openlocfilehash: 1cf6f9c5fe8777f3333e449a804a3c3a0a64ff19
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213088"
---
# <a name="icordebuggcreferenceenumnext-method"></a><span data-ttu-id="2f395-102">Metodo ICorDebugGCReferenceEnum::Next</span><span class="sxs-lookup"><span data-stu-id="2f395-102">ICorDebugGCReferenceEnum::Next Method</span></span>
<span data-ttu-id="2f395-103">Ottiene il numero specificato di istanze di [COR_GC_REFERENCE](cor-gc-reference-structure.md) che contengono informazioni sugli oggetti che verranno sottoposti a Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="2f395-103">Gets the specified number of [COR_GC_REFERENCE](cor-gc-reference-structure.md) instances that contain information about objects that will be garbage-collected.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2f395-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="2f395-104">Syntax</span></span>  
  
```cpp  
HRESULT Next(  
    [in] ULONG celt,    [out, size_is(celt), length_is(*pceltFetched)] COR_GC_REFERENCE roots[],
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="2f395-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="2f395-105">Parameters</span></span>  
 <span data-ttu-id="2f395-106">celt</span><span class="sxs-lookup"><span data-stu-id="2f395-106">celt</span></span>  
 <span data-ttu-id="2f395-107">in Numero di radici da recuperare.</span><span class="sxs-lookup"><span data-stu-id="2f395-107">[in] The number of roots to be retrieved.</span></span>  
  
 <span data-ttu-id="2f395-108">radici</span><span class="sxs-lookup"><span data-stu-id="2f395-108">roots</span></span>  
 <span data-ttu-id="2f395-109">out Matrice di puntatori, ciascuno dei quali punta a un oggetto [COR_GC_REFERENCE](cor-gc-reference-structure.md) che rappresenta la radice di un oggetto da sottoporre a Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="2f395-109">[out] An array of pointers, each of which points to a [COR_GC_REFERENCE](cor-gc-reference-structure.md) object that represents the root of an object to be garbage-collected.</span></span>  
  
 <span data-ttu-id="2f395-110">pceltFetched</span><span class="sxs-lookup"><span data-stu-id="2f395-110">pceltFetched</span></span>  
 <span data-ttu-id="2f395-111">out Puntatore al numero di oggetti [COR_GC_REFERENCE](cor-gc-reference-structure.md) effettivamente restituiti in `roots` .</span><span class="sxs-lookup"><span data-stu-id="2f395-111">[out] A pointer to the number of [COR_GC_REFERENCE](cor-gc-reference-structure.md) objects actually returned in `roots`.</span></span> <span data-ttu-id="2f395-112">Questo valore può essere `null` se `celt` è 1.</span><span class="sxs-lookup"><span data-stu-id="2f395-112">This value may be `null` if `celt` is 1.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="2f395-113">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="2f395-113">Remarks</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2f395-114">Requisiti</span><span class="sxs-lookup"><span data-stu-id="2f395-114">Requirements</span></span>  
 <span data-ttu-id="2f395-115">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="2f395-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2f395-116">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="2f395-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="2f395-117">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="2f395-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="2f395-118">**Versioni .NET Framework:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2f395-118">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2f395-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2f395-119">See also</span></span>

- [<span data-ttu-id="2f395-120">Interfaccia ICorDebugGCReferenceEnum</span><span class="sxs-lookup"><span data-stu-id="2f395-120">ICorDebugGCReferenceEnum Interface</span></span>](icordebuggcreferenceenum-interface.md)
- [<span data-ttu-id="2f395-121">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="2f395-121">Debugging Interfaces</span></span>](debugging-interfaces.md)

---
title: Metodo ICorDebugILCode::GetEHClauses
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILCode.GetEHClauses
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: cf7a0e00-06ae-47a5-8037-598b26196802
topic_type:
- apiref
ms.openlocfilehash: e1fd68cd079b381d941d416831133c54e49ac48a
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210384"
---
# <a name="icordebugilcodegetehclauses-method"></a><span data-ttu-id="5de04-102">Metodo ICorDebugILCode::GetEHClauses</span><span class="sxs-lookup"><span data-stu-id="5de04-102">ICorDebugILCode::GetEHClauses Method</span></span>
<span data-ttu-id="5de04-103">[Supportato in .NET Framework 4.5.2 e versioni successive]</span><span class="sxs-lookup"><span data-stu-id="5de04-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="5de04-104">Restituisce un puntatore a un elenco di clausole di gestione delle eccezioni (EH) definite per questo linguaggio intermedio (IL).</span><span class="sxs-lookup"><span data-stu-id="5de04-104">Returns a pointer to a list of exception handling (EH) clauses that are defined for this intermediate language (IL).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5de04-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="5de04-105">Syntax</span></span>  
  
```cpp
HRESULT GetEHClauses(  
   [in] ULONG32 cClauses,  
   [out] ULONG32 * pcClauses,  
   [out, size_is(cClauses), length_is(*pcClauses)] CorDebugEHClause clauses[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="5de04-106">Parametri</span><span class="sxs-lookup"><span data-stu-id="5de04-106">Parameters</span></span>  
 `cClauses`  
 <span data-ttu-id="5de04-107">[in] Capacità di memoria della matrice `clauses`.</span><span class="sxs-lookup"><span data-stu-id="5de04-107">[in] The storage capacity of the `clauses` array.</span></span> <span data-ttu-id="5de04-108">Per ulteriori informazioni, vedere le sezione Note.</span><span class="sxs-lookup"><span data-stu-id="5de04-108">See the Remarks section for more information.</span></span>  
  
 `pcClauses`  
 <span data-ttu-id="5de04-109">[out] Numero di clausole le cui informazioni vengono scritte nella matrice `clauses`.</span><span class="sxs-lookup"><span data-stu-id="5de04-109">[out] The number of clauses about which information is written to the `clauses` array.</span></span>  
  
 <span data-ttu-id="5de04-110">clausole</span><span class="sxs-lookup"><span data-stu-id="5de04-110">clauses</span></span>  
 <span data-ttu-id="5de04-111">out Matrice di oggetti [CorDebugEHClause](cordebugehclause-structure.md) che contengono informazioni sulle clausole di gestione delle eccezioni definite per questo il.</span><span class="sxs-lookup"><span data-stu-id="5de04-111">[out] An array of [CorDebugEHClause](cordebugehclause-structure.md) objects that contain information on exception handling clauses defined for this IL.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="5de04-112">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="5de04-112">Remarks</span></span>  
 <span data-ttu-id="5de04-113">Se `cClauses` è 0 e `pcClauses` è diverso da**null**, `pcClauses` viene impostato sul numero di clausole di gestione delle eccezioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="5de04-113">If `cClauses` is 0 and `pcClauses` is non-**null**, `pcClauses` is set to the number of available exception handling clauses.</span></span> <span data-ttu-id="5de04-114">Se `cClauses` è diverso da zero, rappresenta la capacità di memoria della matrice `clauses`.</span><span class="sxs-lookup"><span data-stu-id="5de04-114">If `cClauses` is non-zero, it represents the storage capacity of the `clauses` array.</span></span> <span data-ttu-id="5de04-115">Quando il metodo restituisce un valore, `clauses` contiene un massimo di `cClauses` elementi e `pcClauses` viene impostato sul numero di clausole effettivamente scritte nella matrice `clauses`.</span><span class="sxs-lookup"><span data-stu-id="5de04-115">When the method returns, `clauses` contains a maximum of `cClauses` items, and `pcClauses` is set to the number of clauses actually written to the `clauses` array.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="5de04-116">Requisiti</span><span class="sxs-lookup"><span data-stu-id="5de04-116">Requirements</span></span>  
 <span data-ttu-id="5de04-117">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="5de04-117">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5de04-118">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="5de04-118">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="5de04-119">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="5de04-119">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="5de04-120">**Versioni .NET Framework:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="5de04-120">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5de04-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5de04-121">See also</span></span>

- [<span data-ttu-id="5de04-122">Interfaccia ICorDebugILCode</span><span class="sxs-lookup"><span data-stu-id="5de04-122">ICorDebugILCode Interface</span></span>](icordebugilcode-interface.md)
- [<span data-ttu-id="5de04-123">Struttura CorDebugEHClause</span><span class="sxs-lookup"><span data-stu-id="5de04-123">CorDebugEHClause Structure</span></span>](cordebugehclause-structure.md)
- [<span data-ttu-id="5de04-124">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="5de04-124">Debugging Interfaces</span></span>](debugging-interfaces.md)

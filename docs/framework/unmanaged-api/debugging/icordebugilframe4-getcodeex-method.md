---
title: Metodo ICorDebugILFrame4::GetCodeEx
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILFrame4.GetLocalVariableEx
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: aeda0e42-29ee-4ca8-9f21-ac4641677a62
topic_type:
- apiref
ms.openlocfilehash: 582e28c18f36b253425b1e0a2034cdd262fddd57
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213738"
---
# <a name="icordebugilframe4getcodeex-method"></a><span data-ttu-id="b0d04-102">Metodo ICorDebugILFrame4::GetCodeEx</span><span class="sxs-lookup"><span data-stu-id="b0d04-102">ICorDebugILFrame4::GetCodeEx Method</span></span>
<span data-ttu-id="b0d04-103">[Supportato in .NET Framework 4.5.2 e versioni successive]</span><span class="sxs-lookup"><span data-stu-id="b0d04-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="b0d04-104">Recupera un puntatore al codice eseguito da questo stack frame.</span><span class="sxs-lookup"><span data-stu-id="b0d04-104">Gets a pointer to the code that this stack frame is executing.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b0d04-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b0d04-105">Syntax</span></span>  
  
```cpp
HRESULT GetCodeEx(  
   [in] ILCodeKind flags,
   [out] ICorDebugCode **ppCode  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="b0d04-106">Parametri</span><span class="sxs-lookup"><span data-stu-id="b0d04-106">Parameters</span></span>  
 `flags`  
 <span data-ttu-id="b0d04-107">in Membro di enumerazione [ILCodeKind](ilcodekind-enumeration.md) che specifica se il linguaggio intermedio (il) definito dalla richiesta ReJIT del profiler è incluso nel frame.</span><span class="sxs-lookup"><span data-stu-id="b0d04-107">[in] An [ILCodeKind](ilcodekind-enumeration.md) enumeration member that specifies whether the intermediate language (IL) defined by the profiler's ReJIT request is included in the frame.</span></span>  
  
 `ppCode`  
 <span data-ttu-id="b0d04-108">out Puntatore all'indirizzo di un oggetto "ICorDebugCode" che rappresenta il codice in esecuzione nel stack frame.</span><span class="sxs-lookup"><span data-stu-id="b0d04-108">[out] A pointer to the address of an "ICorDebugCode" object that represents the code that this stack frame is executing.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b0d04-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="b0d04-109">Remarks</span></span>  
 <span data-ttu-id="b0d04-110">Questo metodo è simile al metodo [ICorDebugFrame:: GetCode](icordebugframe-getcode-method.md) , ad eccezione del fatto che accede facoltativamente al codice definito dalla richiesta ReJIT del profiler.</span><span class="sxs-lookup"><span data-stu-id="b0d04-110">This method is similar to the [ICorDebugFrame::GetCode](icordebugframe-getcode-method.md) method, except that it optionally accesses code defined by the profiler's ReJIT request.</span></span> <span data-ttu-id="b0d04-111">La chiamata di questo metodo con un `flags` valore `ILCODE_ORIGINAL_IL` equivale alla chiamata a [GetCode](icordebugframe-getcode-method.md); se il metodo è instrumentato, il relativo il non sarà accessibile.</span><span class="sxs-lookup"><span data-stu-id="b0d04-111">Calling this method with a `flags` value of `ILCODE_ORIGINAL_IL` is equivalent to calling [GetCode](icordebugframe-getcode-method.md); if the method is instrumented, its IL will not be accessible.</span></span> <span data-ttu-id="b0d04-112">`ILCODE_REJIT_IL` consente al debugger di accedere al linguaggio intermedio definito dalla richiesta ReJIT del profiler.</span><span class="sxs-lookup"><span data-stu-id="b0d04-112">`ILCODE_REJIT_IL` allows the debugger to access the IL defined by the profiler's ReJIT request.</span></span> <span data-ttu-id="b0d04-113">Se il linguaggio intermedio non è instrumentato, `ppCode` è **null**e il metodo restituisce `S_OK` .</span><span class="sxs-lookup"><span data-stu-id="b0d04-113">If the IL is not instrumented, `ppCode` is **null**, and the method returns `S_OK`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b0d04-114">Requisiti</span><span class="sxs-lookup"><span data-stu-id="b0d04-114">Requirements</span></span>  
 <span data-ttu-id="b0d04-115">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b0d04-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b0d04-116">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="b0d04-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="b0d04-117">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="b0d04-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="b0d04-118">**Versioni .NET Framework:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b0d04-118">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b0d04-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b0d04-119">See also</span></span>

- [<span data-ttu-id="b0d04-120">Interfaccia ICorDebugILFrame4</span><span class="sxs-lookup"><span data-stu-id="b0d04-120">ICorDebugILFrame4 Interface</span></span>](icordebugilframe4-interface.md)
- [<span data-ttu-id="b0d04-121">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="b0d04-121">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="b0d04-122">ReJIT: Guida alle procedure</span><span class="sxs-lookup"><span data-stu-id="b0d04-122">ReJIT: A How-To Guide</span></span>](https://docs.microsoft.com/archive/blogs/davbr/rejit-a-how-to-guide)

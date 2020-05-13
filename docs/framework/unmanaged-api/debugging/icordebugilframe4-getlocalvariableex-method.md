---
title: Metodo ICorDebugILFrame4::GetLocalVariableEx
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILFrame4.GetCodeEx
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 0c8676f8-ca0d-4998-b64d-fefac7e38912
topic_type:
- apiref
ms.openlocfilehash: 8d6ef550309ea7f8bae616a5f7e5c41b4f07374a
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213725"
---
# <a name="icordebugilframe4getlocalvariableex-method"></a><span data-ttu-id="15ab1-102">Metodo ICorDebugILFrame4::GetLocalVariableEx</span><span class="sxs-lookup"><span data-stu-id="15ab1-102">ICorDebugILFrame4::GetLocalVariableEx Method</span></span>
<span data-ttu-id="15ab1-103">[Supportato in .NET Framework 4.5.2 e versioni successive]</span><span class="sxs-lookup"><span data-stu-id="15ab1-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="15ab1-104">Recupera il valore della variabile locale in questo stack frame del linguaggio intermedio e facoltativamente accede a una variabile aggiunta nella strumentazione ReJIT del profiler.</span><span class="sxs-lookup"><span data-stu-id="15ab1-104">Gets the value of the specified local variable in this intermediate language (IL) stack frame, and optionally accesses a variable added in profiler ReJIT instrumentation.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="15ab1-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="15ab1-105">Syntax</span></span>  
  
```cpp
HRESULT GetLocalVariableEx(  
   [in] ILCodeKind flags,
   [in] DWORD dwIndex,
   [out] ICorDebugValue **ppValue  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="15ab1-106">Parametri</span><span class="sxs-lookup"><span data-stu-id="15ab1-106">Parameters</span></span>  
 `flags`  
 <span data-ttu-id="15ab1-107">in Membro di enumerazione [ILCodeKind](ilcodekind-enumeration.md) che specifica se una variabile aggiunta nella strumentazione ReJIT del profiler è inclusa nel frame.</span><span class="sxs-lookup"><span data-stu-id="15ab1-107">[in] An [ILCodeKind](ilcodekind-enumeration.md) enumeration member that specifies whether a variable added in profiler ReJIT instrumentation is included in the frame.</span></span>  
  
 `dwIndex`  
 <span data-ttu-id="15ab1-108">[in] Indice della variabile locale nello stack frame del linguaggio intermedio.</span><span class="sxs-lookup"><span data-stu-id="15ab1-108">[in] The index of the local variable in the IL stack frame.</span></span>  
  
 `ppValue`  
 <span data-ttu-id="15ab1-109">out Puntatore all'indirizzo di un oggetto "ICorDebugValue" che rappresenta il valore recuperato.</span><span class="sxs-lookup"><span data-stu-id="15ab1-109">[out] A pointer to the address of an "ICorDebugValue" object that represents the retrieved value.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="15ab1-110">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="15ab1-110">Remarks</span></span>  
 <span data-ttu-id="15ab1-111">Questo metodo è simile al metodo [GetLocalVariable](icordebugilframe-getlocalvariable-method.md) , ad eccezione del fatto che accede facoltativamente a una variabile aggiunta nella strumentazione ReJIT del profiler.</span><span class="sxs-lookup"><span data-stu-id="15ab1-111">This method is similar to the [GetLocalVariable](icordebugilframe-getlocalvariable-method.md) method, except that it optionally accesses a variable added in profiler ReJIT instrumentation.</span></span> <span data-ttu-id="15ab1-112">La chiamata di questo metodo con un `flags` valore `ILCODE_ORIGINAL_IL` equivale alla chiamata a [GetLocalVariable](icordebugilframe-getlocalvariable-method.md); se il metodo è instrumentato con variabili locali aggiuntive, non è possibile accedere a tali variabili.</span><span class="sxs-lookup"><span data-stu-id="15ab1-112">Calling this method with a `flags` value of `ILCODE_ORIGINAL_IL` is equivalent to calling [GetLocalVariable](icordebugilframe-getlocalvariable-method.md); if the method is instrumented with additional local variables, those variables cannot be accessed.</span></span> <span data-ttu-id="15ab1-113">`ILCODE_REJIT_IL` consente al debugger di accedere alle variabili locali aggiunte nella strumentazione ReJIT del profiler.</span><span class="sxs-lookup"><span data-stu-id="15ab1-113">`ILCODE_REJIT_IL` allows the debugger to access the local variables added in profiler ReJIT instrumentation.</span></span> <span data-ttu-id="15ab1-114">Se il linguaggio intermedio non è instrumentato, il metodo restituisce `E_INVALIDARG`.</span><span class="sxs-lookup"><span data-stu-id="15ab1-114">If the IL is not instrumented, the method returns `E_INVALIDARG`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="15ab1-115">Requisiti</span><span class="sxs-lookup"><span data-stu-id="15ab1-115">Requirements</span></span>  
 <span data-ttu-id="15ab1-116">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="15ab1-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="15ab1-117">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="15ab1-117">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="15ab1-118">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="15ab1-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="15ab1-119">**Versioni .NET Framework:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="15ab1-119">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="15ab1-120">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="15ab1-120">See also</span></span>

- [<span data-ttu-id="15ab1-121">Interfaccia ICorDebugILFrame4</span><span class="sxs-lookup"><span data-stu-id="15ab1-121">ICorDebugILFrame4 Interface</span></span>](icordebugilframe4-interface.md)
- [<span data-ttu-id="15ab1-122">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="15ab1-122">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="15ab1-123">ReJIT: Guida alle procedure</span><span class="sxs-lookup"><span data-stu-id="15ab1-123">ReJIT: A How-To Guide</span></span>](https://docs.microsoft.com/archive/blogs/davbr/rejit-a-how-to-guide)

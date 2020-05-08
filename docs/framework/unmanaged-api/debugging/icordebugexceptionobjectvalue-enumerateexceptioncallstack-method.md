---
title: Metodo ICorDebugExceptionObjectValue::EnumerateExceptionCallStack
ms.date: 03/30/2017
api_name:
- ICorDebugExceptionObjectValue.EnumerateExceptionCallStack
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugExceptionObjectValue::EnumerateExceptionCallStack
helpviewer_keywords:
- EnumerateExceptionCallStack method, ICorDebugExceptionObjectValue interface [.NET Framework debugging]
- ICorDebugExceptionObjectValue::EnumerateExceptionCallStack method [.NET Framework debugging]
ms.assetid: 00c64533-15dd-47f4-bb97-fe80a1ebadef
topic_type:
- apiref
ms.openlocfilehash: e45b180ac6d943d89740ad7ae10500ea4ad1aa9c
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/08/2020
ms.locfileid: "82975966"
---
# <a name="icordebugexceptionobjectvalueenumerateexceptioncallstack-method"></a><span data-ttu-id="362f6-102">Metodo ICorDebugExceptionObjectValue::EnumerateExceptionCallStack</span><span class="sxs-lookup"><span data-stu-id="362f6-102">ICorDebugExceptionObjectValue::EnumerateExceptionCallStack Method</span></span>
<span data-ttu-id="362f6-103">Ottiene un enumeratore per lo stack di chiamate incorporato in un oggetto eccezione.</span><span class="sxs-lookup"><span data-stu-id="362f6-103">Gets an enumerator to the call stack embedded in an exception object.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="362f6-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="362f6-104">Syntax</span></span>  
  
```cpp  
HRESULT EnumerateExceptionCallStack(  
    [out] ICorDebugExceptionObjectCallStackEnum **ppCallStackEnum  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="362f6-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="362f6-105">Parameters</span></span>  
 <span data-ttu-id="362f6-106">ppCallStackEnum</span><span class="sxs-lookup"><span data-stu-id="362f6-106">ppCallStackEnum</span></span>  
 <span data-ttu-id="362f6-107">out Puntatore all'indirizzo di un oggetto interfaccia [ICorDebugExceptionObjectCallStackEnum](icordebugexceptionobjectcallstackenum-interface.md) che è un enumeratore di analisi dello stack per un oggetto eccezione gestita.</span><span class="sxs-lookup"><span data-stu-id="362f6-107">[out] A pointer to the address of an [ICorDebugExceptionObjectCallStackEnum](icordebugexceptionobjectcallstackenum-interface.md) interface object that is a stack trace enumerator for a managed exception object.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="362f6-108">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="362f6-108">Remarks</span></span>  
 <span data-ttu-id="362f6-109">Se non sono disponibili informazioni sullo stack di chiamate, il `S_OK`metodo restituisce e [ICorDebugExceptionObjectCallStackEnum](icordebugexceptionobjectcallstackenum-interface.md) è un enumeratore valido con lunghezza pari a 0.</span><span class="sxs-lookup"><span data-stu-id="362f6-109">If no call stack information is available, the method returns `S_OK`, and [ICorDebugExceptionObjectCallStackEnum](icordebugexceptionobjectcallstackenum-interface.md) is a valid enumerator with a length of 0.</span></span> <span data-ttu-id="362f6-110">Se il metodo non è in grado di recuperare informazioni sulla traccia dello stack, `E_FAIL` il valore restituito è e non viene restituito alcun enumeratore.</span><span class="sxs-lookup"><span data-stu-id="362f6-110">If the method is unable to retrieve stack trace information, the return value is `E_FAIL` and no enumerator is returned.</span></span>  
  
 <span data-ttu-id="362f6-111">L'oggetto [ICorDebugExceptionObjectCallStackEnum](icordebugexceptionobjectcallstackenum-interface.md) è responsabile della decodifica dei dati di traccia dello stack dal `_stackTrace` campo dell'oggetto eccezione.</span><span class="sxs-lookup"><span data-stu-id="362f6-111">The [ICorDebugExceptionObjectCallStackEnum](icordebugexceptionobjectcallstackenum-interface.md) object is responsible for decoding the stack trace data from the `_stackTrace` field of the exception object.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="362f6-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="362f6-112">Requirements</span></span>  
 <span data-ttu-id="362f6-113">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="362f6-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="362f6-114">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="362f6-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="362f6-115">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="362f6-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="362f6-116">**Versioni .NET Framework:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="362f6-116">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="362f6-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="362f6-117">See also</span></span>

- [<span data-ttu-id="362f6-118">Interfaccia ICorDebugExceptionObjectValue</span><span class="sxs-lookup"><span data-stu-id="362f6-118">ICorDebugExceptionObjectValue Interface</span></span>](icordebugexceptionobjectvalue-interface.md)
- [<span data-ttu-id="362f6-119">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="362f6-119">Debugging Interfaces</span></span>](debugging-interfaces.md)

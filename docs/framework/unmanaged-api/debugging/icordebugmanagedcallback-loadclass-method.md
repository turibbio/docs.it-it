---
title: Metodo ICorDebugManagedCallback::LoadClass
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.LoadClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::LoadClass
helpviewer_keywords:
- ICorDebugManagedCallback::LoadClass method [.NET Framework debugging]
- LoadClass method [.NET Framework debugging]
ms.assetid: e58dac7b-85c3-41ca-b9aa-3a7fc9ae6680
topic_type:
- apiref
ms.openlocfilehash: 5d35ab4610ffa04d15dd2404fdf8010308bcb42a
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212733"
---
# <a name="icordebugmanagedcallbackloadclass-method"></a><span data-ttu-id="3fe85-102">Metodo ICorDebugManagedCallback::LoadClass</span><span class="sxs-lookup"><span data-stu-id="3fe85-102">ICorDebugManagedCallback::LoadClass Method</span></span>
<span data-ttu-id="3fe85-103">Notifica al debugger che è stata caricata una classe.</span><span class="sxs-lookup"><span data-stu-id="3fe85-103">Notifies the debugger that a class has been loaded.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3fe85-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="3fe85-104">Syntax</span></span>  
  
```cpp  
HRESULT LoadClass (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugClass     *c  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="3fe85-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="3fe85-105">Parameters</span></span>  
 `pAppDomain`  
 <span data-ttu-id="3fe85-106">in Puntatore a un oggetto ICorDebugAppDomain che rappresenta il dominio applicazione in cui è stata caricata la classe.</span><span class="sxs-lookup"><span data-stu-id="3fe85-106">[in] A pointer to an ICorDebugAppDomain object that represents the application domain into which the class has been loaded.</span></span>  
  
 `c`  
 <span data-ttu-id="3fe85-107">in Puntatore a un oggetto ICorDebugClass che rappresenta la classe.</span><span class="sxs-lookup"><span data-stu-id="3fe85-107">[in] A pointer to an ICorDebugClass object that represents the class.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="3fe85-108">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="3fe85-108">Remarks</span></span>  
 <span data-ttu-id="3fe85-109">Questo callback si verifica solo se è stato abilitato il caricamento della classe per il modulo che contiene la classe.</span><span class="sxs-lookup"><span data-stu-id="3fe85-109">This callback occurs only if class loading has been enabled for the module that contains the class.</span></span> <span data-ttu-id="3fe85-110">Il caricamento delle classi è sempre abilitato per i moduli dinamici.</span><span class="sxs-lookup"><span data-stu-id="3fe85-110">Class loading is always enabled for dynamic modules.</span></span>  
  
 <span data-ttu-id="3fe85-111">Il `LoadClass` callback fornisce un tempo appropriato per associare i punti di interruzione alle classi appena generate nei moduli dinamici.</span><span class="sxs-lookup"><span data-stu-id="3fe85-111">The `LoadClass` callback provides an appropriate time to bind breakpoints to newly generated classes in dynamic modules.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3fe85-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="3fe85-112">Requirements</span></span>  
 <span data-ttu-id="3fe85-113">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3fe85-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3fe85-114">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="3fe85-114">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="3fe85-115">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="3fe85-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="3fe85-116">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3fe85-116">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3fe85-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3fe85-117">See also</span></span>

- [<span data-ttu-id="3fe85-118">Metodo UnloadClass</span><span class="sxs-lookup"><span data-stu-id="3fe85-118">UnloadClass Method</span></span>](icordebugmanagedcallback-unloadclass-method.md)
- [<span data-ttu-id="3fe85-119">Interfaccia ICorDebugManagedCallback</span><span class="sxs-lookup"><span data-stu-id="3fe85-119">ICorDebugManagedCallback Interface</span></span>](icordebugmanagedcallback-interface.md)

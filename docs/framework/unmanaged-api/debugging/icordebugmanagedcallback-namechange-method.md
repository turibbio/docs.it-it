---
title: Metodo ICorDebugManagedCallback::NameChange
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.NameChange
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::NameChange
helpviewer_keywords:
- ICorDebugManagedCallback::NameChange method [.NET Framework debugging]
- NameChange method [.NET Framework debugging]
ms.assetid: a7018a0e-880e-4b68-b52a-1cd22c7aad62
topic_type:
- apiref
ms.openlocfilehash: 48bfce9966ff12fe1b425fbcd9a81860628a54e6
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212672"
---
# <a name="icordebugmanagedcallbacknamechange-method"></a><span data-ttu-id="bee1d-102">Metodo ICorDebugManagedCallback::NameChange</span><span class="sxs-lookup"><span data-stu-id="bee1d-102">ICorDebugManagedCallback::NameChange Method</span></span>
<span data-ttu-id="bee1d-103">Notifica al debugger che il nome di un dominio dell'applicazione o di un thread è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="bee1d-103">Notifies the debugger that the name of either an application domain or a thread has changed.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="bee1d-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="bee1d-104">Syntax</span></span>  
  
```cpp  
HRESULT NameChange (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugThread    *pThread  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="bee1d-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="bee1d-105">Parameters</span></span>  
 `pAppDomain`  
 <span data-ttu-id="bee1d-106">in Puntatore a un oggetto ICorDebugAppDomain che rappresenta il dominio applicazione a cui è stata apportata una modifica del nome o che contiene il thread con una modifica del nome.</span><span class="sxs-lookup"><span data-stu-id="bee1d-106">[in] A pointer to an ICorDebugAppDomain object that represents the application domain that either had a name change or that contains the thread that had a name change.</span></span>  
  
 `pThread`  
 <span data-ttu-id="bee1d-107">in Puntatore a un oggetto ICorDebugThread che rappresenta il thread con una modifica del nome.</span><span class="sxs-lookup"><span data-stu-id="bee1d-107">[in] A pointer to an ICorDebugThread object that represents the thread that had a name change.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="bee1d-108">Requisiti</span><span class="sxs-lookup"><span data-stu-id="bee1d-108">Requirements</span></span>  
 <span data-ttu-id="bee1d-109">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="bee1d-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="bee1d-110">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="bee1d-110">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="bee1d-111">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="bee1d-111">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="bee1d-112">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="bee1d-112">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="bee1d-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="bee1d-113">See also</span></span>

- [<span data-ttu-id="bee1d-114">Interfaccia ICorDebugManagedCallback</span><span class="sxs-lookup"><span data-stu-id="bee1d-114">ICorDebugManagedCallback Interface</span></span>](icordebugmanagedcallback-interface.md)

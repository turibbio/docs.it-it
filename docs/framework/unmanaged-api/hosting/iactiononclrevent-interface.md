---
title: Interfaccia IActionOnCLREvent
ms.date: 03/30/2017
api_name:
- IActionOnCLREvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IActionOnCLREvent
helpviewer_keywords:
- IActionOnCLREvent interface [.NET Framework hosting]
ms.assetid: b5f9b41e-7301-429c-911f-21d5422292b3
topic_type:
- apiref
ms.openlocfilehash: 4e72cd8bee2cb4f35155d7b99cfe8d9cf63f463a
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616073"
---
# <a name="iactiononclrevent-interface"></a><span data-ttu-id="7ca5e-102">Interfaccia IActionOnCLREvent</span><span class="sxs-lookup"><span data-stu-id="7ca5e-102">IActionOnCLREvent Interface</span></span>
<span data-ttu-id="7ca5e-103">Fornisce il metodo [IActionOnCLREvent:: OnEvent](../../../../docs/framework/unmanaged-api/hosting/iactiononclrevent-onevent-method.md) , che esegue i callback sugli eventi che sono stati registrati tramite una chiamata al metodo [ICLROnEventManager:: RegisterActionOnEvent](iclroneventmanager-registeractiononevent-method.md) .</span><span class="sxs-lookup"><span data-stu-id="7ca5e-103">Provides the [IActionOnCLREvent::OnEvent](../../../../docs/framework/unmanaged-api/hosting/iactiononclrevent-onevent-method.md) method, which performs callbacks on events that have been registered by using a call to the [ICLROnEventManager::RegisterActionOnEvent](iclroneventmanager-registeractiononevent-method.md) method.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="7ca5e-104">Metodi</span><span class="sxs-lookup"><span data-stu-id="7ca5e-104">Methods</span></span>  
  
|<span data-ttu-id="7ca5e-105">Metodo</span><span class="sxs-lookup"><span data-stu-id="7ca5e-105">Method</span></span>|<span data-ttu-id="7ca5e-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7ca5e-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="7ca5e-107">Metodo OnEvent</span><span class="sxs-lookup"><span data-stu-id="7ca5e-107">OnEvent Method</span></span>](iactiononclrevent-onevent-method.md)|<span data-ttu-id="7ca5e-108">Esegue un callback per un evento registrato.</span><span class="sxs-lookup"><span data-stu-id="7ca5e-108">Performs a callback for a registered event.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="7ca5e-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="7ca5e-109">Requirements</span></span>  
 <span data-ttu-id="7ca5e-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7ca5e-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7ca5e-111">**Intestazione:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="7ca5e-111">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="7ca5e-112">**Libreria:** Incluso come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="7ca5e-112">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="7ca5e-113">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7ca5e-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7ca5e-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7ca5e-114">See also</span></span>

- [<span data-ttu-id="7ca5e-115">Enumerazione EClrEvent</span><span class="sxs-lookup"><span data-stu-id="7ca5e-115">EClrEvent Enumeration</span></span>](eclrevent-enumeration.md)
- [<span data-ttu-id="7ca5e-116">Interfaccia ICLRControl</span><span class="sxs-lookup"><span data-stu-id="7ca5e-116">ICLRControl Interface</span></span>](iclrcontrol-interface.md)
- [<span data-ttu-id="7ca5e-117">Interfaccia ICLROnEventManager</span><span class="sxs-lookup"><span data-stu-id="7ca5e-117">ICLROnEventManager Interface</span></span>](iclroneventmanager-interface.md)
- [<span data-ttu-id="7ca5e-118">Interfacce di hosting</span><span class="sxs-lookup"><span data-stu-id="7ca5e-118">Hosting Interfaces</span></span>](hosting-interfaces.md)

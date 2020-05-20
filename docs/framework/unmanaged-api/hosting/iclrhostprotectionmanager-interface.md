---
title: Interfaccia ICLRHostProtectionManager
ms.date: 03/30/2017
api_name:
- ICLRHostProtectionManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRHostProtectionManager
helpviewer_keywords:
- ICLRHostProtectionManager interface [.NET Framework hosting]
ms.assetid: ce2770ae-23d0-45d9-8bcf-46504ac5020e
topic_type:
- apiref
ms.openlocfilehash: 7b1fc70380fff3c551c56043f49c2deda507e366
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703848"
---
# <a name="iclrhostprotectionmanager-interface"></a><span data-ttu-id="d42a9-102">Interfaccia ICLRHostProtectionManager</span><span class="sxs-lookup"><span data-stu-id="d42a9-102">ICLRHostProtectionManager Interface</span></span>
<span data-ttu-id="d42a9-103">Consente all'host di bloccare le classi, i metodi, le proprietà e i campi gestiti specifici dall'esecuzione in codice parzialmente attendibile.</span><span class="sxs-lookup"><span data-stu-id="d42a9-103">Enables the host to block specific managed classes, methods, properties, and fields from running in partially trusted code.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="d42a9-104">Metodi</span><span class="sxs-lookup"><span data-stu-id="d42a9-104">Methods</span></span>  
  
|<span data-ttu-id="d42a9-105">Metodo</span><span class="sxs-lookup"><span data-stu-id="d42a9-105">Method</span></span>|<span data-ttu-id="d42a9-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d42a9-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="d42a9-107">SetEagerSerializeGrantSets</span><span class="sxs-lookup"><span data-stu-id="d42a9-107">SetEagerSerializeGrantSets</span></span>](iclrhostprotectionmanager-seteagerserializegrantsets-method.md)|<span data-ttu-id="d42a9-108">Garantisce che alcune condizioni di Race rare che possono causare errori irreversibili di Common Language Runtime (CLR) non verranno mai verificate.</span><span class="sxs-lookup"><span data-stu-id="d42a9-108">Provides a guarantee that certain rare race conditions that can cause fatal common language runtime (CLR) errors will never arise.</span></span>|  
|[<span data-ttu-id="d42a9-109">Metodo SetProtectedCategories</span><span class="sxs-lookup"><span data-stu-id="d42a9-109">SetProtectedCategories Method</span></span>](iclrhostprotectionmanager-setprotectedcategories-method.md)|<span data-ttu-id="d42a9-110">Specifica le categorie di tipi e membri gestiti che devono essere bloccati dall'esecuzione in codice parzialmente attendibile.</span><span class="sxs-lookup"><span data-stu-id="d42a9-110">Specifies the categories of managed types and members that should be blocked from running in partially trusted code.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="d42a9-111">Requisiti</span><span class="sxs-lookup"><span data-stu-id="d42a9-111">Requirements</span></span>  
 <span data-ttu-id="d42a9-112">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="d42a9-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d42a9-113">**Intestazione:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="d42a9-113">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="d42a9-114">**Libreria:** Incluso come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="d42a9-114">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="d42a9-115">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d42a9-115">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d42a9-116">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d42a9-116">See also</span></span>

- [<span data-ttu-id="d42a9-117">Enumerazione EApiCategories</span><span class="sxs-lookup"><span data-stu-id="d42a9-117">EApiCategories Enumeration</span></span>](eapicategories-enumeration.md)
- [<span data-ttu-id="d42a9-118">Interfaccia ICLRControl</span><span class="sxs-lookup"><span data-stu-id="d42a9-118">ICLRControl Interface</span></span>](iclrcontrol-interface.md)

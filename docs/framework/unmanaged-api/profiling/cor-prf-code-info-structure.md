---
title: Struttura COR_PRF_CODE_INFO
ms.date: 03/30/2017
api_name:
- COR_PRF_CODE_INFO
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_CODE_INFO
helpviewer_keywords:
- COR_PRF_CODE_INFO structure [.NET Framework profiling]
ms.assetid: cf30e27c-1f7e-43a2-ba1e-01e4137301db
topic_type:
- apiref
ms.openlocfilehash: 9dbe0219f5932a9d212edaf5181b96335c47db0e
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501014"
---
# <a name="cor_prf_code_info-structure"></a><span data-ttu-id="33b44-102">Struttura COR_PRF_CODE_INFO</span><span class="sxs-lookup"><span data-stu-id="33b44-102">COR_PRF_CODE_INFO Structure</span></span>
<span data-ttu-id="33b44-103">Rappresenta un blocco contiguo di codice nativo archiviato in memoria.</span><span class="sxs-lookup"><span data-stu-id="33b44-103">Represents one contiguous block of native code stored in memory.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="33b44-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="33b44-104">Syntax</span></span>  
  
```cpp  
typedef struct _COR_PRF_CODE_INFO {  
    UINT_PTR startAddress;  
    SIZE_T size;  
} COR_PRF_CODE_INFO;  
```  
  
## <a name="members"></a><span data-ttu-id="33b44-105">Membri</span><span class="sxs-lookup"><span data-stu-id="33b44-105">Members</span></span>  
  
|<span data-ttu-id="33b44-106">Membro</span><span class="sxs-lookup"><span data-stu-id="33b44-106">Member</span></span>|<span data-ttu-id="33b44-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="33b44-107">Description</span></span>|  
|------------|-----------------|  
|`startAddress`|<span data-ttu-id="33b44-108">Indirizzo iniziale del blocco di codice contiguo.</span><span class="sxs-lookup"><span data-stu-id="33b44-108">The starting address of the contiguous block of code.</span></span>|  
|`size`|<span data-ttu-id="33b44-109">Dimensioni del blocco.</span><span class="sxs-lookup"><span data-stu-id="33b44-109">The size of the block.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="33b44-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="33b44-110">Requirements</span></span>  
 <span data-ttu-id="33b44-111">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="33b44-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="33b44-112">**Intestazione:** CorProf. idl</span><span class="sxs-lookup"><span data-stu-id="33b44-112">**Header:** CorProf.idl</span></span>  
  
 <span data-ttu-id="33b44-113">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="33b44-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="33b44-114">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="33b44-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="33b44-115">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="33b44-115">See also</span></span>

- [<span data-ttu-id="33b44-116">Strutture di profilatura</span><span class="sxs-lookup"><span data-stu-id="33b44-116">Profiling Structures</span></span>](profiling-structures.md)

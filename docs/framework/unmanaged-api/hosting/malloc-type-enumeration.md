---
title: Enumerazione MALLOC_TYPE
ms.date: 03/30/2017
api_name:
- MALLOC_TYPE
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- MALLOC_TYPE
helpviewer_keywords:
- MALLOC_TYPE Enumeration
ms.assetid: c02476f9-23a2-4af7-9282-aa9c42c7429b
topic_type:
- apiref
ms.openlocfilehash: 630fe4e79b369bfdefc19be72780f1893090895e
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008456"
---
# <a name="malloc_type-enumeration"></a><span data-ttu-id="28162-102">Enumerazione MALLOC_TYPE</span><span class="sxs-lookup"><span data-stu-id="28162-102">MALLOC_TYPE Enumeration</span></span>
<span data-ttu-id="28162-103">Contiene valori che specificano le caratteristiche della memoria da allocare.</span><span class="sxs-lookup"><span data-stu-id="28162-103">Contains values that specify the characteristics of the memory that is being allocated.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="28162-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="28162-104">Syntax</span></span>  
  
```cpp  
typedef enum {  
    MALLOC_THREADSAFE = 0x1,  
    MALLOC_EXECUTABLE = 0x2,  
} MALLOC_TYPE;  
```  
  
## <a name="members"></a><span data-ttu-id="28162-105">Membri</span><span class="sxs-lookup"><span data-stu-id="28162-105">Members</span></span>  
  
|<span data-ttu-id="28162-106">Membro</span><span class="sxs-lookup"><span data-stu-id="28162-106">Member</span></span>|<span data-ttu-id="28162-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="28162-107">Description</span></span>|  
|------------|-----------------|  
|`MALLOC_EXECUTABLE`|<span data-ttu-id="28162-108">La memoria allocata può contenere un file eseguibile.</span><span class="sxs-lookup"><span data-stu-id="28162-108">The allocated memory can contain an executable file.</span></span>|  
|`MALLOC_THREADSAFE`|<span data-ttu-id="28162-109">La memoria allocata è thread-safe.</span><span class="sxs-lookup"><span data-stu-id="28162-109">The allocated memory is thread-safe.</span></span> <span data-ttu-id="28162-110">Ovvero, la memoria può essere accessibile da più thread senza sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="28162-110">That is, the memory can be accessed by multiple threads without any synchronization.</span></span><br /><br /> <span data-ttu-id="28162-111">Se questo flag non è impostato, le chiamate all'oggetto devono essere serializzate.</span><span class="sxs-lookup"><span data-stu-id="28162-111">If this flag is not set, calls on the object must be serialized.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="28162-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="28162-112">Requirements</span></span>  
 <span data-ttu-id="28162-113">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="28162-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="28162-114">**Intestazione:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="28162-114">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="28162-115">**Libreria:** MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="28162-115">**Library:** MSCorEE.dll</span></span>  
  
 <span data-ttu-id="28162-116">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="28162-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="28162-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="28162-117">See also</span></span>

- [<span data-ttu-id="28162-118">Enumerazioni di hosting</span><span class="sxs-lookup"><span data-stu-id="28162-118">Hosting Enumerations</span></span>](hosting-enumerations.md)

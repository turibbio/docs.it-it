---
title: Enumerazione CorRegFlags
ms.date: 03/30/2017
api_name:
- CorRegFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorRegFlags
helpviewer_keywords:
- CorRegFlags enumeration [.NET Framework metadata]
ms.assetid: 8d3080ee-39fe-4c57-8950-51323632d045
topic_type:
- apiref
ms.openlocfilehash: d8d7a43848929e49a8cb48fb957f37213ac78f2e
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007351"
---
# <a name="corregflags-enumeration"></a><span data-ttu-id="db6c0-102">Enumerazione CorRegFlags</span><span class="sxs-lookup"><span data-stu-id="db6c0-102">CorRegFlags Enumeration</span></span>
<span data-ttu-id="db6c0-103">Fornisce valori di flag usati per la registrazione durante l'installazione di un modulo o un'immagine composita.</span><span class="sxs-lookup"><span data-stu-id="db6c0-103">Provides flag values used for registration when installing a module or composite image.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="db6c0-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="db6c0-104">Syntax</span></span>  
  
```cpp  
typedef enum
{  
    regNoCopy  = 0x00000001,  
    regConfig  = 0x00000002,  
    regHasRefs = 0x00000004  
} CorRegFlags;  
```  
  
## <a name="members"></a><span data-ttu-id="db6c0-105">Membri</span><span class="sxs-lookup"><span data-stu-id="db6c0-105">Members</span></span>  
  
|<span data-ttu-id="db6c0-106">Membro</span><span class="sxs-lookup"><span data-stu-id="db6c0-106">Member</span></span>|<span data-ttu-id="db6c0-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="db6c0-107">Description</span></span>|  
|------------|-----------------|  
|`regNoCopy`|<span data-ttu-id="db6c0-108">Specifica che i file non devono essere copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="db6c0-108">Specifies that files should not be copied into the destination.</span></span>|  
|`regConfig`|<span data-ttu-id="db6c0-109">Specifica che il modulo o composito è una configurazione.</span><span class="sxs-lookup"><span data-stu-id="db6c0-109">Specifies that the module or composite is a configuration.</span></span>|  
|`regHasRefs`|<span data-ttu-id="db6c0-110">Specifica che il modulo o composito contiene riferimenti a classi.</span><span class="sxs-lookup"><span data-stu-id="db6c0-110">Specifies that the module or composite has class references.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="db6c0-111">Requisiti</span><span class="sxs-lookup"><span data-stu-id="db6c0-111">Requirements</span></span>  
 <span data-ttu-id="db6c0-112">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="db6c0-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="db6c0-113">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="db6c0-113">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="db6c0-114">**Libreria:** Incluso come risorsa in MsCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="db6c0-114">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="db6c0-115">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="db6c0-115">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="db6c0-116">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="db6c0-116">See also</span></span>

- [<span data-ttu-id="db6c0-117">Enumerazioni dei metadati</span><span class="sxs-lookup"><span data-stu-id="db6c0-117">Metadata Enumerations</span></span>](metadata-enumerations.md)

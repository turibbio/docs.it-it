---
title: Enumerazione AssemblyRefFlags
ms.date: 03/30/2017
api_name:
- AssemblyRefFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- AssemblyRefFlags
helpviewer_keywords:
- AssemblyRefFlags enumeration [.NET Framework metadata]
ms.assetid: decd4f46-f3b2-466f-9501-e74f2b86b846
topic_type:
- apiref
ms.openlocfilehash: 1307f555c9d8b6d28febcf25db89ae856c143d71
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009405"
---
# <a name="assemblyrefflags-enumeration"></a><span data-ttu-id="23df4-102">Enumerazione AssemblyRefFlags</span><span class="sxs-lookup"><span data-stu-id="23df4-102">AssemblyRefFlags Enumeration</span></span>
<span data-ttu-id="23df4-103">Contiene valori che descrivono le funzionalità di un riferimento a un assembly.</span><span class="sxs-lookup"><span data-stu-id="23df4-103">Contains values that describe features of an assembly reference.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="23df4-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="23df4-104">Syntax</span></span>  
  
```cpp  
typedef enum {  
    arfFullOriginator = 0x0001  
} AssemblyRefFlags;  
```  
  
## <a name="members"></a><span data-ttu-id="23df4-105">Membri</span><span class="sxs-lookup"><span data-stu-id="23df4-105">Members</span></span>  
  
|<span data-ttu-id="23df4-106">Membro</span><span class="sxs-lookup"><span data-stu-id="23df4-106">Member</span></span>|<span data-ttu-id="23df4-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="23df4-107">Description</span></span>|  
|------------|-----------------|  
|`arfFullOriginator`|<span data-ttu-id="23df4-108">Specifica che il riferimento all'assembly contiene informazioni complete e senza hash relative al server di pubblicazione dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="23df4-108">Specifies that the assembly reference contains full, unhashed information about the publisher of the assembly.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="23df4-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="23df4-109">Requirements</span></span>  
 <span data-ttu-id="23df4-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="23df4-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="23df4-111">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="23df4-111">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="23df4-112">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="23df4-112">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="23df4-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="23df4-113">See also</span></span>

- [<span data-ttu-id="23df4-114">Enumerazioni dei metadati</span><span class="sxs-lookup"><span data-stu-id="23df4-114">Metadata Enumerations</span></span>](metadata-enumerations.md)
- [<span data-ttu-id="23df4-115">Interfaccia IMetaDataAssemblyEmit</span><span class="sxs-lookup"><span data-stu-id="23df4-115">IMetaDataAssemblyEmit Interface</span></span>](imetadataassemblyemit-interface.md)
- [<span data-ttu-id="23df4-116">Metodo DefineAssemblyRef</span><span class="sxs-lookup"><span data-stu-id="23df4-116">DefineAssemblyRef Method</span></span>](imetadataassemblyemit-defineassemblyref-method.md)

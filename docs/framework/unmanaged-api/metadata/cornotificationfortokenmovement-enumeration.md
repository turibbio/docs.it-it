---
title: Enumerazione CorNotificationForTokenMovement
ms.date: 03/30/2017
api_name:
- CorNotificationForTokenMovement
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorNotificationForTokenMovement
helpviewer_keywords:
- CorNotificationForTokenMovement enumeration [.NET Framework metadata]
ms.assetid: 1edd1670-976a-4fc8-bef7-7c41e60ad989
topic_type:
- apiref
ms.openlocfilehash: e8065a5492884a4b7f5d662737e4beddc6fca5b3
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007598"
---
# <a name="cornotificationfortokenmovement-enumeration"></a><span data-ttu-id="0c7eb-102">Enumerazione CorNotificationForTokenMovement</span><span class="sxs-lookup"><span data-stu-id="0c7eb-102">CorNotificationForTokenMovement Enumeration</span></span>
<span data-ttu-id="0c7eb-103">Specifica le notifiche che verranno inviate al client dell'API dei metadati quando si verifica un mapping del token.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-103">Specifies the notifications that will be sent to the metadata API client when a token remap occurs.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0c7eb-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="0c7eb-104">Syntax</span></span>  
  
```cpp  
typedef enum CorNotificationForTokenMovement {  
  
    MDNotifyDefault             = 0x0000000f,  
    MDNotifyAll                 = 0xffffffff,  
    MDNotifyNone                = 0x00000000,  
    MDNotifyMethodDef           = 0x00000001,  
    MDNotifyMemberRef           = 0x00000002,  
    MDNotifyFieldDef            = 0x00000004,  
    MDNotifyTypeRef             = 0x00000008,  
  
    MDNotifyTypeDef             = 0x00000010,  
    MDNotifyParamDef            = 0x00000020,  
    MDNotifyInterfaceImpl       = 0x00000040,  
    MDNotifyProperty            = 0x00000080,  
    MDNotifyEvent               = 0x00000100,  
    MDNotifySignature           = 0x00000200,  
    MDNotifyTypeSpec            = 0x00000400,  
    MDNotifyCustomAttribute     = 0x00000800,  
    MDNotifySecurityValue       = 0x00001000,  
    MDNotifyPermission          = 0x00002000,  
    MDNotifyModuleRef           = 0x00004000,  
  
    MDNotifyNameSpace           = 0x00008000,  
  
    MDNotifyAssemblyRef         = 0x01000000,  
    MDNotifyFile                = 0x02000000,  
    MDNotifyExportedType        = 0x04000000,  
    MDNotifyResource            = 0x08000000  
  
} CorNotificationForTokenMovement;  
```  
  
## <a name="members"></a><span data-ttu-id="0c7eb-105">Membri</span><span class="sxs-lookup"><span data-stu-id="0c7eb-105">Members</span></span>  
  
|<span data-ttu-id="0c7eb-106">Membro</span><span class="sxs-lookup"><span data-stu-id="0c7eb-106">Member</span></span>|<span data-ttu-id="0c7eb-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0c7eb-107">Description</span></span>|  
|------------|-----------------|  
|`MDNotifyDefault`|<span data-ttu-id="0c7eb-108">Notifica quando `mdTypeRef` si `mdMethodDef` spostano i token,, `mdMemberRef` o `mdFieldDef` .</span><span class="sxs-lookup"><span data-stu-id="0c7eb-108">Notify when `mdTypeRef`, `mdMethodDef`, `mdMemberRef`, or `mdFieldDef` tokens move.</span></span>|  
|`MDNotifyAll`|<span data-ttu-id="0c7eb-109">Notifica quando un token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-109">Notify when any token moves.</span></span>|  
|`MDNotifyNone`|<span data-ttu-id="0c7eb-110">Non notificare quando i token vengono spostati.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-110">Do not notify when tokens move.</span></span>|  
|`MDNotifyMethodDef`|<span data-ttu-id="0c7eb-111">Notifica quando un `mdMethodDef` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-111">Notify when an `mdMethodDef` token moves.</span></span>|  
|`MDNotifyMemberRef`|<span data-ttu-id="0c7eb-112">Notifica quando un `mdMemberRef` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-112">Notify when an `mdMemberRef` token moves.</span></span>|  
|`MDNotifyFieldDef`|<span data-ttu-id="0c7eb-113">Notifica quando un `mdFieldDef` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-113">Notify when an `mdFieldDef` token moves.</span></span>|  
|`MDNotifyTypeRef`|<span data-ttu-id="0c7eb-114">Notifica quando un `mdTypeRef` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-114">Notify when an `mdTypeRef` token moves.</span></span>|  
|`MDNotifyTypeDef`|<span data-ttu-id="0c7eb-115">Notifica quando un `mdTypeDef` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-115">Notify when an `mdTypeDef` token moves.</span></span>|  
|`MDNotifyParamDef`|<span data-ttu-id="0c7eb-116">Notifica quando un `mdParamDef` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-116">Notify when an `mdParamDef` token moves.</span></span>|  
|`MDNotifyInterfaceImpl`|<span data-ttu-id="0c7eb-117">Notifica quando un `mdInterfaceImpl` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-117">Notify when an `mdInterfaceImpl` token moves.</span></span>|  
|`MDNotifyProperty`|<span data-ttu-id="0c7eb-118">Notifica quando un `mdProperty` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-118">Notify when an `mdProperty` token moves.</span></span>|  
|`MDNotifyEvent`|<span data-ttu-id="0c7eb-119">Notifica quando un `mdEvent` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-119">Notify when an `mdEvent` token moves.</span></span>|  
|`MDNotifySignature`|<span data-ttu-id="0c7eb-120">Notifica quando un `mdSignature` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-120">Notify when an `mdSignature` token moves.</span></span>|  
|`MDNotifyTypeSpec`|<span data-ttu-id="0c7eb-121">Notifica quando un `mdTypeSpec` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-121">Notify when an `mdTypeSpec` token moves.</span></span>|  
|`MDNotifyCustomAttribute`|<span data-ttu-id="0c7eb-122">Notifica quando un `mdCustomAttribute` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-122">Notify when an `mdCustomAttribute` token moves.</span></span>|  
|`MDNotifySecurityValue`|<span data-ttu-id="0c7eb-123">Notifica quando un `mdSecurityValue` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-123">Notify when an `mdSecurityValue` token moves.</span></span>|  
|`MDNotifyPermission`|<span data-ttu-id="0c7eb-124">Notifica quando un `mdPermission` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-124">Notify when an `mdPermission` token moves.</span></span>|  
|`MDNotifyModuleRef`|<span data-ttu-id="0c7eb-125">Notifica quando un `mdModuleRef` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-125">Notify when an `mdModuleRef` token moves.</span></span>|  
|`MDNotifyNameSpace`|<span data-ttu-id="0c7eb-126">Notifica quando un `mdNameSpace` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-126">Notify when an `mdNameSpace` token moves.</span></span>|  
|`MDNotifyAssemblyRef`|<span data-ttu-id="0c7eb-127">Notifica quando un `mdAssemblyRef` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-127">Notify when an `mdAssemblyRef` token moves.</span></span>|  
|`MDNotifyFile`|<span data-ttu-id="0c7eb-128">Notifica quando un `mdFile` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-128">Notify when an `mdFile` token moves.</span></span>|  
|`MDNotifyExportedType`|<span data-ttu-id="0c7eb-129">Notifica quando un `mdExportedType` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-129">Notify when an `mdExportedType` token moves.</span></span>|  
|`MDNotifyResource`|<span data-ttu-id="0c7eb-130">Notifica quando un `mdManifestResource` token viene spostato.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-130">Notify when an `mdManifestResource` token moves.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="0c7eb-131">Commenti</span><span class="sxs-lookup"><span data-stu-id="0c7eb-131">Remarks</span></span>  
 <span data-ttu-id="0c7eb-132">È possibile che venga nuovamente eseguito il mapping di un token (ovvero lo spostamento) durante un'operazione di merge dei metadati.</span><span class="sxs-lookup"><span data-stu-id="0c7eb-132">A token may be re-mapped (that is, moved) during a metadata merge.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="0c7eb-133">Requisiti</span><span class="sxs-lookup"><span data-stu-id="0c7eb-133">Requirements</span></span>  
 <span data-ttu-id="0c7eb-134">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="0c7eb-134">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="0c7eb-135">**Intestazione:** CorHdr. h</span><span class="sxs-lookup"><span data-stu-id="0c7eb-135">**Header:** CorHdr.h</span></span>  
  
 <span data-ttu-id="0c7eb-136">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="0c7eb-136">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0c7eb-137">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0c7eb-137">See also</span></span>

- [<span data-ttu-id="0c7eb-138">Enumerazioni dei metadati</span><span class="sxs-lookup"><span data-stu-id="0c7eb-138">Metadata Enumerations</span></span>](metadata-enumerations.md)

---
title: Metodo IManagedObject::GetSerializedBuffer
ms.date: 03/30/2017
api_name:
- IManagedObject.GetSerializedBuffer
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- GetSerializedBuffer
helpviewer_keywords:
- IManagedObject::GetSerializedBuffer method [.NET Framework hosting]
- GetSerializedBuffer method [.NET Framework hosting]
ms.assetid: c17105bb-b49f-434e-8f9b-77f8c85b9220
topic_type:
- apiref
ms.openlocfilehash: c68ec0b41bb38afc7cefaf47df718fffcf42d250
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842429"
---
# <a name="imanagedobjectgetserializedbuffer-method"></a><span data-ttu-id="0e434-102">Metodo IManagedObject::GetSerializedBuffer</span><span class="sxs-lookup"><span data-stu-id="0e434-102">IManagedObject::GetSerializedBuffer Method</span></span>
<span data-ttu-id="0e434-103">Ottiene la rappresentazione di stringa di questo oggetto gestito.</span><span class="sxs-lookup"><span data-stu-id="0e434-103">Gets the string representation of this managed object.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0e434-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="0e434-104">Syntax</span></span>  
  
```cpp  
HRESULT GetSerializedBuffer (  
    [out] BSTR *pBSTR  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="0e434-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="0e434-105">Parameters</span></span>  
 `pBSTR`  
 <span data-ttu-id="0e434-106">out Puntatore a una stringa che rappresenta l'oggetto serializzato.</span><span class="sxs-lookup"><span data-stu-id="0e434-106">[out] A pointer to a string that is the serialized object.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="0e434-107">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="0e434-107">Remarks</span></span>  
 <span data-ttu-id="0e434-108">Il `GetSerializedBuffer` metodo serializza l'oggetto in modo che possa essere sottoposto a marshalling nel client.</span><span class="sxs-lookup"><span data-stu-id="0e434-108">The `GetSerializedBuffer` method serializes the object so it can be marshaled to the client.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="0e434-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="0e434-109">Requirements</span></span>  
 <span data-ttu-id="0e434-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="0e434-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="0e434-111">**Intestazione:** MSCorEE. h</span><span class="sxs-lookup"><span data-stu-id="0e434-111">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="0e434-112">**Libreria:** Incluso come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="0e434-112">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="0e434-113">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="0e434-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0e434-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0e434-114">See also</span></span>

- [<span data-ttu-id="0e434-115">Interfaccia IManagedObject</span><span class="sxs-lookup"><span data-stu-id="0e434-115">IManagedObject Interface</span></span>](imanagedobject-interface.md)

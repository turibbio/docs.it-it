---
title: Metodo IMetaDataEmit::SetMethodImplFlags
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetMethodImplFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetMethodImplFlags
helpviewer_keywords:
- IMetaDataEmit::SetMethodImplFlags method [.NET Framework metadata]
- SetMethodImpFlags method [.NET Framework metadata]
ms.assetid: 4bc82d9b-9544-4be3-ba51-a2d4d806158a
topic_type:
- apiref
ms.openlocfilehash: a02456393680169ce33369ee5914f6c5216081c6
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009223"
---
# <a name="imetadataemitsetmethodimplflags-method"></a><span data-ttu-id="afa05-102">Metodo IMetaDataEmit::SetMethodImplFlags</span><span class="sxs-lookup"><span data-stu-id="afa05-102">IMetaDataEmit::SetMethodImplFlags Method</span></span>
<span data-ttu-id="afa05-103">Imposta o aggiorna la firma dei metadati dell'implementazione del metodo ereditato a cui fa riferimento il token specificato.</span><span class="sxs-lookup"><span data-stu-id="afa05-103">Sets or updates the metadata signature of the inherited method implementation that is referenced by the specified token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="afa05-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="afa05-104">Syntax</span></span>  
  
```cpp  
HRESULT SetMethodImplFlags (
    [in]  mdMethodDef   md,
    [in]  DWORD         dwImplFlags
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="afa05-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="afa05-105">Parameters</span></span>  
 `md`  
 <span data-ttu-id="afa05-106">in Token per il metodo da modificare.</span><span class="sxs-lookup"><span data-stu-id="afa05-106">[in] The token for the method to be changed.</span></span>  
  
 `dwImplFlags`  
 <span data-ttu-id="afa05-107">in Combinazione dei valori dell'enumerazione [CorMethodImpl](cormethodimpl-enumeration.md) che specifica le funzionalità di implementazione del metodo.</span><span class="sxs-lookup"><span data-stu-id="afa05-107">[in] A combination of the values of the [CorMethodImpl](cormethodimpl-enumeration.md) enumeration that specifies the method implementation features.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="afa05-108">Requisiti</span><span class="sxs-lookup"><span data-stu-id="afa05-108">Requirements</span></span>  
 <span data-ttu-id="afa05-109">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="afa05-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="afa05-110">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="afa05-110">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="afa05-111">**Libreria:** Usato come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="afa05-111">**Library:** Used as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="afa05-112">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="afa05-112">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="afa05-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="afa05-113">See also</span></span>

- [<span data-ttu-id="afa05-114">Interfaccia IMetaDataEmit</span><span class="sxs-lookup"><span data-stu-id="afa05-114">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)
- [<span data-ttu-id="afa05-115">Interfaccia IMetaDataEmit2</span><span class="sxs-lookup"><span data-stu-id="afa05-115">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)

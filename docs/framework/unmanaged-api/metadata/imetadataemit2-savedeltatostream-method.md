---
title: Metodo IMetaDataEmit2::SaveDeltaToStream
ms.date: 03/30/2017
api_name:
- IMetaDataEmit2.SaveDeltaToStream
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit2::SaveDeltaToStream
helpviewer_keywords:
- IMetaDataEmit2::SaveDeltaToStream method [.NET Framework metadata]
- SaveDeltaToStream method [.NET Framework metadata]
ms.assetid: ecd786e8-f9a4-4190-a6ef-af18e8c6d654
topic_type:
- apiref
ms.openlocfilehash: a8f46871dde4c664a502c261fc882f3badf0f362
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84492754"
---
# <a name="imetadataemit2savedeltatostream-method"></a><span data-ttu-id="b96a7-102">Metodo IMetaDataEmit2::SaveDeltaToStream</span><span class="sxs-lookup"><span data-stu-id="b96a7-102">IMetaDataEmit2::SaveDeltaToStream Method</span></span>
<span data-ttu-id="b96a7-103">Salva le modifiche dalla sessione di modifica e continuazione corrente nel flusso specificato.</span><span class="sxs-lookup"><span data-stu-id="b96a7-103">Saves changes from the current edit-and-continue session to the specified stream.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b96a7-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="b96a7-104">Syntax</span></span>  
  
```cpp  
HRESULT SaveDeltaToStream (  
    [in] IStream     *pIStream,
    [in] DWORD       dwSaveFlags  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="b96a7-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="b96a7-105">Parameters</span></span>  
 `pIStream`  
 <span data-ttu-id="b96a7-106">in Puntatore di interfaccia al flusso scrivibile nel quale salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="b96a7-106">[in] An interface pointer to the writable stream to which to save changes.</span></span>  
  
 `dwSaveFlags`  
 <span data-ttu-id="b96a7-107">[in] Riservato.</span><span class="sxs-lookup"><span data-stu-id="b96a7-107">[in] Reserved.</span></span> <span data-ttu-id="b96a7-108">Il valore deve essere zero.</span><span class="sxs-lookup"><span data-stu-id="b96a7-108">This value must be zero.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b96a7-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="b96a7-109">Requirements</span></span>  
 <span data-ttu-id="b96a7-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b96a7-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b96a7-111">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="b96a7-111">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="b96a7-112">**Libreria:** Usato come risorsa in MsCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="b96a7-112">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="b96a7-113">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b96a7-113">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b96a7-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b96a7-114">See also</span></span>

- [<span data-ttu-id="b96a7-115">Interfaccia IMetaDataEmit2</span><span class="sxs-lookup"><span data-stu-id="b96a7-115">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)
- [<span data-ttu-id="b96a7-116">Interfaccia IMetaDataEmit</span><span class="sxs-lookup"><span data-stu-id="b96a7-116">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)

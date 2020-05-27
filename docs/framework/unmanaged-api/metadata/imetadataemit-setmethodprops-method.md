---
title: Metodo IMetaDataEmit::SetMethodProps
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetMethodProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetMethodProps
helpviewer_keywords:
- SetMethodProps method [.NET Framework metadata]
- IMetaDataEmit::SetMethodProps method [.NET Framework metadata]
ms.assetid: e0c6ac12-22ea-43f5-b799-8cda0faf3336
topic_type:
- apiref
ms.openlocfilehash: 57f6de1f7edf7c75a3f96cb2bf9fb98fdbd6f65e
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007858"
---
# <a name="imetadataemitsetmethodprops-method"></a><span data-ttu-id="c69a0-102">Metodo IMetaDataEmit::SetMethodProps</span><span class="sxs-lookup"><span data-stu-id="c69a0-102">IMetaDataEmit::SetMethodProps Method</span></span>
<span data-ttu-id="c69a0-103">Imposta o aggiorna la funzionalità, archiviata in corrispondenza dell'indirizzo virtuale relativo specificato, di un metodo definito da una chiamata precedente a [IMetaDataEmit::D efinemethod](imetadataemit-definemethod-method.md).</span><span class="sxs-lookup"><span data-stu-id="c69a0-103">Sets or updates the feature, stored at the specified relative virtual address, of a method defined by a prior call to [IMetaDataEmit::DefineMethod](imetadataemit-definemethod-method.md).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c69a0-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="c69a0-104">Syntax</span></span>  
  
```cpp  
HRESULT SetMethodProps (
    [in]  mdMethodDef md,
    [in]  DWORD       dwMethodFlags,  
    [in]  ULONG       ulCodeRVA,
    [in]  DWORD       dwImplFlags
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="c69a0-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="c69a0-105">Parameters</span></span>  
 `md`  
 <span data-ttu-id="c69a0-106">in Token per il metodo da modificare.</span><span class="sxs-lookup"><span data-stu-id="c69a0-106">[in] The token for the method to be changed.</span></span>  
  
 `dwMethodFlags`  
 <span data-ttu-id="c69a0-107">in Attributi del membro.</span><span class="sxs-lookup"><span data-stu-id="c69a0-107">[in] The member attributes.</span></span>  
  
 `ulCodeRVA`  
 <span data-ttu-id="c69a0-108">in Indirizzo del codice.</span><span class="sxs-lookup"><span data-stu-id="c69a0-108">[in] The address of the code.</span></span>  
  
 `dwImplFlags`  
 <span data-ttu-id="c69a0-109">in Flag di implementazione per il metodo.</span><span class="sxs-lookup"><span data-stu-id="c69a0-109">[in] The implementation flags for the method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c69a0-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="c69a0-110">Requirements</span></span>  
 <span data-ttu-id="c69a0-111">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="c69a0-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c69a0-112">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="c69a0-112">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="c69a0-113">**Libreria:** Usato come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="c69a0-113">**Library:** Used as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="c69a0-114">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c69a0-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c69a0-115">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c69a0-115">See also</span></span>

- [<span data-ttu-id="c69a0-116">Interfaccia IMetaDataEmit</span><span class="sxs-lookup"><span data-stu-id="c69a0-116">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)
- [<span data-ttu-id="c69a0-117">Interfaccia IMetaDataEmit2</span><span class="sxs-lookup"><span data-stu-id="c69a0-117">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)

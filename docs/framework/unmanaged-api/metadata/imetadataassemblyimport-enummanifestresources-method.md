---
title: Metodo IMetaDataAssemblyImport::EnumManifestResources
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.EnumManifestResources
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::EnumManifestResources
helpviewer_keywords:
- IMetaDataAssemblyImport::EnumManifestResources method [.NET Framework metadata]
- EnumManifestResources method [.NET Framework metadata]
ms.assetid: 9543b111-5705-40c9-935c-a3ffc7a581aa
topic_type:
- apiref
ms.openlocfilehash: 560a6adf85fab7f421b86cba52224d5b1bfe1089
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84006259"
---
# <a name="imetadataassemblyimportenummanifestresources-method"></a><span data-ttu-id="21bfa-102">Metodo IMetaDataAssemblyImport::EnumManifestResources</span><span class="sxs-lookup"><span data-stu-id="21bfa-102">IMetaDataAssemblyImport::EnumManifestResources Method</span></span>
<span data-ttu-id="21bfa-103">Ottiene un puntatore a un enumeratore per le risorse a cui si fa riferimento nel manifesto dell'assembly corrente.</span><span class="sxs-lookup"><span data-stu-id="21bfa-103">Gets a pointer to an enumerator for the resources referenced in the current assembly manifest.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="21bfa-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="21bfa-104">Syntax</span></span>  
  
```cpp  
HRESULT EnumManifestResources (  
    [in, out] HCORENUM         *phEnum,
    [out] mdManifestResource   rManifestResources[],
    [in]  ULONG                cMax,
    [out] ULONG                *pcTokens  
);
```  
  
## <a name="parameters"></a><span data-ttu-id="21bfa-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="21bfa-105">Parameters</span></span>  
 `phEnum`  
 <span data-ttu-id="21bfa-106">[in, out] Puntatore all'enumeratore.</span><span class="sxs-lookup"><span data-stu-id="21bfa-106">[in, out] A pointer to the enumerator.</span></span> <span data-ttu-id="21bfa-107">Deve essere un valore null quando il `EnumManifestResources` metodo viene chiamato per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="21bfa-107">This must be a null value when the `EnumManifestResources` method is called for the first time.</span></span>  
  
 `rManifestResources`  
 <span data-ttu-id="21bfa-108">out Matrice utilizzata per archiviare i `mdManifestResource` token dei metadati.</span><span class="sxs-lookup"><span data-stu-id="21bfa-108">[out] The array used to store the `mdManifestResource` metadata tokens.</span></span>  
  
 `cMax`  
 <span data-ttu-id="21bfa-109">in Numero massimo di `mdManifestResource` token che possono essere inseriti in `rManifestResources` .</span><span class="sxs-lookup"><span data-stu-id="21bfa-109">[in] The maximum number of `mdManifestResource` tokens that can be placed in `rManifestResources`.</span></span>  
  
 `pcTokens`  
 <span data-ttu-id="21bfa-110">out Numero di `mdManifestResource` token effettivamente inseriti in `rManifestResources` .</span><span class="sxs-lookup"><span data-stu-id="21bfa-110">[out] The number of `mdManifestResource` tokens actually placed in `rManifestResources`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="21bfa-111">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="21bfa-111">Return Value</span></span>  
  
|<span data-ttu-id="21bfa-112">HRESULT</span><span class="sxs-lookup"><span data-stu-id="21bfa-112">HRESULT</span></span>|<span data-ttu-id="21bfa-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="21bfa-113">Description</span></span>|  
|-------------|-----------------|  
|`S_OK`|<span data-ttu-id="21bfa-114">`EnumManifestResources`la restituzione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="21bfa-114">`EnumManifestResources` returned successfully.</span></span>|  
|`S_FALSE`|<span data-ttu-id="21bfa-115">Nessun token da enumerare.</span><span class="sxs-lookup"><span data-stu-id="21bfa-115">There are no tokens to enumerate.</span></span> <span data-ttu-id="21bfa-116">In questo caso, `pcTokens` è impostato su zero.</span><span class="sxs-lookup"><span data-stu-id="21bfa-116">In this case, `pcTokens` is set to zero.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="21bfa-117">Requisiti</span><span class="sxs-lookup"><span data-stu-id="21bfa-117">Requirements</span></span>  
 <span data-ttu-id="21bfa-118">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="21bfa-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="21bfa-119">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="21bfa-119">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="21bfa-120">**Libreria:** Usato come risorsa in MsCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="21bfa-120">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="21bfa-121">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="21bfa-121">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="21bfa-122">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="21bfa-122">See also</span></span>

- [<span data-ttu-id="21bfa-123">Interfaccia IMetaDataAssemblyImport</span><span class="sxs-lookup"><span data-stu-id="21bfa-123">IMetaDataAssemblyImport Interface</span></span>](imetadataassemblyimport-interface.md)

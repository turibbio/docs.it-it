---
title: Metodo IMetaDataEmit::DefineModuleRef
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineModuleRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineModuleRef
helpviewer_keywords:
- DefineModuleRef method [.NET Framework metadata]
- IMetaDataEmit::DefineModuleRef method [.NET Framework metadata]
ms.assetid: f2833594-d90b-4a71-9a53-34b12470c64a
topic_type:
- apiref
ms.openlocfilehash: efff491d92ac7910f43f76965ef98d1d0e4ba0aa
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84004426"
---
# <a name="imetadataemitdefinemoduleref-method"></a><span data-ttu-id="34c41-102">Metodo IMetaDataEmit::DefineModuleRef</span><span class="sxs-lookup"><span data-stu-id="34c41-102">IMetaDataEmit::DefineModuleRef Method</span></span>
<span data-ttu-id="34c41-103">Crea la firma dei metadati per un modulo con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="34c41-103">Creates the metadata signature for a module with the specified name.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="34c41-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="34c41-104">Syntax</span></span>  
  
```cpp  
HRESULT DefineModuleRef (
    [in]  LPCWSTR           szName,
    [out] mdModuleRef       *pmur
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="34c41-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="34c41-105">Parameters</span></span>  
 `szName`  
 <span data-ttu-id="34c41-106">in Nome dell'altro file di metadati, in genere una DLL.</span><span class="sxs-lookup"><span data-stu-id="34c41-106">[in] The name of the other metadata file, typically a DLL.</span></span> <span data-ttu-id="34c41-107">Questo è solo il nome del file.</span><span class="sxs-lookup"><span data-stu-id="34c41-107">This is the file name only.</span></span> <span data-ttu-id="34c41-108">Non usare un nome di percorso completo.</span><span class="sxs-lookup"><span data-stu-id="34c41-108">Do not use a full path name.</span></span>  
  
 `pmur`  
 <span data-ttu-id="34c41-109">out Token assegnato `mdModuleRef` .</span><span class="sxs-lookup"><span data-stu-id="34c41-109">[out] The assigned `mdModuleRef` token.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="34c41-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="34c41-110">Requirements</span></span>  
 <span data-ttu-id="34c41-111">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="34c41-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="34c41-112">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="34c41-112">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="34c41-113">**Libreria:** Usato come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="34c41-113">**Library:** Used as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="34c41-114">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="34c41-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="34c41-115">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="34c41-115">See also</span></span>

- [<span data-ttu-id="34c41-116">Interfaccia IMetaDataEmit</span><span class="sxs-lookup"><span data-stu-id="34c41-116">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)
- [<span data-ttu-id="34c41-117">Interfaccia IMetaDataEmit2</span><span class="sxs-lookup"><span data-stu-id="34c41-117">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)

---
title: Metodo IMetaDataImport::FindTypeRef
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindTypeRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindTypeRef
helpviewer_keywords:
- IMetaDataImport::FindTypeRef method [.NET Framework metadata]
- FindTypeRef method [.NET Framework metadata]
ms.assetid: 1b2bbf3f-943e-412e-b66c-e802431b055c
topic_type:
- apiref
ms.openlocfilehash: 545fe1e1d9e641d2225ad92c11453558dc4b97d1
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84491498"
---
# <a name="imetadataimportfindtyperef-method"></a><span data-ttu-id="42fc7-102">Metodo IMetaDataImport::FindTypeRef</span><span class="sxs-lookup"><span data-stu-id="42fc7-102">IMetaDataImport::FindTypeRef Method</span></span>
<span data-ttu-id="42fc7-103">Ottiene un puntatore al token TypeRef per il <xref:System.Type> riferimento che si trova nell'ambito specificato e con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="42fc7-103">Gets a pointer to the TypeRef token for the <xref:System.Type> reference that is in the specified scope and that has the specified name.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="42fc7-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="42fc7-104">Syntax</span></span>  
  
```cpp  
HRESULT FindTypeRef (  
   [in] mdToken        tkResolutionScope,  
   [in]  LPCWSTR       szName,  
   [out] mdTypeRef     *ptr  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="42fc7-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="42fc7-105">Parameters</span></span>  
 `tkResolutionScope`  
 <span data-ttu-id="42fc7-106">in Token ModuleRef, AssemblyRef o TypeRef che specifica rispettivamente il modulo, l'assembly o il tipo in cui è definito il riferimento al tipo.</span><span class="sxs-lookup"><span data-stu-id="42fc7-106">[in] A ModuleRef, AssemblyRef, or TypeRef token that specifies the module, assembly, or type, respectively, in which the type reference is defined.</span></span>  
  
 `szName`  
 <span data-ttu-id="42fc7-107">in Nome del riferimento al tipo di cui eseguire la ricerca.</span><span class="sxs-lookup"><span data-stu-id="42fc7-107">[in] The name of the type reference to search for.</span></span>  
  
 `ptr`  
 <span data-ttu-id="42fc7-108">out Puntatore al token TypeRef corrispondente.</span><span class="sxs-lookup"><span data-stu-id="42fc7-108">[out] A pointer to the matching TypeRef token.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="42fc7-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="42fc7-109">Requirements</span></span>  
 <span data-ttu-id="42fc7-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="42fc7-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="42fc7-111">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="42fc7-111">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="42fc7-112">**Libreria:** Incluso come risorsa in MsCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="42fc7-112">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="42fc7-113">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="42fc7-113">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="42fc7-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="42fc7-114">See also</span></span>

- [<span data-ttu-id="42fc7-115">Interfaccia IMetaDataImport</span><span class="sxs-lookup"><span data-stu-id="42fc7-115">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)
- [<span data-ttu-id="42fc7-116">Interfaccia IMetaDataImport2</span><span class="sxs-lookup"><span data-stu-id="42fc7-116">IMetaDataImport2 Interface</span></span>](imetadataimport2-interface.md)

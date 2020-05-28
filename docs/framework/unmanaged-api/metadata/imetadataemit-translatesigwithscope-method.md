---
title: Metodo IMetaDataEmit::TranslateSigWithScope
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.TranslateSigWithScope
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::TranslateSigWithScope
helpviewer_keywords:
- TranslateSigWithScope method [.NET Framework metadata]
- IMetaDataEmit::TranslateSigWithScope method [.NET Framework metadata]
ms.assetid: 47915d33-b7bf-409e-b484-4ee1df15de22
topic_type:
- apiref
ms.openlocfilehash: 7ef6dbc46806febc6fba89b39a8b894377225c23
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84003966"
---
# <a name="imetadataemittranslatesigwithscope-method"></a><span data-ttu-id="39d2f-102">Metodo IMetaDataEmit::TranslateSigWithScope</span><span class="sxs-lookup"><span data-stu-id="39d2f-102">IMetaDataEmit::TranslateSigWithScope Method</span></span>
<span data-ttu-id="39d2f-103">Importa un assembly nell'ambito corrente e ottiene una nuova firma dei metadati per l'ambito Unito.</span><span class="sxs-lookup"><span data-stu-id="39d2f-103">Imports an assembly into the current scope and gets a new metadata signature for the merged scope.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="39d2f-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="39d2f-104">Syntax</span></span>  
  
```cpp  
HRESULT TranslateSigWithScope (
    [in]  IMetaDataAssemblyImport   *pAssemImport,
    [in]  const void                *pbHashValue,
    [in]  ULONG                     cbHashValue,
    [in]  IMetaDataImport           *import,
    [in]  PCCOR_SIGNATURE           pbSigBlob,
    [in]  ULONG                     cbSigBlob,  
    [in]  IMetaDataAssemblyEmit     *pAssemEmit,
    [in]  IMetaDataEmit             *emit,
    [out] PCOR_SIGNATURE            pvTranslatedSig,
    [in]  ULONG                     cbTranslatedSigMax,
    [out] ULONG                     *pcbTranslatedSig
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="39d2f-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="39d2f-105">Parameters</span></span>  
 `pAssemImport`  
 <span data-ttu-id="39d2f-106">in Interfaccia per l'assembly di importazione (in cui è definita la firma).</span><span class="sxs-lookup"><span data-stu-id="39d2f-106">[in] The interface for import assembly (where the signature is defined).</span></span>  
  
 `pbHashValue`  
 <span data-ttu-id="39d2f-107">in Blob hash per l'assembly.</span><span class="sxs-lookup"><span data-stu-id="39d2f-107">[in] The hash blob for the assembly.</span></span>  
  
 `cbHashValue`  
 <span data-ttu-id="39d2f-108">in Numero di byte in `pbHashValue` .</span><span class="sxs-lookup"><span data-stu-id="39d2f-108">[in] The count of bytes in `pbHashValue`.</span></span>  
  
 `import`  
 <span data-ttu-id="39d2f-109">in Interfaccia per l'ambito dell'importazione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="39d2f-109">[in] The interface for import metadata scope.</span></span>  
  
 `pbSigBlob`  
 <span data-ttu-id="39d2f-110">in Firma da importare.</span><span class="sxs-lookup"><span data-stu-id="39d2f-110">[in] The signature to be imported.</span></span>  
  
 `cbSigBlob`  
 <span data-ttu-id="39d2f-111">in Dimensione, in byte, di `pbSigBlob` .</span><span class="sxs-lookup"><span data-stu-id="39d2f-111">[in] The size, in bytes, of `pbSigBlob`.</span></span>  
  
 `pAssemEmit`  
 <span data-ttu-id="39d2f-112">in Interfaccia per l'esportazione dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="39d2f-112">[in] The interface for export assembly.</span></span>  
  
 `emit`  
 <span data-ttu-id="39d2f-113">in Interfaccia per l'ambito di esportazione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="39d2f-113">[in] The interface for export metadata scope.</span></span>  
  
 `pvTranslatedSig`  
 <span data-ttu-id="39d2f-114">out Buffer in cui memorizzare il BLOB di firma tradotto.</span><span class="sxs-lookup"><span data-stu-id="39d2f-114">[out] The buffer to hold the translated signature blob.</span></span>  
  
 `cbTranslatedSigMax`  
 <span data-ttu-id="39d2f-115">in Capacità, in byte, di `pvTranslatedSig` .</span><span class="sxs-lookup"><span data-stu-id="39d2f-115">[in] The capacity, in bytes, of `pvTranslatedSig`.</span></span>  
  
 `pcbTranslatedSig`  
 <span data-ttu-id="39d2f-116">out Numero di byte effettivi nella firma tradotta.</span><span class="sxs-lookup"><span data-stu-id="39d2f-116">[out] The number of actual bytes in the translated signature.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="39d2f-117">Requisiti</span><span class="sxs-lookup"><span data-stu-id="39d2f-117">Requirements</span></span>  
 <span data-ttu-id="39d2f-118">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="39d2f-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="39d2f-119">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="39d2f-119">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="39d2f-120">**Libreria:** Usato come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="39d2f-120">**Library:** Used as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="39d2f-121">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="39d2f-121">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="39d2f-122">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="39d2f-122">See also</span></span>

- [<span data-ttu-id="39d2f-123">Interfaccia IMetaDataAssemblyEmit</span><span class="sxs-lookup"><span data-stu-id="39d2f-123">IMetaDataAssemblyEmit Interface</span></span>](imetadataassemblyemit-interface.md)
- [<span data-ttu-id="39d2f-124">Interfaccia IMetaDataAssemblyImport</span><span class="sxs-lookup"><span data-stu-id="39d2f-124">IMetaDataAssemblyImport Interface</span></span>](imetadataassemblyimport-interface.md)
- [<span data-ttu-id="39d2f-125">Interfaccia IMetaDataEmit</span><span class="sxs-lookup"><span data-stu-id="39d2f-125">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)
- [<span data-ttu-id="39d2f-126">Interfaccia IMetaDataEmit2</span><span class="sxs-lookup"><span data-stu-id="39d2f-126">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)
- [<span data-ttu-id="39d2f-127">Interfaccia IMetaDataImport</span><span class="sxs-lookup"><span data-stu-id="39d2f-127">IMetaDataImport Interface</span></span>](imetadataimport-interface.md)

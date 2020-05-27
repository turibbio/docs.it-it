---
title: Metodo ICeeGen::GetMethodBuffer
ms.date: 03/30/2017
api_name:
- ICeeGen.GetMethodBuffer
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICeeGen::GetMethodBuffer
helpviewer_keywords:
- ICeeGen::GetMethodBuffer method [.NET Framework metadata]
- GetMethodBuffer method [.NET Framework metadata]
ms.assetid: c7c5b39a-d4ac-41f1-9d1e-44163f563a49
topic_type:
- apiref
ms.openlocfilehash: 99eef11c294dbb17b30b2ef28e65999d4d60f817
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008322"
---
# <a name="iceegengetmethodbuffer-method"></a><span data-ttu-id="7b071-102">Metodo ICeeGen::GetMethodBuffer</span><span class="sxs-lookup"><span data-stu-id="7b071-102">ICeeGen::GetMethodBuffer Method</span></span>
<span data-ttu-id="7b071-103">Ottiene un buffer delle dimensioni appropriate per il metodo in corrispondenza dell'indirizzo virtuale relativo specificato.</span><span class="sxs-lookup"><span data-stu-id="7b071-103">Gets a buffer of the appropriate size for the method at the specified relative virtual address.</span></span>  
  
 <span data-ttu-id="7b071-104">Questo metodo è obsoleto e non deve essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="7b071-104">This method is obsolete and should not be used.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7b071-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="7b071-105">Syntax</span></span>  
  
```cpp  
HRESULT GetMethodBuffer (  
    [in]  ULONG       RVA,  
    [out] UCHAR       **lpBuffer  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="7b071-106">Parametri</span><span class="sxs-lookup"><span data-stu-id="7b071-106">Parameters</span></span>  
 `RVA`  
 <span data-ttu-id="7b071-107">in Indirizzo virtuale relativo del metodo per il quale restituire un buffer.</span><span class="sxs-lookup"><span data-stu-id="7b071-107">[in] The relative virtual address of the method for which to return a buffer.</span></span>  
  
 `lpBuffer`  
 <span data-ttu-id="7b071-108">out Puntatore al buffer restituito.</span><span class="sxs-lookup"><span data-stu-id="7b071-108">[out] A pointer to the returned buffer.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7b071-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="7b071-109">Requirements</span></span>  
 <span data-ttu-id="7b071-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7b071-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7b071-111">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="7b071-111">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="7b071-112">**Libreria:** Usato come risorsa in MsCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="7b071-112">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="7b071-113">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7b071-113">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7b071-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7b071-114">See also</span></span>

- [<span data-ttu-id="7b071-115">Interfaccia ICeeGen</span><span class="sxs-lookup"><span data-stu-id="7b071-115">ICeeGen Interface</span></span>](iceegen-interface.md)

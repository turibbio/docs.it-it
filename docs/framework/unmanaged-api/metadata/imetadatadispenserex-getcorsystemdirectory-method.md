---
title: Metodo IMetaDataDispenserEx::GetCORSystemDirectory
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.GetCORSystemDirectory
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::GetCORSystemDirectory
helpviewer_keywords:
- IMetaDataDispenserEx::GetCORSystemDirectory method [.NET Framework metadata]
- GetCORSystemDirectory method [.NET Framework metadata]
ms.assetid: d9e0f3b6-e106-4820-bada-5bfba34ce360
topic_type:
- apiref
ms.openlocfilehash: a76c17e663fdf6555ed878cca1b86b6a9395730e
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008794"
---
# <a name="imetadatadispenserexgetcorsystemdirectory-method"></a><span data-ttu-id="108a4-102">Metodo IMetaDataDispenserEx::GetCORSystemDirectory</span><span class="sxs-lookup"><span data-stu-id="108a4-102">IMetaDataDispenserEx::GetCORSystemDirectory Method</span></span>
<span data-ttu-id="108a4-103">Ottiene la directory che include la Common Language Runtime corrente (CLR).</span><span class="sxs-lookup"><span data-stu-id="108a4-103">Gets the directory that holds the current common language runtime (CLR).</span></span> <span data-ttu-id="108a4-104">Questo metodo è supportato solo per l'utilizzo da debugger out-of-process.</span><span class="sxs-lookup"><span data-stu-id="108a4-104">This method is supported only for use by out-of-process debuggers.</span></span> <span data-ttu-id="108a4-105">Se viene chiamato da un altro componente, restituirà E_NOTIMPL.</span><span class="sxs-lookup"><span data-stu-id="108a4-105">If called from another component, it will return E_NOTIMPL.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="108a4-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="108a4-106">Syntax</span></span>  
  
```cpp  
HRESULT GetCORSystemDirectory (  
    [out] LPWSTR      szBuffer,
    [in]  DWORD       cchBuffer,
    [out] DWORD*      pchBuffer  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="108a4-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="108a4-107">Parameters</span></span>  
 `szBuffer`  
 <span data-ttu-id="108a4-108">out Buffer per la ricezione del nome della directory.</span><span class="sxs-lookup"><span data-stu-id="108a4-108">[out] The buffer to receive the directory name.</span></span>  
  
 `cchBuffer`  
 <span data-ttu-id="108a4-109">in Dimensione, in byte, di `szBuffer` .</span><span class="sxs-lookup"><span data-stu-id="108a4-109">[in] The size, in bytes, of `szBuffer`.</span></span>  
  
 `pchBuffer`  
 <span data-ttu-id="108a4-110">out Numero di byte effettivamente restituiti in `szBuffer` .</span><span class="sxs-lookup"><span data-stu-id="108a4-110">[out] The number of bytes actually returned in `szBuffer`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="108a4-111">Requisiti</span><span class="sxs-lookup"><span data-stu-id="108a4-111">Requirements</span></span>  
 <span data-ttu-id="108a4-112">**Piattaforma:** Vedere [requisiti di sistema](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="108a4-112">**Platform:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="108a4-113">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="108a4-113">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="108a4-114">**Libreria:** Usato come risorsa in MsCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="108a4-114">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="108a4-115">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="108a4-115">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="108a4-116">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="108a4-116">See also</span></span>

- [<span data-ttu-id="108a4-117">Interfaccia IMetaDataDispenserEx</span><span class="sxs-lookup"><span data-stu-id="108a4-117">IMetaDataDispenserEx Interface</span></span>](imetadatadispenserex-interface.md)
- [<span data-ttu-id="108a4-118">Interfaccia IMetaDataDispenser</span><span class="sxs-lookup"><span data-stu-id="108a4-118">IMetaDataDispenser Interface</span></span>](imetadatadispenser-interface.md)

---
title: Metodo ICLRDataTarget::WriteVirtual
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.WriteVirtual
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::WriteVirtual
helpviewer_keywords:
- ICLRDataTarget::WriteVirtual method [.NET Framework debugging]
- WriteVirtual method [.NET Framework debugging]
ms.assetid: d627e8b7-a605-40ac-b9bb-da9a3f1b66d9
topic_type:
- apiref
ms.openlocfilehash: 6a7a7736837f7e6bbf1ad4982e78a75550abbeab
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860498"
---
# <a name="iclrdatatargetwritevirtual-method"></a><span data-ttu-id="413b0-102">Metodo ICLRDataTarget::WriteVirtual</span><span class="sxs-lookup"><span data-stu-id="413b0-102">ICLRDataTarget::WriteVirtual Method</span></span>
<span data-ttu-id="413b0-103">Scrive i dati dal buffer specificato nell'indirizzo di memoria virtuale specificato.</span><span class="sxs-lookup"><span data-stu-id="413b0-103">Writes data from the specified buffer to the specified virtual memory address.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="413b0-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="413b0-104">Syntax</span></span>  
  
```cpp  
HRESULT WriteVirtual (  
    [in] CLRDATA_ADDRESS    address,  
    [in, size_is(bytesRequested)]
        BYTE                *buffer,  
    [in] ULONG32            bytesRequested,  
    [out] ULONG32           *bytesWritten  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="413b0-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="413b0-105">Parameters</span></span>  
 `address`  
 <span data-ttu-id="413b0-106">in CLRDATA_ADDRESS che archivia l'indirizzo di memoria virtuale.</span><span class="sxs-lookup"><span data-stu-id="413b0-106">[in] A CLRDATA_ADDRESS that stores the virtual memory address.</span></span>  
  
 `buffer`  
 <span data-ttu-id="413b0-107">in Puntatore a un buffer che archivia i dati da scrivere.</span><span class="sxs-lookup"><span data-stu-id="413b0-107">[in] A pointer to a buffer that stores the data to be written.</span></span>  
  
 `bytesRequested`  
 <span data-ttu-id="413b0-108">in Numero di byte da scrivere.</span><span class="sxs-lookup"><span data-stu-id="413b0-108">[in] The number of bytes to be written.</span></span>  
  
 `bytesWritten`  
 <span data-ttu-id="413b0-109">out Puntatore al numero effettivo di byte scritti.</span><span class="sxs-lookup"><span data-stu-id="413b0-109">[out] A pointer to the actual number of bytes that were written.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="413b0-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="413b0-110">Requirements</span></span>  
 <span data-ttu-id="413b0-111">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="413b0-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="413b0-112">**Intestazione:** ClrData. idl, ClrData. h</span><span class="sxs-lookup"><span data-stu-id="413b0-112">**Header:** ClrData.idl, ClrData.h</span></span>  
  
 <span data-ttu-id="413b0-113">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="413b0-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="413b0-114">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="413b0-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="413b0-115">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="413b0-115">See also</span></span>

- [<span data-ttu-id="413b0-116">Interfaccia ICLRDataTarget</span><span class="sxs-lookup"><span data-stu-id="413b0-116">ICLRDataTarget Interface</span></span>](iclrdatatarget-interface.md)

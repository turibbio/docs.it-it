---
title: Metodo ICLRStrongName::StrongNameTokenFromAssembly
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameTokenFromAssembly
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameTokenFromAssembly
helpviewer_keywords:
- ICLRStrongName::StrongNameTokenFromAssembly method [.NET Framework hosting]
- StrongNameTokenFromAssembly method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: fc725afb-b66b-4015-aa44-1c0d1304197f
topic_type:
- apiref
ms.openlocfilehash: e71fcf80b51edc318bbc7d81bb277c614184ee55
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762513"
---
# <a name="iclrstrongnamestrongnametokenfromassembly-method"></a><span data-ttu-id="10f9a-102">Metodo ICLRStrongName::StrongNameTokenFromAssembly</span><span class="sxs-lookup"><span data-stu-id="10f9a-102">ICLRStrongName::StrongNameTokenFromAssembly Method</span></span>
<span data-ttu-id="10f9a-103">Crea un token con nome sicuro dal file di assembly specificato.</span><span class="sxs-lookup"><span data-stu-id="10f9a-103">Creates a strong name token from the specified assembly file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="10f9a-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="10f9a-104">Syntax</span></span>  
  
```cpp  
HRESULT StrongNameTokenFromAssembly (  
    [in]  LPCWSTR   wszFilePath,  
    [out] BYTE      **ppbStrongNameToken,  
    [out] ULONG     *pcbStrongNameToken  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="10f9a-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="10f9a-105">Parameters</span></span>  
 `wszFilePath`  
 <span data-ttu-id="10f9a-106">in Percorso del file eseguibile di tipo PE per l'assembly.</span><span class="sxs-lookup"><span data-stu-id="10f9a-106">[in] The path to the portable executable (PE) file for the assembly.</span></span>  
  
 `ppbStrongNameToken`  
 <span data-ttu-id="10f9a-107">out Token del nome sicuro restituito.</span><span class="sxs-lookup"><span data-stu-id="10f9a-107">[out] The returned strong name token.</span></span>  
  
 `pcbStrongNameToken`  
 <span data-ttu-id="10f9a-108">out Dimensione, in byte, del token del nome sicuro.</span><span class="sxs-lookup"><span data-stu-id="10f9a-108">[out] The size, in bytes, of the strong name token.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="10f9a-109">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="10f9a-109">Return Value</span></span>  
 <span data-ttu-id="10f9a-110">`S_OK`Se il metodo è stato completato correttamente; in caso contrario, valore HRESULT che indica l'esito negativo (vedere [valori HRESULT comuni](/windows/win32/seccrypto/common-hresult-values) per un elenco).</span><span class="sxs-lookup"><span data-stu-id="10f9a-110">`S_OK` if the method completed successfully; otherwise, an HRESULT value that indicates failure (see [Common HRESULT Values](/windows/win32/seccrypto/common-hresult-values) for a list).</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="10f9a-111">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="10f9a-111">Remarks</span></span>  
 <span data-ttu-id="10f9a-112">Un token di nome sicuro è il formato abbreviato di una chiave pubblica.</span><span class="sxs-lookup"><span data-stu-id="10f9a-112">A strong name token is the shortened form of a public key.</span></span> <span data-ttu-id="10f9a-113">Il token è un hash a 64 bit creato dalla chiave pubblica usata per firmare l'assembly.</span><span class="sxs-lookup"><span data-stu-id="10f9a-113">The token is a 64-bit hash that is created from the public key used to sign the assembly.</span></span> <span data-ttu-id="10f9a-114">Il token fa parte del nome sicuro dell'assembly e può essere letto dai metadati dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="10f9a-114">The token is a part of the strong name for the assembly, and can be read from the assembly metadata.</span></span>  
  
 <span data-ttu-id="10f9a-115">Dopo aver creato il token, è necessario chiamare il metodo [ICLRStrongName:: StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md) per rilasciare la memoria allocata.</span><span class="sxs-lookup"><span data-stu-id="10f9a-115">After the token is created, you should call the [ICLRStrongName::StrongNameFreeBuffer](iclrstrongname-strongnamefreebuffer-method.md) method to release the allocated memory.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="10f9a-116">Requisiti</span><span class="sxs-lookup"><span data-stu-id="10f9a-116">Requirements</span></span>  
 <span data-ttu-id="10f9a-117">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="10f9a-117">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="10f9a-118">**Intestazione:** Metahost. h</span><span class="sxs-lookup"><span data-stu-id="10f9a-118">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="10f9a-119">**Libreria:** Incluso come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="10f9a-119">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="10f9a-120">**Versioni .NET Framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="10f9a-120">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="10f9a-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="10f9a-121">See also</span></span>

- [<span data-ttu-id="10f9a-122">Metodo StrongNameTokenFromAssemblyEx</span><span class="sxs-lookup"><span data-stu-id="10f9a-122">StrongNameTokenFromAssemblyEx Method</span></span>](iclrstrongname-strongnametokenfromassemblyex-method.md)
- [<span data-ttu-id="10f9a-123">Interfaccia ICLRStrongName</span><span class="sxs-lookup"><span data-stu-id="10f9a-123">ICLRStrongName Interface</span></span>](iclrstrongname-interface.md)

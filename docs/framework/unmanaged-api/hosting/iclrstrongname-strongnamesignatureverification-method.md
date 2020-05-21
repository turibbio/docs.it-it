---
title: Metodo ICLRStrongName::StrongNameSignatureVerification
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureVerification
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureVerification
helpviewer_keywords:
- ICLRStrongName::StrongNameSignatureVerification method [.NET Framework hosting]
- StrongNameSignatureVerification method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: 734dc4d1-0a76-4736-b5ac-cb4253b3dd49
topic_type:
- apiref
ms.openlocfilehash: d31c9c0db306aad3a7c3472ef6329f25aa6c5902
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762656"
---
# <a name="iclrstrongnamestrongnamesignatureverification-method"></a><span data-ttu-id="75190-102">Metodo ICLRStrongName::StrongNameSignatureVerification</span><span class="sxs-lookup"><span data-stu-id="75190-102">ICLRStrongName::StrongNameSignatureVerification Method</span></span>
<span data-ttu-id="75190-103">Ottiene un valore che indica se il manifesto dell'assembly nel percorso specificato contiene una firma con nome sicuro, che viene verificata in base ai flag specificati.</span><span class="sxs-lookup"><span data-stu-id="75190-103">Gets a value that indicates whether the assembly manifest at the supplied path contains a strong name signature, which is verified according to the specified flags.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="75190-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="75190-104">Syntax</span></span>  
  
```cpp  
HRESULT StrongNameSignatureVerification (  
    [in]  LPCWSTR   wszFilePath,  
    [in]  DWORD     dwInFlags,  
    [out] DWORD     *pdwOutFlags  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="75190-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="75190-105">Parameters</span></span>  
 `wszFilePath`  
 <span data-ttu-id="75190-106">in Percorso del file eseguibile (con estensione dll o exe) portatile per l'assembly da verificare.</span><span class="sxs-lookup"><span data-stu-id="75190-106">[in] The path to the portable executable (.dll or .exe) file for the assembly to verify.</span></span>  
  
 `dwInFlags`  
 <span data-ttu-id="75190-107">in Flag per modificare il comportamento di verifica.</span><span class="sxs-lookup"><span data-stu-id="75190-107">[in] Flags to modify the verification behavior.</span></span> <span data-ttu-id="75190-108">Sono supportati i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="75190-108">The following values are supported:</span></span>  
  
- <span data-ttu-id="75190-109">`SN_INFLAG_FORCE_VER`(0x00000001): impone la verifica anche se è necessario eseguire l'override delle impostazioni del registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="75190-109">`SN_INFLAG_FORCE_VER` (0x00000001) - Forces verification even if it is necessary to override registry settings.</span></span>  
  
- <span data-ttu-id="75190-110">`SN_INFLAG_INSTALL`(0x00000002): specifica che questa è la prima volta che il manifesto viene verificato.</span><span class="sxs-lookup"><span data-stu-id="75190-110">`SN_INFLAG_INSTALL` (0x00000002) - Specifies that this is the first time the manifest is verified.</span></span>  
  
- <span data-ttu-id="75190-111">`SN_INFLAG_ADMIN_ACCESS`(0x00000004): specifica che la cache consentirà l'accesso solo agli utenti che dispongono di privilegi amministrativi.</span><span class="sxs-lookup"><span data-stu-id="75190-111">`SN_INFLAG_ADMIN_ACCESS` (0x00000004) - Specifies that the cache will allow access only to users who have administrative privileges.</span></span>  
  
- <span data-ttu-id="75190-112">`SN_INFLAG_USER_ACCESS`(0x00000008): specifica che l'assembly sarà accessibile solo all'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="75190-112">`SN_INFLAG_USER_ACCESS` (0x00000008) - Specifies that the assembly will be accessible only to the current user.</span></span>  
  
- <span data-ttu-id="75190-113">`SN_INFLAG_ALL_ACCESS`(0x00000010): specifica che la cache non fornirà alcuna garanzia di restrizione di accesso.</span><span class="sxs-lookup"><span data-stu-id="75190-113">`SN_INFLAG_ALL_ACCESS` (0x00000010) - Specifies that the cache will provide no guarantees of access restriction.</span></span>  
  
- <span data-ttu-id="75190-114">`SN_INFLAG_RUNTIME`(0x80000000)-riservato per il debug interno.</span><span class="sxs-lookup"><span data-stu-id="75190-114">`SN_INFLAG_RUNTIME` (0x80000000) - Reserved for internal debugging.</span></span>  
  
 `pdwOutFlags`  
 <span data-ttu-id="75190-115">out Flag che indicano se la firma del nome sicuro è stata verificata.</span><span class="sxs-lookup"><span data-stu-id="75190-115">[out] Flags indicating whether the strong name signature was verified.</span></span> <span data-ttu-id="75190-116">È supportato il valore seguente:</span><span class="sxs-lookup"><span data-stu-id="75190-116">The following value is supported:</span></span>  
  
- <span data-ttu-id="75190-117">`SN_OUTFLAG_WAS_VERIFIED`(0x00000001): questo valore è impostato su `false` per specificare che la verifica ha avuto esito positivo a causa delle impostazioni del registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="75190-117">`SN_OUTFLAG_WAS_VERIFIED` (0x00000001) - This value is set to `false` to specify that the verification succeeded due to registry settings.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="75190-118">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="75190-118">Return Value</span></span>  
 <span data-ttu-id="75190-119">`S_OK`Se il metodo è stato completato correttamente; in caso contrario, valore HRESULT che indica l'esito negativo (vedere [valori HRESULT comuni](/windows/win32/seccrypto/common-hresult-values) per un elenco).</span><span class="sxs-lookup"><span data-stu-id="75190-119">`S_OK` if the method completed successfully; otherwise, an HRESULT value that indicates failure (see [Common HRESULT Values](/windows/win32/seccrypto/common-hresult-values) for a list).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="75190-120">Requisiti</span><span class="sxs-lookup"><span data-stu-id="75190-120">Requirements</span></span>  
 <span data-ttu-id="75190-121">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="75190-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="75190-122">**Intestazione:** Metahost. h</span><span class="sxs-lookup"><span data-stu-id="75190-122">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="75190-123">**Libreria:** Incluso come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="75190-123">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="75190-124">**Versioni .NET Framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="75190-124">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="75190-125">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="75190-125">See also</span></span>

- [<span data-ttu-id="75190-126">Metodo StrongNameSignatureVerificationEx</span><span class="sxs-lookup"><span data-stu-id="75190-126">StrongNameSignatureVerificationEx Method</span></span>](iclrstrongname-strongnamesignatureverificationex-method.md)
- [<span data-ttu-id="75190-127">Interfaccia ICLRStrongName</span><span class="sxs-lookup"><span data-stu-id="75190-127">ICLRStrongName Interface</span></span>](iclrstrongname-interface.md)

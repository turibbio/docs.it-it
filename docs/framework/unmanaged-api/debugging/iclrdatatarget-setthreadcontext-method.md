---
title: Metodo ICLRDataTarget::SetThreadContext
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.SetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::SetThreadContext
helpviewer_keywords:
- SetThreadContext method, ICLRDataTarget interface [.NET Framework debugging]
- ICLRDataTarget::SetThreadContext method [.NET Framework debugging]
ms.assetid: 103c8502-81fe-40d7-9c1e-9008d8fb19e1
topic_type:
- apiref
ms.openlocfilehash: b8c4b4e585bba4df39a743273221f38ce14a9b9d
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860526"
---
# <a name="iclrdatatargetsetthreadcontext-method"></a><span data-ttu-id="571fa-102">Metodo ICLRDataTarget::SetThreadContext</span><span class="sxs-lookup"><span data-stu-id="571fa-102">ICLRDataTarget::SetThreadContext Method</span></span>
<span data-ttu-id="571fa-103">Imposta il contesto corrente del thread specificato nel processo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="571fa-103">Sets the current context of the specified thread in the target process.</span></span> <span data-ttu-id="571fa-104">Questo metodo viene chiamato dai servizi di accesso ai dati di Common Language Runtime (CLR).</span><span class="sxs-lookup"><span data-stu-id="571fa-104">This method is called by the common language runtime (CLR) data access services.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="571fa-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="571fa-105">Syntax</span></span>  
  
```cpp  
HRESULT SetThreadContext (  
    [in] ULONG32            threadID,  
    [in] ULONG32            contextSize,  
    [in, size_is(contextSize)]
         BYTE               *context  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="571fa-106">Parametri</span><span class="sxs-lookup"><span data-stu-id="571fa-106">Parameters</span></span>  
 `threadID`  
 <span data-ttu-id="571fa-107">in Identificatore del sistema operativo di un thread nel processo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="571fa-107">[in] The operating system identifier of a thread in the target process.</span></span>  
  
 `contextSize`  
 <span data-ttu-id="571fa-108">in Dimensioni del contesto.</span><span class="sxs-lookup"><span data-stu-id="571fa-108">[in] The size of the context.</span></span>  
  
 `context`  
 <span data-ttu-id="571fa-109">in Puntatore a un buffer contenente il contesto.</span><span class="sxs-lookup"><span data-stu-id="571fa-109">[in] Pointer to a buffer containing the context.</span></span>  
  
 <span data-ttu-id="571fa-110">I dati nel `context` buffer saranno nel formato della struttura Win32 `CONTEXT` .</span><span class="sxs-lookup"><span data-stu-id="571fa-110">The data in the `context` buffer will be in the format of the Win32 `CONTEXT` structure.</span></span> <span data-ttu-id="571fa-111">Il contesto specifica i dati del registro specifici del processore, pertanto la definizione della `CONTEXT` struttura Win32 dipende dall'architettura del processore.</span><span class="sxs-lookup"><span data-stu-id="571fa-111">The context specifies processor-specific register data, so the definition of the Win32 `CONTEXT` structure depends on the processor's architecture.</span></span> <span data-ttu-id="571fa-112">Per la definizione della struttura Win32 `CONTEXT` , fare riferimento al file di intestazione Winnt. h.</span><span class="sxs-lookup"><span data-stu-id="571fa-112">Refer to the WinNT.h header file for the definition of the Win32 `CONTEXT` structure.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="571fa-113">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="571fa-113">Remarks</span></span>  
 <span data-ttu-id="571fa-114">Questo metodo è implementato dal writer dell'applicazione di debug.</span><span class="sxs-lookup"><span data-stu-id="571fa-114">This method is implemented by the writer of the debugging application.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="571fa-115">Requisiti</span><span class="sxs-lookup"><span data-stu-id="571fa-115">Requirements</span></span>  
 <span data-ttu-id="571fa-116">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="571fa-116">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="571fa-117">**Intestazione:** ClrData. idl, ClrData. h</span><span class="sxs-lookup"><span data-stu-id="571fa-117">**Header:** ClrData.idl, ClrData.h</span></span>  
  
 <span data-ttu-id="571fa-118">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="571fa-118">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="571fa-119">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="571fa-119">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="571fa-120">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="571fa-120">See also</span></span>

- [<span data-ttu-id="571fa-121">Interfaccia ICLRDataTarget</span><span class="sxs-lookup"><span data-stu-id="571fa-121">ICLRDataTarget Interface</span></span>](iclrdatatarget-interface.md)

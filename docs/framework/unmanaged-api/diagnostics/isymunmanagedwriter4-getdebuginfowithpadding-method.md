---
title: Metodo ISymUnmanagedWriter4::GetDebugInfoWithPadding
ms.date: 03/30/2017
ms.assetid: 881e20ca-8131-4bd0-ba41-c2d6391b0fe2
ms.openlocfilehash: cfc6c22558cee780823c8cca0c36b883147e9496
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614643"
---
# <a name="isymunmanagedwriter4getdebuginfowithpadding-method"></a><span data-ttu-id="8176e-102">Metodo ISymUnmanagedWriter4::GetDebugInfoWithPadding</span><span class="sxs-lookup"><span data-stu-id="8176e-102">ISymUnmanagedWriter4::GetDebugInfoWithPadding Method</span></span>
<span data-ttu-id="8176e-103">Funziona allo stesso modo del [Metodo GetDebugInfo](isymunmanagedwriter-getdebuginfo-method.md) , con la differenza che la stringa di percorso viene riempita con zeri che seguono il carattere null di terminazione per fare in modo che i dati della stringa siano di dimensioni fisse `MAX_PATH` .</span><span class="sxs-lookup"><span data-stu-id="8176e-103">Functions the same as [GetDebugInfo Method](isymunmanagedwriter-getdebuginfo-method.md) except that the path string is padded with zeros following the terminating null character to make the string data a fixed size of `MAX_PATH`.</span></span> <span data-ttu-id="8176e-104">La spaziatura interna viene specificata solo se la lunghezza della stringa di percorso è minore di `MAX_PATH` .</span><span class="sxs-lookup"><span data-stu-id="8176e-104">Padding is only given if the path string length itself is less than `MAX_PATH`.</span></span>  
  
 <span data-ttu-id="8176e-105">In questo modo è più semplice scrivere strumenti che differenziano i file PE.</span><span class="sxs-lookup"><span data-stu-id="8176e-105">This makes it easier to write tools that difference PE files.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8176e-106">Sintassi</span><span class="sxs-lookup"><span data-stu-id="8176e-106">Syntax</span></span>  
  
```idl  
HRESULT GetDebugInfoWithPadding(    [in, out] IMAGE_DEBUG_DIRECTORY *pIDD,    [in] DWORD cData,    [out] DWORD *pcData,    [out, size_is(cData), length_is(*pcData)] BYTE data[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="8176e-107">Parametri</span><span class="sxs-lookup"><span data-stu-id="8176e-107">Parameters</span></span>  
  
|<span data-ttu-id="8176e-108">Parametro</span><span class="sxs-lookup"><span data-stu-id="8176e-108">Parameter</span></span>|<span data-ttu-id="8176e-109">Description</span><span class="sxs-lookup"><span data-stu-id="8176e-109">Description</span></span>|  
|---------------|-----------------|  
|`pIDD`||  
|`cData`||  
|`pcData`||  
|`data`||  
  
## <a name="return-value"></a><span data-ttu-id="8176e-110">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="8176e-110">Return Value</span></span>  
 <span data-ttu-id="8176e-111">Restituisce `HRESULT`.</span><span class="sxs-lookup"><span data-stu-id="8176e-111">Returns `HRESULT`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8176e-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="8176e-112">Requirements</span></span>  
 <span data-ttu-id="8176e-113">**Intestazione:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="8176e-113">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8176e-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8176e-114">See also</span></span>

- [<span data-ttu-id="8176e-115">Interfaccia ISymUnmanagedWriter4</span><span class="sxs-lookup"><span data-stu-id="8176e-115">ISymUnmanagedWriter4 Interface</span></span>](isymunmanagedwriter4-interface.md)

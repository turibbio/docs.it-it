---
title: Metodo ISymUnmanagedMethod::GetRootScope
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetRootScope
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetRootScope
helpviewer_keywords:
- ISymUnmanagedMethod::GetRootScope method [.NET Framework debugging]
- GetRootScope method [.NET Framework debugging]
ms.assetid: 7d58caac-2e75-4dfa-9249-32d8a624b247
topic_type:
- apiref
ms.openlocfilehash: 650a64e72b410cddfbee7dce676ddbb5a3b8b3d3
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614448"
---
# <a name="isymunmanagedmethodgetrootscope-method"></a><span data-ttu-id="5fd73-102">Metodo ISymUnmanagedMethod::GetRootScope</span><span class="sxs-lookup"><span data-stu-id="5fd73-102">ISymUnmanagedMethod::GetRootScope Method</span></span>
<span data-ttu-id="5fd73-103">Ottiene l'ambito lessicale radice all'interno di questo metodo.</span><span class="sxs-lookup"><span data-stu-id="5fd73-103">Gets the root lexical scope within this method.</span></span> <span data-ttu-id="5fd73-104">Questo ambito racchiude l'intero metodo.</span><span class="sxs-lookup"><span data-stu-id="5fd73-104">This scope encloses the entire method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5fd73-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="5fd73-105">Syntax</span></span>  
  
```cpp  
HRESULT GetRootScope(  
    [out, retval] ISymUnmanagedScope** pRetVal);  
```  
  
## <a name="parameters"></a><span data-ttu-id="5fd73-106">Parametri</span><span class="sxs-lookup"><span data-stu-id="5fd73-106">Parameters</span></span>  
 `pRetVal`  
 <span data-ttu-id="5fd73-107">out Puntatore impostato sull'interfaccia [ISymUnmanagedScope](isymunmanagedscope-interface.md) restituita.</span><span class="sxs-lookup"><span data-stu-id="5fd73-107">[out] A pointer that is set to the returned [ISymUnmanagedScope](isymunmanagedscope-interface.md) interface.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="5fd73-108">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="5fd73-108">Return Value</span></span>  
 <span data-ttu-id="5fd73-109">S_OK se il metodo ha esito positivo; in caso contrario, E_FAIL o un altro codice di errore.</span><span class="sxs-lookup"><span data-stu-id="5fd73-109">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="5fd73-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="5fd73-110">Requirements</span></span>  
 <span data-ttu-id="5fd73-111">**Intestazione:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="5fd73-111">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5fd73-112">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5fd73-112">See also</span></span>

- [<span data-ttu-id="5fd73-113">Interfaccia ISymUnmanagedMethod</span><span class="sxs-lookup"><span data-stu-id="5fd73-113">ISymUnmanagedMethod Interface</span></span>](isymunmanagedmethod-interface.md)

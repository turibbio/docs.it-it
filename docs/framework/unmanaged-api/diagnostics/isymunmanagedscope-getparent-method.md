---
title: Metodo ISymUnmanagedScope::GetParent
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope.GetParent
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope::GetParent
helpviewer_keywords:
- GetParent method [.NET Framework debugging]
- ISymUnmanagedScope::GetParent method [.NET Framework debugging]
ms.assetid: c7963c87-6ec5-49b3-a5cd-e0fe0c43f9b4
topic_type:
- apiref
ms.openlocfilehash: 95ae081d61200e4fd020609a4d23783f265d2cc6
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615358"
---
# <a name="isymunmanagedscopegetparent-method"></a><span data-ttu-id="aa709-102">Metodo ISymUnmanagedScope::GetParent</span><span class="sxs-lookup"><span data-stu-id="aa709-102">ISymUnmanagedScope::GetParent Method</span></span>
<span data-ttu-id="aa709-103">Ottiene l'ambito padre di questo ambito.</span><span class="sxs-lookup"><span data-stu-id="aa709-103">Gets the parent scope of this scope.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="aa709-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="aa709-104">Syntax</span></span>  
  
```cpp  
HRESULT GetParent(  
    [out, retval] ISymUnmanagedScope** pRetVal);  
```  
  
## <a name="parameters"></a><span data-ttu-id="aa709-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="aa709-105">Parameters</span></span>  
 `pRetVal`  
 <span data-ttu-id="aa709-106">out Puntatore all'interfaccia [ISymUnmanagedScope](isymunmanagedscope-interface.md) restituita.</span><span class="sxs-lookup"><span data-stu-id="aa709-106">[out] A pointer to the returned [ISymUnmanagedScope](isymunmanagedscope-interface.md) interface.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="aa709-107">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="aa709-107">Return Value</span></span>  
 <span data-ttu-id="aa709-108">S_OK se il metodo ha esito positivo; in caso contrario, E_FAIL o un altro codice di errore.</span><span class="sxs-lookup"><span data-stu-id="aa709-108">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="aa709-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="aa709-109">Requirements</span></span>  
 <span data-ttu-id="aa709-110">**Intestazione:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="aa709-110">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="aa709-111">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="aa709-111">See also</span></span>

- [<span data-ttu-id="aa709-112">Interfaccia ISymUnmanagedScope</span><span class="sxs-lookup"><span data-stu-id="aa709-112">ISymUnmanagedScope Interface</span></span>](isymunmanagedscope-interface.md)
- [<span data-ttu-id="aa709-113">Metodo GetChildren</span><span class="sxs-lookup"><span data-stu-id="aa709-113">GetChildren Method</span></span>](isymunmanagedscope-getchildren-method.md)

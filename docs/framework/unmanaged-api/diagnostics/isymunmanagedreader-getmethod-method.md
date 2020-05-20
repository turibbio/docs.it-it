---
title: Metodo ISymUnmanagedReader::GetMethod
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetMethod
helpviewer_keywords:
- GetMethod method, ISymUnmanagedReader interface [.NET Framework debugging]
- ISymUnmanagedReader::GetMethod method [.NET Framework debugging]
ms.assetid: ae6cfb29-bc2c-4606-af86-1d32ebd31020
topic_type:
- apiref
ms.openlocfilehash: 864acb07797676c825afe62321b0d65e37938fa6
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615007"
---
# <a name="isymunmanagedreadergetmethod-method"></a><span data-ttu-id="75427-102">Metodo ISymUnmanagedReader::GetMethod</span><span class="sxs-lookup"><span data-stu-id="75427-102">ISymUnmanagedReader::GetMethod Method</span></span>
<span data-ttu-id="75427-103">Ottiene un metodo del lettore di simboli, dato un token di metodo.</span><span class="sxs-lookup"><span data-stu-id="75427-103">Gets a symbol reader method, given a method token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="75427-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="75427-104">Syntax</span></span>  
  
```cpp  
HRESULT GetMethod (  
    [in]  mdMethodDef  token,  
    [out, retval] ISymUnmanagedMethod**  pRetVal);  
```  
  
## <a name="parameters"></a><span data-ttu-id="75427-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="75427-105">Parameters</span></span>  
 `token`  
 <span data-ttu-id="75427-106">in Token del metodo.</span><span class="sxs-lookup"><span data-stu-id="75427-106">[in] The method token.</span></span>  
  
 `pRetVal`  
 <span data-ttu-id="75427-107">out Puntatore all'interfaccia restituita.</span><span class="sxs-lookup"><span data-stu-id="75427-107">[out] A pointer to the returned interface.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="75427-108">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="75427-108">Return Value</span></span>  
 <span data-ttu-id="75427-109">S_OK se il metodo ha esito positivo; in caso contrario, E_FAIL o un altro codice di errore.</span><span class="sxs-lookup"><span data-stu-id="75427-109">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="75427-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="75427-110">Requirements</span></span>  
 <span data-ttu-id="75427-111">**Intestazione:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="75427-111">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="75427-112">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="75427-112">See also</span></span>

- [<span data-ttu-id="75427-113">Interfaccia ISymUnmanagedReader</span><span class="sxs-lookup"><span data-stu-id="75427-113">ISymUnmanagedReader Interface</span></span>](isymunmanagedreader-interface.md)

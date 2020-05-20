---
title: Metodo ISymUnmanagedVariable::GetAddressField3
ms.date: 03/30/2017
api_name:
- ISymUnmanagedVariable.GetAddressField3
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedVariable::GetAddressField3
helpviewer_keywords:
- ISymUnmanagedVariable::GetAddressField3 method [.NET Framework debugging]
- GetAddressField3 method [.NET Framework debugging]
ms.assetid: 4d834721-ad8d-439d-b356-c6b4aef022fc
topic_type:
- apiref
ms.openlocfilehash: ff888d3e2b86efeea3f4e3d33528f731d85886bf
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615267"
---
# <a name="isymunmanagedvariablegetaddressfield3-method"></a><span data-ttu-id="fac0e-102">Metodo ISymUnmanagedVariable::GetAddressField3</span><span class="sxs-lookup"><span data-stu-id="fac0e-102">ISymUnmanagedVariable::GetAddressField3 Method</span></span>
<span data-ttu-id="fac0e-103">Ottiene il terzo campo dell'indirizzo per questa variabile.</span><span class="sxs-lookup"><span data-stu-id="fac0e-103">Gets the third address field for this variable.</span></span> <span data-ttu-id="fac0e-104">Il suo significato dipende dal tipo di indirizzo.</span><span class="sxs-lookup"><span data-stu-id="fac0e-104">Its meaning depends on the kind of address.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fac0e-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="fac0e-105">Syntax</span></span>  
  
```cpp  
HRESULT GetAddressField3(  
    [out, retval] ULONG32* pRetVal);  
```  
  
## <a name="parameters"></a><span data-ttu-id="fac0e-106">Parametri</span><span class="sxs-lookup"><span data-stu-id="fac0e-106">Parameters</span></span>  
 `pRetVal`  
 <span data-ttu-id="fac0e-107">out Puntatore a un oggetto `ULONG32` che riceve il terzo campo dell'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="fac0e-107">[out] A pointer to a `ULONG32` that receives the third address field.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="fac0e-108">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="fac0e-108">Return Value</span></span>  
 <span data-ttu-id="fac0e-109">S_OK se il metodo ha esito positivo; in caso contrario, E_FAIL o un altro codice di errore.</span><span class="sxs-lookup"><span data-stu-id="fac0e-109">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="fac0e-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="fac0e-110">Requirements</span></span>  
 <span data-ttu-id="fac0e-111">**Intestazione:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="fac0e-111">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fac0e-112">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="fac0e-112">See also</span></span>

- [<span data-ttu-id="fac0e-113">Interfaccia ISymUnmanagedVariable</span><span class="sxs-lookup"><span data-stu-id="fac0e-113">ISymUnmanagedVariable Interface</span></span>](isymunmanagedvariable-interface.md)
- [<span data-ttu-id="fac0e-114">Metodo GetAddressField1</span><span class="sxs-lookup"><span data-stu-id="fac0e-114">GetAddressField1 Method</span></span>](isymunmanagedvariable-getaddressfield1-method.md)
- [<span data-ttu-id="fac0e-115">Metodo GetAddressField2</span><span class="sxs-lookup"><span data-stu-id="fac0e-115">GetAddressField2 Method</span></span>](isymunmanagedvariable-getaddressfield2-method.md)
- [<span data-ttu-id="fac0e-116">Metodo GetAddressKind</span><span class="sxs-lookup"><span data-stu-id="fac0e-116">GetAddressKind Method</span></span>](isymunmanagedvariable-getaddresskind-method.md)

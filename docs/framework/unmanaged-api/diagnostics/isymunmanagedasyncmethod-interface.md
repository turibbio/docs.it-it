---
title: Interfaccia ISymUnmanagedAsyncMethod
ms.date: 03/30/2017
ms.assetid: f2de5224-fd91-45de-9e58-bc600c6d22f1
ms.openlocfilehash: 448ed719331469dce8f15500f14d5c1b0707ecf7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504452"
---
# <a name="isymunmanagedasyncmethod-interface"></a><span data-ttu-id="39c19-102">Interfaccia ISymUnmanagedAsyncMethod</span><span class="sxs-lookup"><span data-stu-id="39c19-102">ISymUnmanagedAsyncMethod Interface</span></span>
<span data-ttu-id="39c19-103">Questa interfaccia è il complemento di lettura per l' [interfaccia ISymUnmanagedAsyncMethodPropertiesWriter](isymunmanagedasyncmethodpropertieswriter-interface.md).</span><span class="sxs-lookup"><span data-stu-id="39c19-103">This interface is the reading complement to [ISymUnmanagedAsyncMethodPropertiesWriter Interface](isymunmanagedasyncmethodpropertieswriter-interface.md).</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="39c19-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="39c19-104">Syntax</span></span>  
  
```idl  
[object,uuid(B20D55B3-532E-4906-87E7-25BD5734ABD2),pointer_default(unique)]interface ISymUnmanagedAsyncMethod : IUnknown  
```  
  
## <a name="methods"></a><span data-ttu-id="39c19-105">Metodi</span><span class="sxs-lookup"><span data-stu-id="39c19-105">Methods</span></span>  
 <span data-ttu-id="39c19-106">Per l'interfaccia sono disponibili i seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="39c19-106">This interface contains the following methods:</span></span>  
  
|<span data-ttu-id="39c19-107">Metodo</span><span class="sxs-lookup"><span data-stu-id="39c19-107">Method</span></span>|<span data-ttu-id="39c19-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="39c19-108">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="39c19-109">Metodo GetAsyncStepInfo</span><span class="sxs-lookup"><span data-stu-id="39c19-109">GetAsyncStepInfo Method</span></span>](isymunmanagedasyncmethod-getasyncstepinfo-method.md)|<span data-ttu-id="39c19-110">Vedere il [Metodo DefineAsyncStepInfo](isymunmanagedasyncmethodpropertieswriter-defineasyncstepinfo-method.md).</span><span class="sxs-lookup"><span data-stu-id="39c19-110">See [DefineAsyncStepInfo Method](isymunmanagedasyncmethodpropertieswriter-defineasyncstepinfo-method.md).</span></span>|  
|[<span data-ttu-id="39c19-111">Metodo GetAsyncStepInfoCount</span><span class="sxs-lookup"><span data-stu-id="39c19-111">GetAsyncStepInfoCount Method</span></span>](isymunmanagedasyncmethod-getasyncstepinfocount-method.md)|<span data-ttu-id="39c19-112">Vedere il [Metodo DefineAsyncStepInfo](isymunmanagedasyncmethodpropertieswriter-defineasyncstepinfo-method.md).</span><span class="sxs-lookup"><span data-stu-id="39c19-112">See [DefineAsyncStepInfo Method](isymunmanagedasyncmethodpropertieswriter-defineasyncstepinfo-method.md).</span></span>|  
|[<span data-ttu-id="39c19-113">Metodo GetCatchHandlerILOffset</span><span class="sxs-lookup"><span data-stu-id="39c19-113">GetCatchHandlerILOffset Method</span></span>](isymunmanagedasyncmethod-getcatchhandleriloffset-method.md)|<span data-ttu-id="39c19-114">Vedere il [Metodo DefineCatchHandlerILOffset](isymunmanagedasyncmethodpropertieswriter-definecatchhandleriloffset-method.md).</span><span class="sxs-lookup"><span data-stu-id="39c19-114">See [DefineCatchHandlerILOffset Method](isymunmanagedasyncmethodpropertieswriter-definecatchhandleriloffset-method.md).</span></span>|  
|[<span data-ttu-id="39c19-115">Metodo GetKickoffMethod</span><span class="sxs-lookup"><span data-stu-id="39c19-115">GetKickoffMethod Method</span></span>](isymunmanagedasyncmethod-getkickoffmethod-method.md)|<span data-ttu-id="39c19-116">Vedere il [Metodo DefineKickoffMethod](isymunmanagedasyncmethodpropertieswriter-definekickoffmethod-method.md).</span><span class="sxs-lookup"><span data-stu-id="39c19-116">See [DefineKickoffMethod Method](isymunmanagedasyncmethodpropertieswriter-definekickoffmethod-method.md).</span></span>|  
|[<span data-ttu-id="39c19-117">Metodo HasCatchHandlerILOffset</span><span class="sxs-lookup"><span data-stu-id="39c19-117">HasCatchHandlerILOffset Method</span></span>](isymunmanagedasyncmethod-hascatchhandleriloffset-method.md)|<span data-ttu-id="39c19-118">Vedere il [Metodo DefineCatchHandlerILOffset](isymunmanagedasyncmethodpropertieswriter-definecatchhandleriloffset-method.md).</span><span class="sxs-lookup"><span data-stu-id="39c19-118">See [DefineCatchHandlerILOffset Method](isymunmanagedasyncmethodpropertieswriter-definecatchhandleriloffset-method.md).</span></span>|  
|[<span data-ttu-id="39c19-119">Metodo IsAsyncMethod</span><span class="sxs-lookup"><span data-stu-id="39c19-119">IsAsyncMethod Method</span></span>](isymunmanagedasyncmethod-isasyncmethod-method.md)|<span data-ttu-id="39c19-120">Verifica se il metodo contiene informazioni asincrone o meno.</span><span class="sxs-lookup"><span data-stu-id="39c19-120">Checks if the method has async information or not.</span></span><br /><br /> <span data-ttu-id="39c19-121">Se questo metodo restituisce `FALSE` , non è valido chiamare altri metodi in questa interfaccia.</span><span class="sxs-lookup"><span data-stu-id="39c19-121">If this method returns `FALSE` then it is invalid to call any other methods in this interface.</span></span> <span data-ttu-id="39c19-122">`E_UNEXPECTED`In questo caso verranno restituiti tutti.</span><span class="sxs-lookup"><span data-stu-id="39c19-122">They will all return `E_UNEXPECTED` in this case.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="39c19-123">Requisiti</span><span class="sxs-lookup"><span data-stu-id="39c19-123">Requirements</span></span>  
 <span data-ttu-id="39c19-124">**Intestazione:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="39c19-124">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="39c19-125">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="39c19-125">See also</span></span>

- [<span data-ttu-id="39c19-126">Interfacce dell'archivio dei simboli di diagnostica</span><span class="sxs-lookup"><span data-stu-id="39c19-126">Diagnostics Symbol Store Interfaces</span></span>](diagnostics-symbol-store-interfaces.md)

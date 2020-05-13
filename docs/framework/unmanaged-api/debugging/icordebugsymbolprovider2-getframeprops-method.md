---
title: Metodo ICorDebugSymbolProvider2::GetFrameProps
ms.date: 03/30/2017
ms.assetid: f07b73f3-188d-43a9-8f7d-44dce2f1ddb7
ms.openlocfilehash: ad44c5a7b2d901967ae354f3c30218a8c7f2c2de
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379328"
---
# <a name="icordebugsymbolprovider2getframeprops-method"></a><span data-ttu-id="ff1b0-102">Metodo ICorDebugSymbolProvider2::GetFrameProps</span><span class="sxs-lookup"><span data-stu-id="ff1b0-102">ICorDebugSymbolProvider2::GetFrameProps Method</span></span>
<span data-ttu-id="ff1b0-103">Restituisce l'indirizzo RVA (Relative Virtual Address) iniziale di un metodo e il frame padre in base a un indirizzo virtuale relativo al codice.</span><span class="sxs-lookup"><span data-stu-id="ff1b0-103">Returns the method starting relative virtual address of a method and the parent frame given a code relative virtual address.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ff1b0-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="ff1b0-104">Syntax</span></span>  
  
```cpp  
HRESULT GetFrameProps(  
   [in] ULONG32 codeRva,  
   [out] ULONG32 *pCodeStartRva,  
   [out] ULONG32 *pParentFrameStartRva  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="ff1b0-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="ff1b0-105">Parameters</span></span>  
 `codeRva`  
 <span data-ttu-id="ff1b0-106">[in] Indirizzo RVA (Relative Virtual Address)</span><span class="sxs-lookup"><span data-stu-id="ff1b0-106">[in] A code relative virtual address.</span></span>  
  
 `pCodeStartRva`  
 <span data-ttu-id="ff1b0-107">[out] Puntatore all'indirizzo RVA (Relative Virtual Address) di avvio del metodo.</span><span class="sxs-lookup"><span data-stu-id="ff1b0-107">[out] A pointer to the method's starting relative virtual address.</span></span>  
  
 `pParentFrameStartRva`  
 <span data-ttu-id="ff1b0-108">[out] Puntatore all'indirizzo RVA (Relative Virtual Address) di avvio del frame.</span><span class="sxs-lookup"><span data-stu-id="ff1b0-108">[out] A pointer to the frame's starting relative virtual address.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="ff1b0-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="ff1b0-109">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ff1b0-110">Questo metodo è disponibile solo con .NET Native.</span><span class="sxs-lookup"><span data-stu-id="ff1b0-110">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ff1b0-111">Requisiti</span><span class="sxs-lookup"><span data-stu-id="ff1b0-111">Requirements</span></span>  
 <span data-ttu-id="ff1b0-112">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ff1b0-112">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ff1b0-113">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="ff1b0-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="ff1b0-114">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="ff1b0-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ff1b0-115">**Versioni .NET Framework:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ff1b0-115">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ff1b0-116">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ff1b0-116">See also</span></span>

- [<span data-ttu-id="ff1b0-117">Interfaccia ICorDebugSymbolProvider2</span><span class="sxs-lookup"><span data-stu-id="ff1b0-117">ICorDebugSymbolProvider2 Interface</span></span>](icordebugsymbolprovider2-interface.md)
- [<span data-ttu-id="ff1b0-118">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="ff1b0-118">Debugging Interfaces</span></span>](debugging-interfaces.md)

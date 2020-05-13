---
title: Metodo ICorDebugMemoryBuffer::GetSize
ms.date: 03/30/2017
ms.assetid: 9ffd5482-268e-4680-9fd1-bfb0b7d66450
ms.openlocfilehash: 1bef2e2d0e1a1cef74c7568fdd2e9b7986500488
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212605"
---
# <a name="icordebugmemorybuffergetsize-method"></a><span data-ttu-id="75133-102">Metodo ICorDebugMemoryBuffer::GetSize</span><span class="sxs-lookup"><span data-stu-id="75133-102">ICorDebugMemoryBuffer::GetSize Method</span></span>
<span data-ttu-id="75133-103">Ottiene le dimensioni del buffer di memoria, espresse in byte.</span><span class="sxs-lookup"><span data-stu-id="75133-103">Gets the size of the memory buffer in bytes.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="75133-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="75133-104">Syntax</span></span>  
  
```cpp  
HRESULT GetSize(  
   [out] ULONG32 *pcbBufferLength  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="75133-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="75133-105">Parameters</span></span>  
 `pcbBufferLength`  
 <span data-ttu-id="75133-106">[out] Puntatore alle dimensioni del buffer di memoria.</span><span class="sxs-lookup"><span data-stu-id="75133-106">[out] A pointer to the size of the memory buffer.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="75133-107">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="75133-107">Remarks</span></span>  
  
> [!NOTE]
> <span data-ttu-id="75133-108">Questo metodo è disponibile solo con .NET Native.</span><span class="sxs-lookup"><span data-stu-id="75133-108">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="75133-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="75133-109">Requirements</span></span>  
 <span data-ttu-id="75133-110">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="75133-110">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="75133-111">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="75133-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="75133-112">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="75133-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="75133-113">**Versioni .NET Framework:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="75133-113">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="75133-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="75133-114">See also</span></span>

- [<span data-ttu-id="75133-115">Interfaccia ICorDebugMemoryBuffer</span><span class="sxs-lookup"><span data-stu-id="75133-115">ICorDebugMemoryBuffer Interface</span></span>](icordebugmemorybuffer-interface.md)
- [<span data-ttu-id="75133-116">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="75133-116">Debugging Interfaces</span></span>](debugging-interfaces.md)

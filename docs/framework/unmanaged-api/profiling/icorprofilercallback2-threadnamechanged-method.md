---
title: Metodo ICorProfilerCallback2::ThreadNameChanged
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.ThreadNameChanged
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::ThreadNameChanged
helpviewer_keywords:
- ThreadNameChanged method [.NET Framework profiling]
- ICorProfilerCallback2::ThreadNameChanged method [.NET Framework profiling]
ms.assetid: c8bbd76d-a9ff-44f2-87a6-be052819da36
topic_type:
- apiref
ms.openlocfilehash: 3eb108ed20d0fd1287cb82eb4d552206aeae15d4
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499727"
---
# <a name="icorprofilercallback2threadnamechanged-method"></a><span data-ttu-id="988f5-102">Metodo ICorProfilerCallback2::ThreadNameChanged</span><span class="sxs-lookup"><span data-stu-id="988f5-102">ICorProfilerCallback2::ThreadNameChanged Method</span></span>
<span data-ttu-id="988f5-103">Notifica all'Code Profiler che il nome di un thread è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="988f5-103">Notifies the code profiler that the name of a thread has changed.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="988f5-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="988f5-104">Syntax</span></span>  
  
```cpp  
HRESULT ThreadNameChanged(  
    [in] ThreadID threadId,  
    [in] ULONG cchName,  
    [in] WCHAR name[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="988f5-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="988f5-105">Parameters</span></span>  
 `threadId`  
 <span data-ttu-id="988f5-106">in ID del thread.</span><span class="sxs-lookup"><span data-stu-id="988f5-106">[in] The ID of the thread.</span></span>  
  
 `cchName`  
 <span data-ttu-id="988f5-107">in Lunghezza del nuovo nome del thread.</span><span class="sxs-lookup"><span data-stu-id="988f5-107">[in] The length of the new name of the thread.</span></span>  
  
 `name`  
 <span data-ttu-id="988f5-108">in Nuovo nome del thread.</span><span class="sxs-lookup"><span data-stu-id="988f5-108">[in] The new name of the thread.</span></span> <span data-ttu-id="988f5-109">Il nome non è con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="988f5-109">The name is not null-terminated.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="988f5-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="988f5-110">Requirements</span></span>  
 <span data-ttu-id="988f5-111">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="988f5-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="988f5-112">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="988f5-112">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="988f5-113">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="988f5-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="988f5-114">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="988f5-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="988f5-115">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="988f5-115">See also</span></span>

- [<span data-ttu-id="988f5-116">Interfaccia ICorProfilerCallback</span><span class="sxs-lookup"><span data-stu-id="988f5-116">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="988f5-117">Interfaccia ICorProfilerCallback2</span><span class="sxs-lookup"><span data-stu-id="988f5-117">ICorProfilerCallback2 Interface</span></span>](icorprofilercallback2-interface.md)

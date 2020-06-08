---
title: Interfaccia ICorProfilerThreadEnum
ms.date: 03/30/2017
api_name:
- ICorProfilerThreadEnum
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerThreadEnum
helpviewer_keywords:
- ICorProfilerThreadEnum interface [.NET Framework profiling]
ms.assetid: 1e35031b-e095-4c14-9644-8deeb3081e0b
topic_type:
- apiref
ms.openlocfilehash: d28991254fba73de7a55135844d16417580d8792
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494384"
---
# <a name="icorprofilerthreadenum-interface"></a><span data-ttu-id="a7d74-102">Interfaccia ICorProfilerThreadEnum</span><span class="sxs-lookup"><span data-stu-id="a7d74-102">ICorProfilerThreadEnum Interface</span></span>
<span data-ttu-id="a7d74-103">Fornisce metodi che consentono di eseguire l'iterazione sequenziale con una raccolta di funzioni in Common Language Runtime.</span><span class="sxs-lookup"><span data-stu-id="a7d74-103">Provides methods to sequentially iterate through a collection of threads in the common language runtime.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="a7d74-104">Metodi</span><span class="sxs-lookup"><span data-stu-id="a7d74-104">Methods</span></span>  
  
|<span data-ttu-id="a7d74-105">Metodo</span><span class="sxs-lookup"><span data-stu-id="a7d74-105">Method</span></span>|<span data-ttu-id="a7d74-106">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a7d74-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="a7d74-107">Metodo Clone</span><span class="sxs-lookup"><span data-stu-id="a7d74-107">Clone Method</span></span>](icorprofilerthreadenum-clone-method.md)|<span data-ttu-id="a7d74-108">Ottiene un puntatore a interfaccia per una copia di questa interfaccia `ICorProfilerThreadEnum`.</span><span class="sxs-lookup"><span data-stu-id="a7d74-108">Gets an interface pointer to a copy of this `ICorProfilerThreadEnum` interface.</span></span>|  
|[<span data-ttu-id="a7d74-109">Metodo GetCount</span><span class="sxs-lookup"><span data-stu-id="a7d74-109">GetCount Method</span></span>](icorprofilerthreadenum-getcount-method.md)|<span data-ttu-id="a7d74-110">Ottiene il numero di thread usati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a7d74-110">Gets the number of threads that are used by the application.</span></span>|  
|[<span data-ttu-id="a7d74-111">Metodo Next</span><span class="sxs-lookup"><span data-stu-id="a7d74-111">Next Method</span></span>](icorprofilerthreadenum-next-method.md)|<span data-ttu-id="a7d74-112">Ottiene il numero specificato di thread contigui da una raccolta sequenziale di moduli, a partire dalla posizione corrente dell'enumeratore nella sequenza.</span><span class="sxs-lookup"><span data-stu-id="a7d74-112">Gets the specified number of contiguous threads from a sequential collection of threads, starting at the enumerator's current position in the sequence.</span></span>|  
|[<span data-ttu-id="a7d74-113">Metodo Reset</span><span class="sxs-lookup"><span data-stu-id="a7d74-113">Reset Method</span></span>](icorprofilerthreadenum-reset-method.md)|<span data-ttu-id="a7d74-114">Sposta il cursore dell'enumeratore nella posizione iniziale della sequenza.</span><span class="sxs-lookup"><span data-stu-id="a7d74-114">Moves the enumerator's cursor to the starting position of the sequence.</span></span>|  
|[<span data-ttu-id="a7d74-115">Metodo Skip</span><span class="sxs-lookup"><span data-stu-id="a7d74-115">Skip Method</span></span>](icorprofilerthreadenum-skip-method.md)|<span data-ttu-id="a7d74-116">Sposta in avanti il cursore dell'enumeratore dalla posizione corrente, in modo che venga ignorato il numero specificato di elementi.</span><span class="sxs-lookup"><span data-stu-id="a7d74-116">Advances the enumerator's cursor from its current position to skip the specified number of elements.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="a7d74-117">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="a7d74-117">Remarks</span></span>  
 <span data-ttu-id="a7d74-118">L'interfaccia `ICorProfilerThreadEnum` è un enumeratore.</span><span class="sxs-lookup"><span data-stu-id="a7d74-118">The `ICorProfilerThreadEnum` interface is an enumerator.</span></span> <span data-ttu-id="a7d74-119">Consente al ricevitore di una matrice di effettuare il pull di elementi dal mittente a una velocità appropriata per il ricevitore.</span><span class="sxs-lookup"><span data-stu-id="a7d74-119">It allows the receiver of an array to pull elements from the sender at a rate that is appropriate for the receiver.</span></span> <span data-ttu-id="a7d74-120">In altre parole, il ricevitore è in grado di controllare in modo esplicito il flusso degli elementi della matrice, evitando così i problemi associati al passaggio di matrici di grandi dimensioni come parametri di metodo.</span><span class="sxs-lookup"><span data-stu-id="a7d74-120">In other words, the receiver is able to explicitly control the flow of array elements, thereby avoiding the problems associated with passing large arrays as method parameters.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a7d74-121">Requisiti</span><span class="sxs-lookup"><span data-stu-id="a7d74-121">Requirements</span></span>  
 <span data-ttu-id="a7d74-122">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a7d74-122">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a7d74-123">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="a7d74-123">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="a7d74-124">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a7d74-124">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a7d74-125">**Versioni .NET Framework:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a7d74-125">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a7d74-126">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a7d74-126">See also</span></span>

- [<span data-ttu-id="a7d74-127">Interfaccia ICorProfilerInfo</span><span class="sxs-lookup"><span data-stu-id="a7d74-127">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)
- [<span data-ttu-id="a7d74-128">Interfacce di profilatura</span><span class="sxs-lookup"><span data-stu-id="a7d74-128">Profiling Interfaces</span></span>](profiling-interfaces.md)

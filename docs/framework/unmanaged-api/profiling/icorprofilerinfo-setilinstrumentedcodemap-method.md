---
title: Metodo ICorProfilerInfo::SetILInstrumentedCodeMap
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.SetILInstrumentedCodeMap
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::SetILInstrumentedCodeMap
helpviewer_keywords:
- ICorProfilerInfo::SetILInstrumentedCodeMap method [.NET Framework profiling]
- SetILInstrumentedCodeMap method [.NET Framework profiling]
ms.assetid: bce1dcf8-b4ec-4e73-a917-f2df1ad49c8a
topic_type:
- apiref
ms.openlocfilehash: cac8e9570dab55af6b6e1fcf6f53b6a697727972
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502912"
---
# <a name="icorprofilerinfosetilinstrumentedcodemap-method"></a><span data-ttu-id="e290a-102">Metodo ICorProfilerInfo::SetILInstrumentedCodeMap</span><span class="sxs-lookup"><span data-stu-id="e290a-102">ICorProfilerInfo::SetILInstrumentedCodeMap Method</span></span>

<span data-ttu-id="e290a-103">Imposta una mappa codice per la funzione specificata utilizzando le voci della mappa MSIL (Microsoft Intermediate Language) specificate.</span><span class="sxs-lookup"><span data-stu-id="e290a-103">Sets a code map for the specified function using the specified Microsoft intermediate language (MSIL) map entries.</span></span>

> [!NOTE]
> <span data-ttu-id="e290a-104">Nel .NET Framework versione 2,0, la chiamata di `SetILInstrumentedCodeMap` su un oggetto `FunctionID` che rappresenta una funzione generica in un particolare dominio applicazione influirà su tutte le istanze di tale funzione nel dominio applicazione.</span><span class="sxs-lookup"><span data-stu-id="e290a-104">In the .NET Framework version 2.0, calling `SetILInstrumentedCodeMap` on a `FunctionID` that represents a generic function in a particular application domain will affect all instances of that function in the application domain.</span></span>

## <a name="syntax"></a><span data-ttu-id="e290a-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="e290a-105">Syntax</span></span>

```cpp
HRESULT SetILInstrumentedCodeMap(
    [in]  FunctionID functionId,
    [in]  BOOL       fStartJit,
    [in]  ULONG      cILMapEntries,
    [in, size_is(cILMapEntries)] COR_IL_MAP rgILMapEntries[]);
```

## <a name="parameters"></a><span data-ttu-id="e290a-106">Parametri</span><span class="sxs-lookup"><span data-stu-id="e290a-106">Parameters</span></span>

`functionId`\
<span data-ttu-id="e290a-107">in ID della funzione per la quale impostare la mappa del codice.</span><span class="sxs-lookup"><span data-stu-id="e290a-107">[in] The ID of the function for which to set the code map.</span></span>

`fStartJit`\
<span data-ttu-id="e290a-108">in Valore booleano che indica se la chiamata al `SetILInstrumentedCodeMap` metodo è la prima per un particolare `FunctionID` .</span><span class="sxs-lookup"><span data-stu-id="e290a-108">[in] A Boolean value that indicates whether the call to the `SetILInstrumentedCodeMap` method is the first for a particular `FunctionID`.</span></span> <span data-ttu-id="e290a-109">Impostare `fStartJit` su `true` nella prima chiamata a `SetILInstrumentedCodeMap` per un oggetto specificato `FunctionID` e su `false` successivamente.</span><span class="sxs-lookup"><span data-stu-id="e290a-109">Set `fStartJit` to `true` in the first call to `SetILInstrumentedCodeMap` for a given `FunctionID`, and to `false` thereafter.</span></span>

`cILMapEntries`\
<span data-ttu-id="e290a-110">in Numero di elementi nella `cILMapEntries` matrice.</span><span class="sxs-lookup"><span data-stu-id="e290a-110">[in] The number of elements in the `cILMapEntries` array.</span></span>

`rgILMapEntries`\
<span data-ttu-id="e290a-111">in Matrice di strutture di COR_IL_MAP, ognuna delle quali specifica un offset MSIL.</span><span class="sxs-lookup"><span data-stu-id="e290a-111">[in] An array of COR_IL_MAP structures, each of which specifies an MSIL offset.</span></span>

## <a name="remarks"></a><span data-ttu-id="e290a-112">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="e290a-112">Remarks</span></span>

<span data-ttu-id="e290a-113">Un profiler spesso inserisce istruzioni all'interno del codice sorgente di un metodo per instrumentare il metodo (ad esempio, per inviare una notifica quando viene raggiunta una determinata riga di codice sorgente).</span><span class="sxs-lookup"><span data-stu-id="e290a-113">A profiler often inserts statements within the source code of a method in order to instrument that method (for example, to notify when a given source line is reached).</span></span> <span data-ttu-id="e290a-114">`SetILInstrumentedCodeMap`consente a un profiler di eseguire il mapping delle istruzioni MSIL originali ai nuovi percorsi.</span><span class="sxs-lookup"><span data-stu-id="e290a-114">`SetILInstrumentedCodeMap` enables a profiler to map the original MSIL instructions to their new locations.</span></span> <span data-ttu-id="e290a-115">Un profiler può usare il metodo [ICorProfilerInfo:: GetILToNativeMapping](icorprofilerinfo-getiltonativemapping-method.md) per ottenere l'offset MSIL originale per un offset nativo specificato.</span><span class="sxs-lookup"><span data-stu-id="e290a-115">A profiler can use the [ICorProfilerInfo::GetILToNativeMapping](icorprofilerinfo-getiltonativemapping-method.md) method to get the original MSIL offset for a given native offset.</span></span>

<span data-ttu-id="e290a-116">Il debugger presuppone che ogni offset precedente faccia riferimento a un offset MSIL all'interno del codice MSIL originale, non modificato e che ogni nuovo offset faccia riferimento all'offset MSIL all'interno del nuovo codice instrumentato.</span><span class="sxs-lookup"><span data-stu-id="e290a-116">The debugger will assume that each old offset refers to an MSIL offset within the original, unmodified MSIL code, and that each new offset refers to the MSIL offset within the new, instrumented code.</span></span> <span data-ttu-id="e290a-117">La mappa deve essere ordinata in ordine crescente.</span><span class="sxs-lookup"><span data-stu-id="e290a-117">The map should be sorted in increasing order.</span></span> <span data-ttu-id="e290a-118">Per il corretto funzionamento, attenersi alle seguenti linee guida:</span><span class="sxs-lookup"><span data-stu-id="e290a-118">For stepping to work properly, follow these guidelines:</span></span>

- <span data-ttu-id="e290a-119">Non riordinare il codice MSIL instrumentato.</span><span class="sxs-lookup"><span data-stu-id="e290a-119">Do not reorder instrumented MSIL code.</span></span>

- <span data-ttu-id="e290a-120">Non rimuovere il codice MSIL originale.</span><span class="sxs-lookup"><span data-stu-id="e290a-120">Do not remove the original MSIL code.</span></span>

- <span data-ttu-id="e290a-121">Includere le voci per tutti i punti di sequenza dal file di database di programma (PDB) nella mappa.</span><span class="sxs-lookup"><span data-stu-id="e290a-121">Include entries for all the sequence points from the program database (PDB) file in the map.</span></span> <span data-ttu-id="e290a-122">La mappa non esegue l'interpolazione delle voci mancanti.</span><span class="sxs-lookup"><span data-stu-id="e290a-122">The map does not interpolate missing entries.</span></span> <span data-ttu-id="e290a-123">Quindi, data la mappa seguente:</span><span class="sxs-lookup"><span data-stu-id="e290a-123">So, given the following map:</span></span>

  <span data-ttu-id="e290a-124">(0 vecchio, 0 nuovo)</span><span class="sxs-lookup"><span data-stu-id="e290a-124">(0 old, 0 new)</span></span>

  <span data-ttu-id="e290a-125">(5 anni, 10 nuovi)</span><span class="sxs-lookup"><span data-stu-id="e290a-125">(5 old, 10 new)</span></span>

  <span data-ttu-id="e290a-126">(9 anni, 20 nuovi)</span><span class="sxs-lookup"><span data-stu-id="e290a-126">(9 old, 20 new)</span></span>

  - <span data-ttu-id="e290a-127">Viene eseguito il mapping di un offset precedente di 0, 1, 2, 3 o 4 al nuovo offset 0.</span><span class="sxs-lookup"><span data-stu-id="e290a-127">An old offset of 0, 1, 2, 3, or 4 will be mapped to new offset 0.</span></span>

  - <span data-ttu-id="e290a-128">Viene eseguito il mapping di un offset precedente di 5, 6, 7 o 8 al nuovo offset 10.</span><span class="sxs-lookup"><span data-stu-id="e290a-128">An old offset of 5, 6, 7, or 8 will be mapped to new offset 10.</span></span>

  - <span data-ttu-id="e290a-129">Verrà eseguito il mapping di un offset precedente di 9 o superiore al nuovo offset 20.</span><span class="sxs-lookup"><span data-stu-id="e290a-129">An old offset of 9 or higher will be mapped to new offset 20.</span></span>

  - <span data-ttu-id="e290a-130">Viene eseguito il mapping di un nuovo offset di 0, 1, 2, 3, 4, 5, 6, 7, 8 o 9 all'offset precedente 0.</span><span class="sxs-lookup"><span data-stu-id="e290a-130">A new offset of 0, 1, 2, 3, 4, 5, 6, 7, 8, or 9 will be mapped to old offset 0.</span></span>

  - <span data-ttu-id="e290a-131">Viene eseguito il mapping di un nuovo offset di 10, 11, 12, 13, 14, 15, 16, 17, 18 o 19 alla precedente offset 5.</span><span class="sxs-lookup"><span data-stu-id="e290a-131">A new offset of 10, 11, 12, 13, 14, 15, 16, 17, 18, or 19 will be mapped to old offset 5.</span></span>

  - <span data-ttu-id="e290a-132">Verrà eseguito il mapping di un nuovo offset di 20 o superiore alla precedente offset 9.</span><span class="sxs-lookup"><span data-stu-id="e290a-132">A new offset of 20 or higher will be mapped to old offset 9.</span></span>

<span data-ttu-id="e290a-133">In .NET Framework 3,5 e versioni precedenti è necessario allocare la `rgILMapEntries` matrice chiamando il metodo [CoTaskMemAlloc](/windows/desktop/api/combaseapi/nf-combaseapi-cotaskmemalloc) .</span><span class="sxs-lookup"><span data-stu-id="e290a-133">In the .NET Framework 3.5 and previous versions, you allocate the `rgILMapEntries` array by calling the [CoTaskMemAlloc](/windows/desktop/api/combaseapi/nf-combaseapi-cotaskmemalloc) method.</span></span> <span data-ttu-id="e290a-134">Poiché il runtime acquisisce la proprietà della memoria, il profiler non deve tentare di liberarlo.</span><span class="sxs-lookup"><span data-stu-id="e290a-134">Because the runtime takes ownership of this memory, the profiler should not attempt to free it.</span></span>

## <a name="requirements"></a><span data-ttu-id="e290a-135">Requisiti</span><span class="sxs-lookup"><span data-stu-id="e290a-135">Requirements</span></span>

<span data-ttu-id="e290a-136">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e290a-136">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>

<span data-ttu-id="e290a-137">**Intestazione:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="e290a-137">**Header:** CorProf.idl, CorProf.h</span></span>

<span data-ttu-id="e290a-138">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e290a-138">**Library:** CorGuids.lib</span></span>

<span data-ttu-id="e290a-139">**Versioni .NET Framework:**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e290a-139">**.NET Framework Versions:** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]</span></span>

## <a name="see-also"></a><span data-ttu-id="e290a-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e290a-140">See also</span></span>

- [<span data-ttu-id="e290a-141">Interfaccia ICorProfilerInfo</span><span class="sxs-lookup"><span data-stu-id="e290a-141">ICorProfilerInfo Interface</span></span>](icorprofilerinfo-interface.md)

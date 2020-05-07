---
title: Metodo ICorDebugCode2::GetCompilerFlags
ms.date: 03/30/2017
api_name:
- ICorDebugCode2.GetCompilerFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode2::GetCompilerFlags
helpviewer_keywords:
- GetCompilerFlags method [.NET Framework debugging]
- ICorDebugCode2::GetCompilerFlags method [.NET Framework debugging]
ms.assetid: 532e9dfd-d114-4c75-b952-1accce102643
topic_type:
- apiref
ms.openlocfilehash: 734a05d96aed309541708d4e6f80ed61cab85637
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82893492"
---
# <a name="icordebugcode2getcompilerflags-method"></a><span data-ttu-id="c03db-102">Metodo ICorDebugCode2::GetCompilerFlags</span><span class="sxs-lookup"><span data-stu-id="c03db-102">ICorDebugCode2::GetCompilerFlags Method</span></span>

<span data-ttu-id="c03db-103">Ottiene i flag che specificano le condizioni in base alle quali l'oggetto di codice è stato compilato o generato JIT usando il generatore di immagini native (Ngen. exe).</span><span class="sxs-lookup"><span data-stu-id="c03db-103">Gets the flags that specify the conditions under which this code object was either just-in-time (JIT) compiled or generated using the native image generator (Ngen.exe).</span></span>

## <a name="syntax"></a><span data-ttu-id="c03db-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="c03db-104">Syntax</span></span>

```cpp
HRESULT GetCompilerFlags (
    [out] DWORD *pdwFlags
);
```

## <a name="parameters"></a><span data-ttu-id="c03db-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="c03db-105">Parameters</span></span>

`pdwFlags`  
<span data-ttu-id="c03db-106">out Puntatore a un valore dell'enumerazione [CorDebugJITCompilerFlags](cordebugjitcompilerflags-enumeration.md) che specifica il comportamento del compilatore JIT o del generatore di immagini native.</span><span class="sxs-lookup"><span data-stu-id="c03db-106">[out] A pointer to a value of the [CorDebugJITCompilerFlags](cordebugjitcompilerflags-enumeration.md) enumeration that specifies the behavior of the JIT compiler or the native image generator.</span></span>

## <a name="requirements"></a><span data-ttu-id="c03db-107">Requisiti</span><span class="sxs-lookup"><span data-stu-id="c03db-107">Requirements</span></span>

<span data-ttu-id="c03db-108">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="c03db-108">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>

<span data-ttu-id="c03db-109">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="c03db-109">**Header:** CorDebug.idl, CorDebug.h</span></span>

<span data-ttu-id="c03db-110">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="c03db-110">**Library:** CorGuids.lib</span></span>

<span data-ttu-id="c03db-111">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c03db-111">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>

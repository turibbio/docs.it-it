---
title: Metodo ICorDebugProcess::GetThread
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.GetThread
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::GetThread
helpviewer_keywords:
- ICorDebugProcess::GetThread method [.NET Framework debugging]
- GetThread method, ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: a48261ed-700b-41c9-8cb4-18c526546603
topic_type:
- apiref
ms.openlocfilehash: 081852f91f243c4a979e2969220e71bd10c8c56b
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212885"
---
# <a name="icordebugprocessgetthread-method"></a><span data-ttu-id="ac0c1-102">Metodo ICorDebugProcess::GetThread</span><span class="sxs-lookup"><span data-stu-id="ac0c1-102">ICorDebugProcess::GetThread Method</span></span>
<span data-ttu-id="ac0c1-103">Ottiene il thread del processo con l'ID del thread del sistema operativo (OS) specificato.</span><span class="sxs-lookup"><span data-stu-id="ac0c1-103">Gets this process's thread that has the specified operating system (OS) thread ID.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ac0c1-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="ac0c1-104">Syntax</span></span>  
  
```cpp  
HRESULT GetThread(  
    [in] DWORD dwThreadId,  
    [out] ICorDebugThread **ppThread);  
```  
  
## <a name="parameters"></a><span data-ttu-id="ac0c1-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="ac0c1-105">Parameters</span></span>  
 `dwThreadId`  
 <span data-ttu-id="ac0c1-106">in ID del thread del sistema operativo del thread da recuperare.</span><span class="sxs-lookup"><span data-stu-id="ac0c1-106">[in] The OS thread ID of the thread to be retrieved.</span></span>  
  
 `ppThread`  
 <span data-ttu-id="ac0c1-107">out Puntatore all'indirizzo di un oggetto ICorDebugThread che rappresenta il thread.</span><span class="sxs-lookup"><span data-stu-id="ac0c1-107">[out] A pointer to the address of an ICorDebugThread object that represents the thread.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ac0c1-108">Requisiti</span><span class="sxs-lookup"><span data-stu-id="ac0c1-108">Requirements</span></span>  
 <span data-ttu-id="ac0c1-109">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ac0c1-109">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ac0c1-110">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="ac0c1-110">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="ac0c1-111">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="ac0c1-111">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="ac0c1-112">**Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ac0c1-112">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>

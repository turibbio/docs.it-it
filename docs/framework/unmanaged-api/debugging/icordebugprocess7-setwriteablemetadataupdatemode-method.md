---
title: Metodo ICorDebugProcess7::SetWriteableMetadataUpdateMode
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugProcess7.SetWriteableMetadataUpdateMode
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 8589bba7-7304-45ba-9e31-7bf43dfd5c19
topic_type:
- apiref
ms.openlocfilehash: 6de75e1e27660ac91bd6320a501db47f3b055fb0
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212256"
---
# <a name="icordebugprocess7setwriteablemetadataupdatemode-method"></a><span data-ttu-id="fd8e4-102">Metodo ICorDebugProcess7::SetWriteableMetadataUpdateMode</span><span class="sxs-lookup"><span data-stu-id="fd8e4-102">ICorDebugProcess7::SetWriteableMetadataUpdateMode Method</span></span>
<span data-ttu-id="fd8e4-103">[Supportato in .NET Framework 4.5.2 e versioni successive]</span><span class="sxs-lookup"><span data-stu-id="fd8e4-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="fd8e4-104">Configura come il debugger gestisce gli aggiornamenti in memoria ai metadati all'interno del processo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="fd8e4-104">Configures how the debugger handles in-memory updates to metadata within the target process.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fd8e4-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="fd8e4-105">Syntax</span></span>  
  
```cpp
HRESULT SetWriteableMetadataUpdateMode(  
   WriteableMetadataUpdateMode flags  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="fd8e4-106">Parametri</span><span class="sxs-lookup"><span data-stu-id="fd8e4-106">Parameters</span></span>  
 `flags`  
 <span data-ttu-id="fd8e4-107">Valore di enumerazione [WriteableMetadataUpdateMode](writeablemetadataupdatemode-enumeration.md) che specifica se gli aggiornamenti in memoria ai metadati nel processo di destinazione sono visibili ( `WriteableMetadataUpdateMode::AlwaysShowUpdates` ) o non sono visibili ( `WriteableMetadataUpdateMode::LegacyCompatPolicy` ) al debugger.</span><span class="sxs-lookup"><span data-stu-id="fd8e4-107">A [WriteableMetadataUpdateMode](writeablemetadataupdatemode-enumeration.md) enumeration value that specifies whether in-memory updates to metadata in the target process are visible (`WriteableMetadataUpdateMode::AlwaysShowUpdates`) or not visible (`WriteableMetadataUpdateMode::LegacyCompatPolicy`) to the debugger.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="fd8e4-108">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="fd8e4-108">Remarks</span></span>  
 <span data-ttu-id="fd8e4-109">Gli aggiornamenti ai metadati del processo di destinazione possono provenire dalle opzioni di Modifica e continuazione, da un profiler o da <xref:System.Reflection.Emit?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="fd8e4-109">Updates to the metadata of the target process can come from Edit and Continue, a profiler, or <xref:System.Reflection.Emit?displayProperty=nameWithType>.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="fd8e4-110">Requisiti</span><span class="sxs-lookup"><span data-stu-id="fd8e4-110">Requirements</span></span>  
 <span data-ttu-id="fd8e4-111">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="fd8e4-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="fd8e4-112">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="fd8e4-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="fd8e4-113">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="fd8e4-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="fd8e4-114">**Versioni .NET Framework:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="fd8e4-114">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fd8e4-115">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="fd8e4-115">See also</span></span>

- [<span data-ttu-id="fd8e4-116">Interfaccia ICorDebugProcess7</span><span class="sxs-lookup"><span data-stu-id="fd8e4-116">ICorDebugProcess7 Interface</span></span>](icordebugprocess7-interface.md)
- [<span data-ttu-id="fd8e4-117">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="fd8e4-117">Debugging Interfaces</span></span>](debugging-interfaces.md)

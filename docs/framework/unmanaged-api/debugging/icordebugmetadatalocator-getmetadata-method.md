---
title: Metodo ICorDebugMetaDataLocator::GetMetaData
ms.date: 03/30/2017
api_name:
- ICorDebugMetaDataLocator.GetMetaData
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMetaDataLocator::GetMetaData
helpviewer_keywords:
- ICorDebugMetaDataLocator::GetMetaData method [.NET Framework debugging]
- GetMetaData method, ICorDebugMetaDataLocator interface [.NET Framework debugging]
ms.assetid: f9b0ff22-54db-45eb-9cc3-508000a3141d
topic_type:
- apiref
ms.openlocfilehash: d9269339e8e2ae8d00da701b015aa30cd51cbef3
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213374"
---
# <a name="icordebugmetadatalocatorgetmetadata-method"></a><span data-ttu-id="39f66-102">Metodo ICorDebugMetaDataLocator::GetMetaData</span><span class="sxs-lookup"><span data-stu-id="39f66-102">ICorDebugMetaDataLocator::GetMetaData Method</span></span>
<span data-ttu-id="39f66-103">Chiede al debugger di restituire il percorso completo di un modulo i cui metadati sono necessari per completare un'operazione richiesta dal debugger.</span><span class="sxs-lookup"><span data-stu-id="39f66-103">Asks the debugger to return the full path to a module whose metadata is needed to complete an operation the debugger requested.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="39f66-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="39f66-104">Syntax</span></span>  
  
```cpp  
HRESULT GetMetaData(  
      [in] LPCWSTR wszImagePath,  
      [in] DWORD   dwImageTimeStamp,  
      [in] DWORD   dwImageSize,  
      [in] ULONG32 cchPathBuffer,  
      [out] ULONG32 * pcchPathBuffer,  
      [out, size_is(cchPathBuffer), length_is(*pcchPathBuffer)]  
               WCHAR wszPathBuffer[]  
      );  
```  
  
## <a name="parameters"></a><span data-ttu-id="39f66-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="39f66-105">Parameters</span></span>  
 `wszImagePath`  
 <span data-ttu-id="39f66-106">[in] Stringa con terminazione null che rappresenta il percorso completo del file.</span><span class="sxs-lookup"><span data-stu-id="39f66-106">[in] A null-terminated string that represents the full path to the file.</span></span> <span data-ttu-id="39f66-107">Se il percorso completo non è disponibile, il nome e l'estensione del file (*nomefile*.\* estensione\*).</span><span class="sxs-lookup"><span data-stu-id="39f66-107">If the full path is not available, the name and extension of the file (*filename*.*extension*).</span></span>  
  
 `dwImageTimeStamp`  
 <span data-ttu-id="39f66-108">[in] Timestamp dalle intestazioni del file PE dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="39f66-108">[in] The time stamp from the image's PE file headers.</span></span> <span data-ttu-id="39f66-109">Questo parametro può essere potenzialmente utilizzato per la ricerca di un server di simboli ([symsrv](/windows/desktop/debug/using-symsrv)).</span><span class="sxs-lookup"><span data-stu-id="39f66-109">This parameter can potentially be used for a symbol server ([SymSrv](/windows/desktop/debug/using-symsrv)) lookup.</span></span>  
  
 `dwImageSize`  
 <span data-ttu-id="39f66-110">[in] Dimensioni dell'immagine dalle intestazioni del file PE.</span><span class="sxs-lookup"><span data-stu-id="39f66-110">[in] The image size from PE file headers.</span></span> <span data-ttu-id="39f66-111">Questo parametro può essere potenzialmente usato per una ricerca in SymSrv.</span><span class="sxs-lookup"><span data-stu-id="39f66-111">This parameter can potentially be used for a SymSrv lookup.</span></span>  
  
 `cchPathBuffer`  
 <span data-ttu-id="39f66-112">[in] Numero di caratteri in `wszPathBuffer`.</span><span class="sxs-lookup"><span data-stu-id="39f66-112">[in] The character count in `wszPathBuffer`.</span></span>  
  
 `pcchPathBuffer`  
 <span data-ttu-id="39f66-113">[out] Numero di `WCHAR` scritto in `wszPathBuffer`.</span><span class="sxs-lookup"><span data-stu-id="39f66-113">[out] The count of `WCHAR`s written to `wszPathBuffer`.</span></span>  
  
 <span data-ttu-id="39f66-114">Se il metodo restituisce E_NOT_SUFFICIENT_BUFFER, contiene il numero di `WCHAR` necessario per archiviare il percorso.</span><span class="sxs-lookup"><span data-stu-id="39f66-114">If the method returns E_NOT_SUFFICIENT_BUFFER, contains the count of `WCHAR`s needed to store the path.</span></span>  
  
 `wszPathBuffer`  
 <span data-ttu-id="39f66-115">[out] Puntatore a un buffer in cui il debugger copierà il percorso completo del file che contiene i metadati richiesti.</span><span class="sxs-lookup"><span data-stu-id="39f66-115">[out] Pointer to a buffer into which the debugger will copy the full path of the file that contains the requested metadata.</span></span>  
  
 <span data-ttu-id="39f66-116">Il `ofReadOnly` flag dell'enumerazione [CorOpenFlags](../metadata/coropenflags-enumeration.md) viene usato per richiedere l'accesso in sola lettura ai metadati in questo file.</span><span class="sxs-lookup"><span data-stu-id="39f66-116">The `ofReadOnly` flag from the [CorOpenFlags](../metadata/coropenflags-enumeration.md) enumeration is used to request read-only access to the metadata in this file.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="39f66-117">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="39f66-117">Return Value</span></span>  
 <span data-ttu-id="39f66-118">Questo metodo restituisce gli specifici HRESULT seguenti, nonché gli errori di HRESULT che indicano la mancata riuscita del metodo.</span><span class="sxs-lookup"><span data-stu-id="39f66-118">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span> <span data-ttu-id="39f66-119">Tutti gli altri HRESULT di errore indicano che il file non è recuperabile.</span><span class="sxs-lookup"><span data-stu-id="39f66-119">All other failure HRESULTs indicate that the file is not retrievable.</span></span>  
  
|<span data-ttu-id="39f66-120">HRESULT</span><span class="sxs-lookup"><span data-stu-id="39f66-120">HRESULT</span></span>|<span data-ttu-id="39f66-121">Description</span><span class="sxs-lookup"><span data-stu-id="39f66-121">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="39f66-122">S_OK</span><span class="sxs-lookup"><span data-stu-id="39f66-122">S_OK</span></span>|<span data-ttu-id="39f66-123">Metodo completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="39f66-123">The method completed successfully.</span></span> <span data-ttu-id="39f66-124">`wszPathBuffer` contiene il percorso completo del file ed è con terminazione null.</span><span class="sxs-lookup"><span data-stu-id="39f66-124">`wszPathBuffer` contains the full path to the file and is null-terminated.</span></span>|  
|<span data-ttu-id="39f66-125">E_NOT_SUFFICIENT_BUFFER</span><span class="sxs-lookup"><span data-stu-id="39f66-125">E_NOT_SUFFICIENT_BUFFER</span></span>|<span data-ttu-id="39f66-126">Le dimensioni correnti di `wszPathBuffer` non sono sufficienti a contenere il percorso completo.</span><span class="sxs-lookup"><span data-stu-id="39f66-126">The current size of `wszPathBuffer` is not sufficient to hold the full path.</span></span> <span data-ttu-id="39f66-127">In questo caso, `pcchPathBuffer` contiene il numero necessario di `WCHAR`s, incluso il carattere di terminazione null e `GetMetaData` viene chiamato una seconda volta con le dimensioni del buffer richiesto.</span><span class="sxs-lookup"><span data-stu-id="39f66-127">In this case, `pcchPathBuffer` contains the needed count of `WCHAR`s, including the terminating null character, and `GetMetaData` is called a second time with the requested buffer size.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="39f66-128">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="39f66-128">Remarks</span></span>  
 <span data-ttu-id="39f66-129">Se `wszImagePath` contiene un percorso completo di un modulo da un dump, specifica il percorso dal computer in cui è stato recuperato il dump.</span><span class="sxs-lookup"><span data-stu-id="39f66-129">If `wszImagePath` contains a full path for a module from a dump, it specifies the path from the computer where the dump was collected.</span></span> <span data-ttu-id="39f66-130">Il file può non esistere in questa posizione oppure un file errato con lo stesso nome può essere archiviato nel percorso.</span><span class="sxs-lookup"><span data-stu-id="39f66-130">The file may not exist at this location, or an incorrect file with the same name may be stored on the path.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="39f66-131">Requisiti</span><span class="sxs-lookup"><span data-stu-id="39f66-131">Requirements</span></span>  
 <span data-ttu-id="39f66-132">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="39f66-132">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="39f66-133">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="39f66-133">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="39f66-134">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="39f66-134">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="39f66-135">**Versioni .NET Framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="39f66-135">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="39f66-136">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="39f66-136">See also</span></span>

- [<span data-ttu-id="39f66-137">Interfaccia ICorDebugThread4</span><span class="sxs-lookup"><span data-stu-id="39f66-137">ICorDebugThread4 Interface</span></span>](icordebugthread4-interface.md)
- [<span data-ttu-id="39f66-138">Interfacce di debug</span><span class="sxs-lookup"><span data-stu-id="39f66-138">Debugging Interfaces</span></span>](debugging-interfaces.md)
- [<span data-ttu-id="39f66-139">Debug</span><span class="sxs-lookup"><span data-stu-id="39f66-139">Debugging</span></span>](index.md)

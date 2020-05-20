---
title: Metodo ISymUnmanagedReader::GetSymbolStoreFileName
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetSymbolStoreFileName
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetSymbolStoreFileName
helpviewer_keywords:
- GetSymbolStoreFileName method [.NET Framework debugging]
- ISymUnmanagedReader::GetSymbolStoreFileName method [.NET Framework debugging]
ms.assetid: c84f4846-9bc8-44a4-9a76-e39106d6d8b2
topic_type:
- apiref
ms.openlocfilehash: 6ffab3b2f81680404f870cfd63ae5125173a346c
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615514"
---
# <a name="isymunmanagedreadergetsymbolstorefilename-method"></a><span data-ttu-id="ef107-102">Metodo ISymUnmanagedReader::GetSymbolStoreFileName</span><span class="sxs-lookup"><span data-stu-id="ef107-102">ISymUnmanagedReader::GetSymbolStoreFileName Method</span></span>
<span data-ttu-id="ef107-103">Fornisce il nome file su disco dell'archivio dei simboli.</span><span class="sxs-lookup"><span data-stu-id="ef107-103">Provides the on-disk file name of the symbol store.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ef107-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="ef107-104">Syntax</span></span>  
  
```cpp  
HRESULT GetSymbolStoreFileName (  
    [in]  ULONG32 cchName,  
    [out] ULONG32 *pcchName,  
    [out, size_is (cchName),  
        length_is (*pcchName)] WCHAR szName[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="ef107-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="ef107-105">Parameters</span></span>  
 `cchName`  
 <span data-ttu-id="ef107-106">in Dimensioni del `szName` buffer.</span><span class="sxs-lookup"><span data-stu-id="ef107-106">[in] The size of the `szName` buffer.</span></span>  
  
 `pcchName`  
 <span data-ttu-id="ef107-107">out Puntatore alla variabile che riceve la lunghezza del nome restituito in `szName` , inclusa la terminazione null.</span><span class="sxs-lookup"><span data-stu-id="ef107-107">[out] A pointer to the variable that receives the length of the name returned in `szName`, including the null termination.</span></span>  
  
 `szName`  
 <span data-ttu-id="ef107-108">out Puntatore alla variabile che riceve il nome file dell'archivio dei simboli.</span><span class="sxs-lookup"><span data-stu-id="ef107-108">[out] A pointer to the variable that receives the file name of the symbol store.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="ef107-109">Valore restituito</span><span class="sxs-lookup"><span data-stu-id="ef107-109">Return Value</span></span>  
 <span data-ttu-id="ef107-110">S_OK se il metodo ha esito positivo; in caso contrario, E_FAIL o un altro codice di errore.</span><span class="sxs-lookup"><span data-stu-id="ef107-110">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ef107-111">Requisiti</span><span class="sxs-lookup"><span data-stu-id="ef107-111">Requirements</span></span>  
 <span data-ttu-id="ef107-112">**Intestazione:** CorSym. idl, CorSym. h</span><span class="sxs-lookup"><span data-stu-id="ef107-112">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ef107-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ef107-113">See also</span></span>

- [<span data-ttu-id="ef107-114">Interfaccia ISymUnmanagedReader</span><span class="sxs-lookup"><span data-stu-id="ef107-114">ISymUnmanagedReader Interface</span></span>](isymunmanagedreader-interface.md)

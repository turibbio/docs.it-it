---
title: Funzione CreateCoreClrDebugTarget
ms.date: 03/30/2017
api_name:
- CreateCorClrDebugTarget
api_location:
- mscordbi_macx86.dll
api_type:
- COM
f1_keywords:
- CreateCoreClrDebugTarget
helpviewer_keywords:
- remote debugging API [Silverlight]
- Silverlight, remote debugging
- CreateCoreClrDebugTarget function
ms.assetid: 1cf4ca8e-d9bb-4633-9adf-5e24315bf87a
topic_type:
- apiref
ms.openlocfilehash: 2271611b5cbbfe487e5798be0429ed94c227a67f
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860878"
---
# <a name="createcoreclrdebugtarget-function"></a>Funzione CreateCoreClrDebugTarget
Crea una connessione a un proxy del debugger in esecuzione su un computer remoto e restituisce un oggetto [ICoreClrDebugTarget](icoreclrdebugtarget-interface.md) che può essere usato per eseguire query sui processi in esecuzione e sui runtime caricati nel computer remoto.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT CreateCoreClrDebugTarget (  
       [in]  DWORD    dwAddress,
       [out] ICoreClrDebugTarget**     ppTarget  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `dwAddress`  
 [in] Indirizzo IPv4 di un computer di destinazione remoto.  
  
 `ppTarget`  
 out Puntatore a un puntatore a un oggetto [ICoreClrDebugTarget](icoreclrdebugtarget-interface.md) che verrà creato.  
  
## <a name="return-value"></a>Valore restituito  
 S_OK  
 Il numero di CLR nel processo è stato determinato correttamente e le matrici di percorsi e di handle corrispondenti sono state riempite correttamente.  
  
 E_OUTOFMEMORY  
 Non è possibile allocare memoria sufficiente per `ppTarget`.  
  
 E_FAIL (o altri codici E_ restituiti)  
 Altri errori.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CoreClrRemoteDebuggingInterfaces. h  
  
 **Libreria:** mscordbi_macx86. dll  
  
 **Versioni .NET Framework:** 3,5 SP1

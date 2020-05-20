---
title: Interfaccia ISymUnmanagedBinder3
ms.date: 03/30/2017
api_name:
- ISymUnmanagedBinder3
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedBinder3 Interface
helpviewer_keywords:
- ISymUnmanagedBinder3 interface [.NET Framework debugging]
ms.assetid: 37527a84-4b03-4f08-8135-94d898599089
topic_type:
- apiref
ms.openlocfilehash: 5a26de2a8f5439b7c81560927c991d449e57b76c
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441591"
---
# <a name="isymunmanagedbinder3-interface"></a>Interfaccia ISymUnmanagedBinder3
Estende l'interfaccia del gestore di associazione dei simboli. Ottenere questa interfaccia chiamando `QueryInterface` su un oggetto che implementa l' `ISymUnmanagedBinder` interfaccia.  
  
> [!IMPORTANT]
> L'apertura di un file di database di programma (PDB) da un'origine non attendibile costituisce un rischio per la sicurezza.  
  
## <a name="methods"></a>Metodi  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[Metodo GetReaderFromCallback](isymunmanagedbinder3-getreaderfromcallback-method.md)|Consente all'utente di implementare o fornire tramite callback o `IID_IDiaReadExeAtRVACallback` `IID_IDiaReadExeAtOffsetCallback` per ottenere le informazioni della directory di debug dalla memoria|  
  
## <a name="requirements"></a>Requisiti  
 **Intestazione:** CorSym. idl, CorSym. h  
  
## <a name="see-also"></a>Vedere anche

- [Interfacce dell'archivio dei simboli di diagnostica](diagnostics-symbol-store-interfaces.md)
- [Interfaccia ISymUnmanagedBinder](isymunmanagedbinder-interface.md)
- [Interfaccia ISymUnmanagedBinder2](isymunmanagedbinder2-interface.md)

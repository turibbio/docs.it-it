---
title: Interfaccia IHostSecurityContext
ms.date: 03/30/2017
api_name:
- IHostSecurityContext
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityContext
helpviewer_keywords:
- IHostSecurityContext interface [.NET Framework hosting]
ms.assetid: 88e2eac0-8ccb-404f-abbc-287d55159842
topic_type:
- apiref
ms.openlocfilehash: f6e25bfe11880730f6f447ccc0406d716d185624
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501495"
---
# <a name="ihostsecuritycontext-interface"></a>Interfaccia IHostSecurityContext
Consente all'Common Language Runtime (CLR) di mantenere le informazioni sul contesto di sicurezza implementate dall'host.  
  
## <a name="methods"></a>Metodi  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[Metodo Capture](ihostsecuritycontext-capture-method.md)|Ottiene un clone dell' `IHostSecurityContext` istanza di restituita da una chiamata a [IHostSecurityManager:: GetSecurityContext](ihostsecuritymanager-getsecuritycontext-method.md).|  
  
## <a name="remarks"></a>Osservazioni  
 Un host può controllare l'accesso al codice a token di thread sia dal codice CLR che dal codice utente. Può inoltre garantire che le informazioni complete sul contesto di sicurezza vengano passate tra le operazioni asincrone o i punti di codice con accesso limitato al codice. `IHostSecurityContext`Incapsula le informazioni sul contesto di sicurezza, che è opaco per il Runtime. Il runtime acquisisce queste informazioni usando `Capture` e le sposta tra la distribuzione degli elementi di lavoro del pool di thread, l'esecuzione del finalizzatore e i costruttori di moduli e classi.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** MSCorEE. h  
  
 **Libreria:** Incluso come risorsa in MSCorEE. dll  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfaccia ICLRHostProtectionManager](iclrhostprotectionmanager-interface.md)
- [Interfaccia IHostSecurityManager](ihostsecuritymanager-interface.md)
- [Interfacce di hosting](hosting-interfaces.md)

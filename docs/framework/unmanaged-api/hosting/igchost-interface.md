---
title: Interfaccia IGCHost
ms.date: 03/30/2017
api_name:
- IGCHost
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IGCHost
helpviewer_keywords:
- IGCHost interface [.NET Framework hosting]
ms.assetid: 9ad70ffd-6963-4ab2-8c84-3d86c3fb8deb
topic_type:
- apiref
ms.openlocfilehash: 6b6f2dbaa49c29f6614e9c39a3f408d4d1453983
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501625"
---
# <a name="igchost-interface"></a>Interfaccia IGCHost
Fornisce metodi per ottenere informazioni sul sistema Garbage Collection e per controllare alcuni aspetti di Garbage Collection.  
  
> [!NOTE]
> A partire da .NET Framework 4,5, è possibile usare il metodo [IGCHost2:: SetGCStartupLimitsEx](igchost2-setgcstartuplimitsex-method.md) per impostare le dimensioni di un segmento di Garbage Collection e le dimensioni massime della generazione 0 del sistema di Garbage Collection su valori maggiori del `DWORD` limite imposto dal metodo [SetGCStartupLimits](igchost-setgcstartuplimits-method.md) .  
  
> [!NOTE]
> Questa interfaccia è solo per uso esperto. Può influire sulle prestazioni di un'applicazione se utilizzata in modo errato.  
  
## <a name="methods"></a>Metodi  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[Metodo Collect](igchost-collect-method.md)|Impone l'esecuzione di una raccolta per la generazione specificata, indipendentemente dallo stato della Garbage Collection corrente.|  
|[Metodo GetStats](igchost-getstats-method.md)|Ottiene le statistiche per lo stato corrente del sistema di Garbage Collection.|  
|[Metodo GetThreadStats](igchost-getthreadstats-method.md)|Ottiene le statistiche per thread per Garbage Collection.|  
|[Metodo SetGCStartupLimits](igchost-setgcstartuplimits-method.md)|Imposta le dimensioni del segmento e le dimensioni massime per la generazione 0.|  
|[Metodo SetVirtualMemLimit](igchost-setvirtualmemlimit-method.md)|Imposta la dimensione massima della memoria virtuale del runtime.|  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** GCHost. idl, GCHost. h  
  
 **Libreria:** Incluso come risorsa in MSCorEE. dll  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfacce di hosting](hosting-interfaces.md)
- [Coclasse CorRuntimeHost](corruntimehost-coclass.md)

---
title: Metodo EmitInternalExportedTypes
ms.date: 03/30/2017
api_name:
- EmitInternalExportedTypes
- IALink2.EmitInternalExportedTypes
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- EmitInternalExportedTypes
helpviewer_keywords:
- EmitInternalExportedTypes method
ms.assetid: 28c8b00d-2c14-40b4-aed5-a1db0e2428eb
topic_type:
- apiref
ms.openlocfilehash: d4b7064b0339825c29e4001bc35c4a604098468a
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2019
ms.locfileid: "74446502"
---
# <a name="emitinternalexportedtypes-method"></a>Metodo EmitInternalExportedTypes
Genera tipi aggiunti all'assembly. Chiamare questo metodo dopo che sono stati aggiunti tipi interni noti.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT EmitInternalExportedTypes(  
    mdAssembly AssemblyID  
) PURE;  
```  
  
## <a name="parameters"></a>Parametri  
 `AssemblyID`  
 ID dell'assembly.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce S_OK se il metodo ha esito positivo.  
  
## <a name="requirements"></a>Requisiti  
 Richiede ALink. h  
  
## <a name="see-also"></a>Vedere anche

- [Interfaccia IALink2](ialink2-interface.md)
- [Interfaccia IALink](ialink-interface.md)
- [Alink (API)](index.md)

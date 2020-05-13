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
# <a name="icordebugprocess7setwriteablemetadataupdatemode-method"></a>Metodo ICorDebugProcess7::SetWriteableMetadataUpdateMode
[Supportato in .NET Framework 4.5.2 e versioni successive]  
  
 Configura come il debugger gestisce gli aggiornamenti in memoria ai metadati all'interno del processo di destinazione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
HRESULT SetWriteableMetadataUpdateMode(  
   WriteableMetadataUpdateMode flags  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `flags`  
 Valore di enumerazione [WriteableMetadataUpdateMode](writeablemetadataupdatemode-enumeration.md) che specifica se gli aggiornamenti in memoria ai metadati nel processo di destinazione sono visibili ( `WriteableMetadataUpdateMode::AlwaysShowUpdates` ) o non sono visibili ( `WriteableMetadataUpdateMode::LegacyCompatPolicy` ) al debugger.  
  
## <a name="remarks"></a>Osservazioni  
 Gli aggiornamenti ai metadati del processo di destinazione possono provenire dalle opzioni di Modifica e continuazione, da un profiler o da <xref:System.Reflection.Emit?displayProperty=nameWithType>.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, CorDebug.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfaccia ICorDebugProcess7](icordebugprocess7-interface.md)
- [Interfacce di debug](debugging-interfaces.md)

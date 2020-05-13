---
title: Metodo ICorDebugMutableDataTarget::WriteVirtual
ms.date: 03/30/2017
ms.assetid: 80833648-58a7-491a-8dc8-9a48e9bb3adc
ms.openlocfilehash: 6325dba99fba0ab5e2f752a0635fdd428d3065eb
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83206747"
---
# <a name="icordebugmutabledatatargetwritevirtual-method"></a>Metodo ICorDebugMutableDataTarget::WriteVirtual
Scrive dalla memoria nello spazio degli indirizzi del processo di destinazione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT WriteVirtual(  
   [in] CORDB_ADDRESS address,  
   [in, size_is(bytesRequested)] const BYTE * pBuffer,  
   [in] ULONG32 bytesRequested);  
```  
  
## <a name="parameters"></a>Parametri  
 `address`  
 [in] Indirizzo in cui scrivere il contenuto di `pBuffer`.  
  
 `pBuffer`  
 [in] Puntatore a una matrice di byte che contiene i byte da scrivere.  
  
 `address`  
 [in] Numero di byte in `pBuffer`.  
  
## <a name="return-value"></a>Valore restituito  
 `S_OK` in caso di esito positivo o qualsiasi altro `HRESULT` in caso di errore.  
  
## <a name="remarks"></a>Osservazioni  
 Se non è possibile scrivere dei byte, la chiamata al metodo non riesce e non modifica i byte nello spazio degli indirizzi di destinazione (altrimenti la destinazione potrebbe trovarsi in uno stato incoerente che renderebbe il debug successivo inaffidabile).  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, CorDebug.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni .NET Framework:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfaccia ICorDebugMutableDataTarget](icordebugmutabledatatarget-interface.md)
- [Interfacce di debug](debugging-interfaces.md)

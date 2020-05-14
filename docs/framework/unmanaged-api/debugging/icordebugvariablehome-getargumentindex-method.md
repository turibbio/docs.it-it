---
title: 'Metodo ICorDebugVariableHome:: GetArgumentIndex'
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHome.GetArgumentIndex
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHome::GetArgumentIndex
helpviewer_keywords:
- ICorDebugVariableHome::GetArgumentIndex method [.NET Framework debugging]
- GetArgumentIndex method, ICorDebugVariableHome interface [.NET Framework debugging]
ms.assetid: e86fcc72-388d-4009-ab21-8f9c3323e9a3
topic_type:
- apiref
ms.openlocfilehash: 27a676fd1d2d7903943e44f8a7201b88af4fba89
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2020
ms.locfileid: "83397003"
---
# <a name="icordebugvariablehomegetargumentindex-method"></a>Metodo ICorDebugVariableHome:: GetArgumentIndex

Ottiene l'indice di un argomento della funzione.

## <a name="syntax"></a>Sintassi

```cpp
HRESULT GetArgumentIndex(
    [out] ULONG32* pArgumentIndex
);
```

## <a name="parameters"></a>Parametri

`pArgumentIndex`\
out Puntatore all'indice dell'argomento.

## <a name="return-value"></a>Valore restituito

Il metodo restituisce i valori seguenti.

|Valore|Descrizione|
|-----------|-----------------|
|`S_OK`|La chiamata al metodo ha restituito un indice di argomento valido.|
|`E_FAIL`|L'istanza corrente di [ICorDebugVariableHome](icordebugvariablehome-interface.md) rappresenta una variabile locale.|

## <a name="remarks"></a>Commenti

L'indice dell'argomento può essere utilizzato per recuperare i metadati per questo argomento.

## <a name="requirements"></a>Requisiti

**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).

**Intestazione:** CorDebug.idl, CorDebug.h

**Libreria:** CorGuids.lib

**Versioni .NET Framework:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]

## <a name="see-also"></a>Vedi anche

- [Interfaccia ICorDebugVariableHome](icordebugvariablehome-interface.md)

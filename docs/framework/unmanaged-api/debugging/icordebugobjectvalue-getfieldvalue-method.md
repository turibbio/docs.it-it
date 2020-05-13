---
title: Metodo ICorDebugObjectValue::GetFieldValue
ms.date: 03/30/2017
api_name:
- ICorDebugObjectValue.GetFieldValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugObjectValue::GetFieldValue
helpviewer_keywords:
- ICorDebugObjectValue::GetFieldValue method [.NET Framework debugging]
- GetFieldValue method [.NET Framework debugging]
ms.assetid: c96770b0-3e09-47bb-bd29-20353b043459
topic_type:
- apiref
ms.openlocfilehash: 660bc13e8109994f59444c0adebbc97f54de0b43
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207583"
---
# <a name="icordebugobjectvaluegetfieldvalue-method"></a><span data-ttu-id="5969c-102">Metodo ICorDebugObjectValue::GetFieldValue</span><span class="sxs-lookup"><span data-stu-id="5969c-102">ICorDebugObjectValue::GetFieldValue Method</span></span>
<span data-ttu-id="5969c-103">Ottiene il valore del campo specificato della classe specificata per il valore dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="5969c-103">Gets the value of the specified field of the specified class for this object value.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5969c-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="5969c-104">Syntax</span></span>  
  
```cpp  
HRESULT GetFieldValue (  
    [in]  ICorDebugClass     *pClass,  
    [in]  mdFieldDef         fieldDef,  
    [out] ICorDebugValue     **ppValue  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="5969c-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="5969c-105">Parameters</span></span>  
 `pClass`  
 <span data-ttu-id="5969c-106">in Puntatore a un oggetto "ICorDebugClass" che rappresenta la classe per la quale ottenere il valore del campo.</span><span class="sxs-lookup"><span data-stu-id="5969c-106">[in] A pointer to an "ICorDebugClass" object that represents the class for which to get the field value.</span></span>  
  
 `fieldDef`  
 <span data-ttu-id="5969c-107">in `mdFieldDef`Token che fa riferimento ai metadati che descrivono il campo.</span><span class="sxs-lookup"><span data-stu-id="5969c-107">[in] An `mdFieldDef` token that references the metadata describing the field.</span></span>  
  
 `ppValue`  
 <span data-ttu-id="5969c-108">out Puntatore a un oggetto "ICorDebugValue" che rappresenta il valore del campo specificato.</span><span class="sxs-lookup"><span data-stu-id="5969c-108">[out] A pointer to an "ICorDebugValue" object that represents the value of the specified field.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="5969c-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="5969c-109">Remarks</span></span>  
 <span data-ttu-id="5969c-110">La classe, specificata nel `pClass` parametro, deve trovarsi nella gerarchia della classe del valore dell'oggetto e il campo deve essere un campo di tale classe.</span><span class="sxs-lookup"><span data-stu-id="5969c-110">The class, specified in the `pClass` parameter, must be in the hierarchy of the object value's class, and the field must be a field of that class.</span></span>  
  
 <span data-ttu-id="5969c-111">Il `GetFieldValue` metodo avrà comunque esito positivo per gli oggetti generici e le classi generiche.</span><span class="sxs-lookup"><span data-stu-id="5969c-111">The `GetFieldValue` method will still succeed for generic objects and generic classes.</span></span> <span data-ttu-id="5969c-112">Se, ad esempio, \< il> di dizionario v eredita dalla stringa del dizionario \< , v> e il valore dell'oggetto è di tipo dizionario \< Int32>, il passaggio dell' `ICorDebugClass` oggetto per il dizionario \< K, v> otterrà correttamente un campo di stringa del dizionario \< , Int32>.</span><span class="sxs-lookup"><span data-stu-id="5969c-112">For example, if MyDictionary\<V> inherits from Dictionary\<string,V>, and the object value is of type MyDictionary\<int32>, passing the `ICorDebugClass` object for Dictionary\<K,V> will successfully get a field of Dictionary\<string,int32>.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="5969c-113">Requisiti</span><span class="sxs-lookup"><span data-stu-id="5969c-113">Requirements</span></span>  
 <span data-ttu-id="5969c-114">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="5969c-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5969c-115">**Intestazione:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="5969c-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="5969c-116">**Libreria:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="5969c-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="5969c-117">**Versioni .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="5969c-117">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5969c-118">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5969c-118">See also</span></span>

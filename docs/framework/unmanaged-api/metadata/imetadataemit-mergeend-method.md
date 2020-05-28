---
title: Metodo IMetaDataEmit::MergeEnd
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.MergeEnd
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::MergeEnd
helpviewer_keywords:
- MergeEnd method [.NET Framework metadata]
- IMetaDataEmit::MergeEnd method [.NET Framework metadata]
ms.assetid: 2d64315a-1af1-4c60-aedf-f8a781914aea
topic_type:
- apiref
ms.openlocfilehash: feb81b86190f953b50f43f244f4e58a0a482f86e
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84003919"
---
# <a name="imetadataemitmergeend-method"></a><span data-ttu-id="85003-102">Metodo IMetaDataEmit::MergeEnd</span><span class="sxs-lookup"><span data-stu-id="85003-102">IMetaDataEmit::MergeEnd Method</span></span>

<span data-ttu-id="85003-103">Esegue il merge nell'ambito corrente di tutti gli ambiti dei metadati specificati da una o più chiamate precedenti a [IMetaDataEmit:: merge](imetadataemit-merge-method.md).</span><span class="sxs-lookup"><span data-stu-id="85003-103">Merges into the current scope all the metadata scopes specified by one or more prior calls to [IMetaDataEmit::Merge](imetadataemit-merge-method.md).</span></span>

## <a name="syntax"></a><span data-ttu-id="85003-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="85003-104">Syntax</span></span>

```cppcpp
HRESULT MergeEnd ();
```

## <a name="parameters"></a><span data-ttu-id="85003-105">Parametri</span><span class="sxs-lookup"><span data-stu-id="85003-105">Parameters</span></span>

<span data-ttu-id="85003-106">Questo metodo non accetta parametri.</span><span class="sxs-lookup"><span data-stu-id="85003-106">This method takes no parameters.</span></span>

## <a name="remarks"></a><span data-ttu-id="85003-107">Commenti</span><span class="sxs-lookup"><span data-stu-id="85003-107">Remarks</span></span>

<span data-ttu-id="85003-108">Questa routine attiva il merge effettivo dei metadati, di tutti gli ambiti di importazione specificati dalle chiamate precedenti a `IMetaDataEmit::Merge` , nell'ambito di output corrente.</span><span class="sxs-lookup"><span data-stu-id="85003-108">This routine triggers the actual merge of metadata, of all import scopes specified by preceding calls to `IMetaDataEmit::Merge`, into the current output scope.</span></span>

<span data-ttu-id="85003-109">Per l'Unione si applicano le seguenti condizioni speciali:</span><span class="sxs-lookup"><span data-stu-id="85003-109">The following special conditions apply to the merge:</span></span>

- <span data-ttu-id="85003-110">Un identificatore della versione del modulo (MVID) non viene mai importato, perché è univoco per i metadati nell'ambito di importazione.</span><span class="sxs-lookup"><span data-stu-id="85003-110">A module version identifier (MVID) is never imported, because it is unique to the metadata in the import scope.</span></span>

- <span data-ttu-id="85003-111">Nessuna proprietà esistente a livello di modulo viene sovrascritta.</span><span class="sxs-lookup"><span data-stu-id="85003-111">No existing module-wide properties are overwritten.</span></span>

  <span data-ttu-id="85003-112">Se le proprietà del modulo sono già state impostate per l'ambito corrente, non vengono importate proprietà del modulo.</span><span class="sxs-lookup"><span data-stu-id="85003-112">If module properties were already set for the current scope, no module properties are imported.</span></span> <span data-ttu-id="85003-113">Tuttavia, se le proprietà del modulo non sono state impostate nell'ambito corrente, vengono importate una sola volta, quando vengono rilevate per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="85003-113">However, if module properties have not been set in the current scope, they are imported only once, when they are first encountered.</span></span> <span data-ttu-id="85003-114">Se le proprietà del modulo vengono rilevate, si tratta di duplicati.</span><span class="sxs-lookup"><span data-stu-id="85003-114">If those module properties are encountered again, they are duplicates.</span></span> <span data-ttu-id="85003-115">Se vengono confrontati i valori di tutte le proprietà del modulo (ad eccezione di MVID) e non viene trovato alcun duplicato, viene generato un errore.</span><span class="sxs-lookup"><span data-stu-id="85003-115">If the values of all module properties (except MVID) are compared and no duplicates are found, an error is raised.</span></span>

- <span data-ttu-id="85003-116">Per le definizioni di tipo ( `TypeDef` ), nessun duplicato viene unito nell'ambito corrente.</span><span class="sxs-lookup"><span data-stu-id="85003-116">For type definitions (`TypeDef`), no duplicates are merged into the current scope.</span></span> <span data-ttu-id="85003-117">`TypeDef`viene verificata la presenza di duplicati in base al numero di versione GUID del *nome di oggetto completo*  +  *GUID*  +  *version number*.</span><span class="sxs-lookup"><span data-stu-id="85003-117">`TypeDef` objects are checked for duplicates against each *fully-qualified object name* + *GUID* + *version number*.</span></span> <span data-ttu-id="85003-118">Se esiste una corrispondenza con il nome o il GUID e uno degli altri due elementi è diverso, viene generato un errore.</span><span class="sxs-lookup"><span data-stu-id="85003-118">If there is a match on either name or GUID, and any of the other two elements is different, an error is raised.</span></span> <span data-ttu-id="85003-119">In caso contrario, se tutti e tre gli elementi corrispondono, `MergeEnd` esegue un controllo cursore per verificare che le voci siano effettivamente duplicate; in caso contrario, viene generato un errore.</span><span class="sxs-lookup"><span data-stu-id="85003-119">Otherwise, if all three items match, `MergeEnd` does a cursory check to ensure the entries are indeed duplicates; if not, an error is raised.</span></span> <span data-ttu-id="85003-120">Questo controllo cursore Cerca:</span><span class="sxs-lookup"><span data-stu-id="85003-120">This cursory check looks for:</span></span>

  - <span data-ttu-id="85003-121">Stesse dichiarazioni di membri, che si verificano nello stesso ordine.</span><span class="sxs-lookup"><span data-stu-id="85003-121">The same member declarations, occurring in the same order.</span></span> <span data-ttu-id="85003-122">I membri contrassegnati come `mdPrivateScope` (vedere l'enumerazione [CorMethodAttr](cormethodattr-enumeration.md) ) non sono inclusi in questo controllo. vengono uniti in modo specifico.</span><span class="sxs-lookup"><span data-stu-id="85003-122">Members that are flagged as `mdPrivateScope` (see the [CorMethodAttr](cormethodattr-enumeration.md) enumeration) are not included in this check; they are merged specially.</span></span>

  - <span data-ttu-id="85003-123">Lo stesso layout di classe.</span><span class="sxs-lookup"><span data-stu-id="85003-123">The same class layout.</span></span>

  <span data-ttu-id="85003-124">Ciò significa che un `TypeDef` oggetto deve essere sempre definito in modo completo e coerente in ogni ambito di metadati in cui è dichiarato. se le relative implementazioni dei membri (per una classe) sono distribuite tra più unità di compilazione, la definizione completa si presuppone che sia presente in ogni ambito e non incrementale per ogni ambito.</span><span class="sxs-lookup"><span data-stu-id="85003-124">This means that a `TypeDef` object must always be fully and consistently defined in every metadata scope in which it is declared; if its member implementations (for a class) are spread across multiple compilation units, the full definition is assumed to be present in every scope and not incremental to each scope.</span></span> <span data-ttu-id="85003-125">Se, ad esempio, i nomi dei parametri sono rilevanti per il contratto, è necessario emetterli nello stesso modo in ogni ambito. Se non sono rilevanti, non devono essere emesse nei metadati.</span><span class="sxs-lookup"><span data-stu-id="85003-125">For example, if parameter names are relevant to the contract, they must be emitted the same way into every scope; if they are not relevant, they should not be emitted into metadata.</span></span>

  <span data-ttu-id="85003-126">L'eccezione è che un `TypeDef` oggetto può avere membri incrementali contrassegnati come `mdPrivateScope` .</span><span class="sxs-lookup"><span data-stu-id="85003-126">The exception is that a `TypeDef` object can have incremental members flagged as `mdPrivateScope`.</span></span> <span data-ttu-id="85003-127">Quando si verificano questi elementi, `MergeEnd` li aggiunge all'ambito corrente senza considerare i duplicati.</span><span class="sxs-lookup"><span data-stu-id="85003-127">On encountering these, `MergeEnd` incrementally adds them to the current scope without regard for duplicates.</span></span> <span data-ttu-id="85003-128">Poiché il compilatore riconosce l'ambito privato, il compilatore deve essere responsabile dell'applicazione di regole.</span><span class="sxs-lookup"><span data-stu-id="85003-128">Because the compiler understands the private scope, the compiler must be responsible for enforcing rules.</span></span>

- <span data-ttu-id="85003-129">Gli indirizzi virtuali relativi (RVA) non vengono importati o Uniti; si prevede che il compilatore emetta nuovamente queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="85003-129">Relative virtual addresses (RVAs) are not imported or merged; the compiler is expected to re-emit this information.</span></span>

- <span data-ttu-id="85003-130">Gli attributi personalizzati vengono uniti solo quando l'elemento a cui sono collegati viene Unito.</span><span class="sxs-lookup"><span data-stu-id="85003-130">Custom attributes are merged only when the item to which they are attached is merged.</span></span> <span data-ttu-id="85003-131">Ad esempio, gli attributi personalizzati associati a una classe vengono uniti quando la classe viene rilevata per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="85003-131">For example, custom attributes associated with a class are merged when the class is first encountered.</span></span> <span data-ttu-id="85003-132">Se gli attributi personalizzati sono associati a un oggetto `TypeDef` o `MemberDef` specifico dell'unità di compilazione, ad esempio il timestamp di una compilazione di un membro, non vengono Uniti e il compilatore deve rimuovere o aggiornare tali metadati.</span><span class="sxs-lookup"><span data-stu-id="85003-132">If custom attributes are associated with a `TypeDef` or `MemberDef` that is specific to the compilation unit (such as the time stamp of a member compile), they are not merged and it is up to the compiler to remove or update such metadata.</span></span>

## <a name="requirements"></a><span data-ttu-id="85003-133">Requisiti</span><span class="sxs-lookup"><span data-stu-id="85003-133">Requirements</span></span>

<span data-ttu-id="85003-134">**Piattaforme:** vedere [Requisiti di sistema di .NET Framework](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="85003-134">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>

<span data-ttu-id="85003-135">**Intestazione:** Cor. h</span><span class="sxs-lookup"><span data-stu-id="85003-135">**Header:** Cor.h</span></span>

<span data-ttu-id="85003-136">**Libreria:** Usato come risorsa in MSCorEE. dll</span><span class="sxs-lookup"><span data-stu-id="85003-136">**Library:** Used as a resource in MSCorEE.dll</span></span>

<span data-ttu-id="85003-137">**Versioni .NET Framework:**[!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="85003-137">**.NET Framework Versions:** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]</span></span>

## <a name="see-also"></a><span data-ttu-id="85003-138">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="85003-138">See also</span></span>

- [<span data-ttu-id="85003-139">Interfaccia IMetaDataEmit</span><span class="sxs-lookup"><span data-stu-id="85003-139">IMetaDataEmit Interface</span></span>](imetadataemit-interface.md)
- [<span data-ttu-id="85003-140">Interfaccia IMetaDataEmit2</span><span class="sxs-lookup"><span data-stu-id="85003-140">IMetaDataEmit2 Interface</span></span>](imetadataemit2-interface.md)

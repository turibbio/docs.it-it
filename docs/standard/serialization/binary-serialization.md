---
title: Serializzazione binaria
ms.date: 01/02/2018
helpviewer_keywords:
- binary serialization
- serialization, about serialization
- deserialization
- binary serialization, about serialization
- binary serialization, .net core serialization
- serialization, cross-framework
ms.assetid: 2b1ea3be-1152-4032-b2b3-07794054c405
author: ViktorHofer
ms.openlocfilehash: 9df9b73a1a1347b952d76b76c9058578f5e9f401
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/14/2020
ms.locfileid: "79400638"
---
# <a name="binary-serialization"></a><span data-ttu-id="c69aa-102">Serializzazione binaria</span><span class="sxs-lookup"><span data-stu-id="c69aa-102">Binary serialization</span></span>

<span data-ttu-id="c69aa-103">La serializzazione può essere definita come il processo di archiviazione dello stato di un oggetto su un supporto di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c69aa-103">Serialization can be defined as the process of storing the state of an object to a storage medium.</span></span> <span data-ttu-id="c69aa-104">Durante tale processo, i campi pubblici e privati dell'oggetto e il nome della classe, incluso l'assembly contenente la classe, vengono convertiti in un flusso di byte che viene scritto in un flusso di dati.</span><span class="sxs-lookup"><span data-stu-id="c69aa-104">During this process, the public and private fields of the object and the name of the class, including the assembly containing the class, are converted to a stream of bytes, which is then written to a data stream.</span></span> <span data-ttu-id="c69aa-105">Quando l'oggetto viene successivamente deserializzato, viene creato un clone esatto dell'oggetto originale.</span><span class="sxs-lookup"><span data-stu-id="c69aa-105">When the object is subsequently deserialized, an exact clone of the original object is created.</span></span>

<span data-ttu-id="c69aa-106">Quando si implementa un meccanismo di serializzazione in un ambiente orientato agli oggetti, è necessario fare una serie di compromessi tra semplicità di utilizzo e flessibilità.</span><span class="sxs-lookup"><span data-stu-id="c69aa-106">When implementing a serialization mechanism in an object-oriented environment, you have to make a number of tradeoffs between ease of use and flexibility.</span></span> <span data-ttu-id="c69aa-107">Il processo può essere automatizzato in un ambito di grandi dimensioni, purché si disponga di controllo sufficiente sul processo.</span><span class="sxs-lookup"><span data-stu-id="c69aa-107">The process can be automated to a large extent, provided you are given sufficient control over the process.</span></span> <span data-ttu-id="c69aa-108">Ad esempio, possono verificarsi situazioni in cui non è sufficiente la semplice serializzazione binaria o potrebbe esserci una ragione specifica per decidere quali campi in una classe devono essere serializzati.</span><span class="sxs-lookup"><span data-stu-id="c69aa-108">For example, situations may arise where simple binary serialization is not sufficient, or there might be a specific reason to decide which fields in a class need to be serialized.</span></span> <span data-ttu-id="c69aa-109">Nelle sezioni seguenti viene esaminato l'avanzato meccanismo di serializzazione fornito con .NET e vengono evidenziate alcune importanti funzionalità che consentono di personalizzare il processo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="c69aa-109">The following sections examine the robust serialization mechanism provided with .NET and highlight a number of important features that allow you to customize the process to meet your needs.</span></span>

> [!NOTE]
> <span data-ttu-id="c69aa-110">Lo stato di un oggetto codificato UTF-7 o UTF-8 non viene mantenuto se le relative operazioni di serializzazione e deserializzazione vengono eseguite con versioni di .NET Framework diverse.</span><span class="sxs-lookup"><span data-stu-id="c69aa-110">The state of a UTF-8 or UTF-7 encoded object is not preserved if the object is serialized and deserialized using different .NET Framework versions.</span></span>

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

<span data-ttu-id="c69aa-111">Con la serializzazione binaria è possibile modificare membri privati all'interno di un oggetto e quindi modificarne lo stato.</span><span class="sxs-lookup"><span data-stu-id="c69aa-111">Binary serialization allows modifying private members inside an object and therefore changing the state of it.</span></span> <span data-ttu-id="c69aa-112">Per questo motivo, sono consigliati altri Framework di serializzazione, ad esempio <xref:System.Text.Json?displayProperty=fullName>, che operano sulla superficie dell'API pubblica.</span><span class="sxs-lookup"><span data-stu-id="c69aa-112">Because of this, other serialization frameworks, like <xref:System.Text.Json?displayProperty=fullName>, that operate on the public API surface are recommended.</span></span>

## <a name="net-core"></a><span data-ttu-id="c69aa-113">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c69aa-113">.NET Core</span></span>

<span data-ttu-id="c69aa-114">.NET Core supporta la serializzazione binaria per un subset di tipi.</span><span class="sxs-lookup"><span data-stu-id="c69aa-114">.NET Core supports binary serialization for a subset of types.</span></span> <span data-ttu-id="c69aa-115">È possibile visualizzare l'elenco dei tipi supportati nella sezione [tipi serializzabili](#serializable-types) riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="c69aa-115">You can see the list of supported types in the [Serializable types](#serializable-types) section that follows.</span></span> <span data-ttu-id="c69aa-116">I tipi elencati sono sicuramente serializzabili tra .NET Framework 4.5.1 e versioni successive e tra .NET Core 2,0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c69aa-116">The listed types are guaranteed to be serializable between .NET Framework 4.5.1 and later versions and between .NET Core 2.0 and later versions.</span></span> <span data-ttu-id="c69aa-117">Altre implementazioni di .NET, ad esempio mono, non sono ufficialmente supportate, ma dovrebbero anche funzionare.</span><span class="sxs-lookup"><span data-stu-id="c69aa-117">Other .NET implementations, such as Mono, aren't officially supported but should also work.</span></span>

### <a name="serializable-types"></a><span data-ttu-id="c69aa-118">Tipi serializzabili</span><span class="sxs-lookup"><span data-stu-id="c69aa-118">Serializable types</span></span>

> [!div class="mx-tdCol2BreakAll"]
> | <span data-ttu-id="c69aa-119">Type</span><span class="sxs-lookup"><span data-stu-id="c69aa-119">Type</span></span> | <span data-ttu-id="c69aa-120">Note</span><span class="sxs-lookup"><span data-stu-id="c69aa-120">Notes</span></span> |
> | - | - |
> | <xref:Microsoft.CSharp.RuntimeBinder.RuntimeBinderException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-121">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-121">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:Microsoft.CSharp.RuntimeBinder.RuntimeBinderInternalCompilerException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-122">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-122">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.AccessViolationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-123">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-123">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.AggregateException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-124">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-124">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.AppDomainUnloadedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-125">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-125">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ApplicationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-126">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-126">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ArgumentException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-127">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-127">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ArgumentNullException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-128">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-128">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ArgumentOutOfRangeException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-129">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-129">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ArithmeticException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-130">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-130">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Array?displayProperty=nameWithType> | |
> | <xref:System.ArraySegment%601?displayProperty=nameWithType> | |
> | <xref:System.ArrayTypeMismatchException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-131">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-131">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Attribute?displayProperty=nameWithType> | |
> | <xref:System.BadImageFormatException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-132">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-132">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Boolean?displayProperty=nameWithType> | |
> | <xref:System.Byte?displayProperty=nameWithType> | |
> | <xref:System.CannotUnloadAppDomainException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-133">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-133">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Char?displayProperty=nameWithType> | |
> | <xref:System.Collections.ArrayList?displayProperty=nameWithType> | |
> | <xref:System.Collections.BitArray?displayProperty=nameWithType> | |
> | <xref:System.Collections.Comparer?displayProperty=nameWithType> | |
> | <xref:System.Collections.DictionaryEntry?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.Comparer%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.EqualityComparer%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.HashSet%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-134">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-134">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Collections.Generic.KeyValuePair%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.LinkedList%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.SortedList%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.SortedSet%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Generic.Stack%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Hashtable?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.Collection%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.KeyedCollection%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.ReadOnlyDictionary%602?displayProperty=nameWithType> | |
> | <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601?displayProperty=nameWithType> | |
> | <xref:System.Collections.Queue?displayProperty=nameWithType> | |
> | <xref:System.Collections.SortedList?displayProperty=nameWithType> | |
> | <xref:System.Collections.Specialized.HybridDictionary?displayProperty=nameWithType> | |
> | <xref:System.Collections.Specialized.ListDictionary?displayProperty=nameWithType> | |
> | <xref:System.Collections.Specialized.OrderedDictionary?displayProperty=nameWithType> | |
> | <xref:System.Collections.Specialized.StringCollection?displayProperty=nameWithType> | |
> | <xref:System.Collections.Specialized.StringDictionary?displayProperty=nameWithType> | |
> | <xref:System.Collections.Stack?displayProperty=nameWithType> | |
> | `System.Collections.Generic.NonRandomizedStringEqualityComparer` | <span data-ttu-id="c69aa-135">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-135">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.BindingList%601?displayProperty=nameWithType> | |
> | <xref:System.ComponentModel.DataAnnotations.ValidationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-136">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-136">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.Design.CheckoutException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-137">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-137">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.InvalidAsynchronousStateException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-138">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-138">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.InvalidEnumArgumentException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-139">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-139">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.LicenseException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-140">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-140">Starting in .NET Core 2.0.4.</span></span><br/><span data-ttu-id="c69aa-141">La serializzazione da .NET Framework a .NET Core non è supportata.</span><span class="sxs-lookup"><span data-stu-id="c69aa-141">Serialization from .NET Framework to .NET Core is not supported.</span></span> |
> | <xref:System.ComponentModel.WarningException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-142">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-142">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ComponentModel.Win32Exception?displayProperty=nameWithType> | <span data-ttu-id="c69aa-143">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-143">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.ConfigurationErrorsException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-144">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-144">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.ConfigurationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-145">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-145">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.Provider.ProviderException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-146">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-146">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.SettingsPropertyIsReadOnlyException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-147">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-147">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.SettingsPropertyNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-148">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-148">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Configuration.SettingsPropertyWrongTypeException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-149">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-149">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ContextMarshalException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-150">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-150">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DBNull?displayProperty=nameWithType> | <span data-ttu-id="c69aa-151">A partire da .NET Core 2.0.2 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c69aa-151">Starting in .NET Core 2.0.2 and later versions.</span></span> |
> | <xref:System.Data.Common.DbException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-152">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-152">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.ConstraintException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-153">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-153">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.DBConcurrencyException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-154">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-154">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.DataException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-155">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-155">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.DataSet?displayProperty=nameWithType> | |
> | <xref:System.Data.DataTable?displayProperty=nameWithType> | <span data-ttu-id="c69aa-156">Se si imposta `RemotingFormat` su `SerializationFormat.Binary`, può essere scambiato solo con .NET Core 2,1 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c69aa-156">If you set `RemotingFormat` to `SerializationFormat.Binary`, it can only be exchanged with .NET Core 2.1 and later versions.</span></span> |
> | <xref:System.Data.DeletedRowInaccessibleException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-157">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-157">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.DuplicateNameException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-158">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-158">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.EvaluateException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-159">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-159">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.InRowChangingEventException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-160">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-160">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.InvalidConstraintException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-161">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-161">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.InvalidExpressionException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-162">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-162">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.MissingPrimaryKeyException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-163">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-163">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.NoNullAllowedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-164">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-164">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.Odbc.OdbcException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-165">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-165">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.OperationAbortedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-166">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-166">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.PropertyCollection?displayProperty=nameWithType> | |
> | <xref:System.Data.ReadOnlyException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-167">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-167">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.RowNotInTableException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-168">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-168">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SqlClient.SqlException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-169">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-169">Starting in .NET Core 2.0.4.</span></span><br/><span data-ttu-id="c69aa-170">La serializzazione da .NET Framework a .NET Core non è supportata</span><span class="sxs-lookup"><span data-stu-id="c69aa-170">Serialization from .NET Framework to .NET Core is not supported</span></span> |
> | <xref:System.Data.SqlTypes.SqlAlreadyFilledException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-171">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-171">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SqlTypes.SqlBoolean?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlByte?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlDateTime?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlDouble?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlGuid?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlInt16?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlInt32?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlInt64?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlNotFilledException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-172">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-172">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SqlTypes.SqlNullValueException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-173">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-173">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SqlTypes.SqlString?displayProperty=nameWithType> | |
> | <xref:System.Data.SqlTypes.SqlTruncateException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-174">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-174">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SqlTypes.SqlTypeException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-175">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-175">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.StrongTypingException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-176">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-176">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.SyntaxErrorException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-177">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-177">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Data.VersionNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-178">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-178">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DataMisalignedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-179">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-179">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DateTime?displayProperty=nameWithType> | |
> | <xref:System.DateTimeOffset?displayProperty=nameWithType> | |
> | <xref:System.Decimal?displayProperty=nameWithType> | |
> | `System.Diagnostics.Contracts.ContractException` | <span data-ttu-id="c69aa-180">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-180">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Diagnostics.Tracing.EventSourceException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-181">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-181">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.DirectoryNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-182">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-182">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.MultipleMatchesException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-183">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-183">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.NoMatchingPrincipalException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-184">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-184">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.PasswordException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-185">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-185">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.PrincipalException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-186">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-186">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.PrincipalExistsException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-187">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-187">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.PrincipalOperationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-188">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-188">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.AccountManagement.PrincipalServerDownException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-189">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-189">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectExistsException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-190">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-190">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-191">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-191">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryOperationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-192">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-192">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryServerDownException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-193">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-193">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.ForestTrustCollisionException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-194">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-194">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.ActiveDirectory.SyncFromAllServersOperationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-195">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-195">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.DirectoryServicesCOMException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-196">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-196">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.Protocols.BerConversionException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-197">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-197">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.Protocols.DirectoryException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-198">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-198">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.Protocols.DirectoryOperationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-199">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-199">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.Protocols.LdapException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-200">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-200">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DirectoryServices.Protocols.TlsOperationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-201">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-201">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DivideByZeroException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-202">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-202">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.DllNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-203">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-203">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Double?displayProperty=nameWithType> | |
> | <xref:System.Drawing.Color?displayProperty=nameWithType> | |
> | <xref:System.Drawing.Point?displayProperty=nameWithType> | |
> | <xref:System.Drawing.PointF?displayProperty=nameWithType> | |
> | <xref:System.Drawing.Rectangle?displayProperty=nameWithType> | |
> | <xref:System.Drawing.RectangleF?displayProperty=nameWithType> | |
> | <xref:System.Drawing.Size?displayProperty=nameWithType> | |
> | <xref:System.Drawing.SizeF?displayProperty=nameWithType> | |
> | <xref:System.DuplicateWaitObjectException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-204">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-204">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.EntryPointNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-205">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-205">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Enum?displayProperty=nameWithType> | |
> | <xref:System.EventArgs?displayProperty=nameWithType> | <span data-ttu-id="c69aa-206">A partire da .NET Core 2.0.6.</span><span class="sxs-lookup"><span data-stu-id="c69aa-206">Starting in .NET Core 2.0.6.</span></span> |
> | <xref:System.Exception?displayProperty=nameWithType> | |
> | <xref:System.ExecutionEngineException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-207">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-207">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.FieldAccessException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-208">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-208">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.FormatException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-209">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-209">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Globalization.CompareInfo?displayProperty=nameWithType> | |
> | <xref:System.Globalization.CultureNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-210">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-210">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Globalization.SortVersion?displayProperty=nameWithType> | |
> | <xref:System.Guid?displayProperty=nameWithType> | |
> | `System.IO.Compression.ZLibException` | <span data-ttu-id="c69aa-211">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-211">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.DriveNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-212">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-212">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.EndOfStreamException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-213">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-213">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.FileFormatException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-214">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-214">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.FileLoadException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-215">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-215">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.FileNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-216">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-216">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.IOException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-217">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-217">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.InternalBufferOverflowException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-218">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-218">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.InvalidDataException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-219">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-219">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.IsolatedStorage.IsolatedStorageException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-220">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-220">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IO.PathTooLongException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-221">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-221">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.IndexOutOfRangeException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-222">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-222">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.InsufficientExecutionStackException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-223">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-223">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.InsufficientMemoryException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-224">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-224">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Int16?displayProperty=nameWithType> | |
> | <xref:System.Int32?displayProperty=nameWithType> | |
> | <xref:System.Int64?displayProperty=nameWithType> | |
> | <xref:System.IntPtr?displayProperty=nameWithType> | |
> | <xref:System.InvalidCastException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-225">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-225">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.InvalidOperationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-226">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-226">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.InvalidProgramException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-227">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-227">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.InvalidTimeZoneException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-228">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-228">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MemberAccessException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-229">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-229">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MethodAccessException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-230">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-230">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MissingFieldException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-231">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-231">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MissingMemberException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-232">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-232">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MissingMethodException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-233">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-233">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.MulticastNotSupportedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-234">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-234">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.Cookie?displayProperty=nameWithType> | |
> | <xref:System.Net.CookieCollection?displayProperty=nameWithType> | |
> | <xref:System.Net.CookieContainer?displayProperty=nameWithType> | |
> | <xref:System.Net.CookieException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-235">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-235">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.HttpListenerException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-236">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-236">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.Mail.SmtpException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-237">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-237">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.Mail.SmtpFailedRecipientException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-238">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-238">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.Mail.SmtpFailedRecipientsException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-239">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-239">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.NetworkInformation.NetworkInformationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-240">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-240">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.NetworkInformation.PingException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-241">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-241">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.ProtocolViolationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-242">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-242">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.Sockets.SocketException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-243">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-243">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.WebException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-244">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-244">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Net.WebSockets.WebSocketException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-245">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-245">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.NotFiniteNumberException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-246">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-246">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.NotImplementedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-247">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-247">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.NotSupportedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-248">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-248">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.NullReferenceException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-249">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-249">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Nullable%601?displayProperty=nameWithType> | |
> | <xref:System.Numerics.BigInteger?displayProperty=nameWithType> | |
> | <xref:System.Numerics.Complex?displayProperty=nameWithType> | |
> | <xref:System.Object?displayProperty=nameWithType> | |
> | <xref:System.ObjectDisposedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-250">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-250">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.OperationCanceledException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-251">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-251">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.OutOfMemoryException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-252">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-252">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.OverflowException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-253">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-253">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.PlatformNotSupportedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-254">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-254">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.RankException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-255">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-255">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.AmbiguousMatchException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-256">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-256">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.CustomAttributeFormatException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-257">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-257">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.InvalidFilterCriteriaException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-258">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-258">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.ReflectionTypeLoadException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-259">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-259">Starting in .NET Core 2.0.4.</span></span><br/><span data-ttu-id="c69aa-260">La serializzazione da .NET Framework a .NET Core non è supportata.</span><span class="sxs-lookup"><span data-stu-id="c69aa-260">Serialization from .NET Framework to .NET Core is not supported.</span></span> |
> | <xref:System.Reflection.TargetException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-261">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-261">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.TargetInvocationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-262">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-262">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Reflection.TargetParameterCountException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-263">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-263">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Resources.MissingManifestResourceException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-264">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-264">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Resources.MissingSatelliteAssemblyException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-265">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-265">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.CompilerServices.RuntimeWrappedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-266">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-266">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.COMException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-267">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-267">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.ExternalException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-268">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-268">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.InvalidComObjectException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-269">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-269">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.InvalidOleVariantTypeException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-270">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-270">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.MarshalDirectiveException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-271">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-271">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.SEHException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-272">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-272">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.SafeArrayRankMismatchException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-273">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-273">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.InteropServices.SafeArrayTypeMismatchException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-274">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-274">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.Serialization.InvalidDataContractException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-275">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-275">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Runtime.Serialization.SerializationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-276">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-276">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.SByte?displayProperty=nameWithType> | |
> | <xref:System.Security.AccessControl.PrivilegeNotHeldException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-277">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-277">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Authentication.AuthenticationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-278">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-278">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Authentication.InvalidCredentialException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-279">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-279">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Cryptography.CryptographicException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-280">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-280">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Cryptography.CryptographicUnexpectedOperationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-281">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-281">Starting in .NET Core 2.0.4.</span></span> |
> | `System.Security.Cryptography.Xml.CryptoSignedXmlRecursionException` | <span data-ttu-id="c69aa-282">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-282">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.HostProtectionException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-283">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-283">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Policy.PolicyException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-284">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-284">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.Principal.IdentityNotMappedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-285">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-285">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.SecurityException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-286">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-286">Starting in .NET Core 2.0.4.</span></span><br/><span data-ttu-id="c69aa-287">Dati di serializzazione limitati.</span><span class="sxs-lookup"><span data-stu-id="c69aa-287">Limited serialization data.</span></span> |
> | <xref:System.Security.VerificationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-288">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-288">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Security.XmlSyntaxException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-289">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-289">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ServiceProcess.TimeoutException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-290">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-290">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Single?displayProperty=nameWithType> | |
> | <xref:System.StackOverflowException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-291">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-291">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.String?displayProperty=nameWithType> | |
> | <xref:System.StringComparer?displayProperty=nameWithType> | |
> | <xref:System.SystemException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-292">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-292">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Text.DecoderFallbackException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-293">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-293">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Text.EncoderFallbackException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-294">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-294">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Text.RegularExpressions.RegexMatchTimeoutException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-295">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-295">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Text.StringBuilder?displayProperty=nameWithType> | |
> | <xref:System.Threading.AbandonedMutexException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-296">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-296">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.BarrierPostPhaseException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-297">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-297">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.LockRecursionException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-298">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-298">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.SemaphoreFullException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-299">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-299">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.SynchronizationLockException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-300">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-300">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.Tasks.TaskCanceledException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-301">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-301">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.Tasks.TaskSchedulerException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-302">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-302">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.ThreadAbortException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-303">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-303">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.ThreadInterruptedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-304">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-304">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.ThreadStartException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-305">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-305">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.ThreadStateException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-306">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-306">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Threading.WaitHandleCannotBeOpenedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-307">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-307">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.TimeSpan?displayProperty=nameWithType> | |
> | <xref:System.TimeZoneInfo.AdjustmentRule?displayProperty=nameWithType> | |
> | <xref:System.TimeZoneInfo?displayProperty=nameWithType> | |
> | <xref:System.TimeZoneNotFoundException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-308">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-308">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.TimeoutException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-309">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-309">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Transactions.TransactionAbortedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-310">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-310">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Transactions.TransactionException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-311">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-311">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Transactions.TransactionInDoubtException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-312">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-312">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Transactions.TransactionManagerCommunicationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-313">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-313">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Transactions.TransactionPromotionException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-314">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-314">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Tuple?displayProperty=nameWithType> | |
> | <xref:System.TypeAccessException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-315">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-315">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.TypeInitializationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-316">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-316">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.TypeLoadException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-317">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-317">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.TypeUnloadedException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-318">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-318">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.UInt16?displayProperty=nameWithType> | |
> | <xref:System.UInt32?displayProperty=nameWithType> | |
> | <xref:System.UInt64?displayProperty=nameWithType> | |
> | <xref:System.UIntPtr?displayProperty=nameWithType> | |
> | <xref:System.UnauthorizedAccessException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-319">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-319">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Uri?displayProperty=nameWithType> | |
> | <xref:System.UriFormatException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-320">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-320">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.ValueTuple?displayProperty=nameWithType> | <span data-ttu-id="c69aa-321">Non serializzabile in .NET Framework 4,7 e versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="c69aa-321">Not serializable in .NET Framework 4.7 and earlier versions.</span></span> |
> | <xref:System.ValueType?displayProperty=nameWithType> | |
> | <xref:System.Version?displayProperty=nameWithType> | |
> | <xref:System.WeakReference%601?displayProperty=nameWithType> | |
> | <xref:System.WeakReference?displayProperty=nameWithType> | |
> | <xref:System.Xml.Schema.XmlSchemaException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-322">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-322">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.Schema.XmlSchemaInferenceException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-323">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-323">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.Schema.XmlSchemaValidationException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-324">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-324">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.XPath.XPathException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-325">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-325">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.XmlException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-326">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-326">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.Xsl.XsltCompileException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-327">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-327">Starting in .NET Core 2.0.4.</span></span> |
> | <xref:System.Xml.Xsl.XsltException?displayProperty=nameWithType> | <span data-ttu-id="c69aa-328">A partire da .NET Core 2.0.4.</span><span class="sxs-lookup"><span data-stu-id="c69aa-328">Starting in .NET Core 2.0.4.</span></span> |

## <a name="see-also"></a><span data-ttu-id="c69aa-329">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="c69aa-329">See also</span></span>

- <xref:System.Runtime.Serialization>\
<span data-ttu-id="c69aa-330">Contiene classi utilizzabili per la serializzazione e la deserializzazione di oggetti.</span><span class="sxs-lookup"><span data-stu-id="c69aa-330">Contains classes that can be used for serializing and deserializing objects.</span></span>

- <span data-ttu-id="c69aa-331">[Serializzazione SOAP e XML](../../../docs/standard/serialization/xml-and-soap-serialization.md)</span><span class="sxs-lookup"><span data-stu-id="c69aa-331">[XML and SOAP Serialization](../../../docs/standard/serialization/xml-and-soap-serialization.md)</span></span>\
<span data-ttu-id="c69aa-332">Descrive il meccanismo della serializzazione XML incluso nel Common Language Runtime.</span><span class="sxs-lookup"><span data-stu-id="c69aa-332">Describes the XML serialization mechanism that is included with the common language runtime.</span></span>

- <span data-ttu-id="c69aa-333">[Sicurezza e serializzazione](../../../docs/framework/misc/security-and-serialization.md)</span><span class="sxs-lookup"><span data-stu-id="c69aa-333">[Security and Serialization](../../../docs/framework/misc/security-and-serialization.md)</span></span>\
<span data-ttu-id="c69aa-334">Descrive le linee guida per la creazione di codice protetto da seguire in caso di scrittura di codice che esegue la serializzazione.</span><span class="sxs-lookup"><span data-stu-id="c69aa-334">Describes the secure coding guidelines to follow when writing code that performs serialization.</span></span>

- <span data-ttu-id="c69aa-335">[Servizi remoti .NET](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="c69aa-335">[.NET Remoting](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))</span></span>\
<span data-ttu-id="c69aa-336">Vengono descritti i vari metodi a partire da .NET Framework per le comunicazioni remote.</span><span class="sxs-lookup"><span data-stu-id="c69aa-336">Describes the various methods Starting in .NET Framework for remote communications.</span></span>

- <span data-ttu-id="c69aa-337">[Servizi Web XML creati con ASP.NET e client di servizi Web XML](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7bkzywba(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="c69aa-337">[XML Web Services Created Using ASP.NET and XML Web Service Clients](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7bkzywba(v=vs.100))</span></span>\
<span data-ttu-id="c69aa-338">Articoli che descrivono e spiegano come programmare i servizi Web XML creati con ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c69aa-338">Articles that describe and explain how to program XML Web services created using ASP.NET.</span></span>

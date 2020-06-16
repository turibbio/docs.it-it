---
title: Convenzioni per l'utilizzo di maiuscole e minuscole
description: Applicare le convenzioni di utilizzo delle maiuscole per identificatori, parole composte e termini comuni. Informazioni sul funzionamento della distinzione tra maiuscole e minuscole in .NET.
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- camel-case names [.NET Framework]
- class library design guidelines [.NET Framework], capitalization
- Pascal-case names [.NET Framework]
- case sensitivity, capitalization conventions
- names [.NET Framework], capitalization
ms.assetid: 4c4ea526-9203-486f-b72d-29d61c5b3c6d
ms.openlocfilehash: 4903dc587d84ef36bfaa641cfbda59484266c23c
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2020
ms.locfileid: "84767793"
---
# <a name="capitalization-conventions"></a><span data-ttu-id="21e75-104">Convenzioni per l'utilizzo di maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="21e75-104">Capitalization Conventions</span></span>
<span data-ttu-id="21e75-105">Le linee guida in questo capitolo definiscono un metodo semplice per l'utilizzo di case che, quando vengono applicate in modo coerente, rendono facili da leggere gli identificatori di tipi, membri e parametri.</span><span class="sxs-lookup"><span data-stu-id="21e75-105">The guidelines in this chapter lay out a simple method for using case that, when applied consistently, make identifiers for types, members, and parameters easy to read.</span></span>

## <a name="capitalization-rules-for-identifiers"></a><span data-ttu-id="21e75-106">Regole relative alle maiuscole per gli identificatori</span><span class="sxs-lookup"><span data-stu-id="21e75-106">Capitalization Rules for Identifiers</span></span>
 <span data-ttu-id="21e75-107">Per distinguere le parole in un identificatore, sfruttare la prima lettera di ogni parola nell'identificatore.</span><span class="sxs-lookup"><span data-stu-id="21e75-107">To differentiate words in an identifier, capitalize the first letter of each word in the identifier.</span></span> <span data-ttu-id="21e75-108">Non usare caratteri di sottolineatura per distinguere le parole, o per tale importanza, in qualsiasi punto degli identificatori.</span><span class="sxs-lookup"><span data-stu-id="21e75-108">Do not use underscores to differentiate words, or for that matter, anywhere in identifiers.</span></span> <span data-ttu-id="21e75-109">Esistono due modi appropriati per capitalizzare gli identificatori, a seconda dell'utilizzo dell'identificatore:</span><span class="sxs-lookup"><span data-stu-id="21e75-109">There are two appropriate ways to capitalize identifiers, depending on the use of the identifier:</span></span>

- <span data-ttu-id="21e75-110">Sistema Pascal</span><span class="sxs-lookup"><span data-stu-id="21e75-110">PascalCasing</span></span>

- <span data-ttu-id="21e75-111">camelCasing</span><span class="sxs-lookup"><span data-stu-id="21e75-111">camelCasing</span></span>

 <span data-ttu-id="21e75-112">La convenzione sistema Pascal, usata per tutti gli identificatori eccetto i nomi di parametro, converte in maiuscolo il primo carattere di ogni parola (inclusi gli acronimi per due lettere di lunghezza), come illustrato negli esempi seguenti:</span><span class="sxs-lookup"><span data-stu-id="21e75-112">The PascalCasing convention, used for all identifiers except parameter names, capitalizes the first character of each word (including acronyms over two letters in length), as shown in the following examples:</span></span>

 `PropertyDescriptor`
 `HtmlTag`

 <span data-ttu-id="21e75-113">Viene creato un caso speciale per gli acronimi di due lettere in cui entrambe le lettere sono in maiuscolo, come illustrato nell'identificatore seguente:</span><span class="sxs-lookup"><span data-stu-id="21e75-113">A special case is made for two-letter acronyms in which both letters are capitalized, as shown in the following identifier:</span></span>

 `IOStream`

 <span data-ttu-id="21e75-114">La convenzione camelCasing, usata solo per i nomi dei parametri, converte in maiuscolo il primo carattere di ogni parola eccetto la prima parola, come illustrato negli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="21e75-114">The camelCasing convention, used only for parameter names, capitalizes the first character of each word except the first word, as shown in the following examples.</span></span> <span data-ttu-id="21e75-115">Come illustrato nell'esempio, gli acronimi a due lettere che iniziano un identificatore con distinzione tra maiuscole e minuscole sono entrambi minuscoli.</span><span class="sxs-lookup"><span data-stu-id="21e75-115">As the example also shows, two-letter acronyms that begin a camel-cased identifier are both lowercase.</span></span>

 `propertyDescriptor`
 `ioStream`
 `htmlTag`

 <span data-ttu-id="21e75-116">✔️ utilizzare sistema Pascal per tutti i nomi di membri, tipi e spazi dei nomi pubblici costituiti da più parole.</span><span class="sxs-lookup"><span data-stu-id="21e75-116">✔️ DO use PascalCasing for all public member, type, and namespace names consisting of multiple words.</span></span>

 <span data-ttu-id="21e75-117">✔️ utilizzare camelCasing per i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="21e75-117">✔️ DO use camelCasing for parameter names.</span></span>

 <span data-ttu-id="21e75-118">Nella tabella seguente vengono descritte le regole di utilizzo delle maiuscole per diversi tipi di identificatori.</span><span class="sxs-lookup"><span data-stu-id="21e75-118">The following table describes the capitalization rules for different types of identifiers.</span></span>

|<span data-ttu-id="21e75-119">Identificatore</span><span class="sxs-lookup"><span data-stu-id="21e75-119">Identifier</span></span>|<span data-ttu-id="21e75-120">Maiuscole/minuscole</span><span class="sxs-lookup"><span data-stu-id="21e75-120">Casing</span></span>|<span data-ttu-id="21e75-121">Esempio</span><span class="sxs-lookup"><span data-stu-id="21e75-121">Example</span></span>|
|----------------|------------|-------------|
|<span data-ttu-id="21e75-122">Spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="21e75-122">Namespace</span></span>|<span data-ttu-id="21e75-123">Pascal</span><span class="sxs-lookup"><span data-stu-id="21e75-123">Pascal</span></span>|`namespace System.Security { ... }`|
|<span data-ttu-id="21e75-124">Type</span><span class="sxs-lookup"><span data-stu-id="21e75-124">Type</span></span>|<span data-ttu-id="21e75-125">Pascal</span><span class="sxs-lookup"><span data-stu-id="21e75-125">Pascal</span></span>|`public class StreamReader { ... }`|
|<span data-ttu-id="21e75-126">Interfaccia</span><span class="sxs-lookup"><span data-stu-id="21e75-126">Interface</span></span>|<span data-ttu-id="21e75-127">Pascal</span><span class="sxs-lookup"><span data-stu-id="21e75-127">Pascal</span></span>|`public interface IEnumerable { ... }`|
|<span data-ttu-id="21e75-128">Metodo</span><span class="sxs-lookup"><span data-stu-id="21e75-128">Method</span></span>|<span data-ttu-id="21e75-129">Pascal</span><span class="sxs-lookup"><span data-stu-id="21e75-129">Pascal</span></span>|`public class Object {` <br />  `public virtual string ToString();` <br /> `}`|
|<span data-ttu-id="21e75-130">Proprietà</span><span class="sxs-lookup"><span data-stu-id="21e75-130">Property</span></span>|<span data-ttu-id="21e75-131">Pascal</span><span class="sxs-lookup"><span data-stu-id="21e75-131">Pascal</span></span>|`public class String {` <br />  `public int Length { get; }` <br /> `}`|
|<span data-ttu-id="21e75-132">Evento</span><span class="sxs-lookup"><span data-stu-id="21e75-132">Event</span></span>|<span data-ttu-id="21e75-133">Pascal</span><span class="sxs-lookup"><span data-stu-id="21e75-133">Pascal</span></span>|`public class Process {` <br />  `public event EventHandler Exited;` <br /> `}`|
|<span data-ttu-id="21e75-134">Campo</span><span class="sxs-lookup"><span data-stu-id="21e75-134">Field</span></span>|<span data-ttu-id="21e75-135">Pascal</span><span class="sxs-lookup"><span data-stu-id="21e75-135">Pascal</span></span>|`public class MessageQueue {` <br />  `public static readonly TimeSpan` <br /> `InfiniteTimeout;` <br /> `}` <br /> `public struct UInt32 {` <br />  `public const Min = 0;` <br /> `}`|
|<span data-ttu-id="21e75-136">Valore enum</span><span class="sxs-lookup"><span data-stu-id="21e75-136">Enum value</span></span>|<span data-ttu-id="21e75-137">Pascal</span><span class="sxs-lookup"><span data-stu-id="21e75-137">Pascal</span></span>|`public enum FileMode {` <br />  `Append,` <br />  `...` <br /> `}`|
|<span data-ttu-id="21e75-138">Parametro</span><span class="sxs-lookup"><span data-stu-id="21e75-138">Parameter</span></span>|<span data-ttu-id="21e75-139">notazione Camel</span><span class="sxs-lookup"><span data-stu-id="21e75-139">Camel</span></span>|`public class Convert {` <br />  `public static int ToInt32(string value);` <br /> `}`|

## <a name="capitalizing-compound-words-and-common-terms"></a><span data-ttu-id="21e75-140">Capitalizzazione di parole composte e termini comuni</span><span class="sxs-lookup"><span data-stu-id="21e75-140">Capitalizing Compound Words and Common Terms</span></span>
 <span data-ttu-id="21e75-141">La maggior parte dei termini composti viene considerata come una singola parola per scopi di maiuscole.</span><span class="sxs-lookup"><span data-stu-id="21e75-141">Most compound terms are treated as single words for purposes of capitalization.</span></span>

 <span data-ttu-id="21e75-142">❌NON capitalizzare ogni parola nelle parole composte a forma chiusa.</span><span class="sxs-lookup"><span data-stu-id="21e75-142">❌ DO NOT capitalize each word in so-called closed-form compound words.</span></span>

 <span data-ttu-id="21e75-143">Si tratta di parole composte scritte come una singola parola, ad esempio endpoint.</span><span class="sxs-lookup"><span data-stu-id="21e75-143">These are compound words written as a single word, such as endpoint.</span></span> <span data-ttu-id="21e75-144">Ai fini delle linee guida per l'utilizzo di maiuscole e minuscole, considerare una parola composta a forma chiusa come una singola parola.</span><span class="sxs-lookup"><span data-stu-id="21e75-144">For the purpose of casing guidelines, treat a closed-form compound word as a single word.</span></span> <span data-ttu-id="21e75-145">Usare un dizionario corrente per determinare se una parola composta viene scritta in formato chiuso.</span><span class="sxs-lookup"><span data-stu-id="21e75-145">Use a current dictionary to determine if a compound word is written in closed form.</span></span>

|<span data-ttu-id="21e75-146">Pascal</span><span class="sxs-lookup"><span data-stu-id="21e75-146">Pascal</span></span>|<span data-ttu-id="21e75-147">notazione Camel</span><span class="sxs-lookup"><span data-stu-id="21e75-147">Camel</span></span>|<span data-ttu-id="21e75-148">Not</span><span class="sxs-lookup"><span data-stu-id="21e75-148">Not</span></span>|
|------------|-----------|---------|
|`BitFlag`|`bitFlag`|`Bitflag`|
|`Callback`|`callback`|`CallBack`|
|`Canceled`|`canceled`|`Cancelled`|
|`DoNot`|`doNot`|`Don't`|
|`Email`|`email`|`EMail`|
|`Endpoint`|`endpoint`|`EndPoint`|
|`FileName`|`fileName`|`Filename`|
|`Gridline`|`gridline`|`GridLine`|
|`Hashtable`|`hashtable`|`HashTable`|
|`Id`|`id`|`ID`|
|`Indexes`|`indexes`|`Indices`|
|`LogOff`|`logOff`|`LogOut`|
|`LogOn`|`logOn`|`LogIn`|
|`Metadata`|`metadata`|`MetaData, metaData`|
|`Multipanel`|`multipanel`|`MultiPanel`|
|`Multiview`|`multiview`|`MultiView`|
|`Namespace`|`namespace`|`NameSpace`|
|`Ok`|`ok`|`OK`|
|`Pi`|`pi`|`PI`|
|`Placeholder`|`placeholder`|`PlaceHolder`|
|`SignIn`|`signIn`|`SignOn`|
|`SignOut`|`signOut`|`SignOff`|
|`UserName`|`userName`|`Username`|
|`WhiteSpace`|`whiteSpace`|`Whitespace`|
|`Writable`|`writable`|`Writeable`|

## <a name="case-sensitivity"></a><span data-ttu-id="21e75-149">Maiuscole/minuscole</span><span class="sxs-lookup"><span data-stu-id="21e75-149">Case Sensitivity</span></span>
 <span data-ttu-id="21e75-150">Le lingue che possono essere eseguite su CLR non devono supportare la distinzione tra maiuscole e minuscole, sebbene alcune operazioni.</span><span class="sxs-lookup"><span data-stu-id="21e75-150">Languages that can run on the CLR are not required to support case-sensitivity, although some do.</span></span> <span data-ttu-id="21e75-151">Anche se il linguaggio lo supporta, altre lingue che potrebbero accedere al Framework non lo sono.</span><span class="sxs-lookup"><span data-stu-id="21e75-151">Even if your language supports it, other languages that might access your framework do not.</span></span> <span data-ttu-id="21e75-152">Le API che sono accessibili esternamente, pertanto, non possono basarsi solo su case per distinguere tra due nomi nello stesso contesto.</span><span class="sxs-lookup"><span data-stu-id="21e75-152">Any APIs that are externally accessible, therefore, cannot rely on case alone to distinguish between two names in the same context.</span></span>

 <span data-ttu-id="21e75-153">❌Non presupporre che tutti i linguaggi di programmazione fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="21e75-153">❌ DO NOT assume that all programming languages are case sensitive.</span></span> <span data-ttu-id="21e75-154">Ma non lo sono.</span><span class="sxs-lookup"><span data-stu-id="21e75-154">They are not.</span></span> <span data-ttu-id="21e75-155">I nomi non possono differire solo per caso.</span><span class="sxs-lookup"><span data-stu-id="21e75-155">Names cannot differ by case alone.</span></span>

 <span data-ttu-id="21e75-156">*Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti riservati.*</span><span class="sxs-lookup"><span data-stu-id="21e75-156">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>

 <span data-ttu-id="21e75-157">*Ristampato con l'autorizzazione di Pearson Education, Inc. da [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2a edizione](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) di Krzysztof Cwalina and Brad Abrams, pubblicato il 22 ottobre 2008 da Addison-Wesley Professional nella collana Microsoft Windows Development Series.*</span><span class="sxs-lookup"><span data-stu-id="21e75-157">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>

## <a name="see-also"></a><span data-ttu-id="21e75-158">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="21e75-158">See also</span></span>

- [<span data-ttu-id="21e75-159">Linee guida per la progettazione di Framework</span><span class="sxs-lookup"><span data-stu-id="21e75-159">Framework Design Guidelines</span></span>](index.md)
- [<span data-ttu-id="21e75-160">Linee guida per la denominazione</span><span class="sxs-lookup"><span data-stu-id="21e75-160">Naming Guidelines</span></span>](naming-guidelines.md)

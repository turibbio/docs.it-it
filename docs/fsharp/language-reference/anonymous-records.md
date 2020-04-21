---
title: Record anonimi
description: Informazioni su come usare la costruzione e l'utilizzo di record anonimi, una funzionalità del linguaggio che consente di modificare i dati.
ms.date: 06/12/2019
ms.openlocfilehash: 121f0f638dff2ae529b2488d8e3b1ad9c064cf90
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/21/2020
ms.locfileid: "81738508"
---
# <a name="anonymous-records"></a><span data-ttu-id="838d7-103">Record anonimi</span><span class="sxs-lookup"><span data-stu-id="838d7-103">Anonymous Records</span></span>

<span data-ttu-id="838d7-104">I record anonimi sono aggregazioni semplici di valori denominati che non devono essere dichiarati prima dell'uso.</span><span class="sxs-lookup"><span data-stu-id="838d7-104">Anonymous records are simple aggregates of named values that don't need to be declared before use.</span></span> <span data-ttu-id="838d7-105">È possibile dichiararli come struct o tipi di riferimento.</span><span class="sxs-lookup"><span data-stu-id="838d7-105">You can declare them as either structs or reference types.</span></span> <span data-ttu-id="838d7-106">Sono tipi di riferimento per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="838d7-106">They're reference types by default.</span></span>

## <a name="syntax"></a><span data-ttu-id="838d7-107">Sintassi</span><span class="sxs-lookup"><span data-stu-id="838d7-107">Syntax</span></span>

<span data-ttu-id="838d7-108">Negli esempi seguenti viene illustrata la sintassi dei record anonimi.</span><span class="sxs-lookup"><span data-stu-id="838d7-108">The following examples demonstrate the anonymous record syntax.</span></span> <span data-ttu-id="838d7-109">Elementi delimitati `[item]` come sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="838d7-109">Items delimited as `[item]` are optional.</span></span>

```fsharp
// Construct an anonymous record
let value-name = [struct] {| Label1: Type1; Label2: Type2; ...|}

// Use an anonymous record as a type parameter
let value-name = Type-Name<[struct] {| Label1: Type1; Label2: Type2; ...|}>

// Define a parameter with an anonymous record as input
let function-name (arg-name: [struct] {| Label1: Type1; Label2: Type2; ...|}) ...
```

## <a name="basic-usage"></a><span data-ttu-id="838d7-110">Utilizzo di base</span><span class="sxs-lookup"><span data-stu-id="838d7-110">Basic usage</span></span>

<span data-ttu-id="838d7-111">I record anonimi sono meglio considerati come tipi di record F , che non è necessario dichiararsi prima della creazione di un'istanza.</span><span class="sxs-lookup"><span data-stu-id="838d7-111">Anonymous records are best thought of as F# record types that don't need to be declared before instantiation.</span></span>

<span data-ttu-id="838d7-112">Ad esempio, in questo caso è possibile interagire con una funzione che produce un record anonimo:For example, here how you can interact with a function that produces an anonymous record:</span><span class="sxs-lookup"><span data-stu-id="838d7-112">For example, here how you can interact with a function that produces an anonymous record:</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let r = 2.0
let stats = getCircleStats r
printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
    r stats.Diameter stats.Area stats.Circumference
```

<span data-ttu-id="838d7-113">L'esempio seguente si espande su `printCircleStats` quello precedente con una funzione che accetta un record anonimo come input:The following example expands on the previous one with a function that takes an anonymous record as input:</span><span class="sxs-lookup"><span data-stu-id="838d7-113">The following example expands on the previous one with a `printCircleStats` function that takes an anonymous record as input:</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let printCircleStats r (stats: {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

<span data-ttu-id="838d7-114">La `printCircleStats` chiamata con qualsiasi tipo di record anonimo che non ha la stessa forma del tipo di input non verrà compilata:Calling with any anonymous record type that doesn't have the same "shape" as the input type will fail to compile:</span><span class="sxs-lookup"><span data-stu-id="838d7-114">Calling `printCircleStats` with any anonymous record type that doesn't have the same "shape" as the input type will fail to compile:</span></span>

```fsharp
printCircleStats r {| Diameter = 2.0; Area = 4.0; MyCircumference = 12.566371 |}
// Two anonymous record types have mismatched sets of field names
// '["Area"; "Circumference"; "Diameter"]' and '["Area"; "Diameter"; "MyCircumference"]'
```

## <a name="struct-anonymous-records"></a><span data-ttu-id="838d7-115">Struct record anonimi</span><span class="sxs-lookup"><span data-stu-id="838d7-115">Struct anonymous records</span></span>

<span data-ttu-id="838d7-116">I record anonimi possono anche essere `struct` definiti come struct con la parola chiave facoltativa.</span><span class="sxs-lookup"><span data-stu-id="838d7-116">Anonymous records can also be defined as struct with the optional `struct` keyword.</span></span> <span data-ttu-id="838d7-117">L'esempio seguente aumenta quello precedente producendo e utilizzando un record anonimo struct:The following example augments the previous by producing and consuming a struct anonymous record:</span><span class="sxs-lookup"><span data-stu-id="838d7-117">The following example augments the previous one by producing and consuming a struct anonymous record:</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    // Note that the keyword comes before the '{| |}' brace pair
    struct {| Area = a; Circumference = c; Diameter = d |}

// the 'struct' keyword also comes before the '{| |}' brace pair when declaring the parameter type
let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

### <a name="structness-inference"></a><span data-ttu-id="838d7-118">Inferenza di struttura</span><span class="sxs-lookup"><span data-stu-id="838d7-118">Structness inference</span></span>

<span data-ttu-id="838d7-119">Struct record anonimi consentono anche "inferenza structness" in `struct` cui non è necessario specificare la parola chiave nel sito di chiamata.</span><span class="sxs-lookup"><span data-stu-id="838d7-119">Struct anonymous records also allow for "structness inference" where you do not need to specify the `struct` keyword at the call site.</span></span> <span data-ttu-id="838d7-120">In questo esempio, si `struct` elide `printCircleStats`la parola chiave quando si chiama :</span><span class="sxs-lookup"><span data-stu-id="838d7-120">In this example, you elide the `struct` keyword when calling `printCircleStats`:</span></span>

```fsharp

let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

printCircleStats r {| Area = 4.0; Circumference = 12.6; Diameter = 12.6 |}
```

<span data-ttu-id="838d7-121">Il modello inverso, che specifica `struct` quando il tipo di input non è un record anonimo struct, non verrà compilato.</span><span class="sxs-lookup"><span data-stu-id="838d7-121">The reverse pattern - specifying `struct` when the input type is not a struct anonymous record - will fail to compile.</span></span>

## <a name="embedding-anonymous-records-within-other-types"></a><span data-ttu-id="838d7-122">Incorporamento di record anonimi all'interno di altri tipi</span><span class="sxs-lookup"><span data-stu-id="838d7-122">Embedding anonymous records within other types</span></span>

<span data-ttu-id="838d7-123">È utile dichiarare [le unioni discriminate](discriminated-unions.md) i cui casi sono record.</span><span class="sxs-lookup"><span data-stu-id="838d7-123">It's useful to declare [discriminated unions](discriminated-unions.md) whose cases are records.</span></span> <span data-ttu-id="838d7-124">Tuttavia, se i dati nei record sono dello stesso tipo dell'unione discriminata, è necessario definire tutti i tipi come ricorsivi reciprocamente.</span><span class="sxs-lookup"><span data-stu-id="838d7-124">But if the data in the records is the same type as the discriminated union, you must define all types as mutually recursive.</span></span> <span data-ttu-id="838d7-125">L'utilizzo di record anonimi evita questa restrizione.</span><span class="sxs-lookup"><span data-stu-id="838d7-125">Using anonymous records avoids this restriction.</span></span> <span data-ttu-id="838d7-126">Quello che segue è un tipo di esempio e una funzione che il modello corrisponde su di esso:What follows is an example type and function that pattern matches over it:</span><span class="sxs-lookup"><span data-stu-id="838d7-126">What follows is an example type and function that pattern matches over it:</span></span>

```fsharp
type FullName = { FirstName: string; LastName: string }

// Note that using a named record for Manager and Executive would require mutually recursive definitions.
type Employee =
    | Engineer of FullName
    | Manager of {| Name: FullName; Reports: Employee list |}
    | Executive of {| Name: FullName; Reports: Employee list; Assistant: Employee |}

let getFirstName e =
    match e with
    | Engineer fullName -> fullName.FirstName
    | Manager m -> m.Name.FirstName
    | Executive ex -> ex.Name.FirstName
```

## <a name="copy-and-update-expressions"></a><span data-ttu-id="838d7-127">Copiare e aggiornare espressioni</span><span class="sxs-lookup"><span data-stu-id="838d7-127">Copy and update expressions</span></span>

<span data-ttu-id="838d7-128">I record anonimi supportano la costruzione con [espressioni di copia e aggiornamento](copy-and-update-record-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="838d7-128">Anonymous records support construction with [copy and update expressions](copy-and-update-record-expressions.md).</span></span> <span data-ttu-id="838d7-129">Ad esempio, ecco come è possibile costruire una nuova istanza di un record anonimo che copia i dati di uno esistente:For example, here's how you can construct a new instance of an anonymous record that copies an existing's data:</span><span class="sxs-lookup"><span data-stu-id="838d7-129">For example, here's how you can construct a new instance of an anonymous record that copies an existing one's data:</span></span>

```fsharp
let data = {| X = 1; Y = 2 |}
let data' = {| data with Y = 3 |}
```

<span data-ttu-id="838d7-130">Tuttavia, a differenza dei record denominati, i record anonimi consentono di creare moduli completamente diversi con espressioni di copia e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="838d7-130">However, unlike named records, anonymous records allow you to construct entirely different forms with copy and update expressions.</span></span> <span data-ttu-id="838d7-131">L'esempio seguente accetta lo stesso record anonimo dell'esempio precedente e lo espande in un nuovo record anonimo:</span><span class="sxs-lookup"><span data-stu-id="838d7-131">The follow example takes the same anonymous record from the previous example and expands it into a new anonymous record:</span></span>

```fsharp
let data = {| X = 1; Y = 2 |}
let expandedData = {| data with Z = 3 |} // Gives {| X=1; Y=2; Z=3 |}
```

<span data-ttu-id="838d7-132">È anche possibile creare record anonimi da istanze di record denominati:</span><span class="sxs-lookup"><span data-stu-id="838d7-132">It is also possible to construct anonymous records from instances of named records:</span></span>

```fsharp
type R = { X: int }
let data = { X = 1 }
let data' = {| data with Y = 2 |} // Gives {| X=1; Y=2 |}
```

<span data-ttu-id="838d7-133">È inoltre possibile copiare dati da e verso i record anonimi di riferimento e struct:You can also copy data to and from reference and struct anonymous records:</span><span class="sxs-lookup"><span data-stu-id="838d7-133">You can also copy data to and from reference and struct anonymous records:</span></span>

```fsharp
// Copy data from a reference record into a struct anonymous record
type R1 = { X: int }
let r1 = { X = 1 }

let data1 = struct {| r1 with Y = 1 |}

// Copy data from a struct record into a reference anonymous record
[<Struct>]
type R2 = { X: int }
let r2 = { X = 1 }

let data2 = {| r1 with Y = 1 |}

// Copy the reference anonymous record data into a struct anonymous record
let data3 = struct {| data2 with Z = r2.X |}
```

## <a name="properties-of-anonymous-records"></a><span data-ttu-id="838d7-134">Proprietà dei record anonimi</span><span class="sxs-lookup"><span data-stu-id="838d7-134">Properties of anonymous records</span></span>

<span data-ttu-id="838d7-135">I record anonimi hanno una serie di caratteristiche essenziali per comprendere appieno come possono essere utilizzati.</span><span class="sxs-lookup"><span data-stu-id="838d7-135">Anonymous records have a number of characteristics that are essential to fully understanding how they can be used.</span></span>

### <a name="anonymous-records-are-nominal"></a><span data-ttu-id="838d7-136">I record anonimi sono nominali</span><span class="sxs-lookup"><span data-stu-id="838d7-136">Anonymous records are nominal</span></span>

<span data-ttu-id="838d7-137">I record anonimi sono [di tipo nominale](https://en.wikipedia.org/wiki/Nominal_type_system).</span><span class="sxs-lookup"><span data-stu-id="838d7-137">Anonymous records are [nominal types](https://en.wikipedia.org/wiki/Nominal_type_system).</span></span> <span data-ttu-id="838d7-138">È meglio che siano considerati come tipi di [record](records.md) denominati (che sono anche nominali) che non richiedono una dichiarazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="838d7-138">They are best thought as named [record](records.md) types (which are also nominal) that do not require an up-front declaration.</span></span>

<span data-ttu-id="838d7-139">Si consideri l'esempio seguente con due dichiarazioni di record anonimi:Consider the following example with two anonymous record declarations:</span><span class="sxs-lookup"><span data-stu-id="838d7-139">Consider the following example with two anonymous record declarations:</span></span>

```fsharp
let x = {| X = 1 |}
let y = {| Y = 1 |}
```

<span data-ttu-id="838d7-140">I `x` `y` valori e hanno tipi diversi e non sono compatibili tra loro.</span><span class="sxs-lookup"><span data-stu-id="838d7-140">The `x` and `y` values have different types and are not compatible with one another.</span></span> <span data-ttu-id="838d7-141">Non sono equabili e non sono comparabili.</span><span class="sxs-lookup"><span data-stu-id="838d7-141">They are not equatable and they are not comparable.</span></span> <span data-ttu-id="838d7-142">Per illustrare questo concetto, si consideri un equivalente record denominato:To illustrate this, consider a named record equivalent:</span><span class="sxs-lookup"><span data-stu-id="838d7-142">To illustrate this, consider a named record equivalent:</span></span>

```fsharp
type X = { X: int }
type Y = { Y: int }

let x = { X = 1 }
let y = { Y = 1 }
```

<span data-ttu-id="838d7-143">Non c'è nulla di intrinsecamente diverso nei record anonimi rispetto ai rispettivi equivalenti di record denominati per quanto riguarda l'equivalenza o il confronto dei tipi.</span><span class="sxs-lookup"><span data-stu-id="838d7-143">There isn't anything inherently different about anonymous records when compared with their named record equivalents when concerning type equivalency or comparison.</span></span>

### <a name="anonymous-records-use-structural-equality-and-comparison"></a><span data-ttu-id="838d7-144">I record anonimi utilizzano l'uguaglianza strutturale e il confronto</span><span class="sxs-lookup"><span data-stu-id="838d7-144">Anonymous records use structural equality and comparison</span></span>

<span data-ttu-id="838d7-145">Come i tipi di record, i record anonimi sono strutturalmente equabili e comparabili.</span><span class="sxs-lookup"><span data-stu-id="838d7-145">Like record types, anonymous records are structurally equatable and comparable.</span></span> <span data-ttu-id="838d7-146">Questo è vero solo se tutti i tipi costitutivi supportano l'uguaglianza e il confronto, ad esempio con i tipi di record.</span><span class="sxs-lookup"><span data-stu-id="838d7-146">This is only true if all constituent types support equality and comparison, like with record types.</span></span> <span data-ttu-id="838d7-147">Per supportare l'uguaglianza o il confronto, due record anonimi devono avere la stessa "forma".</span><span class="sxs-lookup"><span data-stu-id="838d7-147">To support equality or comparison, two anonymous records must have the same "shape".</span></span>

```fsharp
{| a = 1+1 |} = {| a = 2 |} // true
{| a = 1+1 |} > {| a = 1 |} // true

// error FS0001: Two anonymous record types have mismatched sets of field names '["a"]' and '["a"; "b"]'
{| a = 1 + 1 |} = {| a = 2;  b = 1|}
```

### <a name="anonymous-records-are-serializable"></a><span data-ttu-id="838d7-148">I record anonimi sono serializzabili</span><span class="sxs-lookup"><span data-stu-id="838d7-148">Anonymous records are serializable</span></span>

<span data-ttu-id="838d7-149">È possibile serializzare i record anonimi come con i record denominati.</span><span class="sxs-lookup"><span data-stu-id="838d7-149">You can serialize anonymous records just as you can with named records.</span></span> <span data-ttu-id="838d7-150">Di seguito è riportato un esempio di utilizzo [di Newtonsoft.Json:](https://www.nuget.org/packages/Newtonsoft.Json/)</span><span class="sxs-lookup"><span data-stu-id="838d7-150">Here is an example using [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/):</span></span>

```fsharp
open Newtonsoft.Json

let phillip' = {| name="Phillip"; age=28 |}
let philStr = JsonConvert.SerializeObject(phillip')

let phillip = JsonConvert.DeserializeObject<{|name: string; age: int|}>(philStr)
printfn "Name: %s Age: %d" phillip.name phillip.age
```

<span data-ttu-id="838d7-151">I record anonimi sono utili per l'invio di dati leggeri in rete senza la necessità di definire un dominio per i tipi serializzati/deserializzati in anticipo.</span><span class="sxs-lookup"><span data-stu-id="838d7-151">Anonymous records are useful for sending lightweight data over a network without the need to define a domain for your serialized/deserialized types up front.</span></span>

### <a name="anonymous-records-interoperate-with-c-anonymous-types"></a><span data-ttu-id="838d7-152">I record anonimi interagiscono con i tipi anonimi di C</span><span class="sxs-lookup"><span data-stu-id="838d7-152">Anonymous records interoperate with C# anonymous types</span></span>

<span data-ttu-id="838d7-153">È possibile utilizzare un'API .NET che richiede l'utilizzo di [tipi anonimi di C.](../../csharp/programming-guide/classes-and-structs/anonymous-types.md)</span><span class="sxs-lookup"><span data-stu-id="838d7-153">It is possible to use a .NET API that requires the use of [C# anonymous types](../../csharp/programming-guide/classes-and-structs/anonymous-types.md).</span></span> <span data-ttu-id="838d7-154">I tipi anonimi di C, sono semplici per interagire con l'utilizzo di record anonimi.</span><span class="sxs-lookup"><span data-stu-id="838d7-154">C# anonymous types are trivial to interoperate with by using anonymous records.</span></span> <span data-ttu-id="838d7-155">Nell'esempio seguente viene illustrato come utilizzare i record anonimi per chiamare un overload LINQ che richiede un tipo anonimo:The following example shows how to use anonymous records to call a [LINQ](../../csharp/programming-guide/concepts/linq/index.md) overload that requires an anonymous type:</span><span class="sxs-lookup"><span data-stu-id="838d7-155">The following example shows how to use anonymous records to call a [LINQ](../../csharp/programming-guide/concepts/linq/index.md) overload that requires an anonymous type:</span></span>

```fsharp
open System.Linq

let names = [ "Ana"; "Felipe"; "Emilia"]
let nameGrouping = names.Select(fun n -> {| Name = n; FirstLetter = n.[0] |})
for ng in nameGrouping do
    printfn "%s has first letter %c" ng.Name ng.FirstLetter
```

<span data-ttu-id="838d7-156">Esistono una moltitudine di altre API utilizzate in .NET che richiedono l'uso di passaggio in un tipo anonimo.</span><span class="sxs-lookup"><span data-stu-id="838d7-156">There are a multitude of other APIs used throughout .NET that require the use of passing in an anonymous type.</span></span> <span data-ttu-id="838d7-157">I record anonimi sono il tuo strumento per lavorare con loro.</span><span class="sxs-lookup"><span data-stu-id="838d7-157">Anonymous records are your tool for working with them.</span></span>

## <a name="limitations"></a><span data-ttu-id="838d7-158">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="838d7-158">Limitations</span></span>

<span data-ttu-id="838d7-159">I record anonimi hanno alcune restrizioni sul loro utilizzo.</span><span class="sxs-lookup"><span data-stu-id="838d7-159">Anonymous records have some restrictions in their usage.</span></span> <span data-ttu-id="838d7-160">Alcuni sono inerenti al loro design, ma altri sono suscettibili di cambiare.</span><span class="sxs-lookup"><span data-stu-id="838d7-160">Some are inherent to their design, but others are amenable to change.</span></span>

### <a name="limitations-with-pattern-matching"></a><span data-ttu-id="838d7-161">Limitazioni con criteri di ricerca</span><span class="sxs-lookup"><span data-stu-id="838d7-161">Limitations with pattern matching</span></span>

<span data-ttu-id="838d7-162">I record anonimi non supportano i criteri di ricerca, a differenza dei record denominati.</span><span class="sxs-lookup"><span data-stu-id="838d7-162">Anonymous records do not support pattern matching, unlike named records.</span></span> <span data-ttu-id="838d7-163">Ci sono tre ragioni:</span><span class="sxs-lookup"><span data-stu-id="838d7-163">There are three reasons:</span></span>

1. <span data-ttu-id="838d7-164">Un modello dovrebbe tenere conto di ogni campo di un record anonimo, a differenza dei tipi di record denominati.</span><span class="sxs-lookup"><span data-stu-id="838d7-164">A pattern would have to account for every field of an anonymous record, unlike named record types.</span></span> <span data-ttu-id="838d7-165">Ciò è dovuto al fatto che i record anonimi non supportano il sottotipi strutturale, ovvero tipi nominali.</span><span class="sxs-lookup"><span data-stu-id="838d7-165">This is because anonymous records do not support structural subtyping – they are nominal types.</span></span>
2. <span data-ttu-id="838d7-166">A causa di (1), non è possibile avere modelli aggiuntivi in un'espressione di corrispondenza di modello, poiché ogni modello distinto implicherebbe un tipo di record anonimo diverso.</span><span class="sxs-lookup"><span data-stu-id="838d7-166">Because of (1), there is no ability to have additional patterns in a pattern match expression, as each distinct pattern would imply a different anonymous record type.</span></span>
3. <span data-ttu-id="838d7-167">A causa di (3), qualsiasi modello di record anonimo sarebbe più dettagliato rispetto all'uso della notazione "punto".</span><span class="sxs-lookup"><span data-stu-id="838d7-167">Because of (3), any anonymous record pattern would be more verbose than the use of “dot” notation.</span></span>

<span data-ttu-id="838d7-168">È disponibile un suggerimento linguistico aperto per consentire la [corrispondenza dei modelli in contesti limitati.](https://github.com/fsharp/fslang-suggestions/issues/713)</span><span class="sxs-lookup"><span data-stu-id="838d7-168">There is an open language suggestion to [allow pattern matching in limited contexts](https://github.com/fsharp/fslang-suggestions/issues/713).</span></span>

### <a name="limitations-with-mutability"></a><span data-ttu-id="838d7-169">Limitazioni con mutabilità</span><span class="sxs-lookup"><span data-stu-id="838d7-169">Limitations with mutability</span></span>

<span data-ttu-id="838d7-170">Al momento non è possibile definire `mutable` un record anonimo con dati.</span><span class="sxs-lookup"><span data-stu-id="838d7-170">It is not currently possible to define an anonymous record with `mutable` data.</span></span> <span data-ttu-id="838d7-171">È disponibile un [suggerimento linguistico aperto](https://github.com/fsharp/fslang-suggestions/issues/732) per consentire i dati modificabili.</span><span class="sxs-lookup"><span data-stu-id="838d7-171">There is an [open language suggestion](https://github.com/fsharp/fslang-suggestions/issues/732) to allow mutable data.</span></span>

### <a name="limitations-with-struct-anonymous-records"></a><span data-ttu-id="838d7-172">Limitazioni con i record anonimi structLimitations with struct anonymous records</span><span class="sxs-lookup"><span data-stu-id="838d7-172">Limitations with struct anonymous records</span></span>

<span data-ttu-id="838d7-173">Non è possibile dichiarare record `IsByRefLike` anonimi `IsReadOnly`struct come o .</span><span class="sxs-lookup"><span data-stu-id="838d7-173">It is not possible to declare struct anonymous records as `IsByRefLike` or `IsReadOnly`.</span></span> <span data-ttu-id="838d7-174">C'è un [suggerimento linguistico aperto](https://github.com/fsharp/fslang-suggestions/issues/712) per i record per `IsByRefLike` e `IsReadOnly` anonimi.</span><span class="sxs-lookup"><span data-stu-id="838d7-174">There is an [open language suggestion](https://github.com/fsharp/fslang-suggestions/issues/712) to for `IsByRefLike` and `IsReadOnly` anonymous records.</span></span>

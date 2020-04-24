---
title: Raccolte (C#)
ms.date: 07/20/2015
ms.assetid: 317d7dc3-8587-4873-8b3e-556f86497939
ms.openlocfilehash: d2996648690fc03b5f1d6a90e0be96155c5a24ed
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/20/2020
ms.locfileid: "81645475"
---
# <a name="collections-c"></a><span data-ttu-id="0b62c-102">Raccolte (C#)</span><span class="sxs-lookup"><span data-stu-id="0b62c-102">Collections (C#)</span></span>

<span data-ttu-id="0b62c-103">Per molte applicazioni è utile creare e gestire gruppi di oggetti correlati.</span><span class="sxs-lookup"><span data-stu-id="0b62c-103">For many applications, you want to create and manage groups of related objects.</span></span> <span data-ttu-id="0b62c-104">È possibile raggruppare gli oggetti in due modi: creando matrici di oggetti e creando raccolte di oggetti.</span><span class="sxs-lookup"><span data-stu-id="0b62c-104">There are two ways to group objects: by creating arrays of objects, and by creating collections of objects.</span></span>

<span data-ttu-id="0b62c-105">Le matrici sono estremamente utili per la creazione e l'uso di un numero fisso di oggetti fortemente tipizzati.</span><span class="sxs-lookup"><span data-stu-id="0b62c-105">Arrays are most useful for creating and working with a fixed number of strongly-typed objects.</span></span> <span data-ttu-id="0b62c-106">Per altre informazioni sulle matrici, vedere [Matrici](../arrays/index.md).</span><span class="sxs-lookup"><span data-stu-id="0b62c-106">For information about arrays, see [Arrays](../arrays/index.md).</span></span>

<span data-ttu-id="0b62c-107">Le raccolte consentono di lavorare in modo più flessibile con gruppi di oggetti.</span><span class="sxs-lookup"><span data-stu-id="0b62c-107">Collections provide a more flexible way to work with groups of objects.</span></span> <span data-ttu-id="0b62c-108">A differenza delle matrici, il gruppo di oggetti con cui si lavora può aumentare e diminuire in modo dinamico in base alle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0b62c-108">Unlike arrays, the group of objects you work with can grow and shrink dynamically as the needs of the application change.</span></span> <span data-ttu-id="0b62c-109">Per alcune raccolte è possibile assegnare una chiave a qualsiasi oggetto inserito nella raccolta in modo da recuperare rapidamente l'oggetto usando la chiave.</span><span class="sxs-lookup"><span data-stu-id="0b62c-109">For some collections, you can assign a key to any object that you put into the collection so that you can quickly retrieve the object by using the key.</span></span>

<span data-ttu-id="0b62c-110">Una raccolta è una classe. Di conseguenza, prima di poter aggiungere elementi a una nuova raccolta è necessario dichiarare la raccolta.</span><span class="sxs-lookup"><span data-stu-id="0b62c-110">A collection is a class, so you must declare an instance of the class before you can add elements to that collection.</span></span>

<span data-ttu-id="0b62c-111">Se la raccolta contiene elementi di un solo tipo di dati, è possibile usare una delle classi dello spazio dei nomi <xref:System.Collections.Generic?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="0b62c-111">If your collection contains elements of only one data type, you can use one of the classes in the <xref:System.Collections.Generic?displayProperty=nameWithType> namespace.</span></span> <span data-ttu-id="0b62c-112">In una raccolta generica viene imposta l'indipendenza dai tipi, in modo da impedire che vengano aggiunti altri tipi di dati alla raccolta.</span><span class="sxs-lookup"><span data-stu-id="0b62c-112">A generic collection enforces type safety so that no other data type can be added to it.</span></span> <span data-ttu-id="0b62c-113">Quando si recupera un elemento da una raccolta generica, non è necessario determinarne il tipo di dati né convertirlo.</span><span class="sxs-lookup"><span data-stu-id="0b62c-113">When you retrieve an element from a generic collection, you do not have to determine its data type or convert it.</span></span>

> [!NOTE]
> <span data-ttu-id="0b62c-114">Per gli esempi in questo argomento, includere le direttive [using](../../language-reference/keywords/using-directive.md) per gli spazi dei nomi `System.Collections.Generic` e `System.Linq`.</span><span class="sxs-lookup"><span data-stu-id="0b62c-114">For the examples in this topic, include [using](../../language-reference/keywords/using-directive.md) directives for the `System.Collections.Generic` and `System.Linq` namespaces.</span></span>

 <span data-ttu-id="0b62c-115">**In questo argomento**</span><span class="sxs-lookup"><span data-stu-id="0b62c-115">**In this topic**</span></span>

- [<span data-ttu-id="0b62c-116">Uso di una raccolta semplice</span><span class="sxs-lookup"><span data-stu-id="0b62c-116">Using a Simple Collection</span></span>](#BKMK_SimpleCollection)

- [<span data-ttu-id="0b62c-117">Tipi di raccolte</span><span class="sxs-lookup"><span data-stu-id="0b62c-117">Kinds of Collections</span></span>](#BKMK_KindsOfCollections)

  - [<span data-ttu-id="0b62c-118">Classi System.Collections.Generic</span><span class="sxs-lookup"><span data-stu-id="0b62c-118">System.Collections.Generic Classes</span></span>](#BKMK_Generic)

  - [<span data-ttu-id="0b62c-119">Classi System.Collections.Concurrent</span><span class="sxs-lookup"><span data-stu-id="0b62c-119">System.Collections.Concurrent Classes</span></span>](#BKMK_Concurrent)

  - [<span data-ttu-id="0b62c-120">Classi System.Collections</span><span class="sxs-lookup"><span data-stu-id="0b62c-120">System.Collections Classes</span></span>](#BKMK_Collections)

- [<span data-ttu-id="0b62c-121">Implementazione di una raccolta di coppie chiave/valore</span><span class="sxs-lookup"><span data-stu-id="0b62c-121">Implementing a Collection of Key/Value Pairs</span></span>](#BKMK_KeyValuePairs)

- [<span data-ttu-id="0b62c-122">Uso di LINQ per accedere a una raccolta</span><span class="sxs-lookup"><span data-stu-id="0b62c-122">Using LINQ to Access a Collection</span></span>](#BKMK_LINQ)

- [<span data-ttu-id="0b62c-123">Ordinamento di una raccolta</span><span class="sxs-lookup"><span data-stu-id="0b62c-123">Sorting a Collection</span></span>](#BKMK_Sorting)

- [<span data-ttu-id="0b62c-124">Definizione di una raccolta personalizzata</span><span class="sxs-lookup"><span data-stu-id="0b62c-124">Defining a Custom Collection</span></span>](#BKMK_CustomCollection)

- [<span data-ttu-id="0b62c-125">Iterators</span><span class="sxs-lookup"><span data-stu-id="0b62c-125">Iterators</span></span>](#BKMK_Iterators)

<a name="BKMK_SimpleCollection"></a>

## <a name="using-a-simple-collection"></a><span data-ttu-id="0b62c-126">Uso di una raccolta semplice</span><span class="sxs-lookup"><span data-stu-id="0b62c-126">Using a Simple Collection</span></span>

<span data-ttu-id="0b62c-127">Gli esempi in questa sezione usano la classe generica <xref:System.Collections.Generic.List%601>, che consente di usare un elenco di oggetti fortemente tipizzato.</span><span class="sxs-lookup"><span data-stu-id="0b62c-127">The examples in this section use the generic <xref:System.Collections.Generic.List%601> class, which enables you to work with a strongly typed list of objects.</span></span>

<span data-ttu-id="0b62c-128">L'esempio seguente crea un elenco di stringhe, quindi esegue l'iterazione nelle stringhe usando un'istruzione [foreach](../../language-reference/keywords/foreach-in.md).</span><span class="sxs-lookup"><span data-stu-id="0b62c-128">The following example creates a list of strings and then iterates through the strings by using a [foreach](../../language-reference/keywords/foreach-in.md) statement.</span></span>

```csharp
// Create a list of strings.
var salmons = new List<string>();
salmons.Add("chinook");
salmons.Add("coho");
salmons.Add("pink");
salmons.Add("sockeye");

// Iterate through the list.
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook coho pink sockeye
```

<span data-ttu-id="0b62c-129">Se il contenuto di una raccolta è noto in anticipo, si può usare un *inizializzatore di raccolta* per inizializzare la raccolta.</span><span class="sxs-lookup"><span data-stu-id="0b62c-129">If the contents of a collection are known in advance, you can use a *collection initializer* to initialize the collection.</span></span> <span data-ttu-id="0b62c-130">Per altre informazioni, vedere [Inizializzatori di oggetto e di raccolta](../classes-and-structs/object-and-collection-initializers.md).</span><span class="sxs-lookup"><span data-stu-id="0b62c-130">For more information, see [Object and Collection Initializers](../classes-and-structs/object-and-collection-initializers.md).</span></span>

<span data-ttu-id="0b62c-131">L'esempio seguente è identico all'esempio precedente, ma usa un inizializzatore di raccolta per aggiungere elementi alla raccolta.</span><span class="sxs-lookup"><span data-stu-id="0b62c-131">The following example is the same as the previous example, except a collection initializer is used to add elements to the collection.</span></span>

```csharp
// Create a list of strings by using a
// collection initializer.
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };

// Iterate through the list.
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook coho pink sockeye
```

<span data-ttu-id="0b62c-132">È possibile usare un'istruzione [for](../../language-reference/keywords/for.md) anziché un'istruzione `foreach` per eseguire l'iterazione in una raccolta.</span><span class="sxs-lookup"><span data-stu-id="0b62c-132">You can use a [for](../../language-reference/keywords/for.md) statement instead of a `foreach` statement to iterate through a collection.</span></span> <span data-ttu-id="0b62c-133">Questo è possibile mediante l'accesso agli elementi della raccolta dalla posizione di indice.</span><span class="sxs-lookup"><span data-stu-id="0b62c-133">You accomplish this by accessing the collection elements by the index position.</span></span> <span data-ttu-id="0b62c-134">L'indice degli elementi inizia da 0 e termina in corrispondenza del numero di elementi meno 1.</span><span class="sxs-lookup"><span data-stu-id="0b62c-134">The index of the elements starts at 0 and ends at the element count minus 1.</span></span>

<span data-ttu-id="0b62c-135">Nell'esempio seguente l'iterazione negli elementi di una raccolta avviene mediante `for` anziché mediante `foreach`.</span><span class="sxs-lookup"><span data-stu-id="0b62c-135">The following example iterates through the elements of a collection by using `for` instead of `foreach`.</span></span>

```csharp
// Create a list of strings by using a
// collection initializer.
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };

for (var index = 0; index < salmons.Count; index++)
{
    Console.Write(salmons[index] + " ");
}
// Output: chinook coho pink sockeye
```

<span data-ttu-id="0b62c-136">Nell'esempio seguente viene rimosso un elemento dalla raccolta specificando l'oggetto da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="0b62c-136">The following example removes an element from the collection by specifying the object to remove.</span></span>

```csharp
// Create a list of strings by using a
// collection initializer.
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };

// Remove an element from the list by specifying
// the object.
salmons.Remove("coho");

// Iterate through the list.
foreach (var salmon in salmons)
{
    Console.Write(salmon + " ");
}
// Output: chinook pink sockeye
```

<span data-ttu-id="0b62c-137">Nell'esempio seguente vengono rimossi elementi da un elenco generico.</span><span class="sxs-lookup"><span data-stu-id="0b62c-137">The following example removes elements from a generic list.</span></span> <span data-ttu-id="0b62c-138">Invece di un'istruzione `foreach` viene usata un'istruzione [for](../../language-reference/keywords/for.md) che esegue l'iterazione in ordine decrescente.</span><span class="sxs-lookup"><span data-stu-id="0b62c-138">Instead of a `foreach` statement, a [for](../../language-reference/keywords/for.md) statement that iterates in descending order is used.</span></span> <span data-ttu-id="0b62c-139">Ciò è necessario perché il metodo <xref:System.Collections.Generic.List%601.RemoveAt%2A> fa sì che gli elementi dopo un elemento rimosso abbiano un valore di indice inferiore.</span><span class="sxs-lookup"><span data-stu-id="0b62c-139">This is because the <xref:System.Collections.Generic.List%601.RemoveAt%2A> method causes elements after a removed element to have a lower index value.</span></span>

```csharp
var numbers = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };

// Remove odd numbers.
for (var index = numbers.Count - 1; index >= 0; index--)
{
    if (numbers[index] % 2 == 1)
    {
        // Remove the element by specifying
        // the zero-based index in the list.
        numbers.RemoveAt(index);
    }
}

// Iterate through the list.
// A lambda expression is placed in the ForEach method
// of the List(T) object.
numbers.ForEach(
    number => Console.Write(number + " "));
// Output: 0 2 4 6 8
```

<span data-ttu-id="0b62c-140">Per il tipo di elementi in <xref:System.Collections.Generic.List%601>, è possibile anche definire una classe personalizzata.</span><span class="sxs-lookup"><span data-stu-id="0b62c-140">For the type of elements in the <xref:System.Collections.Generic.List%601>, you can also define your own class.</span></span> <span data-ttu-id="0b62c-141">Nell'esempio seguente la classe `Galaxy` viene usata dall'oggetto <xref:System.Collections.Generic.List%601> definito nel codice.</span><span class="sxs-lookup"><span data-stu-id="0b62c-141">In the following example, the `Galaxy` class that is used by the <xref:System.Collections.Generic.List%601> is defined in the code.</span></span>

```csharp
private static void IterateThroughList()
{
    var theGalaxies = new List<Galaxy>
        {
            new Galaxy() { Name="Tadpole", MegaLightYears=400},
            new Galaxy() { Name="Pinwheel", MegaLightYears=25},
            new Galaxy() { Name="Milky Way", MegaLightYears=0},
            new Galaxy() { Name="Andromeda", MegaLightYears=3}
        };

    foreach (Galaxy theGalaxy in theGalaxies)
    {
        Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears);
    }

    // Output:
    //  Tadpole  400
    //  Pinwheel  25
    //  Milky Way  0
    //  Andromeda  3
}

public class Galaxy
{
    public string Name { get; set; }
    public int MegaLightYears { get; set; }
}
```

<a name="BKMK_KindsOfCollections"></a>

## <a name="kinds-of-collections"></a><span data-ttu-id="0b62c-142">Tipi di raccolte</span><span class="sxs-lookup"><span data-stu-id="0b62c-142">Kinds of Collections</span></span>

<span data-ttu-id="0b62c-143">Molte raccolte comuni vengono fornite da .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="0b62c-143">Many common collections are provided by the .NET Framework.</span></span> <span data-ttu-id="0b62c-144">Ogni tipo di raccolta è progettato per uno scopo specifico.</span><span class="sxs-lookup"><span data-stu-id="0b62c-144">Each type of collection is designed for a specific purpose.</span></span>

<span data-ttu-id="0b62c-145">In questa sezione sono descritte alcune classi di raccolte comuni:</span><span class="sxs-lookup"><span data-stu-id="0b62c-145">Some of the common collection classes are described in this section:</span></span>

- <span data-ttu-id="0b62c-146">Classi <xref:System.Collections.Generic></span><span class="sxs-lookup"><span data-stu-id="0b62c-146"><xref:System.Collections.Generic> classes</span></span>

- <span data-ttu-id="0b62c-147">Classi <xref:System.Collections.Concurrent></span><span class="sxs-lookup"><span data-stu-id="0b62c-147"><xref:System.Collections.Concurrent> classes</span></span>

- <span data-ttu-id="0b62c-148">Classi <xref:System.Collections></span><span class="sxs-lookup"><span data-stu-id="0b62c-148"><xref:System.Collections> classes</span></span>

<a name="BKMK_Generic"></a>

### <a name="systemcollectionsgeneric-classes"></a><span data-ttu-id="0b62c-149">Classi System.Collections.Generic</span><span class="sxs-lookup"><span data-stu-id="0b62c-149">System.Collections.Generic Classes</span></span>

<span data-ttu-id="0b62c-150">È possibile creare una raccolta generica usando una delle classi dello spazio dei nomi <xref:System.Collections.Generic>.</span><span class="sxs-lookup"><span data-stu-id="0b62c-150">You can create a generic collection by using one of the classes in the <xref:System.Collections.Generic> namespace.</span></span> <span data-ttu-id="0b62c-151">Una raccolta generica è utile quando ogni elemento al suo interno presenta lo stesso tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="0b62c-151">A generic collection is useful when every item in the collection has the same data type.</span></span> <span data-ttu-id="0b62c-152">Una raccolta generica applica la tipizzazione forte consentendo di aggiungere soltanto i tipi di dati desiderati.</span><span class="sxs-lookup"><span data-stu-id="0b62c-152">A generic collection enforces strong typing by allowing only the desired data type to be added.</span></span>

<span data-ttu-id="0b62c-153">La tabella seguente elenca alcune delle classi di uso frequente dello spazio dei nomi <xref:System.Collections.Generic?displayProperty=nameWithType>:</span><span class="sxs-lookup"><span data-stu-id="0b62c-153">The following table lists some of the frequently used classes of the <xref:System.Collections.Generic?displayProperty=nameWithType> namespace:</span></span>

|<span data-ttu-id="0b62c-154">Classe</span><span class="sxs-lookup"><span data-stu-id="0b62c-154">Class</span></span>|<span data-ttu-id="0b62c-155">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0b62c-155">Description</span></span>|
|---|---|
|<xref:System.Collections.Generic.Dictionary%602>|<span data-ttu-id="0b62c-156">Rappresenta una raccolta di coppie chiave/valore organizzate in base alla chiave.</span><span class="sxs-lookup"><span data-stu-id="0b62c-156">Represents a collection of key/value pairs that are organized based on the key.</span></span>|
|<xref:System.Collections.Generic.List%601>|<span data-ttu-id="0b62c-157">Rappresenta un elenco di oggetti accessibile in base all'indice.</span><span class="sxs-lookup"><span data-stu-id="0b62c-157">Represents a list of objects that can be accessed by index.</span></span> <span data-ttu-id="0b62c-158">Fornisce metodi per la ricerca, l'ordinamento e la modifica degli elenchi.</span><span class="sxs-lookup"><span data-stu-id="0b62c-158">Provides methods to search, sort, and modify lists.</span></span>|
|<xref:System.Collections.Generic.Queue%601>|<span data-ttu-id="0b62c-159">Rappresenta una raccolta di oggetti FIFO (First-In First-Out).</span><span class="sxs-lookup"><span data-stu-id="0b62c-159">Represents a first in, first out (FIFO) collection of objects.</span></span>|
|<xref:System.Collections.Generic.SortedList%602>|<span data-ttu-id="0b62c-160">Rappresenta una raccolta di coppie chiave/valore ordinate per chiave in base all'implementazione <xref:System.Collections.Generic.IComparer%601> associata.</span><span class="sxs-lookup"><span data-stu-id="0b62c-160">Represents a collection of key/value pairs that are sorted by key based on the associated <xref:System.Collections.Generic.IComparer%601> implementation.</span></span>|
|<xref:System.Collections.Generic.Stack%601>|<span data-ttu-id="0b62c-161">Rappresenta una raccolta di oggetti LIFO (Last-In First-Out).</span><span class="sxs-lookup"><span data-stu-id="0b62c-161">Represents a last in, first out (LIFO) collection of objects.</span></span>|

<span data-ttu-id="0b62c-162">Per altre informazioni, vedere [Tipi di raccolte comunemente utilizzate](../../../standard/collections/commonly-used-collection-types.md), [Selezione di una classe Collection](../../../standard/collections/selecting-a-collection-class.md) e <xref:System.Collections.Generic>.</span><span class="sxs-lookup"><span data-stu-id="0b62c-162">For additional information, see [Commonly Used Collection Types](../../../standard/collections/commonly-used-collection-types.md), [Selecting a Collection Class](../../../standard/collections/selecting-a-collection-class.md), and <xref:System.Collections.Generic>.</span></span>

<a name="BKMK_Concurrent"></a>

### <a name="systemcollectionsconcurrent-classes"></a><span data-ttu-id="0b62c-163">Classi System.Collections.Concurrent</span><span class="sxs-lookup"><span data-stu-id="0b62c-163">System.Collections.Concurrent Classes</span></span>

<span data-ttu-id="0b62c-164">In .NET Framework 4 o versioni successive le raccolte dello spazio dei nomi <xref:System.Collections.Concurrent> garantiscono operazioni thread-safe efficienti per accedere agli elementi della raccolta da più thread.</span><span class="sxs-lookup"><span data-stu-id="0b62c-164">In the .NET Framework 4 or newer, the collections in the <xref:System.Collections.Concurrent> namespace provide efficient thread-safe operations for accessing collection items from multiple threads.</span></span>

<span data-ttu-id="0b62c-165">Le classi dello spazio dei nomi <xref:System.Collections.Concurrent> devono essere usate in sostituzione dei tipi corrispondenti negli spazi dei nomi <xref:System.Collections.Generic?displayProperty=nameWithType> e <xref:System.Collections?displayProperty=nameWithType> ogni volta che più thread accedono contemporaneamente alla raccolta.</span><span class="sxs-lookup"><span data-stu-id="0b62c-165">The classes in the <xref:System.Collections.Concurrent> namespace should be used instead of the corresponding types in the <xref:System.Collections.Generic?displayProperty=nameWithType> and <xref:System.Collections?displayProperty=nameWithType> namespaces whenever multiple threads are accessing the collection concurrently.</span></span> <span data-ttu-id="0b62c-166">Per altre informazioni, vedere [Raccolte thread-safe](../../../standard/collections/thread-safe/index.md) e <xref:System.Collections.Concurrent>.</span><span class="sxs-lookup"><span data-stu-id="0b62c-166">For more information, see [Thread-Safe Collections](../../../standard/collections/thread-safe/index.md) and <xref:System.Collections.Concurrent>.</span></span>

<span data-ttu-id="0b62c-167">Alcune classi incluse nello spazio dei nomi <xref:System.Collections.Concurrent> sono <xref:System.Collections.Concurrent.BlockingCollection%601>, <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, <xref:System.Collections.Concurrent.ConcurrentQueue%601> e <xref:System.Collections.Concurrent.ConcurrentStack%601>.</span><span class="sxs-lookup"><span data-stu-id="0b62c-167">Some classes included in the <xref:System.Collections.Concurrent> namespace are <xref:System.Collections.Concurrent.BlockingCollection%601>, <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, <xref:System.Collections.Concurrent.ConcurrentQueue%601>, and <xref:System.Collections.Concurrent.ConcurrentStack%601>.</span></span>

<a name="BKMK_Collections"></a>

### <a name="systemcollections-classes"></a><span data-ttu-id="0b62c-168">Classi System.Collections</span><span class="sxs-lookup"><span data-stu-id="0b62c-168">System.Collections Classes</span></span>

<span data-ttu-id="0b62c-169">Le classi dello spazio dei nomi <xref:System.Collections?displayProperty=nameWithType> non archiviano gli elementi come oggetti tipizzati in modo specifico, ma come oggetti di tipo `Object`.</span><span class="sxs-lookup"><span data-stu-id="0b62c-169">The classes in the <xref:System.Collections?displayProperty=nameWithType> namespace do not store elements as specifically typed objects, but as objects of type `Object`.</span></span>

<span data-ttu-id="0b62c-170">Quando possibile, usare le raccolte generiche degli spazi dei nomi <xref:System.Collections.Generic?displayProperty=nameWithType> o <xref:System.Collections.Concurrent> al posto dei tipi legacy dello spazio dei nomi `System.Collections`.</span><span class="sxs-lookup"><span data-stu-id="0b62c-170">Whenever possible, you should use the generic collections in the <xref:System.Collections.Generic?displayProperty=nameWithType> namespace or the <xref:System.Collections.Concurrent> namespace instead of the legacy types in the `System.Collections` namespace.</span></span>

<span data-ttu-id="0b62c-171">La tabella seguente elenca alcune classi di uso frequente nello spazio dei nomi `System.Collections`:</span><span class="sxs-lookup"><span data-stu-id="0b62c-171">The following table lists some of the frequently used classes in the `System.Collections` namespace:</span></span>

|<span data-ttu-id="0b62c-172">Classe</span><span class="sxs-lookup"><span data-stu-id="0b62c-172">Class</span></span>|<span data-ttu-id="0b62c-173">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0b62c-173">Description</span></span>|
|---|---|
|<xref:System.Collections.ArrayList>|<span data-ttu-id="0b62c-174">Rappresenta una matrice di oggetti le cui dimensioni sono incrementate in modo dinamico in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="0b62c-174">Represents an array of objects whose size is dynamically increased as required.</span></span>|
|<xref:System.Collections.Hashtable>|<span data-ttu-id="0b62c-175">Rappresenta una raccolta di coppie chiave/valore organizzate in base al codice hash della chiave.</span><span class="sxs-lookup"><span data-stu-id="0b62c-175">Represents a collection of key/value pairs that are organized based on the hash code of the key.</span></span>|
|<xref:System.Collections.Queue>|<span data-ttu-id="0b62c-176">Rappresenta una raccolta di oggetti FIFO (First-In First-Out).</span><span class="sxs-lookup"><span data-stu-id="0b62c-176">Represents a first in, first out (FIFO) collection of objects.</span></span>|
|<xref:System.Collections.Stack>|<span data-ttu-id="0b62c-177">Rappresenta una raccolta di oggetti LIFO (Last-In First-Out).</span><span class="sxs-lookup"><span data-stu-id="0b62c-177">Represents a last in, first out (LIFO) collection of objects.</span></span>|

<span data-ttu-id="0b62c-178">Lo spazio dei nomi <xref:System.Collections.Specialized> offre classi di raccolte fortemente tipizzate e specializzate, ad esempio raccolte di sole stringhe, dizionari ibridi e dizionari a elenchi collegati.</span><span class="sxs-lookup"><span data-stu-id="0b62c-178">The <xref:System.Collections.Specialized> namespace provides specialized and strongly typed collection classes, such as string-only collections and linked-list and hybrid dictionaries.</span></span>

<a name="BKMK_KeyValuePairs"></a>

## <a name="implementing-a-collection-of-keyvalue-pairs"></a><span data-ttu-id="0b62c-179">Implementazione di una raccolta di coppie chiave/valore</span><span class="sxs-lookup"><span data-stu-id="0b62c-179">Implementing a Collection of Key/Value Pairs</span></span>

<span data-ttu-id="0b62c-180">La raccolta generica <xref:System.Collections.Generic.Dictionary%602> consente di accedere agli elementi di una raccolta usando la chiave di ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="0b62c-180">The <xref:System.Collections.Generic.Dictionary%602> generic collection enables you to access to elements in a collection by using the key of each element.</span></span> <span data-ttu-id="0b62c-181">Ogni aggiunta al dizionario è costituita da un valore e dalla chiave associata corrispondente.</span><span class="sxs-lookup"><span data-stu-id="0b62c-181">Each addition to the dictionary consists of a value and its associated key.</span></span> <span data-ttu-id="0b62c-182">Il recupero di un valore tramite la relativa chiave è un'operazione veloce, perché la classe `Dictionary` viene implementata come tabella hash.</span><span class="sxs-lookup"><span data-stu-id="0b62c-182">Retrieving a value by using its key is fast because the `Dictionary` class is implemented as a hash table.</span></span>

<span data-ttu-id="0b62c-183">L'esempio seguente crea una raccolta `Dictionary` ed esegue l'iterazione nel dizionario usando un'istruzione `foreach`.</span><span class="sxs-lookup"><span data-stu-id="0b62c-183">The following example creates a `Dictionary` collection and iterates through the dictionary by using a `foreach` statement.</span></span>

```csharp
private static void IterateThruDictionary()
{
    Dictionary<string, Element> elements = BuildDictionary();

    foreach (KeyValuePair<string, Element> kvp in elements)
    {
        Element theElement = kvp.Value;

        Console.WriteLine("key: " + kvp.Key);
        Console.WriteLine("values: " + theElement.Symbol + " " +
            theElement.Name + " " + theElement.AtomicNumber);
    }
}

private static Dictionary<string, Element> BuildDictionary()
{
    var elements = new Dictionary<string, Element>();

    AddToDictionary(elements, "K", "Potassium", 19);
    AddToDictionary(elements, "Ca", "Calcium", 20);
    AddToDictionary(elements, "Sc", "Scandium", 21);
    AddToDictionary(elements, "Ti", "Titanium", 22);

    return elements;
}

private static void AddToDictionary(Dictionary<string, Element> elements,
    string symbol, string name, int atomicNumber)
{
    Element theElement = new Element();

    theElement.Symbol = symbol;
    theElement.Name = name;
    theElement.AtomicNumber = atomicNumber;

    elements.Add(key: theElement.Symbol, value: theElement);
}

public class Element
{
    public string Symbol { get; set; }
    public string Name { get; set; }
    public int AtomicNumber { get; set; }
}
```

<span data-ttu-id="0b62c-184">Per usare invece un inizializzatore di raccolta per compilare la raccolta `Dictionary`, è possibile sostituire i metodi `BuildDictionary` e `AddToDictionary` con il metodo seguente.</span><span class="sxs-lookup"><span data-stu-id="0b62c-184">To instead use a collection initializer to build the `Dictionary` collection, you can replace the `BuildDictionary` and `AddToDictionary` methods with the following method.</span></span>

```csharp
private static Dictionary<string, Element> BuildDictionary2()
{
    return new Dictionary<string, Element>
    {
        {"K",
            new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},
        {"Ca",
            new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},
        {"Sc",
            new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},
        {"Ti",
            new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}}
    };
}
```

<span data-ttu-id="0b62c-185">L'esempio seguente usa il metodo <xref:System.Collections.Generic.Dictionary%602.ContainsKey%2A> e la proprietà <xref:System.Collections.Generic.Dictionary%602.Item%2A> di `Dictionary` per trovare rapidamente un elemento in base alla chiave.</span><span class="sxs-lookup"><span data-stu-id="0b62c-185">The following example uses the <xref:System.Collections.Generic.Dictionary%602.ContainsKey%2A> method and the <xref:System.Collections.Generic.Dictionary%602.Item%2A> property of `Dictionary` to quickly find an item by key.</span></span> <span data-ttu-id="0b62c-186">La proprietà `Item` consente di accedere a un elemento nella raccolta `elements` usando il codice `elements[symbol]` in C#.</span><span class="sxs-lookup"><span data-stu-id="0b62c-186">The `Item` property enables you to access an item in the `elements` collection by using the `elements[symbol]` in C#.</span></span>

```csharp
private static void FindInDictionary(string symbol)
{
    Dictionary<string, Element> elements = BuildDictionary();

    if (elements.ContainsKey(symbol) == false)
    {
        Console.WriteLine(symbol + " not found");
    }
    else
    {
        Element theElement = elements[symbol];
        Console.WriteLine("found: " + theElement.Name);
    }
}
```

<span data-ttu-id="0b62c-187">L'esempio seguente usa invece il metodo <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> per individuare rapidamente un elemento in base alla chiave.</span><span class="sxs-lookup"><span data-stu-id="0b62c-187">The following example instead uses the <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> method quickly find an item by key.</span></span>

```csharp
private static void FindInDictionary2(string symbol)
{
    Dictionary<string, Element> elements = BuildDictionary();

    Element theElement = null;
    if (elements.TryGetValue(symbol, out theElement) == false)
        Console.WriteLine(symbol + " not found");
    else
        Console.WriteLine("found: " + theElement.Name);
}
```

<a name="BKMK_LINQ"></a>

## <a name="using-linq-to-access-a-collection"></a><span data-ttu-id="0b62c-188">Uso di LINQ per accedere a una raccolta</span><span class="sxs-lookup"><span data-stu-id="0b62c-188">Using LINQ to Access a Collection</span></span>

<span data-ttu-id="0b62c-189">È possibile usare LINQ (Language-Integrated Query) per accedere alle raccolte.</span><span class="sxs-lookup"><span data-stu-id="0b62c-189">LINQ (Language-Integrated Query) can be used to access collections.</span></span> <span data-ttu-id="0b62c-190">Le query LINQ forniscono funzionalità di filtro, ordinamento e raggruppamento.</span><span class="sxs-lookup"><span data-stu-id="0b62c-190">LINQ queries provide filtering, ordering, and grouping capabilities.</span></span> <span data-ttu-id="0b62c-191">Per ulteriori informazioni, vedere [Guida introduttiva a LINQ in C.](linq/index.md)</span><span class="sxs-lookup"><span data-stu-id="0b62c-191">For more information, see [Getting Started with LINQ in C#](linq/index.md).</span></span>

<span data-ttu-id="0b62c-192">Nell'esempio seguente viene eseguita una query LINQ su un oggetto `List` generico.</span><span class="sxs-lookup"><span data-stu-id="0b62c-192">The following example runs a LINQ query against a generic `List`.</span></span> <span data-ttu-id="0b62c-193">La query LINQ restituisce una raccolta diversa che contiene i risultati.</span><span class="sxs-lookup"><span data-stu-id="0b62c-193">The LINQ query returns a different collection that contains the results.</span></span>

```csharp
private static void ShowLINQ()
{
    List<Element> elements = BuildList();

    // LINQ Query.
    var subset = from theElement in elements
                 where theElement.AtomicNumber < 22
                 orderby theElement.Name
                 select theElement;

    foreach (Element theElement in subset)
    {
        Console.WriteLine(theElement.Name + " " + theElement.AtomicNumber);
    }

    // Output:
    //  Calcium 20
    //  Potassium 19
    //  Scandium 21
}

private static List<Element> BuildList()
{
    return new List<Element>
    {
        { new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},
        { new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},
        { new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},
        { new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}}
    };
}

public class Element
{
    public string Symbol { get; set; }
    public string Name { get; set; }
    public int AtomicNumber { get; set; }
}
```

<a name="BKMK_Sorting"></a>

## <a name="sorting-a-collection"></a><span data-ttu-id="0b62c-194">Ordinamento di una raccolta</span><span class="sxs-lookup"><span data-stu-id="0b62c-194">Sorting a Collection</span></span>

<span data-ttu-id="0b62c-195">L'esempio seguente illustra una procedura per ordinare una raccolta.</span><span class="sxs-lookup"><span data-stu-id="0b62c-195">The following example illustrates a procedure for sorting a collection.</span></span> <span data-ttu-id="0b62c-196">Nell'esempio vengono ordinate le istanze della classe `Car` archiviate in un oggetto <xref:System.Collections.Generic.List%601>.</span><span class="sxs-lookup"><span data-stu-id="0b62c-196">The example sorts instances of the `Car` class that are stored in a <xref:System.Collections.Generic.List%601>.</span></span> <span data-ttu-id="0b62c-197">La classe `Car` implementa l'interfaccia <xref:System.IComparable%601>, che richiede l'implementazione del metodo <xref:System.IComparable%601.CompareTo%2A>.</span><span class="sxs-lookup"><span data-stu-id="0b62c-197">The `Car` class implements the <xref:System.IComparable%601> interface, which requires that the <xref:System.IComparable%601.CompareTo%2A> method be implemented.</span></span>

<span data-ttu-id="0b62c-198">Ogni chiamata al metodo <xref:System.IComparable%601.CompareTo%2A> effettua un confronto unico che viene usato per l'ordinamento.</span><span class="sxs-lookup"><span data-stu-id="0b62c-198">Each call to the <xref:System.IComparable%601.CompareTo%2A> method makes a single comparison that is used for sorting.</span></span> <span data-ttu-id="0b62c-199">Il codice scritto dall'utente presente nel metodo `CompareTo` restituisce un valore per ogni confronto dell'oggetto corrente con un altro oggetto.</span><span class="sxs-lookup"><span data-stu-id="0b62c-199">User-written code in the `CompareTo` method returns a value for each comparison of the current object with another object.</span></span> <span data-ttu-id="0b62c-200">Il valore restituito è minore di zero se l'oggetto corrente è inferiore all'altro oggetto, maggiore di zero se l'oggetto corrente è superiore all'altro oggetto e zero se sono uguali.</span><span class="sxs-lookup"><span data-stu-id="0b62c-200">The value returned is less than zero if the current object is less than the other object, greater than zero if the current object is greater than the other object, and zero if they are equal.</span></span> <span data-ttu-id="0b62c-201">In questo modo è possibile definire nel codice i criteri di maggiore, minore e uguale.</span><span class="sxs-lookup"><span data-stu-id="0b62c-201">This enables you to define in code the criteria for greater than, less than, and equal.</span></span>

<span data-ttu-id="0b62c-202">Nel metodo `ListCars` l'istruzione `cars.Sort()` ordina l'elenco.</span><span class="sxs-lookup"><span data-stu-id="0b62c-202">In the `ListCars` method, the `cars.Sort()` statement sorts the list.</span></span> <span data-ttu-id="0b62c-203">Questa chiamata al metodo <xref:System.Collections.Generic.List%601.Sort%2A> di <xref:System.Collections.Generic.List%601> determina la chiamata automatica al metodo `CompareTo` per gli oggetti `Car` in `List`.</span><span class="sxs-lookup"><span data-stu-id="0b62c-203">This call to the <xref:System.Collections.Generic.List%601.Sort%2A> method of the <xref:System.Collections.Generic.List%601> causes the `CompareTo` method to be called automatically for the `Car` objects in the `List`.</span></span>

```csharp
private static void ListCars()
{
    var cars = new List<Car>
    {
        { new Car() { Name = "car1", Color = "blue", Speed = 20}},
        { new Car() { Name = "car2", Color = "red", Speed = 50}},
        { new Car() { Name = "car3", Color = "green", Speed = 10}},
        { new Car() { Name = "car4", Color = "blue", Speed = 50}},
        { new Car() { Name = "car5", Color = "blue", Speed = 30}},
        { new Car() { Name = "car6", Color = "red", Speed = 60}},
        { new Car() { Name = "car7", Color = "green", Speed = 50}}
    };

    // Sort the cars by color alphabetically, and then by speed
    // in descending order.
    cars.Sort();

    // View all of the cars.
    foreach (Car thisCar in cars)
    {
        Console.Write(thisCar.Color.PadRight(5) + " ");
        Console.Write(thisCar.Speed.ToString() + " ");
        Console.Write(thisCar.Name);
        Console.WriteLine();
    }

    // Output:
    //  blue  50 car4
    //  blue  30 car5
    //  blue  20 car1
    //  green 50 car7
    //  green 10 car3
    //  red   60 car6
    //  red   50 car2
}

public class Car : IComparable<Car>
{
    public string Name { get; set; }
    public int Speed { get; set; }
    public string Color { get; set; }

    public int CompareTo(Car other)
    {
        // A call to this method makes a single comparison that is
        // used for sorting.

        // Determine the relative order of the objects being compared.
        // Sort by color alphabetically, and then by speed in
        // descending order.

        // Compare the colors.
        int compare;
        compare = String.Compare(this.Color, other.Color, true);

        // If the colors are the same, compare the speeds.
        if (compare == 0)
        {
            compare = this.Speed.CompareTo(other.Speed);

            // Use descending order for speed.
            compare = -compare;
        }

        return compare;
    }
}
```

<a name="BKMK_CustomCollection"></a>

## <a name="defining-a-custom-collection"></a><span data-ttu-id="0b62c-204">Definizione di una raccolta personalizzata</span><span class="sxs-lookup"><span data-stu-id="0b62c-204">Defining a Custom Collection</span></span>

<span data-ttu-id="0b62c-205">È possibile definire una raccolta implementando l'interfaccia <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Collections.IEnumerable>.</span><span class="sxs-lookup"><span data-stu-id="0b62c-205">You can define a collection by implementing the <xref:System.Collections.Generic.IEnumerable%601> or <xref:System.Collections.IEnumerable> interface.</span></span>

<span data-ttu-id="0b62c-206">Sebbene sia possibile definire una raccolta personalizzata, in genere è preferibile usare le raccolte incluse in .NET Framework, descritte in [Tipi di raccolte](#BKMK_KindsOfCollections) in precedenza in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="0b62c-206">Although you can define a custom collection, it is usually better to instead use the collections that are included in the .NET Framework, which are described in [Kinds of Collections](#BKMK_KindsOfCollections) earlier in this topic.</span></span>

<span data-ttu-id="0b62c-207">L'esempio seguente definisce una classe di raccolte personalizzata denominata `AllColors`.</span><span class="sxs-lookup"><span data-stu-id="0b62c-207">The following example defines a custom collection class named `AllColors`.</span></span> <span data-ttu-id="0b62c-208">Questa classe implementa l'interfaccia <xref:System.Collections.IEnumerable> che richiede l'implementazione del metodo <xref:System.Collections.IEnumerable.GetEnumerator%2A>.</span><span class="sxs-lookup"><span data-stu-id="0b62c-208">This class implements the <xref:System.Collections.IEnumerable> interface, which requires that the <xref:System.Collections.IEnumerable.GetEnumerator%2A> method be implemented.</span></span>

<span data-ttu-id="0b62c-209">Il metodo `GetEnumerator` restituisce un'istanza della classe `ColorEnumerator`.</span><span class="sxs-lookup"><span data-stu-id="0b62c-209">The `GetEnumerator` method returns an instance of the `ColorEnumerator` class.</span></span> <span data-ttu-id="0b62c-210">`ColorEnumerator` implementa l'interfaccia <xref:System.Collections.IEnumerator> che richiede l'implementazione della proprietà <xref:System.Collections.IEnumerator.Current%2A> e dei metodi <xref:System.Collections.IEnumerator.MoveNext%2A> e <xref:System.Collections.IEnumerator.Reset%2A>.</span><span class="sxs-lookup"><span data-stu-id="0b62c-210">`ColorEnumerator` implements the <xref:System.Collections.IEnumerator> interface, which requires that the <xref:System.Collections.IEnumerator.Current%2A> property, <xref:System.Collections.IEnumerator.MoveNext%2A> method, and <xref:System.Collections.IEnumerator.Reset%2A> method be implemented.</span></span>

```csharp
private static void ListColors()
{
    var colors = new AllColors();

    foreach (Color theColor in colors)
    {
        Console.Write(theColor.Name + " ");
    }
    Console.WriteLine();
    // Output: red blue green
}

// Collection class.
public class AllColors : System.Collections.IEnumerable
{
    Color[] _colors =
    {
        new Color() { Name = "red" },
        new Color() { Name = "blue" },
        new Color() { Name = "green" }
    };

    public System.Collections.IEnumerator GetEnumerator()
    {
        return new ColorEnumerator(_colors);

        // Instead of creating a custom enumerator, you could
        // use the GetEnumerator of the array.
        //return _colors.GetEnumerator();
    }

    // Custom enumerator.
    private class ColorEnumerator : System.Collections.IEnumerator
    {
        private Color[] _colors;
        private int _position = -1;

        public ColorEnumerator(Color[] colors)
        {
            _colors = colors;
        }

        object System.Collections.IEnumerator.Current
        {
            get
            {
                return _colors[_position];
            }
        }

        bool System.Collections.IEnumerator.MoveNext()
        {
            _position++;
            return (_position < _colors.Length);
        }

        void System.Collections.IEnumerator.Reset()
        {
            _position = -1;
        }
    }
}

// Element class.
public class Color
{
    public string Name { get; set; }
}
```

<a name="BKMK_Iterators"></a>

## <a name="iterators"></a><span data-ttu-id="0b62c-211">Iterators</span><span class="sxs-lookup"><span data-stu-id="0b62c-211">Iterators</span></span>

<span data-ttu-id="0b62c-212">Un *iteratore* viene usato per eseguire un'iterazione personalizzata in una raccolta.</span><span class="sxs-lookup"><span data-stu-id="0b62c-212">An *iterator* is used to perform a custom iteration over a collection.</span></span> <span data-ttu-id="0b62c-213">Un iteratore può essere un metodo o una funzione di accesso `get`.</span><span class="sxs-lookup"><span data-stu-id="0b62c-213">An iterator can be a method or a `get` accessor.</span></span> <span data-ttu-id="0b62c-214">Un iteratore usa un'istruzione [yield return](../../language-reference/keywords/yield.md) per restituire ogni elemento della raccolta, uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="0b62c-214">An iterator uses a [yield return](../../language-reference/keywords/yield.md) statement to return each element of the collection one at a time.</span></span>

<span data-ttu-id="0b62c-215">Per chiamare un iteratore usare un'istruzione [foreach](../../language-reference/keywords/foreach-in.md).</span><span class="sxs-lookup"><span data-stu-id="0b62c-215">You call an iterator by using a [foreach](../../language-reference/keywords/foreach-in.md) statement.</span></span> <span data-ttu-id="0b62c-216">Ogni iterazione del ciclo `foreach` chiama l'iteratore.</span><span class="sxs-lookup"><span data-stu-id="0b62c-216">Each iteration of the `foreach` loop calls the iterator.</span></span> <span data-ttu-id="0b62c-217">Quando si raggiunge un'istruzione `yield return` nell'iteratore, viene restituita un'espressione e viene mantenuta la posizione corrente nel codice.</span><span class="sxs-lookup"><span data-stu-id="0b62c-217">When a `yield return` statement is reached in the iterator, an expression is returned, and the current location in code is retained.</span></span> <span data-ttu-id="0b62c-218">L'esecuzione viene ripresa a partire da quella posizione la volta successiva che viene chiamato l'iteratore.</span><span class="sxs-lookup"><span data-stu-id="0b62c-218">Execution is restarted from that location the next time that the iterator is called.</span></span>

<span data-ttu-id="0b62c-219">Per altre informazioni, vedere [Iteratori (C#)](./iterators.md).</span><span class="sxs-lookup"><span data-stu-id="0b62c-219">For more information, see [Iterators (C#)](./iterators.md).</span></span>

<span data-ttu-id="0b62c-220">Nell'esempio seguente viene usato un metodo iteratore.</span><span class="sxs-lookup"><span data-stu-id="0b62c-220">The following example uses an iterator method.</span></span> <span data-ttu-id="0b62c-221">Il metodo iteratore dispone di un'istruzione `yield return` all'interno di un ciclo [for](../../language-reference/keywords/for.md).</span><span class="sxs-lookup"><span data-stu-id="0b62c-221">The iterator method has a `yield return` statement that is inside a [for](../../language-reference/keywords/for.md) loop.</span></span> <span data-ttu-id="0b62c-222">Nel metodo `ListEvenNumbers` ogni iterazione del corpo dell'istruzione `foreach` crea una chiamata al metodo iteratore, che procede all'istruzione `yield return` successiva.</span><span class="sxs-lookup"><span data-stu-id="0b62c-222">In the `ListEvenNumbers` method, each iteration of the `foreach` statement body creates a call to the iterator method, which proceeds to the next `yield return` statement.</span></span>

```csharp
private static void ListEvenNumbers()
{
    foreach (int number in EvenSequence(5, 18))
    {
        Console.Write(number.ToString() + " ");
    }
    Console.WriteLine();
    // Output: 6 8 10 12 14 16 18
}

private static IEnumerable<int> EvenSequence(
    int firstNumber, int lastNumber)
{
    // Yield even numbers in the range.
    for (var number = firstNumber; number <= lastNumber; number++)
    {
        if (number % 2 == 0)
        {
            yield return number;
        }
    }
}
```

## <a name="see-also"></a><span data-ttu-id="0b62c-223">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0b62c-223">See also</span></span>

- [<span data-ttu-id="0b62c-224">Inizializzatori di oggetto e di raccolta</span><span class="sxs-lookup"><span data-stu-id="0b62c-224">Object and Collection Initializers</span></span>](../classes-and-structs/object-and-collection-initializers.md)
- [<span data-ttu-id="0b62c-225">Concetti di programmazione (C#)</span><span class="sxs-lookup"><span data-stu-id="0b62c-225">Programming Concepts (C#)</span></span>](./index.md)
- [<span data-ttu-id="0b62c-226">Istruzione Option Strict</span><span class="sxs-lookup"><span data-stu-id="0b62c-226">Option Strict Statement</span></span>](../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [<span data-ttu-id="0b62c-227">LINQ to Objects (C#)</span><span class="sxs-lookup"><span data-stu-id="0b62c-227">LINQ to Objects (C#)</span></span>](./linq/linq-to-objects.md)
- [<span data-ttu-id="0b62c-228">Parallel LINQ (PLINQ)</span><span class="sxs-lookup"><span data-stu-id="0b62c-228">Parallel LINQ (PLINQ)</span></span>](../../../standard/parallel-programming/introduction-to-plinq.md)
- [<span data-ttu-id="0b62c-229">Raccolte e strutture di dati</span><span class="sxs-lookup"><span data-stu-id="0b62c-229">Collections and Data Structures</span></span>](../../../standard/collections/index.md)
- [<span data-ttu-id="0b62c-230">Selezione di una classe Collection</span><span class="sxs-lookup"><span data-stu-id="0b62c-230">Selecting a Collection Class</span></span>](../../../standard/collections/selecting-a-collection-class.md)
- [<span data-ttu-id="0b62c-231">Confronti e ordinamenti all'interno delle raccolte</span><span class="sxs-lookup"><span data-stu-id="0b62c-231">Comparisons and Sorts Within Collections</span></span>](../../../standard/collections/comparisons-and-sorts-within-collections.md)
- [<span data-ttu-id="0b62c-232">Quando utilizzare raccolte genericheWhen to Use Generic Collections</span><span class="sxs-lookup"><span data-stu-id="0b62c-232">When to Use Generic Collections</span></span>](../../../standard/collections/when-to-use-generic-collections.md)

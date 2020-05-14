---
title: Usare raccolte - Esercitazione introduttiva su C#
description: Imparare a usare C# esplorando la raccolta List in questa esercitazione.
ms.date: 10/13/2017
ms.custom: mvc
ms.openlocfilehash: c99f5582702120db238de1206de42d964837cdbd
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396888"
---
# <a name="learn-to-manage-data-collections-using-the-generic-list-type"></a><span data-ttu-id="2c42e-103">Informazioni su come gestire le raccolte dati tramite il tipo di elenco generico</span><span class="sxs-lookup"><span data-stu-id="2c42e-103">Learn to manage data collections using the generic list type</span></span>

<span data-ttu-id="2c42e-104">Questa esercitazione introduttiva offre un'introduzione al linguaggio C# e i concetti di base relativi alla classe <xref:System.Collections.Generic.List%601>.</span><span class="sxs-lookup"><span data-stu-id="2c42e-104">This introductory tutorial provides an introduction to the C# language and the basics of the <xref:System.Collections.Generic.List%601> class.</span></span>

<span data-ttu-id="2c42e-105">Questa esercitazione prevede la presenza di un computer da usare per lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="2c42e-105">This tutorial expects you to have a machine you can use for development.</span></span> <span data-ttu-id="2c42e-106">L'esercitazione .NET [Hello World in 10 minuti](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro) contiene le istruzioni per configurare l'ambiente di sviluppo locale in Windows, Linux o MacOS.</span><span class="sxs-lookup"><span data-stu-id="2c42e-106">The .NET tutorial [Hello World in 10 minutes](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro) has instructions for setting up your local development environment on Windows, Linux, or macOS.</span></span> <span data-ttu-id="2c42e-107">Una breve panoramica dei comandi usati è disponibile in [Acquisire familiarità con gli strumenti di sviluppo](local-environment.md), che contiene collegamenti a informazioni più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="2c42e-107">A quick overview of the commands you'll use is in [Become familiar with the development tools](local-environment.md), with links to more details.</span></span>

## <a name="a-basic-list-example"></a><span data-ttu-id="2c42e-108">Esempio di elenco di base</span><span class="sxs-lookup"><span data-stu-id="2c42e-108">A basic list example</span></span>

<span data-ttu-id="2c42e-109">Creare una directory denominata *list-tutorial*.</span><span class="sxs-lookup"><span data-stu-id="2c42e-109">Create a directory named *list-tutorial*.</span></span> <span data-ttu-id="2c42e-110">Impostarla come directory corrente ed eseguire `dotnet new console`.</span><span class="sxs-lookup"><span data-stu-id="2c42e-110">Make that the current directory and run `dotnet new console`.</span></span>

<span data-ttu-id="2c42e-111">Aprire *Program.cs* nell'editor preferito e sostituire il codice esistente con il seguente:</span><span class="sxs-lookup"><span data-stu-id="2c42e-111">Open *Program.cs* in your favorite editor, and replace the existing code with the following:</span></span>

```csharp
using System;
using System.Collections.Generic;

namespace list_tutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            var names = new List<string> { "<name>", "Ana", "Felipe" };
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }
        }
    }
}
```

<span data-ttu-id="2c42e-112">Sostituire `<name>` con il proprio nome.</span><span class="sxs-lookup"><span data-stu-id="2c42e-112">Replace `<name>` with your name.</span></span> <span data-ttu-id="2c42e-113">Salvare *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="2c42e-113">Save *Program.cs*.</span></span> <span data-ttu-id="2c42e-114">Digitare `dotnet run` nella finestra della console per provare il codice.</span><span class="sxs-lookup"><span data-stu-id="2c42e-114">Type `dotnet run` in your console window to try it.</span></span>

<span data-ttu-id="2c42e-115">Questo codice consente di creare un elenco di stringhe, aggiungere tre nomi all'elenco e stampare i nomi in lettere maiuscole.</span><span class="sxs-lookup"><span data-stu-id="2c42e-115">You've created a list of strings, added three names to that list, and printed out the names in all CAPS.</span></span> <span data-ttu-id="2c42e-116">Vengono usati i concetti appresi nelle esercitazioni precedenti per eseguire il ciclo dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2c42e-116">You're using concepts that you've learned in earlier tutorials to loop through the list.</span></span>

<span data-ttu-id="2c42e-117">Il codice per visualizzare i nomi usa la funzionalità di [interpolazione di stringhe](../../language-reference/tokens/interpolated.md).</span><span class="sxs-lookup"><span data-stu-id="2c42e-117">The code to display names makes use of the [string interpolation](../../language-reference/tokens/interpolated.md) feature.</span></span>  <span data-ttu-id="2c42e-118">Anteponendo il carattere `$` a `string`, è possibile incorporare il codice C# nella dichiarazione della stringa.</span><span class="sxs-lookup"><span data-stu-id="2c42e-118">When you precede a `string` with the `$` character, you can embed C# code in the string declaration.</span></span> <span data-ttu-id="2c42e-119">La stringa effettiva sostituisce il codice C# con il valore generato.</span><span class="sxs-lookup"><span data-stu-id="2c42e-119">The actual string replaces that C# code with the value it generates.</span></span> <span data-ttu-id="2c42e-120">In questo esempio, `{name.ToUpper()}` viene sostituito con ogni nome, convertito in lettere maiuscole, perché è stato chiamato il metodo <xref:System.String.ToUpper%2A>.</span><span class="sxs-lookup"><span data-stu-id="2c42e-120">In this example, it replaces the `{name.ToUpper()}` with each name, converted to capital letters, because you called the <xref:System.String.ToUpper%2A> method.</span></span>

<span data-ttu-id="2c42e-121">L'esplorazione continua nelle prossime lezioni.</span><span class="sxs-lookup"><span data-stu-id="2c42e-121">Let's keep exploring.</span></span>

## <a name="modify-list-contents"></a><span data-ttu-id="2c42e-122">Modificare il contenuto dell'elenco</span><span class="sxs-lookup"><span data-stu-id="2c42e-122">Modify list contents</span></span>

<span data-ttu-id="2c42e-123">La raccolta creata usa il tipo <xref:System.Collections.Generic.List%601>.</span><span class="sxs-lookup"><span data-stu-id="2c42e-123">The collection you created uses the <xref:System.Collections.Generic.List%601> type.</span></span> <span data-ttu-id="2c42e-124">Questo tipo archivia sequenze di elementi.</span><span class="sxs-lookup"><span data-stu-id="2c42e-124">This type stores sequences of elements.</span></span> <span data-ttu-id="2c42e-125">Il tipo degli elementi viene specificato tra parentesi uncinate.</span><span class="sxs-lookup"><span data-stu-id="2c42e-125">You specify the type of the elements between the angle brackets.</span></span>

<span data-ttu-id="2c42e-126">Un aspetto importante di questo tipo di <xref:System.Collections.Generic.List%601> è che supporta estensioni o riduzioni, consentendo l'aggiunta o la rimozione di elementi.</span><span class="sxs-lookup"><span data-stu-id="2c42e-126">One important aspect of this <xref:System.Collections.Generic.List%601> type is that it can grow or shrink, enabling you to add or remove elements.</span></span> <span data-ttu-id="2c42e-127">Aggiungere questo codice prima della parentesi `}` di chiusura nel metodo `Main`:</span><span class="sxs-lookup"><span data-stu-id="2c42e-127">Add this code before the closing `}` in the `Main` method:</span></span>

```csharp
Console.WriteLine();
names.Add("Maria");
names.Add("Bill");
names.Remove("Ana");
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

<span data-ttu-id="2c42e-128">Sono stati aggiunti altri due nomi alla fine dell'elenco</span><span class="sxs-lookup"><span data-stu-id="2c42e-128">You've added two more names to the end of the list.</span></span> <span data-ttu-id="2c42e-129">e ne è stato anche rimosso uno.</span><span class="sxs-lookup"><span data-stu-id="2c42e-129">You've also removed one as well.</span></span> <span data-ttu-id="2c42e-130">Salvare il file e digitare `dotnet run` per provare il codice.</span><span class="sxs-lookup"><span data-stu-id="2c42e-130">Save the file, and type `dotnet run` to try it.</span></span>

<span data-ttu-id="2c42e-131"><xref:System.Collections.Generic.List%601> consente di fare riferimento a singoli elementi anche in base all'**indice**.</span><span class="sxs-lookup"><span data-stu-id="2c42e-131">The <xref:System.Collections.Generic.List%601> enables you to reference individual items by **index** as well.</span></span> <span data-ttu-id="2c42e-132">Inserire l'indice tra i token `[` e `]` dopo il nome dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2c42e-132">You place the index between `[` and `]` tokens following the list name.</span></span> <span data-ttu-id="2c42e-133">C# usa il valore 0 per il primo indice.</span><span class="sxs-lookup"><span data-stu-id="2c42e-133">C# uses 0 for the first index.</span></span> <span data-ttu-id="2c42e-134">Aggiungere questo codice direttamente sotto il codice appena aggiunto e provarlo:</span><span class="sxs-lookup"><span data-stu-id="2c42e-134">Add this code directly below the code you just added and try it:</span></span>

```csharp
Console.WriteLine($"My name is {names[0]}");
Console.WriteLine($"I've added {names[2]} and {names[3]} to the list");
```

<span data-ttu-id="2c42e-135">Non è possibile accedere a un indice oltre la fine dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2c42e-135">You can't access an index beyond the end of the list.</span></span> <span data-ttu-id="2c42e-136">Tenere presente che gli indici iniziano da 0, pertanto l'indice massimo valido è minore di un'unità rispetto al numero di elementi nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2c42e-136">Remember that indices start at 0, so the largest valid index is one less than the number of items in the list.</span></span> <span data-ttu-id="2c42e-137">È possibile controllare la lunghezza dell'elenco tramite la proprietà <xref:System.Collections.Generic.List%601.Count%2A>.</span><span class="sxs-lookup"><span data-stu-id="2c42e-137">You can check how long the list is using the <xref:System.Collections.Generic.List%601.Count%2A> property.</span></span> <span data-ttu-id="2c42e-138">Aggiungere il codice seguente alla fine del metodo Main:</span><span class="sxs-lookup"><span data-stu-id="2c42e-138">Add the following code at the end of the Main method:</span></span>

```csharp
Console.WriteLine($"The list has {names.Count} people in it");
 ```

<span data-ttu-id="2c42e-139">Salvare il file e digitare di nuovo `dotnet run` per visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="2c42e-139">Save the file, and type `dotnet run` again to see the results.</span></span>

## <a name="search-and-sort-lists"></a><span data-ttu-id="2c42e-140">Eseguire ricerche negli elenchi e ordinarli</span><span class="sxs-lookup"><span data-stu-id="2c42e-140">Search and sort lists</span></span>

<span data-ttu-id="2c42e-141">In questi esempi vengono usati elenchi relativamente piccoli, ma le applicazioni reali creano spesso elenchi con molti più elementi, a volte anche migliaia.</span><span class="sxs-lookup"><span data-stu-id="2c42e-141">Our samples use relatively small lists, but your applications may often create lists with many more elements, sometimes numbering in the thousands.</span></span> <span data-ttu-id="2c42e-142">Per trovare elementi in raccolte di tali dimensioni, è necessario avere la possibilità di eseguire ricerche nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2c42e-142">To find elements in these larger collections, you need to search the list for different items.</span></span> <span data-ttu-id="2c42e-143">Il metodo <xref:System.Collections.Generic.List%601.IndexOf%2A> cerca un elemento e ne restituisce l'indice.</span><span class="sxs-lookup"><span data-stu-id="2c42e-143">The <xref:System.Collections.Generic.List%601.IndexOf%2A> method searches for an item and returns the index of the item.</span></span> <span data-ttu-id="2c42e-144">Se l'elemento non è presente nell'elenco, `IndexOf` restituisce `-1` .</span><span class="sxs-lookup"><span data-stu-id="2c42e-144">If the item isn't in the list, `IndexOf` returns `-1`.</span></span> <span data-ttu-id="2c42e-145">Aggiungere questo codice in fondo al metodo `Main`:</span><span class="sxs-lookup"><span data-stu-id="2c42e-145">Add this code to the bottom of your `Main` method:</span></span>

```csharp
var index = names.IndexOf("Felipe");
if (index == -1)
{
    Console.WriteLine($"When an item is not found, IndexOf returns {index}");
}
else
{
    Console.WriteLine($"The name {names[index]} is at index {index}");
}

index = names.IndexOf("Not Found");
if (index == -1)
{
    Console.WriteLine($"When an item is not found, IndexOf returns {index}");
}
else
{
    Console.WriteLine($"The name {names[index]} is at index {index}");

}
```

<span data-ttu-id="2c42e-146">Gli elementi in un elenco possono anche essere ordinati.</span><span class="sxs-lookup"><span data-stu-id="2c42e-146">The items in your list can be sorted as well.</span></span> <span data-ttu-id="2c42e-147">Il <xref:System.Collections.Generic.List%601.Sort%2A> metodo ordina in ordine normale tutti gli elementi dell'elenco (in ordine alfabetico per le stringhe).</span><span class="sxs-lookup"><span data-stu-id="2c42e-147">The <xref:System.Collections.Generic.List%601.Sort%2A> method sorts all the items in the list in their normal order (alphabetically for strings).</span></span> <span data-ttu-id="2c42e-148">Aggiungere questo codice in fondo al metodo `Main`:</span><span class="sxs-lookup"><span data-stu-id="2c42e-148">Add this code to the bottom of our `Main` method:</span></span>

```csharp
names.Sort();
foreach (var name in names)
{
    Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

<span data-ttu-id="2c42e-149">Salvare il file e digitare `dotnet run` per provare quest'ultima versione.</span><span class="sxs-lookup"><span data-stu-id="2c42e-149">Save the file and type `dotnet run` to try this latest version.</span></span>

<span data-ttu-id="2c42e-150">Prima di iniziare la sezione successiva, è necessario spostare il codice corrente in un metodo separato.</span><span class="sxs-lookup"><span data-stu-id="2c42e-150">Before you start the next section, let's move the current code into a separate method.</span></span> <span data-ttu-id="2c42e-151">In questo modo sarà più semplice iniziare a lavorare con un nuovo esempio.</span><span class="sxs-lookup"><span data-stu-id="2c42e-151">That makes it easier to start working with a new example.</span></span> <span data-ttu-id="2c42e-152">Rinominare il metodo `Main` in `WorkingWithStrings` e scrivere un nuovo metodo `Main` che chiama `WorkingWithStrings`.</span><span class="sxs-lookup"><span data-stu-id="2c42e-152">Rename your `Main` method to `WorkingWithStrings` and write a new `Main` method that calls `WorkingWithStrings`.</span></span> <span data-ttu-id="2c42e-153">Al termine, il codice dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2c42e-153">When you've finished, your code should look like this:</span></span>

```csharp
using System;
using System.Collections.Generic;

namespace list_tutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            WorkingWithStrings();
        }

        static void WorkingWithStrings()
        {
            var names = new List<string> { "<name>", "Ana", "Felipe" };
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }

            Console.WriteLine();
            names.Add("Maria");
            names.Add("Bill");
            names.Remove("Ana");
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }

            Console.WriteLine($"My name is {names[0]}");
            Console.WriteLine($"I've added {names[2]} and {names[3]} to the list");

            Console.WriteLine($"The list has {names.Count} people in it");

            var index = names.IndexOf("Felipe");
            if (index == -1)
            {
                Console.WriteLine($"When an item is not found, IndexOf returns {index}");
            }
            else
            {
                Console.WriteLine($"The name {names[index]} is at index {index}");
            }

            index = names.IndexOf("Not Found");
            if (index == -1)
            {
                Console.WriteLine($"When an item is not found, IndexOf returns {index}");
            }
            else
            {
                Console.WriteLine($"The name {names[index]} is at index {index}");

            }

            names.Sort();
            foreach (var name in names)
            {
                Console.WriteLine($"Hello {name.ToUpper()}!");
            }
        }
    }
}
```

## <a name="lists-of-other-types"></a><span data-ttu-id="2c42e-154">Elenchi di altri tipi</span><span class="sxs-lookup"><span data-stu-id="2c42e-154">Lists of other types</span></span>

<span data-ttu-id="2c42e-155">Finora è stato usato il tipo `string` negli elenchi.</span><span class="sxs-lookup"><span data-stu-id="2c42e-155">You've been using the `string` type in lists so far.</span></span> <span data-ttu-id="2c42e-156">Di seguito verrà creato un <xref:System.Collections.Generic.List%601> con un tipo diverso.</span><span class="sxs-lookup"><span data-stu-id="2c42e-156">Let's make a <xref:System.Collections.Generic.List%601> using a different type.</span></span> <span data-ttu-id="2c42e-157">Per iniziare, creare un set di numeri.</span><span class="sxs-lookup"><span data-stu-id="2c42e-157">Let's build a set of numbers.</span></span>

<span data-ttu-id="2c42e-158">Aggiungere il codice seguente alla fine del nuovo metodo `Main`:</span><span class="sxs-lookup"><span data-stu-id="2c42e-158">Add the following to the bottom of your new `Main` method:</span></span>

```csharp
var fibonacciNumbers = new List<int> {1, 1};
```

<span data-ttu-id="2c42e-159">Questo codice crea un elenco di interi e imposta i primi due interi sul valore 1.</span><span class="sxs-lookup"><span data-stu-id="2c42e-159">That creates a list of integers, and sets the first two integers to the value 1.</span></span> <span data-ttu-id="2c42e-160">Questi sono i primi due valori di una *successione di Fibonacci*, ovvero una sequenza di numeri.</span><span class="sxs-lookup"><span data-stu-id="2c42e-160">These are the first two values of a *Fibonacci Sequence*, a sequence of numbers.</span></span> <span data-ttu-id="2c42e-161">Ogni numero della successione di Fibonacci viene ottenuto dalla somma dei due numeri precedenti.</span><span class="sxs-lookup"><span data-stu-id="2c42e-161">Each next Fibonacci number is found by taking the sum of the previous two numbers.</span></span> <span data-ttu-id="2c42e-162">Aggiungere questo codice:</span><span class="sxs-lookup"><span data-stu-id="2c42e-162">Add this code:</span></span>

```csharp
var previous = fibonacciNumbers[fibonacciNumbers.Count - 1];
var previous2 = fibonacciNumbers[fibonacciNumbers.Count - 2];

fibonacciNumbers.Add(previous + previous2);

foreach (var item in fibonacciNumbers)
    Console.WriteLine(item);
```

<span data-ttu-id="2c42e-163">Salvare il file e digitare `dotnet run` per visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="2c42e-163">Save the file and type `dotnet run` to see the results.</span></span>

> [!TIP]
> <span data-ttu-id="2c42e-164">Per concentrarsi solo su questa sezione, è possibile impostare come commento il codice che chiama `WorkingWithStrings();`.</span><span class="sxs-lookup"><span data-stu-id="2c42e-164">To concentrate on just this section, you can comment out the code that calls `WorkingWithStrings();`.</span></span> <span data-ttu-id="2c42e-165">Inserire due caratteri `/` prima della chiamata come di seguito: `// WorkingWithStrings();`.</span><span class="sxs-lookup"><span data-stu-id="2c42e-165">Just put two `/` characters in front of the call like this:  `// WorkingWithStrings();`.</span></span>

## <a name="challenge"></a><span data-ttu-id="2c42e-166">Esercizio</span><span class="sxs-lookup"><span data-stu-id="2c42e-166">Challenge</span></span>

<span data-ttu-id="2c42e-167">È il momento di scoprire se è possibile mettere in pratica alcuni dei concetti appresi in questa lezione e in quelle precedenti.</span><span class="sxs-lookup"><span data-stu-id="2c42e-167">See if you can put together some of the concepts from this and earlier lessons.</span></span> <span data-ttu-id="2c42e-168">Applicare i concetti appresi finora in relazione ai numeri di Fibonacci.</span><span class="sxs-lookup"><span data-stu-id="2c42e-168">Expand on what you've built so far with Fibonacci Numbers.</span></span> <span data-ttu-id="2c42e-169">Provare a scrivere il codice per generare i primi 20 numeri nella successione.</span><span class="sxs-lookup"><span data-stu-id="2c42e-169">Try to write the code to generate the first 20 numbers in the sequence.</span></span> <span data-ttu-id="2c42e-170">Tenere presente che il 20° numero di Fibonacci è 6765.</span><span class="sxs-lookup"><span data-stu-id="2c42e-170">(As a hint, the 20th Fibonacci number is 6765.)</span></span>

## <a name="complete-challenge"></a><span data-ttu-id="2c42e-171">Completare l'esercizio</span><span class="sxs-lookup"><span data-stu-id="2c42e-171">Complete challenge</span></span>

<span data-ttu-id="2c42e-172">È possibile visualizzare una soluzione di esempio [esaminando il codice di esempio completato su GitHub](https://github.com/dotnet/samples/tree/master/csharp/list-quickstart/Program.cs#L13-L23).</span><span class="sxs-lookup"><span data-stu-id="2c42e-172">You can see an example solution by [looking at the finished sample code on GitHub](https://github.com/dotnet/samples/tree/master/csharp/list-quickstart/Program.cs#L13-L23).</span></span>

<span data-ttu-id="2c42e-173">A ogni iterazione del ciclo, gli ultimi due interi nell'elenco vengono sommati e il valore risultante viene aggiunto all'elenco.</span><span class="sxs-lookup"><span data-stu-id="2c42e-173">With each iteration of the loop, you're taking the last two integers in the list, summing them, and adding that value to the list.</span></span> <span data-ttu-id="2c42e-174">Il ciclo viene ripetuto fino ad aggiungere 20 elementi all'elenco.</span><span class="sxs-lookup"><span data-stu-id="2c42e-174">The loop repeats until you've added 20 items to the list.</span></span>

<span data-ttu-id="2c42e-175">Complimenti, è stata completata questa esercitazione dedicata agli elenchi.</span><span class="sxs-lookup"><span data-stu-id="2c42e-175">Congratulations, you've completed the list tutorial.</span></span> <span data-ttu-id="2c42e-176">È possibile continuare con l'esercitazione [Introduzione alle classi](introduction-to-classes.md) nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="2c42e-176">You can continue with the [Introduction to classes](introduction-to-classes.md) tutorial in your own development environment.</span></span>

<span data-ttu-id="2c42e-177">Per altre informazioni sull'uso del `List` tipo, vedere l'articolo della [Guida di .NET](../../../standard/index.yml) sulle [raccolte](../../../standard/collections/index.md).</span><span class="sxs-lookup"><span data-stu-id="2c42e-177">You can learn more about working with the `List` type in the [.NET guide](../../../standard/index.yml) article on [collections](../../../standard/collections/index.md).</span></span> <span data-ttu-id="2c42e-178">Questo argomento include anche informazioni su molti altri tipi di raccolta.</span><span class="sxs-lookup"><span data-stu-id="2c42e-178">You'll also learn about many other collection types.</span></span>

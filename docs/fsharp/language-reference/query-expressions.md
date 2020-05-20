---
title: Espressioni di query
description: 'Informazioni sul supporto delle espressioni di query per LINQ nel linguaggio di programmazione F #.'
ms.date: 05/16/2016
ms.openlocfilehash: bbd15352aa89bd1891b409177921a675784a0227
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83419187"
---
# <a name="query-expressions"></a><span data-ttu-id="36eee-103">Espressioni di query</span><span class="sxs-lookup"><span data-stu-id="36eee-103">Query Expressions</span></span>

> [!NOTE]
> <span data-ttu-id="36eee-104">I collegamenti di riferimento all'API in questo articolo portano a MSDN.</span><span class="sxs-lookup"><span data-stu-id="36eee-104">The API reference links in this article will take you to MSDN.</span></span>  <span data-ttu-id="36eee-105">Il riferimento all'API in Microsoft Docs (docs.microsoft.com) non è completo.</span><span class="sxs-lookup"><span data-stu-id="36eee-105">The docs.microsoft.com API reference is not complete.</span></span>

<span data-ttu-id="36eee-106">Le espressioni di query consentono di eseguire una query su un'origine dati e di inserire i dati nel formato desiderato.</span><span class="sxs-lookup"><span data-stu-id="36eee-106">Query expressions enable you to query a data source and put the data in a desired form.</span></span> <span data-ttu-id="36eee-107">Le espressioni di query forniscono supporto per LINQ in F #.</span><span class="sxs-lookup"><span data-stu-id="36eee-107">Query expressions provide support for LINQ in F#.</span></span>

## <a name="syntax"></a><span data-ttu-id="36eee-108">Sintassi</span><span class="sxs-lookup"><span data-stu-id="36eee-108">Syntax</span></span>

```fsharp
query { expression }
```

## <a name="remarks"></a><span data-ttu-id="36eee-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="36eee-109">Remarks</span></span>

<span data-ttu-id="36eee-110">Le espressioni di query sono un tipo di espressione di calcolo simile a espressioni di sequenza.</span><span class="sxs-lookup"><span data-stu-id="36eee-110">Query expressions are a type of computation expression similar to sequence expressions.</span></span> <span data-ttu-id="36eee-111">Così come si specifica una sequenza fornendo codice in un'espressione di sequenza, è possibile specificare un set di dati fornendo codice in un'espressione di query.</span><span class="sxs-lookup"><span data-stu-id="36eee-111">Just as you specify a sequence by providing code in a sequence expression, you specify a set of data by providing code in a query expression.</span></span> <span data-ttu-id="36eee-112">In un'espressione di sequenza la `yield` parola chiave identifica i dati da restituire come parte della sequenza risultante.</span><span class="sxs-lookup"><span data-stu-id="36eee-112">In a sequence expression, the `yield` keyword identifies data to be returned as part of the resulting sequence.</span></span> <span data-ttu-id="36eee-113">Nelle espressioni di query, la `select` parola chiave esegue la stessa funzione.</span><span class="sxs-lookup"><span data-stu-id="36eee-113">In query expressions, the `select` keyword performs the same function.</span></span> <span data-ttu-id="36eee-114">Oltre alla `select` parola chiave, F # supporta anche un numero di operatori di query che sono molto simili alle parti di un'istruzione SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="36eee-114">In addition to the `select` keyword, F# also supports a number of query operators that are much like the parts of a SQL SELECT statement.</span></span> <span data-ttu-id="36eee-115">Di seguito è riportato un esempio di un'espressione di query semplice, insieme al codice che si connette all'origine Northwind OData.</span><span class="sxs-lookup"><span data-stu-id="36eee-115">Here is an example of a simple query expression, along with code that connects to the Northwind OData source.</span></span>

```fsharp
// Use the OData type provider to create types that can be used to access the Northwind database.
// Add References to FSharp.Data.TypeProviders and System.Data.Services.Client
open Microsoft.FSharp.Data.TypeProviders

type Northwind = ODataService<"http://services.odata.org/Northwind/Northwind.svc">
let db = Northwind.GetDataContext()

// A query expression.
let query1 =
    query {
        for customer in db.Customers do
            select customer
    }

// Print results
query1
|> Seq.iter (fun customer -> printfn "Company: %s Contact: %s" customer.CompanyName customer.ContactName)
```

<span data-ttu-id="36eee-116">Nell'esempio di codice precedente, l'espressione di query è racchiusa tra parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="36eee-116">In the previous code example, the query expression is in curly braces.</span></span> <span data-ttu-id="36eee-117">Il significato del codice nell'espressione è, restituire ogni cliente nella tabella Customers del database nei risultati della query.</span><span class="sxs-lookup"><span data-stu-id="36eee-117">The meaning of the code in the expression is, return every customer in the Customers table in the database in the query results.</span></span> <span data-ttu-id="36eee-118">Le espressioni di query restituiscono un tipo che implementa <xref:System.Linq.IQueryable%601> e <xref:System.Collections.Generic.IEnumerable%601> , quindi è possibile eseguirne l'iterazione usando il [modulo Seq](https://msdn.microsoft.com/library/54e8f059-ca52-4632-9ae9-49685ee9b684) come illustrato nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="36eee-118">Query expressions return a type that implements <xref:System.Linq.IQueryable%601> and <xref:System.Collections.Generic.IEnumerable%601>, and so they can be iterated using the [Seq module](https://msdn.microsoft.com/library/54e8f059-ca52-4632-9ae9-49685ee9b684) as the example shows.</span></span>

<span data-ttu-id="36eee-119">Ogni tipo di espressione di calcolo viene compilato da una classe del generatore.</span><span class="sxs-lookup"><span data-stu-id="36eee-119">Every computation expression type is built from a builder class.</span></span> <span data-ttu-id="36eee-120">La classe Builder per l'espressione di calcolo della query è `QueryBuilder` .</span><span class="sxs-lookup"><span data-stu-id="36eee-120">The builder class for the query computation expression is `QueryBuilder`.</span></span> <span data-ttu-id="36eee-121">Per altre informazioni, vedere [espressioni di calcolo](computation-expressions.md) e [classe LINQ. QueryBuilder](https://msdn.microsoft.com/visualfsharpdocs/conceptual/linq.querybuilder-class-%5bfsharp%5d).</span><span class="sxs-lookup"><span data-stu-id="36eee-121">For more information, see [Computation Expressions](computation-expressions.md) and [Linq.QueryBuilder Class](https://msdn.microsoft.com/visualfsharpdocs/conceptual/linq.querybuilder-class-%5bfsharp%5d).</span></span>

## <a name="query-operators"></a><span data-ttu-id="36eee-122">Operatori di query</span><span class="sxs-lookup"><span data-stu-id="36eee-122">Query Operators</span></span>

<span data-ttu-id="36eee-123">Gli operatori di query consentono di specificare i dettagli della query, ad esempio di inserire criteri per i record da restituire, oppure di specificare l'ordinamento dei risultati.</span><span class="sxs-lookup"><span data-stu-id="36eee-123">Query operators enable you to specify the details of the query, such as to put criteria on records to be returned, or specify the sorting order of results.</span></span> <span data-ttu-id="36eee-124">L'origine della query deve supportare l'operatore di query.</span><span class="sxs-lookup"><span data-stu-id="36eee-124">The query source must support the query operator.</span></span> <span data-ttu-id="36eee-125">Se si tenta di utilizzare un operatore di query non supportato, `System.NotSupportedException` verrà generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="36eee-125">If you attempt to use an unsupported query operator, `System.NotSupportedException` will be thrown.</span></span>

<span data-ttu-id="36eee-126">Nelle espressioni di query sono consentite solo espressioni che possono essere convertite in SQL.</span><span class="sxs-lookup"><span data-stu-id="36eee-126">Only expressions that can be translated to SQL are allowed in query expressions.</span></span> <span data-ttu-id="36eee-127">Ad esempio, non sono consentite chiamate di funzione nelle espressioni quando si usa l' `where` operatore di query.</span><span class="sxs-lookup"><span data-stu-id="36eee-127">For example, no function calls are allowed in the expressions when you use the `where` query operator.</span></span>

<span data-ttu-id="36eee-128">La tabella 1 Mostra gli operatori di query disponibili.</span><span class="sxs-lookup"><span data-stu-id="36eee-128">Table 1 shows available query operators.</span></span> <span data-ttu-id="36eee-129">Vedere anche Table2, che confronta le query SQL e le espressioni di query F # equivalenti più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="36eee-129">In addition, see Table2, which compares SQL queries and the equivalent F# query expressions later in this topic.</span></span> <span data-ttu-id="36eee-130">Alcuni operatori di query non sono supportati da alcuni provider di tipi.</span><span class="sxs-lookup"><span data-stu-id="36eee-130">Some query operators aren't supported by some type providers.</span></span> <span data-ttu-id="36eee-131">In particolare, il provider di tipi OData è limitato negli operatori di query supportati a causa di limitazioni in OData.</span><span class="sxs-lookup"><span data-stu-id="36eee-131">In particular, the OData type provider is limited in the query operators that it supports due to limitations in OData.</span></span> <span data-ttu-id="36eee-132">Per ulteriori informazioni, vedere [provider di tipi ODataService (F #)](https://msdn.microsoft.com/library/bac609dd-9d12-4bf9-a662-24bdf4faa43e).</span><span class="sxs-lookup"><span data-stu-id="36eee-132">For more information, see [ODataService Type Provider (F#)](https://msdn.microsoft.com/library/bac609dd-9d12-4bf9-a662-24bdf4faa43e).</span></span>

<span data-ttu-id="36eee-133">In questa tabella si presuppone che il database sia nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="36eee-133">This table assumes a database in the following form:</span></span>

![Diagramma che mostra un database di esempio.](./media/query-expressions/student-course-database.png)

<span data-ttu-id="36eee-135">Il codice nelle tabelle che seguono presuppone anche il codice di connessione al database seguente.</span><span class="sxs-lookup"><span data-stu-id="36eee-135">The code in the tables that follow also assumes the following database connection code.</span></span> <span data-ttu-id="36eee-136">I progetti devono aggiungere riferimenti agli assembly System. Data, System. Data. Linq e FSharp. Data. TypeProviders.</span><span class="sxs-lookup"><span data-stu-id="36eee-136">Projects should add references to System.Data,  System.Data.Linq, and FSharp.Data.TypeProviders assemblies.</span></span> <span data-ttu-id="36eee-137">Il codice che crea il database è incluso alla fine di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="36eee-137">The code that creates this database is included at the end of this topic.</span></span>

```fsharp
open System
open Microsoft.FSharp.Data.TypeProviders
open System.Data.Linq.SqlClient
open System.Linq
open Microsoft.FSharp.Linq

type schema = SqlDataConnection< @"Data Source=SERVER\INSTANCE;Initial Catalog=MyDatabase;Integrated Security=SSPI;" >

let db = schema.GetDataContext()

// Needed for some query operator examples:
let data = [ 1; 5; 7; 11; 18; 21]
```

### <a name="table-1-query-operators"></a><span data-ttu-id="36eee-138">Tabella 1.</span><span class="sxs-lookup"><span data-stu-id="36eee-138">Table 1.</span></span> <span data-ttu-id="36eee-139">Operatori di query</span><span class="sxs-lookup"><span data-stu-id="36eee-139">Query Operators</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="36eee-140">Operatore</span><span class="sxs-lookup"><span data-stu-id="36eee-140">Operator</span></span></th>
    <th><span data-ttu-id="36eee-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="36eee-141">Description</span></span></th>
  </tr>
  <tr>
  <td><code>contains</code></td>
<td><span data-ttu-id="36eee-142">Determina se gli elementi selezionati includono un elemento specificato.</span><span class="sxs-lookup"><span data-stu-id="36eee-142">Determines whether the selected elements include a specified element.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    select student.Age.Value
    contains 11
}
</code></pre>

</td>
</tr>

<tr>
  <td><code>count</code></td><td><span data-ttu-id="36eee-143">Restituisce il numero di elementi selezionati.</span><span class="sxs-lookup"><span data-stu-id="36eee-143">Returns the number of selected elements.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    select student
    count
}
</code></pre>

</td></tr>
<tr>
<td><code>last</code></td><td><span data-ttu-id="36eee-144">Seleziona l'ultimo elemento di quelli selezionati finora.</span><span class="sxs-lookup"><span data-stu-id="36eee-144">Selects the last element of those selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for number in data do
    last
}
</code></pre>

</td></tr>
<tr>
<td><code>lastOrDefault</code></td><td><span data-ttu-id="36eee-145">Seleziona l'ultimo elemento di quelli selezionati finora o un valore predefinito se non viene trovato alcun elemento.</span><span class="sxs-lookup"><span data-stu-id="36eee-145">Selects the last element of those selected so far, or a default value if no element is found.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for number in data do
    where (number &lt; 0)
    lastOrDefault
}
</code></pre>

</td></tr><tr>
<td><code>exactlyOne</code></td><td><span data-ttu-id="36eee-146">Seleziona il singolo elemento specifico selezionato fino a questo momento.</span><span class="sxs-lookup"><span data-stu-id="36eee-146">Selects the single, specific element selected so far.</span></span> <span data-ttu-id="36eee-147">Se sono presenti più elementi, viene generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="36eee-147">If multiple elements are present, an exception is thrown.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where (student.StudentID = 1)
    select student
    exactlyOne
}
</code></pre>

</td></tr><tr>
<td><code>exactlyOneOrDefault</code></td><td><span data-ttu-id="36eee-148">Seleziona il singolo elemento specifico di quelli selezionati finora o un valore predefinito se tale elemento non viene trovato.</span><span class="sxs-lookup"><span data-stu-id="36eee-148">Selects the single, specific element of those selected so far, or a default value if that element is not found.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where (student.StudentID = 1)
    select student
    exactlyOneOrDefault
}
</code></pre>

</td></tr><tr>
<td><code>headOrDefault</code></td><td><span data-ttu-id="36eee-149">Seleziona il primo elemento di quelli selezionati finora o un valore predefinito se la sequenza non contiene elementi.</span><span class="sxs-lookup"><span data-stu-id="36eee-149">Selects the first element of those selected so far, or a default value if the sequence contains no elements.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    select student
    headOrDefault
}
</code></pre>

</td></tr><tr>
<td><code>select</code></td><td><span data-ttu-id="36eee-150">Proietta ogni elemento selezionato fino a questo momento.</span><span class="sxs-lookup"><span data-stu-id="36eee-150">Projects each of the elements selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    select student
}
</code></pre>

</td></tr><tr>
<td><code>where</code></td><td><span data-ttu-id="36eee-151">Seleziona gli elementi in base a un predicato specificato.</span><span class="sxs-lookup"><span data-stu-id="36eee-151">Selects elements based on a specified predicate.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where (student.StudentID > 4)
    select student
}
</code></pre>

</td></tr><tr>
<td><code>minBy</code></td><td><span data-ttu-id="36eee-152">Seleziona un valore per ogni elemento selezionato finora e restituisce il valore minimo risultante.</span><span class="sxs-lookup"><span data-stu-id="36eee-152">Selects a value for each element selected so far and returns the minimum resulting value.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    minBy student.StudentID
}
</code></pre>

</td></tr><tr>
<td><code>maxBy</code></td><td><span data-ttu-id="36eee-153">Seleziona un valore per ogni elemento selezionato finora e restituisce il valore massimo risultante.</span><span class="sxs-lookup"><span data-stu-id="36eee-153">Selects a value for each element selected so far and returns the maximum resulting value.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    maxBy student.StudentID
}
</code></pre>

</td></tr><tr>
<td><code>groupBy</code></td><td><span data-ttu-id="36eee-154">Raggruppa gli elementi selezionati finora in base a un selettore di chiave specificato.</span><span class="sxs-lookup"><span data-stu-id="36eee-154">Groups the elements selected so far according to a specified key selector.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    groupBy student.Age into g
    select (g.Key, g.Count())
}
</code></pre>

</td></tr><tr>
<td><code>sortBy</code></td><td><span data-ttu-id="36eee-155">Ordina gli elementi selezionati finora in ordine crescente in base alla chiave di ordinamento specificata.</span><span class="sxs-lookup"><span data-stu-id="36eee-155">Sorts the elements selected so far in ascending order by the given sorting key.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortBy student.Name
    select student
}
</code></pre>

</td></tr><tr>
<td><code>sortByDescending</code></td><td><span data-ttu-id="36eee-156">Ordina gli elementi selezionati finora in ordine decrescente in base alla chiave di ordinamento specificata.</span><span class="sxs-lookup"><span data-stu-id="36eee-156">Sorts the elements selected so far in descending order by the given sorting key.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortByDescending student.Name
    select student
}
</code></pre>

</td></tr><tr>
<td><code>thenBy</code></td><td><span data-ttu-id="36eee-157">Esegue un ordinamento successivo degli elementi selezionati finora in ordine crescente in base alla chiave di ordinamento specificata.</span><span class="sxs-lookup"><span data-stu-id="36eee-157">Performs a subsequent ordering of the elements selected so far in ascending order by the given sorting key.</span></span> <span data-ttu-id="36eee-158">Questo operatore può essere utilizzato solo dopo <code>sortBy</code> , <code>sortByDescending</code> , <code>thenBy</code> o <code>thenByDescending</code> .</span><span class="sxs-lookup"><span data-stu-id="36eee-158">This operator may only be used after a <code>sortBy</code>, <code>sortByDescending</code>, <code>thenBy</code>, or <code>thenByDescending</code>.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where student.Age.HasValue
    sortBy student.Age.Value
    thenBy student.Name
    select student
}
</code></pre>

</td></tr><tr>
<td><code>thenByDescending</code></td><td><span data-ttu-id="36eee-159">Esegue un ordinamento successivo degli elementi selezionati finora in ordine decrescente in base alla chiave di ordinamento specificata.</span><span class="sxs-lookup"><span data-stu-id="36eee-159">Performs a subsequent ordering of the elements selected so far in descending order by the given sorting key.</span></span> <span data-ttu-id="36eee-160">Questo operatore può essere utilizzato solo dopo <code>sortBy</code> , <code>sortByDescending</code> , <code>thenBy</code> o <code>thenByDescending</code> .</span><span class="sxs-lookup"><span data-stu-id="36eee-160">This operator may only be used after a <code>sortBy</code>, <code>sortByDescending</code>, <code>thenBy</code>, or <code>thenByDescending</code>.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where student.Age.HasValue
    sortBy student.Age.Value
    thenByDescending student.Name
    select student
}
</code></pre>

</td></tr><tr>
<td><code>groupValBy</code></td><td><span data-ttu-id="36eee-161">Seleziona un valore per ogni elemento selezionato fino a questo momento e raggruppa gli elementi in base alla chiave specificata.</span><span class="sxs-lookup"><span data-stu-id="36eee-161">Selects a value for each element selected so far and groups the elements by the given key.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    groupValBy student.Name student.Age into g
    select (g, g.Key, g.Count())
}
</code></pre>

</td></tr><tr>
<td><code>join</code></td><td><span data-ttu-id="36eee-162">Correla due set di valori selezionati in base alle chiavi corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="36eee-162">Correlates two sets of selected values based on matching keys.</span></span> <span data-ttu-id="36eee-163">Si noti che l'ordine delle chiavi intorno al segno = in un'espressione di join è significativo.</span><span class="sxs-lookup"><span data-stu-id="36eee-163">Note that the order of the keys around the = sign in a join expression is significant.</span></span> <span data-ttu-id="36eee-164">In tutti i join, se la riga viene divisa dopo il <code>-&gt;</code> simbolo, il rientro deve essere rientrato almeno per quanto riguarda la parola chiave <code>for</code> .</span><span class="sxs-lookup"><span data-stu-id="36eee-164">In all joins, if the line is split after the <code>-&gt;</code> symbol, the indentation must be indented at least as far as the keyword <code>for</code>.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    select (student, selection)
}
</code></pre>

</td></tr><tr>
<td><code>groupJoin</code></td><td><span data-ttu-id="36eee-165">Correla due set di valori selezionati in base alle chiavi corrispondenti e raggruppa i risultati.</span><span class="sxs-lookup"><span data-stu-id="36eee-165">Correlates two sets of selected values based on matching keys and groups the results.</span></span> <span data-ttu-id="36eee-166">Si noti che l'ordine delle chiavi intorno al segno = in un'espressione di join è significativo.</span><span class="sxs-lookup"><span data-stu-id="36eee-166">Note that the order of the keys around the = sign in a join expression is significant.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    groupJoin courseSelection in db.CourseSelection
        on (student.StudentID = courseSelection.StudentID) into g
    for courseSelection in g do
    join course in db.Course
        on (courseSelection.CourseID = course.CourseID)
    select (student.Name, course.CourseName)
}
</code></pre>

</td></tr><tr>
<td><code>leftOuterJoin</code></td><td><span data-ttu-id="36eee-167">Correla due set di valori selezionati in base alle chiavi corrispondenti e raggruppa i risultati.</span><span class="sxs-lookup"><span data-stu-id="36eee-167">Correlates two sets of selected values based on matching keys and groups the results.</span></span> <span data-ttu-id="36eee-168">Se un gruppo è vuoto, viene invece utilizzato un gruppo con un solo valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="36eee-168">If any group is empty, a group with a single default value is used instead.</span></span> <span data-ttu-id="36eee-169">Si noti che l'ordine delle chiavi intorno al segno = in un'espressione di join è significativo.</span><span class="sxs-lookup"><span data-stu-id="36eee-169">Note that the order of the keys around the = sign in a join expression is significant.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    leftOuterJoin selection in db.CourseSelection
        on (student.StudentID = selection.StudentID) into result
    for selection in result.DefaultIfEmpty() do
    select (student, selection)
}
</code></pre>

</td></tr><tr>
<td><code>sumByNullable</code></td><td><span data-ttu-id="36eee-170">Seleziona un valore Nullable per ogni elemento selezionato fino a questo momento e restituisce la somma di questi valori.</span><span class="sxs-lookup"><span data-stu-id="36eee-170">Selects a nullable value for each element selected so far and returns the sum of these values.</span></span> <span data-ttu-id="36eee-171">Se non è presente alcun valore Nullable, viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="36eee-171">If any nullable does not have a value, it is ignored.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sumByNullable student.Age
}
</code></pre>

</td></tr><tr>
<td><code>minByNullable</code></td><td><span data-ttu-id="36eee-172">Seleziona un valore Nullable per ogni elemento selezionato finora e restituisce il valore minimo di questi valori.</span><span class="sxs-lookup"><span data-stu-id="36eee-172">Selects a nullable value for each element selected so far and returns the minimum of these values.</span></span> <span data-ttu-id="36eee-173">Se non è presente alcun valore Nullable, viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="36eee-173">If any nullable does not have a value, it is ignored.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    minByNullable student.Age
}
</code></pre>

</td></tr><tr>
<td><code>maxByNullable</code></td><td><span data-ttu-id="36eee-174">Seleziona un valore Nullable per ogni elemento selezionato finora e restituisce il numero massimo di questi valori.</span><span class="sxs-lookup"><span data-stu-id="36eee-174">Selects a nullable value for each element selected so far and returns the maximum of these values.</span></span> <span data-ttu-id="36eee-175">Se non è presente alcun valore Nullable, viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="36eee-175">If any nullable does not have a value, it is ignored.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    maxByNullable student.Age
}
</code></pre>

</td></tr><tr>
<td><code>averageByNullable</code></td><td><span data-ttu-id="36eee-176">Seleziona un valore Nullable per ogni elemento selezionato finora e restituisce la media di questi valori.</span><span class="sxs-lookup"><span data-stu-id="36eee-176">Selects a nullable value for each element selected so far and returns the average of these values.</span></span> <span data-ttu-id="36eee-177">Se non è presente alcun valore Nullable, viene ignorato.</span><span class="sxs-lookup"><span data-stu-id="36eee-177">If any nullable does not have a value, it is ignored.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    averageByNullable (Nullable.float student.Age)
}
</code></pre>

</td></tr><tr>
<td><code>averageBy</code></td><td><span data-ttu-id="36eee-178">Seleziona un valore per ogni elemento selezionato finora e restituisce la media di questi valori.</span><span class="sxs-lookup"><span data-stu-id="36eee-178">Selects a value for each element selected so far and returns the average of these values.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    averageBy (float student.StudentID)
}
</code></pre>

</td></tr><tr>
<td><code>distinct</code></td><td><span data-ttu-id="36eee-179">Seleziona elementi distinti dagli elementi selezionati finora.</span><span class="sxs-lookup"><span data-stu-id="36eee-179">Selects distinct elements from the elements selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    distinct
}
</code></pre>

</td></tr><tr>
<td><code>exists</code></td><td><span data-ttu-id="36eee-180">Determina se un elemento selezionato fino a questo momento soddisfa una condizione.</span><span class="sxs-lookup"><span data-stu-id="36eee-180">Determines whether any element selected so far satisfies a condition.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where
        (query {
            for courseSelection in db.CourseSelection do
            exists (courseSelection.StudentID = student.StudentID) })
    select student
}
</code></pre>

</td></tr><tr>
<td><code>find</code></td><td><span data-ttu-id="36eee-181">Seleziona il primo elemento selezionato fino a quel momento che soddisfa una condizione specificata.</span><span class="sxs-lookup"><span data-stu-id="36eee-181">Selects the first element selected so far that satisfies a specified condition.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    find (student.Name = "Abercrombie, Kim")
}
</code></pre>

</td></tr><tr>
<td><code>all</code></td><td><span data-ttu-id="36eee-182">Determina se tutti gli elementi selezionati finora soddisfano una condizione.</span><span class="sxs-lookup"><span data-stu-id="36eee-182">Determines whether all elements selected so far satisfy a condition.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    all (SqlMethods.Like(student.Name, "%,%"))
}
</code></pre>

</td></tr><tr>
<td><code>head</code></td><td><span data-ttu-id="36eee-183">Seleziona il primo elemento da quelli selezionati finora.</span><span class="sxs-lookup"><span data-stu-id="36eee-183">Selects the first element from those selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    head
}
</code></pre>

</td></tr><tr>
<td><code>nth</code></td><td><span data-ttu-id="36eee-184">Seleziona l'elemento in corrispondenza di un indice specificato tra quelli selezionati finora.</span><span class="sxs-lookup"><span data-stu-id="36eee-184">Selects the element at a specified index amongst those selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for numbers in data do
    nth 3
}
</code></pre>

</td></tr><tr>
<td><code>skip</code></td><td><span data-ttu-id="36eee-185">Ignora un numero specificato di elementi selezionati fino a questo momento e quindi seleziona gli elementi rimanenti.</span><span class="sxs-lookup"><span data-stu-id="36eee-185">Bypasses a specified number of the elements selected so far and then selects the remaining elements.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    skip 1
}
</code></pre>

</td></tr><tr>
<td><code>skipWhile</code></td><td><span data-ttu-id="36eee-186">Ignora gli elementi in una sequenza finché una condizione specificata è true e quindi seleziona gli elementi rimanenti.</span><span class="sxs-lookup"><span data-stu-id="36eee-186">Bypasses elements in a sequence as long as a specified condition is true and then selects the remaining elements.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for number in data do
    skipWhile (number &lt; 3)
    select student
}
</code></pre>

</td></tr><tr>
<td><code>sumBy</code></td><td><span data-ttu-id="36eee-187">Seleziona un valore per ogni elemento selezionato fino a questo momento e restituisce la somma di questi valori.</span><span class="sxs-lookup"><span data-stu-id="36eee-187">Selects a value for each element selected so far and returns the sum of these values.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sumBy student.StudentID
}
</code></pre>

</td></tr><tr>
<td><code>take</code></td><td><span data-ttu-id="36eee-188">Seleziona un numero specificato di elementi contigui da quelli selezionati finora.</span><span class="sxs-lookup"><span data-stu-id="36eee-188">Selects a specified number of contiguous elements from those selected so far.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    select student
    take 2
}
</code></pre>

</td></tr><tr>
<td><code>takeWhile</code></td><td><span data-ttu-id="36eee-189">Seleziona gli elementi da una sequenza finché una condizione specificata è true e quindi ignora gli elementi rimanenti.</span><span class="sxs-lookup"><span data-stu-id="36eee-189">Selects elements from a sequence as long as a specified condition is true, and then skips the remaining elements.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for number in data do
    takeWhile (number &lt; 10)
}
</code></pre>

</td></tr><tr>
<td><code>sortByNullable</code></td><td><span data-ttu-id="36eee-190">Ordina gli elementi selezionati finora in ordine crescente in base alla chiave di ordinamento nullable specificata.</span><span class="sxs-lookup"><span data-stu-id="36eee-190">Sorts the elements selected so far in ascending order by the given nullable sorting key.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortByNullable student.Age
    select student
}
</code></pre>

</td></tr><tr>
<td><code>sortByNullableDescending</code></td><td><span data-ttu-id="36eee-191">Ordina gli elementi selezionati finora in ordine decrescente in base alla chiave di ordinamento nullable specificata.</span><span class="sxs-lookup"><span data-stu-id="36eee-191">Sorts the elements selected so far in descending order by the given nullable sorting key.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortByNullableDescending student.Age
    select student
}
</code></pre>

</td></tr><tr>
<td><code>thenByNullable</code></td><td><span data-ttu-id="36eee-192">Esegue un ordinamento successivo degli elementi selezionati finora in ordine crescente in base alla chiave di ordinamento nullable specificata.</span><span class="sxs-lookup"><span data-stu-id="36eee-192">Performs a subsequent ordering of the elements selected so far in ascending order by the given nullable sorting key.</span></span> <span data-ttu-id="36eee-193">Questo operatore può essere utilizzato solo immediatamente dopo un oggetto <code>sortBy</code> , <code>sortByDescending</code> , o o <code>thenBy</code> <code>thenByDescending</code> le varianti Nullable.</span><span class="sxs-lookup"><span data-stu-id="36eee-193">This operator may only be used immediately after a <code>sortBy</code>, <code>sortByDescending</code>, <code>thenBy</code>, or <code>thenByDescending</code>, or their nullable variants.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortBy student.Name
    thenByNullable student.Age
    select student
}
</code></pre>

</td></tr><tr>
<td><code>thenByNullableDescending</code></td><td><span data-ttu-id="36eee-194">Esegue un ordinamento successivo degli elementi selezionati finora in ordine decrescente in base alla chiave di ordinamento nullable specificata.</span><span class="sxs-lookup"><span data-stu-id="36eee-194">Performs a subsequent ordering of the elements selected so far in descending order by the given nullable sorting key.</span></span> <span data-ttu-id="36eee-195">Questo operatore può essere utilizzato solo immediatamente dopo un oggetto <code>sortBy</code> , <code>sortByDescending</code> , o o <code>thenBy</code> <code>thenByDescending</code> le varianti Nullable.</span><span class="sxs-lookup"><span data-stu-id="36eee-195">This operator may only be used immediately after a <code>sortBy</code>, <code>sortByDescending</code>, <code>thenBy</code>, or <code>thenByDescending</code>, or their nullable variants.</span></span><br/><br/>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    sortBy student.Name
    thenByNullableDescending student.Age
    select student
}
</code></pre>

</td></tr>
</table>

## <a name="comparison-of-transact-sql-and-f-query-expressions"></a><span data-ttu-id="36eee-196">Confronto tra espressioni di query Transact-SQL e F #</span><span class="sxs-lookup"><span data-stu-id="36eee-196">Comparison of Transact-SQL and F# Query Expressions</span></span>

<span data-ttu-id="36eee-197">Nella tabella seguente vengono illustrate alcune query Transact-SQL comuni e i relativi equivalenti in F #.</span><span class="sxs-lookup"><span data-stu-id="36eee-197">The following table shows some common Transact-SQL queries and their equivalents in F#.</span></span> <span data-ttu-id="36eee-198">Il codice in questa tabella presuppone anche lo stesso database della tabella precedente e lo stesso codice iniziale per configurare il provider di tipi.</span><span class="sxs-lookup"><span data-stu-id="36eee-198">The code in this table also assumes the same database as the previous table and the same initial code to set up the type provider.</span></span>

### <a name="table-2-transact-sql-and-f-query-expressions"></a><span data-ttu-id="36eee-199">Tabella 2.</span><span class="sxs-lookup"><span data-stu-id="36eee-199">Table 2.</span></span> <span data-ttu-id="36eee-200">Espressioni di query Transact-SQL e F #</span><span class="sxs-lookup"><span data-stu-id="36eee-200">Transact-SQL and F# Query Expressions</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="36eee-201">Transact-SQL (senza distinzione tra maiuscole e minuscole)</span><span class="sxs-lookup"><span data-stu-id="36eee-201">Transact-SQL (not case sensitive)</span></span></th>
    <th><span data-ttu-id="36eee-202">Espressione di query F # (maiuscole/minuscole)</span><span class="sxs-lookup"><span data-stu-id="36eee-202">F# Query Expression (case sensitive)</span></span></th>
  </tr>
<tr><td>
<span data-ttu-id="36eee-203">Selezionare tutti i campi dalla tabella.</span><span class="sxs-lookup"><span data-stu-id="36eee-203">Select all fields from table.</span></span><br>

<pre><code class="lang-sql">SELECT * FROM Student
</code></pre>

</td><td>
<pre><code class="lang-fsharp">// All students.
query {
    for student in db.Student do
    select student
}
</code></pre>

</td></tr>
<tr><td>
<span data-ttu-id="36eee-204">Conteggio di record in una tabella.</span><span class="sxs-lookup"><span data-stu-id="36eee-204">Count records in a table.</span></span><br/>

<pre><code class="lang-sql">SELECT COUNT( * ) FROM Student
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Count of students.
query {
    for student in db.Student do
    count
}
</code></pre>

</td></tr><tr>
<td><code>EXISTS</code>
<br />

<!-- markdownlint-capture -->
<!-- markdownlint-disable no-space-in-emphasis -->
<pre><code class="lang-sql">SELECT * FROM Student
WHERE EXISTS
  (SELECT * FROM CourseSelection
   WHERE CourseSelection.StudentID = Student.StudentID)
</code></pre>
<!-- markdownlint-restore -->
</td>

<td>

<pre><code class="lang-fsharp">// Find students who have signed up at least one course.
query {
    for student in db.Student do
    where
        (query {
            for courseSelection in db.CourseSelection do
            exists (courseSelection.StudentID = student.StudentID) })
    select student
}
</code></pre>

</td></tr><tr>
<td><span data-ttu-id="36eee-205">Raggruppamento</span><span class="sxs-lookup"><span data-stu-id="36eee-205">Grouping</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Age, COUNT( * ) FROM Student
GROUP BY Student.Age
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Group by age and count.
query {
    for n in db.Student do
    groupBy n.Age into g
    select (g.Key, g.Count())
}
// OR
query {
    for n in db.Student do
    groupValBy n.Age n.Age into g
    select (g.Key, g.Count())
}
</code></pre>
</td></tr><tr><td>
<span data-ttu-id="36eee-206">Raggruppamento con condizione.</span><span class="sxs-lookup"><span data-stu-id="36eee-206">Grouping with condition.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Age, COUNT( * )
FROM Student
GROUP BY Student.Age
HAVING student.Age > 10
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Group students by age where age > 10.
query {
    for student in db.Student do
    groupBy student.Age into g
    where (g.Key.HasValue && g.Key.Value > 10)
    select (g.Key, g.Count())
}
</code></pre>

</td></tr><tr><td>
<span data-ttu-id="36eee-207">Raggruppamento con la condizione Count.</span><span class="sxs-lookup"><span data-stu-id="36eee-207">Grouping with count condition.</span></span><br/>

<!-- markdownlint-capture -->
<!-- markdownlint-disable no-space-in-emphasis -->
<pre><code class="lang-sql">SELECT Student.Age, COUNT( * )
FROM Student
GROUP BY Student.Age
HAVING COUNT( * ) > 1
</code></pre>
<!-- markdownlint-restore -->

</td><td>

<pre><code class="lang-fsharp">// Group students by age and count number of students
// at each age with more than 1 student.
query {
    for student in db.Student do
    groupBy student.Age into group
    where (group.Count() > 1)
    select (group.Key, group.Count())
}
</code></pre>

</td></tr><tr><td>
<span data-ttu-id="36eee-208">Raggruppamento, conteggio e somma.</span><span class="sxs-lookup"><span data-stu-id="36eee-208">Grouping, counting, and summing.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Age, COUNT( * ), SUM(Student.Age) as total
FROM Student
GROUP BY Student.Age
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Group students by age and sum ages.
query {
    for student in db.Student do
    groupBy student.Age into g
    let total =
        query {
            for student in g do
            sumByNullable student.Age
        }
    select (g.Key, g.Count(), total)
}
</code></pre>

</td></tr><tr><td>
<span data-ttu-id="36eee-209">Raggruppamento, conteggio e ordinamento in base al conteggio.</span><span class="sxs-lookup"><span data-stu-id="36eee-209">Grouping, counting, and ordering by count.</span></span><br/>

<!-- markdownlint-capture -->
<!-- markdownlint-disable no-space-in-emphasis -->
<pre><code class="lang-sql">SELECT Student.Age, COUNT( * ) as myCount
FROM Student
GROUP BY Student.Age
HAVING COUNT( * ) > 1
ORDER BY COUNT( * ) DESC
</code></pre>
<!-- markdownlint-restore -->

</td><td>

<pre><code class="lang-fsharp">// Group students by age, count number of students
// at each age, and display all with count > 1
// in descending order of count.
query {
    for student in db.Student do
    groupBy student.Age into g
    where (g.Count() > 1)
    sortByDescending (g.Count())
    select (g.Key, g.Count())
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-210">
<code>IN</code>set di valori specificati</span><span class="sxs-lookup"><span data-stu-id="36eee-210">
<code>IN</code> a set of specified values</span></span><br/>

<pre><code class="lang-sql">SELECT *
FROM Student
WHERE Student.StudentID IN (1, 2, 5, 10)
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Select students where studentID is one of a given list.
let idQuery =
    query {
        for id in [1; 2; 5; 10] do
        select id
    }
query {
    for student in db.Student do
    where (idQuery.Contains(student.StudentID))
    select student
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-211">
<code>LIKE</code> e <code>TOP</code>.</span><span class="sxs-lookup"><span data-stu-id="36eee-211">
<code>LIKE</code> and <code>TOP</code>.</span></span><br/>

<pre><code class="lang-sql">-- '_e%' matches strings where the second character is 'e'
SELECT TOP 2 * FROM Student
WHERE Student.Name LIKE '_e%'
</code></pre>

</td><td>
<pre><code class="lang-fsharp">// Look for students with Name match _e% pattern and take first two.
query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "_e%") )
    select student
    take 2
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-212">
<code>LIKE</code>con set di corrispondenze dei criteri.</span><span class="sxs-lookup"><span data-stu-id="36eee-212">
<code>LIKE</code> with pattern match set.</span></span><br/>

<pre><code class="lang-sql">-- '[abc]%' matches strings where the first character is
-- 'a', 'b', 'c', 'A', 'B', or 'C'
SELECT * FROM Student
WHERE Student.Name LIKE '[abc]%'
</code></pre>
</td><td>

<pre><code class="lang-fsharp">query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "[abc]%") )
    select student
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-213">
<code>LIKE</code>con il modello di esclusione set.</span><span class="sxs-lookup"><span data-stu-id="36eee-213">
<code>LIKE</code> with set exclusion pattern.</span></span><br/>

<pre><code class="lang-sql">-- '[^abc]%' matches strings where the first character is
-- not 'a', 'b', 'c', 'A', 'B', or 'C'
SELECT * FROM Student
WHERE Student.Name LIKE '[^abc]%'
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Look for students with name matching [^abc]%% pattern.
query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "[^abc]%") )
    select student
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-214">
<code>LIKE</code>in un campo, ma selezionare un campo diverso.</span><span class="sxs-lookup"><span data-stu-id="36eee-214">
<code>LIKE</code> on one field, but select a different field.</span></span><br/>

<pre><code class="lang-sql">SELECT StudentID AS ID FROM Student
WHERE Student.Name LIKE '[^abc]%'
</code></pre>

</td><td>

<pre><code class="lang-fsharp">query {
    for n in db.Student do
    where (SqlMethods.Like( n.Name, "[^abc]%") )
    select n.StudentID
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-215"><code>LIKE</code>, con ricerca di sottostringhe.</span><span class="sxs-lookup"><span data-stu-id="36eee-215"><code>LIKE</code>, with substring search.</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student
WHERE Student.Name like '%A%'
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Using Contains as a query filter.
query {
    for student in db.Student do
    where (student.Name.Contains("a"))
    select student
}
</code></pre>

</td></tr><tr><td>
<span data-ttu-id="36eee-216">Semplice <code>JOIN</code> con due tabelle.</span><span class="sxs-lookup"><span data-stu-id="36eee-216">Simple <code>JOIN</code> with two tables.</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student
JOIN CourseSelection
ON Student.StudentID = CourseSelection.StudentID
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Join Student and CourseSelection tables.
query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    select (student, selection)
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-217"><code>LEFT JOIN</code>con due tabelle.</span><span class="sxs-lookup"><span data-stu-id="36eee-217"><code>LEFT JOIN</code> with two tables.</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student
LEFT JOIN CourseSelection
ON Student.StudentID = CourseSelection.StudentID
</code></pre>

</td><td>

<pre><code class="lang-fsharp">//Left Join Student and CourseSelection tables.
query {
    for student in db.Student do
    leftOuterJoin selection in db.CourseSelection
        on (student.StudentID = selection.StudentID) into result
    for selection in result.DefaultIfEmpty() do
    select (student, selection)
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-218"><code>JOIN</code> con <code>COUNT</code></span><span class="sxs-lookup"><span data-stu-id="36eee-218"><code>JOIN</code> with <code>COUNT</code></span></span><br/>

<pre><code class="lang-sql">SELECT COUNT( * ) FROM Student
JOIN CourseSelection
ON Student.StudentID = CourseSelection.StudentID
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Join with count.
query {
    for n in db.Student do
    join e in db.CourseSelection
        on (n.StudentID = e.StudentID)
    count
}
</code></pre>

</td></tr><tr><td><code>DISTINCT</code><br/>

<pre><code class="lang-sql">SELECT DISTINCT StudentID FROM CourseSelection
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Join with distinct.
query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    distinct
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-219">Distinct Count.</span><span class="sxs-lookup"><span data-stu-id="36eee-219">Distinct count.</span></span><br/>

<pre><code class="lang-sql">SELECT DISTINCT COUNT(StudentID) FROM CourseSelection
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Join with distinct and count.
query {
    for n in db.Student do
    join e in db.CourseSelection
        on (n.StudentID = e.StudentID)
    distinct
    count
}
</code></pre>

</td></tr><tr><td><code>BETWEEN</code><br/>

<pre><code class="lang-sql">SELECT * FROM Student
WHERE Student.Age BETWEEN 10 AND 15
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Selecting students with ages between 10 and 15.
query {
    for student in db.Student do
    where (student.Age ?>= 10 && student.Age ?&lt; 15)
    select student
}
</code></pre>

</td></tr><tr><td><code>OR</code><br/>

<pre><code class="lang-sql">SELECT * FROM Student
WHERE Student.Age = 11 OR Student.Age = 12
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Selecting students with age that's either 11 or 12.
query {
    for student in db.Student do
    where (student.Age.Value = 11 &#124;&#124; student.Age.Value = 12)
    select student
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-220"><code>OR</code>con ordinamento</span><span class="sxs-lookup"><span data-stu-id="36eee-220"><code>OR</code> with ordering</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student
WHERE Student.Age = 12 OR Student.Age = 13
ORDER BY Student.Age DESC
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Selecting students in a certain age range and sorting.
query {
    for n in db.Student do
    where (n.Age.Value = 12 &#124;&#124; n.Age.Value = 13)
    sortByNullableDescending n.Age
    select n
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-221"><code>TOP</code>, <code>OR</code> e ordinamento.</span><span class="sxs-lookup"><span data-stu-id="36eee-221"><code>TOP</code>, <code>OR</code>, and ordering.</span></span><br/>

<pre><code class="lang-sql">SELECT TOP 2 student.Name FROM Student
WHERE Student.Age = 11 OR Student.Age = 12
ORDER BY Student.Name DESC
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Selecting students with certain ages,
// taking account of the possibility of nulls.
query {
    for student in db.Student do
    where
        ((student.Age.HasValue && student.Age.Value = 11) &#124;&#124;
         (student.Age.HasValue && student.Age.Value = 12))
    sortByDescending student.Name
    select student.Name
    take 2
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-222"><code>UNION</code>di due query.</span><span class="sxs-lookup"><span data-stu-id="36eee-222"><code>UNION</code> of two queries.</span></span><br/>

<!-- markdownlint-capture -->
<!-- markdownlint-disable no-space-in-emphasis -->
<pre><code class="lang-sql">SELECT * FROM Student
UNION
SELECT * FROM lastStudent
</code></pre>
<!-- markdownlint-restore -->

</td><td>

<pre><code class="lang-fsharp">
let query1 =
    query {
        for n in db.Student do
        select (n.Name, n.Age)
    }

let query2 =
    query {
        for n in db.LastStudent do
        select (n.Name, n.Age)
    }

query2.Union (query1)
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-223">Intersezione di due query.</span><span class="sxs-lookup"><span data-stu-id="36eee-223">Intersection of two queries.</span></span><br/>

<!-- markdownlint-capture -->
<!-- markdownlint-disable no-space-in-emphasis -->
<pre><code class="lang-sql">SELECT * FROM Student
INTERSECT
SELECT * FROM LastStudent
</code></pre>
<!-- markdownlint-restore -->
</td><td>

<pre><code class="lang-fsharp">
let query1 =
    query {
        for n in db.Student do
        select (n.Name, n.Age)
    }

let query2 =
    query {
        for n in db.LastStudent do
        select (n.Name, n.Age)
    }

query1.Intersect(query2)
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-224"><code>CASE</code>condizione.</span><span class="sxs-lookup"><span data-stu-id="36eee-224"><code>CASE</code> condition.</span></span><br/>

<pre><code class="lang-sql">SELECT student.StudentID,
CASE Student.Age
  WHEN -1 THEN 100
  ELSE Student.Age
END,
Student.Age
FROM Student
</code></pre>

</td><td>
<pre><code class="lang-fsharp">// Using if statement to alter results for special value.
query {
    for student in db.Student do
    select
        (if student.Age.HasValue && student.Age.Value = -1 then
             (student.StudentID, System.Nullable&lt;int&gt;(100), student.Age)
         else (student.StudentID, student.Age, student.Age))
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-225">Più case.</span><span class="sxs-lookup"><span data-stu-id="36eee-225">Multiple cases.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.StudentID,
CASE Student.Age
  WHEN -1 THEN 100
  WHEN 0 THEN 1000
  ELSE Student.Age
END,
Student.Age
FROM Student
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Using if statement to alter results for special values.
query {
    for student in db.Student do
    select
        (if student.Age.HasValue && student.Age.Value = -1 then
             (student.StudentID, System.Nullable&lt;int&gt;(100), student.Age)
         elif student.Age.HasValue && student.Age.Value = 0 then
             (student.StudentID, System.Nullable&lt;int&gt;(1000), student.Age)
         else (student.StudentID, student.Age, student.Age))
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-226">Più tabelle.</span><span class="sxs-lookup"><span data-stu-id="36eee-226">Multiple tables.</span></span><br/>

<pre><code class="lang-sql">SELECT * FROM Student, Course
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Multiple table select.
query {
    for student in db.Student do
    for course in db.Course do
    select (student, course)
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-227">Join multipli.</span><span class="sxs-lookup"><span data-stu-id="36eee-227">Multiple joins.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Name, Course.CourseName
FROM Student
JOIN CourseSelection
ON CourseSelection.StudentID = Student.StudentID
JOIN Course
ON Course.CourseID = CourseSelection.CourseID
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Multiple joins.
query {
    for student in db.Student do
    join courseSelection in db.CourseSelection
        on (student.StudentID = courseSelection.StudentID)
    join course in db.Course
        on (courseSelection.CourseID = course.CourseID)
    select (student.Name, course.CourseName)
}
</code></pre>

</td></tr><tr><td><span data-ttu-id="36eee-228">Più left outer join.</span><span class="sxs-lookup"><span data-stu-id="36eee-228">Multiple left outer joins.</span></span><br/>

<pre><code class="lang-sql">SELECT Student.Name, Course.CourseName
FROM Student
LEFT OUTER JOIN CourseSelection
ON CourseSelection.StudentID = Student.StudentID
LEFT OUTER JOIN Course
ON Course.CourseID = CourseSelection.CourseID
</code></pre>

</td><td>

<pre><code class="lang-fsharp">// Using leftOuterJoin with multiple joins.
query {
    for student in db.Student do
    leftOuterJoin courseSelection in db.CourseSelection
        on (student.StudentID = courseSelection.StudentID) into g1
    for courseSelection in g1.DefaultIfEmpty() do
    leftOuterJoin course in db.Course
        on (courseSelection.CourseID = course.CourseID) into g2
    for course in g2.DefaultIfEmpty() do
    select (student.Name, course.CourseName)
}
</code></pre>

</td></tr></table>

<span data-ttu-id="36eee-229">Il codice seguente può essere utilizzato per creare il database di esempio per questi esempi.</span><span class="sxs-lookup"><span data-stu-id="36eee-229">The following code can be used to create the sample database for these examples.</span></span>

<pre><code class="lang-sql">SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

USE [master];
GO

IF EXISTS (SELECT * FROM sys.databases WHERE name = 'MyDatabase')
DROP DATABASE MyDatabase;
GO

-- Create the MyDatabase database.
CREATE DATABASE MyDatabase COLLATE SQL_Latin1_General_CP1_CI_AS;
GO

-- Specify a simple recovery model
-- to keep the log growth to a minimum.
ALTER DATABASE MyDatabase
SET RECOVERY SIMPLE;
GO

USE MyDatabase;
GO

CREATE TABLE [dbo].[Course] (
[CourseID]   INT           NOT NULL,
[CourseName] NVARCHAR (50) NOT NULL,
PRIMARY KEY CLUSTERED ([CourseID] ASC)
);

CREATE TABLE [dbo].[Student] (
[StudentID] INT           NOT NULL,
[Name]      NVARCHAR (50) NOT NULL,
[Age]       INT           NULL,
PRIMARY KEY CLUSTERED ([StudentID] ASC)
);

CREATE TABLE [dbo].[CourseSelection] (
[ID]        INT NOT NULL,
[StudentID] INT NOT NULL,
[CourseID]  INT NOT NULL,
PRIMARY KEY CLUSTERED ([ID] ASC),
CONSTRAINT [FK_CourseSelection_ToTable] FOREIGN KEY ([StudentID]) REFERENCES [dbo].[Student] ([StudentID]) ON DELETE NO ACTION ON UPDATE NO ACTION,
CONSTRAINT [FK_CourseSelection_Course_1] FOREIGN KEY ([CourseID]) REFERENCES [dbo].[Course] ([CourseID]) ON DELETE NO ACTION ON UPDATE NO ACTION
);

CREATE TABLE [dbo].[LastStudent] (
[StudentID] INT           NOT NULL,
[Name]      NVARCHAR (50) NOT NULL,
[Age]       INT           NULL,
PRIMARY KEY CLUSTERED ([StudentID] ASC)
);

-- Insert data into the tables.
USE MyDatabase
INSERT INTO Course (CourseID, CourseName)
VALUES(1, 'Algebra I');
INSERT INTO Course (CourseID, CourseName)
VALUES(2, 'Trigonometry');
INSERT INTO Course (CourseID, CourseName)
VALUES(3, 'Algebra II');
INSERT INTO Course (CourseID, CourseName)
VALUES(4, 'History');
INSERT INTO Course (CourseID, CourseName)
VALUES(5, 'English');
INSERT INTO Course (CourseID, CourseName)
VALUES(6, 'French');
INSERT INTO Course (CourseID, CourseName)
VALUES(7, 'Chinese');

INSERT INTO Student (StudentID, Name, Age)
VALUES(1, 'Abercrombie, Kim', 10);
INSERT INTO Student (StudentID, Name, Age)
VALUES(2, 'Abolrous, Hazen', 14);
INSERT INTO Student (StudentID, Name, Age)
VALUES(3, 'Hance, Jim', 12);
INSERT INTO Student (StudentID, Name, Age)
VALUES(4, 'Adams, Terry', 12);
INSERT INTO Student (StudentID, Name, Age)
VALUES(5, 'Hansen, Claus', 11);
INSERT INTO Student (StudentID, Name, Age)
VALUES(6, 'Penor, Lori', 13);
INSERT INTO Student (StudentID, Name, Age)
VALUES(7, 'Perham, Tom', 12);
INSERT INTO Student (StudentID, Name, Age)
VALUES(8, 'Peng, Yun-Feng', NULL);

INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(1, 1, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(2, 1, 3);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(3, 1, 5);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(4, 2, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(5, 2, 5);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(6, 2, 6);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(7, 2, 3);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(8, 3, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(9, 3, 1);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(10, 4, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(11, 4, 5);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(12, 4, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(13, 5, 3);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(14, 5, 2);
INSERT INTO CourseSelection (ID, StudentID, CourseID)
VALUES(15, 7, 3);
</code></pre>

<span data-ttu-id="36eee-230">Il codice seguente contiene il codice di esempio visualizzato in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="36eee-230">The following code contains  the sample code that appears in this topic.</span></span>

```fsharp
#if INTERACTIVE
#r "FSharp.Data.TypeProviders.dll"
#r "System.Data.dll"
#r "System.Data.Linq.dll"
#endif
open System
open Microsoft.FSharp.Data.TypeProviders
open System.Data.Linq.SqlClient
open System.Linq

type schema = SqlDataConnection<"Data Source=SERVER\INSTANCE;Initial Catalog=MyDatabase;Integrated Security=SSPI;">

let db = schema.GetDataContext()

let data = [1; 5; 7; 11; 18; 21]

type Nullable<'T when 'T : ( new : unit -> 'T) and 'T : struct and 'T :> ValueType > with
    member this.Print() =
        if this.HasValue then this.Value.ToString()
        else "NULL"

printfn "\ncontains query operator"
query {
    for student in db.Student do
    select student.Age.Value
    contains 11
}
|> printfn "Is at least one student age 11? %b"

printfn "\ncount query operator"
query {
    for student in db.Student do
    select student
    count
}
|> printfn "Number of students: %d"

printfn "\nlast query operator."
let num =
    query {
        for number in data do
        sortBy number
        last
    }
printfn "Last number: %d" num

open Microsoft.FSharp.Linq

printfn "\nlastOrDefault query operator."
query {
    for number in data do
    sortBy number
    lastOrDefault
}
|> printfn "lastOrDefault: %d"

printfn "\nexactlyOne query operator."
let student2 =
    query {
        for student in db.Student do
        where (student.StudentID = 1)
        select student
        exactlyOne
    }
printfn "Student with StudentID = 1 is %s" student2.Name

printfn "\nexactlyOneOrDefault query operator."
let student3 =
    query {
        for student in db.Student do
        where (student.StudentID = 1)
        select student
        exactlyOneOrDefault
    }
printfn "Student with StudentID = 1 is %s" student3.Name

printfn "\nheadOrDefault query operator."
let student4 =
    query {
        for student in db.Student do
        select student
        headOrDefault
    }
printfn "head student is %s" student4.Name

printfn "\nselect query operator."
query {
    for student in db.Student do
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.StudentID student.Name)

printfn "\nwhere query operator."
query {
    for student in db.Student do
    where (student.StudentID > 4)
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.StudentID student.Name)

printfn "\nminBy query operator."
let student5 =
    query {
        for student in db.Student do
        minBy student.StudentID
    }

printfn "\nmaxBy query operator."
let student6 =
    query {
        for student in db.Student do
        maxBy student.StudentID
    }

printfn "\ngroupBy query operator."
query {
    for student in db.Student do
    groupBy student.Age into g
    select (g.Key, g.Count())
}
|> Seq.iter (fun (age, count) -> printfn "Age: %s Count at that age: %d" (age.Print()) count)

printfn "\nsortBy query operator."
query {
    for student in db.Student do
    sortBy student.Name
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.StudentID student.Name)

printfn "\nsortByDescending query operator."
query {
    for student in db.Student do
    sortByDescending student.Name
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.StudentID student.Name)

printfn "\nthenBy query operator."
query {
    for student in db.Student do
    where student.Age.HasValue
    sortBy student.Age.Value
    thenBy student.Name
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.Age.Value student.Name)

printfn "\nthenByDescending query operator."
query {
    for student in db.Student do
    where student.Age.HasValue
    sortBy student.Age.Value
    thenByDescending student.Name
    select student
}
|> Seq.iter (fun student -> printfn "StudentID, Name: %d %s" student.Age.Value student.Name)

printfn "\ngroupValBy query operator."
query {
    for student in db.Student do
    groupValBy student.Name student.Age into g
    select (g, g.Key, g.Count())
}
|> Seq.iter (fun (group, age, count) ->
    printfn "Age: %s Count at that age: %d" (age.Print()) count
    group |> Seq.iter (fun name -> printfn "Name: %s" name))

printfn "\n sumByNullable query operator"
query {
    for student in db.Student do
    sumByNullable student.Age
}
|> (fun sum -> printfn "Sum of ages: %s" (sum.Print()))

printfn "\n minByNullable"
query {
    for student in db.Student do
    minByNullable student.Age
}
|> (fun age -> printfn "Minimum age: %s" (age.Print()))

printfn "\n maxByNullable"
query {
    for student in db.Student do
    maxByNullable student.Age
}
|> (fun age -> printfn "Maximum age: %s" (age.Print()))

printfn "\n averageBy"
query {
    for student in db.Student do
    averageBy (float student.StudentID)
}
|> printfn "Average student ID: %f"

printfn "\n averageByNullable"
query {
    for student in db.Student do
    averageByNullable (Nullable.float student.Age)
}
|> (fun avg -> printfn "Average age: %s" (avg.Print()))

printfn "\n find query operator"
query {
    for student in db.Student do
    find (student.Name = "Abercrombie, Kim")
}
|> (fun student -> printfn "Found a match with StudentID = %d" student.StudentID)

printfn "\n all query operator"
query {
    for student in db.Student do
    all (SqlMethods.Like(student.Name, "%,%"))
}
|> printfn "Do all students have a comma in the name? %b"

printfn "\n head query operator"
query {
    for student in db.Student do
    head
}
|> (fun student -> printfn "Found the head student with StudentID = %d" student.StudentID)

printfn "\n nth query operator"
query {
    for numbers in data do
    nth 3
}
|> printfn "Third number is %d"

printfn "\n skip query operator"
query {
    for student in db.Student do
    skip 1
}
|> Seq.iter (fun student -> printfn "StudentID = %d" student.StudentID)

printfn "\n skipWhile query operator"
query {
    for number in data do
    skipWhile (number < 3)
    select number
}
|> Seq.iter (fun number -> printfn "Number = %d" number)

printfn "\n sumBy query operator"
query {
    for student in db.Student do
    sumBy student.StudentID
}
|> printfn "Sum of student IDs: %d"

printfn "\n take query operator"
query {
    for student in db.Student do
    select student
    take 2
}
|> Seq.iter (fun student -> printfn "StudentID = %d" student.StudentID)

printfn "\n takeWhile query operator"
query {
    for number in data do
    takeWhile (number < 10)
}
|> Seq.iter (fun number -> printfn "Number = %d" number)

printfn "\n sortByNullable query operator"
query {
    for student in db.Student do
    sortByNullable student.Age
    select student
}
|> Seq.iter (fun student ->
    printfn "StudentID, Name, Age: %d %s %s" student.StudentID student.Name (student.Age.Print()))

printfn "\n sortByNullableDescending query operator"
query {
    for student in db.Student do
    sortByNullableDescending student.Age
    select student
}
|> Seq.iter (fun student ->
    printfn "StudentID, Name, Age: %d %s %s" student.StudentID student.Name (student.Age.Print()))

printfn "\n thenByNullable query operator"
query {
    for student in db.Student do
    sortBy student.Name
    thenByNullable student.Age
    select student
}
|> Seq.iter (fun student ->
    printfn "StudentID, Name, Age: %d %s %s" student.StudentID student.Name (student.Age.Print()))

printfn "\n thenByNullableDescending query operator"
query {
    for student in db.Student do
    sortBy student.Name
    thenByNullableDescending student.Age
    select student
}
|> Seq.iter (fun student ->
    printfn "StudentID, Name, Age: %d %s %s" student.StudentID student.Name (student.Age.Print()))

printfn "All students: "
query {
    for student in db.Student do
    select student
}
|> Seq.iter (fun student -> printfn "%s %d %s" student.Name student.StudentID (student.Age.Print()))

printfn "\nCount of students: "
query {
    for student in db.Student do
    count
}
|> (fun count -> printfn "Student count: %d" count)

printfn "\nExists."
query {
    for student in db.Student do
    where
        (query {
            for courseSelection in db.CourseSelection do
            exists (courseSelection.StudentID = student.StudentID) })
    select student
}
|> Seq.iter (fun student -> printfn "%A" student.Name)

printfn "\n Group by age and count"
query {
    for n in db.Student do
    groupBy n.Age into g
    select (g.Key, g.Count())
}
|> Seq.iter (fun (age, count) -> printfn "%s %d" (age.Print()) count)

printfn "\n Group value by age."
query {
    for n in db.Student do
    groupValBy n.Age n.Age into g
    select (g.Key, g.Count())
}
|> Seq.iter (fun (age, count) -> printfn "%s %d" (age.Print()) count)

printfn "\nGroup students by age where age > 10."
query {
    for student in db.Student do
    groupBy student.Age into g
    where (g.Key.HasValue && g.Key.Value > 10)
    select (g, g.Key)
}
|> Seq.iter (fun (students, age) ->
    printfn "Age: %s" (age.Value.ToString())
    students
    |> Seq.iter (fun student -> printfn "%s" student.Name))

printfn "\nGroup students by age and print counts of number of students at each age with more than 1 student."
query {
    for student in db.Student do
    groupBy student.Age into group
    where (group.Count() > 1)
    select (group.Key, group.Count())
}
|> Seq.iter (fun (age, ageCount) ->
    printfn "Age: %s Count: %d" (age.Print()) ageCount)

printfn "\nGroup students by age and sum ages."
query {
    for student in db.Student do
    groupBy student.Age into g
    let total = query { for student in g do sumByNullable student.Age }
    select (g.Key, g.Count(), total)
}
|> Seq.iter (fun (age, count, total) ->
    printfn "Age: %d" (age.GetValueOrDefault())
    printfn "Count: %d" count
    printfn "Total years: %s" (total.ToString()))

printfn "\nGroup students by age and count number of students at each age, and display all with count > 1 in descending order of count."
query {
    for student in db.Student do
    groupBy student.Age into g
    where (g.Count() > 1)
    sortByDescending (g.Count())
    select (g.Key, g.Count())
}
|> Seq.iter (fun (age, myCount) ->
    printfn "Age: %s" (age.Print())
    printfn "Count: %d" myCount)

printfn "\n Select students from a set of IDs"
let idList = [1; 2; 5; 10]
let idQuery =
    query { for id in idList do select id }
query {
    for student in db.Student do
    where (idQuery.Contains(student.StudentID))
    select student
}
|> Seq.iter (fun student ->
    printfn "Name: %s" student.Name)

printfn "\nLook for students with Name match _e%% pattern and take first two."
query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "_e%") )
    select student
    take 2
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\nLook for students with Name matching [abc]%% pattern."
query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "[abc]%") )
    select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\nLook for students with name matching [^abc]%% pattern."
query {
    for student in db.Student do
    where (SqlMethods.Like( student.Name, "[^abc]%") )
    select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\nLook for students with name matching [^abc]%% pattern and select ID."
query {
    for n in db.Student do
    where (SqlMethods.Like( n.Name, "[^abc]%") )
    select n.StudentID
}
|> Seq.iter (fun id -> printfn "%d" id)

printfn "\n Using Contains as a query filter."
query {
    for student in db.Student do
    where (student.Name.Contains("a"))
    select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\nSearching for names from a list."
let names = [|"a";"b";"c"|]
query {
    for student in db.Student do
    if names.Contains (student.Name) then select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\nJoin Student and CourseSelection tables."
query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    select (student, selection)
}
|> Seq.iter (fun (student, selection) -> printfn "%d %s %d" student.StudentID student.Name selection.CourseID)

printfn "\nLeft Join Student and CourseSelection tables."
query {
    for student in db.Student do
    leftOuterJoin selection in db.CourseSelection
        on (student.StudentID = selection.StudentID) into result
    for selection in result.DefaultIfEmpty() do
    select (student, selection)
}
|> Seq.iter (fun (student, selection) ->
    let selectionID, studentID, courseID =
        match selection with
        | null -> "NULL", "NULL", "NULL"
        | sel -> (sel.ID.ToString(), sel.StudentID.ToString(), sel.CourseID.ToString())
    printfn "%d %s %d %s %s %s" student.StudentID student.Name (student.Age.GetValueOrDefault()) selectionID studentID courseID)

printfn "\nJoin with count"
query {
    for n in db.Student do
    join e in db.CourseSelection
        on (n.StudentID = e.StudentID)
    count
}
|> printfn "%d"

printfn "\n Join with distinct."
query {
    for student in db.Student do
    join selection in db.CourseSelection
        on (student.StudentID = selection.StudentID)
    distinct
}
|> Seq.iter (fun (student, selection) -> printfn "%s %d" student.Name selection.CourseID)

printfn "\n Join with distinct and count."
query {
    for n in db.Student do
    join e in db.CourseSelection
        on (n.StudentID = e.StudentID)
    distinct
    count
}
|> printfn "%d"

printfn "\n Selecting students with age between 10 and 15."
query {
    for student in db.Student do
    where (student.Age.Value >= 10 && student.Age.Value < 15)
    select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\n Selecting students with age either 11 or 12."
query {
    for student in db.Student do
    where (student.Age.Value = 11 || student.Age.Value = 12)
    select student
}
|> Seq.iter (fun student -> printfn "%s" student.Name)

printfn "\n Selecting students in a certain age range and sorting."
query {
    for n in db.Student do
    where (n.Age.Value = 12 || n.Age.Value = 13)
    sortByNullableDescending n.Age
    select n
}
|> Seq.iter (fun student -> printfn "%s %s" student.Name (student.Age.Print()))

printfn "\n Selecting students with certain ages, taking account of possibility of nulls."
query {
    for student in db.Student do
    where
        ((student.Age.HasValue && student.Age.Value = 11) ||
         (student.Age.HasValue && student.Age.Value = 12))
    sortByDescending student.Name
    select student.Name
    take 2
}
|> Seq.iter (fun name -> printfn "%s" name)

printfn "\n Union of two queries."
module Queries =
    let query1 = query {
        for n in db.Student do
        select (n.Name, n.Age)
    }

    let query2 = query {
        for n in db.LastStudent do
        select (n.Name, n.Age)
    }

    query2.Union (query1)
    |> Seq.iter (fun (name, age) -> printfn "%s %s" name (age.Print()))

printfn "\n Intersect of two queries."
module Queries2 =
    let query1 = query {
        for n in db.Student do
        select (n.Name, n.Age)
    }

    let query2 = query {
        for n in db.LastStudent do
        select (n.Name, n.Age)
    }

    query1.Intersect(query2)
    |> Seq.iter (fun (name, age) -> printfn "%s %s" name (age.Print()))

printfn "\n Using if statement to alter results for special value."
query {
    for student in db.Student do
    select
        (if student.Age.HasValue && student.Age.Value = -1 then
            (student.StudentID, System.Nullable<int>(100), student.Age)
         else (student.StudentID, student.Age, student.Age))
}
|> Seq.iter (fun (id, value, age) -> printfn "%d %s %s" id (value.Print()) (age.Print()))

printfn "\n Using if statement to alter results special values."
query {
    for student in db.Student do
    select
        (if student.Age.HasValue && student.Age.Value = -1 then
            (student.StudentID, System.Nullable<int>(100), student.Age)
         elif student.Age.HasValue && student.Age.Value = 0 then
            (student.StudentID, System.Nullable<int>(100), student.Age)
         else (student.StudentID, student.Age, student.Age))
}
|> Seq.iter (fun (id, value, age) -> printfn "%d %s %s" id (value.Print()) (age.Print()))

printfn "\n Multiple table select."
query {
    for student in db.Student do
    for course in db.Course do
    select (student, course)
}
|> Seq.iteri (fun index (student, course) ->
    if index = 0 then
        printfn "StudentID Name Age CourseID CourseName"
    printfn "%d %s %s %d %s" student.StudentID student.Name (student.Age.Print()) course.CourseID course.CourseName)

printfn "\nMultiple Joins"
query {
    for student in db.Student do
    join courseSelection in db.CourseSelection
        on (student.StudentID = courseSelection.StudentID)
    join course in db.Course
        on (courseSelection.CourseID = course.CourseID)
    select (student.Name, course.CourseName)
}
|> Seq.iter (fun (studentName, courseName) -> printfn "%s %s" studentName courseName)

printfn "\nMultiple Left Outer Joins"
query {
    for student in db.Student do
    leftOuterJoin courseSelection in db.CourseSelection
        on (student.StudentID = courseSelection.StudentID) into g1
    for courseSelection in g1.DefaultIfEmpty() do
    leftOuterJoin course in db.Course
        on (courseSelection.CourseID = course.CourseID) into g2
    for course in g2.DefaultIfEmpty() do
    select (student.Name, course.CourseName)
}
|> Seq.iter (fun (studentName, courseName) -> printfn "%s %s" studentName courseName)
```

<span data-ttu-id="36eee-231">Questo è l'output completo quando questo codice viene eseguito in F# Interactive.</span><span class="sxs-lookup"><span data-stu-id="36eee-231">And here is the full output when this code is run in F# Interactive.</span></span>

```console
--> Referenced 'C:\Program Files (x86)\Reference Assemblies\Microsoft\FSharp\3.0\Runtime\v4.0\Type Providers\FSharp.Data.TypeProviders.dll'

--> Referenced 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\System.Data.dll'

--> Referenced 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\System.Data.Linq.dll'

contains query operator
Binding session to 'C:\Users\ghogen\AppData\Local\Temp\tmp5E3C.dll'...
Binding session to 'C:\Users\ghogen\AppData\Local\Temp\tmp611A.dll'...
Is at least one student age 11? true

count query operator
Number of students: 8

last query operator.
Last number: 21

lastOrDefault query operator.
lastOrDefault: 21

exactlyOne query operator.
Student with StudentID = 1 is Abercrombie, Kim

exactlyOneOrDefault query operator.
Student with StudentID = 1 is Abercrombie, Kim

headOrDefault query operator.
head student is Abercrombie, Kim

select query operator.
StudentID, Name: 1 Abercrombie, Kim
StudentID, Name: 2 Abolrous, Hazen
StudentID, Name: 3 Hance, Jim
StudentID, Name: 4 Adams, Terry
StudentID, Name: 5 Hansen, Claus
StudentID, Name: 6 Penor, Lori
StudentID, Name: 7 Perham, Tom
StudentID, Name: 8 Peng, Yun-Feng

where query operator.
StudentID, Name: 5 Hansen, Claus
StudentID, Name: 6 Penor, Lori
StudentID, Name: 7 Perham, Tom
StudentID, Name: 8 Peng, Yun-Feng

minBy query operator.

maxBy query operator.

groupBy query operator.
Age: NULL Count at that age: 1
Age: 10 Count at that age: 1
Age: 11 Count at that age: 1
Age: 12 Count at that age: 3
Age: 13 Count at that age: 1
Age: 14 Count at that age: 1

sortBy query operator.
StudentID, Name: 1 Abercrombie, Kim
StudentID, Name: 2 Abolrous, Hazen
StudentID, Name: 4 Adams, Terry
StudentID, Name: 3 Hance, Jim
StudentID, Name: 5 Hansen, Claus
StudentID, Name: 8 Peng, Yun-Feng
StudentID, Name: 6 Penor, Lori
StudentID, Name: 7 Perham, Tom

sortByDescending query operator.
StudentID, Name: 7 Perham, Tom
StudentID, Name: 6 Penor, Lori
StudentID, Name: 8 Peng, Yun-Feng
StudentID, Name: 5 Hansen, Claus
StudentID, Name: 3 Hance, Jim
StudentID, Name: 4 Adams, Terry
StudentID, Name: 2 Abolrous, Hazen
StudentID, Name: 1 Abercrombie, Kim

thenBy query operator.
StudentID, Name: 10 Abercrombie, Kim
StudentID, Name: 11 Hansen, Claus
StudentID, Name: 12 Adams, Terry
StudentID, Name: 12 Hance, Jim
StudentID, Name: 12 Perham, Tom
StudentID, Name: 13 Penor, Lori
StudentID, Name: 14 Abolrous, Hazen

thenByDescending query operator.
StudentID, Name: 10 Abercrombie, Kim
StudentID, Name: 11 Hansen, Claus
StudentID, Name: 12 Perham, Tom
StudentID, Name: 12 Hance, Jim
StudentID, Name: 12 Adams, Terry
StudentID, Name: 13 Penor, Lori
StudentID, Name: 14 Abolrous, Hazen

groupValBy query operator.
Age: NULL Count at that age: 1
Name: Peng, Yun-Feng
Age: 10 Count at that age: 1
Name: Abercrombie, Kim
Age: 11 Count at that age: 1
Name: Hansen, Claus
Age: 12 Count at that age: 3
Name: Hance, Jim
Name: Adams, Terry
Name: Perham, Tom
Age: 13 Count at that age: 1
Name: Penor, Lori
Age: 14 Count at that age: 1
Name: Abolrous, Hazen

sumByNullable query operator
Sum of ages: 84

minByNullable
Minimum age: 10

maxByNullable
Maximum age: 14

averageBy
Average student ID: 4.500000

averageByNullable
Average age: 12

find query operator
Found a match with StudentID = 1

all query operator
Do all students have a comma in the name? true

head query operator
Found the head student with StudentID = 1

nth query operator
Third number is 11

skip query operator
StudentID = 2
StudentID = 3
StudentID = 4
StudentID = 5
StudentID = 6
StudentID = 7
StudentID = 8

skipWhile query operator
Number = 5
Number = 7
Number = 11
Number = 18
Number = 21

sumBy query operator
Sum of student IDs: 36

take query operator
StudentID = 1
StudentID = 2

takeWhile query operator
Number = 1
Number = 5
Number = 7

sortByNullable query operator
StudentID, Name, Age: 8 Peng, Yun-Feng NULL
StudentID, Name, Age: 1 Abercrombie, Kim 10
StudentID, Name, Age: 5 Hansen, Claus 11
StudentID, Name, Age: 7 Perham, Tom 12
StudentID, Name, Age: 3 Hance, Jim 12
StudentID, Name, Age: 4 Adams, Terry 12
StudentID, Name, Age: 6 Penor, Lori 13
StudentID, Name, Age: 2 Abolrous, Hazen 14

sortByNullableDescending query operator
StudentID, Name, Age: 2 Abolrous, Hazen 14
StudentID, Name, Age: 6 Penor, Lori 13
StudentID, Name, Age: 7 Perham, Tom 12
StudentID, Name, Age: 3 Hance, Jim 12
StudentID, Name, Age: 4 Adams, Terry 12
StudentID, Name, Age: 5 Hansen, Claus 11
StudentID, Name, Age: 1 Abercrombie, Kim 10
StudentID, Name, Age: 8 Peng, Yun-Feng NULL

thenByNullable query operator
StudentID, Name, Age: 1 Abercrombie, Kim 10
StudentID, Name, Age: 2 Abolrous, Hazen 14
StudentID, Name, Age: 4 Adams, Terry 12
StudentID, Name, Age: 3 Hance, Jim 12
StudentID, Name, Age: 5 Hansen, Claus 11
StudentID, Name, Age: 8 Peng, Yun-Feng NULL
StudentID, Name, Age: 6 Penor, Lori 13
StudentID, Name, Age: 7 Perham, Tom 12

thenByNullableDescending query operator
StudentID, Name, Age: 1 Abercrombie, Kim 10
StudentID, Name, Age: 2 Abolrous, Hazen 14
StudentID, Name, Age: 4 Adams, Terry 12
StudentID, Name, Age: 3 Hance, Jim 12
StudentID, Name, Age: 5 Hansen, Claus 11
StudentID, Name, Age: 8 Peng, Yun-Feng NULL
StudentID, Name, Age: 6 Penor, Lori 13
StudentID, Name, Age: 7 Perham, Tom 12
All students:
Abercrombie, Kim 1 10
Abolrous, Hazen 2 14
Hance, Jim 3 12
Adams, Terry 4 12
Hansen, Claus 5 11
Penor, Lori 6 13
Perham, Tom 7 12
Peng, Yun-Feng 8 NULL

Count of students:
Student count: 8

Exists.
"Abercrombie, Kim"
"Abolrous, Hazen"
"Hance, Jim"
"Adams, Terry"
"Hansen, Claus"
"Perham, Tom"

Group by age and count
NULL 1
10 1
11 1
12 3
13 1
14 1

Group value by age.
NULL 1
10 1
11 1
12 3
13 1
14 1

Group students by age where age > 10.
Age: 11
Hansen, Claus
Age: 12
Hance, Jim
Adams, Terry
Perham, Tom
Age: 13
Penor, Lori
Age: 14
Abolrous, Hazen

Group students by age and print counts of number of students at each age with more than 1 student.
Age: 12 Count: 3

Group students by age and sum ages.
Age: 0
Count: 1
Total years:
Age: 10
Count: 1
Total years: 10
Age: 11
Count: 1
Total years: 11
Age: 12
Count: 3
Total years: 36
Age: 13
Count: 1
Total years: 13
Age: 14
Count: 1
Total years: 14

Group students by age and count number of students at each age, and display all with count > 1 in descending order of count.
Age: 12
Count: 3

Select students from a set of IDs
Name: Abercrombie, Kim
Name: Abolrous, Hazen
Name: Hansen, Claus

Look for students with Name match _e% pattern and take first two.
Penor, Lori
Perham, Tom

Look for students with Name matching [abc]% pattern.
Abercrombie, Kim
Abolrous, Hazen
Adams, Terry

Look for students with name matching [^abc]% pattern.
Hance, Jim
Hansen, Claus
Penor, Lori
Perham, Tom
Peng, Yun-Feng

Look for students with name matching [^abc]% pattern and select ID.
3
5
6
7
8

Using Contains as a query filter.
Abercrombie, Kim
Abolrous, Hazen
Hance, Jim
Adams, Terry
Hansen, Claus
Perham, Tom

Searching for names from a list.

Join Student and CourseSelection tables.
2 Abolrous, Hazen 2
3 Hance, Jim 3
5 Hansen, Claus 5
2 Abolrous, Hazen 2
5 Hansen, Claus 5
6 Penor, Lori 6
3 Hance, Jim 3
2 Abolrous, Hazen 2
1 Abercrombie, Kim 1
2 Abolrous, Hazen 2
5 Hansen, Claus 5
2 Abolrous, Hazen 2
3 Hance, Jim 3
2 Abolrous, Hazen 2
3 Hance, Jim 3

Left Join Student and CourseSelection tables.
1 Abercrombie, Kim 10 9 3 1
2 Abolrous, Hazen 14 1 1 2
2 Abolrous, Hazen 14 4 2 2
2 Abolrous, Hazen 14 8 3 2
2 Abolrous, Hazen 14 10 4 2
2 Abolrous, Hazen 14 12 4 2
2 Abolrous, Hazen 14 14 5 2
3 Hance, Jim 12 2 1 3
3 Hance, Jim 12 7 2 3
3 Hance, Jim 12 13 5 3
3 Hance, Jim 12 15 7 3
4 Adams, Terry 12 NULL NULL NULL
5 Hansen, Claus 11 3 1 5
5 Hansen, Claus 11 5 2 5
5 Hansen, Claus 11 11 4 5
6 Penor, Lori 13 6 2 6
7 Perham, Tom 12 NULL NULL NULL
8 Peng, Yun-Feng 0 NULL NULL NULL

Join with count
15

Join with distinct.
Abercrombie, Kim 2
Abercrombie, Kim 3
Abercrombie, Kim 5
Abolrous, Hazen 2
Abolrous, Hazen 5
Abolrous, Hazen 6
Abolrous, Hazen 3
Hance, Jim 2
Hance, Jim 1
Adams, Terry 2
Adams, Terry 5
Adams, Terry 2
Hansen, Claus 3
Hansen, Claus 2
Perham, Tom 3

Join with distinct and count.
15

Selecting students with age between 10 and 15.
Abercrombie, Kim
Abolrous, Hazen
Hance, Jim
Adams, Terry
Hansen, Claus
Penor, Lori
Perham, Tom

Selecting students with age either 11 or 12.
Hance, Jim
Adams, Terry
Hansen, Claus
Perham, Tom

Selecting students in a certain age range and sorting.
Penor, Lori 13
Perham, Tom 12
Hance, Jim 12
Adams, Terry 12

Selecting students with certain ages, taking account of possibility of nulls.
Hance, Jim
Adams, Terry

Union of two queries.
Abercrombie, Kim 10
Abolrous, Hazen 14
Hance, Jim 12
Adams, Terry 12
Hansen, Claus 11
Penor, Lori 13
Perham, Tom 12
Peng, Yun-Feng NULL

Intersect of two queries.

Using if statement to alter results for special value.
1 10 10
2 14 14
3 12 12
4 12 12
5 11 11
6 13 13
7 12 12
8 NULL NULL

Using if statement to alter results special values.
1 10 10
2 14 14
3 12 12
4 12 12
5 11 11
6 13 13
7 12 12
8 NULL NULL

Multiple table select.
StudentID Name Age CourseID CourseName
1 Abercrombie, Kim 10 1 Algebra I
2 Abolrous, Hazen 14 1 Algebra I
3 Hance, Jim 12 1 Algebra I
4 Adams, Terry 12 1 Algebra I
5 Hansen, Claus 11 1 Algebra I
6 Penor, Lori 13 1 Algebra I
7 Perham, Tom 12 1 Algebra I
8 Peng, Yun-Feng NULL 1 Algebra I
1 Abercrombie, Kim 10 2 Trigonometry
2 Abolrous, Hazen 14 2 Trigonometry
3 Hance, Jim 12 2 Trigonometry
4 Adams, Terry 12 2 Trigonometry
5 Hansen, Claus 11 2 Trigonometry
6 Penor, Lori 13 2 Trigonometry
7 Perham, Tom 12 2 Trigonometry
8 Peng, Yun-Feng NULL 2 Trigonometry
1 Abercrombie, Kim 10 3 Algebra II
2 Abolrous, Hazen 14 3 Algebra II
3 Hance, Jim 12 3 Algebra II
4 Adams, Terry 12 3 Algebra II
5 Hansen, Claus 11 3 Algebra II
6 Penor, Lori 13 3 Algebra II
7 Perham, Tom 12 3 Algebra II
8 Peng, Yun-Feng NULL 3 Algebra II
1 Abercrombie, Kim 10 4 History
2 Abolrous, Hazen 14 4 History
3 Hance, Jim 12 4 History
4 Adams, Terry 12 4 History
5 Hansen, Claus 11 4 History
6 Penor, Lori 13 4 History
7 Perham, Tom 12 4 History
8 Peng, Yun-Feng NULL 4 History
1 Abercrombie, Kim 10 5 English
2 Abolrous, Hazen 14 5 English
3 Hance, Jim 12 5 English
4 Adams, Terry 12 5 English
5 Hansen, Claus 11 5 English
6 Penor, Lori 13 5 English
7 Perham, Tom 12 5 English
8 Peng, Yun-Feng NULL 5 English
1 Abercrombie, Kim 10 6 French
2 Abolrous, Hazen 14 6 French
3 Hance, Jim 12 6 French
4 Adams, Terry 12 6 French
5 Hansen, Claus 11 6 French
6 Penor, Lori 13 6 French
7 Perham, Tom 12 6 French
8 Peng, Yun-Feng NULL 6 French
1 Abercrombie, Kim 10 7 Chinese
2 Abolrous, Hazen 14 7 Chinese
3 Hance, Jim 12 7 Chinese
4 Adams, Terry 12 7 Chinese
5 Hansen, Claus 11 7 Chinese
6 Penor, Lori 13 7 Chinese
7 Perham, Tom 12 7 Chinese
8 Peng, Yun-Feng NULL 7 Chinese

Multiple Joins
Abercrombie, Kim Trigonometry
Abercrombie, Kim Algebra II
Abercrombie, Kim English
Abolrous, Hazen Trigonometry
Abolrous, Hazen English
Abolrous, Hazen French
Abolrous, Hazen Algebra II
Hance, Jim Trigonometry
Hance, Jim Algebra I
Adams, Terry Trigonometry
Adams, Terry English
Adams, Terry Trigonometry
Hansen, Claus Algebra II
Hansen, Claus Trigonometry
Perham, Tom Algebra II

Multiple Left Outer Joins
Abercrombie, Kim Trigonometry
Abercrombie, Kim Algebra II
Abercrombie, Kim English
Abolrous, Hazen Trigonometry
Abolrous, Hazen English
Abolrous, Hazen French
Abolrous, Hazen Algebra II
Hance, Jim Trigonometry
Hance, Jim Algebra I
Adams, Terry Trigonometry
Adams, Terry English
Adams, Terry Trigonometry
Hansen, Claus Algebra II
Hansen, Claus Trigonometry
Penor, Lori
Perham, Tom Algebra II
Peng, Yun-Feng

type schema
val db : schema.ServiceTypes.SimpleDataContextTypes.MyDatabase1
val student : System.Data.Linq.Table<schema.ServiceTypes.Student>
val data : int list = [1; 5; 7; 11; 18; 21]
type Nullable<'T
                when 'T : (new : unit ->  'T) and 'T : struct and
                     'T :> System.ValueType> with
  member Print : unit -> string
val num : int = 21
val student2 : schema.ServiceTypes.Student
val student3 : schema.ServiceTypes.Student
val student4 : schema.ServiceTypes.Student
val student5 : int = 1
val student6 : int = 8
val idList : int list = [1; 2; 5; 10]
val idQuery : seq<int>
val names : string [] = [|"a"; "b"; "c"|]
module Queries = begin
  val query1 : System.Linq.IQueryable<string * System.Nullable<int>>
  val query2 : System.Linq.IQueryable<string * System.Nullable<int>>
end
module Queries2 = begin
  val query1 : System.Linq.IQueryable<string * System.Nullable<int>>
  val query2 : System.Linq.IQueryable<string * System.Nullable<int>>
end
```

## <a name="see-also"></a><span data-ttu-id="36eee-232">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="36eee-232">See also</span></span>

- [<span data-ttu-id="36eee-233">Riferimenti per il linguaggio F #</span><span class="sxs-lookup"><span data-stu-id="36eee-233">F# Language Reference</span></span>](index.md)
- [<span data-ttu-id="36eee-234">LINQ. QueryBuilder (classe)</span><span class="sxs-lookup"><span data-stu-id="36eee-234">Linq.QueryBuilder Class</span></span>](https://msdn.microsoft.com/visualfsharpdocs/conceptual/linq.querybuilder-class-%5bfsharp%5d)
- [<span data-ttu-id="36eee-235">Espressioni di calcolo</span><span class="sxs-lookup"><span data-stu-id="36eee-235">Computation Expressions</span></span>](Computation-Expressions.md)

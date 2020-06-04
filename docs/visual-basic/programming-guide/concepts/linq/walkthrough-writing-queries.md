---
title: Scrittura di query
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], writing
- LINQ [Visual Basic], walkthroughs
- LINQ [Visual Basic], writing queries
- writing LINQ queries [Visual Basic]
ms.assetid: f0045808-b9fe-4d31-88d1-473d9957211e
ms.openlocfilehash: 25905d7ac3ca4bb66a22ad1df421b400eaa6b08f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413271"
---
# <a name="walkthrough-writing-queries-in-visual-basic"></a><span data-ttu-id="8bb7a-102">Procedura dettagliata: Scrittura delle query in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="8bb7a-102">Walkthrough: Writing Queries in Visual Basic</span></span>

<span data-ttu-id="8bb7a-103">In questa procedura dettagliata viene illustrato come è possibile utilizzare le funzionalità del linguaggio Visual Basic per scrivere espressioni di query LINQ (Language-Integrated Query).</span><span class="sxs-lookup"><span data-stu-id="8bb7a-103">This walkthrough demonstrates how you can use Visual Basic language features to write Language-Integrated Query (LINQ) query expressions.</span></span> <span data-ttu-id="8bb7a-104">Nella procedura dettagliata viene illustrato come creare query in un elenco di oggetti Student, come eseguire le query e come modificarli.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-104">The walkthrough demonstrates how to create queries on a list of Student objects, how to run the queries, and how to modify them.</span></span> <span data-ttu-id="8bb7a-105">Le query includono diverse funzionalità, inclusi gli inizializzatori di oggetto, l'inferenza del tipo locale e i tipi anonimi.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-105">The queries incorporate several features including object initializers, local type inference, and anonymous types.</span></span>

<span data-ttu-id="8bb7a-106">Al termine di questa procedura dettagliata, si sarà pronti a passare agli esempi e alla documentazione per il provider LINQ specifico a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-106">After completing this walkthrough, you will be ready to move on to the samples and documentation for the specific LINQ provider you are interested in.</span></span> <span data-ttu-id="8bb7a-107">I provider LINQ includono [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] , LINQ to DataSet e [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] .</span><span class="sxs-lookup"><span data-stu-id="8bb7a-107">LINQ providers include [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)], LINQ to DataSet, and [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)].</span></span>

## <a name="create-a-project"></a><span data-ttu-id="8bb7a-108">Creazione di un progetto</span><span class="sxs-lookup"><span data-stu-id="8bb7a-108">Create a Project</span></span>

### <a name="to-create-a-console-application-project"></a><span data-ttu-id="8bb7a-109">Per creare un progetto di applicazione console</span><span class="sxs-lookup"><span data-stu-id="8bb7a-109">To create a console application project</span></span>

1. <span data-ttu-id="8bb7a-110">Avviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-110">Start Visual Studio.</span></span>

2. <span data-ttu-id="8bb7a-111">Scegliere **Nuovo** dal menu **File**e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-111">On the **File** menu, point to **New**, and then click **Project**.</span></span>

3. <span data-ttu-id="8bb7a-112">Nell'elenco **modelli installati** fare clic su **Visual Basic**.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-112">In the **Installed Templates** list, click **Visual Basic**.</span></span>

4. <span data-ttu-id="8bb7a-113">Nell'elenco dei tipi di progetto fare clic su **applicazione console**.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-113">In the list of project types, click **Console Application**.</span></span> <span data-ttu-id="8bb7a-114">Nella casella **nome** Digitare un nome per il progetto, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-114">In the **Name** box, type a name for the project, and then click **OK**.</span></span>

    <span data-ttu-id="8bb7a-115">Viene creato un progetto.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-115">A project is created.</span></span> <span data-ttu-id="8bb7a-116">Per impostazione predefinita, contiene un riferimento a System. Core. dll.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-116">By default, it contains a reference to System.Core.dll.</span></span> <span data-ttu-id="8bb7a-117">Inoltre, l'elenco degli **spazi dei nomi importati** nella [pagina riferimenti, progettazione progetti (Visual Basic)](/visualstudio/ide/reference/references-page-project-designer-visual-basic) include lo <xref:System.Linq?displayProperty=nameWithType> spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-117">Also, the **Imported namespaces** list on the [References Page, Project Designer (Visual Basic)](/visualstudio/ide/reference/references-page-project-designer-visual-basic) includes the <xref:System.Linq?displayProperty=nameWithType> namespace.</span></span>

5. <span data-ttu-id="8bb7a-118">Nella [pagina compilazione, Progettazione progetti (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic), assicurarsi che l' **opzione deduce** sia impostata **su on**.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-118">On the [Compile Page, Project Designer (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic), ensure that **Option infer** is set to **On**.</span></span>

## <a name="add-an-in-memory-data-source"></a><span data-ttu-id="8bb7a-119">Aggiungere un'origine dati in memoria</span><span class="sxs-lookup"><span data-stu-id="8bb7a-119">Add an In-Memory Data Source</span></span>

<span data-ttu-id="8bb7a-120">L'origine dati per le query in questa procedura dettagliata è un elenco di `Student` oggetti.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-120">The data source for the queries in this walkthrough is a list of `Student` objects.</span></span> <span data-ttu-id="8bb7a-121">Ogni `Student` oggetto contiene un nome, un cognome, un anno di classe e un rango accademico nel corpo degli studenti.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-121">Each `Student` object contains a first name, a last name, a class year, and an academic rank in the student body.</span></span>

### <a name="to-add-the-data-source"></a><span data-ttu-id="8bb7a-122">Per aggiungere l'origine dati</span><span class="sxs-lookup"><span data-stu-id="8bb7a-122">To add the data source</span></span>

- <span data-ttu-id="8bb7a-123">Definire una `Student` classe e creare un elenco di istanze della classe.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-123">Define a `Student` class, and create a list of instances of the class.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8bb7a-124">Il codice necessario per definire la `Student` classe e creare l'elenco usato negli esempi di procedura dettagliata è disponibile in [procedura: creare un elenco di elementi](how-to-create-a-list-of-items.md).</span><span class="sxs-lookup"><span data-stu-id="8bb7a-124">The code needed to define the `Student` class and create the list used in the walkthrough examples is provided in [How to: Create a List of Items](how-to-create-a-list-of-items.md).</span></span> <span data-ttu-id="8bb7a-125">È possibile copiarlo da questa posizione e incollarlo nel progetto.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-125">You can copy it from there and paste it into your project.</span></span> <span data-ttu-id="8bb7a-126">Il nuovo codice sostituisce il codice visualizzato quando è stato creato il progetto.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-126">The new code replaces the code that appeared when you created the project.</span></span>

### <a name="to-add-a-new-student-to-the-students-list"></a><span data-ttu-id="8bb7a-127">Per aggiungere un nuovo studente all'elenco degli studenti</span><span class="sxs-lookup"><span data-stu-id="8bb7a-127">To add a new student to the students list</span></span>

- <span data-ttu-id="8bb7a-128">Seguire il modello nel `getStudents` metodo per aggiungere un'altra istanza della `Student` classe all'elenco.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-128">Follow the pattern in the `getStudents` method to add another instance of the `Student` class to the list.</span></span> <span data-ttu-id="8bb7a-129">Aggiungendo lo studente si introdurranno gli inizializzatori di oggetto.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-129">Adding the student will introduce you to object initializers.</span></span> <span data-ttu-id="8bb7a-130">Per altre informazioni, vedere [inizializzatori di oggetto: tipi denominati e anonimi](../../language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md).</span><span class="sxs-lookup"><span data-stu-id="8bb7a-130">For more information, see [Object Initializers: Named and Anonymous Types](../../language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md).</span></span>

## <a name="create-a-query"></a><span data-ttu-id="8bb7a-131">Creare una query</span><span class="sxs-lookup"><span data-stu-id="8bb7a-131">Create a Query</span></span>

<span data-ttu-id="8bb7a-132">Quando viene eseguita, la query aggiunta in questa sezione produce un elenco degli studenti il cui rango accademico li inserisce nei primi dieci.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-132">When executed, the query added in this section produces a list of the students whose academic rank puts them in the top ten.</span></span> <span data-ttu-id="8bb7a-133">Poiché la query seleziona l' `Student` oggetto completo ogni volta, il tipo del risultato della query è `IEnumerable(Of Student)` .</span><span class="sxs-lookup"><span data-stu-id="8bb7a-133">Because the query selects the complete `Student` object each time, the type of the query result is `IEnumerable(Of Student)`.</span></span> <span data-ttu-id="8bb7a-134">Tuttavia, il tipo della query non viene in genere specificato nelle definizioni di query.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-134">However, the type of the query typically is not specified in query definitions.</span></span> <span data-ttu-id="8bb7a-135">Al contrario, il compilatore usa l'inferenza del tipo locale per determinare il tipo.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-135">Instead, the compiler uses local type inference to determine the type.</span></span> <span data-ttu-id="8bb7a-136">Per altre informazioni, vedere [inferenza dei tipi locali](../../language-features/variables/local-type-inference.md).</span><span class="sxs-lookup"><span data-stu-id="8bb7a-136">For more information, see [Local Type Inference](../../language-features/variables/local-type-inference.md).</span></span> <span data-ttu-id="8bb7a-137">La variabile di intervallo della query, `currentStudent` , funge da riferimento a ogni `Student` istanza nell'origine, `students` fornendo l'accesso alle proprietà di ogni oggetto in `students` .</span><span class="sxs-lookup"><span data-stu-id="8bb7a-137">The query's range variable, `currentStudent`, serves as a reference to each `Student` instance in the source, `students`, providing access to the properties of each object in `students`.</span></span>

### <a name="to-create-a-simple-query"></a><span data-ttu-id="8bb7a-138">Per creare una query semplice</span><span class="sxs-lookup"><span data-stu-id="8bb7a-138">To create a simple query</span></span>

1. <span data-ttu-id="8bb7a-139">Individuare la posizione nel `Main` metodo del progetto contrassegnata come segue:</span><span class="sxs-lookup"><span data-stu-id="8bb7a-139">Find the place in the `Main` method of the project that is marked as follows:</span></span>

    [!code-vb[VbLINQWalkthrough#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#1)]

    <span data-ttu-id="8bb7a-140">Copiare il codice seguente e incollarlo in.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-140">Copy the following code and paste it in.</span></span>

    [!code-vb[VbLINQWalkthrough#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#2)]

2. <span data-ttu-id="8bb7a-141">Posizionare il puntatore del mouse sul `studentQuery` codice per verificare che il tipo assegnato dal compilatore sia `IEnumerable(Of Student)` .</span><span class="sxs-lookup"><span data-stu-id="8bb7a-141">Rest the mouse pointer over `studentQuery` in your code to verify that the compiler-assigned type is `IEnumerable(Of Student)`.</span></span>

## <a name="run-the-query"></a><span data-ttu-id="8bb7a-142">Eseguire la query</span><span class="sxs-lookup"><span data-stu-id="8bb7a-142">Run the Query</span></span>

<span data-ttu-id="8bb7a-143">La variabile `studentQuery` contiene la definizione della query, non i risultati dell'esecuzione della query.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-143">The variable `studentQuery` contains the definition of the query, not the results of running the query.</span></span> <span data-ttu-id="8bb7a-144">Un meccanismo tipico per l'esecuzione di una query è un `For Each` ciclo.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-144">A typical mechanism for running a query is a `For Each` loop.</span></span> <span data-ttu-id="8bb7a-145">È possibile accedere a ogni elemento nella sequenza restituita tramite la variabile di iterazione del ciclo.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-145">Each element in the returned sequence is accessed through the loop iteration variable.</span></span> <span data-ttu-id="8bb7a-146">Per ulteriori informazioni sull'esecuzione di query, vedere [scrittura della prima query LINQ](writing-your-first-linq-query.md).</span><span class="sxs-lookup"><span data-stu-id="8bb7a-146">For more information about query execution, see [Writing Your First LINQ Query](writing-your-first-linq-query.md).</span></span>

### <a name="to-run-the-query"></a><span data-ttu-id="8bb7a-147">Per eseguire la query</span><span class="sxs-lookup"><span data-stu-id="8bb7a-147">To run the query</span></span>

1. <span data-ttu-id="8bb7a-148">Aggiungere il seguente `For Each` ciclo sotto la query nel progetto.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-148">Add the following `For Each` loop below the query in your project.</span></span>

    [!code-vb[VbLINQWalkthrough#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#3)]

2. <span data-ttu-id="8bb7a-149">Posizionare il puntatore del mouse sulla variabile di controllo loop `studentRecord` per visualizzarne il tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-149">Rest the mouse pointer over the loop control variable `studentRecord` to see its data type.</span></span> <span data-ttu-id="8bb7a-150">Il tipo di `studentRecord` viene dedotto come `Student` , perché `studentQuery` restituisce una raccolta di istanze di `Student` .</span><span class="sxs-lookup"><span data-stu-id="8bb7a-150">The type of `studentRecord` is inferred to be `Student`, because `studentQuery` returns a collection of `Student` instances.</span></span>

3. <span data-ttu-id="8bb7a-151">Compilare ed eseguire l'applicazione premendo CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-151">Build and run the application by pressing CTRL+F5.</span></span> <span data-ttu-id="8bb7a-152">Si notino i risultati nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-152">Note the results in the console window.</span></span>

## <a name="modify-the-query"></a><span data-ttu-id="8bb7a-153">Modificare la query</span><span class="sxs-lookup"><span data-stu-id="8bb7a-153">Modify the Query</span></span>

<span data-ttu-id="8bb7a-154">È più semplice analizzare i risultati della query se sono in un ordine specificato.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-154">It is easier to scan query results if they are in a specified order.</span></span> <span data-ttu-id="8bb7a-155">È possibile ordinare la sequenza restituita in base a qualsiasi campo disponibile.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-155">You can sort the returned sequence based on any available field.</span></span>

### <a name="to-order-the-results"></a><span data-ttu-id="8bb7a-156">Per ordinare i risultati</span><span class="sxs-lookup"><span data-stu-id="8bb7a-156">To order the results</span></span>

1. <span data-ttu-id="8bb7a-157">Aggiungere la `Order By` clausola seguente tra l' `Where` istruzione e l' `Select` istruzione della query.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-157">Add the following `Order By` clause between the `Where` statement and the `Select` statement of the query.</span></span> <span data-ttu-id="8bb7a-158">Con la `Order By` clausola i risultati vengono ordinati in ordine alfabetico da a a Z, in base al cognome di ogni studente.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-158">The `Order By` clause will order the results alphabetically from A to Z, according to the last name of each student.</span></span>

    ```vb
    Order By currentStudent.Last Ascending
    ```

2. <span data-ttu-id="8bb7a-159">Per eseguire l'ordinamento in base al cognome e quindi al nome, aggiungere entrambi i campi alla query:</span><span class="sxs-lookup"><span data-stu-id="8bb7a-159">To order by last name and then first name, add both fields to the query:</span></span>

    ```vb
    Order By currentStudent.Last Ascending, currentStudent.First Ascending
    ```

    <span data-ttu-id="8bb7a-160">È anche possibile specificare `Descending` di ordinare da Z A a.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-160">You can also specify `Descending` to order from Z to A.</span></span>

3. <span data-ttu-id="8bb7a-161">Compilare ed eseguire l'applicazione premendo CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-161">Build and run the application by pressing CTRL+F5.</span></span> <span data-ttu-id="8bb7a-162">Si notino i risultati nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-162">Note the results in the console window.</span></span>

### <a name="to-introduce-a-local-identifier"></a><span data-ttu-id="8bb7a-163">Per introdurre un identificatore locale</span><span class="sxs-lookup"><span data-stu-id="8bb7a-163">To introduce a local identifier</span></span>

1. <span data-ttu-id="8bb7a-164">Aggiungere il codice in questa sezione per introdurre un identificatore locale nell'espressione di query.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-164">Add the code in this section to introduce a local identifier in the query expression.</span></span> <span data-ttu-id="8bb7a-165">L'identificatore locale conterrà un risultato intermedio.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-165">The local identifier will hold an intermediate result.</span></span> <span data-ttu-id="8bb7a-166">Nell'esempio seguente `name` è un identificatore che include una concatenazione del nome e del cognome dello studente.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-166">In the following example, `name` is an identifier that holds a concatenation of the student's first and last names.</span></span> <span data-ttu-id="8bb7a-167">Un identificatore locale può essere usato per praticità oppure può migliorare le prestazioni archiviando i risultati di un'espressione che altrimenti verrebbe calcolata più volte.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-167">A local identifier can be used for convenience, or it can enhance performance by storing the results of an expression that would otherwise be calculated multiple times.</span></span>

    [!code-vb[VbLINQWalkthrough#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#4)]

2. <span data-ttu-id="8bb7a-168">Compilare ed eseguire l'applicazione premendo CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-168">Build and run the application by pressing CTRL+F5.</span></span> <span data-ttu-id="8bb7a-169">Si notino i risultati nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-169">Note the results in the console window.</span></span>

### <a name="to-project-one-field-in-the-select-clause"></a><span data-ttu-id="8bb7a-170">Per proiettare un campo nella clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="8bb7a-170">To project one field in the Select clause</span></span>

1. <span data-ttu-id="8bb7a-171">Aggiungere la query e il `For Each` ciclo da questa sezione per creare una query che produce una sequenza i cui elementi differiscono dagli elementi nell'origine.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-171">Add the query and `For Each` loop from this section to create a query that produces a sequence whose elements differ from the elements in the source.</span></span> <span data-ttu-id="8bb7a-172">Nell'esempio seguente, l'origine è una raccolta di `Student` oggetti, ma viene restituito solo un membro di ogni oggetto: il nome degli studenti il cui cognome è Garcia.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-172">In the following example, the source is a collection of `Student` objects, but only one member of each object is returned: the first name of students whose last name is Garcia.</span></span> <span data-ttu-id="8bb7a-173">Poiché `currentStudent.First` è una stringa, il tipo di dati della sequenza restituita da `studentQuery3` è `IEnumerable(Of String)` , una sequenza di stringhe.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-173">Because `currentStudent.First` is a string, the data type of the sequence returned by `studentQuery3` is `IEnumerable(Of String)`, a sequence of strings.</span></span> <span data-ttu-id="8bb7a-174">Come negli esempi precedenti, l'assegnazione di un tipo di dati per `studentQuery3` viene lasciata dal compilatore per determinare utilizzando l'inferenza del tipo locale.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-174">As in earlier examples, the assignment of a data type for `studentQuery3` is left for the compiler to determine by using local type inference.</span></span>

    [!code-vb[VbLINQWalkthrough#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#5)]

2. <span data-ttu-id="8bb7a-175">Posizionare il puntatore del mouse sul `studentQuery3` codice per verificare che il tipo assegnato sia `IEnumerable(Of String)` .</span><span class="sxs-lookup"><span data-stu-id="8bb7a-175">Rest the mouse pointer over `studentQuery3` in your code to verify that the assigned type is `IEnumerable(Of String)`.</span></span>

3. <span data-ttu-id="8bb7a-176">Compilare ed eseguire l'applicazione premendo CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-176">Build and run the application by pressing CTRL+F5.</span></span> <span data-ttu-id="8bb7a-177">Si notino i risultati nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-177">Note the results in the console window.</span></span>

### <a name="to-create-an-anonymous-type-in-the-select-clause"></a><span data-ttu-id="8bb7a-178">Per creare un tipo anonimo nella clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="8bb7a-178">To create an anonymous type in the Select clause</span></span>

1. <span data-ttu-id="8bb7a-179">Aggiungere il codice da questa sezione per vedere come vengono usati i tipi anonimi nelle query.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-179">Add the code from this section to see how anonymous types are used in queries.</span></span> <span data-ttu-id="8bb7a-180">Vengono usati nelle query quando si desidera restituire più campi dall'origine dati anziché record completi ( `currentStudent` record negli esempi precedenti) o campi singoli ( `First` nella sezione precedente).</span><span class="sxs-lookup"><span data-stu-id="8bb7a-180">You use them in queries when you want to return several fields from the data source rather than complete records (`currentStudent` records in previous examples) or single fields (`First` in the preceding section).</span></span> <span data-ttu-id="8bb7a-181">Anziché definire un nuovo tipo denominato che contiene i campi che si desidera includere nel risultato, è necessario specificare i campi nella `Select` clausola e il compilatore crea un tipo anonimo con tali campi come proprietà.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-181">Instead of defining a new named type that contains the fields you want to include in the result, you specify the fields in the `Select` clause and the compiler creates an anonymous type with those fields as its properties.</span></span> <span data-ttu-id="8bb7a-182">Per ulteriori informazioni, vedere [tipi anonimi](../../language-features/objects-and-classes/anonymous-types.md).</span><span class="sxs-lookup"><span data-stu-id="8bb7a-182">For more information, see [Anonymous Types](../../language-features/objects-and-classes/anonymous-types.md).</span></span>

    <span data-ttu-id="8bb7a-183">Nell'esempio seguente viene creata una query che restituisce il nome e il rango degli anziani il cui rango accademico è compreso tra 1 e 10, in ordine di rango accademico.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-183">The following example creates a query that returns the name and rank of seniors whose academic rank is between 1 and 10, in order of academic rank.</span></span> <span data-ttu-id="8bb7a-184">In questo esempio, il tipo di `studentQuery4` deve essere dedotto perché la `Select` clausola restituisce un'istanza di un tipo anonimo e un tipo anonimo non ha un nome utilizzabile.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-184">In this example, the type of `studentQuery4` must be inferred because the `Select` clause returns an instance of an anonymous type, and an anonymous type has no usable name.</span></span>

    [!code-vb[VbLINQWalkthrough#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#6)]

2. <span data-ttu-id="8bb7a-185">Compilare ed eseguire l'applicazione premendo CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-185">Build and run the application by pressing CTRL+F5.</span></span> <span data-ttu-id="8bb7a-186">Si notino i risultati nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-186">Note the results in the console window.</span></span>

## <a name="additional-examples"></a><span data-ttu-id="8bb7a-187">Esempi aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="8bb7a-187">Additional Examples</span></span>

<span data-ttu-id="8bb7a-188">A questo punto, dopo aver compreso le nozioni di base, di seguito è riportato un elenco di esempi aggiuntivi per illustrare la flessibilità e la potenza delle query LINQ.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-188">Now that you understand the basics, the following is a list of additional examples to illustrate the flexibility and power of LINQ queries.</span></span> <span data-ttu-id="8bb7a-189">Ogni esempio è preceduto da una breve descrizione dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-189">Each example is preceded by a brief description of what it does.</span></span> <span data-ttu-id="8bb7a-190">Posizionare il puntatore del mouse sulla variabile dei risultati della query per ogni query per visualizzare il tipo dedotto.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-190">Rest the mouse pointer over the query result variable for each query to see the inferred type.</span></span> <span data-ttu-id="8bb7a-191">Usare un `For Each` ciclo per produrre i risultati.</span><span class="sxs-lookup"><span data-stu-id="8bb7a-191">Use a `For Each` loop to produce the results.</span></span>

[!code-vb[VbLINQWalkthrough#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#7)]

## <a name="additional-information"></a><span data-ttu-id="8bb7a-192">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8bb7a-192">Additional Information</span></span>

<span data-ttu-id="8bb7a-193">Dopo aver acquisito familiarità con i concetti di base relativi all'utilizzo delle query, è possibile leggere la documentazione e gli esempi relativi al tipo specifico di provider LINQ a cui si è interessati:</span><span class="sxs-lookup"><span data-stu-id="8bb7a-193">After you are familiar with the basic concepts of working with queries, you are ready to read the documentation and samples for the specific type of LINQ provider that you are interested in:</span></span>

- [<span data-ttu-id="8bb7a-194">LINQ to Objects</span><span class="sxs-lookup"><span data-stu-id="8bb7a-194">LINQ to Objects</span></span>](linq-to-objects.md)

- [<span data-ttu-id="8bb7a-195">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="8bb7a-195">LINQ to SQL</span></span>](../../../../framework/data/adonet/sql/linq/index.md)

- [<span data-ttu-id="8bb7a-196">LINQ to XML</span><span class="sxs-lookup"><span data-stu-id="8bb7a-196">LINQ to XML</span></span>](linq-to-xml.md)

- [<span data-ttu-id="8bb7a-197">LINQ to DataSet</span><span class="sxs-lookup"><span data-stu-id="8bb7a-197">LINQ to DataSet</span></span>](../../../../framework/data/adonet/linq-to-dataset.md)

## <a name="see-also"></a><span data-ttu-id="8bb7a-198">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8bb7a-198">See also</span></span>

- [<span data-ttu-id="8bb7a-199">LINQ (Language-Integrated Query) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="8bb7a-199">Language-Integrated Query (LINQ) (Visual Basic)</span></span>](index.md)
- [<span data-ttu-id="8bb7a-200">Introduzione a LINQ in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="8bb7a-200">Getting Started with LINQ in Visual Basic</span></span>](getting-started-with-linq.md)
- [<span data-ttu-id="8bb7a-201">Inferenza del tipo di variabile locale</span><span class="sxs-lookup"><span data-stu-id="8bb7a-201">Local Type Inference</span></span>](../../language-features/variables/local-type-inference.md)
- [<span data-ttu-id="8bb7a-202">Inizializzatori di oggetto: tipi denominati e tipi anonimi</span><span class="sxs-lookup"><span data-stu-id="8bb7a-202">Object Initializers: Named and Anonymous Types</span></span>](../../language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [<span data-ttu-id="8bb7a-203">Tipi anonimi</span><span class="sxs-lookup"><span data-stu-id="8bb7a-203">Anonymous Types</span></span>](../../language-features/objects-and-classes/anonymous-types.md)
- [<span data-ttu-id="8bb7a-204">Introduzione a LINQ in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="8bb7a-204">Introduction to LINQ in Visual Basic</span></span>](../../language-features/linq/introduction-to-linq.md)
- [<span data-ttu-id="8bb7a-205">LINQ</span><span class="sxs-lookup"><span data-stu-id="8bb7a-205">LINQ</span></span>](../../language-features/linq/index.md)
- [<span data-ttu-id="8bb7a-206">Query</span><span class="sxs-lookup"><span data-stu-id="8bb7a-206">Queries</span></span>](../../../language-reference/queries/index.md)

---
title: 'Procedura dettagliata: Modello a oggetti e query semplici (C#)'
description: Seguire questa procedura dettagliata per creare una classe di entità per la modellazione di una tabella in un database di esempio. Creare quindi una semplice query per elencare i clienti in una determinata posizione.
ms.date: 03/30/2017
ms.assetid: 419961cc-92d6-45f5-ae8a-d485bdde3a37
ms.openlocfilehash: 4637fabecc1726d8fec12857a667073912cfbed5
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286301"
---
# <a name="walkthrough-simple-object-model-and-query-c"></a><span data-ttu-id="5870d-104">Procedura dettagliata: Modello a oggetti e query semplici (C#)</span><span class="sxs-lookup"><span data-stu-id="5870d-104">Walkthrough: Simple Object Model and Query (C#)</span></span>

<span data-ttu-id="5870d-105">In questa procedura dettagliata viene descritto uno scenario [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] end-to-end di base con minime complessità.</span><span class="sxs-lookup"><span data-stu-id="5870d-105">This walkthrough provides a fundamental end-to-end [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] scenario with minimal complexities.</span></span> <span data-ttu-id="5870d-106">Verranno create una classe di entità per la modellazione della tabella Customers nel database Northwind di esempio,</span><span class="sxs-lookup"><span data-stu-id="5870d-106">You will create an entity class that models the Customers table in the sample Northwind database.</span></span> <span data-ttu-id="5870d-107">quindi una semplice query per elencare i clienti residenti nell'area londinese.</span><span class="sxs-lookup"><span data-stu-id="5870d-107">You will then create a simple query to list customers who are located in London.</span></span>

<span data-ttu-id="5870d-108">Questa procedura dettagliata è basata sul codice in fase di progettazione per illustrare i concetti di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].</span><span class="sxs-lookup"><span data-stu-id="5870d-108">This walkthrough is code-oriented by design to help show [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] concepts.</span></span> <span data-ttu-id="5870d-109">In genere, è possibile utilizzare il Object Relational Designer per creare il modello a oggetti.</span><span class="sxs-lookup"><span data-stu-id="5870d-109">Normally speaking, you would use the Object Relational Designer to create your object model.</span></span>

[!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]

<span data-ttu-id="5870d-110">Questa procedura è stata scritta usando Impostazioni di sviluppo di Visual C#.</span><span class="sxs-lookup"><span data-stu-id="5870d-110">This walkthrough was written by using Visual C# Development Settings.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5870d-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5870d-111">Prerequisites</span></span>

- <span data-ttu-id="5870d-112">Per i file usati nella procedura dettagliata viene usata una cartella dedicata ("c:\linqtest5").</span><span class="sxs-lookup"><span data-stu-id="5870d-112">This walkthrough uses a dedicated folder ("c:\linqtest5") to hold files.</span></span> <span data-ttu-id="5870d-113">Creare la cartella prima di avviare la procedura.</span><span class="sxs-lookup"><span data-stu-id="5870d-113">Create this folder before you begin the walkthrough.</span></span>

- <span data-ttu-id="5870d-114">Per questa procedura dettagliata è richiesto il database di esempio Northwind.</span><span class="sxs-lookup"><span data-stu-id="5870d-114">This walkthrough requires the Northwind sample database.</span></span> <span data-ttu-id="5870d-115">Se questo database non è disponibile nel computer di sviluppo, è possibile scaricarlo dal sito di download Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5870d-115">If you do not have this database on your development computer, you can download it from the Microsoft download site.</span></span> <span data-ttu-id="5870d-116">Per istruzioni, vedere [download di database di esempio](downloading-sample-databases.md).</span><span class="sxs-lookup"><span data-stu-id="5870d-116">For instructions, see [Downloading Sample Databases](downloading-sample-databases.md).</span></span> <span data-ttu-id="5870d-117">Dopo avere scaricato il database, copiare il file nella cartella c:\linqtest5.</span><span class="sxs-lookup"><span data-stu-id="5870d-117">After you have downloaded the database, copy the file to the c:\linqtest5 folder.</span></span>

## <a name="overview"></a><span data-ttu-id="5870d-118">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5870d-118">Overview</span></span>

<span data-ttu-id="5870d-119">La procedura dettagliata è costituita da sei attività principali:</span><span class="sxs-lookup"><span data-stu-id="5870d-119">This walkthrough consists of six main tasks:</span></span>

- <span data-ttu-id="5870d-120">Creazione [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] di una soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5870d-120">Creating a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] solution in Visual Studio.</span></span>

- <span data-ttu-id="5870d-121">Mapping di una classe a una tabella del database.</span><span class="sxs-lookup"><span data-stu-id="5870d-121">Mapping a class to a database table.</span></span>

- <span data-ttu-id="5870d-122">Definizione di proprietà nella classe per rappresentare colonne del database.</span><span class="sxs-lookup"><span data-stu-id="5870d-122">Designating properties on the class to represent database columns.</span></span>

- <span data-ttu-id="5870d-123">Definizione della connessione al database Northwind.</span><span class="sxs-lookup"><span data-stu-id="5870d-123">Specifying the connection to the Northwind database.</span></span>

- <span data-ttu-id="5870d-124">Creazione di una semplice query da eseguire sul database.</span><span class="sxs-lookup"><span data-stu-id="5870d-124">Creating a simple query to run against the database.</span></span>

- <span data-ttu-id="5870d-125">Esecuzione della query e analisi dei risultati.</span><span class="sxs-lookup"><span data-stu-id="5870d-125">Executing the query and observing the results.</span></span>

## <a name="creating-a-linq-to-sql-solution"></a><span data-ttu-id="5870d-126">Creazione di una soluzione LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="5870d-126">Creating a LINQ to SQL Solution</span></span>

<span data-ttu-id="5870d-127">In questa prima attività viene creata una soluzione di Visual Studio che contiene i riferimenti necessari per compilare ed eseguire un [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] progetto.</span><span class="sxs-lookup"><span data-stu-id="5870d-127">In this first task, you create a Visual Studio solution that contains the necessary references to build and run a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] project.</span></span>

### <a name="to-create-a-linq-to-sql-solution"></a><span data-ttu-id="5870d-128">Per creare una soluzione LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="5870d-128">To create a LINQ to SQL solution</span></span>

1. <span data-ttu-id="5870d-129">Scegliere **nuovo**dal menu **file** di Visual Studio, quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="5870d-129">On the Visual Studio **File** menu, point to **New**, and then click **Project**.</span></span>

2. <span data-ttu-id="5870d-130">Nel riquadro **Tipi progetto** della finestra di dialogo **nuovo progetto** fare clic su **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="5870d-130">In the **Project types** pane of the **New Project** dialog box, click **Visual C#**.</span></span>

3. <span data-ttu-id="5870d-131">Nel riquadro **Modelli** fare clic su **Applicazione console**.</span><span class="sxs-lookup"><span data-stu-id="5870d-131">In the **Templates** pane, click **Console Application**.</span></span>

4. <span data-ttu-id="5870d-132">Nella casella **nome** digitare **LinqConsoleApp**.</span><span class="sxs-lookup"><span data-stu-id="5870d-132">In the **Name** box, type **LinqConsoleApp**.</span></span>

5. <span data-ttu-id="5870d-133">Nella casella **percorso** , verificare dove si desidera archiviare i file di progetto.</span><span class="sxs-lookup"><span data-stu-id="5870d-133">In the **Location** box, verify where you want to store your project files.</span></span>

6. <span data-ttu-id="5870d-134">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5870d-134">Click **OK**.</span></span>

## <a name="adding-linq-references-and-directives"></a><span data-ttu-id="5870d-135">Aggiunta di riferimenti e direttive LINQ</span><span class="sxs-lookup"><span data-stu-id="5870d-135">Adding LINQ References and Directives</span></span>

<span data-ttu-id="5870d-136">In questa procedura dettagliata vengono usati assembly che potrebbero non essere installati per impostazione predefinita nel progetto.</span><span class="sxs-lookup"><span data-stu-id="5870d-136">This walkthrough uses assemblies that might not be installed by default in your project.</span></span> <span data-ttu-id="5870d-137">Se System. Data. Linq non è elencato come riferimento nel progetto (espandere il nodo **riferimenti** in **Esplora soluzioni**), aggiungerlo, come illustrato nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="5870d-137">If System.Data.Linq is not listed as a reference in your project (expand the **References** node in **Solution Explorer**), add it, as explained in the following steps.</span></span>

### <a name="to-add-systemdatalinq"></a><span data-ttu-id="5870d-138">Per aggiungere System.Data.Linq</span><span class="sxs-lookup"><span data-stu-id="5870d-138">To add System.Data.Linq</span></span>

1. <span data-ttu-id="5870d-139">In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **riferimenti**, quindi scegliere **Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="5870d-139">In **Solution Explorer**, right-click **References**, and then click **Add Reference**.</span></span>

2. <span data-ttu-id="5870d-140">Nella finestra di dialogo **Aggiungi riferimento** fare clic su **.NET**, selezionare l'assembly System. Data. Linq, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5870d-140">In the **Add Reference** dialog box, click **.NET**, click the System.Data.Linq assembly, and then click **OK**.</span></span>

     <span data-ttu-id="5870d-141">L'assembly verrà aggiunto al progetto.</span><span class="sxs-lookup"><span data-stu-id="5870d-141">The assembly is added to the project.</span></span>

3. <span data-ttu-id="5870d-142">Aggiungere le direttive seguenti all'inizio di **Program.cs**:</span><span class="sxs-lookup"><span data-stu-id="5870d-142">Add the following directives at the top of **Program.cs**:</span></span>

     [!code-csharp[DLinqWalk1CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#1)]

## <a name="mapping-a-class-to-a-database-table"></a><span data-ttu-id="5870d-143">Mapping di una classe a una tabella del database</span><span class="sxs-lookup"><span data-stu-id="5870d-143">Mapping a Class to a Database Table</span></span>

<span data-ttu-id="5870d-144">In questo passaggio verrà creata una classe ed eseguito il mapping della classe a una tabella di database.</span><span class="sxs-lookup"><span data-stu-id="5870d-144">In this step, you create a class and map it to a database table.</span></span> <span data-ttu-id="5870d-145">Tale classe viene definita una classe di *entità*.</span><span class="sxs-lookup"><span data-stu-id="5870d-145">Such a class is termed an *entity class*.</span></span> <span data-ttu-id="5870d-146">Notare che il mapping viene eseguito semplicemente aggiungendo l'attributo <xref:System.Data.Linq.Mapping.TableAttribute>.</span><span class="sxs-lookup"><span data-stu-id="5870d-146">Note that the mapping is accomplished by just adding the <xref:System.Data.Linq.Mapping.TableAttribute> attribute.</span></span> <span data-ttu-id="5870d-147">La proprietà <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A> consente di specificare il nome della tabella nel database.</span><span class="sxs-lookup"><span data-stu-id="5870d-147">The <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A> property specifies the name of the table in the database.</span></span>

### <a name="to-create-an-entity-class-and-map-it-to-a-database-table"></a><span data-ttu-id="5870d-148">Per creare una classe di entità ed eseguire il mapping della classe a una tabella di database</span><span class="sxs-lookup"><span data-stu-id="5870d-148">To create an entity class and map it to a database table</span></span>

- <span data-ttu-id="5870d-149">Digitare o incollare il codice seguente in Program.cs immediatamente sopra la dichiarazione della classe `Program`:</span><span class="sxs-lookup"><span data-stu-id="5870d-149">Type or paste the following code into Program.cs immediately above the `Program` class declaration:</span></span>

     [!code-csharp[DLinqWalk1CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#2)]

## <a name="designating-properties-on-the-class-to-represent-database-columns"></a><span data-ttu-id="5870d-150">Definizione di proprietà nella classe per rappresentare colonne del database</span><span class="sxs-lookup"><span data-stu-id="5870d-150">Designating Properties on the Class to Represent Database Columns</span></span>

<span data-ttu-id="5870d-151">In questo passaggio si completeranno diverse attività.</span><span class="sxs-lookup"><span data-stu-id="5870d-151">In this step, you accomplish several tasks.</span></span>

- <span data-ttu-id="5870d-152">Usare l'attributo <xref:System.Data.Linq.Mapping.ColumnAttribute> per definire le proprietà `CustomerID` e `City` nella classe di entità in modo che rappresentino colonne nella tabella del database.</span><span class="sxs-lookup"><span data-stu-id="5870d-152">You use the <xref:System.Data.Linq.Mapping.ColumnAttribute> attribute to designate `CustomerID` and `City` properties on the entity class as representing columns in the database table.</span></span>

- <span data-ttu-id="5870d-153">Definire la proprietà `CustomerID` in modo che rappresenti una colonna di chiave primaria nel database.</span><span class="sxs-lookup"><span data-stu-id="5870d-153">You designate the `CustomerID` property as representing a primary key column in the database.</span></span>

- <span data-ttu-id="5870d-154">Definire i campi `_CustomerID` e `_City` per l'archiviazione privata.</span><span class="sxs-lookup"><span data-stu-id="5870d-154">You designate `_CustomerID` and `_City` fields for private storage.</span></span> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="5870d-155">sarà quindi in grado di archiviare e recuperare direttamente i valori, anziché usare funzioni di accesso pubbliche che potrebbero includere la logica di business.</span><span class="sxs-lookup"><span data-stu-id="5870d-155">can then store and retrieve values directly, instead of using public accessors that might include business logic.</span></span>

### <a name="to-represent-characteristics-of-two-database-columns"></a><span data-ttu-id="5870d-156">Per rappresentare caratteristiche di due colonne del database</span><span class="sxs-lookup"><span data-stu-id="5870d-156">To represent characteristics of two database columns</span></span>

- <span data-ttu-id="5870d-157">Digitare o incollare il codice seguente in Program.cs all'interno delle parentesi graffe della classe `Customer`:</span><span class="sxs-lookup"><span data-stu-id="5870d-157">Type or paste the following code into Program.cs inside the curly braces for the `Customer` class.</span></span>

     [!code-csharp[DLinqWalk1CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#3)]

## <a name="specifying-the-connection-to-the-northwind-database"></a><span data-ttu-id="5870d-158">Definizione della connessione al database Northwind</span><span class="sxs-lookup"><span data-stu-id="5870d-158">Specifying the Connection to the Northwind Database</span></span>

<span data-ttu-id="5870d-159">In questo passaggio viene usato un oggetto <xref:System.Data.Linq.DataContext> per stabilire una connessione tra le strutture di dati basate sul codice e il database stesso.</span><span class="sxs-lookup"><span data-stu-id="5870d-159">In this step you use a <xref:System.Data.Linq.DataContext> object to establish a connection between your code-based data structures and the database itself.</span></span> <span data-ttu-id="5870d-160"><xref:System.Data.Linq.DataContext> è il canale principale tramite il quale vengono recuperati oggetti dal database e vengono inviate modifiche.</span><span class="sxs-lookup"><span data-stu-id="5870d-160">The <xref:System.Data.Linq.DataContext> is the main channel through which you retrieve objects from the database and submit changes.</span></span>

<span data-ttu-id="5870d-161">Viene inoltre dichiarato un oggetto `Table<Customer>` che fungerà da tabella tipizzata logica per le query sulla tabella Customers nel database.</span><span class="sxs-lookup"><span data-stu-id="5870d-161">You also declare a `Table<Customer>` to act as the logical, typed table for your queries against the Customers table in the database.</span></span> <span data-ttu-id="5870d-162">Tali query verranno quindi create ed eseguite nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="5870d-162">You will create and execute these queries in later steps.</span></span>

### <a name="to-specify-the-database-connection"></a><span data-ttu-id="5870d-163">Per specificare la connessione al database</span><span class="sxs-lookup"><span data-stu-id="5870d-163">To specify the database connection</span></span>

- <span data-ttu-id="5870d-164">Digitare o incollare il codice seguente nel metodo `Main`:</span><span class="sxs-lookup"><span data-stu-id="5870d-164">Type or paste the following code into the `Main` method.</span></span>

     <span data-ttu-id="5870d-165">Si presuppone che il file `northwnd.mdf` si trovi nella cartella linqtest5.</span><span class="sxs-lookup"><span data-stu-id="5870d-165">Note that the `northwnd.mdf` file is assumed to be in the linqtest5 folder.</span></span> <span data-ttu-id="5870d-166">Per altre informazioni, vedere la sezione precedente relativa ai prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="5870d-166">For more information, see the Prerequisites section earlier in this walkthrough.</span></span>

     [!code-csharp[DLinqWalk1CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#4)]

## <a name="creating-a-simple-query"></a><span data-ttu-id="5870d-167">Creazione di una query semplice</span><span class="sxs-lookup"><span data-stu-id="5870d-167">Creating a Simple Query</span></span>

<span data-ttu-id="5870d-168">In questo passaggio viene creata una query per cercare i clienti nella tabella di database Customers residenti nell'area londinese.</span><span class="sxs-lookup"><span data-stu-id="5870d-168">In this step, you create a query to find which customers in the database Customers table are located in London.</span></span> <span data-ttu-id="5870d-169">Il codice della query in questo passaggio descrive semplicemente la query,</span><span class="sxs-lookup"><span data-stu-id="5870d-169">The query code in this step just describes the query.</span></span> <span data-ttu-id="5870d-170">ma non la esegue.</span><span class="sxs-lookup"><span data-stu-id="5870d-170">It does not execute it.</span></span> <span data-ttu-id="5870d-171">Questo approccio è noto come *esecuzione posticipata*.</span><span class="sxs-lookup"><span data-stu-id="5870d-171">This approach is known as *deferred execution*.</span></span> <span data-ttu-id="5870d-172">Per altre informazioni, vedere [Introduzione alle query LINQ (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).</span><span class="sxs-lookup"><span data-stu-id="5870d-172">For more information, see [Introduction to LINQ Queries (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).</span></span>

<span data-ttu-id="5870d-173">Verrà anche prodotto un output del log per mostrare i comandi SQL generati da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].</span><span class="sxs-lookup"><span data-stu-id="5870d-173">You will also produce a log output to show the SQL commands that [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] generates.</span></span> <span data-ttu-id="5870d-174">Questa funzionalità di registrazione, che usa <xref:System.Data.Linq.DataContext.Log%2A>, è utile per eseguire il debug e per determinare che i comandi inviati al database rappresentano accuratamente la query.</span><span class="sxs-lookup"><span data-stu-id="5870d-174">This logging feature (which uses <xref:System.Data.Linq.DataContext.Log%2A>) is helpful in debugging, and in determining that the commands being sent to the database accurately represent your query.</span></span>

### <a name="to-create-a-simple-query"></a><span data-ttu-id="5870d-175">Per creare una query semplice</span><span class="sxs-lookup"><span data-stu-id="5870d-175">To create a simple query</span></span>

- <span data-ttu-id="5870d-176">Digitare o incollare il codice seguente nel metodo `Main` dopo la dichiarazione `Table<Customer>`.</span><span class="sxs-lookup"><span data-stu-id="5870d-176">Type or paste the following code into the `Main` method after the `Table<Customer>` declaration.</span></span>

     [!code-csharp[DLinqWalk1ACS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#5)]

## <a name="executing-the-query"></a><span data-ttu-id="5870d-177">Esecuzione della query</span><span class="sxs-lookup"><span data-stu-id="5870d-177">Executing the Query</span></span>

<span data-ttu-id="5870d-178">In questo passaggio verrà effettivamente eseguita la query.</span><span class="sxs-lookup"><span data-stu-id="5870d-178">In this step, you actually execute the query.</span></span> <span data-ttu-id="5870d-179">Le espressioni di query create nei passaggi precedenti non vengono valutate finché i risultati non saranno necessari.</span><span class="sxs-lookup"><span data-stu-id="5870d-179">The query expressions you created in the previous steps are not evaluated until the results are needed.</span></span> <span data-ttu-id="5870d-180">Quando si inizia l'iterazione `foreach`, viene eseguito un comando SQL sul database e gli oggetti vengono materializzati.</span><span class="sxs-lookup"><span data-stu-id="5870d-180">When you begin the `foreach` iteration, a SQL command is executed against the database and objects are materialized.</span></span>

### <a name="to-execute-the-query"></a><span data-ttu-id="5870d-181">Per eseguire la query</span><span class="sxs-lookup"><span data-stu-id="5870d-181">To execute the query</span></span>

1. <span data-ttu-id="5870d-182">Digitare o incollare il codice seguente alla fine del metodo `Main` dopo la descrizione della query.</span><span class="sxs-lookup"><span data-stu-id="5870d-182">Type or paste the following code at the end of the `Main` method (after the query description).</span></span>

     [!code-csharp[DLinqWalk1ACS#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#6)]

2. <span data-ttu-id="5870d-183">‎Premere F5 per eseguire il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5870d-183">Press F5 to debug the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5870d-184">Se l'applicazione genera un errore di run-time, vedere la sezione relativa alla risoluzione dei problemi di [apprendimento per procedure dettagliate](learning-by-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="5870d-184">If your application generates a run-time error, see the Troubleshooting section of [Learning by Walkthroughs](learning-by-walkthroughs.md).</span></span>

     <span data-ttu-id="5870d-185">I risultati della query nella finestra della console dovrebbero avere il seguente aspetto:</span><span class="sxs-lookup"><span data-stu-id="5870d-185">The query results in the console window should appear as follows:</span></span>

     `ID=AROUT, City=London`

     `ID=BSBEV, City=London`

     `ID=CONSH, City=London`

     `ID=EASTC, City=London`

     `ID=NORTS, City=London`

     `ID=SEVES, City=London`

3. <span data-ttu-id="5870d-186">Premere INVIO nella finestra della console per chiudere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5870d-186">Press Enter in the console window to close the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5870d-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5870d-187">Next Steps</span></span>

<span data-ttu-id="5870d-188">L'argomento [procedura dettagliata: esecuzione di query tra relazioni (C#)](walkthrough-querying-across-relationships-csharp.md) continua dove termina questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="5870d-188">The [Walkthrough: Querying Across Relationships (C#)](walkthrough-querying-across-relationships-csharp.md) topic continues where this walkthrough ends.</span></span> <span data-ttu-id="5870d-189">Nella procedura dettagliata relativa alla query tra relazioni viene illustrato come è [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] possibile eseguire query tra tabelle, in modo analogo ai *join* in un database relazionale.</span><span class="sxs-lookup"><span data-stu-id="5870d-189">The Query Across Relationships walkthrough demonstrates how [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] can query across tables, similar to *joins* in a relational database.</span></span>

<span data-ttu-id="5870d-190">Se si desidera eseguire la procedura dettagliata relativa all'esecuzione di query tra relazioni, è indispensabile salvare la soluzione per la procedura dettagliata appena completata.</span><span class="sxs-lookup"><span data-stu-id="5870d-190">If you want to do the Query Across Relationships walkthrough, make sure to save the solution for the walkthrough you have just completed, which is a prerequisite.</span></span>

## <a name="see-also"></a><span data-ttu-id="5870d-191">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="5870d-191">See also</span></span>

- [<span data-ttu-id="5870d-192">Apprendimento tramite procedure dettagliate</span><span class="sxs-lookup"><span data-stu-id="5870d-192">Learning by Walkthroughs</span></span>](learning-by-walkthroughs.md)

---
title: 'Esercitazione: classificare i fiori Iris-clustering k-means'
description: Informazioni su come usare ML.NET in uno scenario di clustering
author: pkulikov
ms.date: 06/30/2020
ms.topic: tutorial
ms.custom: mvc, title-hack-0516
ms.openlocfilehash: 0cc42a196589a7ffe77300c9f2cd9cb28229a0a9
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803976"
---
# <a name="tutorial-categorize-iris-flowers-using-k-means-clustering-with-mlnet"></a><span data-ttu-id="c35e7-103">Esercitazione: categorizzare i fiori Iris con il clustering k-means con ML.NET</span><span class="sxs-lookup"><span data-stu-id="c35e7-103">Tutorial: Categorize iris flowers using k-means clustering with ML.NET</span></span>

<span data-ttu-id="c35e7-104">Questa esercitazione illustra come usare ML.NET per compilare un [modello di clustering](../resources/tasks.md#clustering) per il [set di dati dei fiori iris](https://en.wikipedia.org/wiki/Iris_flower_data_set).</span><span class="sxs-lookup"><span data-stu-id="c35e7-104">This tutorial illustrates how to use ML.NET to build a [clustering model](../resources/tasks.md#clustering) for the [iris flower data set](https://en.wikipedia.org/wiki/Iris_flower_data_set).</span></span>

<span data-ttu-id="c35e7-105">In questa esercitazione verranno illustrate le procedure per:</span><span class="sxs-lookup"><span data-stu-id="c35e7-105">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
>
> - <span data-ttu-id="c35e7-106">Informazioni sul problema</span><span class="sxs-lookup"><span data-stu-id="c35e7-106">Understand the problem</span></span>
> - <span data-ttu-id="c35e7-107">Selezionare l'attività di apprendimento automatico appropriata</span><span class="sxs-lookup"><span data-stu-id="c35e7-107">Select the appropriate machine learning task</span></span>
> - <span data-ttu-id="c35e7-108">Preparare i dati</span><span class="sxs-lookup"><span data-stu-id="c35e7-108">Prepare the data</span></span>
> - <span data-ttu-id="c35e7-109">Caricare e trasformare i dati</span><span class="sxs-lookup"><span data-stu-id="c35e7-109">Load and transform the data</span></span>
> - <span data-ttu-id="c35e7-110">Scegliere un algoritmo di apprendimento</span><span class="sxs-lookup"><span data-stu-id="c35e7-110">Choose a learning algorithm</span></span>
> - <span data-ttu-id="c35e7-111">Eseguire il training del modello</span><span class="sxs-lookup"><span data-stu-id="c35e7-111">Train the model</span></span>
> - <span data-ttu-id="c35e7-112">Usare il modello per le stime</span><span class="sxs-lookup"><span data-stu-id="c35e7-112">Use the model for predictions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c35e7-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c35e7-113">Prerequisites</span></span>

- <span data-ttu-id="c35e7-114">[Visual studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) o versione successiva o visual studio 2017 versione 15,6 o successiva con il carico di lavoro "sviluppo multipiattaforma .NET Core" installato.</span><span class="sxs-lookup"><span data-stu-id="c35e7-114">[Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) or later or Visual Studio 2017 version 15.6 or later with the ".NET Core cross-platform development" workload installed.</span></span>

## <a name="understand-the-problem"></a><span data-ttu-id="c35e7-115">Informazioni sul problema</span><span class="sxs-lookup"><span data-stu-id="c35e7-115">Understand the problem</span></span>

<span data-ttu-id="c35e7-116">Questo problema riguarda il set dei fiori iris in gruppi diversi in base alle caratteristiche dei fiori.</span><span class="sxs-lookup"><span data-stu-id="c35e7-116">This problem is about dividing the set of iris flowers in different groups based on the flower features.</span></span> <span data-ttu-id="c35e7-117">Tali caratteristiche sono la lunghezza e la larghezza di un sepalo e la lunghezza e la larghezza di un petalo.</span><span class="sxs-lookup"><span data-stu-id="c35e7-117">Those features are the length and width of a sepal and the length and width of a petal.</span></span> <span data-ttu-id="c35e7-118">Per questa esercitazione, si supponga che il tipo di ogni fiore sia sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="c35e7-118">For this tutorial, assume that the type of each flower is unknown.</span></span> <span data-ttu-id="c35e7-119">Si desidera apprendere la struttura di un set di dati dalle caratteristiche e prevedere come un'istanza di dati si adatta a questa struttura.</span><span class="sxs-lookup"><span data-stu-id="c35e7-119">You want to learn the structure of a data set from the features and predict how a data instance fits this structure.</span></span>

## <a name="select-the-appropriate-machine-learning-task"></a><span data-ttu-id="c35e7-120">Selezionare l'attività di apprendimento automatico appropriata</span><span class="sxs-lookup"><span data-stu-id="c35e7-120">Select the appropriate machine learning task</span></span>

<span data-ttu-id="c35e7-121">Poiché non si sa a quale gruppo appartenga ciascun fiore, scegliere l'attività di [apprendimento automatico senza supervisione](../resources/glossary.md#unsupervised-machine-learning).</span><span class="sxs-lookup"><span data-stu-id="c35e7-121">As you don't know to which group each flower belongs to, you choose the [unsupervised machine learning](../resources/glossary.md#unsupervised-machine-learning) task.</span></span> <span data-ttu-id="c35e7-122">Per dividere un set di dati in gruppi in modo che gli elementi nello stesso gruppo siano più simili tra loro rispetto a quelli di altri gruppi, usare un'attività di apprendimento automatico di [clustering](../resources/tasks.md#clustering).</span><span class="sxs-lookup"><span data-stu-id="c35e7-122">To divide a data set in groups in such a way that elements in the same group are more similar to each other than to those in other groups, use a [clustering](../resources/tasks.md#clustering) machine learning task.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="c35e7-123">Creare un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="c35e7-123">Create a console application</span></span>

1. <span data-ttu-id="c35e7-124">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c35e7-124">Open Visual Studio.</span></span> <span data-ttu-id="c35e7-125">Scegliere **file**  >  **nuovo**  >  **progetto** dalla barra dei menu.</span><span class="sxs-lookup"><span data-stu-id="c35e7-125">Select **File** > **New** > **Project** from the menu bar.</span></span> <span data-ttu-id="c35e7-126">Nella finestra di dialogo **nuovo progetto** selezionare il nodo **Visual C#** seguito dal nodo **.NET Core** .</span><span class="sxs-lookup"><span data-stu-id="c35e7-126">In the **New Project** dialog, select the **Visual C#** node followed by the **.NET Core** node.</span></span> <span data-ttu-id="c35e7-127">Selezionare quindi il modello di progetto **App Console (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="c35e7-127">Then select the **Console App (.NET Core)** project template.</span></span> <span data-ttu-id="c35e7-128">Nella casella di testo **Nome** digitare "IrisFlowerClustering" e quindi selezionare il pulsante **OK**.</span><span class="sxs-lookup"><span data-stu-id="c35e7-128">In the **Name** text box, type "IrisFlowerClustering" and then select the **OK** button.</span></span>

1. <span data-ttu-id="c35e7-129">Creare una directory denominata *Data* nel progetto per archiviare il set di dati e i file di modello:</span><span class="sxs-lookup"><span data-stu-id="c35e7-129">Create a directory named *Data* in your project to store the data set and model files:</span></span>

    <span data-ttu-id="c35e7-130">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Aggiungi** > **Nuova cartella**.</span><span class="sxs-lookup"><span data-stu-id="c35e7-130">In **Solution Explorer**, right-click the project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="c35e7-131">Digitare "Data" e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="c35e7-131">Type "Data" and hit Enter.</span></span>

1. <span data-ttu-id="c35e7-132">Installare il pacchetto NuGet **Microsoft.ml** :</span><span class="sxs-lookup"><span data-stu-id="c35e7-132">Install the **Microsoft.ML** NuGet package:</span></span>

    [!INCLUDE [mlnet-current-nuget-version](../../../includes/mlnet-current-nuget-version.md)]

    <span data-ttu-id="c35e7-133">In **Esplora soluzioni**fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c35e7-133">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="c35e7-134">Scegliere "nuget.org" come origine del pacchetto, selezionare la scheda **Sfoglia** , cercare **Microsoft.ml** e selezionare il pulsante **Installa** .</span><span class="sxs-lookup"><span data-stu-id="c35e7-134">Choose "nuget.org" as the Package source, select the **Browse** tab, search for **Microsoft.ML** and select the **Install** button.</span></span> <span data-ttu-id="c35e7-135">Selezionare il pulsante **OK** nella finestra di dialogo **Anteprima modifiche** e quindi selezionare il pulsante **Accetto** nella finestra di dialogo **Accettazione della licenza** se si accettano le condizioni di licenza per i pacchetti elencati.</span><span class="sxs-lookup"><span data-stu-id="c35e7-135">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the **License Acceptance** dialog if you agree with the license terms for the packages listed.</span></span>

## <a name="prepare-the-data"></a><span data-ttu-id="c35e7-136">Preparare i dati</span><span class="sxs-lookup"><span data-stu-id="c35e7-136">Prepare the data</span></span>

1. <span data-ttu-id="c35e7-137">Scaricare il set di dati [iris.data](https://github.com/dotnet/machinelearning/blob/master/test/data/iris.data) e salvarlo nella cartella *Dati* creata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="c35e7-137">Download the [iris.data](https://github.com/dotnet/machinelearning/blob/master/test/data/iris.data) data set and save it to the *Data* folder you've created at the previous step.</span></span> <span data-ttu-id="c35e7-138">Per altre informazioni sui set di dati iris, vedere la pagina [Dataset Iris](https://en.wikipedia.org/wiki/Iris_flower_data_set) di Wikipedia e la pagina [Iris Data Set](http://archive.ics.uci.edu/ml/datasets/Iris), che rappresenta l'origine del set di dati.</span><span class="sxs-lookup"><span data-stu-id="c35e7-138">For more information about the iris data set, see the [Iris flower data set](https://en.wikipedia.org/wiki/Iris_flower_data_set) Wikipedia page and the [Iris Data Set](http://archive.ics.uci.edu/ml/datasets/Iris) page, which is the source of the data set.</span></span>

1. <span data-ttu-id="c35e7-139">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul file *iris.data* e selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="c35e7-139">In **Solution Explorer**, right-click the *iris.data* file and select **Properties**.</span></span> <span data-ttu-id="c35e7-140">In **Avanzate**impostare il valore di **copia nella directory di output** su **copia se più recente**.</span><span class="sxs-lookup"><span data-stu-id="c35e7-140">Under **Advanced**, change the value of **Copy to Output Directory** to **Copy if newer**.</span></span>

<span data-ttu-id="c35e7-141">Il file *iris.data* contiene cinque colonne che rappresentano:</span><span class="sxs-lookup"><span data-stu-id="c35e7-141">The *iris.data* file contains five columns that represent:</span></span>

- <span data-ttu-id="c35e7-142">lunghezza SEPA in centimetri</span><span class="sxs-lookup"><span data-stu-id="c35e7-142">sepal length in centimeters</span></span>
- <span data-ttu-id="c35e7-143">Larghezza SEPA in centimetri</span><span class="sxs-lookup"><span data-stu-id="c35e7-143">sepal width in centimeters</span></span>
- <span data-ttu-id="c35e7-144">lunghezza petalo in centimetri</span><span class="sxs-lookup"><span data-stu-id="c35e7-144">petal length in centimeters</span></span>
- <span data-ttu-id="c35e7-145">Larghezza petalo in centimetri</span><span class="sxs-lookup"><span data-stu-id="c35e7-145">petal width in centimeters</span></span>
- <span data-ttu-id="c35e7-146">tipo di fiore iris</span><span class="sxs-lookup"><span data-stu-id="c35e7-146">type of iris flower</span></span>

<span data-ttu-id="c35e7-147">Per l'esempio del clustering, questa esercitazione ignora l'ultima colonna.</span><span class="sxs-lookup"><span data-stu-id="c35e7-147">For the sake of the clustering example, this tutorial ignores the last column.</span></span>

## <a name="create-data-classes"></a><span data-ttu-id="c35e7-148">Creare classi di dati</span><span class="sxs-lookup"><span data-stu-id="c35e7-148">Create data classes</span></span>

<span data-ttu-id="c35e7-149">Creare le classi per i dati di input e le stime:</span><span class="sxs-lookup"><span data-stu-id="c35e7-149">Create classes for the input data and the predictions:</span></span>

1. <span data-ttu-id="c35e7-150">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e quindi selezionare **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="c35e7-150">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span>
1. <span data-ttu-id="c35e7-151">Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Classe** e impostare il campo **Nome** su *IrisData.cs*.</span><span class="sxs-lookup"><span data-stu-id="c35e7-151">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *IrisData.cs*.</span></span> <span data-ttu-id="c35e7-152">Selezionare quindi il pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c35e7-152">Then, select the **Add** button.</span></span>
1. <span data-ttu-id="c35e7-153">Aggiungere la direttiva `using` seguente al nuovo file:</span><span class="sxs-lookup"><span data-stu-id="c35e7-153">Add the following `using` directive to the new file:</span></span>

   [!code-csharp[Add necessary usings](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/IrisData.cs#Usings)]

<span data-ttu-id="c35e7-154">Rimuovere la definizione di classe esistente e aggiungere il codice seguente, che contiene le classi `IrisData` e `ClusterPrediction`, al file *IrisData.cs*:</span><span class="sxs-lookup"><span data-stu-id="c35e7-154">Remove the existing class definition and add the following code, which defines the classes `IrisData` and `ClusterPrediction`, to the *IrisData.cs* file:</span></span>

[!code-csharp[Define data classes](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/IrisData.cs#ClassDefinitions)]

<span data-ttu-id="c35e7-155">`IrisData` è la classe dei dati di input e contiene le definizioni per ogni caratteristica del set di dati.</span><span class="sxs-lookup"><span data-stu-id="c35e7-155">`IrisData` is the input data class and has definitions for each feature from the data set.</span></span> <span data-ttu-id="c35e7-156">Usare l'attributo [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute) per specificare gli indici delle colonne di origine nel file del set di dati.</span><span class="sxs-lookup"><span data-stu-id="c35e7-156">Use the [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute) attribute to specify the indices of the source columns in the data set file.</span></span>

<span data-ttu-id="c35e7-157">La classe `ClusterPrediction` rappresenta l'output del modello di clustering applicato a un'istanza `IrisData`.</span><span class="sxs-lookup"><span data-stu-id="c35e7-157">The `ClusterPrediction` class represents the output of the clustering model applied to an `IrisData` instance.</span></span> <span data-ttu-id="c35e7-158">Usare l'attributo [ColumnName](xref:Microsoft.ML.Data.ColumnNameAttribute) per associare i campi `PredictedClusterId` e `Distances` rispettivamente alle colonne **PredictedLabel** e **Score**.</span><span class="sxs-lookup"><span data-stu-id="c35e7-158">Use the [ColumnName](xref:Microsoft.ML.Data.ColumnNameAttribute) attribute to bind the `PredictedClusterId` and `Distances` fields to the **PredictedLabel** and **Score** columns respectively.</span></span> <span data-ttu-id="c35e7-159">In caso di attività di clustering, queste colonne hanno il significato seguente:</span><span class="sxs-lookup"><span data-stu-id="c35e7-159">In case of the clustering task those columns have the following meaning:</span></span>

- <span data-ttu-id="c35e7-160">La colonna **PredictedLabel** include l'ID del cluster stimato.</span><span class="sxs-lookup"><span data-stu-id="c35e7-160">**PredictedLabel** column contains the ID of the predicted cluster.</span></span>
- <span data-ttu-id="c35e7-161">La colonna **Score** contiene una matrice con le distanze Euclidee quadrate rispetto ai centroidi del cluster.</span><span class="sxs-lookup"><span data-stu-id="c35e7-161">**Score** column contains an array with squared Euclidean distances to the cluster centroids.</span></span> <span data-ttu-id="c35e7-162">La lunghezza della matrice è uguale al numero di cluster.</span><span class="sxs-lookup"><span data-stu-id="c35e7-162">The array length is equal to the number of clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="c35e7-163">Usare il tipo `float` per rappresentare i valori a virgola mobile nelle classi di dati di input e di previsione.</span><span class="sxs-lookup"><span data-stu-id="c35e7-163">Use the `float` type to represent floating-point values in the input and prediction data classes.</span></span>

## <a name="define-data-and-model-paths"></a><span data-ttu-id="c35e7-164">Definire i percorsi dei dati e del modello</span><span class="sxs-lookup"><span data-stu-id="c35e7-164">Define data and model paths</span></span>

<span data-ttu-id="c35e7-165">Tornare al file *Program.cs* e aggiungere due campi per i percorsi del file dei set di dati e del file per il salvataggio del modello:</span><span class="sxs-lookup"><span data-stu-id="c35e7-165">Go back to the *Program.cs* file and add two fields to hold the paths to the data set file and to the file to save the model:</span></span>

- <span data-ttu-id="c35e7-166">`_dataPath` contiene il percorso del file con il set di dati usato per il training del modello.</span><span class="sxs-lookup"><span data-stu-id="c35e7-166">`_dataPath` contains the path to the file with the data set used to train the model.</span></span>
- <span data-ttu-id="c35e7-167">`_modelPath` contiene il percorso del file in cui è archiviato il modello sottoposto a training.</span><span class="sxs-lookup"><span data-stu-id="c35e7-167">`_modelPath` contains the path to the file where the trained model is stored.</span></span>

<span data-ttu-id="c35e7-168">Aggiungere il codice seguente immediatamente sopra il metodo `Main` per specificare questi percorsi:</span><span class="sxs-lookup"><span data-stu-id="c35e7-168">Add the following code right above the `Main` method to specify those paths:</span></span>

[!code-csharp[Initialize paths](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/Program.cs#Paths)]

<span data-ttu-id="c35e7-169">Per consentire la compilazione del codice precedente, aggiungere le direttive `using` seguenti all'inizio del file *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="c35e7-169">To make the preceding code compile, add the following `using` directives at the top of the *Program.cs* file:</span></span>

[!code-csharp[Add usings for paths](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/Program.cs#UsingsForPaths)]

## <a name="create-ml-context"></a><span data-ttu-id="c35e7-170">Creare il contesto di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c35e7-170">Create ML context</span></span>

<span data-ttu-id="c35e7-171">Aggiungere le direttive `using` seguenti all'inizio del file *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="c35e7-171">Add the following additional `using` directives to the top of the *Program.cs* file:</span></span>

[!code-csharp[Add Microsoft.ML usings](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/Program.cs#MLUsings)]

<span data-ttu-id="c35e7-172">Nel metodo `Main` sostituire la riga `Console.WriteLine("Hello World!");` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c35e7-172">In the `Main` method, replace the `Console.WriteLine("Hello World!");` line with the following code:</span></span>

[!code-csharp[Create ML context](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/Program.cs#CreateContext)]

<span data-ttu-id="c35e7-173">La classe <xref:Microsoft.ML.MLContext?displayProperty=nameWithType> rappresenta l'ambiente di machine learning (apprendimento automatico) e offre meccanismi per la registrazione e punti di ingresso per il caricamento dei dati, il training del modello, le stime e altre attività.</span><span class="sxs-lookup"><span data-stu-id="c35e7-173">The <xref:Microsoft.ML.MLContext?displayProperty=nameWithType> class represents the machine learning environment and provides mechanisms for logging and entry points for data loading, model training, prediction, and other tasks.</span></span> <span data-ttu-id="c35e7-174">A livello concettuale questa operazione è paragonabile all'uso di `DbContext` in Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="c35e7-174">This is comparable conceptually to using `DbContext` in Entity Framework.</span></span>

## <a name="set-up-data-loading"></a><span data-ttu-id="c35e7-175">Configurare il caricamento dei dati</span><span class="sxs-lookup"><span data-stu-id="c35e7-175">Set up data loading</span></span>

<span data-ttu-id="c35e7-176">Aggiungere il codice seguente al `Main` metodo per configurare la modalità di caricamento dei dati:</span><span class="sxs-lookup"><span data-stu-id="c35e7-176">Add the following code to the `Main` method to set up the way to load data:</span></span>

[!code-csharp[Create text loader](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/Program.cs#CreateDataView)]

<span data-ttu-id="c35e7-177">Il [ `MLContext.Data.LoadFromTextFile` metodo di estensione](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) generico deduce lo schema del set di dati dal `IrisData` tipo fornito e restituisce <xref:Microsoft.ML.IDataView> che può essere utilizzato come input per i trasformatori.</span><span class="sxs-lookup"><span data-stu-id="c35e7-177">The generic [`MLContext.Data.LoadFromTextFile` extension method](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) infers the data set schema from the provided `IrisData` type and returns <xref:Microsoft.ML.IDataView> which can be used as input for transformers.</span></span>

## <a name="create-a-learning-pipeline"></a><span data-ttu-id="c35e7-178">Creare una pipeline di apprendimento</span><span class="sxs-lookup"><span data-stu-id="c35e7-178">Create a learning pipeline</span></span>

<span data-ttu-id="c35e7-179">Per questa esercitazione, la pipeline di apprendimento dell'attività di clustering è costituita dai due passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c35e7-179">For this tutorial, the learning pipeline of the clustering task comprises two following steps:</span></span>

- <span data-ttu-id="c35e7-180">Concatenare le colonne caricate in un'unica colonna **Features**, che viene usata da un trainer di clustering;</span><span class="sxs-lookup"><span data-stu-id="c35e7-180">concatenate loaded columns into one **Features** column, which is used by a clustering trainer;</span></span>
- <span data-ttu-id="c35e7-181">Usare un trainer <xref:Microsoft.ML.Trainers.KMeansTrainer> per eseguire il training del modello usando l'algoritmo di clustering k-means++.</span><span class="sxs-lookup"><span data-stu-id="c35e7-181">use a <xref:Microsoft.ML.Trainers.KMeansTrainer> trainer to train the model using the k-means++ clustering algorithm.</span></span>

<span data-ttu-id="c35e7-182">Aggiungere il codice seguente al metodo `Main`:</span><span class="sxs-lookup"><span data-stu-id="c35e7-182">Add the following code to the `Main` method:</span></span>

[!code-csharp[Create pipeline](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/Program.cs#CreatePipeline)]

<span data-ttu-id="c35e7-183">Il codice specifica che il set di dati deve essere suddiviso in tre cluster.</span><span class="sxs-lookup"><span data-stu-id="c35e7-183">The code specifies that the data set should be split in three clusters.</span></span>

## <a name="train-the-model"></a><span data-ttu-id="c35e7-184">Eseguire il training del modello</span><span class="sxs-lookup"><span data-stu-id="c35e7-184">Train the model</span></span>

<span data-ttu-id="c35e7-185">I passaggi aggiunti nelle sezioni precedenti hanno preparato la pipeline per il training, che tuttavia non è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="c35e7-185">The steps added in the preceding sections prepared the pipeline for training, however, none have been executed.</span></span> <span data-ttu-id="c35e7-186">Aggiungere la riga seguente al metodo `Main` per eseguire il caricamento dei dati e il training del modello:</span><span class="sxs-lookup"><span data-stu-id="c35e7-186">Add the following line to the `Main` method to perform data loading and model training:</span></span>

[!code-csharp[Train the model](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/Program.cs#TrainModel)]

### <a name="save-the-model"></a><span data-ttu-id="c35e7-187">Salvare il modello</span><span class="sxs-lookup"><span data-stu-id="c35e7-187">Save the model</span></span>

<span data-ttu-id="c35e7-188">A questo punto, è disponibile un modello che può essere integrato in tutte le applicazioni .NET nuove o esistenti.</span><span class="sxs-lookup"><span data-stu-id="c35e7-188">At this point, you have a model that can be integrated into any of your existing or new .NET applications.</span></span> <span data-ttu-id="c35e7-189">Per salvare il modello in un file con estensione zip, aggiungere il codice seguente al metodo `Main`:</span><span class="sxs-lookup"><span data-stu-id="c35e7-189">To save your model to a .zip file, add the following code to the `Main` method:</span></span>

[!code-csharp[Save the model](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/Program.cs#SaveModel)]

## <a name="use-the-model-for-predictions"></a><span data-ttu-id="c35e7-190">Usare il modello per le stime</span><span class="sxs-lookup"><span data-stu-id="c35e7-190">Use the model for predictions</span></span>

<span data-ttu-id="c35e7-191">Per eseguire stime, usare la classe <xref:Microsoft.ML.PredictionEngine%602>, che accetta le istanze del tipo di input tramite la pipeline convertitore e genera istanze del tipo di output.</span><span class="sxs-lookup"><span data-stu-id="c35e7-191">To make predictions, use the <xref:Microsoft.ML.PredictionEngine%602> class that takes instances of the input type through the transformer pipeline and produces instances of the output type.</span></span> <span data-ttu-id="c35e7-192">Aggiungere la riga seguente al metodo `Main` per creare un'istanza della classe:</span><span class="sxs-lookup"><span data-stu-id="c35e7-192">Add the following line to the `Main` method to create an instance of that class:</span></span>

[!code-csharp[Create predictor](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/Program.cs#Predictor)]

<span data-ttu-id="c35e7-193">[PredictionEngine](xref:Microsoft.ML.PredictionEngine%602) è un'API di praticità, che consente di eseguire una stima su una singola istanza di dati.</span><span class="sxs-lookup"><span data-stu-id="c35e7-193">The [PredictionEngine](xref:Microsoft.ML.PredictionEngine%602) is a convenience API, which allows you to perform a prediction on a single instance of data.</span></span> <span data-ttu-id="c35e7-194">[`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)non è thread-safe.</span><span class="sxs-lookup"><span data-stu-id="c35e7-194">[`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) is not thread-safe.</span></span> <span data-ttu-id="c35e7-195">È accettabile usare in ambienti a thread singolo o prototipi.</span><span class="sxs-lookup"><span data-stu-id="c35e7-195">It's acceptable to use in single-threaded or prototype environments.</span></span> <span data-ttu-id="c35e7-196">Per migliorare le prestazioni e thread safety negli ambienti di produzione, utilizzare il `PredictionEnginePool` servizio, che consente di creare un oggetto [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) di [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) oggetti da utilizzare nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c35e7-196">For improved performance and thread safety in production environments, use the `PredictionEnginePool` service, which creates an [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601) of [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) objects for use throughout your application.</span></span> <span data-ttu-id="c35e7-197">Vedere questa guida su come [usare `PredictionEnginePool` in un'API Web di ASP.NET Core](../how-to-guides/serve-model-web-api-ml-net.md#register-predictionenginepool-for-use-in-the-application).</span><span class="sxs-lookup"><span data-stu-id="c35e7-197">See this guide on how to [use `PredictionEnginePool` in an ASP.NET Core Web API](../how-to-guides/serve-model-web-api-ml-net.md#register-predictionenginepool-for-use-in-the-application).</span></span>

> [!NOTE]
> <span data-ttu-id="c35e7-198">L'estensione del servizio `PredictionEnginePool` è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="c35e7-198">`PredictionEnginePool` service extension is currently in preview.</span></span>

<span data-ttu-id="c35e7-199">Creare la classe `TestIrisData` per ospitare le istanze dei dati di test:</span><span class="sxs-lookup"><span data-stu-id="c35e7-199">Create the `TestIrisData` class to house test data instances:</span></span>

1. <span data-ttu-id="c35e7-200">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e quindi selezionare **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="c35e7-200">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span>
1. <span data-ttu-id="c35e7-201">Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Classe** e impostare il campo **Nome** su *TestIrisData.cs*.</span><span class="sxs-lookup"><span data-stu-id="c35e7-201">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *TestIrisData.cs*.</span></span> <span data-ttu-id="c35e7-202">Selezionare quindi il pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c35e7-202">Then, select the **Add** button.</span></span>
1. <span data-ttu-id="c35e7-203">Modificare la classe in modo da renderla statica, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c35e7-203">Modify the class to be static like in the following example:</span></span>

   [!code-csharp[Make class static](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/TestIrisData.cs#Static)]

<span data-ttu-id="c35e7-204">Questa esercitazione presenta un'istanza di dati iris all'interno di questa classe.</span><span class="sxs-lookup"><span data-stu-id="c35e7-204">This tutorial introduces one iris data instance within this class.</span></span> <span data-ttu-id="c35e7-205">È possibile aggiungere altri scenari da sperimentare con il modello.</span><span class="sxs-lookup"><span data-stu-id="c35e7-205">You can add other scenarios to experiment with the model.</span></span> <span data-ttu-id="c35e7-206">Aggiungere il codice seguente nella classe `TestIrisData`:</span><span class="sxs-lookup"><span data-stu-id="c35e7-206">Add the following code into the `TestIrisData` class:</span></span>

[!code-csharp[Test data](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/TestIrisData.cs#TestData)]

<span data-ttu-id="c35e7-207">Per individuare il cluster a cui appartiene l'elemento specificato, tornare al file *Program.cs* e aggiungere il codice seguente nel metodo `Main`:</span><span class="sxs-lookup"><span data-stu-id="c35e7-207">To find out the cluster to which the specified item belongs to, go back to the *Program.cs* file and add the following code into the `Main` method:</span></span>

[!code-csharp[Predict and output results](~/samples/snippets/machine-learning/IrisFlowerClustering/csharp/Program.cs#PredictionExample)]

<span data-ttu-id="c35e7-208">Eseguire il programma per vedere quale cluster contiene l'istanza dati specificata e le distanze al quadrato da tale istanza ai centroidi del cluster.</span><span class="sxs-lookup"><span data-stu-id="c35e7-208">Run the program to see which cluster contains the specified data instance and squared distances from that instance to the cluster centroids.</span></span> <span data-ttu-id="c35e7-209">I risultati saranno simili ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="c35e7-209">Your results should be similar to the following:</span></span>

```text
Cluster: 2
Distances: 11.69127 0.02159119 25.59896
```

<span data-ttu-id="c35e7-210">Congratulazioni!</span><span class="sxs-lookup"><span data-stu-id="c35e7-210">Congratulations!</span></span> <span data-ttu-id="c35e7-211">È stato creato un modello di apprendimento automatico per il clustering iris, quindi il modello è stato usato per produrre stime.</span><span class="sxs-lookup"><span data-stu-id="c35e7-211">You've now successfully built a machine learning model for iris clustering and used it to make predictions.</span></span> <span data-ttu-id="c35e7-212">È possibile trovare il codice sorgente per questa esercitazione nel repository GitHub [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/IrisFlowerClustering).</span><span class="sxs-lookup"><span data-stu-id="c35e7-212">You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/IrisFlowerClustering) GitHub repository.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c35e7-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c35e7-213">Next steps</span></span>

<span data-ttu-id="c35e7-214">In questa esercitazione sono state illustrate le procedure per:</span><span class="sxs-lookup"><span data-stu-id="c35e7-214">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
>
> - <span data-ttu-id="c35e7-215">Informazioni sul problema</span><span class="sxs-lookup"><span data-stu-id="c35e7-215">Understand the problem</span></span>
> - <span data-ttu-id="c35e7-216">Selezionare l'attività di apprendimento automatico appropriata</span><span class="sxs-lookup"><span data-stu-id="c35e7-216">Select the appropriate machine learning task</span></span>
> - <span data-ttu-id="c35e7-217">Preparare i dati</span><span class="sxs-lookup"><span data-stu-id="c35e7-217">Prepare the data</span></span>
> - <span data-ttu-id="c35e7-218">Caricare e trasformare i dati</span><span class="sxs-lookup"><span data-stu-id="c35e7-218">Load and transform the data</span></span>
> - <span data-ttu-id="c35e7-219">Scegliere un algoritmo di apprendimento</span><span class="sxs-lookup"><span data-stu-id="c35e7-219">Choose a learning algorithm</span></span>
> - <span data-ttu-id="c35e7-220">Eseguire il training del modello</span><span class="sxs-lookup"><span data-stu-id="c35e7-220">Train the model</span></span>
> - <span data-ttu-id="c35e7-221">Usare il modello per le stime</span><span class="sxs-lookup"><span data-stu-id="c35e7-221">Use the model for predictions</span></span>

<span data-ttu-id="c35e7-222">Visitare il repository GitHub per ottenere altre informazioni ed esempi.</span><span class="sxs-lookup"><span data-stu-id="c35e7-222">Check out our GitHub repository to continue learning and find more samples.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c35e7-223">Repository GitHub dotnet/machinelearning</span><span class="sxs-lookup"><span data-stu-id="c35e7-223">dotnet/machinelearning GitHub repository</span></span>](https://github.com/dotnet/machinelearning/)

---
title: 'Esercitazione: Rilevare gli oggetti usando un modello di deep learning ONNXTutorial: Detect objects using an ONNX deep learning model'
description: Questa esercitazione illustra come usare un modello di Deep Learning ONNX già sottoposto a training in ML.NET per rilevare gli oggetti nelle immagini.
author: luisquintanilla
ms.author: luquinta
ms.date: 01/30/2020
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: d9677c6c9da542123146fc9eef9c311ef30c174e
ms.sourcegitcommit: d9470d8b2278b33108332c05224d86049cb9484b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81608010"
---
# <a name="tutorial-detect-objects-using-onnx-in-mlnet"></a><span data-ttu-id="b44e8-103">Esercitazione: Rilevare gli oggetti utilizzando ONNX in ML.NET</span><span class="sxs-lookup"><span data-stu-id="b44e8-103">Tutorial: Detect objects using ONNX in ML.NET</span></span>

<span data-ttu-id="b44e8-104">Informazioni su come usare un modello ONNX già sottoposto a training in ML.NET per rilevare gli oggetti nelle immagini.</span><span class="sxs-lookup"><span data-stu-id="b44e8-104">Learn how to use a pre-trained ONNX model in ML.NET to detect objects in images.</span></span>

<span data-ttu-id="b44e8-105">Il training di un modello di rilevamento degli oggetti da zero richiede l'impostazione di milioni di parametri, numerosi dati di training con etichetta e una notevole quantità di risorse di calcolo (centinaia di ore di GPU).</span><span class="sxs-lookup"><span data-stu-id="b44e8-105">Training an object detection model from scratch requires setting millions of parameters, a large amount of labeled training data and a vast amount of compute resources (hundreds of GPU hours).</span></span> <span data-ttu-id="b44e8-106">L'uso di un modello già sottoposto a training consente di abbreviare il processo di training.</span><span class="sxs-lookup"><span data-stu-id="b44e8-106">Using a pre-trained model allows you to shortcut the training process.</span></span>

<span data-ttu-id="b44e8-107">In questa esercitazione verranno illustrate le procedure per:</span><span class="sxs-lookup"><span data-stu-id="b44e8-107">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
>
> - <span data-ttu-id="b44e8-108">Informazioni sul problema</span><span class="sxs-lookup"><span data-stu-id="b44e8-108">Understand the problem</span></span>
> - <span data-ttu-id="b44e8-109">Acquisire familiarità con ONNX e comprenderne il funzionamento con ML.NET</span><span class="sxs-lookup"><span data-stu-id="b44e8-109">Learn what ONNX is and how it works with ML.NET</span></span>
> - <span data-ttu-id="b44e8-110">Acquisire familiarità con il modello</span><span class="sxs-lookup"><span data-stu-id="b44e8-110">Understand the model</span></span>
> - <span data-ttu-id="b44e8-111">Riutilizzare il modello già sottoposto a training</span><span class="sxs-lookup"><span data-stu-id="b44e8-111">Reuse the pre-trained model</span></span>
> - <span data-ttu-id="b44e8-112">Rilevare oggetti con un modello caricato</span><span class="sxs-lookup"><span data-stu-id="b44e8-112">Detect objects with a loaded model</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="b44e8-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b44e8-113">Pre-requisites</span></span>

- <span data-ttu-id="b44e8-114">[Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) o versione successiva o Visual Studio 2017 versione 15.6 o successiva con il carico di lavoro "sviluppo multipiattaforma .NET Core" installato.</span><span class="sxs-lookup"><span data-stu-id="b44e8-114">[Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) or later or Visual Studio 2017 version 15.6 or later with the ".NET Core cross-platform development" workload installed.</span></span>
- [<span data-ttu-id="b44e8-115">Pacchetto NuGet Microsoft.ML</span><span class="sxs-lookup"><span data-stu-id="b44e8-115">Microsoft.ML NuGet Package</span></span>](https://www.nuget.org/packages/Microsoft.ML/)
- [<span data-ttu-id="b44e8-116">Pacchetto NuGet Microsoft.ML.ImageAnalytics</span><span class="sxs-lookup"><span data-stu-id="b44e8-116">Microsoft.ML.ImageAnalytics NuGet Package</span></span>](https://www.nuget.org/packages/Microsoft.ML.ImageAnalytics/)
- [<span data-ttu-id="b44e8-117">Pacchetto NuGet Microsoft.ML.OnnxTransformer</span><span class="sxs-lookup"><span data-stu-id="b44e8-117">Microsoft.ML.OnnxTransformer NuGet Package</span></span>](https://www.nuget.org/packages/Microsoft.ML.OnnxTransformer/)
- [<span data-ttu-id="b44e8-118">Modello Tiny YOLOv2 già sottoposto a training</span><span class="sxs-lookup"><span data-stu-id="b44e8-118">Tiny YOLOv2 pre-trained model</span></span>](https://github.com/onnx/models/tree/master/vision/object_detection_segmentation/tiny_yolov2)
- <span data-ttu-id="b44e8-119">[Netron](https://github.com/lutzroeder/netron) (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="b44e8-119">[Netron](https://github.com/lutzroeder/netron) (optional)</span></span>

## <a name="onnx-object-detection-sample-overview"></a><span data-ttu-id="b44e8-120">Panoramica dell'esempio di rilevamento degli oggetti ONNX</span><span class="sxs-lookup"><span data-stu-id="b44e8-120">ONNX object detection sample overview</span></span>

<span data-ttu-id="b44e8-121">Questo esempio crea un'applicazione console .NET Core che rileva gli oggetti all'interno di un'immagine usando un modello ONNX di Deep Learning già sottoposto a training.</span><span class="sxs-lookup"><span data-stu-id="b44e8-121">This sample creates a .NET core console application that detects objects within an image using a pre-trained deep learning ONNX model.</span></span> <span data-ttu-id="b44e8-122">Il codice per questo esempio è disponibile nel [repository dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx) in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b44e8-122">The code for this sample can be found on the [dotnet/machinelearning-samples repository](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx) on GitHub.</span></span>

## <a name="what-is-object-detection"></a><span data-ttu-id="b44e8-123">Che cos'è il rilevamento degli oggetti?</span><span class="sxs-lookup"><span data-stu-id="b44e8-123">What is object detection?</span></span>

<span data-ttu-id="b44e8-124">Il rilevamento degli oggetti è una questione correlata alla visione artificiale.</span><span class="sxs-lookup"><span data-stu-id="b44e8-124">Object detection is a computer vision problem.</span></span> <span data-ttu-id="b44e8-125">Sebbene sia un concetto strettamente correlato alla classificazione delle immagini, il rilevamento degli oggetti esegue l'operazione di classificazione delle immagini su scala più granulare.</span><span class="sxs-lookup"><span data-stu-id="b44e8-125">While closely related to image classification, object detection performs image classification at a more granular scale.</span></span> <span data-ttu-id="b44e8-126">Il rilevamento degli oggetti individua _e_ classifica le entità all'interno delle immagini.</span><span class="sxs-lookup"><span data-stu-id="b44e8-126">Object detection both locates _and_ categorizes entities within images.</span></span> <span data-ttu-id="b44e8-127">Usare il rilevamento degli oggetti quando le immagini contengono più oggetti di tipi diversi.</span><span class="sxs-lookup"><span data-stu-id="b44e8-127">Use object detection when images contain multiple objects of different types.</span></span>

![Screenshot che mostrano la classificazione delle immagini e la classificazione degli oggetti.](./media/object-detection-onnx/img-classification-obj-detection.png)

<span data-ttu-id="b44e8-129">Ecco alcuni casi d'uso per il rilevamento degli oggetti:</span><span class="sxs-lookup"><span data-stu-id="b44e8-129">Some use cases for object detection include:</span></span>

- <span data-ttu-id="b44e8-130">Auto senza guidatore</span><span class="sxs-lookup"><span data-stu-id="b44e8-130">Self-Driving Cars</span></span>
- <span data-ttu-id="b44e8-131">Robotica</span><span class="sxs-lookup"><span data-stu-id="b44e8-131">Robotics</span></span>
- <span data-ttu-id="b44e8-132">Rilevamento viso</span><span class="sxs-lookup"><span data-stu-id="b44e8-132">Face Detection</span></span>
- <span data-ttu-id="b44e8-133">Sicurezza nell'ambiente di lavoro</span><span class="sxs-lookup"><span data-stu-id="b44e8-133">Workplace Safety</span></span>
- <span data-ttu-id="b44e8-134">Conteggio di oggetti</span><span class="sxs-lookup"><span data-stu-id="b44e8-134">Object Counting</span></span>
- <span data-ttu-id="b44e8-135">Riconoscimento di attività</span><span class="sxs-lookup"><span data-stu-id="b44e8-135">Activity Recognition</span></span>

## <a name="select-a-deep-learning-model"></a><span data-ttu-id="b44e8-136">Selezionare un modello di Deep Learning</span><span class="sxs-lookup"><span data-stu-id="b44e8-136">Select a deep learning model</span></span>

<span data-ttu-id="b44e8-137">Il Deep Learning è un subset del Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="b44e8-137">Deep learning is a subset of machine learning.</span></span> <span data-ttu-id="b44e8-138">Per eseguire il training di modelli di Deep Learning, sono necessarie grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="b44e8-138">To train deep learning models, large quantities of data are required.</span></span> <span data-ttu-id="b44e8-139">I modelli nei dati sono rappresentati da una serie di livelli.</span><span class="sxs-lookup"><span data-stu-id="b44e8-139">Patterns in the data are represented by a series of layers.</span></span> <span data-ttu-id="b44e8-140">Le relazioni nei dati sono codificate come connessioni tra i livelli contenenti pesi.</span><span class="sxs-lookup"><span data-stu-id="b44e8-140">The relationships in the data are encoded as connections between the layers containing weights.</span></span> <span data-ttu-id="b44e8-141">Maggiore è il peso, più forte è la relazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-141">The higher the weight, the stronger the relationship.</span></span> <span data-ttu-id="b44e8-142">Collettivamente, questa serie di livelli e connessioni è nota come rete neurale artificiale.</span><span class="sxs-lookup"><span data-stu-id="b44e8-142">Collectively, this series of layers and connections are known as artificial neural networks.</span></span> <span data-ttu-id="b44e8-143">Maggiore è il numero di livelli in una rete, più "profonda" è la rete, che diventa una rete neurale profonda.</span><span class="sxs-lookup"><span data-stu-id="b44e8-143">The more layers in a network, the "deeper" it is, making it a deep neural network.</span></span>

<span data-ttu-id="b44e8-144">Ci sono diversi tipi di reti neurali, tra cui i più comuni sono percettrone multistrato (MLP, Multi-Layered Perceptron), rete neurale convoluzionale (CNN, Convolutional Neural Network) e rete neurale ricorrente (RNN, Recurrent Neural Network).</span><span class="sxs-lookup"><span data-stu-id="b44e8-144">There are different types of neural networks, the most common being Multi-Layered Perceptron (MLP), Convolutional Neural Network (CNN) and Recurrent Neural Network (RNN).</span></span> <span data-ttu-id="b44e8-145">Il tipo più semplice è MLP, che esegue il mapping di un set di input a un set di output.</span><span class="sxs-lookup"><span data-stu-id="b44e8-145">The most basic is the MLP, which maps a set of inputs to a set of outputs.</span></span> <span data-ttu-id="b44e8-146">Questa rete neurale è efficace quando i dati non hanno una componente spaziale o temporale.</span><span class="sxs-lookup"><span data-stu-id="b44e8-146">This neural network is good when the data does not have a spatial or time component.</span></span> <span data-ttu-id="b44e8-147">La rete CNN usa i livelli convoluzionali per elaborare le informazioni spaziali contenute nei dati.</span><span class="sxs-lookup"><span data-stu-id="b44e8-147">The CNN makes use of convolutional layers to process spatial information contained in the data.</span></span> <span data-ttu-id="b44e8-148">Un buon caso d'uso per le reti CNN è l'elaborazione di immagini per rilevare la presenza di una caratteristica in un'area di un'immagine (ad esempio, è presente un naso al centro di un'immagine?).</span><span class="sxs-lookup"><span data-stu-id="b44e8-148">A good use case for CNNs is image processing to detect the presence of a feature in a region of an image (for example, is there a nose in the center of an image?).</span></span> <span data-ttu-id="b44e8-149">Infine, le reti RNN consentono di usare come input la persistenza dello stato o della memoria.</span><span class="sxs-lookup"><span data-stu-id="b44e8-149">Finally, RNNs allow for the persistence of state or memory to be used as input.</span></span> <span data-ttu-id="b44e8-150">Le reti RNN vengono usate per l'analisi delle serie temporali, in cui l'ordinamento sequenziale e il contesto degli eventi sono importanti.</span><span class="sxs-lookup"><span data-stu-id="b44e8-150">RNNs are used for time-series analysis, where the sequential ordering and context of events is important.</span></span>

### <a name="understand-the-model"></a><span data-ttu-id="b44e8-151">Acquisire familiarità con il modello</span><span class="sxs-lookup"><span data-stu-id="b44e8-151">Understand the model</span></span>

<span data-ttu-id="b44e8-152">Il rilevamento di oggetti è un'attività di elaborazione delle immagini.</span><span class="sxs-lookup"><span data-stu-id="b44e8-152">Object detection is an image-processing task.</span></span> <span data-ttu-id="b44e8-153">Per questo motivo, i modelli di Deep Learning sottoposti a training per risolvere questo problema sono prevalentemente di tipo CNN.</span><span class="sxs-lookup"><span data-stu-id="b44e8-153">Therefore, most deep learning models trained to solve this problem are CNNs.</span></span> <span data-ttu-id="b44e8-154">Il modello utilizzato in questa esercitazione è il modello Tiny YOLOv2, una versione più compatta del modello YOLOv2 descritto nel documento: ["YOLO9000: Better, Faster, Stronger" di Redmon e Fadhari](https://arxiv.org/pdf/1612.08242.pdf).</span><span class="sxs-lookup"><span data-stu-id="b44e8-154">The model used in this tutorial is the Tiny YOLOv2 model, a more compact version of the YOLOv2 model described in the paper: ["YOLO9000: Better, Faster, Stronger" by Redmon and Fadhari](https://arxiv.org/pdf/1612.08242.pdf).</span></span> <span data-ttu-id="b44e8-155">Il training di Tiny YOLOv2 viene eseguito sul set di dati Pascal VOC ed è costituito da 15 livelli in grado di eseguire stime per 20 diverse classi di oggetti.</span><span class="sxs-lookup"><span data-stu-id="b44e8-155">Tiny YOLOv2 is trained on the Pascal VOC dataset and is made up of 15 layers that can predict 20 different classes of objects.</span></span> <span data-ttu-id="b44e8-156">Poiché il modello Tiny YOLOv2 è una versione ridotta del modello YOLOv2 originale, rappresenta un compromesso tra velocità e accuratezza.</span><span class="sxs-lookup"><span data-stu-id="b44e8-156">Because Tiny YOLOv2 is a condensed version of the original YOLOv2 model, a tradeoff is made between speed and accuracy.</span></span> <span data-ttu-id="b44e8-157">I diversi livelli che compongono il modello possono essere visualizzati usando strumenti come Netron.</span><span class="sxs-lookup"><span data-stu-id="b44e8-157">The different layers that make up the model can be visualized using tools like Netron.</span></span> <span data-ttu-id="b44e8-158">L'esame del modello restituirebbe un mapping delle connessioni tra tutti i livelli che compongono la rete neurale, in cui ogni livello contiene il nome del livello insieme alle dimensioni del rispettivo input/output.</span><span class="sxs-lookup"><span data-stu-id="b44e8-158">Inspecting the model would yield a mapping of the connections between all the layers that make up the neural network, where each layer would contain the name of the layer along with the dimensions of the respective input / output.</span></span> <span data-ttu-id="b44e8-159">Le strutture di dati usate per descrivere gli input e gli output del modello sono note come tensori.</span><span class="sxs-lookup"><span data-stu-id="b44e8-159">The data structures used to describe the inputs and outputs of the model are known as tensors.</span></span> <span data-ttu-id="b44e8-160">I tensori possono essere considerati contenitori che archiviano i dati in N dimensioni.</span><span class="sxs-lookup"><span data-stu-id="b44e8-160">Tensors can be thought of as containers that store data in N-dimensions.</span></span> <span data-ttu-id="b44e8-161">Nel caso di Tiny YOLOv2, il nome del livello di input è `image` e prevede un tensore con dimensioni `3 x 416 x 416`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-161">In the case of Tiny YOLOv2, the name of the input layer is `image` and it expects a tensor of dimensions `3 x 416 x 416`.</span></span> <span data-ttu-id="b44e8-162">Il nome del livello di output è `grid` e genera un tensore di output con dimensioni `125 x 13 x 13`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-162">The name of the output layer is `grid` and generates an output tensor of dimensions `125 x 13 x 13`.</span></span>

![Livello di input diviso in livelli nascosti, quindi livello di output](./media/object-detection-onnx/netron-model-map-layers.png)

<span data-ttu-id="b44e8-164">Il modello YOLO accetta un'immagine `3(RGB) x 416px x 416px`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-164">The YOLO model takes an image `3(RGB) x 416px x 416px`.</span></span> <span data-ttu-id="b44e8-165">Il modello accetta questo input e lo passa attraverso i diversi livelli per produrre un output.</span><span class="sxs-lookup"><span data-stu-id="b44e8-165">The model takes this input and passes it through the different layers to produce an output.</span></span> <span data-ttu-id="b44e8-166">L'output divide l'immagine di input in una griglia `13 x 13`, con ogni cella della griglia costituita da `125` valori.</span><span class="sxs-lookup"><span data-stu-id="b44e8-166">The output divides the input image into a `13 x 13` grid, with each cell in the grid consisting of `125` values.</span></span>

### <a name="what-is-an-onnx-model"></a><span data-ttu-id="b44e8-167">Che cos'è un modello ONNX?</span><span class="sxs-lookup"><span data-stu-id="b44e8-167">What is an ONNX model?</span></span>

<span data-ttu-id="b44e8-168">Open Neural Network Exchange (ONNX) è un formato open source per i modelli di intelligenza artificiale.</span><span class="sxs-lookup"><span data-stu-id="b44e8-168">The Open Neural Network Exchange (ONNX) is an open source format for AI models.</span></span> <span data-ttu-id="b44e8-169">ONNX supporta l'interoperabilità tra framework.</span><span class="sxs-lookup"><span data-stu-id="b44e8-169">ONNX supports interoperability between frameworks.</span></span> <span data-ttu-id="b44e8-170">Ciò significa che è possibile eseguire il training di un modello in uno dei numerosi framework di apprendimento automatico diffusi, ad esempio PyTorch, eseguire la conversione in formato ONNX e utilizzare il modello ONNX in un framework diverso, come ML.NET.</span><span class="sxs-lookup"><span data-stu-id="b44e8-170">This means you can train a model in one of the many popular machine learning frameworks like PyTorch, convert it into ONNX format and consume the ONNX model in a different framework like ML.NET.</span></span> <span data-ttu-id="b44e8-171">Per altre informazioni, vedere il [sito Web ONNX](https://onnx.ai/).</span><span class="sxs-lookup"><span data-stu-id="b44e8-171">To learn more, visit the [ONNX website](https://onnx.ai/).</span></span>

![Diagramma dei formati supportati da ONNX in uso.](./media/object-detection-onnx/onnx-supported-formats.png)

<span data-ttu-id="b44e8-173">Il modello Tiny YOLOv2 già sottoposto a training è archiviato in formato ONNX, una rappresentazione serializzata dei livelli e dei modelli appresi di tali livelli.</span><span class="sxs-lookup"><span data-stu-id="b44e8-173">The pre-trained Tiny YOLOv2 model is stored in ONNX format, a serialized representation of the layers and learned patterns of those layers.</span></span> <span data-ttu-id="b44e8-174">In ML.NET, l'interoperabilità con ONNX viene ottenuta con i [`ImageAnalytics`](xref:Microsoft.ML.Transforms.Image) pacchetti e [`OnnxTransformer`](xref:Microsoft.ML.Transforms.Onnx.OnnxTransformer) NuGet.</span><span class="sxs-lookup"><span data-stu-id="b44e8-174">In ML.NET, interoperability with ONNX is achieved with the [`ImageAnalytics`](xref:Microsoft.ML.Transforms.Image) and [`OnnxTransformer`](xref:Microsoft.ML.Transforms.Onnx.OnnxTransformer) NuGet packages.</span></span> <span data-ttu-id="b44e8-175">Il [`ImageAnalytics`](xref:Microsoft.ML.Transforms.Image) pacchetto contiene una serie di trasformazioni che accettano un'immagine e la codificano in valori numerici che possono essere usati come input in una pipeline di stima o di training.</span><span class="sxs-lookup"><span data-stu-id="b44e8-175">The [`ImageAnalytics`](xref:Microsoft.ML.Transforms.Image) package contains a series of transforms that take an image and encode it into numerical values that can be used as input into a prediction or training pipeline.</span></span> <span data-ttu-id="b44e8-176">Il [`OnnxTransformer`](xref:Microsoft.ML.Transforms.Onnx.OnnxTransformer) pacchetto sfrutta il runtime ONNX per caricare un modello ONNX e usarlo per eseguire stime in base all'input fornito.</span><span class="sxs-lookup"><span data-stu-id="b44e8-176">The [`OnnxTransformer`](xref:Microsoft.ML.Transforms.Onnx.OnnxTransformer) package leverages the ONNX Runtime to load an ONNX model and use it to make predictions based on input provided.</span></span>

![Flusso di dati del file ONNX nel runtime ONNX.](./media/object-detection-onnx/onnx-ml-net-integration.png)

## <a name="set-up-the-net-core-project"></a><span data-ttu-id="b44e8-178">Configurare il progetto .NET Core</span><span class="sxs-lookup"><span data-stu-id="b44e8-178">Set up the .NET Core project</span></span>

<span data-ttu-id="b44e8-179">Ora che sono state apprese le nozioni generali su ONNX e sul funzionamento di Tiny YOLOv2, è possibile creare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-179">Now that you have a general understanding of what ONNX is and how Tiny YOLOv2 works, it's time to build the application.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="b44e8-180">Creare un'applicazione console</span><span class="sxs-lookup"><span data-stu-id="b44e8-180">Create a console application</span></span>

1. <span data-ttu-id="b44e8-181">Creare un'**applicazione console .NET Core** denominata "ObjectDetection".</span><span class="sxs-lookup"><span data-stu-id="b44e8-181">Create a **.NET Core Console Application** called "ObjectDetection".</span></span>

1. <span data-ttu-id="b44e8-182">Installare il **pacchetto NuGet Microsoft.ML**:</span><span class="sxs-lookup"><span data-stu-id="b44e8-182">Install the **Microsoft.ML NuGet Package**:</span></span>

    - <span data-ttu-id="b44e8-183">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e selezionare **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-183">In Solution Explorer, right-click on your project and select **Manage NuGet Packages**.</span></span>
    - <span data-ttu-id="b44e8-184">Scegliere "nuget.org" come origine del pacchetto, selezionare la scheda Sfoglia e cercare **Microsoft.ML**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-184">Choose "nuget.org" as the Package source, select the Browse tab, search for **Microsoft.ML**.</span></span>
    - <span data-ttu-id="b44e8-185">Selezionare il pulsante **Installa**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-185">Select the **Install** button.</span></span>
    - <span data-ttu-id="b44e8-186">Selezionare il pulsante **OK** nella finestra di dialogo **Anteprima modifiche** e quindi selezionare il pulsante **Accetto** nella finestra di dialogo **Accettazione della licenza** se si accettano le condizioni di licenza per i pacchetti elencati.</span><span class="sxs-lookup"><span data-stu-id="b44e8-186">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the **License Acceptance** dialog if you agree with the license terms for the packages listed.</span></span>
    - <span data-ttu-id="b44e8-187">Ripetere questi passaggi per **Microsoft.ML.ImageAnalytics** e **Microsoft.ML.OnnxTransformer**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-187">Repeat these steps for **Microsoft.ML.ImageAnalytics** and **Microsoft.ML.OnnxTransformer**.</span></span>

### <a name="prepare-your-data-and-pre-trained-model"></a><span data-ttu-id="b44e8-188">Preparare i dati e il modello già sottoposto a training</span><span class="sxs-lookup"><span data-stu-id="b44e8-188">Prepare your data and pre-trained model</span></span>

1. <span data-ttu-id="b44e8-189">Scaricare il [file ZIP della directory assets del progetto](https://github.com/dotnet/machinelearning-samples/raw/master/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/assets.zip) e decomprimerlo.</span><span class="sxs-lookup"><span data-stu-id="b44e8-189">Download [The project assets directory zip file](https://github.com/dotnet/machinelearning-samples/raw/master/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/assets.zip) and unzip.</span></span>

1. <span data-ttu-id="b44e8-190">Copiare la directory `assets` nella directory del progetto *ObjectDetection*.</span><span class="sxs-lookup"><span data-stu-id="b44e8-190">Copy the `assets` directory into your *ObjectDetection* project directory.</span></span> <span data-ttu-id="b44e8-191">Questa directory e le relative sottodirectory contengono i file di immagine (ad eccezione del modello Tiny YOLOv2, che verrà scaricato e aggiunto nel passaggio successivo) richiesti per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-191">This directory and its subdirectories contain the image files (except for the Tiny YOLOv2 model, which you'll download and add in the next step) needed for this tutorial.</span></span>

1. <span data-ttu-id="b44e8-192">Scaricare il [modello Tiny YOLOv2](https://onnxzoo.blob.core.windows.net/models/opset_8/tiny_yolov2/tiny_yolov2.tar.gz) da [ONNX Model Zoo](https://github.com/onnx/models/tree/master/vision/object_detection_segmentation/tiny_yolov2) e decomprimerlo.</span><span class="sxs-lookup"><span data-stu-id="b44e8-192">Download the [Tiny YOLOv2 model](https://onnxzoo.blob.core.windows.net/models/opset_8/tiny_yolov2/tiny_yolov2.tar.gz) from the [ONNX Model Zoo](https://github.com/onnx/models/tree/master/vision/object_detection_segmentation/tiny_yolov2), and unzip.</span></span>

    <span data-ttu-id="b44e8-193">Aprire il prompt dei comandi e immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b44e8-193">Open the command prompt and enter the following command:</span></span>

    ```shell
    tar -xvzf tiny_yolov2.tar.gz
    ```

1. <span data-ttu-id="b44e8-194">Copiare il file `model.onnx` estratto dalla directory appena decompressa nella directory `assets\Model` del progetto*ObjectDetection* e rinominarlo in `TinyYolo2_model.onnx`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-194">Copy the extracted `model.onnx` file from the directory just unzipped into your *ObjectDetection* project `assets\Model` directory and rename it to `TinyYolo2_model.onnx`.</span></span> <span data-ttu-id="b44e8-195">Questa directory contiene il modello necessario per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-195">This directory contains the model needed for this tutorial.</span></span>

1. <span data-ttu-id="b44e8-196">In Esplora soluzioni fare clic con il pulsante destro del mouse su ognuno dei file nella directory assets e nelle relative sottodirectory e selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-196">In Solution Explorer, right-click each of the files in the asset directory and subdirectories and select **Properties**.</span></span> <span data-ttu-id="b44e8-197">In **Avanzate**, modificare il valore di **Copia nella directory** di output in Copia se **più recente**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-197">Under **Advanced**, change the value of **Copy to Output Directory** to **Copy if newer**.</span></span>

### <a name="create-classes-and-define-paths"></a><span data-ttu-id="b44e8-198">Creare le classi e definire i percorsi</span><span class="sxs-lookup"><span data-stu-id="b44e8-198">Create classes and define paths</span></span>

<span data-ttu-id="b44e8-199">Aprire il file *Program.cs* e aggiungere le istruzioni `using` aggiuntive seguenti all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="b44e8-199">Open the *Program.cs* file and add the following additional `using` statements to the top of the file:</span></span>

[!code-csharp [ProgramUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L1-L7)]

<span data-ttu-id="b44e8-200">Definire quindi i percorsi dei diversi asset.</span><span class="sxs-lookup"><span data-stu-id="b44e8-200">Next, define the paths of the various assets.</span></span>

1. <span data-ttu-id="b44e8-201">Prima di tutto, aggiungere il metodo `GetAbsolutePath` seguente al metodo `Main` nella classe `Program`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-201">First, add the `GetAbsolutePath` method below the `Main` method in the `Program` class.</span></span>

    [!code-csharp [GetAbsolutePath](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L66-L74)]

1. <span data-ttu-id="b44e8-202">Quindi, all'interno del metodo `Main` creare i campi per archiviare il percorso degli asset.</span><span class="sxs-lookup"><span data-stu-id="b44e8-202">Then, inside the `Main` method, create fields to store the location of your assets.</span></span>

    [!code-csharp [AssetDefinition](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L17-L21)]

<span data-ttu-id="b44e8-203">Aggiungere una nuova directory al progetto per archiviare i dati di input e le classi di stima.</span><span class="sxs-lookup"><span data-stu-id="b44e8-203">Add a new directory to your project to store your input data and prediction classes.</span></span>

<span data-ttu-id="b44e8-204">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Aggiungi** > **Nuova cartella**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-204">In **Solution Explorer**, right-click the project, and then select **Add** > **New Folder**.</span></span> <span data-ttu-id="b44e8-205">Quando la nuova cartella viene visualizzata in Esplora soluzioni, assegnarle il nome "DataStructures".</span><span class="sxs-lookup"><span data-stu-id="b44e8-205">When the new folder appears in the Solution Explorer, name it "DataStructures".</span></span>

<span data-ttu-id="b44e8-206">Creare la classe di dati di input nella directory *DataStructures* appena creata.</span><span class="sxs-lookup"><span data-stu-id="b44e8-206">Create your input data class in the newly created *DataStructures* directory.</span></span>

1. <span data-ttu-id="b44e8-207">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla directory *DataStructures* e quindi scegliere **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-207">In **Solution Explorer**, right-click the *DataStructures* directory, and then select **Add** > **New Item**.</span></span>
1. <span data-ttu-id="b44e8-208">Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Classe** e modificare il campo **Nome** in *ImageNetData.cs*.</span><span class="sxs-lookup"><span data-stu-id="b44e8-208">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *ImageNetData.cs*.</span></span> <span data-ttu-id="b44e8-209">Selezionare quindi il pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-209">Then, select the **Add** button.</span></span>

    <span data-ttu-id="b44e8-210">Il file *ImageNetData.cs* viene aperto nell'editor del codice.</span><span class="sxs-lookup"><span data-stu-id="b44e8-210">The *ImageNetData.cs* file opens in the code editor.</span></span> <span data-ttu-id="b44e8-211">Aggiungere l'istruzione `using` seguente all'inizio di *ImageNetData.cs*:</span><span class="sxs-lookup"><span data-stu-id="b44e8-211">Add the following `using` statement to the top of *ImageNetData.cs*:</span></span>

    [!code-csharp [ImageNetDataUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/DataStructures/ImageNetData.cs#L1-L4)]

    <span data-ttu-id="b44e8-212">Rimuovere la definizione di classe esistente e aggiungere il codice seguente per la classe `ImageNetData` al file *ImageNetData.cs*:</span><span class="sxs-lookup"><span data-stu-id="b44e8-212">Remove the existing class definition and add the following code for the `ImageNetData` class to the *ImageNetData.cs* file:</span></span>

    [!code-csharp [ImageNetDataClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/DataStructures/ImageNetData.cs#L8-L23)]

    <span data-ttu-id="b44e8-213">`ImageNetData` è la classe dei dati di immagine di input e ha i campi <xref:System.String> seguenti:</span><span class="sxs-lookup"><span data-stu-id="b44e8-213">`ImageNetData` is the input image data class and has the following <xref:System.String> fields:</span></span>

    - <span data-ttu-id="b44e8-214">`ImagePath` contiene il percorso in cui è archiviata l'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-214">`ImagePath` contains the path where the image is stored.</span></span>
    - <span data-ttu-id="b44e8-215">`Label` contiene il nome del file.</span><span class="sxs-lookup"><span data-stu-id="b44e8-215">`Label` contains the name of the file.</span></span>

    <span data-ttu-id="b44e8-216">Inoltre, `ImageNetData` contiene un `ReadFromFile` metodo che carica più `imageFolder` file di immagine archiviati `ImageNetData` nel percorso specificato e li restituisce come una raccolta di oggetti.</span><span class="sxs-lookup"><span data-stu-id="b44e8-216">Additionally, `ImageNetData` contains a method `ReadFromFile` that loads multiple image files stored in the `imageFolder` path specified and returns them as a collection of `ImageNetData` objects.</span></span>

<span data-ttu-id="b44e8-217">Creare la classe di stima nella directory *DataStructures*.</span><span class="sxs-lookup"><span data-stu-id="b44e8-217">Create your prediction class in the *DataStructures* directory.</span></span>

1. <span data-ttu-id="b44e8-218">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla directory *DataStructures* e quindi scegliere **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-218">In **Solution Explorer**, right-click the *DataStructures* directory, and then select **Add** > **New Item**.</span></span>
1. <span data-ttu-id="b44e8-219">Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Classe** e modificare il campo **Nome** in *ImageNetPrediction.cs*.</span><span class="sxs-lookup"><span data-stu-id="b44e8-219">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *ImageNetPrediction.cs*.</span></span> <span data-ttu-id="b44e8-220">Selezionare quindi il pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-220">Then, select the **Add** button.</span></span>

    <span data-ttu-id="b44e8-221">Il file *ImageNetPrediction.cs* viene aperto nell'editor del codice.</span><span class="sxs-lookup"><span data-stu-id="b44e8-221">The *ImageNetPrediction.cs* file opens in the code editor.</span></span> <span data-ttu-id="b44e8-222">Aggiungere l'istruzione `using` seguente all'inizio di *ImageNetPrediction.cs*:</span><span class="sxs-lookup"><span data-stu-id="b44e8-222">Add the following `using` statement to the top of *ImageNetPrediction.cs*:</span></span>

    [!code-csharp [ImageNetPredictionUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/DataStructures/ImageNetPrediction.cs#L1)]

    <span data-ttu-id="b44e8-223">Rimuovere la definizione di classe esistente e aggiungere il codice seguente per la classe `ImageNetPrediction` al file *ImageNetPrediction.cs*:</span><span class="sxs-lookup"><span data-stu-id="b44e8-223">Remove the existing class definition and add the following code for the `ImageNetPrediction` class to the *ImageNetPrediction.cs* file:</span></span>

    [!code-csharp [ImageNetPredictionClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/DataStructures/ImageNetPrediction.cs#L5-L9)]

    <span data-ttu-id="b44e8-224">`ImageNetPrediction` è la classe di dati di stima e ha il campo `float[]` seguente:</span><span class="sxs-lookup"><span data-stu-id="b44e8-224">`ImageNetPrediction` is the prediction data class and has the following `float[]` field:</span></span>

    - <span data-ttu-id="b44e8-225">`PredictedLabel`contiene le dimensioni, il punteggio di oggettività e le probabilità di classe per ciascuno dei rettangoli di selezione rilevati in un'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-225">`PredictedLabel` contains the dimensions, objectness score, and class probabilities for each of the bounding boxes detected in an image.</span></span>

### <a name="initialize-variables-in-main"></a><span data-ttu-id="b44e8-226">Inizializzare le variabili in Main</span><span class="sxs-lookup"><span data-stu-id="b44e8-226">Initialize variables in Main</span></span>

<span data-ttu-id="b44e8-227">La [classe MLContext](xref:Microsoft.ML.MLContext) è un punto di partenza per tutte le operazioni ML.NET e l'inizializzazione di `mlContext` crea un nuovo ambiente ML.NET che può essere condiviso tra gli oggetti del flusso di lavoro della creazione del modello.</span><span class="sxs-lookup"><span data-stu-id="b44e8-227">The [MLContext class](xref:Microsoft.ML.MLContext) is a starting point for all ML.NET operations, and initializing `mlContext` creates a new ML.NET environment that can be shared across the model creation workflow objects.</span></span> <span data-ttu-id="b44e8-228">Dal punto di vista concettuale è simile a `DBContext` in Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="b44e8-228">It's similar, conceptually, to `DBContext` in Entity Framework.</span></span>

<span data-ttu-id="b44e8-229">Inizializzare la variabile `mlContext` con una nuova istanza di `MLContext` aggiungendo la riga seguente al metodo `Main` di *Program.cs* sotto il campo `outputFolder`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-229">Initialize the `mlContext` variable with a new instance of `MLContext` by adding the following line to the `Main` method of *Program.cs* below the `outputFolder` field.</span></span>

[!code-csharp [InitMLContext](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L24)]

## <a name="create-a-parser-to-post-process-model-outputs"></a><span data-ttu-id="b44e8-230">Creare un parser per la post-elaborazione degli output del modello</span><span class="sxs-lookup"><span data-stu-id="b44e8-230">Create a parser to post-process model outputs</span></span>

<span data-ttu-id="b44e8-231">Il modello segmenta un'immagine in una griglia `13 x 13`, in cui ogni cella è `32px x 32px`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-231">The model segments an image into a `13 x 13` grid, where each grid cell is `32px x 32px`.</span></span> <span data-ttu-id="b44e8-232">Ogni cella della griglia contiene 5 rettangoli di selezione di oggetti potenziali.</span><span class="sxs-lookup"><span data-stu-id="b44e8-232">Each grid cell contains 5 potential object bounding boxes.</span></span> <span data-ttu-id="b44e8-233">Un rettangolo di selezione contiene 25 elementi:</span><span class="sxs-lookup"><span data-stu-id="b44e8-233">A bounding box has  25 elements:</span></span>

![Esempio di griglia a sinistra e Esempio di riquadro di delimitazione a destra](./media/object-detection-onnx/model-output-description.png)

- <span data-ttu-id="b44e8-235">`x` la posizione x del centro del rettangolo di selezione rispetto alla cella della griglia a cui è associato.</span><span class="sxs-lookup"><span data-stu-id="b44e8-235">`x` the x position of the bounding box center relative to the grid cell it's associated with.</span></span>
- <span data-ttu-id="b44e8-236">`y` la posizione y del centro del rettangolo di selezione rispetto alla cella della griglia a cui è associato.</span><span class="sxs-lookup"><span data-stu-id="b44e8-236">`y` the y position of the bounding box center relative to the grid cell it's associated with.</span></span>
- <span data-ttu-id="b44e8-237">`w` la larghezza del rettangolo di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-237">`w` the width of the bounding box.</span></span>
- <span data-ttu-id="b44e8-238">`h` l'altezza del rettangolo di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-238">`h` the height of the bounding box.</span></span>
- <span data-ttu-id="b44e8-239">`o` il valore di confidenza che un oggetto esiste nel rettangolo di selezione, noto anche come punteggio di riconoscimento degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="b44e8-239">`o` the confidence value that an object exists within the bounding box, also known as objectness score.</span></span>
- <span data-ttu-id="b44e8-240">`p1-p20` le probabilità delle classi per ognuna delle 20 classi stimate dal modello.</span><span class="sxs-lookup"><span data-stu-id="b44e8-240">`p1-p20` class probabilities for each of the 20 classes predicted by the model.</span></span>

<span data-ttu-id="b44e8-241">In totale, i 25 elementi che descrivono ognuno dei 5 rettangoli di selezione costituiscono i 125 elementi contenuti in ogni cella della griglia.</span><span class="sxs-lookup"><span data-stu-id="b44e8-241">In total, the 25 elements describing each of the 5 bounding boxes make up the 125 elements contained in each grid cell.</span></span>

<span data-ttu-id="b44e8-242">L'output generato dal modello ONNX già sottoposto a training è una matrice mobile di lunghezza `21125` che rappresenta gli elementi di un tensore con dimensioni `125 x 13 x 13`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-242">The output generated by the pre-trained ONNX model is a float array of length `21125`, representing the elements of a tensor with dimensions `125 x 13 x 13`.</span></span> <span data-ttu-id="b44e8-243">Per trasformare le stime generate dal modello in un tensore, è necessario eseguire alcune operazioni di post-elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-243">In order to transform the predictions generated by the model into a tensor, some post-processing work is required.</span></span> <span data-ttu-id="b44e8-244">A tale scopo, creare un set di classi per l'analisi dell'output.</span><span class="sxs-lookup"><span data-stu-id="b44e8-244">To do so, create a set of classes to help parse the output.</span></span>

<span data-ttu-id="b44e8-245">Aggiungere una nuova directory al progetto per organizzare il set di classi parser.</span><span class="sxs-lookup"><span data-stu-id="b44e8-245">Add a new directory to your project to organize the set of parser classes.</span></span>

1. <span data-ttu-id="b44e8-246">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Aggiungi** > **Nuova cartella**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-246">In **Solution Explorer**, right-click the project, and then select **Add** > **New Folder**.</span></span> <span data-ttu-id="b44e8-247">Quando la nuova cartella viene visualizzata in Esplora soluzioni, assegnarle il nome "YoloParser".</span><span class="sxs-lookup"><span data-stu-id="b44e8-247">When the new folder appears in the Solution Explorer, name it "YoloParser".</span></span>

### <a name="create-bounding-boxes-and-dimensions"></a><span data-ttu-id="b44e8-248">Creare rettangoli di selezione e dimensioni</span><span class="sxs-lookup"><span data-stu-id="b44e8-248">Create bounding boxes and dimensions</span></span>

<span data-ttu-id="b44e8-249">I dati restituiti dal modello contengono le coordinate e le dimensioni dei rettangoli di selezione degli oggetti all'interno dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-249">The data output by the model contains coordinates and dimensions of the bounding boxes of objects within the image.</span></span> <span data-ttu-id="b44e8-250">Creare una classe di base per le dimensioni.</span><span class="sxs-lookup"><span data-stu-id="b44e8-250">Create a base class for dimensions.</span></span>

1. <span data-ttu-id="b44e8-251">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla directory *YoloParser* e quindi scegliere **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-251">In **Solution Explorer**, right-click the *YoloParser* directory, and then select **Add** > **New Item**.</span></span>
1. <span data-ttu-id="b44e8-252">Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Classe** e modificare il campo **Nome** in *DimensionsBase.cs*.</span><span class="sxs-lookup"><span data-stu-id="b44e8-252">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *DimensionsBase.cs*.</span></span> <span data-ttu-id="b44e8-253">Selezionare quindi il pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-253">Then, select the **Add** button.</span></span>

    <span data-ttu-id="b44e8-254">Il file *DimensionsBase.cs* viene aperto nell'editor del codice.</span><span class="sxs-lookup"><span data-stu-id="b44e8-254">The *DimensionsBase.cs* file opens in the code editor.</span></span> <span data-ttu-id="b44e8-255">Rimuovere tutte le istruzioni `using` e la definizione di classe esistente.</span><span class="sxs-lookup"><span data-stu-id="b44e8-255">Remove all `using` statements and existing class definition.</span></span>

    <span data-ttu-id="b44e8-256">Aggiungere il codice seguente per la classe `DimensionsBase` al file *DimensionsBase.cs*:</span><span class="sxs-lookup"><span data-stu-id="b44e8-256">Add the following code for the `DimensionsBase` class to the *DimensionsBase.cs* file:</span></span>

    [!code-csharp [DimensionsBaseClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/DimensionsBase.cs#L3-L9)]

    <span data-ttu-id="b44e8-257">`DimensionsBase`ha le `float` seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="b44e8-257">`DimensionsBase` has the following `float` properties:</span></span>

    - <span data-ttu-id="b44e8-258">`X` contiene la posizione dell'oggetto lungo l'asse x.</span><span class="sxs-lookup"><span data-stu-id="b44e8-258">`X` contains the position of the object along the x-axis.</span></span>
    - <span data-ttu-id="b44e8-259">`Y` contiene la posizione dell'oggetto lungo l'asse y.</span><span class="sxs-lookup"><span data-stu-id="b44e8-259">`Y` contains the position of the object along the y-axis.</span></span>
    - <span data-ttu-id="b44e8-260">`Height` contiene l'altezza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="b44e8-260">`Height` contains the height of the object.</span></span>
    - <span data-ttu-id="b44e8-261">`Width` contiene la larghezza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="b44e8-261">`Width` contains the width of the object.</span></span>

<span data-ttu-id="b44e8-262">Creare quindi una classe per i rettangoli di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-262">Next, create a class for your bounding boxes.</span></span>

1. <span data-ttu-id="b44e8-263">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla directory *YoloParser* e quindi scegliere **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-263">In **Solution Explorer**, right-click the *YoloParser* directory, and then select **Add** > **New Item**.</span></span>
1. <span data-ttu-id="b44e8-264">Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Classe** e modificare il campo **Nome** in *YoloBoundingBox.cs*.</span><span class="sxs-lookup"><span data-stu-id="b44e8-264">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *YoloBoundingBox.cs*.</span></span> <span data-ttu-id="b44e8-265">Selezionare quindi il pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-265">Then, select the **Add** button.</span></span>

    <span data-ttu-id="b44e8-266">Il file *YoloBoundingBox.cs* viene aperto nell'editor del codice.</span><span class="sxs-lookup"><span data-stu-id="b44e8-266">The *YoloBoundingBox.cs* file opens in the code editor.</span></span> <span data-ttu-id="b44e8-267">Aggiungere l'istruzione `using` seguente all'inizio di *YoloBoundingBox.cs*:</span><span class="sxs-lookup"><span data-stu-id="b44e8-267">Add the following `using` statement to the top of *YoloBoundingBox.cs*:</span></span>

    [!code-csharp [YoloBoundingBoxUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloBoundingBox.cs#L1)]

    <span data-ttu-id="b44e8-268">Appena sopra la definizione di classe `BoundingBoxDimensions` esistente, aggiungere `DimensionsBase` una nuova definizione di classe denominata che eredita dalla classe per contenere le dimensioni del rispettivo riquadro di delimitazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-268">Just above the existing class definition, add a new class definition called `BoundingBoxDimensions` that inherits from the `DimensionsBase` class to contain the dimensions of the respective bounding box.</span></span>

    [!code-csharp [BoundingBoxDimClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloBoundingBox.cs#L5)]

    <span data-ttu-id="b44e8-269">Rimuovere la definizione di classe `YoloBoundingBox` esistente e aggiungere il codice seguente per la classe `YoloBoundingBox` al file *YoloBoundingBox.cs*:</span><span class="sxs-lookup"><span data-stu-id="b44e8-269">Remove the existing `YoloBoundingBox` class definition and add the following code for the `YoloBoundingBox` class to the *YoloBoundingBox.cs* file:</span></span>

    [!code-csharp [YoloBoundingBoxClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloBoundingBox.cs#L7-L21)]

    <span data-ttu-id="b44e8-270">`YoloBoundingBox`ha le seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="b44e8-270">`YoloBoundingBox` has the following properties:</span></span>

    - <span data-ttu-id="b44e8-271">`Dimensions` contiene le dimensioni del rettangolo di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-271">`Dimensions` contains dimensions of the bounding box.</span></span>
    - <span data-ttu-id="b44e8-272">`Label` contiene la classe dell'oggetto rilevato nel rettangolo di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-272">`Label` contains the class of object detected within the bounding box.</span></span>
    - <span data-ttu-id="b44e8-273">`Confidence` contiene la confidenza della classe.</span><span class="sxs-lookup"><span data-stu-id="b44e8-273">`Confidence` contains the confidence of the class.</span></span>
    - <span data-ttu-id="b44e8-274">`Rect` contiene la rappresentazione del rettangolo delle dimensioni del rettangolo di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-274">`Rect` contains the rectangle representation of the bounding box's dimensions.</span></span>
    - <span data-ttu-id="b44e8-275">`BoxColor` contiene il colore associato alla rispettiva classe usata per disegnare l'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-275">`BoxColor` contains the color associated with the respective class used to draw on the image.</span></span>

### <a name="create-the-parser"></a><span data-ttu-id="b44e8-276">Creare il parser</span><span class="sxs-lookup"><span data-stu-id="b44e8-276">Create the parser</span></span>

<span data-ttu-id="b44e8-277">Dopo aver creato le classi per le dimensioni e i rettangoli di selezione, è possibile creare il parser.</span><span class="sxs-lookup"><span data-stu-id="b44e8-277">Now that the classes for dimensions and bounding boxes are created, it's time to create the parser.</span></span>

1. <span data-ttu-id="b44e8-278">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla directory *YoloParser* e quindi scegliere **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-278">In **Solution Explorer**, right-click the *YoloParser* directory, and then select **Add** > **New Item**.</span></span>
1. <span data-ttu-id="b44e8-279">Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Classe** e modificare il campo **Nome** in *YoloOutputParser.cs*.</span><span class="sxs-lookup"><span data-stu-id="b44e8-279">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *YoloOutputParser.cs*.</span></span> <span data-ttu-id="b44e8-280">Selezionare quindi il pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-280">Then, select the **Add** button.</span></span>

    <span data-ttu-id="b44e8-281">Il file *YoloOutputParser.cs* viene aperto nell'editor del codice.</span><span class="sxs-lookup"><span data-stu-id="b44e8-281">The *YoloOutputParser.cs* file opens in the code editor.</span></span> <span data-ttu-id="b44e8-282">Aggiungere l'istruzione `using` seguente all'inizio di *YoloOutputParser.cs*:</span><span class="sxs-lookup"><span data-stu-id="b44e8-282">Add the following `using` statement to the top of *YoloOutputParser.cs*:</span></span>

    [!code-csharp [YoloParserUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L1-L4)]

    <span data-ttu-id="b44e8-283">All'interno della definizione di classe `YoloOutputParser` esistente aggiungere una classe annidata che contiene le dimensioni di ciascuna cella nell'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-283">Inside the existing `YoloOutputParser` class definition, add a nested class that contains the dimensions of each of the cells in the image.</span></span> <span data-ttu-id="b44e8-284">Aggiungere il codice `CellDimensions` seguente per la `DimensionsBase` classe che eredita `YoloOutputParser` dalla classe all'inizio della definizione della classe.</span><span class="sxs-lookup"><span data-stu-id="b44e8-284">Add the following code for the `CellDimensions` class that inherits from the `DimensionsBase` class at the top of the `YoloOutputParser` class definition.</span></span>

    [!code-csharp [YoloParserUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L10)]

1. <span data-ttu-id="b44e8-285">All'interno della definizione della `YoloOutputParser` classe aggiungere le costanti e i campi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b44e8-285">Inside the `YoloOutputParser` class definition, add the following constants and fields.</span></span>

    [!code-csharp [ParserVarDefinitions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L12-L21)]

    - <span data-ttu-id="b44e8-286">`ROW_COUNT`: numero di righe nella griglia in cui è divisa l'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-286">`ROW_COUNT` is the number of rows in the grid the image is divided into.</span></span>
    - <span data-ttu-id="b44e8-287">`COL_COUNT`: numero di colonne nella griglia in cui è divisa l'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-287">`COL_COUNT` is the number of columns in the grid the image is divided into.</span></span>
    - <span data-ttu-id="b44e8-288">`CHANNEL_COUNT`: numero totale di valori contenuti in una cella della griglia.</span><span class="sxs-lookup"><span data-stu-id="b44e8-288">`CHANNEL_COUNT` is the total number of values contained in one cell of the grid.</span></span>
    - <span data-ttu-id="b44e8-289">`BOXES_PER_CELL`: numero di rettangoli di selezione in una cella.</span><span class="sxs-lookup"><span data-stu-id="b44e8-289">`BOXES_PER_CELL` is the number of bounding boxes in a cell,</span></span>
    - <span data-ttu-id="b44e8-290">`BOX_INFO_FEATURE_COUNT`: numero di funzionalità contenute all'interno di un rettangolo di selezione (x, y, altezza, larghezza, confidenza).</span><span class="sxs-lookup"><span data-stu-id="b44e8-290">`BOX_INFO_FEATURE_COUNT` is the number of features contained within a box (x,y,height,width,confidence).</span></span>
    - <span data-ttu-id="b44e8-291">`CLASS_COUNT` numero di stime delle classi contenute in ogni rettangolo di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-291">`CLASS_COUNT` is the number of class predictions contained in each bounding box.</span></span>
    - <span data-ttu-id="b44e8-292">`CELL_WIDTH`: larghezza di una cella nella griglia dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-292">`CELL_WIDTH` is the width of one cell in the image grid.</span></span>
    - <span data-ttu-id="b44e8-293">`CELL_HEIGHT`: altezza di una cella nella griglia dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-293">`CELL_HEIGHT` is the height of one cell in the image grid.</span></span>
    - <span data-ttu-id="b44e8-294">`channelStride`: posizione iniziale della cella corrente nella griglia.</span><span class="sxs-lookup"><span data-stu-id="b44e8-294">`channelStride` is the starting position of the current cell in the grid.</span></span>

    <span data-ttu-id="b44e8-295">Quando il modello esegue una stima, operazione nota anche come assegnazione di punteggi, divide l'immagine di input `416px x 416px` in una griglia di celle delle dimensioni di `13 x 13`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-295">When the model makes a prediction, also known as scoring, it divides the `416px x 416px` input image into a grid of cells the size of `13 x 13`.</span></span> <span data-ttu-id="b44e8-296">Ogni cella contenuta è `32px x 32px`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-296">Each cell contains is `32px x 32px`.</span></span> <span data-ttu-id="b44e8-297">All'interno di ogni cella sono presenti 5 rettangoli di selezione, ognuno contenente 5 funzionalità (x, y, larghezza, altezza, confidenza).</span><span class="sxs-lookup"><span data-stu-id="b44e8-297">Within each cell, there are 5 bounding boxes each containing 5 features (x, y, width, height, confidence).</span></span> <span data-ttu-id="b44e8-298">Inoltre, ogni riquadro di delimitazione contiene la probabilità di ciascuna delle classi, che in questo caso è 20.</span><span class="sxs-lookup"><span data-stu-id="b44e8-298">In addition, each bounding box contains the probability of each of the classes, which in this case is 20.</span></span> <span data-ttu-id="b44e8-299">Di conseguenza, ogni cella contiene 125 informazioni (5 funzionalità + 20 probabilità delle classi).</span><span class="sxs-lookup"><span data-stu-id="b44e8-299">Therefore, each cell contains 125 pieces of information (5 features + 20 class probabilities).</span></span>

<span data-ttu-id="b44e8-300">Creare un elenco di ancoraggi sotto `channelStride` per tutti i 5 rettangoli di selezione:</span><span class="sxs-lookup"><span data-stu-id="b44e8-300">Create a list of anchors below `channelStride` for all 5 bounding boxes:</span></span>

[!code-csharp [ParserAnchors](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L23-L26)]

<span data-ttu-id="b44e8-301">Gli ancoraggi sono rapporti di altezza e larghezza predefiniti per i rettangoli di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-301">Anchors are pre-defined height and width ratios of bounding boxes.</span></span> <span data-ttu-id="b44e8-302">La maggior parte degli oggetti o delle classi rilevate da un modello ha proporzioni simili.</span><span class="sxs-lookup"><span data-stu-id="b44e8-302">Most object or classes detected by a model have similar ratios.</span></span> <span data-ttu-id="b44e8-303">Questo è importante quando si tratta di creare rettangoli di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-303">This is valuable when it comes to creating bounding boxes.</span></span> <span data-ttu-id="b44e8-304">Anziché stimare i rettangoli di selezione, viene calcolato l'offset dalle dimensioni predefinite, riducendo di conseguenza il calcolo necessario per stimare il rettangolo di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-304">Instead of predicting the bounding boxes, the offset from the pre-defined dimensions is calculated therefore reducing the computation required to predict the bounding box.</span></span> <span data-ttu-id="b44e8-305">In genere i rapporti di ancoraggio vengono calcolati in base al set di dati usato.</span><span class="sxs-lookup"><span data-stu-id="b44e8-305">Typically these anchor ratios are calculated based on the dataset used.</span></span> <span data-ttu-id="b44e8-306">In questo caso, poiché il set di dati è noto e i valori sono stati precalcolati, gli ancoraggi possono essere hardcoded.</span><span class="sxs-lookup"><span data-stu-id="b44e8-306">In this case, because the dataset is known and the values have been pre-computed, the anchors can be hard-coded.</span></span>

<span data-ttu-id="b44e8-307">Definire quindi le etichette o le classi che devono essere stimate dal modello.</span><span class="sxs-lookup"><span data-stu-id="b44e8-307">Next, define the labels or classes that the model will predict.</span></span> <span data-ttu-id="b44e8-308">Questo modello stima 20 classi, che è un sottoinsieme del numero totale di classi previsto dal modello YOLOv2 originale.</span><span class="sxs-lookup"><span data-stu-id="b44e8-308">This model predicts 20 classes, which is a subset of the total number of classes predicted by the original YOLOv2 model.</span></span>

<span data-ttu-id="b44e8-309">Aggiungere l'elenco di etichette sotto `anchors`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-309">Add your list of labels below the `anchors`.</span></span>

[!code-csharp [ParserLabels](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L28-L34)]

<span data-ttu-id="b44e8-310">A ognuna delle classi sono associati colori specifici.</span><span class="sxs-lookup"><span data-stu-id="b44e8-310">There are colors associated with each of the classes.</span></span> <span data-ttu-id="b44e8-311">Assegnare i colori delle classi sotto `labels`:</span><span class="sxs-lookup"><span data-stu-id="b44e8-311">Assign your class colors below your `labels`:</span></span>

[!code-csharp [ParserColors](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L36-L59)]

### <a name="create-helper-functions"></a><span data-ttu-id="b44e8-312">Creare funzioni di supporto</span><span class="sxs-lookup"><span data-stu-id="b44e8-312">Create helper functions</span></span>

<span data-ttu-id="b44e8-313">La fase di post-elaborazione prevede una serie di passaggi.</span><span class="sxs-lookup"><span data-stu-id="b44e8-313">There are a series of steps involved in the post-processing phase.</span></span> <span data-ttu-id="b44e8-314">Per semplificare questi passaggi, è possibile usare diversi metodi di supporto.</span><span class="sxs-lookup"><span data-stu-id="b44e8-314">To help with that, several helper methods can be employed.</span></span>

<span data-ttu-id="b44e8-315">I metodi di supporto usati dal parser sono:</span><span class="sxs-lookup"><span data-stu-id="b44e8-315">The helper methods used in by the parser are:</span></span>

- <span data-ttu-id="b44e8-316">`Sigmoid`: applica la funzione sigma che restituisce un numero compreso tra 0 e 1.</span><span class="sxs-lookup"><span data-stu-id="b44e8-316">`Sigmoid` applies the sigmoid function that outputs a number between 0 and 1.</span></span>
- <span data-ttu-id="b44e8-317">`Softmax`: normalizza un vettore di input in una distribuzione di probabilità.</span><span class="sxs-lookup"><span data-stu-id="b44e8-317">`Softmax` normalizes an input vector into a probability distribution.</span></span>
- <span data-ttu-id="b44e8-318">`GetOffset`: esegue il mapping degli elementi nell'output di un modello unidimensionale alla posizione corrispondente in un tensore `125 x 13 x 13`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-318">`GetOffset` maps elements in the one-dimensional model output to the corresponding position in a `125 x 13 x 13` tensor.</span></span>
- <span data-ttu-id="b44e8-319">`ExtractBoundingBoxes`: estrae le dimensioni dei rettangoli di selezione usando il metodo `GetOffset` dall'output del modello.</span><span class="sxs-lookup"><span data-stu-id="b44e8-319">`ExtractBoundingBoxes` extracts the bounding box dimensions using the `GetOffset` method from the model output.</span></span>
- <span data-ttu-id="b44e8-320">`GetConfidence`estrae il valore di confidenza che indica quanto `Sigmoid` sia sicuro che il modello sia rilevato un oggetto e utilizza la funzione per trasformarlo in una percentuale.</span><span class="sxs-lookup"><span data-stu-id="b44e8-320">`GetConfidence` extracts the confidence value that states how sure the model is that it has detected an object and uses the `Sigmoid` function to turn it into a percentage.</span></span>
- <span data-ttu-id="b44e8-321">`MapBoundingBoxToCell`: usa le dimensioni del rettangolo di selezione e ne esegue il mapping alla rispettiva cella all'interno dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-321">`MapBoundingBoxToCell` uses the bounding box dimensions and maps them onto its respective cell within the image.</span></span>
- <span data-ttu-id="b44e8-322">`ExtractClasses`: estrae le stime delle classi per il rettangolo di selezione dall'output del modello usando il metodo `GetOffset` e le converte in una distribuzione di probabilità tramite il metodo `Softmax`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-322">`ExtractClasses` extracts the class predictions for the bounding box from the model output using the `GetOffset` method and turns them into a probability distribution using the `Softmax` method.</span></span>
- <span data-ttu-id="b44e8-323">`GetTopResult`: seleziona la classe dall'elenco delle classi stimate con la probabilità maggiore.</span><span class="sxs-lookup"><span data-stu-id="b44e8-323">`GetTopResult` selects the class from the list of predicted classes with the highest probability.</span></span>
- <span data-ttu-id="b44e8-324">`IntersectionOverUnion`: filtra i rettangoli di selezione sovrapposti con probabilità inferiori.</span><span class="sxs-lookup"><span data-stu-id="b44e8-324">`IntersectionOverUnion` filters overlapping bounding boxes with lower probabilities.</span></span>

<span data-ttu-id="b44e8-325">Aggiungere il codice per tutti i metodi di supporto sotto l'elenco `classColors`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-325">Add the code for all the helper methods below your list of `classColors`.</span></span>

[!code-csharp [ParserHelperMethods](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L61-L151)]

<span data-ttu-id="b44e8-326">Dopo aver definito tutti i metodi di supporto, è possibile usarli per elaborare l'output del modello.</span><span class="sxs-lookup"><span data-stu-id="b44e8-326">Once you have defined all of the helper methods, it's time to use them to process the model output.</span></span>

<span data-ttu-id="b44e8-327">Sotto il metodo `IntersectionOverUnion` creare il metodo `ParseOutputs` per elaborare l'output generato dal modello.</span><span class="sxs-lookup"><span data-stu-id="b44e8-327">Below the `IntersectionOverUnion` method, create the `ParseOutputs` method to process the output generated by the model.</span></span>

```csharp
public IList<YoloBoundingBox> ParseOutputs(float[] yoloModelOutputs, float threshold = .3F)
{

}
```

<span data-ttu-id="b44e8-328">Creare un elenco per archiviare i rettangoli di selezione e definire variabili all'interno del metodo `ParseOutputs`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-328">Create a list to store your bounding boxes and define variables inside the `ParseOutputs` method.</span></span>

[!code-csharp [BBoxList](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L155)]

<span data-ttu-id="b44e8-329">Ogni immagine è divisa in una griglia di celle `13 x 13`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-329">Each image is divided into a grid of `13 x 13` cells.</span></span> <span data-ttu-id="b44e8-330">Ogni cella contiene cinque rettangoli di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-330">Each cell contains five bounding boxes.</span></span> <span data-ttu-id="b44e8-331">Sotto la variabile `boxes` aggiungere il codice per elaborare tutti i rettangoli in ognuna delle celle.</span><span class="sxs-lookup"><span data-stu-id="b44e8-331">Below the `boxes` variable, add code to process all of the boxes in each of the cells.</span></span>

```csharp
for (int row = 0; row < ROW_COUNT; row++)
{
    for (int column = 0; column < COL_COUNT; column++)
    {
        for (int box = 0; box < BOXES_PER_CELL; box++)
        {

        }
    }
}
```

<span data-ttu-id="b44e8-332">All'interno del ciclo più interno calcolare la posizione iniziale del rettangolo corrente all'interno dell'output del modello unidimensionale.</span><span class="sxs-lookup"><span data-stu-id="b44e8-332">Inside the inner-most loop, calculate the starting position of the current box within the one-dimensional model output.</span></span>

[!code-csharp [ChannelDef](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L163)]

<span data-ttu-id="b44e8-333">Direttamente sotto usare il metodo `ExtractBoundingBoxDimensions` per ottenere le dimensioni del rettangolo di selezione corrente.</span><span class="sxs-lookup"><span data-stu-id="b44e8-333">Directly below that, use the `ExtractBoundingBoxDimensions` method to get the dimensions of the current bounding box.</span></span>

[!code-csharp [GetBBoxDims](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L165)]

<span data-ttu-id="b44e8-334">Usare quindi il metodo `GetConfidence` per ottenere la confidenza per il rettangolo di selezione corrente.</span><span class="sxs-lookup"><span data-stu-id="b44e8-334">Then, use the `GetConfidence` method to get the confidence for the current bounding box.</span></span>

[!code-csharp [GetConfidence](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L167)]

<span data-ttu-id="b44e8-335">Usare ora il metodo `MapBoundingBoxToCell` per eseguire il mapping del rettangolo di selezione corrente alla cella corrente in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-335">After that, use the `MapBoundingBoxToCell` method to map the current bounding box to the current cell being processed.</span></span>

[!code-csharp [MapBoundingBoxes](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L169)]

<span data-ttu-id="b44e8-336">Prima di eseguire altre operazioni di elaborazione, controllare se il valore di confidenza è maggiore della soglia specificata.</span><span class="sxs-lookup"><span data-stu-id="b44e8-336">Before doing any further processing, check whether your confidence value is greater than the threshold provided.</span></span> <span data-ttu-id="b44e8-337">In caso contrario, elaborare il rettangolo di selezione successivo.</span><span class="sxs-lookup"><span data-stu-id="b44e8-337">If not, process the next bounding box.</span></span>

[!code-csharp [CheckThreshold1](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L171-L172)]

<span data-ttu-id="b44e8-338">Altrimenti, proseguire con l'elaborazione dell'output.</span><span class="sxs-lookup"><span data-stu-id="b44e8-338">Otherwise, continue processing the output.</span></span> <span data-ttu-id="b44e8-339">Il passaggio successivo consiste nell'ottenere la distribuzione di probabilità delle classi stimate per il rettangolo di selezione corrente usando il metodo `ExtractClasses`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-339">The next step is to get the probability distribution of the predicted classes for the current bounding box using the `ExtractClasses` method.</span></span>

[!code-csharp [ExtractClasses](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L174)]

<span data-ttu-id="b44e8-340">Usare quindi il metodo `GetTopResult` per ottenere il valore e l'indice della classe con la probabilità maggiore per il rettangolo corrente e calcolarne il punteggio.</span><span class="sxs-lookup"><span data-stu-id="b44e8-340">Then, use the `GetTopResult` method to get the value and index of the class with the highest probability for the current box and compute its score.</span></span>

[!code-csharp [GetTopResult](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L176-L177)]

<span data-ttu-id="b44e8-341">Usare `topScore` ancora una volta per mantenere solo i rettangoli di selezione che superano la soglia specificata.</span><span class="sxs-lookup"><span data-stu-id="b44e8-341">Use the `topScore` to once again keep only those bounding boxes that are above the specified threshold.</span></span>

[!code-csharp [CheckThreshold2](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L179-L180)]

<span data-ttu-id="b44e8-342">Infine, se il rettangolo di selezione corrente supera la soglia, creare un nuovo oggetto `BoundingBox` e aggiungerlo all'elenco `boxes`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-342">Finally, if the current bounding box exceeds the threshold, create a new `BoundingBox` object and add it to the `boxes` list.</span></span>

[!code-csharp [AddBBoxToList](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L182-L194)]

<span data-ttu-id="b44e8-343">Dopo aver elaborato tutte le celle nell'immagine, restituire l'elenco `boxes`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-343">Once all cells in the image have been processed, return the `boxes` list.</span></span> <span data-ttu-id="b44e8-344">Aggiungere l'istruzione return seguente sotto il ciclo for più esterno nel metodo `ParseOutputs`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-344">Add the following return statement below the outer-most for-loop in the `ParseOutputs` method.</span></span>

[!code-csharp [ReturnBoxes](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L198)]

### <a name="filter-overlapping-boxes"></a><span data-ttu-id="b44e8-345">Filtrare i rettangoli sovrapposti</span><span class="sxs-lookup"><span data-stu-id="b44e8-345">Filter overlapping boxes</span></span>

<span data-ttu-id="b44e8-346">Ora che tutti i rettangoli di selezione con confidenza elevata sono stati estratti dall'output del modello, è necessario filtrarli ulteriormente per rimuovere le immagini sovrapposte.</span><span class="sxs-lookup"><span data-stu-id="b44e8-346">Now that all of the highly confident bounding boxes have been extracted from the model output, additional filtering needs to be done to remove overlapping images.</span></span> <span data-ttu-id="b44e8-347">Aggiungere un metodo denominato `FilterBoundingBoxes` sotto il metodo `ParseOutputs`:</span><span class="sxs-lookup"><span data-stu-id="b44e8-347">Add a method called `FilterBoundingBoxes` below the `ParseOutputs` method:</span></span>

```csharp
public IList<YoloBoundingBox> FilterBoundingBoxes(IList<YoloBoundingBox> boxes, int limit, float threshold)
{

}
```

<span data-ttu-id="b44e8-348">All'interno del metodo `FilterBoundingBoxes` iniziare creando una matrice uguale alle dimensioni dei rettangoli rilevati e contrassegnando tutti gli slot come attivi o pronti per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-348">Inside the `FilterBoundingBoxes` method, start off by creating an array equal to the size of detected boxes and marking all slots as active or ready for processing.</span></span>

[!code-csharp [InitActiveSlots](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L203-L207)]

<span data-ttu-id="b44e8-349">Ordinare quindi l'elenco contenente i rettangoli di selezione in ordine decrescente in base alla confidenza.</span><span class="sxs-lookup"><span data-stu-id="b44e8-349">Then, sort the list containing your bounding boxes in descending order based on confidence.</span></span>

[!code-csharp [SortBoxes](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L209-L211)]

<span data-ttu-id="b44e8-350">Infine, creare un elenco che conterrà i risultati filtrati.</span><span class="sxs-lookup"><span data-stu-id="b44e8-350">After that, create a list to hold the filtered results.</span></span>

[!code-csharp [InitFilterResult](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L213)]

<span data-ttu-id="b44e8-351">Iniziare a elaborare ogni rettangolo di selezione tramite l'iterazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-351">Begin processing each bounding box by iterating over each of the bounding boxes.</span></span>

```csharp
for (int i = 0; i < boxes.Count; i++)
{

}
```

<span data-ttu-id="b44e8-352">All'interno di questo ciclo for controllare se il rettangolo di selezione corrente può essere elaborato.</span><span class="sxs-lookup"><span data-stu-id="b44e8-352">Inside of this for-loop, check whether the current bounding box can be processed.</span></span>

```csharp
if (isActiveBoxes[i])
{

}
```

<span data-ttu-id="b44e8-353">Se sì, aggiungere il rettangolo di selezione all'elenco dei risultati.</span><span class="sxs-lookup"><span data-stu-id="b44e8-353">If so, add the bounding box to the list of results.</span></span> <span data-ttu-id="b44e8-354">Se i risultati superano il limite specificato di caselle da estrarre, uscire dal ciclo.</span><span class="sxs-lookup"><span data-stu-id="b44e8-354">If the results exceed the specified limit of boxes to be extracted, break out of the loop.</span></span> <span data-ttu-id="b44e8-355">Aggiungere il codice seguente all'interno dell'istruzione if.</span><span class="sxs-lookup"><span data-stu-id="b44e8-355">Add the following code inside the if-statement.</span></span>

[!code-csharp [AddFirstBBoxToResults](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L219-L223)]

<span data-ttu-id="b44e8-356">In caso contrario, controllare i rettangoli di selezione adiacenti.</span><span class="sxs-lookup"><span data-stu-id="b44e8-356">Otherwise, look at the adjacent bounding boxes.</span></span> <span data-ttu-id="b44e8-357">Aggiungere il codice seguente sotto il controllo del limite di rettangoli.</span><span class="sxs-lookup"><span data-stu-id="b44e8-357">Add the following code below the box limit check.</span></span>

```csharp
for (var j = i + 1; j < boxes.Count; j++)
{

}
```

<span data-ttu-id="b44e8-358">Come per il primo rettangolo, se il rettangolo adiacente è attivo o pronto per l'elaborazione, usare il metodo `IntersectionOverUnion` per verificare se il primo e il secondo rettangolo superano la soglia specificata.</span><span class="sxs-lookup"><span data-stu-id="b44e8-358">Like the first box, if the adjacent box is active or ready to be processed, use the `IntersectionOverUnion` method to check whether the first box and the second box exceed the specified threshold.</span></span> <span data-ttu-id="b44e8-359">Aggiungere il codice seguente al ciclo for più interno.</span><span class="sxs-lookup"><span data-stu-id="b44e8-359">Add the following code to your innermost for-loop.</span></span>

[!code-csharp [IOUBBox](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L227-L239)]

<span data-ttu-id="b44e8-360">All'esterno del ciclo for più interno che controlla i rettangoli di selezione adiacenti, verificare se sono presenti altri rettangoli di selezione da elaborare.</span><span class="sxs-lookup"><span data-stu-id="b44e8-360">Outside of the inner-most for-loop that checks adjacent bounding boxes, see whether there are any remaining bounding boxes to be processed.</span></span> <span data-ttu-id="b44e8-361">In caso contrario, interrompere il ciclo for esterno.</span><span class="sxs-lookup"><span data-stu-id="b44e8-361">If not, break out of the outer for-loop.</span></span>

[!code-csharp [CheckActiveSlots](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L242-L243)]

<span data-ttu-id="b44e8-362">Infine, all'esterno del ciclo for iniziale del metodo `FilterBoundingBoxes` restituire i risultati:</span><span class="sxs-lookup"><span data-stu-id="b44e8-362">Finally, outside of the initial for-loop of the `FilterBoundingBoxes` method, return the results:</span></span>

[!code-csharp [ReturnFilteredBBox](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L246)]

<span data-ttu-id="b44e8-363">L'installazione è riuscita.</span><span class="sxs-lookup"><span data-stu-id="b44e8-363">Great!</span></span> <span data-ttu-id="b44e8-364">È ora possibile usare il codice insieme al modello per l'assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="b44e8-364">Now it's time to use this code along with the model for scoring.</span></span>

## <a name="use-the-model-for-scoring"></a><span data-ttu-id="b44e8-365">Usare il modello per l'assegnazione dei punteggi</span><span class="sxs-lookup"><span data-stu-id="b44e8-365">Use the model for scoring</span></span>

<span data-ttu-id="b44e8-366">Analogamente alla post-elaborazione, la fase di assegnazione dei punteggi prevede alcuni passaggi.</span><span class="sxs-lookup"><span data-stu-id="b44e8-366">Just like with post-processing, there are a few steps in the scoring steps.</span></span> <span data-ttu-id="b44e8-367">Per semplificare questi passaggi, aggiungere una classe che conterrà la logica di assegnazione dei punteggi al progetto.</span><span class="sxs-lookup"><span data-stu-id="b44e8-367">To help with this, add a class that will contain the scoring logic to your project.</span></span>

1. <span data-ttu-id="b44e8-368">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e quindi selezionare **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-368">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span>
1. <span data-ttu-id="b44e8-369">Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **Classe** e modificare il campo **Nome** in *OnnxModelScorer.cs*.</span><span class="sxs-lookup"><span data-stu-id="b44e8-369">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *OnnxModelScorer.cs*.</span></span> <span data-ttu-id="b44e8-370">Selezionare quindi il pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b44e8-370">Then, select the **Add** button.</span></span>

    <span data-ttu-id="b44e8-371">Il file *OnnxModelScorer.cs* viene aperto nell'editor del codice.</span><span class="sxs-lookup"><span data-stu-id="b44e8-371">The *OnnxModelScorer.cs* file opens in the code editor.</span></span> <span data-ttu-id="b44e8-372">Aggiungere l'istruzione `using` seguente all'inizio di *OnnxModelScorer.cs*:</span><span class="sxs-lookup"><span data-stu-id="b44e8-372">Add the following `using` statement to the top of *OnnxModelScorer.cs*:</span></span>

    [!code-csharp [ScorerUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L1-L7)]

    <span data-ttu-id="b44e8-373">Aggiungere le variabili seguenti all'interno della definizione di classe `OnnxModelScorer`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-373">Inside the `OnnxModelScorer` class definition, add the following variables.</span></span>

    [!code-csharp [InitScorerVars](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L13-L17)]

    <span data-ttu-id="b44e8-374">Direttamente sotto creare un costruttore per la classe `OnnxModelScorer` che Inizializzerà le variabili definite in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b44e8-374">Directly below that, create a constructor for the `OnnxModelScorer` class that will initialize the previously defined variables.</span></span>

    [!code-csharp [ScorerCtor](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L19-L24)]

    <span data-ttu-id="b44e8-375">Dopo aver creato il costruttore, definire un paio di struct che contengono variabili correlate alle impostazioni dell'immagine e del modello.</span><span class="sxs-lookup"><span data-stu-id="b44e8-375">Once you have created the constructor, define a couple of structs that contain variables related to the image and model settings.</span></span> <span data-ttu-id="b44e8-376">Creare uno struct denominato `ImageNetSettings` che conterrà l'altezza e la larghezza previste come input per il modello.</span><span class="sxs-lookup"><span data-stu-id="b44e8-376">Create a struct called `ImageNetSettings` to contain the height and width expected as input for the model.</span></span>

    [!code-csharp [ImageNetSettingStruct](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L26-L30)]

    <span data-ttu-id="b44e8-377">Successivamente, creare un `TinyYoloModelSettings` altro struct chiamato che contiene i nomi dei layer di input e output del modello.</span><span class="sxs-lookup"><span data-stu-id="b44e8-377">After that, create another struct called `TinyYoloModelSettings` that contains the names of the input and output layers of the model.</span></span> <span data-ttu-id="b44e8-378">Per visualizzare il nome dei livelli di input e output del modello, è possibile usare uno strumento come [Netron](https://github.com/lutzroeder/netron).</span><span class="sxs-lookup"><span data-stu-id="b44e8-378">To visualize the name of the input and output layers of the model, you can use a tool like [Netron](https://github.com/lutzroeder/netron).</span></span>

    [!code-csharp [YoloSettingsStruct](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L32-L43)]

    <span data-ttu-id="b44e8-379">Creare quindi il primo set di metodi da usare per l'assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="b44e8-379">Next, create the first set of methods use for scoring.</span></span> <span data-ttu-id="b44e8-380">Creare il metodo `LoadModel` all'interno della classe `OnnxModelScorer`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-380">Create the `LoadModel` method inside of your `OnnxModelScorer` class.</span></span>

    ```csharp
    private ITransformer LoadModel(string modelLocation)
    {

    }
    ```

    <span data-ttu-id="b44e8-381">All'interno del metodo `LoadModel` aggiungere il codice seguente per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-381">Inside the `LoadModel` method, add the following code for logging.</span></span>

    [!code-csharp [LoadModelLog](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L47-L49)]

    <span data-ttu-id="b44e8-382">ML.NET pipeline di ML.NET devono conoscere lo [`Fit`](xref:Microsoft.ML.IEstimator%601.Fit*) schema di dati su cui operare quando viene chiamato il metodo.</span><span class="sxs-lookup"><span data-stu-id="b44e8-382">ML.NET pipelines need to know the data schema to operate on when the [`Fit`](xref:Microsoft.ML.IEstimator%601.Fit*) method is called.</span></span> <span data-ttu-id="b44e8-383">In questo caso, verrà usato un processo simile al training.</span><span class="sxs-lookup"><span data-stu-id="b44e8-383">In this case, a process similar to training will be used.</span></span> <span data-ttu-id="b44e8-384">Tuttavia, poiché non è in corso alcuna formazione effettiva, è accettabile utilizzare un file vuoto. [`IDataView`](xref:Microsoft.ML.IDataView)</span><span class="sxs-lookup"><span data-stu-id="b44e8-384">However, because no actual training is happening, it is acceptable to use an empty [`IDataView`](xref:Microsoft.ML.IDataView).</span></span> <span data-ttu-id="b44e8-385">Creare una [`IDataView`](xref:Microsoft.ML.IDataView) nuova per la pipeline da un elenco vuoto.</span><span class="sxs-lookup"><span data-stu-id="b44e8-385">Create a new [`IDataView`](xref:Microsoft.ML.IDataView) for the pipeline from an empty list.</span></span>

    [!code-csharp [LoadEmptyIDV](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L52)]

    <span data-ttu-id="b44e8-386">Sotto questo codice definire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="b44e8-386">Below that, define the pipeline.</span></span> <span data-ttu-id="b44e8-387">La pipeline sarà costituita da quattro trasformazioni.</span><span class="sxs-lookup"><span data-stu-id="b44e8-387">The pipeline will consist of four transforms.</span></span>

    - <span data-ttu-id="b44e8-388">[`LoadImages`](xref:Microsoft.ML.ImageEstimatorsCatalog.LoadImages*)carica l'immagine come Bitmap.</span><span class="sxs-lookup"><span data-stu-id="b44e8-388">[`LoadImages`](xref:Microsoft.ML.ImageEstimatorsCatalog.LoadImages*) loads the image as a Bitmap.</span></span>
    - <span data-ttu-id="b44e8-389">[`ResizeImages`](xref:Microsoft.ML.ImageEstimatorsCatalog.ResizeImages*)ridimensiona l'immagine in base alle dimensioni `416 x 416`specificate (in questo caso, ).</span><span class="sxs-lookup"><span data-stu-id="b44e8-389">[`ResizeImages`](xref:Microsoft.ML.ImageEstimatorsCatalog.ResizeImages*) rescales the image to the size specified (in this case, `416 x 416`).</span></span>
    - <span data-ttu-id="b44e8-390">[`ExtractPixels`](xref:Microsoft.ML.ImageEstimatorsCatalog.ExtractPixels*)cambia la rappresentazione in pixel dell'immagine da Bitmap a un vettore numerico.</span><span class="sxs-lookup"><span data-stu-id="b44e8-390">[`ExtractPixels`](xref:Microsoft.ML.ImageEstimatorsCatalog.ExtractPixels*) changes the pixel representation of the image from a Bitmap to a numerical vector.</span></span>
    - <span data-ttu-id="b44e8-391">[`ApplyOnnxModel`](xref:Microsoft.ML.OnnxCatalog.ApplyOnnxModel*)carica il modello ONNX e lo utilizza per ottenere un punteggio sui dati forniti.</span><span class="sxs-lookup"><span data-stu-id="b44e8-391">[`ApplyOnnxModel`](xref:Microsoft.ML.OnnxCatalog.ApplyOnnxModel*) loads the ONNX model and uses it to score on the data provided.</span></span>

    <span data-ttu-id="b44e8-392">Definire la pipeline nel metodo `LoadModel` sotto la variabile `data`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-392">Define your pipeline in the `LoadModel` method below the `data` variable.</span></span>

    [!code-csharp [ScoringPipeline](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L55-L58)]

    <span data-ttu-id="b44e8-393">È ora possibile creare un'istanza del modello per l'assegnazione dei punteggi.</span><span class="sxs-lookup"><span data-stu-id="b44e8-393">Now it's time to instantiate the model for scoring.</span></span> <span data-ttu-id="b44e8-394">Chiamare [`Fit`](xref:Microsoft.ML.IEstimator%601.Fit*) il metodo nella pipeline e restituirlo per un'ulteriore elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-394">Call the [`Fit`](xref:Microsoft.ML.IEstimator%601.Fit*) method on the pipeline and return it for further processing.</span></span>

    [!code-csharp [FitReturnModel](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L61-L63)]

<span data-ttu-id="b44e8-395">Una volta caricato, il modello può essere usato per eseguire stime.</span><span class="sxs-lookup"><span data-stu-id="b44e8-395">Once the model is loaded, it can then be used to make predictions.</span></span> <span data-ttu-id="b44e8-396">Per semplificare il processo, creare un metodo denominato `PredictDataUsingModel` sotto il metodo `LoadModel`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-396">To facilitate that process, create a method called `PredictDataUsingModel` below the `LoadModel` method.</span></span>

```csharp
private IEnumerable<float[]> PredictDataUsingModel(IDataView testData, ITransformer model)
{

}
```

<span data-ttu-id="b44e8-397">All'interno di `PredictDataUsingModel` aggiungere il codice seguente per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-397">Inside the `PredictDataUsingModel`, add the following code for logging.</span></span>

[!code-csharp [PredictDataLog](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L68-L71)]

<span data-ttu-id="b44e8-398">Quindi, utilizzare [`Transform`](xref:Microsoft.ML.ITransformer.Transform*) il metodo per assegnare un punteggio ai dati.</span><span class="sxs-lookup"><span data-stu-id="b44e8-398">Then, use the [`Transform`](xref:Microsoft.ML.ITransformer.Transform*) method to score the data.</span></span>

[!code-csharp [ScoreImages](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L73)]

<span data-ttu-id="b44e8-399">Estrarre le probabilità stimate e restituirle per l'ulteriore elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-399">Extract the predicted probabilities and return them for additional processing.</span></span>

[!code-csharp [ReturnModelOutput](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L75-L77)]

<span data-ttu-id="b44e8-400">Una volta configurati entrambi i passaggi, combinarli in un unico metodo.</span><span class="sxs-lookup"><span data-stu-id="b44e8-400">Now that both steps are set up, combine them into a single method.</span></span> <span data-ttu-id="b44e8-401">Sotto il metodo `PredictDataUsingModel` aggiungere un nuovo metodo denominato `Score`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-401">Below the `PredictDataUsingModel` method, add a new method called `Score`.</span></span>

[!code-csharp [ScoreMethod](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L80-L85)]

<span data-ttu-id="b44e8-402">La configurazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="b44e8-402">Almost there!</span></span> <span data-ttu-id="b44e8-403">È ora possibile usarla per lo scopo di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-403">Now it's time to put it all to use.</span></span>

## <a name="detect-objects"></a><span data-ttu-id="b44e8-404">Rilevare oggetti</span><span class="sxs-lookup"><span data-stu-id="b44e8-404">Detect objects</span></span>

<span data-ttu-id="b44e8-405">Dopo aver completato la configurazione, è possibile iniziare a rilevare alcuni oggetti.</span><span class="sxs-lookup"><span data-stu-id="b44e8-405">Now that all of the setup is complete, it's time to detect some objects.</span></span> <span data-ttu-id="b44e8-406">Per iniziare, aggiungere i riferimenti al marcatore e al parser nella classe *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="b44e8-406">Start off by adding references to the scorer and parser in your *Program.cs* class.</span></span>

[!code-csharp [ReferenceScorerParser](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L8-L9)]

### <a name="score-and-parse-model-outputs"></a><span data-ttu-id="b44e8-407">Assegnare punteggi agli output del modello e analizzarli</span><span class="sxs-lookup"><span data-stu-id="b44e8-407">Score and parse model outputs</span></span>

<span data-ttu-id="b44e8-408">All'interno del metodo `Main` della classe *Program.cs* aggiungere un'istruzione try-catch.</span><span class="sxs-lookup"><span data-stu-id="b44e8-408">Inside the `Main` method of your *Program.cs* class, add a try-catch statement.</span></span>

```csharp
try
{

}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}
```

<span data-ttu-id="b44e8-409">All'interno del blocco `try` iniziare a implementare la logica di rilevamento degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="b44e8-409">Inside of the `try` block, start implementing the object detection logic.</span></span> <span data-ttu-id="b44e8-410">Innanzitutto, caricare i [`IDataView`](xref:Microsoft.ML.IDataView)dati in un file .</span><span class="sxs-lookup"><span data-stu-id="b44e8-410">First, load the data into an [`IDataView`](xref:Microsoft.ML.IDataView).</span></span>

[!code-csharp [LoadData](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L29-L30)]

<span data-ttu-id="b44e8-411">Creare quindi un'istanza di `OnnxModelScorer` e usarla per assegnare punteggi ai dati caricati.</span><span class="sxs-lookup"><span data-stu-id="b44e8-411">Then, create an instance of `OnnxModelScorer` and use it to score the loaded data.</span></span>

[!code-csharp [ScoreData](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L33-L36)]

<span data-ttu-id="b44e8-412">È ora possibile passare alla fase di post-elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-412">Now it's time for the post-processing step.</span></span> <span data-ttu-id="b44e8-413">Creare un'istanza di `YoloOutputParser` e usarla per elaborare l'output del modello.</span><span class="sxs-lookup"><span data-stu-id="b44e8-413">Create an instance of `YoloOutputParser` and use it to process the model output.</span></span>

[!code-csharp [ParsePredictions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L39-L44)]

<span data-ttu-id="b44e8-414">Dopo aver elaborato l'output del modello, è possibile tracciare i rettangoli di selezione sulle immagini.</span><span class="sxs-lookup"><span data-stu-id="b44e8-414">Once the model output has been processed, it's time to draw the bounding boxes on the images.</span></span>

### <a name="visualize-predictions"></a><span data-ttu-id="b44e8-415">Visualizzare stime</span><span class="sxs-lookup"><span data-stu-id="b44e8-415">Visualize predictions</span></span>

<span data-ttu-id="b44e8-416">Dopo che il modello ha assegnato un punteggio alle immagini e gli output sono stati elaborati, è necessario disegnare i rettangoli di selezione sull'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-416">After the model has scored the images and the outputs have been processed, the bounding boxes have to be drawn on the image.</span></span> <span data-ttu-id="b44e8-417">A tale scopo, aggiungere un metodo denominato `DrawBoundingBox` sotto il metodo `GetAbsolutePath` all'interno di *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="b44e8-417">To do so, add a method called `DrawBoundingBox` below the `GetAbsolutePath` method inside of *Program.cs*.</span></span>

```csharp
private static void DrawBoundingBox(string inputImageLocation, string outputImageLocation, string imageName, IList<YoloBoundingBox> filteredBoundingBoxes)
{

}
```

<span data-ttu-id="b44e8-418">Caricare prima di tutto l'immagine e ottenere le dimensioni di altezza e larghezza nel metodo `DrawBoundingBox`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-418">First, load the image and get the height and width dimensions in the `DrawBoundingBox` method.</span></span>

[!code-csharp [LoadImage](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L78-L81)]

<span data-ttu-id="b44e8-419">Creare quindi un ciclo for-each per eseguire l'iterazione di ogni rettangolo di selezione rilevato dal modello.</span><span class="sxs-lookup"><span data-stu-id="b44e8-419">Then, create a for-each loop to iterate over each of the bounding boxes detected by the model.</span></span>

```csharp
foreach (var box in filteredBoundingBoxes)
{

}
```

<span data-ttu-id="b44e8-420">All'interno del ciclo for-each, ottenere le dimensioni del rettangolo di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-420">Inside of the for-each loop, get the dimensions of the bounding box.</span></span>

[!code-csharp [GetBBoxDimensions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L86-L89)]

<span data-ttu-id="b44e8-421">Poiché le dimensioni del rettangolo di selezione corrispondono all'input del modello di `416 x 416`, ridimensionare il rettangolo di selezione in modo che le sue dimensioni corrispondano a quelle effettive dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-421">Because the dimensions of the bounding box correspond to the model input of `416 x 416`, scale the bounding box dimensions to match the actual size of the image.</span></span>

[!code-csharp [ScaleImage](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L92-L95)]

<span data-ttu-id="b44e8-422">Quindi, definite un modello per il testo che verrà visualizzato sopra ogni riquadro di delimitazione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-422">Then, define a template for text that will appear above each bounding box.</span></span> <span data-ttu-id="b44e8-423">Il testo conterrà la classe dell'oggetto all'interno del rispettivo rettangolo di selezione e la confidenza.</span><span class="sxs-lookup"><span data-stu-id="b44e8-423">The text will contain the class of the object inside of the respective bounding box as well as the confidence.</span></span>

[!code-csharp [DefineBBoxText](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L98)]

<span data-ttu-id="b44e8-424">Per disegnare sull'immagine, convertirla in un [`Graphics`](xref:System.Drawing.Graphics) oggetto.</span><span class="sxs-lookup"><span data-stu-id="b44e8-424">In order to draw on the image, convert it to a [`Graphics`](xref:System.Drawing.Graphics) object.</span></span>

```csharp
using (Graphics thumbnailGraphic = Graphics.FromImage(image))
{

}
```

<span data-ttu-id="b44e8-425">All'interno del `using` blocco di [`Graphics`](xref:System.Drawing.Graphics) codice, regolare le impostazioni dell'oggetto dell'elemento grafico.</span><span class="sxs-lookup"><span data-stu-id="b44e8-425">Inside the `using` code block, tune the graphic's [`Graphics`](xref:System.Drawing.Graphics) object settings.</span></span>

[!code-csharp [TuneGraphicSettings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L102-L104)]

<span data-ttu-id="b44e8-426">Al di sotto, impostare le opzioni relative al tipo di carattere e al colore per il testo e il rettangolo di selezione.</span><span class="sxs-lookup"><span data-stu-id="b44e8-426">Below that, set the font and color options for the text and bounding box.</span></span>

[!code-csharp [SetColorOptions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L106-L114)]

<span data-ttu-id="b44e8-427">Create e riempite un rettangolo sopra il [`FillRectangle`](xref:System.Drawing.Graphics.FillRectangle*) rettangolo di selezione per contenere il testo utilizzando il metodo .</span><span class="sxs-lookup"><span data-stu-id="b44e8-427">Create and fill a rectangle above the bounding box to contain the text using the [`FillRectangle`](xref:System.Drawing.Graphics.FillRectangle*) method.</span></span> <span data-ttu-id="b44e8-428">Ciò consentirà di creare un contrasto per il testo e migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="b44e8-428">This will help contrast the text and improve readability.</span></span>

[!code-csharp [DrawTextBackground](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L117)]

<span data-ttu-id="b44e8-429">Quindi, disegnare il testo e il riquadro di delimitazione sull'immagine utilizzando i [`DrawString`](xref:System.Drawing.Graphics.DrawString*) metodi e [`DrawRectangle`](xref:System.Drawing.Graphics.DrawRectangle*) .</span><span class="sxs-lookup"><span data-stu-id="b44e8-429">Then, Draw the text and bounding box on the image using the [`DrawString`](xref:System.Drawing.Graphics.DrawString*) and [`DrawRectangle`](xref:System.Drawing.Graphics.DrawRectangle*) methods.</span></span>

[!code-csharp [DrawClassAndBBox](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L118-L121)]

<span data-ttu-id="b44e8-430">Al di fuori del ciclo for-each aggiungere il codice per salvare le immagini in `outputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-430">Outside of the for-each loop, add code to save the images in the `outputDirectory`.</span></span>

[!code-csharp [SaveImage](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L125-L130)]

<span data-ttu-id="b44e8-431">Per ottenere un ulteriore riscontro che l'applicazione stia eseguendo le stime come previsto in fase di runtime, aggiungere un metodo denominato `LogDetectedObjects` sotto il metodo `DrawBoundingBox` nel file *Program.cs* per restituire gli oggetti rilevati nella console.</span><span class="sxs-lookup"><span data-stu-id="b44e8-431">For additional feedback that the application is making predictions as expected at runtime, add a method called `LogDetectedObjects` below the `DrawBoundingBox` method in the *Program.cs* file to output the detected objects to the console.</span></span>

[!code-csharp [LogOutputs](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L133-L143)]

<span data-ttu-id="b44e8-432">Ora che sono disponibili metodi helper per creare un riscontro visivo dalle stime, aggiungere un ciclo for per scorrere ognuna delle immagini con punteggio.</span><span class="sxs-lookup"><span data-stu-id="b44e8-432">Now that you have helper methods to create visual feedback from the predictions, add a for-loop to iterate over each of the scored images.</span></span>

```csharp
for (var i = 0; i < images.Count(); i++)
{

}
```

<span data-ttu-id="b44e8-433">All'interno del ciclo for ottenere il nome del file di immagine e dei rettangoli di selezione associati.</span><span class="sxs-lookup"><span data-stu-id="b44e8-433">Inside of the for-loop, get the name of the image file and the bounding boxes associated with it.</span></span>

[!code-csharp [GetImageFileName](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L49-L50)]

<span data-ttu-id="b44e8-434">Sotto questo codice usare il metodo `DrawBoundingBox` per tracciare i rettangoli di selezione sull'immagine.</span><span class="sxs-lookup"><span data-stu-id="b44e8-434">Below that, use the `DrawBoundingBox` method to draw the bounding boxes on the image.</span></span>

[!code-csharp [DrawBBoxes](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L52)]

<span data-ttu-id="b44e8-435">Infine, usare il metodo `LogDetectedObjects` per restituire le stime alla console.</span><span class="sxs-lookup"><span data-stu-id="b44e8-435">Lastly, use the `LogDetectedObjects` method to output predictions to the console.</span></span>

[!code-csharp [LogPredictionsOutput](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L54)]

<span data-ttu-id="b44e8-436">Dopo l'istruzione try-catch aggiungere logica aggiuntiva per indicare che l'esecuzione del processo è stata completata.</span><span class="sxs-lookup"><span data-stu-id="b44e8-436">After the try-catch statement, add additional logic to indicate the process is done running.</span></span>

[!code-csharp [EndProcessLog](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L62-L63)]

<span data-ttu-id="b44e8-437">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="b44e8-437">That's it!</span></span>

## <a name="results"></a><span data-ttu-id="b44e8-438">Risultati</span><span class="sxs-lookup"><span data-stu-id="b44e8-438">Results</span></span>

<span data-ttu-id="b44e8-439">Dopo aver completato i passaggi precedenti, eseguire l'app console (CTRL+F5).</span><span class="sxs-lookup"><span data-stu-id="b44e8-439">After following the previous steps, run your console app (Ctrl + F5).</span></span> <span data-ttu-id="b44e8-440">I risultati saranno simili all'output seguente.</span><span class="sxs-lookup"><span data-stu-id="b44e8-440">Your results should be similar to the following output.</span></span> <span data-ttu-id="b44e8-441">È possibile che vengano visualizzati avvisi o messaggi di elaborazione che tuttavia, per chiarezza, sono stati rimossi dai risultati riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="b44e8-441">You may see warnings or processing messages, but these messages have been removed from the following results for clarity.</span></span>

```console
=====Identify the objects in the images=====

.....The objects in the image image1.jpg are detected as below....
car and its Confidence score: 0.9697262
car and its Confidence score: 0.6674225
person and its Confidence score: 0.5226039
car and its Confidence score: 0.5224892
car and its Confidence score: 0.4675332

.....The objects in the image image2.jpg are detected as below....
cat and its Confidence score: 0.6461141
cat and its Confidence score: 0.6400049

.....The objects in the image image3.jpg are detected as below....
chair and its Confidence score: 0.840578
chair and its Confidence score: 0.796363
diningtable and its Confidence score: 0.6056048
diningtable and its Confidence score: 0.3737402

.....The objects in the image image4.jpg are detected as below....
dog and its Confidence score: 0.7608147
person and its Confidence score: 0.6321323
dog and its Confidence score: 0.5967442
person and its Confidence score: 0.5730394
person and its Confidence score: 0.5551759

========= End of Process..Hit any Key ========
```

<span data-ttu-id="b44e8-442">Per visualizzare le immagini con i rettangoli di selezione, passare alla directory `assets/images/output/`.</span><span class="sxs-lookup"><span data-stu-id="b44e8-442">To see the images with bounding boxes, navigate to the `assets/images/output/` directory.</span></span> <span data-ttu-id="b44e8-443">Di seguito viene fornito un esempio da una delle immagini elaborate.</span><span class="sxs-lookup"><span data-stu-id="b44e8-443">Below is a sample from one of the processed images.</span></span>

![Esempio di immagine elaborata di una sala da pranzo](./media/object-detection-onnx/dinning-room-table-chairs.png)

<span data-ttu-id="b44e8-445">Congratulazioni!</span><span class="sxs-lookup"><span data-stu-id="b44e8-445">Congratulations!</span></span> <span data-ttu-id="b44e8-446">È stato creato un modello di Machine Learning per il rilevamento di oggetti riutilizzando un modello `ONNX` già sottoposto a training in ML.NET.</span><span class="sxs-lookup"><span data-stu-id="b44e8-446">You've now successfully built a machine learning model for object detection by reusing a pre-trained `ONNX` model in ML.NET.</span></span>

<span data-ttu-id="b44e8-447">È possibile trovare il codice sorgente per questa esercitazione nel repository [dotnet/machinelearning-samples.You](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx) can find the source code for this tutorial at the dotnet/machinelearning-samples repository.</span><span class="sxs-lookup"><span data-stu-id="b44e8-447">You can find the source code for this tutorial at the [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx) repository.</span></span>

<span data-ttu-id="b44e8-448">In questa esercitazione sono state illustrate le procedure per:</span><span class="sxs-lookup"><span data-stu-id="b44e8-448">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
>
> - <span data-ttu-id="b44e8-449">Informazioni sul problema</span><span class="sxs-lookup"><span data-stu-id="b44e8-449">Understand the problem</span></span>
> - <span data-ttu-id="b44e8-450">Acquisire familiarità con ONNX e comprenderne il funzionamento con ML.NET</span><span class="sxs-lookup"><span data-stu-id="b44e8-450">Learn what ONNX is and how it works with ML.NET</span></span>
> - <span data-ttu-id="b44e8-451">Acquisire familiarità con il modello</span><span class="sxs-lookup"><span data-stu-id="b44e8-451">Understand the model</span></span>
> - <span data-ttu-id="b44e8-452">Riutilizzare il modello già sottoposto a training</span><span class="sxs-lookup"><span data-stu-id="b44e8-452">Reuse the pre-trained model</span></span>
> - <span data-ttu-id="b44e8-453">Rilevare oggetti con un modello caricato</span><span class="sxs-lookup"><span data-stu-id="b44e8-453">Detect objects with a loaded model</span></span>

<span data-ttu-id="b44e8-454">Consultare il repository GitHub degli esempi di Machine Learning per esaminare un esempio di rilevamento di oggetti esteso.</span><span class="sxs-lookup"><span data-stu-id="b44e8-454">Check out the Machine Learning samples GitHub repository to explore an expanded object detection sample.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b44e8-455">Repository GitHub dotnet/machinelearning-samples</span><span class="sxs-lookup"><span data-stu-id="b44e8-455">dotnet/machinelearning-samples GitHub repository</span></span>](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx)

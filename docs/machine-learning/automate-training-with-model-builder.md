---
title: Che cos'è il generatore di modelli e come funziona?
description: Come usare il generatore di modelli di ML.NET per eseguire automaticamente il training di un modello di Machine Learning
ms.date: 03/25/2020
ms.custom: overview, mlnet-tooling
ms.openlocfilehash: 9cf66455109908ebd9fc10e62cf4f067609b57d9
ms.sourcegitcommit: 59e36e65ac81cdd094a5a84617625b2a0ff3506e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2020
ms.locfileid: "80344777"
---
# <a name="what-is-model-builder-and-how-does-it-work"></a>Che cos'è il generatore di modelli e come funziona?

Il generatore di modelli di ML.NET è un'estensione grafica intuitiva di Visual Studio che consente di compilare, eseguire il training e distribuire modelli di Machine Learning personalizzati.

Il generatore di modelli usa il Machine Learning automatico (AutoML) per esplorare diversi algoritmi di Machine Learning e impostazioni per individuare quelli più adatti allo scenario.

Non è necessario avere competenze di Machine Learning per usare il generatore di modelli. Servono solo alcuni dati e un problema da risolvere. Il generatore di modelli genera il codice per aggiungere il modello all'applicazione .NET.

![Animazione dell'interfaccia utente dell'estensione del generatore di modelli di Visual Studio](media/ml-dotnet-model-builder.gif)

> [!NOTE]
> Il generatore di modelli è attualmente in anteprima.

## <a name="scenario"></a>Scenario

È possibile trasferire molti scenari diversi nel generatore di modelli per generare un modello di Machine Learning per l'applicazione.

Uno scenario è una descrizione del tipo di previsione che si vuole eseguire usando i dati. Ad esempio:

- prevedere il volume di vendita futuro dei prodotti in base ai dati storici di vendita
- classificare le valutazioni come positive o negative in base alle recensioni dei clienti
- rilevare se una transazione bancaria è fraudolenta
- indirizzare i problemi dei feedback dei clienti al team corretto nell'azienda

### <a name="which-machine-learning-scenario-is-right-for-me"></a>Quale scenario di Machine Learning è adatto alle mie esigenze?

In Model Builder, è necessario selezionare uno scenario. Il tipo di scenario dipende dal tipo di stima che si sta tentando di eseguire.

#### <a name="text-classification"></a>Classificazione del testo

La classificazione viene utilizzata per classificare i dati in categorie.

![Diagramma che mostra esempi di classificazione binaria, tra cui il rilevamento delle frodi, la mitigazione dei rischi e lo screening delle applicazioni](media/binary-classification-examples.png)

![Esempi di classificazione multiclasse, tra cui la classificazione di documenti e prodotti, il routing dei ticket di supporto e l'assegnazione di priorità ai problemi dei clienti](media/multiclass-classification-examples.png)

#### <a name="value-prediction"></a>Stima del valore

La regressione viene usata per prevedere i numeri.

![Diagramma che mostra esempi di regressione, ad esempio stime del prezzo, previsioni di vendita e manutenzione predittiva](media/regression-examples.png)

#### <a name="image-classification"></a>Classificazione di immagini

La classificazione delle immagini può essere utilizzata per identificare immagini di diverse categorie. Ad esempio, diversi tipi di terreno o animali o difetti di produzione.

È possibile utilizzare lo scenario di classificazione delle immagini se si dispone di un set di immagini e si desidera classificare le immagini in categorie diverse.

#### <a name="recommendation"></a>Recommendation

Lo scenario di raccomandazione prevede un elenco di elementi suggeriti per un determinato utente, in base a quanto simili i loro like e antipatie sono ad altri utenti'.

È possibile utilizzare lo scenario di raccomandazione quando si dispone di un insieme di utenti e di un insieme di "prodotti", ad esempio articoli da acquistare, film, libri o programmi TV, insieme a un insieme di "valutazioni" di tali prodotti da parte di un insieme di utenti.

## <a name="environment"></a>Environment

È possibile eseguire il training del modello di apprendimento automatico in un modo in locale nel computer o nel cloud in Azure.You can train your machine learning model locally on your machine or in the cloud on Azure.

Quando si esegue il training in locale, si lavora entro i vincoli delle risorse del computer (CPU, memoria e disco). Quando si esegue il training nel cloud, è possibile aumentare le risorse per soddisfare le esigenze dello scenario, in particolare per set di dati di grandi dimensioni.

La formazione locale è supportata per tutti gli scenari.

Il training di Azure è supportato per la classificazione delle immagini.

## <a name="data"></a>Dati

Dopo aver scelto lo scenario, Model Builder richiede di fornire un set di dati. I dati vengono usati per il training, la valutazione e la scelta del modello più adatto per lo scenario.

![Diagramma che illustra i passaggi del generatore di modelli](media/model-builder-steps.png)

Model Builder supporta set di dati in formato .tsv, .csv, .txt, così come il formato di database SQL. Se si dispone di un file con `,`estensione `;` `/t` txt, le colonne devono essere separate da o e il file deve avere una riga di intestazione.

Se il set di dati è costituito `.jpg` `.png`da immagini, i tipi di file supportati sono e .

Per ulteriori informazioni, consultate Caricare dati di [training in Model Builder.](how-to-guides/load-data-model-builder.md)

### <a name="choose-the-output-to-predict-label"></a>Scegliere l'output da prevedere (etichetta)

Un set di dati è una tabella di righe di esempi di training e di colonne di attributi. Ogni riga include:

- un'**etichetta** (l'attributo da prevedere)
- le **caratteristiche** (gli attributi usati come input per la previsione dell'etichetta).

Per lo scenario di stima del prezzo della casa, è possibile usare le caratteristiche seguenti:

- i metri quadrati della casa
- il numero di camere da letto e bagni
- il codice postale

L'etichetta è il prezzo storico della casa per la riga dei valori dei metri quadrati, delle camere da letto e dei bagni e il codice postale.

![Tabella che mostra le righe e le colonne di dati sui prezzi delle case con le caratteristiche delle dimensioni dei locali, del codice postale e dell'etichetta del prezzo](media/model-builder-data.png)

### <a name="example-datasets"></a>Set di dati di esempio

Se non sono ancora disponibili dati, provare uno dei set di dati seguenti:

|Scenario|Esempio|Dati|Etichetta|Funzionalità|
|-|-|-|-|-|
|Classificazione|Prevedere le anomalie di vendita|[dati di vendita dei prodotti](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv)|Vendita dei prodotti|Month|
||Prevedere il sentiment dei commenti del sito Web|[dati dei commenti del sito Web](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/wikipedia-detox-250-line-data.tsv)|Etichetta (0 con sentiment negativo, 1 con sentiment positivo)|Commento, anno|
||Prevedere transazioni fraudolente con carta di credito|[dati della carta di credito](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/getting-started/BinaryClassification_CreditCardFraudDetection/CreditCardFraudDetection.Trainer/assets/input/creditcardfraud-dataset.zip)|Classe (1 quando fraudolento, 0 in caso contrario)|Quantità, V1-V28 (caratteristiche anonime)|
||Prevedere il tipo di problema in un repository GitHubPredict the type of issue in a GitHub repository|[dati del problema di GitHub](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/end-to-end-apps/MulticlassClassification-GitHubLabeler/GitHubLabeler/Data/corefx-issues-train.tsv)|Area|Titolo, descrizione|
|Stima del valore|Prevedere il prezzo tariffario del taxi|[dati delle tariffe dei taxi](https://github.com/dotnet/machinelearning-samples/blob/master/datasets/taxi-fare-train.csv)|Tariffe|Tempo della corsa, distanza|
|Classificazione di immagini|Prevedere la categoria di un problema|[immagini floreali](http://download.tensorflow.org/example_images/flower_photos.tgz)|Il tipo di fiore: margherita, tarassaco, rose, girasoli, tulipani|I dati dell'immagine stessa|
|Recommendation|Prevedi i film che piaceranno a qualcuno|[valutazioni dei film](http://files.grouplens.org/datasets/movielens/ml-latest-small.zip)|Utenti, Film|Classificazioni|

## <a name="train"></a>Eseguire il training

Dopo aver selezionato lo scenario, i dati e l'etichetta, il generatore di modelli esegue il training del modello.

### <a name="what-is-training"></a>Cos'è il training?

Il training è un processo automatico tramite il quale il generatore di modelli indica al modello come rispondere alle domande per lo scenario. Dopo aver eseguito il training, il modello può effettuare previsioni con dati di input completamente nuovi. Ad esempio, se si sta eseguendo la stima dei prezzi e viene immessa sul mercato una nuova casa, è possibile prevederne il prezzo di vendita.

Poiché il generatore di modelli usa Il Machine Learning automatico (AutoML), non viene richiesto alcun input o ottimizzazione durante il training.

### <a name="how-long-should-i-train-for"></a>Per quanto tempo è consigliabile eseguire il training?

Model Builder utilizza AutoML per esplorare più modelli per trovare il modello più performante.

Periodi di allenamento più lunghi consentono ad AutoML di esplorare più modelli con una gamma più ampia di impostazioni.

La tabella seguente riepiloga il tempo medio impiegato per ottenere buone prestazioni per un gruppo di set di dati di esempio, in un computer locale.

|Dimensioni set di dati|Tempo medio per allenarsi|
|------------|---------------------|
|0 - 10 MB|10 sec|
|Da 10 a 100 MB|10 min|
|100 - 500 MB|30 min|
|500 - 1 GB|60 min|
|1 GB di lavoro|Più di 3 ore|

Questi numeri sono solo una guida. L'esatta durata della formazione dipende da:

- il numero di feature (colonne) utilizzate come input per il modello
- il tipo di colonne
- l'attività ML
- le prestazioni della CPU, del disco e della memoria del computer utilizzato per il training

## <a name="evaluate"></a>Valutazione

La valutazione è il processo di misurazione della qualità del modello. Model Builder usa il modello sottoposto a training per eseguire stime con nuovi dati di test e quindi misura l'efficacia delle stime.

Il generatore di modelli suddivide i dati di training in un set di training e un set di test. I dati di training (80%) vengono usati per eseguire il training del modello, mentre i dati di test (20%) vengono usati per la valutazione del modello.

### <a name="how-do-i-understand-my-model-performance"></a>Come posso capire le prestazioni del mio modello?

Uno scenario esegue il mapping a un'attività di apprendimento automatico. Ogni attività di ML dispone di un proprio set di metriche di valutazione.

#### <a name="value-prediction"></a>Stima del valore

La metrica predefinita per i problemi di stima del valore è RSquared, il valore degli intervalli RSquared compresi tra 0 e 1. 1 è il miglior valore possibile o in altre parole più vicino è il valore di RSquared a 1 migliore sarà l'esecuzione del modello.

Altre metriche segnalate, ad esempio perdita assoluta, perdita quadrata e perdita RMS, sono metriche aggiuntive, che possono essere usate per comprendere le prestazioni del modello e confrontarlo con altri modelli di stima del valore.

#### <a name="classification-2-categories"></a>Classificazione (2 categorie)

La metrica predefinita per i problemi di classificazione è l'accuratezza. Precisione definisce la proporzione di stime corrette che il modello sta facendo sul set di dati di test. Più vicino al 100% o 1,0 meglio è.

Altre metriche segnalate come AUC (Area sotto la curva), che misura il vero tasso positivo rispetto al tasso di falsi positivi dovrebbe essere maggiore di 0,50 per i modelli per essere accettabili.

Metriche aggiuntive come il punteggio F1 possono essere utilizzate per controllare il bilanciamento tra Precisione e Richiamo.

#### <a name="classification-3-categories"></a>Classificazione (più di 3 categorie)

La metrica predefinita per la classificazione multiclasse è Precisione micro. Più il Micro Accuracy è vicino al 100% o 1.0 meglio è.

Un'altra metrica importante per la classificazione multiclasse è l'accuratezza macro, simile alla Precisione Micro, più è meglio è. Un buon modo per pensare a questi due tipi di precisione è:

- Micro-precisione: con quale frequenza un biglietto in entrata viene classificato nella squadra giusta?
- Macro-precisione: Per una squadra media, con quale frequenza un biglietto in entrata è corretto per la propria squadra?

### <a name="more-information-on-evaluation-metrics"></a>Ulteriori informazioni sulle metriche di valutazione

Per altre informazioni, vedere [Metriche di valutazione dei modelli](resources/metrics.md).

## <a name="improve"></a>Migliorare

Se il punteggio delle prestazioni del modello non è quello desiderato, è possibile:

- Eseguire il training per un periodo di tempo più lungo. Con più tempo, il motore di apprendimento automatico sperimenta più algoritmi e impostazioni.

- Aggiungere altri dati. A volte la quantità di dati non è sufficiente per eseguire il training di un modello di Machine Learning di qualità elevata.

- Bilanciare i dati. Per le attività di classificazione, assicurarsi che il set di training sia bilanciato tra le categorie. Ad esempio, se sono presenti quattro classi per 100 esempi di training e le prime due classi (tag1 e tag2) vengono usate per 90 record mentre le altre due classi (tag3 e tag4) vengono usate solo per i rimanenti 10 record, la mancanza di dati bilanciati può rendere più difficile per il modello prevedere correttamente tag3 o tag4.

## <a name="code"></a>Codice

Dopo la fase di valutazione, il generatore di modelli restituisce un file di modello e il codice che è possibile usare per aggiungere il modello all'applicazione. I modelli di ML.NET vengono salvati come file con estensione zip. Il codice per caricare e usare il modello viene aggiunto come nuovo progetto nella soluzione. Il generatore di modelli aggiunge anche un'app console di esempio che è possibile eseguire per visualizzare il modello in azione.

Il generatore di modelli restituisce anche il codice che ha generato il modello che consente di comprendere i passaggi eseguiti per generare il modello. È anche possibile usare il codice di training del modello per ripetere il training del modello con nuovi dati.

## <a name="whats-next"></a>Quali sono le operazioni successive?

[Installare](how-to-guides/install-model-builder.md) l'estensione di Visual Studio per il generatore di modelli

Provare [uno scenario di regressione o stima dei prezzi](tutorials/predict-prices-with-model-builder.md)

---
title: Creazione di flussi di lavoro, attività ed espressioni tramite codice imperativo
description: Una definizione del flusso di lavoro di Workflow Foundation è un albero di oggetti attività configurati. Utilizzare il codice per creare definizioni, attività ed espressioni del flusso di lavoro.
ms.date: 03/30/2017
ms.assetid: cefc9cfc-2882-4eb9-8c94-7a6da957f2b2
ms.openlocfilehash: d8b4cb8b85d3ea3759d58e15df823a72146772e8
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421553"
---
# <a name="authoring-workflows-activities-and-expressions-using-imperative-code"></a>Creazione di flussi di lavoro, attività ed espressioni tramite codice imperativo
Una definizione del flusso di lavoro è un albero degli oggetti attività configurati che può essere definita in diversi modi, ad esempio modificando manualmente il codice XAML o usando l'utilità di progettazione del flusso di lavoro per produrre codice XAML. L'utilizzo di XAML tuttavia non è un requisito. Le definizioni del flusso di lavoro possono essere create anche a livello di codice. In questo argomento viene fornita una panoramica sulla creazione di definizioni del flusso di lavoro, di attività e di espressioni tramite codice. Per esempi relativi all'uso di flussi di lavoro XAML tramite codice, vedere [serializzazione di flussi di lavoro e attività da e verso XAML](serializing-workflows-and-activities-to-and-from-xaml.md).  
  
## <a name="creating-workflow-definitions"></a>Creazione di definizioni del flusso di lavoro  
 È possibile creare una definizione del flusso di lavoro creando un'istanza di un tipo di attività e configurando le proprietà dell'oggetto attività. Per attività che non contengono attività figlio, questa operazione può essere completata usando alcune righe di codice.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#47](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#47)]  
  
> [!NOTE]
> Negli esempi del presente argomento viene usato <xref:System.Activities.WorkflowInvoker> per l'esecuzione dei flussi di lavoro di esempio. Per ulteriori informazioni sulla chiamata di flussi di lavoro, sul passaggio di argomenti e sulle diverse opzioni di hosting disponibili, vedere [utilizzo di WorkflowInvoker e WorkflowApplication](using-workflowinvoker-and-workflowapplication.md).  
  
 In questo esempio viene creato un flusso di lavoro che è costituito da una singola attività <xref:System.Activities.Statements.WriteLine>. L'argomento <xref:System.Activities.Statements.WriteLine> dell'attività <xref:System.Activities.Statements.WriteLine.Text%2A> viene impostato e il flusso di lavoro viene richiamato. Se un'attività contiene attività figlio, il metodo di costruzione è simile. Nell'esempio seguente viene usata un'attività <xref:System.Activities.Statements.Sequence> che contiene due attività <xref:System.Activities.Statements.WriteLine>.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#48](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#48)]  
  
### <a name="using-object-initializers"></a>Uso di inizializzatori di oggetti  
 Negli esempi di questo argomento viene usata la sintassi di inizializzazione oggetti che può essere utile per creare definizioni del flusso di lavoro in codice in quanto fornisce una visualizzazione gerarchica delle attività nel flusso di lavoro e consente di illustrare la relazione tra le attività. Non è previsto alcun requisito per usare la sintassi di inizializzazione oggetti quando si creano flussi di lavoro a livello di codice. L'esempio seguente rappresenta l'equivalente funzionale dell'esempio precedente.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#49](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#49)]  
  
 Per altre informazioni sugli inizializzatori di oggetto, vedere [procedura: inizializzare oggetti senza chiamare un costruttore (Guida per programmatori C#)](../../csharp/programming-guide/classes-and-structs/how-to-initialize-objects-by-using-an-object-initializer.md) e [procedura: dichiarare un oggetto usando un inizializzatore di oggetto](../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md).  
  
### <a name="working-with-variables-literal-values-and-expressions"></a>Uso di variabili, valori letterali ed espressioni  
 Quando si crea una definizione del flusso di lavoro tramite codice, prestare attenzione a quale parte di codice viene eseguita per la creazione della definizione del flusso di lavoro e a quale invece per l'esecuzione di un'istanza di quel flusso di lavoro. Ad esempio il flusso di lavoro seguente viene usato per generare un numero casuale e scriverlo nella console.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#50](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#50)]  
  
 Quando viene eseguito questo codice di definizione del flusso di lavoro, viene effettuata la chiamata all'oggetto `Random.Next` e il risultato viene archiviato nella definizione del flusso di lavoro come valore letterale. È possibile richiamare molte istanze di questo flusso di lavoro e tutte vengono visualizzate con lo stesso numero. Per la generazione di numeri casuali durante l'esecuzione del flusso di lavoro, è necessario usare un'espressione che viene valutata ad ogni esecuzione del flusso di lavoro. Nell'esempio seguente riportato di seguito viene usata un'espressione di Visual Basic con un elemento <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#51](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#51)]  
  
 L'espressione nell'esempio precedente poteva essere distribuita anche usando un elemento <xref:Microsoft.CSharp.Activities.CSharpValue%601> e un'espressione C#.  
  
```csharp  
new Assign<int>  
{  
    To = n,  
    Value = new CSharpValue<int>("new Random().Next(1, 101)")  
}  
```  
  
 Le espressioni C# devono essere compilate prima che il flusso di lavoro che le contiene venga richiamato. Se le espressioni C# non vengono compilate, <xref:System.NotSupportedException> viene generata un'eccezione quando il flusso di lavoro viene richiamato con un messaggio simile al seguente: ``Expression Activity type 'CSharpValue`1' requires compilation in order to run.  Please ensure that the workflow has been compiled.`` nella maggior parte degli scenari che coinvolgono i flussi di lavoro creati in Visual Studio le espressioni c# vengono compilate automaticamente, ma in alcuni scenari, ad esempio i flussi di lavoro di codice, le espressioni c# devono essere compilate manualmente. Per un esempio di come compilare espressioni C#, vedere la sezione [uso di espressioni c# nei flussi di lavoro del codice](csharp-expressions.md#CodeWorkflows) dell'argomento [espressioni di c#](csharp-expressions.md) .  
  
 <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> rappresenta un'espressione nella sintassi di Visual Basic che può essere usata come r-value in un'espressione e <xref:Microsoft.CSharp.Activities.CSharpValue%601> rappresenta un'espressione nella sintassi di C# che può essere usata come r-value in un'espressione. Queste espressioni vengono valutate ad ogni esecuzione dell'attività che le contiene. Il risultato dell'espressione viene assegnato alla variabile `n` del flusso di lavoro e questi risultati vengono utilizzati dalla successiva attività nel flusso di lavoro. Per accedere al valore della variabile `n` del flusso di lavoro in fase di esecuzione, è necessario l'oggetto <xref:System.Activities.ActivityContext> al quale è possibile accedere tramite l'espressione lambda seguente.  
  
> [!NOTE]
> Si noti che entrambi i codici di esempio usano C# come linguaggio di programmazione, ma uno usa un oggetto <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> e l'altro usa un oggetto <xref:Microsoft.CSharp.Activities.CSharpValue%601>. <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> e <xref:Microsoft.CSharp.Activities.CSharpValue%601> possono essere usati sia nei progetti C# che in progetti Visual Basic. Per impostazione predefinita, le espressioni create nella finestra di progettazione del flusso di lavoro corrispondono al linguaggio del progetto di hosting. Durante la creazione dei flussi di lavoro nel codice, il linguaggio usato è a discrezione dell'autore del flusso di lavoro.  
  
 In questi esempi il risultato dell'espressione viene assegnato alla variabile `n` del flusso di lavoro e questi risultati vengono usati dalla successiva attività nel flusso di lavoro. Per accedere al valore della variabile `n` del flusso di lavoro in fase di esecuzione, è necessario l'oggetto <xref:System.Activities.ActivityContext> al quale è possibile accedere tramite l'espressione lambda seguente.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#52](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#52)]  
  
 Per ulteriori informazioni sulle espressioni lambda, vedere [espressioni lambda (Guida per programmatori C#)](../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md) o [espressioni lambda (Visual Basic)](../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
 Le espressioni lambda non sono serializzabili nel formato XAML. Se viene effettuato un tentativo di serializzare un flusso di lavoro con espressioni lambda, viene generata un'eccezione <xref:System.Activities.Expressions.LambdaSerializationException> con il messaggio seguente: "Il flusso di lavoro contiene le espressioni lambda specificate nel codice. Queste espressioni non sono serializzabili in XAML. Per rendere il flusso di lavoro serializzabile in XAML, usare VisualBasicValue/VisualBasicReference o ExpressionServices.Convert(lambda). In questo modo le espressioni lambda verranno convertite in attività di espressione." Per rendere questa espressione compatibile con XAML, usare l'oggetto <xref:System.Activities.Expressions.ExpressionServices> e il metodo <xref:System.Activities.Expressions.ExpressionServices.Convert%2A>, come illustrato nell'esempio seguente.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#53](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#53)]  
  
 Si può usare anche un oggetto <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>. Si noti che le espressioni lambda non sono obbligatorie quando si usa un'espressione di Visual Basic.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#54](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#54)]  
  
 In fase di runtime, le espressioni di Visual Basic vengono compilate nelle espressioni LINQ. Entrambi gli esempi precedenti sono serializzabili in XAML, ma se si intende visualizzare e modificare il codice XAML serializzato nella finestra di progettazione del flusso di lavoro, usare <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> per le espressioni. I flussi di lavoro serializzati che usano `ExpressionServices.Convert` possono essere aperti nella finestra di progettazione, ma il valore dell'espressione sarà vuoto. Per ulteriori informazioni sulla serializzazione dei flussi di lavoro in XAML, vedere [serializzazione di flussi di lavoro e attività da e verso XAML](serializing-workflows-and-activities-to-and-from-xaml.md).  
  
#### <a name="literal-expressions-and-reference-types"></a>Espressioni letterali e tipi riferimento  
 Le espressioni letterali sono rappresentate nei flussi di lavoro dall'attività <xref:System.Activities.Expressions.Literal%601>. Le seguenti attività <xref:System.Activities.Statements.WriteLine> sono equivalenti a livello funzionale.  
  
```csharp  
new WriteLine  
{  
    Text = "Hello World."  
},  
new WriteLine  
{  
    Text = new Literal<string>("Hello World.")  
}  
```  
  
 Non è valido inizializzare un'espressione letterale con qualsiasi tipo di riferimento eccetto <xref:System.String>. Nell'esempio riportato di seguito, la proprietà <xref:System.Activities.Statements.Assign> di un'attività <xref:System.Activities.Statements.Assign.Value%2A> viene inizializzata con un'espressione letterale usando `List<string>`.  
  
```csharp  
new Assign  
{  
    To = new OutArgument<List<string>>(items),  
    Value = new InArgument<List<string>>(new List<string>())  
},  
```  
  
 Quando il flusso di lavoro che contiene questa attività viene convalidato, viene restituito il seguente errore di convalida: “Il valore letterale supporta solo tipi di valore e il tipo non modificabile System.String. Impossibile usare System.Collections.Generic.List`1[System.String] come valore letterale". Se il flusso di lavoro viene richiamato, viene generata un'eccezione <xref:System.Activities.InvalidWorkflowException> contenente il testo dell'errore di convalida. Si tratta di un errore di convalida perché la creazione di un'espressione letterale con un tipo di riferimento non crea una nuova istanza del tipo di riferimento per ogni istanza del flusso di lavoro. Per risolvere il problema, sostituire l'espressione letterale con una che crea e restituisce una nuova istanza del tipo di riferimento.  
  
```csharp  
new Assign  
{  
    To = new OutArgument<List<string>>(items),  
    Value = new InArgument<List<string>>(new VisualBasicValue<List<string>>("New List(Of String)"))  
},  
```  
  
 Per ulteriori informazioni sulle espressioni, vedere [espressioni](expressions.md).  
  
#### <a name="invoking-methods-on-objects-using-expressions-and-the-invokemethod-activity"></a>Chiamata di metodi su oggetti usando le espressioni e l'attività InvokeMethod  
 L'attività <xref:System.Activities.Expressions.InvokeMethod%601> può essere usata per richiamare i metodi statici e di istanza di classi di .NET Framework. In un esempio precedente in questo argomento, un numero casuale è stato generato usando la classe <xref:System.Random>.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#51](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#51)]  
  
 Si sarebbe anche potuto usare l'attività <xref:System.Activities.Expressions.InvokeMethod%601> per chiamare il metodo <xref:System.Random.Next%2A> della classe <xref:System.Random>.  
  
```csharp  
new InvokeMethod<int>  
{  
    TargetObject = new InArgument<Random>(new VisualBasicValue<Random>("New Random()")),  
    MethodName = "Next",  
    Parameters =
    {  
        new InArgument<int>(1),  
        new InArgument<int>(101)  
    },  
    Result = n  
}  
```  
  
 Poiché <xref:System.Random.Next%2A> non è un metodo statico, un'istanza della classe <xref:System.Random> viene fornita per la proprietà <xref:System.Activities.Expressions.InvokeMethod%601.TargetObject%2A>. In questo esempio viene creata una nuova istanza usando un'espressione di Visual Basic, ma avrebbe potuto essere creata in precedenza ed essere archiviata in una variabile del flusso di lavoro. In questo esempio, sarebbe più semplice usare l'attività <xref:System.Activities.Statements.Assign%601> anziché l'attività <xref:System.Activities.Expressions.InvokeMethod%601>. Se la chiamata al metodo richiamato di recente dalla attività <xref:System.Activities.Statements.Assign%601> o <xref:System.Activities.Expressions.InvokeMethod%601> ha un'esecuzione prolungata, <xref:System.Activities.Expressions.InvokeMethod%601> ha un vantaggio poiché dispone di una proprietà <xref:System.Activities.Expressions.InvokeMethod%601.RunAsynchronously%2A>. Se questa proprietà è impostata su `true`, il metodo richiamato verrà eseguito in modo asincrono rispetto al flusso di lavoro. Se vi sono altre attività in parallelo, queste non verranno bloccate durante l'esecuzione asincrona del metodo. Inoltre, se il metodo da richiamare non ha valore restituito, <xref:System.Activities.Expressions.InvokeMethod%601> rappresenta la soluzione appropriata per richiamare il metodo.  
  
## <a name="arguments-and-dynamic-activities"></a>Argomenti e attività dinamiche  
 Una definizione del flusso di lavoro viene creata in codice assemblando le attività in un albero delle attività e configurando qualsiasi proprietà e argomento. Gli argomenti esistenti possono essere associati, ma quelli nuovi non possono essere aggiunti alle attività, inclusi gli argomenti del flusso di lavoro passati all'attività radice. In codice imperativo, gli argomenti del flusso di lavoro vengono specificati come proprietà in un nuovo tipo CLR e in XAML vengono dichiarati tramite gli oggetti `x:Class` e `x:Member`. Poiché non è disponibile alcun nuovo tipo CLR creato quando una definizione del flusso di lavoro viene creata come albero degli oggetti in memoria, gli argomenti non possono essere aggiunti. Tuttavia, gli argomenti possono essere aggiunti a un oggetto <xref:System.Activities.DynamicActivity>. In questo esempio viene creato un oggetto <xref:System.Activities.DynamicActivity%601> che accetta due argomenti Integer, li somma e restituisce il risultato. Viene creato un oggetto <xref:System.Activities.DynamicActivityProperty> per ogni argomento e il risultato dell'operazione viene assegnato all'argomento <xref:System.Activities.Activity%601.Result%2A> dell'oggetto <xref:System.Activities.DynamicActivity%601>.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#55](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#55)]  
  
 Per ulteriori informazioni sulle attività dinamiche, vedere [creazione di un'attività in fase di esecuzione](creating-an-activity-at-runtime-with-dynamicactivity.md).  
  
## <a name="compiled-activities"></a>Attività compilate  
 Le attività dinamiche sono un modo per definire tramite codice un'attività che contiene argomenti, ma le attività possono anche essere create nel codice e compilate nei tipi. È possibile creare attività semplici che derivano da <xref:System.Activities.CodeActivity>e attività asincrone che derivano da <xref:System.Activities.AsyncCodeActivity>. Queste attività possono avere argomenti, valori restituiti e definiscono la relativa logica usando il codice imperativo. Per esempi di creazione di questi tipi di attività, vedere [classe di base CodeActivity](workflow-activity-authoring-using-the-codeactivity-class.md) e [creazione di attività asincrone](creating-asynchronous-activities-in-wf.md).  
  
 Le attività che derivano da <xref:System.Activities.NativeActivity> possono definire la relativa logica usando il codice imperativo possono inoltre contenere attività figlio che definiscono la logica. Dispongono inoltre dell'accesso completo alle funzionalità del runtime come la creazione dei segnalibri. Per esempi relativi alla creazione di un' <xref:System.Activities.NativeActivity> attività basata su, vedere la pagina relativa alla [classe di base NativeActivity](nativeactivity-base-class.md), [procedura: creare un'attività](how-to-create-an-activity.md)e l'esempio [Custom Composite using Native Activity](./samples/custom-composite-using-native-activity.md) .  
  
 Le attività che derivano da <xref:System.Activities.Activity> definiscono la relativa logica unicamente attraverso l'uso di attività figlio. Queste attività vengono in genere create tramite la finestra di progettazione del flusso di lavoro, ma possono essere definite anche tramite codice. Nell'esempio seguente viene definita un'attività `Square` che deriva da `Activity<int>`. L'attività `Square` ha un unico <xref:System.Activities.InArgument%601> denominato `Value` e definisce la relativa logica specificando un'attività <xref:System.Activities.Statements.Sequence> che usa la proprietà <xref:System.Activities.Activity.Implementation%2A>. L'attività <xref:System.Activities.Statements.Sequence> contiene un'attività <xref:System.Activities.Statements.WriteLine> e un'attività <xref:System.Activities.Statements.Assign%601>. Insieme, queste tre attività implementano la logica dell'attività `Square`.  
  
```csharp  
class Square : Activity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Value { get; set; }  
  
    public Square()  
    {  
        this.Implementation = () => new Sequence  
        {  
            Activities =  
            {  
                new WriteLine  
                {  
                    Text = new InArgument<string>((env) => "Squaring the value: " + this.Value.Get(env))  
                },  
                new Assign<int>  
                {  
                    To = new OutArgument<int>((env) => this.Result.Get(env)),  
                    Value = new InArgument<int>((env) => this.Value.Get(env) * this.Value.Get(env))  
                }  
            }  
        };  
    }  
}  
```  
  
 Nell'esempio riportato di seguito, una definizione del flusso di lavoro costituita da un'unica attività `Square` viene richiamata usando <xref:System.Activities.WorkflowInvoker>.  
  
```csharp  
Dictionary<string, object> inputs = new Dictionary<string, object> {{ "Value", 5}};  
int result = WorkflowInvoker.Invoke(new Square(), inputs);  
Console.WriteLine("Result: {0}", result);  
```  
  
 Quando il flusso di lavoro viene richiamato, l'output seguente viene visualizzato nella console:  
  
 **Elevazione al quadrato del valore: 5.**  
**Result: 25**

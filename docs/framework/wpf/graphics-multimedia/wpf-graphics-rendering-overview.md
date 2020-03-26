---
title: Panoramica del rendering della grafica
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], rendering
- rendering graphics [WPF]
ms.assetid: 6dec9657-4d8c-4e46-8c54-40fb80008265
ms.openlocfilehash: 9d58aa973f7de6c073611e13f2889913ff26dd55
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111920"
---
# <a name="wpf-graphics-rendering-overview"></a>Cenni preliminari sul rendering della grafica WPF
Questo argomento offre una panoramica del livello visivo di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Si concentra sul ruolo della <xref:System.Windows.Media.Visual> classe per il [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] rendering del supporto nel modello.  

<a name="role_of_visual_object"></a>
## <a name="role-of-the-visual-object"></a>Ruolo dell'oggetto visivo  
 La <xref:System.Windows.Media.Visual> classe è l'astrazione <xref:System.Windows.FrameworkElement> di base da cui deriva ogni oggetto. Viene anche usata come punto di ingresso per la scrittura di nuovi controlli in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e in molti casi può essere considerata come l'handle di finestra (HWND) nel modello di applicazione Win32.  
  
 L'oggetto <xref:System.Windows.Media.Visual> è [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] un oggetto principale, il cui ruolo principale è quello di fornire il supporto per il rendering. I controlli dell'interfaccia <xref:System.Windows.Controls.TextBox>utente, <xref:System.Windows.Media.Visual> quali <xref:System.Windows.Controls.Button> e , derivano dalla classe e li utilizzano per rendere persistenti i dati di rendering. L'oggetto <xref:System.Windows.Media.Visual> fornisce supporto per:  
  
- Visualizzazione dell'output: eseguire il rendering del contenuto del disegno serializzato e salvato in modo permanente di un oggetto visivo.  
  
- Trasformazioni: eseguire trasformazioni su un oggetto visivo.  
  
- Ritaglio: offrire supporto dell'area di ritaglio per un oggetto visivo.  
  
- Hit testing: determinare se una coordinata o una geometria è contenuta all'interno di un oggetto visivo.  
  
- Calcoli relativi al rettangolo di selezione: determinare il rettangolo delimitatore di un oggetto visivo.  
  
 Tuttavia, <xref:System.Windows.Media.Visual> l'oggetto non include il supporto per le funzionalità non di rendering, ad esempio:However, the object does not include support for non-rendering features, such as:  
  
- Gestione degli eventi  
  
- Layout  
  
- Stili  
  
- Associazione dati  
  
- Globalizzazione  
  
 <xref:System.Windows.Media.Visual>viene esposto come classe astratta pubblica da cui devono essere derivate le classi figlio. La figura seguente illustra la gerarchia degli oggetti visivi esposti in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 ![Diagramma delle classi derivate dall'oggetto Visual](./media/wpf-graphics-rendering-overview/classes-derived-visual-object.png)
  
### <a name="drawingvisual-class"></a>Classe DrawingVisual  
 Si <xref:System.Windows.Media.DrawingVisual> tratta di una classe di disegno leggera utilizzata per eseguire il rendering di forme, immagini o testo. Questa classe è considerata semplice perché non offre la gestione di layout o eventi, che migliora le prestazioni di runtime. Per questo motivo, i disegni sono ideali per sfondi e ClipArt. L'oggetto <xref:System.Windows.Media.DrawingVisual> può essere utilizzato per creare un oggetto visivo personalizzato. Per altre informazioni, vedere [Uso degli oggetti DrawingVisual](using-drawingvisual-objects.md).  
  
### <a name="viewport3dvisual-class"></a>Classe Viewport3DVisual  
 L'oggetto <xref:System.Windows.Media.Media3D.Viewport3DVisual> fornisce un <xref:System.Windows.Media.Visual> <xref:System.Windows.Media.Media3D.Visual3D> ponte tra 2D e oggetti. La <xref:System.Windows.Media.Media3D.Visual3D> classe è la classe base per tutti gli elementi visivi 3D. Il <xref:System.Windows.Media.Media3D.Viewport3DVisual> richiede di <xref:System.Windows.Media.Media3D.Viewport3DVisual.Camera%2A> definire un <xref:System.Windows.Media.Media3D.Viewport3DVisual.Viewport%2A> valore e un valore. La camera consente di visualizzare la scena. Il viewport stabilisce dove viene eseguito il mapping della proiezione sulla superficie 2D. Per ulteriori informazioni sul [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]3D in , vedere [Cenni preliminari sulla grafica 3D](3-d-graphics-overview.md).  
  
### <a name="containervisual-class"></a>Classe ContainerVisual  
 La <xref:System.Windows.Media.ContainerVisual> classe viene utilizzata come contenitore per una raccolta di <xref:System.Windows.Media.Visual> oggetti. La <xref:System.Windows.Media.DrawingVisual> classe deriva <xref:System.Windows.Media.ContainerVisual> dalla classe , consentendo di contenere una raccolta di oggetti visivi.  
  
### <a name="drawing-content-in-visual-objects"></a>Contenuto del disegno in oggetti visivi  
 Un <xref:System.Windows.Media.Visual> oggetto archivia i dati di rendering come elenco di **istruzioni di grafica vettoriale.** Ogni elemento nell'elenco di istruzioni rappresenta un set di dati grafici di basso livello e risorse associate in un formato serializzato. Esistono quattro diversi tipi di dati di rendering che possono contenere il contenuto del disegno.  
  
|Tipo di contenuto del disegno|Descrizione|  
|--------------------------|-----------------|  
|Grafica vettoriale|Rappresenta i dati grafici <xref:System.Windows.Media.Brush> <xref:System.Windows.Media.Pen> vettoriali e tutte le informazioni e le informazioni associate.|  
|Immagine|Rappresenta un'immagine all'interno <xref:System.Windows.Rect>di un'area definita da un oggetto .|  
|Icona|Rappresenta un disegno <xref:System.Windows.Media.GlyphRun>che esegue il rendering di un oggetto , che è una sequenza di glifi da una risorsa tipo di carattere specificata. Ecco come viene rappresentato il testo.|  
|Video|Rappresenta un disegno che esegue il rendering di video.|  
  
 L'oggetto <xref:System.Windows.Media.DrawingContext> consente <xref:System.Windows.Media.Visual> di popolare un oggetto con contenuto visivo. Quando si <xref:System.Windows.Media.DrawingContext> utilizzano i comandi di disegno di un oggetto, si archivia effettivamente un set di dati di rendering che verranno successivamente utilizzati dal sistema grafico; non si sta disegnando sullo schermo in tempo reale.  
  
 Quando si [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] crea un controllo, ad esempio un <xref:System.Windows.Controls.Button>oggetto , il controllo genera in modo implicito i dati di rendering per il disegno stesso. Ad esempio, <xref:System.Windows.Controls.ContentControl.Content%2A> l'impostazione della proprietà dell'oggetto <xref:System.Windows.Controls.Button> fa sì che il controllo memorizzi una rappresentazione di rendering di un glifo.  
  
 Un <xref:System.Windows.Media.Visual> oggetto descrive il contenuto <xref:System.Windows.Media.Drawing> come uno <xref:System.Windows.Media.DrawingGroup>o più oggetti contenuti all'interno di un oggetto . Un <xref:System.Windows.Media.DrawingGroup> oggetto descrive inoltre le maschere di opacità, le trasformazioni, gli effetti bitmap e altre operazioni applicate al relativo contenuto. <xref:System.Windows.Media.DrawingGroup>Le operazioni vengono applicate nel seguente <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>ordine <xref:System.Windows.Media.DrawingGroup.Opacity%2A> <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>quando <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>viene eseguito il rendering del contenuto: , , , , <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>, e quindi <xref:System.Windows.Media.DrawingGroup.Transform%2A>.  
  
 Nella figura seguente viene <xref:System.Windows.Media.DrawingGroup> illustrato l'ordine in cui le operazioni vengono applicate durante la sequenza di rendering.  
  
 ![Ordine delle operazioni DrawingGroup](./media/graphcismm-drawinggroup-order.png "graphcismm_drawinggroup_order")  
Ordine delle operazioni DrawingGroup  
  
 Per altre informazioni, vedere [Cenni preliminari sugli oggetti Drawing](drawing-objects-overview.md).  
  
#### <a name="drawing-content-at-the-visual-layer"></a>Contenuto del disegno a livello visivo  
 Non si crea <xref:System.Windows.Media.DrawingContext>mai direttamente un'istanza di ; è tuttavia possibile acquisire un contesto di <xref:System.Windows.Media.DrawingGroup.Open%2A?displayProperty=nameWithType> <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A?displayProperty=nameWithType>disegno da determinati metodi, ad esempio e . Nell'esempio seguente <xref:System.Windows.Media.DrawingContext> viene <xref:System.Windows.Media.DrawingVisual> recuperato un da un e viene utilizzato per disegnare un rettangolo.  
  
 [!code-csharp[drawingvisualsample#101](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#101)]
 [!code-vb[drawingvisualsample#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#101)]  
  
#### <a name="enumerating-drawing-content-at-the-visual-layer"></a>Enumerazione del contenuto del disegno a livello visivo  
 Oltre agli altri utilizzi, <xref:System.Windows.Media.Drawing> gli oggetti forniscono anche un <xref:System.Windows.Media.Visual>modello a oggetti per l'enumerazione del contenuto di un oggetto .  
  
> [!NOTE]
> Quando si enumera il contenuto dell'oggetto visivo, si recuperano <xref:System.Windows.Media.Drawing> gli oggetti e non la rappresentazione sottostante dei dati di rendering come elenco di istruzioni di grafica vettoriale.  
  
 Nell'esempio seguente <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> viene utilizzato <xref:System.Windows.Media.DrawingGroup> il <xref:System.Windows.Media.Visual> metodo per recuperare il valore di un oggetto ed enumerarlo.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
<a name="how_visual_objects_are_used_to_build_controls"></a>
## <a name="how-visual-objects-are-used-to-build-controls"></a>Uso degli oggetti visivi per la compilazione di controlli  
 Molti degli oggetti in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono costituiti da altri oggetti visivi, cioè possono contenere gerarchie variabili di oggetti discendenti. Molti degli elementi dell'interfaccia utente in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], ad esempio i controlli, sono composti da più oggetti visivi che rappresentano tipi diversi di elementi di rendering. Ad esempio, <xref:System.Windows.Controls.Button> il controllo può contenere <xref:Microsoft.Windows.Themes.ClassicBorderDecorator>una <xref:System.Windows.Controls.ContentPresenter>serie <xref:System.Windows.Controls.TextBlock>di altri oggetti, tra cui , e .  
  
 Nel codice seguente <xref:System.Windows.Controls.Button> viene illustrato un controllo definito nel markup.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet1)]  
  
 Se si desidera enumerare gli oggetti <xref:System.Windows.Controls.Button> visivi che costituiscono il controllo predefinito, è possibile trovare la gerarchia degli oggetti visivi illustrata di seguito:If you were to enumerate the visual objects that comprise the default control, you would find the hierarchy of visual objects illustrated below:  
  
 ![Diagramma della gerarchia di una struttura ad albero visuale](./media/wpf-graphics-rendering-overview/visual-object-diagram.gif)
  
 Il <xref:System.Windows.Controls.Button> controllo <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> contiene un elemento, che <xref:System.Windows.Controls.ContentPresenter> a sua volta contiene un elemento. L'elemento <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> è responsabile del disegno <xref:System.Windows.Controls.Button>di un bordo e di uno sfondo per il file . L'elemento <xref:System.Windows.Controls.ContentPresenter> è responsabile della <xref:System.Windows.Controls.Button>visualizzazione del contenuto dell'oggetto . In questo caso, poiché si <xref:System.Windows.Controls.ContentPresenter> visualizza il <xref:System.Windows.Controls.TextBlock> testo, l'elemento contiene un elemento. Il fatto <xref:System.Windows.Controls.Button> che il <xref:System.Windows.Controls.ContentPresenter> controllo utilizza un mezzo che il contenuto <xref:System.Windows.Controls.Image> potrebbe essere rappresentato <xref:System.Windows.Media.EllipseGeometry>da altri elementi, ad esempio un o una geometria, ad esempio un oggetto .  
  
### <a name="control-templates"></a>Modelli di controllo  
 La chiave per l'espansione di un controllo <xref:System.Windows.Controls.ControlTemplate>in una gerarchia di controlli è la . Un modello di controllo specifica la gerarchia visiva predefinita per un controllo. Quando si fa riferimento in modo esplicito a un controllo, si fa riferimento in modo implicito alla relativa gerarchia visiva. È possibile eseguire l'override dei valori predefiniti di un modello di controllo per creare un aspetto visivo personalizzato per un controllo. Ad esempio, è possibile modificare il <xref:System.Windows.Controls.Button> valore del colore di sfondo del controllo in modo che utilizzi un valore di colore sfumato lineare anziché un valore di colore a tinta unita. Per altre informazioni, vedere [Stili e modelli di Button](../controls/button-styles-and-templates.md).  
  
 Un elemento dell'interfaccia <xref:System.Windows.Controls.Button> utente, ad esempio un controllo, contiene diversi elenchi di istruzioni di grafica vettoriale che descrivono l'intera definizione di rendering di un controllo. Nel codice seguente <xref:System.Windows.Controls.Button> viene illustrato un controllo definito nel markup.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet2)]  
  
 Se si dovessero enumerare gli oggetti visivi <xref:System.Windows.Controls.Button> e gli elenchi di istruzioni di grafica vettoriale che costituiscono il controllo, è necessario trovare la gerarchia di oggetti illustrata di seguito:If you were to enumerate the visual objects and vector graphics instruction lists that comprise the control, you would find the hierarchy of objects illustrated below:  
  
 ![Diagramma della struttura ad albero e dei dati di rendering](./media/wpf-graphics-rendering-overview/visual-tree-rendering-data.png)  
  
 Il <xref:System.Windows.Controls.Button> controllo <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> contiene un elemento, che <xref:System.Windows.Controls.ContentPresenter> a sua volta contiene un elemento. L'elemento <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> è responsabile del disegno di tutti gli elementi grafici discreti che costituiscono il bordo e lo sfondo di un pulsante. L'elemento <xref:System.Windows.Controls.ContentPresenter> è responsabile della <xref:System.Windows.Controls.Button>visualizzazione del contenuto dell'oggetto . In questo caso, poiché si sta <xref:System.Windows.Controls.ContentPresenter> visualizzando <xref:System.Windows.Controls.Image> un'immagine, l'elemento contiene un elemento.  
  
 Tenere in considerazione alcuni punti sulla gerarchia degli oggetti visivi e sugli elenchi di istruzioni di grafica vettoriale:  
  
- L'ordinamento nella gerarchia rappresenta l'ordine di rendering delle informazioni di disegno. A partire dall'elemento visivo radice, gli elementi figlio vengono attraversati da sinistra a destra e dall'alto verso il basso. Se un elemento contiene elementi visivi figlio, essi vengono attraversati prima degli elementi di pari livello.  
  
- Gli elementi del nodo non foglia nella gerarchia, ad <xref:System.Windows.Controls.ContentPresenter>esempio , vengono utilizzati per contenere elementi figlio, ovvero non contengono elenchi di istruzioni.  
  
- Se un elemento visivo contiene sia un elenco di istruzioni di grafica vettoriale che oggetti visivi figlio, viene eseguito il rendering dell'elenco di istruzioni nell'elemento visivo padre prima dei disegni in uno qualsiasi degli oggetti visivi figlio.  
  
- Il rendering degli elementi nell'elenco di istruzioni di grafica vettoriale viene eseguito da sinistra a destra.  
  
<a name="visual_tree"></a>
## <a name="visual-tree"></a>Struttura ad albero visuale  
 La struttura ad albero visuale contiene tutti gli elementi visivi usati nell'interfaccia utente di un'applicazione. Poiché un elemento visivo contiene informazioni sul disegno salvate in modo permanente, la struttura ad albero visuale può essere considerata come un grafico della scena, contenente tutte le informazioni di rendering necessarie per comporre l'output verso il dispositivo di visualizzazione. Questo albero è costituito da tutti gli elementi visivi creati direttamente dall'applicazione, nel codice o nel markup. La struttura ad albero visuale contiene anche tutti gli elementi visivi creati dall'espansione del modello di elementi quali controlli e oggetti dati.  
  
 Il codice seguente <xref:System.Windows.Controls.StackPanel> mostra un elemento definito nel markup.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet3)]  
  
 Se si desidera enumerare gli <xref:System.Windows.Controls.StackPanel> oggetti visivi che costituiscono l'elemento nell'esempio di markup, è necessario trovare la gerarchia di oggetti visivi illustrata di seguito:If you were to enumerate the visual objects that comprise the element in the markup example, you would find the hierarchy of visual objects illustrated below:  
  
 ![Diagramma della gerarchia di una struttura ad albero visuale](./media/wpf-graphics-rendering-overview/visual-tree-hierarchy.gif)  
  
### <a name="rendering-order"></a>Ordine di rendering  
 La struttura ad albero visuale determina l'ordine di rendering degli oggetti visivi e di disegno di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. L'ordine di attraversamento inizia con l'oggetto visivo radice, ovvero il nodo superiore nella struttura ad albero visuale. Gli elementi figlio dell'oggetto visivo radice vengono quindi attraversati, da sinistra a destra. Se un oggetto visivo ha elementi figlio, questi ultimi vengono attraversati prima degli elementi di pari livello. Ciò significa che viene eseguito il rendering del contenuto di un oggetto visivo figlio prima del contenuto dell'oggetto visivo stesso.  
  
 ![Diagramma dell'ordine di rendering della struttura ad albero visuale](./media/wpf-graphics-rendering-overview/visual-tree-rendering-order.gif)
  
### <a name="root-visual"></a>Oggetto visivo radice  
 L'**oggetto visivo radice** è l'elemento di primo livello di una gerarchia struttura ad albero visuale. Nella maggior parte delle applicazioni, la <xref:System.Windows.Window> classe <xref:System.Windows.Navigation.NavigationWindow>base dell'oggetto visivo radice è o . Se venissero tuttavia ospitati oggetti visivi in un'applicazione Win32, l'oggetto visivo radice sarebbe l'oggetto visivo di primo livello ospitato nella finestra Win32. Per altre informazioni, vedere [Esercitazione: hosting di oggetti visivi in un'applicazione Win32](tutorial-hosting-visual-objects-in-a-win32-application.md).  
  
### <a name="relationship-to-the-logical-tree"></a>Relazione con l'albero logico  
 L'albero logico in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] rappresenta gli elementi di un'applicazione in fase di esecuzione. Sebbene questo albero non venga modificato direttamente, la visualizzazione dell'applicazione è utile per comprendere l'ereditarietà delle proprietà e il routing degli eventi. A differenza della struttura ad albero visuale, l'albero logico può rappresentare oggetti dati non visivi, ad <xref:System.Windows.Documents.ListItem>esempio . In molti casi, l'albero logico corrisponde strettamente alle definizioni di markup dell'applicazione. Il codice seguente <xref:System.Windows.Controls.DockPanel> mostra un elemento definito nel markup.  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet5](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet5)]  
  
 Se si dovessero enumerare gli <xref:System.Windows.Controls.DockPanel> oggetti logici che costituiscono l'elemento nell'esempio di markup, è possibile trovare la gerarchia di oggetti logici illustrata di seguito:If you were to enumerate the logical objects that comprise the element in the markup example, you would find the hierarchy of logical objects illustrated below:  
  
 ![Diagramma ad albero](./media/tree1-wcp.gif "Tree1_wcp")  
Diagramma dell'albero logico  
  
 La struttura ad albero visuale e l'albero logico sono sincronizzati con il set corrente di elementi dell'applicazione che riflette qualsiasi aggiunta, eliminazione o modifica di elementi. Presentano tuttavia visualizzazioni diverse dell'applicazione. A differenza della struttura ad albero visuale, <xref:System.Windows.Controls.ContentPresenter> l'albero logico non espande l'elemento di un controllo. Ciò significa che non vi è una corrispondenza diretta tra un albero logico e una struttura ad albero visuale per lo stesso set di oggetti. Infatti, la chiamata del metodo <xref:System.Windows.LogicalTreeHelper.GetChildren%2A> dell'oggetto **LogicalTreeHelper** e <xref:System.Windows.Media.VisualTreeHelper.GetChild%2A> del metodo dell'oggetto **VisualTreeHelper** utilizzando lo stesso elemento di un parametro produce risultati diversi.  
  
 Per altre informazioni sull'albero logico, vedere [Strutture ad albero in WPF](../advanced/trees-in-wpf.md).  
  
### <a name="viewing-the-visual-tree-with-xamlpad"></a>Visualizzazione della struttura ad albero visuale con XamlPad  
 Lo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] strumento XamlPad offre un'opzione per la visualizzazione e l'esplorazione della struttura ad albero visuale che corrisponde al contenuto XAML attualmente definito. Fare clic sul pulsante **Show Visual Tree** (Mostra struttura ad albero visuale) sulla barra dei menu per visualizzare la struttura ad albero visuale. Di seguito viene illustrata l'espansione del contenuto XAML in nodi della struttura ad albero visuale nel riquadro **Esplora albero visuale** di XamlPad:The following illustrates the expansion of XAML content into visual tree nodes in the Visual Tree Explorer panel of XamlPad:  
  
 ![Pannello Visual Tree Explorer in XamlPad](./media/wpf-graphics-rendering-overview/visual-tree-explorer.png)  

 Si noti <xref:System.Windows.Controls.TextBox>come <xref:System.Windows.Controls.Button> i <xref:System.Windows.Controls.Label>controlli , e visualizzino ciascuno una gerarchia di oggetti visivi separata nel pannello Esplora struttura **ad albero visuale** di XamlPad. Ciò [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è dovuto <xref:System.Windows.Controls.ControlTemplate> al fatto che i controlli dispongono di un che contiene la struttura ad albero visuale di tale controllo. Quando si fa riferimento in modo esplicito a un controllo, si fa riferimento in modo implicito alla relativa gerarchia visiva.  
  
### <a name="profiling-visual-performance"></a>Profilatura delle prestazioni visive  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] include una suite di strumenti per la profilatura delle prestazioni che consentono di analizzare il comportamento dell'applicazione in fase di esecuzione e di determinare i tipi di ottimizzazioni delle prestazioni che è possibile applicare. Lo strumento Visual Profiler offre una visualizzazione grafica completa dei dati sulle prestazioni eseguendo il mapping direttamente alla struttura ad albero visuale dell'applicazione. In questa schermata, la sezione **Utilizzo della CPU** di Visual Profiler fornisce un'indicazione dettagliata dell'uso dei servizi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] da parte di un oggetto, ad esempio il layout e il rendering.  
  
 ![Output di Visual Profiler](./media/wpfperf-visualprofiler-04.png "WPFPerf_VisualProfiler_04")  
Output di Visual Profiler  
  
<a name="visual_rendering_behavior"></a>
## <a name="visual-rendering-behavior"></a>Comportamento di rendering visivo  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] introduce numerose funzionalità che influiscono sul comportamento di rendering degli oggetti visivi: grafica in modalità differita, grafica vettoriale e grafica indipendente dal dispositivo.  
  
### <a name="retained-mode-graphics"></a>Grafica in modalità differita  
 Uno dei fattori chiave per comprendere il ruolo dell'oggetto visivo consiste nel comprendere la differenza tra i sistemi di grafica in **modalità immediata** e in **modalità differita**. Un'applicazione Win32 standard basata su GDI o GDI+ usa un sistema di grafica in modalità immediata. Ciò significa che l'applicazione è responsabile dell'aggiornamento della porzione dell'area client invalidata, a causa di un'azione, ad esempio il ridimensionamento di una finestra o la modifica dell'aspetto visivo di un oggetto.  
  
 ![Diagramma della sequenza di rendering Win32](./media/wpf-graphics-rendering-overview/win32-rendering-squence.png)  
  
 Al contrario, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usa un sistema in modalità differita. Questo significa che gli oggetti applicazione che hanno un aspetto visivo definiscono un set di dati di disegno serializzato. Dopo aver definito i dati di disegno, il sistema è responsabile della successiva risposta a tutte le richieste di aggiornamento per il rendering degli oggetti applicazione. Anche in fase di esecuzione, è possibile modificare o creare oggetti applicazione e affidarsi al sistema per rispondere alle richieste di aggiornamento. Il punto forte di un sistema di grafica in modalità differita è che le informazioni sul disegno vengono sempre salvate in modo permanente in uno stato serializzato dall'applicazione, ma la responsabilità del rendering viene lasciata al sistema. Il diagramma seguente mostra come l'applicazione si basa su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per rispondere alle richieste di aggiornamento.  
  
 ![Diagramma della sequenza di rendering WPF](./media/wpf-graphics-rendering-overview/wpf-rendering-sequence.png)  

#### <a name="intelligent-redrawing"></a>Ridisegno intelligente  
 Uno dei maggiori vantaggi nell'uso della grafica in modalità differita è che [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] può ottimizzare in modo efficace ciò che deve essere ridisegnato nell'applicazione. Anche se si ha a che fare con una scena complessa con livelli di opacità variabili, in genere non è necessario scrivere un codice specifico per ottimizzare il ridisegno. Confrontare questo aspetto con la programmazione Win32 in cui può succedere di dedicare un notevole impegno per ottimizzare l'applicazione riducendo al minimo la quantità di ridisegno nell'area di aggiornamento. Vedere [Ridisegno nell'area di aggiornamento](/windows/desktop/gdi/redrawing-in-the-update-region) per un esempio del tipo di complessità inclusa nell'ottimizzazione del ridisegno nelle applicazioni Win32.  
  
### <a name="vector-graphics"></a>Grafica vettoriale  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] usa la **grafica vettoriale** come formato per i dati di rendering. Le immagini vettoriali, che includono Scalable Vector Graphics (con estensione svg), Windows Metafile (con estensione wmf) e i tipi di carattere TrueType, archiviano i dati di rendering e li trasmettono come un elenco di istruzioni che descrivono come ricreare un'immagine mediante primitive grafiche. I tipi di carattere TrueType sono ad esempio caratteri vettoriali che descrivono un set di linee, curve e comandi, anziché una matrice di pixel. Uno dei principali vantaggi della grafica vettoriale è la possibilità di adattarsi a qualsiasi dimensione e risoluzione.  
  
 A differenza delle immagini vettoriali, le immagini bitmap archiviano i dati di rendering come rappresentazione pixel per pixel di un'immagine, di cui è stato eseguito il pre-rendering per una risoluzione specifica. Una delle differenze principali tra i formati di immagini bitmap e vettoriali è la fedeltà all'immagine originale. Quando ad esempio viene modificata la dimensione di un'immagine di origine, i sistemi di grafica bitmap allungano l'immagine, mentre i sistemi di grafica vettoriale la ridimensionano, conservandone la fedeltà.  
  
 La figura seguente illustra un'immagine di origine che è stata ridimensionata del 300%. Si notino le distorsioni visualizzate quando l'immagine di origine viene allungata come immagine bitmap anziché ridimensionata come immagine vettoriale.  
  
 ![Differenze tra grafica raster e vettoriale](./media/wpf-graphics-rendering-overview/raster-vector-differences.png)  
  
 Il markup seguente <xref:System.Windows.Shapes.Path> mostra due elementi definiti. Il secondo elemento <xref:System.Windows.Media.ScaleTransform> utilizza un per ridimensionare le istruzioni di disegno del primo elemento del 300%. Si noti che <xref:System.Windows.Shapes.Path> le istruzioni di disegno negli elementi rimangono invariate.  
  
 [!code-xaml[VectorGraphicsSnippets#VectorGraphicsSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VectorGraphicsSnippets/CS/PageOne.xaml#vectorgraphicssnippet1)]  
  
### <a name="about-resolution-and-device-independent-graphics"></a>Informazioni sulla grafica indipendente dalla risoluzione e dal dispositivo  
 Esistono due fattori di sistema che determinano la dimensione del testo e della grafica sullo schermo: risoluzione e DPI. La risoluzione indica il numero di pixel visualizzati sullo schermo. Con l'aumento della risoluzione i pixel vengono rimpiccioliti, con la conseguente riduzione della dimensione di grafica e testo. Un'immagine visualizzata su un monitor impostato su 1024 x 768 apparirà molto più piccola quando viene modificata la risoluzione in 1600 x 1200.  
  
 L'altra impostazione di sistema, DPI, descrive le dimensioni di un pollice di schermo in pixel. La maggior parte dei sistemi Windows ha un Valore DPI di 96, il che significa che un pollice dello schermo è 96 pixel. Se si aumenta l'impostazione DPI il pollice di schermo diventa più grande; se si diminuisce, il pollice di schermo diventa più piccolo. Ciò significa che, nella maggior parte dei sistemi, un pollice di schermo non ha le stesse dimensioni di un pollice reale. Quando si aumenta il valore DPI, il testo e la grafica compatibili con DPI diventano più grandi poiché viene aumentata la dimensione del pollice di schermo. L'aumento del valore DPI può rendere il testo più leggibile, soprattutto a risoluzioni elevate.  
  
 Non tutte le applicazioni sono compatibili con il valore DPI: alcune usano i pixel hardware come unità di misura primaria. La modifica del valore DPI di sistema non ha alcun effetto su tali applicazioni. Molte altre applicazioni usano unità compatibili con DPI per descrivere le dimensioni dei tipi di carattere, ma usano i pixel per descrivere tutto il resto. L'eccessiva riduzione o l'eccessivo aumento del valore DPI può causare problemi di layout per queste applicazioni, poiché il testo delle applicazioni viene ridimensionato con l'impostazione DPI del sistema, ma non l'interfaccia utente. Questo problema è stato eliminato per le applicazioni sviluppate usando [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] supporta il ridimensionamento automatico usando il pixel indipendente dal dispositivo come unità di misura primaria, anziché i pixel hardware. La grafica e il testo vengono ridimensionati correttamente senza operazioni aggiuntive da parte dello sviluppatore dell'applicazione. La figura seguente illustra un esempio di come vengono visualizzati la grafica e il testo di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] con impostazioni DPI diverse.  
  
 ![Grafica e testo con impostazioni DPI diverse](./media/graphicsmm-dpi-setting-examples.png "graphicsmm_dpi_setting_examples")  
Grafica e testo con impostazioni DPI diverse  
  
<a name="visualtreehelper_class"></a>
## <a name="visualtreehelper-class"></a>Classe VisualTreeHelper  
 La <xref:System.Windows.Media.VisualTreeHelper> classe è una classe helper statica che fornisce funzionalità di basso livello per la programmazione a livello di oggetto visivo, che è utile in scenari molto specifici, ad esempio lo sviluppo di controlli personalizzati ad alte prestazioni. Nella maggior parte dei [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] casi, gli <xref:System.Windows.Controls.Canvas> oggetti <xref:System.Windows.Controls.TextBlock>framework di livello superiore, ad esempio e , offrono maggiore flessibilità e facilità d'uso.  
  
### <a name="hit-testing"></a>Hit Testing  
 La <xref:System.Windows.Media.VisualTreeHelper> classe fornisce metodi per l'hit testing sugli oggetti visivi quando il supporto dell'hit test predefinito non soddisfa le proprie esigenze. È possibile <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> utilizzare i <xref:System.Windows.Media.VisualTreeHelper> metodi nella classe per determinare se un valore di coordinata geometrica o punto si trova all'interno del limite di un determinato oggetto, ad esempio un controllo o un elemento grafico. È ad esempio possibile usare l'hit testing per stabilire se un clic del mouse all'interno del rettangolo delimitatore di un oggetto rientra nella geometria di un cerchio. È anche possibile scegliere di eseguire l'override dell'implementazione predefinita dell'hit testing per eseguire calcoli di hit testing personalizzati.  
  
 Per altre informazioni sull'hit testing, vedere [Hit testing a livello visivo](hit-testing-in-the-visual-layer.md).  
  
### <a name="enumerating-the-visual-tree"></a>Enumerazione della struttura ad albero visuale  
 La <xref:System.Windows.Media.VisualTreeHelper> classe fornisce funzionalità per l'enumerazione dei membri di una struttura ad albero visuale. Per recuperare un elemento <xref:System.Windows.Media.VisualTreeHelper.GetParent%2A> padre, chiamare il metodo . Per recuperare un elemento figlio, o discendente <xref:System.Windows.Media.VisualTreeHelper.GetChild%2A> diretto, di un oggetto visivo, chiamare il metodo . Questo metodo restituisce un elemento figlio <xref:System.Windows.Media.Visual> dell'elemento padre in corrispondenza dell'indice specificato.  
  
 L'esempio seguente illustra come enumerare tutti i discendenti di un oggetto visivo. Si tratta di una tecnica da usare se si desidera serializzare tutte le informazioni di rendering di una gerarchia di oggetti visivi.  
  
 [!code-csharp[VisualsOverview#101](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#101)]
 [!code-vb[VisualsOverview#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#101)]  
  
 Nella maggior parte dei casi, l'albero logico è una rappresentazione più utile degli elementi di un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Sebbene l'albero logico non venga modificato direttamente, la visualizzazione dell'applicazione è utile per comprendere l'ereditarietà delle proprietà e il routing degli eventi. A differenza della struttura ad albero visuale, l'albero logico può rappresentare oggetti dati non visivi, ad <xref:System.Windows.Documents.ListItem>esempio . Per altre informazioni sull'albero logico, vedere [Strutture ad albero in WPF](../advanced/trees-in-wpf.md).  
  
 La <xref:System.Windows.Media.VisualTreeHelper> classe fornisce metodi per restituire il rettangolo di delimitazione degli oggetti visivi. È possibile restituire il rettangolo di <xref:System.Windows.Media.VisualTreeHelper.GetContentBounds%2A>delimitazione di un oggetto visivo chiamando . È possibile restituire il rettangolo di delimitazione di tutti i discendenti <xref:System.Windows.Media.VisualTreeHelper.GetDescendantBounds%2A>di un oggetto visivo, incluso l'oggetto visivo stesso, chiamando . Il codice seguente illustra come calcolare il rettangolo delimitatore di un oggetto visivo e di tutti i relativi discendenti.  
  
 [!code-csharp[VisualsOverview#102](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#102)]
 [!code-vb[VisualsOverview#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#102)]  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Media.Visual>
- <xref:System.Windows.Media.VisualTreeHelper>
- <xref:System.Windows.Media.DrawingVisual>
- [Grafica 2D e creazione di immagini](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [Hit testing a livello visivo](hit-testing-in-the-visual-layer.md)
- [Utilizzo degli oggetti DrawingVisual](using-drawingvisual-objects.md)
- [Esercitazione: Hosting di oggetti visivi in un'applicazione Win32](tutorial-hosting-visual-objects-in-a-win32-application.md)
- [Ottimizzazione delle prestazioni di applicazioni WPF](../advanced/optimizing-wpf-application-performance.md)

---
title: Introduzione a WPF
titleSuffix: ''
description: Crea esperienze utente visivamente accattivanti in Windows. Scopri le funzionalità e i concetti chiave di Windows Presentation Foundation (WPF).
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: b8d7cf43-d1f2-4f3d-adb0-4f3a6428edc0
dev_langs:
- csharp
- vb
ms.openlocfilehash: 7a79174f5f3aebe90190db45566b37bd5e9fbe3f
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853582"
---
# <a name="wpf-overview"></a>Panoramica di WPF

Windows Presentation Foundation (WPF) consente di creare applicazioni client desktop per Windows capaci di offrire all'utente un'esperienza visiva sorprendente.

![Esempio di interfaccia utente Contoso Healthcare](media/introduction-to-wpf/wpfintrofigure24.png)

L'elemento principale di WPF è un motore di rendering vettoriale e indipendente dalla risoluzione compilato per sfruttare i vantaggi dei moderni componenti hardware grafici. Oltre a questo elemento principale, WPF offre un set completo di funzionalità per lo sviluppo di applicazioni che includono Extensible Application Markup Language (XAML), controlli, data binding, layout, grafica 2D e 3D, animazioni, stili, modelli, documenti, supporti, testo e tipografia. WPF fa parte di .NET e, pertanto, è possibile compilare applicazioni che incorporano altri elementi dell'API .NET.

Questa panoramica, destinata ai principianti, illustra le funzionalità e i concetti chiave di WPF.

## <a name="program-with-wpf"></a>Programmazione con WPF

WPF è un subset di tipi di .NET in gran parte contenuti nello spazio dei nomi <xref:System.Windows>. Se in precedenza si sono già compilate applicazioni con .NET usando tecnologie gestite come ASP.NET e Windows Forms, si è già acquisita familiarità con le operazioni fondamentali di programmazione WPF. È possibile creare istanze di classi, impostare proprietà, chiamare metodi e gestire eventi usando il linguaggio di programmazione .NET preferito, ad esempio C# o Visual Basic.

WPF include costrutti di programmazione aggiuntivi che migliorano proprietà ed eventi: [proprietà di dipendenza](advanced/dependency-properties-overview.md) ed [eventi indirizzati](advanced/routed-events-overview.md).

## <a name="markup-and-code-behind"></a>Markup e code-behind

WPF consente di sviluppare applicazioni usando sia *markup* sia *code-behind*, un'esperienza nota agli sviluppatori ASP.NET. Il markup XAML viene normalmente usato per implementare l'aspetto di un'applicazione, mentre i linguaggi di programmazione gestiti (code-behind) vengono usati per implementarne il comportamento. La separazione tra aspetto e comportamento offre alcuni vantaggi:

- I costi di sviluppo e gestione risultano ridotti, perché il markup specifico per l'aspetto non è associato strettamente a codice specifico per il comportamento.

- Lo sviluppo è più efficiente, perché i progettisti possono implementare l'aspetto di un'applicazione mentre, contemporaneamente, gli sviluppatori ne implementano il comportamento.

- Le operazioni di[globalizzazione e localizzazione](advanced/wpf-globalization-and-localization-overview.md) delle applicazioni WPF sono state semplificate.

### <a name="markup"></a>markup

XAML è un linguaggio di markup basato su XML che implementa l'aspetto di un'applicazione in modo dichiarativo. Viene in genere usato per creare finestre, finestre di dialogo, pagine e controlli utente e per inserire in questi elementi controlli, forme e grafica.

Nell'esempio seguente viene usato XAML per implementare l'aspetto di una finestra che contiene un singolo pulsante:

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    Title="Window with Button"
    Width="250" Height="100">

  <!-- Add button to window -->
  <Button Name="button">Click Me!</Button>

</Window>
```

In particolare, questo codice XAML definisce una finestra e un pulsante con gli elementi `Window` e `Button` , rispettivamente. Ogni elemento viene configurato con attributi, ad esempio l'attributo `Window` dell'elemento `Title` per specificare il testo della barra del titolo della finestra. In fase di esecuzione, WPF converte gli elementi e gli attributi definiti nel markup in istanze di classi WPF. Ad esempio, l'elemento `Window` viene convertito in un'istanza della classe <xref:System.Windows.Window> la cui proprietà <xref:System.Windows.Window.Title%2A> è il valore dell'attributo `Title` .

Nella figura seguente viene illustrata l'interfaccia utente (UI) definita da XAML nell'esempio precedente:

![Finestra contenente un pulsante](media/introduction-to-wpf/wpfintrofigure10.png)

Poiché XAML è basato su XML, l'interfaccia utente composta con tale linguaggio viene assemblata in una gerarchia di elementi annidati nota come [struttura ad albero di elementi](advanced/trees-in-wpf.md). Questa struttura ad albero di elementi costituisce un modo logico e intuitivo per creare e gestire le interfacce utente.

### <a name="code-behind"></a>Code-behind

Il comportamento principale di un'applicazione consiste nell'implementare la funzionalità che risponde alle interazioni dell'utente, inclusa la gestione di eventi (ad esempio la scelta di un menu, una barra degli strumenti o un pulsante) e la chiamata alla logica di business e alla logica di accesso ai dati in risposta a tali eventi. In WPF questo comportamento viene in genere implementato in codice associato a markup. Questo tipo di codice è noto come code-behind. L'esempio seguente illustra il markup aggiornato dell'esempio precedente e il code-behind:

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.AWindow"
    Title="Window with Button"
    Width="250" Height="100">

  <!-- Add button to window -->
  <Button Name="button" Click="button_Click">Click Me!</Button>

</Window>
```

```csharp
using System.Windows; // Window, RoutedEventArgs, MessageBox

namespace SDKSample
{
    public partial class AWindow : Window
    {
        public AWindow()
        {
            // InitializeComponent call is required to merge the UI
            // that is defined in markup with this class, including  
            // setting properties and registering event handlers
            InitializeComponent();
        }

        void button_Click(object sender, RoutedEventArgs e)
        {
            // Show message box when button is clicked.
            MessageBox.Show("Hello, Windows Presentation Foundation!");
        }
    }
}
```

```vb
Namespace SDKSample

    Partial Public Class AWindow
        Inherits System.Windows.Window

        Public Sub New()

            ' InitializeComponent call is required to merge the UI
            ' that is defined in markup with this class, including  
            ' setting properties and registering event handlers
            InitializeComponent()

        End Sub

        Private Sub button_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)

            ' Show message box when button is clicked.
            MessageBox.Show("Hello, Windows Presentation Foundation!")

        End Sub

    End Class

End Namespace
```

In questo esempio il code-behind implementa una classe che deriva dalla classe <xref:System.Windows.Window> . L'attributo `x:Class` viene usato per associare il markup alla classe code-behind. `InitializeComponent` viene chiamato dal costruttore della classe code-behind per unire l'interfaccia utente definita nel markup con la classe code-behind. `InitializeComponent`viene generato automaticamente quando viene compilata l'applicazione, motivo per cui non è necessario implementarla manualmente. La combinazione di `x:Class` e `InitializeComponent` assicura che l'implementazione venga inizializzata correttamente ogni volta che viene creata. La classe code-behind implementa anche un gestore dell'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> del pulsante. Quando si fa clic sul pulsante, il gestore eventi mostra una finestra di messaggio chiamando il metodo <xref:System.Windows.MessageBox.Show%2A?displayProperty=fullName> .

La figura seguente mostra il risultato quando si fa clic sul pulsante:

![MessageBox](media/introduction-to-wpf/wpfintrofigure25.png)

## <a name="controls"></a>Controlli

Le esperienze utente fornite dal modello di applicazione sono controlli costruiti. In WPF, *controllo* è un termine generico che si applica a una categoria di classi WPF ospitate in una finestra o una pagina, che hanno un'interfaccia utente e che implementano un comportamento.

Per altre informazioni, vedere [Controlli](controls/index.md).

### <a name="wpf-controls-by-function"></a>Controlli WPF per funzione

I controlli WPF incorporati sono elencati di seguito:

- **Pulsanti**: <xref:System.Windows.Controls.Button> e <xref:System.Windows.Controls.Primitives.RepeatButton> .

- **Visualizzazione dei dati**: <xref:System.Windows.Controls.DataGrid> , <xref:System.Windows.Controls.ListView> e <xref:System.Windows.Controls.TreeView> .

- **Visualizzazione e selezione di date**: <xref:System.Windows.Controls.Calendar> e <xref:System.Windows.Controls.DatePicker> .

- **Finestre di dialogo**: <xref:Microsoft.Win32.OpenFileDialog> , <xref:System.Windows.Controls.PrintDialog> e <xref:Microsoft.Win32.SaveFileDialog> .

- **Input penna digitale**: <xref:System.Windows.Controls.InkCanvas> e <xref:System.Windows.Controls.InkPresenter> .

- **Documenti**: <xref:System.Windows.Controls.DocumentViewer> , <xref:System.Windows.Controls.FlowDocumentPageViewer> , <xref:System.Windows.Controls.FlowDocumentReader> , <xref:System.Windows.Controls.FlowDocumentScrollViewer> e <xref:System.Windows.Controls.StickyNoteControl> .

- **Input**: <xref:System.Windows.Controls.TextBox> , <xref:System.Windows.Controls.RichTextBox> e <xref:System.Windows.Controls.PasswordBox> .

- **Layout**: <xref:System.Windows.Controls.Border> , <xref:System.Windows.Controls.Primitives.BulletDecorator> , <xref:System.Windows.Controls.Canvas> , <xref:System.Windows.Controls.DockPanel> , <xref:System.Windows.Controls.Expander> , <xref:System.Windows.Controls.Grid> , <xref:System.Windows.Controls.GridView> , <xref:System.Windows.Controls.GridSplitter> , <xref:System.Windows.Controls.GroupBox> , <xref:System.Windows.Controls.Panel> , <xref:System.Windows.Controls.Primitives.ResizeGrip> , <xref:System.Windows.Controls.Separator> , <xref:System.Windows.Controls.Primitives.ScrollBar> , <xref:System.Windows.Controls.ScrollViewer> , <xref:System.Windows.Controls.StackPanel> , <xref:System.Windows.Controls.Primitives.Thumb> , <xref:System.Windows.Controls.Viewbox> , <xref:System.Windows.Controls.VirtualizingStackPanel> , <xref:System.Windows.Window> e <xref:System.Windows.Controls.WrapPanel> .

- **Supporti**: <xref:System.Windows.Controls.Image> , <xref:System.Windows.Controls.MediaElement> e <xref:System.Windows.Controls.SoundPlayerAction> .

- **Menu**: <xref:System.Windows.Controls.ContextMenu> , <xref:System.Windows.Controls.Menu> e <xref:System.Windows.Controls.ToolBar> .

- **Navigazione**: <xref:System.Windows.Controls.Frame> , <xref:System.Windows.Documents.Hyperlink> , <xref:System.Windows.Controls.Page> , <xref:System.Windows.Navigation.NavigationWindow> e <xref:System.Windows.Controls.TabControl> .

- **Selezione**: <xref:System.Windows.Controls.CheckBox> , <xref:System.Windows.Controls.ComboBox> , <xref:System.Windows.Controls.ListBox> , <xref:System.Windows.Controls.RadioButton> e <xref:System.Windows.Controls.Slider> .

- **Informazioni utente**: <xref:System.Windows.Controls.AccessText> , <xref:System.Windows.Controls.Label> , <xref:System.Windows.Controls.Primitives.Popup> , <xref:System.Windows.Controls.ProgressBar> , <xref:System.Windows.Controls.Primitives.StatusBar> , <xref:System.Windows.Controls.TextBlock> e <xref:System.Windows.Controls.ToolTip> .

## <a name="input-and-commands"></a>Input e comandi

I controlli nella maggior parte dei casi rilevano e rispondono all'input dell'utente. Il [sistema di input di WPF](advanced/input-overview.md) usa eventi sia diretti sia indirizzati per supportare l'input di testo, la gestione dello stato attivo e il posizionamento del mouse.

I requisiti di input delle applicazioni sono spesso complessi. In WPF è disponibile un [sistema di comandi](advanced/commanding-overview.md) che separa le azioni di input utente dal codice che risponde a tali azioni.

## <a name="layout"></a>Layout

Quando si crea un'interfaccia utente, si dispongono i controlli per percorso e dimensione per creare un layout. Il requisito principale di qualsiasi layout è quello di adattarsi alle modifiche nella dimensione delle finestre e nelle impostazioni di visualizzazione. Anziché richiedere la scrittura di codice per adattare un layout in tali circostanze, WPF offre un efficiente sistema di layout estendibile.

L'elemento fondamentale del sistema di layout è il posizionamento relativo che aumenta la capacità di adattamento a condizioni di finestre e visualizzazione mutevoli. Il sistema di layout gestisce inoltre la negoziazione tra i controlli per determinare il layout. La negoziazione è un processo a due fasi in cui innanzitutto un controllo indica il percorso e le dimensioni richieste alla relativa entità principale, quindi l'entità principale indica lo spazio disponibile al controllo.

Il sistema di layout viene esposto ai controlli figlio tramite le classi base di WPF. Per layout comuni, ad esempio griglie, sovrapposizioni e ancoraggio, WPF include vari controlli di layout:

- <xref:System.Windows.Controls.Canvas>: i controlli figlio forniscono il proprio layout.

- <xref:System.Windows.Controls.DockPanel>: i controlli figlio sono allineati ai bordi del pannello.

- <xref:System.Windows.Controls.Grid>: i controlli figlio sono posizionati per righe e colonne.

- <xref:System.Windows.Controls.StackPanel>: i controlli figlio sono sovrapposti in verticale o in orizzontale.

- <xref:System.Windows.Controls.VirtualizingStackPanel>: i controlli figlio sono virtualizzati e disposti su una sola riga orientata in senso orizzontale o verticale.

- <xref:System.Windows.Controls.WrapPanel>: i controlli figlio sono posizionati in ordine da sinistra a destra e mandati a capo quando sulla riga corrente sono presenti troppi controlli rispetto allo spazio disponibile.

Nell'esempio seguente viene usato un oggetto <xref:System.Windows.Controls.DockPanel> per disporre diversi <xref:System.Windows.Controls.TextBox> Controlli:

[!code-xaml[IntroToWPFSnippets#LayoutMARKUP](~/samples/snippets/xaml/wpf/introduction-to-wpf/introduction-to-wpf_1.xaml)]

<xref:System.Windows.Controls.DockPanel> consente ai controlli <xref:System.Windows.Controls.TextBox> figlio di indicare la modalità di disposizione. A tale scopo, <xref:System.Windows.Controls.DockPanel> implementa una proprietà associata `Dock` esposta ai controlli figlio per consentire a ognuno di essi di specificare uno stile di ancoraggio.

> [!NOTE]
> Una proprietà implementata da un controllo padre per essere usata dai controlli figlio è un costrutto di WPF denominato [proprietà associata](advanced/attached-properties-overview.md).

La figura seguente illustra il risultato del markup XAML nell'esempio precedente:

![Pagina DockPanel](media/introduction-to-wpf/wpfintrofigure11.png)

## <a name="data-binding"></a>Associazione dati

La maggior parte delle applicazioni viene creata per consentire agli utenti di visualizzare e modificare i dati. Per le applicazioni WPF, le operazioni di archiviazione e accesso ai dati sono fornite da tecnologie quali SQL Server e ADO.NET. Dopo l'accesso ai dati e il loro caricamento negli oggetti gestiti di un'applicazione, ha inizio la fase più complessa delle applicazioni WPF. Questa fase comporta essenzialmente due punti:

1. Copia dei dati dagli oggetti gestiti ai controlli, per consentirne la visualizzazione e la modifica.

2. Verifica che le modifiche apportate ai dati usando i controlli vengano copiate negli oggetti gestiti.

Per semplificare lo sviluppo delle applicazioni, in WPF è disponibile un motore di data binding per eseguire automaticamente queste operazioni. L'unità principale di questo motore è la classe <xref:System.Windows.Data.Binding> , il cui scopo è associare un controllo (destinazione) a un oggetto dati (origine). La figura seguente illustra questa relazione:

![Diagramma di associazione dati di base](media/introduction-to-wpf/databindingmostbasic.png)

L'esempio seguente descrive come associare un oggetto <xref:System.Windows.Controls.TextBox> a un'istanza di un oggetto `Person` personalizzato. L'esempio di codice seguente mostra l'implementazione di `Person`:

[!code-vb[SimpleDataBindingSnippets#PersonClassCODE](~/samples/snippets/visualbasic/wpf/introduction-to-wpf/introduction-to-wpf_2.vb)]
[!code-csharp[SimpleDataBindingSnippets#PersonClassCODE](~/samples/snippets/csharp/wpf/introduction-to-wpf/introduction-to-wpf_2.cs)]

Il markup seguente associa <xref:System.Windows.Controls.TextBox> a un'istanza di un `Person` oggetto personalizzato:

```xaml
 <Window
     xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
     xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
     x:Class="SDKSample.DataBindingWindow">

   <!-- Bind the TextBox to the data source (TextBox.Text to Person.Name) -->
   <TextBox Name="personNameTextBox" Text="{Binding Path=Name}" />

 </Window>
```

[!code-vb[SimpleDataBindingSnippets#DataBindingCODEBEHIND](~/samples/snippets/visualbasic/wpf/introduction-to-wpf/introduction-to-wpf_6.vb)]
[!code-csharp[SimpleDataBindingSnippets#DataBindingCODEBEHIND](~/samples/snippets/csharp/wpf/introduction-to-wpf/introduction-to-wpf_6.cs)]

In questo esempio viene creata un'istanza della classe `Person` in code-behind e viene impostata come contesto dei dati per l'oggetto `DataBindingWindow`. Nel markup la proprietà <xref:System.Windows.Controls.TextBox.Text%2A> dell'oggetto <xref:System.Windows.Controls.TextBox> è associata alla proprietà `Person.Name` per mezzo della sintassi XAML "`{Binding ... }`". Questo codice XAML comunica a WPF di associare il controllo <xref:System.Windows.Controls.TextBox> all'oggetto `Person` archiviato nella proprietà <xref:System.Windows.FrameworkElement.DataContext%2A> della finestra.

Il motore di data binding di WPF offre supporto aggiuntivo che include convalida, ordinamento, filtro e raggruppamento. Il data binding supporta anche l'uso di modelli di dati per creare un'interfaccia utente personalizzata per i dati associati quando l'interfaccia utente visualizzata dai controlli WPF standard non è adatta.

Per altre informazioni, vedere [Cenni preliminari sul data binding](../../desktop-wpf/data/data-binding-overview.md).

## <a name="graphics"></a>Grafica

In WPF è disponibile un set completo, scalabile e flessibile di funzionalità grafiche che offrono i vantaggi seguenti:

- **Grafica indipendente dalla risoluzione e dal dispositivo**. L'unità di misura di base nel sistema grafico di WPF è il Device Independent Pixel, pari a 1/96 di pollice, indipendentemente dall'effettiva risoluzione dello schermo, che costituisce la base per il rendering indipendente dalla risoluzione e dal dispositivo. Ogni Device Independent Pixel viene ridimensionato automaticamente in modo da corrispondere all'impostazione in punti per pollice (dpi) del sistema in cui viene eseguito il rendering.

- **Maggiore precisione**. Il sistema di coordinate WPF viene misurato con numeri a virgola mobile a precisione doppia anziché a precisione singola. Anche i valori di opacità e delle trasformazioni vengono espressi come precisione doppia. WPF supporta anche un'ampia gamma di colori (scRGB) e offre il supporto integrato per la gestione di input da spazi colore diversi.

- **Grafica e supporto dell'animazione avanzati**. WPF semplifica la programmazione grafica. Grazie alla gestione automatica delle scene di animazione, infatti, non occorre preoccuparsi dell'elaborazione delle scene, dei cicli di rendering e dell'interpolazione bilineare. In WPF è anche disponibile il supporto per hit testing e composizione alfa completa.

- **Accelerazione hardware**. Il sistema grafico di WPF sfrutta i vantaggi dei componenti hardware grafici per ridurre al minimo l'uso della CPU.

### <a name="2d-shapes"></a>Forme 2D

In WPF è disponibile una libreria di forme 2D comuni disegnate da vettori, ad esempio i rettangoli e le ellissi mostrati nella figura seguente:

![Ellissi e rettangoli](media/introduction-to-wpf/wpfintrofigure4.PNG)

La caratteristica interessante delle forme è che non vengono usate solo per la visualizzazione. Le forme, infatti, implementano molte delle funzionalità fornite dai controlli, incluso l'input della tastiera e del mouse. Nell'esempio seguente viene illustrato l' <xref:System.Windows.UIElement.MouseUp> evento di un oggetto <xref:System.Windows.Shapes.Ellipse> gestito:

[!code-xaml[IntroToWPFSnippets#HandleEllipseMouseUpEventMARKUP](~/samples/snippets/xaml/wpf/introduction-to-wpf/introduction-to-wpf_7.xaml)]

[!code-vb[IntroToWPFSnippets#HandleEllipseMouseUpEventCODEBEHIND](~/samples/snippets/visualbasic/wpf/introduction-to-wpf/introduction-to-wpf_8.vb)]
[!code-csharp[IntroToWPFSnippets#HandleEllipseMouseUpEventCODEBEHIND](~/samples/snippets/csharp/wpf/introduction-to-wpf/introduction-to-wpf_8.cs)]

Nella figura seguente viene illustrato ciò che viene prodotto dal codice precedente:

![Finestra con il testo "you clicked the ellipse&#33;"](media/introduction-to-wpf/wpfintrofigure12.png)

Per altre informazioni, vedere [Cenni preliminari sulle forme e il disegno di base in WPF](../../desktop-wpf/data/data-binding-overview.md).

### <a name="2d-geometries"></a>Geometrie 2D

Le forme 2D disponibili in WPF coprono il set standard di forme di base. Può tuttavia essere necessario creare forme personalizzate per semplificare la progettazione di un'interfaccia utente personalizzata. A questo scopo, in WPF sono disponibili le geometrie. La figura seguente illustra come usare le geometrie per creare una forma personalizzata che può essere disegnata direttamente o usata come pennello o per ritagliare altre forme e controlli.

Gli oggetti<xref:System.Windows.Shapes.Path> possono essere usati per disegnare forme chiuse o aperte, più forme e anche forme curve.

Gli oggetti <xref:System.Windows.Media.Geometry> possono essere usati per ritagliare ed eseguire hit testing e rendering di dati grafici 2D.

![Vari usi di un percorso](media/introduction-to-wpf/wpfintrofigure5.png)

Per altre informazioni, vedere [Cenni preliminari sulle classi Geometry](graphics-multimedia/geometry-overview.md).

### <a name="2d-effects"></a>Effetti 2D

Un subset di funzionalità 2D di WPF include effetti visivi, ad esempio sfumature, bitmap, disegni, disegni con video, rotazione, ridimensionamento e inclinazione. Si ottengono tutti con pennelli; nella figura seguente vengono illustrati alcuni esempi:

![Illustrazione di pennelli diversi](media/introduction-to-wpf/wpfintrofigure6.png)

Per altre informazioni, vedere [Cenni preliminari sui pennelli di WPF](graphics-multimedia/wpf-brushes-overview.md).

### <a name="3d-rendering"></a>Rendering 3D

WPF include anche funzionalità di rendering 3D che si integrano con la grafica 2D per consentire la creazione di interfacce utente più interessanti e interessanti. Ad esempio, la figura seguente mostra le immagini 2D sottoposte a rendering su forme 3D:

![Schermata dell'esempio Visual3D](media/introduction-to-wpf/wpfintrofigure13.png)

Per altre informazioni, vedere [Cenni preliminari sulla grafica tridimensionale](graphics-multimedia/3-d-graphics-overview.md).

## <a name="animation"></a>Animazione

Il supporto di animazione di WPF consente di fare crescere, muovere, ruotare e dissolvere i controlli per creare interessanti transizioni di pagina e altro ancora. È possibile animare la maggior parte delle classi WPF, anche quelle personalizzate. Nella figura seguente viene illustrata un'animazione semplice in azione:

![Immagini di un cubo animato](media/introduction-to-wpf/wpfintrofigure7.png)

Per altre informazioni, vedere [Cenni preliminari sull'animazione](graphics-multimedia/animation-overview.md).

## <a name="media"></a>Contenuti multimediali

L'uso di supporti audiovisivi è un modo per inserire contenuto dettagliato. WPF offre un supporto speciale per immagini, video e audio.

### <a name="images"></a>Immagini

Le immagini sono comuni alla maggior parte delle applicazioni e in WPF possono essere usate in diversi modi. La figura seguente illustra un'interfaccia utente con una casella di riepilogo che contiene immagini di anteprima. Quando si seleziona un'anteprima, l'immagine viene visualizzata ingrandita.

![Immagini di anteprima e con le dimensioni originali](media/introduction-to-wpf/wpfintrofigure8.png)

Per altre informazioni, vedere [Cenni preliminari sulla creazione dell'immagine](graphics-multimedia/imaging-overview.md).

### <a name="video-and-audio"></a>Video e audio

Il controllo <xref:System.Windows.Controls.MediaElement> consente di riprodurre video e audio e, grazie alle caratteristiche di flessibilità, può essere usato come base per un lettore multimediale personalizzato. Il markup XAML seguente implementa un lettore multimediale:

[!code-xaml[IntroToWPFSnippets#MediaElementMARKUP](~/samples/snippets/xaml/wpf/introduction-to-wpf/introduction-to-wpf_9.xaml)]

La finestra nella figura seguente illustra il <xref:System.Windows.Controls.MediaElement> controllo in azione:

![Controllo MediaElement con audio e video](media/introduction-to-wpf/wpfintrofigure1.png)

Per altre informazioni, vedere [Grafica e funzionalità multimediali](graphics-multimedia/index.md).

## <a name="text-and-typography"></a>Testo e tipografia

Per semplificare il rendering di testo di alta qualità, WPF offre le funzionalità seguenti:

- Supporto dei tipi di carattere OpenType

- Miglioramenti di ClearType.

- Prestazioni elevate che sfruttano i vantaggi dell'accelerazione hardware.

- Integrazione del testo con elementi multimediali, grafica e animazione.

- Supporto dei tipi di carattere internazionali e meccanismi di fallback.

Come dimostrazione dell'integrazione del testo con la grafica, la figura seguente illustra l'applicazione di decorazioni di testo:

![Testo con varie decorazioni](media/introduction-to-wpf/wpfintrofigure23.png)

Per altre informazioni, vedere [Funzionalità tipografiche di WPF](advanced/typography-in-wpf.md).

## <a name="customize-wpf-apps"></a>Personalizzazione delle applicazioni WPF

Finora, sono stati presentati i blocchi di compilazione principali di WPF per lo sviluppo di applicazioni. Il modello di applicazione viene usato per ospitare e fornire contenuto di applicazione, costituito principalmente da controlli. Per semplificare la disposizione dei controlli in un'interfaccia utente e per mantenere tale disposizione anche in caso di modifiche alle dimensioni della finestra e alle impostazioni di visualizzazione, viene usato il sistema di layout di WPF. Poiché la maggior parte delle applicazioni consente agli utenti di interagire con i dati, per ridurre le operazioni di integrazione dell'interfaccia utente con i dati viene usato il data binding. Per migliorare l'aspetto visivo dell'applicazione, è possibile usare una gamma completa di grafica, animazione ed elementi multimediali disponibili in WPF.

Spesso, tuttavia, le funzionalità di base non sono sufficienti per creare e gestire applicazioni davvero uniche e visivamente sorprendenti per gli utenti. I controlli WPF standard potrebbero non integrarsi con l'aspetto desiderato dell'applicazione. I dati potrebbero non essere visualizzati nel modo più efficace. L'esperienza utente complessiva di un'applicazione può non essere adeguata all'aspetto dei temi di Windows. Per una tecnologia di presentazione è necessaria l'estendibilità visiva, tanto quanto altri tipi di estendibilità.

Per questo motivo, WPF offre una varietà di meccanismi per la creazione di esperienze utente univoche, incluso un modello di contenuto dettagliato per controlli, trigger, modelli di controllo e di dati, stili, risorse dell'interfaccia utente, temi e interfacce.

### <a name="content-model"></a>Modello di contenuto

Lo scopo principale di gran parte dei controlli di WPF è quello di visualizzare il contenuto. In WPF il tipo e il numero di elementi che possono costituire il contenuto di un controllo è indicato come *modello di contenuto*del controllo. Alcuni controlli possono contenere un solo elemento e tipo di contenuto. Ad esempio, il contenuto di un oggetto <xref:System.Windows.Controls.TextBox> è un valore stringa assegnato alla proprietà <xref:System.Windows.Controls.TextBox.Text%2A> . Nell'esempio seguente viene impostato il contenuto di un oggetto <xref:System.Windows.Controls.TextBox> :

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.TextBoxContentWindow"
    Title="TextBox Content">

    <TextBox Text="This is the content of a TextBox." />
</Window>
```

Nella figura seguente viene illustrato il risultato:

![Controllo TextBox contenente testo](media/introduction-to-wpf/wpfintrofigure21.png)

Gli altri controlli, tuttavia, possono contenere più elementi di tipi diversi di contenuto. Il contenuto di un oggetto <xref:System.Windows.Controls.Button>, specificato dalla proprietà <xref:System.Windows.Controls.ContentControl.Content%2A>, può contenere vari elementi, inclusi i controlli di layout, testo, immagini e forme. Nell'esempio seguente viene illustrato un oggetto <xref:System.Windows.Controls.Button> con contenuto che include un oggetto <xref:System.Windows.Controls.DockPanel> , un oggetto, un oggetto <xref:System.Windows.Controls.Label> <xref:System.Windows.Controls.Border> e un oggetto <xref:System.Windows.Controls.MediaElement> :

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.ButtonContentWindow"
    Title="Button Content">

  <Button Margin="20">
    <!-- Button Content -->
    <DockPanel Width="200" Height="180">
      <Label DockPanel.Dock="Top" HorizontalAlignment="Center">Click Me!</Label>
      <Border Background="Black" BorderBrush="Yellow" BorderThickness="2"
        CornerRadius="2" Margin="5">
        <MediaElement Source="media/wpf.wmv" Stretch="Fill" />
      </Border>
    </DockPanel>
  </Button>
</Window>
```

Nella figura seguente viene illustrato il contenuto di questo pulsante:

![Pulsante con più tipi di contenuto](media/introduction-to-wpf/wpfintrofigure22.png)

Per altre informazioni sui tipi di contenuto supportati dai vari controlli, vedere [Modello di contenuto WPF](controls/wpf-content-model.md).

### <a name="triggers"></a>Trigger

Anche se lo scopo principale del markup XAML consiste nell'implementare l'aspetto di un'applicazione, è anche possibile usare XAML per implementare alcuni aspetti del comportamento di un'applicazione. Un esempio è dato dall'uso dei trigger per modificare l'aspetto di un'applicazione in base alle interazioni dell'utente. Per altre informazioni, vedere [stili e modelli](../../desktop-wpf/fundamentals/styles-templates-overview.md).

### <a name="control-templates"></a>Modelli di controllo

Le interfacce utente predefinite per i controlli WPF sono in genere costituite da altri controlli e forme. Ad esempio, un oggetto <xref:System.Windows.Controls.Button> è composto da entrambi i controlli <xref:Microsoft.Windows.Themes.ButtonChrome> e <xref:System.Windows.Controls.ContentPresenter> . <xref:Microsoft.Windows.Themes.ButtonChrome> fornisce l'aspetto del pulsante standard, mentre <xref:System.Windows.Controls.ContentPresenter> consente di visualizzare il contenuto del pulsante, come specificato dalla proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> .

A volte l'aspetto predefinito di un controllo può non essere coerente con l'aspetto complessivo di un'applicazione. In tal caso, è possibile usare un oggetto <xref:System.Windows.Controls.ControlTemplate> per modificare l'aspetto dell'interfaccia utente del controllo senza modificarne il contenuto e il comportamento.

Nell'esempio seguente viene illustrato come modificare l'aspetto di un oggetto <xref:System.Windows.Controls.Button> utilizzando un oggetto <xref:System.Windows.Controls.ControlTemplate> :

[!code-xaml[IntroToWPFSnippets#ButtonControlTemplateWindowMARKUP](~/samples/snippets/xaml/wpf/introduction-to-wpf/introduction-to-wpf_16.xaml)]

[!code-csharp[IntroToWPFSnippets#ButtonControlTemplateWindowCODEBEHIND](~/samples/snippets/csharp/wpf/introduction-to-wpf/introduction-to-wpf_17.cs)]
[!code-vb[IntroToWPFSnippets#ButtonControlTemplateWindowCODEBEHIND](~/samples/snippets/visualbasic/wpf/introduction-to-wpf/introduction-to-wpf_17.vb)]

In questo esempio, l'interfaccia utente predefinita del pulsante è stata sostituita con un oggetto <xref:System.Windows.Shapes.Ellipse> che presenta un bordo blu scuro e viene riempito con un oggetto <xref:System.Windows.Media.RadialGradientBrush>. Il controllo <xref:System.Windows.Controls.ContentPresenter> consente di visualizzare il contenuto dell'oggetto <xref:System.Windows.Controls.Button>, "Click Me!". Quando si fa clic sull'oggetto <xref:System.Windows.Controls.Button> , viene comunque generato l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> come parte del comportamento predefinito del controllo <xref:System.Windows.Controls.Button> . Il risultato è illustrato nella figura seguente:

![Pulsante ellittico e una seconda finestra](media/introduction-to-wpf/wpfintrofigure2.png)

### <a name="data-templates"></a>Modelli di dati

Mentre un modello di controllo consente di specificare l'aspetto di un controllo, un modello di dati consente di specificare l'aspetto del contenuto di un controllo. I modelli di dati sono spesso usati per migliorare la modalità di visualizzazione dei dati associati. Nella figura seguente viene illustrato l'aspetto predefinito per un oggetto <xref:System.Windows.Controls.ListBox> associato a una raccolta di `Task` oggetti, dove ogni attività ha un nome, una descrizione e una priorità:

![Casella di riepilogo con aspetto predefinito](media/introduction-to-wpf/wpfintrofigure18.png)

L'aspetto predefinito è quello previsto per un oggetto <xref:System.Windows.Controls.ListBox>. L'aspetto predefinito di ciascuna attività, tuttavia, contiene solo il nome dell'attività. Per visualizzare il nome, la descrizione e la priorità di un'attività, è necessario modificare l'aspetto predefinito degli elementi elenco associati del controllo <xref:System.Windows.Controls.ListBox> usando un oggetto <xref:System.Windows.DataTemplate>. Il codice XAML seguente definisce un oggetto <xref:System.Windows.DataTemplate> , che viene applicato a ogni attività tramite l' <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> attributo:

```xaml
<Window
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  x:Class="SDKSample.DataTemplateWindow"
  Title="With a Data Template">
  <Window.Resources>
    <!-- Data Template (applied to each bound task item in the task collection) -->
    <DataTemplate x:Key="myTaskTemplate">
      <Border Name="border" BorderBrush="DarkSlateBlue" BorderThickness="2"
        CornerRadius="2" Padding="5" Margin="5">
        <Grid>
          <Grid.RowDefinitions>
            <RowDefinition/>
            <RowDefinition/>
            <RowDefinition/>
          </Grid.RowDefinitions>
          <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Auto" />
            <ColumnDefinition />
          </Grid.ColumnDefinitions>
          <TextBlock Grid.Row="0" Grid.Column="0" Padding="0,0,5,0" Text="Task Name:"/>
          <TextBlock Grid.Row="0" Grid.Column="1" Text="{Binding Path=TaskName}"/>
          <TextBlock Grid.Row="1" Grid.Column="0" Padding="0,0,5,0" Text="Description:"/>
          <TextBlock Grid.Row="1" Grid.Column="1" Text="{Binding Path=Description}"/>
          <TextBlock Grid.Row="2" Grid.Column="0" Padding="0,0,5,0" Text="Priority:"/>
          <TextBlock Grid.Row="2" Grid.Column="1" Text="{Binding Path=Priority}"/>
        </Grid>
      </Border>
    </DataTemplate>
  </Window.Resources>

  <!-- UI -->
  <DockPanel>
    <!-- Title -->
    <Label DockPanel.Dock="Top" FontSize="18" Margin="5" Content="My Task List:"/>

    <!-- Data template is specified by the ItemTemplate attribute -->
    <ListBox
      ItemsSource="{Binding}"
      ItemTemplate="{StaticResource myTaskTemplate}"
      HorizontalContentAlignment="Stretch"
      IsSynchronizedWithCurrentItem="True"
      Margin="5,0,5,5" />

 </DockPanel>
</Window>
```

Nella figura seguente viene illustrato l'effetto di questo codice:

![Casella di riepilogo che usa un modello di dati](media/introduction-to-wpf/wpfintrofigure19.png)

Si noti che <xref:System.Windows.Controls.ListBox> mantiene il proprio comportamento e l'aspetto complessivo. Solo l'aspetto del contenuto visualizzato dalla casella di riepilogo viene modificato.

Per altre informazioni, vedere [Cenni preliminari sui modelli di dati](data/data-templating-overview.md).

### <a name="styles"></a>Stili

Gli stili consentono agli sviluppatori e ai progettisti di standardizzare un determinato aspetto del prodotto. WPF offre un modello di stile avanzato, basato sull'elemento <xref:System.Windows.Style> . Nell'esempio seguente viene creato uno stile che imposta il colore di sfondo per ogni <xref:System.Windows.Controls.Button> oggetto in una finestra per `Orange` :

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.StyleWindow"
    Title="Styles">
  <!-- Style that will be applied to all buttons -->
  <Style TargetType="{x:Type Button}">
    <Setter Property="Background" Value="Orange" />
    <Setter Property="BorderBrush" Value="Crimson" />
    <Setter Property="FontSize" Value="20" />
    <Setter Property="FontWeight" Value="Bold" />
    <Setter Property="Margin" Value="5" />
  </Style>
  <!-- This button will have the style applied to it -->
  <Button>Click Me!</Button>

  <!-- This label will not have the style applied to it -->
  <Label>Don't Click Me!</Label>

  <!-- This button will have the style applied to it -->
  <Button>Click Me!</Button>
</Window>
```

Poiché lo stile ha come destinazione tutti i controlli <xref:System.Windows.Controls.Button>, viene applicato automaticamente a tutti i pulsanti nella finestra, come illustrato nella figura seguente:

![Due pulsanti di colore arancione](media/introduction-to-wpf/wpfintrofigure20.png)

Per altre informazioni, vedere [stili e modelli](../../desktop-wpf/fundamentals/styles-templates-overview.md).

### <a name="resources"></a>Risorse

I controlli di un'applicazione devono condividere lo stesso aspetto, che può includere qualsiasi elemento dai tipi di carattere e i colori di sfondo ai modelli di controllo e di dati, agli stili. È possibile usare il supporto WPF per le risorse dell'interfaccia utente per incapsulare queste risorse in un'unica posizione e permettere di usarle nuovamente.

L'esempio seguente definisce un colore di sfondo comune condiviso da un oggetto <xref:System.Windows.Controls.Button> e un oggetto <xref:System.Windows.Controls.Label> :

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.ResourcesWindow"
    Title="Resources Window">

  <!-- Define window-scoped background color resource -->
  <Window.Resources>
    <SolidColorBrush x:Key="defaultBackground" Color="Red" />
  </Window.Resources>

  <!-- Button background is defined by window-scoped resource -->
  <Button Background="{StaticResource defaultBackground}">One Button</Button>

  <!-- Label background is defined by window-scoped resource -->
  <Label Background="{StaticResource defaultBackground}">One Label</Label>
</Window>
```

Questo esempio implementa una risorsa di colore di sfondo usando l'elemento della proprietà `Window.Resources` . Questa risorsa è disponibile per tutti gli elementi figlio dell'oggetto <xref:System.Windows.Window>. Sono disponibili vari ambiti di risorsa, inclusi quelli riportati di seguito, elencati nell'ordine in cui vengono risolti:

1. Un singolo controllo (che usa la proprietà <xref:System.Windows.FrameworkElement.Resources%2A?displayProperty=fullName> ereditata).

2. Un oggetto <xref:System.Windows.Window> o <xref:System.Windows.Controls.Page> (che usa la proprietà <xref:System.Windows.FrameworkElement.Resources%2A?displayProperty=fullName> ereditata).

3. Un oggetto <xref:System.Windows.Application> (che usa la proprietà <xref:System.Windows.Application.Resources%2A?displayProperty=fullName> ).

La varietà degli ambiti offre flessibilità riguardo alla modalità di definizione e condivisione delle risorse.

In alternativa all'associazione diretta delle risorse a un determinato ambito, è possibile comprimere una o più risorse usando un oggetto <xref:System.Windows.ResourceDictionary> separato a cui è possibile fare riferimento in altre parti di un'applicazione. Ad esempio, l'esempio seguente definisce un colore di sfondo predefinito in un dizionario risorse:

```xaml
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">

  <!-- Define background color resource -->
  <SolidColorBrush x:Key="defaultBackground" Color="Red" />

  <!-- Define other resources -->
</ResourceDictionary>
```

Nell'esempio seguente viene fatto riferimento al dizionario risorse definito nell'esempio precedente in modo che sia condiviso tra un'applicazione:

```xaml
<Application
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.App">

  <Application.Resources>
    <ResourceDictionary>
      <ResourceDictionary.MergedDictionaries>
        <ResourceDictionary Source="BackgroundColorResources.xaml"/>
      </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
  </Application.Resources>
</Application>
```

Risorse e dizionari risorse sono la base del supporto di WPF per temi e interfacce.

Per altre informazioni, vedere [Risorse](../../desktop-wpf/fundamentals/xaml-resources-define.md).

### <a name="custom-controls"></a>Controlli personalizzati

Anche se WPF offre un ampio supporto per la personalizzazione, in alcune situazioni i controlli di WPF esistenti potrebbero non soddisfare le necessità di un'applicazione o degli utenti. Questo può verificarsi nei casi seguenti:

- Non è possibile creare l'interfaccia utente richiesta personalizzando l'aspetto delle implementazioni di WPF esistenti.

- Il comportamento richiesto non è supportato (o non è supportato facilmente) dalle implementazioni di WPF esistenti.

A questo punto, è tuttavia possibile sfruttare uno dei tre modelli di WPF per creare un nuovo controllo. Ogni modello è destinato a uno scenario specifico e richiede che il controllo personalizzato derivi da una determinata classe di base di WPF. I tre modelli sono elencati di seguito:

- **Modello di controllo utente**. Un controllo personalizzato deriva da <xref:System.Windows.Controls.UserControl> ed è composto da uno o più controlli.

- **Modello di controllo**. Un controllo personalizzato deriva da <xref:System.Windows.Controls.Control> e viene usato per compilare implementazioni che separano il comportamento dall'aspetto tramite modelli, come la maggior parte dei controlli di WPF. La derivazione da <xref:System.Windows.Controls.Control> consente una maggiore libertà nella creazione di un'interfaccia utente personalizzata rispetto ai controlli utente, ma può risultare più complessa.

- **Modello di elemento framework**. Un controllo personalizzato deriva da <xref:System.Windows.FrameworkElement> quando il suo aspetto è definito da logica di rendering personalizzata (non dai modelli).

L'esempio seguente mostra un controllo su/giù numerico personalizzato che deriva da <xref:System.Windows.Controls.UserControl> :

[!code-xaml[IntroToWPFSnippets#UserControlMARKUP](~/samples/snippets/xaml/wpf/introduction-to-wpf/introduction-to-wpf_33.xaml)]

[!code-csharp[IntroToWPFSnippets#UserControlCODEBEHIND1](~/samples/snippets/csharp/wpf/introduction-to-wpf/introduction-to-wpf_34.cs)]
[!code-vb[IntroToWPFSnippets#UserControlCODEBEHIND1](~/samples/snippets/visualbasic/wpf/introduction-to-wpf/introduction-to-wpf_34.vb)]

Nell'esempio seguente viene illustrato il codice XAML necessario per incorporare il controllo utente in un <xref:System.Windows.Window> :

[!code-xaml[IntroToWPFSnippets#UserControlWindowMARKUP1](~/samples/snippets/xaml/wpf/introduction-to-wpf/introduction-to-wpf_37.xaml)]

La figura seguente mostra il `NumericUpDown` controllo ospitato in un <xref:System.Windows.Window> :

![UserControl personalizzato](media/introduction-to-wpf/wpfintrofigure3.png)

Per altre informazioni sui controlli personalizzati, vedere [Cenni preliminari sulla modifica di controlli](controls/control-authoring-overview.md).

## <a name="wpf-best-practices"></a>Procedure consigliate di WPF

Come per qualsiasi piattaforma di sviluppo, è possibile usare WPF in diversi modi per ottenere il risultato desiderato. Per creare applicazioni WPF capaci di fornire l'esperienza utente richiesta e soddisfare le esigenze generali dei destinatari, ci sono procedure consigliate per l'accessibilità, la globalizzazione e localizzazione e le prestazioni. Per altre informazioni, vedere:

- [Accessibilità](../ui-automation/accessibility-best-practices.md)
- [Globalizzazione e localizzazione WPF](advanced/wpf-globalization-and-localization-overview.md)
- [Prestazioni dell'applicazione WPF](advanced/optimizing-wpf-application-performance.md)
- [Sicurezza WPF](security-wpf.md)

## <a name="next-steps"></a>Passaggi successivi

Abbiamo esaminato le funzionalità chiave di WPF. Adesso è necessario compilare la prima applicazione WPF.

> [!div class="nextstepaction"]
> [Procedura dettagliata: Prima applicazione desktop WPF](getting-started/walkthrough-my-first-wpf-desktop-application.md)

## <a name="see-also"></a>Vedere anche

- [Guida introduttiva a WPF](getting-started/index.md)
- [Windows Presentation Foundation](index.md)
- [Risorse della community WPF](getting-started/community-feedback.md)

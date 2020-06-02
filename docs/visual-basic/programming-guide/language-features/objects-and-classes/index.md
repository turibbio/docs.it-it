---
title: Oggetti e classi
ms.date: 05/26/2020
helpviewer_keywords:
- classes [Visual Basic]
- objects [Visual Basic]
ms.assetid: c68c5752-1006-46e1-975a-6717b62a42fc
ms.openlocfilehash: 10e257a1cbc8778565a9838aeef423522f9d2970
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290617"
---
# <a name="objects-and-classes-in-visual-basic"></a>Oggetti e classi in Visual Basic

Un *oggetto* è una combinazione di codice e dati che è possibile considerare come singola unità. Un oggetto può essere una parte di un'applicazione, ad esempio un controllo o un form. Anche un'intera applicazione può essere un oggetto.

Quando si crea un'applicazione in Visual Basic, si utilizzano costantemente gli oggetti. È possibile utilizzare gli oggetti forniti da Visual Basic, ad esempio controlli, form e oggetti di accesso ai dati. È anche possibile usare oggetti di altre applicazioni all'interno dell'applicazione Visual Basic. È inoltre possibile creare oggetti personalizzati e definire per essi proprietà e metodi aggiuntivi. Per i programmi, gli oggetti svolgono la stessa funzione dei blocchi predefiniti. Consentono infatti di scrivere un pezzo di codice una sola volta e di riutilizzarlo quanto necessario.

Questo argomento fornisce informazioni dettagliate sugli oggetti.

## <a name="objects-and-classes"></a>Oggetti e classi

Ogni oggetto in Visual Basic è definito da una *classe*. che ne descrive le variabili, le proprietà, le routine e gli eventi. Gli oggetti sono istanze di classi. Dopo aver definito una classe, sarà possibile creare tutti gli oggetti necessari.

Per comprendere la relazione esistente tra un oggetto e la classe di appartenenza, si pensi alla relazione tra gli stampi per biscotti e i biscotti. La classe è lo stampo che definisce le caratteristiche di ogni biscotto, ad esempio le dimensioni e la forma. La classe viene usata per creare oggetti. Gli oggetti sono i biscotti.

È necessario creare un oggetto prima di poter accedere ai relativi membri, ad eccezione dei [`Shared`](../../../language-reference/modifiers/shared.md) membri a cui è possibile accedere senza un oggetto della classe.

### <a name="create-an-object-from-a-class"></a>Creare un oggetto da una classe

1. Determinare da quale classe si desidera creare un oggetto o definire una classe personalizzata. Ad esempio:

   ```vb
   Public Class Customer
       Public Property AccountNumber As Integer
   End Class
   ```

2. Scrivere un'[istruzione Dim](../../../language-reference/statements/dim-statement.md) per creare una variabile a cui assegnare un'istanza di una classe. La variabile dovrebbe essere del tipo della classe desiderata.

   ```vb
   Dim nextCustomer As Customer
   ```

3. Aggiungere la parola chiave [New](../../../language-reference/operators/new-operator.md) per inizializzare la variabile su una nuova istanza della classe.

   ```vb
   Dim nextCustomer As New Customer
   ```

4. È ora possibile accedere ai membri della classe mediante la variabile oggetto.

   ```vb
   nextCustomer.AccountNumber = lastAccountNumber + 1
   ```

> [!NOTE]
> Quando possibile, è necessario dichiarare che la variabile appartiene al tipo classe a cui si vuole assegnarla. Questa operazione è definita *associazione anticipata*. Se il tipo di classe non è noto in fase di compilazione, è possibile richiamare l'*associazione tardiva* dichiarando che la variabile è del [tipo di dati Object](../../../language-reference/data-types/object-data-type.md). Questo tipo di associazione, tuttavia, può determinare un rallentamento delle prestazioni e limitare l'accesso ai membri dell'oggetto in fase di esecuzione. Per altre informazioni, vedere [Object Variable Declaration](../variables/object-variable-declaration.md) (Dichiarazione di variabili oggetto).

### <a name="multiple-instances"></a>Istanze multiple

Gli oggetti creati da una classe sono spesso identici. Una volta definiti come singoli oggetti, è comunque possibile modificarne le variabili e le proprietà indipendentemente dalle altre istanze. Se, ad esempio, si aggiungono tre caselle di controllo a un form, ogni oggetto casella di controllo è un'istanza della classe <xref:System.Windows.Forms.CheckBox>. I singoli oggetti <xref:System.Windows.Forms.CheckBox> condividono un set di caratteristiche e funzionalità, ad esempio proprietà, variabili, routine ed eventi, definito dalla classe. Ognuno di essi, tuttavia, ha un proprio nome, può essere abilitato e disabilitato separatamente e può essere posizionato in un punto diverso del form.

## <a name="object-members"></a>Membri di oggetti

Un oggetto è un elemento di un'applicazione che rappresenta un'*istanza* di una classe. I campi, le proprietà, i metodi e gli eventi sono i blocchi predefiniti degli oggetti e ne costituiscono i *membri*.

### <a name="member-access"></a>Accesso ai membri

Per accedere a un membro di un oggetto, è necessario specificare il nome della variabile oggetto, un punto (`.`) e il nome del membro, nell'ordine indicato. Nell'esempio seguente viene impostata la proprietà <xref:System.Windows.Forms.Control.Text%2A> di un oggetto <xref:System.Windows.Forms.Label>.

```vb
warningLabel.Text = "Data not saved"
```

#### <a name="intellisense-listing-of-members"></a>Elenco di membri IntelliSense

Quando si richiama l'opzione Elenca membri relativa a una classe, ad esempio quando si digita un punto (`.`) come operatore di accesso ai membri, IntelliSense elenca i membri di tale classe. Se si digita il punto dopo il nome di una variabile dichiarata come istanza della classe, vengono elencati tutti i membri di istanza ma nessuno dei membri condivisi. Se si digita il punto dopo il nome della classe, vengono elencati tutti i membri condivisi ma nessuno dei membri di istanza. Per altre informazioni, vedere [Using IntelliSense](/visualstudio/ide/using-intellisense) (Uso di IntelliSense).

### <a name="fields-and-properties"></a>Campi e proprietà

I *campi* e le *proprietà* rappresentano le informazioni contenute in un oggetto. È possibile recuperare e impostare i valori dei campi e delle proprietà usando le istruzioni di assegnazione, nello stesso modo in cui si recuperano e impostano le variabili locali di una routine. Nell'esempio seguente viene recuperata la proprietà <xref:System.Windows.Forms.Control.Width%2A> e impostata la proprietà <xref:System.Windows.Forms.Control.ForeColor%2A> di un oggetto <xref:System.Windows.Forms.Label>.

```vb
Dim warningWidth As Integer = warningLabel.Width
warningLabel.ForeColor = System.Drawing.Color.Red
```

Si noti che un campo viene chiamato anche *variabile membro*.

Usare le routine delle proprietà nei casi seguenti:

- È necessario controllare come e quando un valore viene impostato o recuperato.

- La proprietà presenta un insieme di valori ben definito che è necessario convalidare.

- L'impostazione di un valore determina modifiche percettibili nello stato dell'oggetto, ad esempio una proprietà `IsVisible`.

- L'impostazione della proprietà determina modifiche ad altre variabili interne o ai valori di altre proprietà.

- Per poter impostare o recuperare la proprietà, è necessario eseguire prima una serie di passaggi.

Usare i campi nei casi seguenti:

- Il valore è di tipo auto-convalidante. Ad esempio, se a una variabile `Boolean` viene assegnato un valore diverso da `True` o `False`, si verifica un errore o una conversione automatica di dati.

- Tutti i valori compresi nell'intervallo supportato dal tipo dati sono validi. Questa affermazione è vera per diverse proprietà di tipo `Single` o `Double`.

- La proprietà è un tipo dati `String`. Non è presente alcun vincolo riguardo alle dimensioni o al valore della stringa.

- Per altre informazioni, vedere [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md).

> [!TIP]
> Mantieni sempre i campi non costanti privati. Quando si desidera renderla pubblica, utilizzare invece una proprietà.

### <a name="methods"></a>Metodi

Un *metodo* è un'azione che può essere eseguita da un oggetto. Ad esempio, <xref:System.Windows.Forms.ComboBox.ObjectCollection.Add%2A> è un metodo dell'oggetto <xref:System.Windows.Forms.ComboBox> che aggiunge una nuova voce in una casella combinata.

Nell'esempio seguente viene illustrato il metodo <xref:System.Windows.Forms.Timer.Start%2A> di un oggetto <xref:System.Windows.Forms.Timer>.

```vb
Dim safetyTimer As New System.Windows.Forms.Timer
safetyTimer.Start()
```

Si noti che un metodo è semplicemente una *routine* esposta da un oggetto.

Per altre informazioni, vedere [Routine](../procedures/index.md).

### <a name="events"></a>Eventi

Un evento è un'azione che viene riconosciuta da un oggetto, ad esempio il clic del mouse o la pressione di un tasto, e alla quale è possibile rispondere mediante un codice scritto appositamente. Gli eventi possono verificarsi come conseguenza di un'azione utente o un codice programma oppure possono essere generati dal sistema. Il codice che segnala un evento è detto codice che *genera* l'evento, mentre il codice che risponde all'evento è detto codice che *gestisce* l'evento.

È inoltre possibile sviluppare eventi personalizzati generati dai propri oggetti e gestiti da altri oggetti. Per altre informazioni, vedere [Eventi](../events/index.md).

### <a name="instance-members-and-shared-members"></a>Membri di istanza e membri condivisi

Quando si crea un oggetto da una classe, il risultato è un'istanza di tale classe. I membri non dichiarati con la parola chiave [Shared](../../../language-reference/modifiers/shared.md) sono *membri di istanza* e appartengono soltanto a tale istanza. Un membro di istanza appartenente a una determinata istanza è indipendente dallo stesso membro appartenente a un'altra istanza della stessa classe. Una variabile membro di istanza, ad esempio, può avere valori differenti in istanze differenti.

I membri dichiarati con la parola chiave `Shared` sono *membri condivisi*. Questo significa che appartengono all'intera classe e non a una particolare istanza. Un membro condiviso viene definito una sola volta, indipendentemente dal numero di istanze della relativa classe che vengono create. Questo è vero anche se non viene creata alcuna istanza. Una variabile membro condiviso, ad esempio, può avere un unico valore, che può essere usato da tutto il codice che ha accesso alla classe.

#### <a name="accessing-non-shared-members"></a>Accesso a membri non condivisi

1. Verificare che l'oggetto sia stato creato a partire dalla relativa classe e che sia stato assegnato a una variabile oggetto.

   ```vb
   Dim secondForm As New System.Windows.Forms.Form
   ```

2. Nell'istruzione che accede al membro, seguire il nome della variabile oggetto con l' *operatore di accesso ai membri* ( `.` ) e quindi il nome del membro.

   ```vb
   secondForm.Show()
   ```

#### <a name="accessing-shared-members"></a>Accesso a membri condivisi

- Seguire il nome della classe con l' *operatore di accesso ai membri* ( `.` ) e quindi il nome del membro. È necessario accedere sempre a un membro `Shared` dell'oggetto tramite il nome della classe.

   ```vb
   Console.WriteLine("This computer is called " & Environment.MachineName)
   ```

- In alternativa, se è già stato creato un oggetto a partire dalla classe, è possibile accedere a un membro `Shared` tramite la variabile dell'oggetto.

### <a name="differences-between-classes-and-modules"></a>Differenze tra classi e moduli

La differenza principale tra le classi e i moduli consiste nel fatto che è possibile creare istanze delle classi come oggetti, ma tale operazione non è possibile per i moduli standard. Poiché è presente una sola copia di dati di un modulo standard, quando una parte del programma modifica una variabile pubblica in un modulo standard, a una successiva lettura della variabile qualsiasi altra parte del programma ottiene lo stesso valore. I dati oggetto, invece, sono separati per ciascun oggetto di cui è stata creata un'istanza. A differenza dei moduli standard, inoltre, le classi possono implementare interfacce. Se una classe è contrassegnata con il modificatore [MustInherit](../../../language-reference/modifiers/mustinherit.md) , non è possibile crearne un'istanza direttamente. Tuttavia, è ancora diverso da un modulo perché può essere ereditato mentre i moduli non possono essere ereditati.

> [!NOTE]
> Quando si applica un modificatore `Shared` a un membro di una classe, il modificatore viene associato alla classe stessa anziché a una particolare istanza di quest'ultima. L'accesso al membro avviene direttamente tramite il nome della classe, nello stesso modo in cui si accede ai membri del modulo.

Le classi e i moduli usano inoltre ambiti diversi per i relativi membri. I membri definiti di una classe vengono dichiarati nell'ambito di una specifica istanza di tale classe ed esistono solo per la durata dell'oggetto. Per accedere ai membri di una classe dall'esterno di quest'ultima, è necessario usare nomi completi nel formato *Oggetto*.*Membro*.

D'altra parte, i membri dichiarati all'interno di un modulo sono accessibili pubblicamente per impostazione predefinita e ad essi può accedere qualsiasi codice che abbia accesso al modulo. Questo significa che le variabili presenti in un modulo standard sono effettivamente variabili globali poiché sono visibili da qualsiasi punto del progetto ed esistono per la durata del programma.

## <a name="reusing-classes-and-objects"></a>Riutilizzo di classi e oggetti

Grazie agli oggetti, è possibile dichiarare variabili e routine una sola volta e quindi riutilizzarle quando necessario. Se, ad esempio, si desidera aggiungere un correttore ortografico a un'applicazione, è possibile definire tutte le variabili e le funzioni di supporto per fornire la funzionalità di correttore ortografico. Se il controllo ortografico viene creato come classe, sarà possibile riutilizzarlo in altre applicazioni aggiungendo un riferimento all'assembly compilato. Soluzione ancora migliore, sarà possibile risparmiare lavoro usando una classe correttore ortografico già sviluppata da altri programmatori.

.NET fornisce molti esempi di componenti disponibili per l'utilizzo. Nell'esempio seguente viene usata la classe <xref:System.TimeZone> nello spazio dei nomi <xref:System>. La classe <xref:System.TimeZone> specifica i membri che consentono di recuperare le informazioni sul fuso orario del computer corrente.

```vb
Public Sub ExamineTimeZone()
    Dim tz As System.TimeZone = System.TimeZone.CurrentTimeZone
    Dim s As String = "Current time zone is "
    s &= CStr(tz.GetUtcOffset(Now).Hours) & " hours and "
    s &= CStr(tz.GetUtcOffset(Now).Minutes) & " minutes "
    s &= "different from UTC (coordinated universal time)"
    s &= vbCrLf & "and is currently "
    If tz.IsDaylightSavingTime(Now) = False Then s &= "not "
    s &= "on ""summer time""."
    Console.WriteLine(s)
End Sub
```

Nell'esempio precedente, la prima [istruzione Dim](../../../language-reference/statements/dim-statement.md) dichiara una variabile oggetto di tipo <xref:System.TimeZone> e assegna alla variabile un oggetto <xref:System.TimeZone> restituito dalla proprietà <xref:System.TimeZone.CurrentTimeZone%2A>.

## <a name="relationships-among-objects"></a>Relazioni tra oggetti

Gli oggetti possono essere posti in relazione tra loro in diversi modi. Esistono due tipi principali di relazione, ovvero *gerarchica* e *di contenimento*.

### <a name="hierarchical-relationship"></a>Relazione gerarchica

Se sono presenti classi di maggiore importanza e classi da esse derivate, tra le prime e le seconde esiste una *relazione gerarchica*. Le gerarchie di classi sono utili per descrivere gli elementi che sono un sottotipo di una classe più generale.

Nell'esempio seguente, si supponga di voler definire un tipo speciale di classe <xref:System.Windows.Forms.Button> che si comporti come una classe <xref:System.Windows.Forms.Button> normale ma che allo stesso tempo esponga un metodo per invertire i colori di sfondo e di primo piano.

#### <a name="define-a-class-that-is-derived-from-an-already-existing-class"></a>Definire una classe derivata da una classe già esistente

1. Usare un'[istruzione Class](../../../language-reference/statements/class-statement.md) per definire una classe dalla quale creare l'oggetto necessario.

   ```vb
   Public Class ReversibleButton
   ```

   Verificare che l'ultima riga di codice della classe sia seguita da un'istruzione `End Class`. Per impostazione predefinita, quando si immette un'istruzione `Class` l'ambiente di sviluppo integrato (IDE) genera automaticamente un'istruzione `End Class`.

2. Aggiungere un'[istruzione Inherits](../../../language-reference/statements/inherits-statement.md) subito dopo l'istruzione `Class`. Specificare la classe dalla quale deriva la nuova classe.

   ```vb
   Inherits System.Windows.Forms.Button
   ```

   La nuova classe eredita tutti i membri definiti dalla classe di base.

3. Aggiungere il codice per i membri aggiuntivi esposti dalla classe derivata. Ad esempio, è possibile aggiungere un metodo `ReverseColors`. La classe derivata sarà simile alla seguente:

   ```vb
   Public Class ReversibleButton
       Inherits System.Windows.Forms.Button
           Public Sub ReverseColors()
               Dim saveColor As System.Drawing.Color = Me.BackColor
               Me.BackColor = Me.ForeColor
               Me.ForeColor = saveColor
          End Sub
   End Class
   ```

   Se si crea un oggetto dalla `ReversibleButton` classe, può accedere a tutti i membri della <xref:System.Windows.Forms.Button> classe, nonché al `ReverseColors` metodo e a qualsiasi altro nuovo membro definito in `ReversibleButton` .

Le classi derivate ereditano i membri della classe su cui sono basate, consentendo di raggiungere una maggiore complessità mano a mano che si avanza nella gerarchia. Per altre informazioni, vedere [Nozioni fondamentali sull'ereditarietà](inheritance-basics.md).

### <a name="compile-the-code"></a>Compilare il codice

Verificare che il compilatore possa accedere alla classe da cui si vuole derivare la nuova classe. A tale scopo è possibile fornire il nome completo della classe, come nell'esempio precedente, oppure specificare il relativo spazio dei nomi in un'[istruzione Imports (tipo e spazio dei nomi .NET)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md). Se la classe si trova in un progetto differente, può essere necessario aggiungere un riferimento a tale progetto. Per ulteriori informazioni, vedere [gestione dei riferimenti in un progetto](/visualstudio/ide/managing-references-in-a-project).

### <a name="containment-relationship"></a>Relazione di contenuto

Un altro tipo di relazione tra oggetti è la *relazione di contenimento*. Gli oggetti contenitore incapsulano logicamente altri oggetti. Ad esempio, l'oggetto <xref:System.OperatingSystem> contiene logicamente un oggetto <xref:System.Version>, restituito tramite la proprietà <xref:System.OperatingSystem.Version%2A>. Tenere presente che l'oggetto contenitore non contiene fisicamente altri oggetti.

#### <a name="collections"></a>Raccolte

Un tipo particolare di contenimento degli oggetti è rappresentato dalle *raccolte*. Le raccolte sono gruppi di oggetti simili che possono essere enumerati. Visual Basic supporta una sintassi specifica in [for each... Istruzione successiva](../../../language-reference/statements/for-each-next-statement.md) che consente di scorrere gli elementi di una raccolta. Inoltre, le raccolte consentono spesso di usare un <xref:Microsoft.VisualBasic.Collection.Item%2A> per recuperare gli elementi in base al relativo indice o tramite l'associazione a una stringa univoca. Le raccolte possono risultare di uso più semplice rispetto alle matrici, in quanto consentono di aggiungere o rimuovere elementi senza ricorrere agli indici. Grazie alla loro facilità d'uso, vengono spesso usate per l'archiviazione di form e controlli.

## <a name="related-topics"></a>Argomenti correlati

[Procedura dettagliata: definizione delle classi](walkthrough-defining-classes.md)\
Viene fornita una descrizione dettagliata della creazione di una classe.

[Metodi e proprietà di overload](overloaded-properties-and-methods.md)\
Metodi e proprietà di overload

[Nozioni fondamentali sull'ereditarietà](inheritance-basics.md)\
Vengono illustrati modificatori di ereditarietà, override di metodi e proprietà, MyClass e MyBase.

[Durata degli oggetti: come creare ed eliminare definitivamente oggetti](object-lifetime-how-objects-are-created-and-destroyed.md)\
Vengono illustrate la creazione e l'eliminazione delle istanze di classe.

[Tipi anonimi](anonymous-types.md)\
Viene descritto come creare e usare i tipi anonimi, che consentono di creare oggetti senza scrivere una definizione della classe per il tipo dati.

[Inizializzatori di oggetto: tipi denominati e anonimi](object-initializers-named-and-anonymous-types.md)\
Vengono discussi gli inizializzatori di oggetto, usati per creare istanze di tipi denominati e anonimi mediante un'unica espressione.

[Procedura: dedurre tipi e nomi di proprietà nelle dichiarazioni di tipo anonimo](how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)\
Viene descritto come dedurre nomi e tipi di proprietà nelle dichiarazioni di tipo anonimo. Vengono forniti esempi di inferenze riuscite e non riuscite.

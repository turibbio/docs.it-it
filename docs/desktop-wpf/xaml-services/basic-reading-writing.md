---
title: Classe XAMLServices e lettura o scrittura di XAML di base
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], XamlServices class
- XamlServices class [XAML Services], how to use
ms.assetid: 6ac27fad-3687-4d7a-add1-3e90675fdfde
ms.openlocfilehash: 264a8c4abcf9a7efceb7c7accd786495d35476e5
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/12/2020
ms.locfileid: "82071878"
---
# <a name="xamlservices-class-and-basic-xaml-reading-or-writing"></a>Classe XAMLServices e lettura o scrittura XAML di baseXAMLServices class and basic XAML reading or writing

<xref:System.Xaml.XamlServices>è una classe fornita da .NET che può essere utilizzata per risolvere scenari XAML che non richiedono l'accesso specifico al flusso del nodo XAML o alle informazioni sul sistema di tipi XAML ottenute da tali nodi. <xref:System.Xaml.XamlServices>L'API può essere `Load` riepilogata come `Parse` segue: `Save` o per supportare `Transform` un percorso di caricamento XAML, per supportare un percorso di salvataggio XAML e per fornire una tecnica che unisce un percorso di caricamento e un percorso di salvataggio. `Transform` può essere usato per passare da uno schema XAML a un altro. In questo argomento vengono riepilogate le classificazioni di ognuna di queste API e vengono descritte le differenze tra determinati overload dei metodi.

## <a name="load"></a>Caricamento

Diversi overload di <xref:System.Xaml.XamlServices.Load%2A> implementano la logica completa per un percorso di caricamento. Il percorso di caricamento usa XAML in diversi formati e restituisce un flusso del nodo XAML. La maggior parte di questi percorsi di caricamento usa XAML in un formato di file di testo XML codificato. È tuttavia anche possibile caricare un flusso generale oppure un'origine XAML precaricata già inclusa in una implementazione <xref:System.Xaml.XamlReader> diversa.

L'overload più semplice per la maggior parte degli scenari è <xref:System.Xaml.XamlServices.Load%28System.String%29>. Questo overload dispone di un parametro `fileName` che rappresenta semplicemente il nome di un file di testo contenente il codice XAML da caricare. Costituisce la soluzione appropriata per scenari di applicazioni, ad esempio applicazioni con attendibilità totale in cui è stata eseguita in precedenza la serializzazione dello stato o dei dati nel computer locale. È anche utile per i framework in cui viene definito il modello di applicazione e si vuole caricare uno dei file standard che definisce il comportamento dell'applicazione, l'interfaccia utente di avvio o altre funzionalità definite dal framework che usano XAML.

<xref:System.Xaml.XamlServices.Load%28System.IO.Stream%29> dispone di altri scenari simili. Questo overload può essere utile nei casi in cui l'utente sceglie i file da caricare, in quanto <xref:System.IO.Stream> rappresenta un output frequente di altre API <xref:System.IO> che possono accedere a un file system oppure nei casi in cui l'accesso alle origini XAML viene eseguito tramite download asincroni o altre tecniche di rete che forniscono anche un flusso. Il caricamento da un flusso o da un'origine selezionata dall'utente può avere implicazioni di sicurezza. Per altre informazioni, vedere [XAML Security Considerations](security-considerations.md).

<xref:System.Xaml.XamlServices.Load%28System.IO.TextReader%29>e <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> sono overload che si basano su lettori di formati di versioni precedenti di .NET. Per usare questi overload, è necessario aver già `Create` creato un'istanza del lettore e usato la relativa API per caricare il codice XAML nel formato pertinente (testo o XML). Non è importante se i puntatori dei record sono stati già spostati negli altri reader o se con questi sono state eseguite altre operazioni. La logica del percorso di caricamento da <xref:System.Xaml.XamlServices.Load%2A> determina sempre l'elaborazione dell'intero input XAML dalla radice verso il basso. I seguenti scenari potrebbero giustificare l'uso di questi overload:

- Aree di progettazione in cui si forniscono funzionalità di modifica di XAML semplici da un editor di testo specifico di XML esistente.

- Varianti degli scenari di <xref:System.IO> in cui si usano i reader dedicati per aprire file o flussi. La logica esegue la verifica rudimentale o l'elaborazione del contenuto prima di effettuare un tentativo di caricamento come XAML.

È possibile caricare un file o un <xref:System.Xml.XmlReader>flusso <xref:System.IO.TextReader>oppure caricare un file , oppure <xref:System.Xaml.XamlReader> che esegue il wrapping dell'input XAML caricando con le API del lettore.

A livello interno, ognuno degli overload precedenti è in definitiva un oggetto <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29>e l'oggetto <xref:System.Xml.XmlReader> passato viene usato per creare un nuovo oggetto <xref:System.Xaml.XamlXmlReader>.

La firma `Load` che fornisce scenari più avanzati è <xref:System.Xaml.XamlServices.Load%28System.Xaml.XamlReader%29>. È possibile usare questa firma per uno dei casi seguenti:

- È stata definita la propria <xref:System.Xaml.XamlReader>implementazione di un oggetto .

- È necessario specificare impostazioni per <xref:System.Xaml.XamlReader> diverse dalle impostazioni predefinite.

Esempi di impostazioni non predefinite:

<xref:System.Xaml.XamlReaderSettings.AllowProtectedMembersOnRoot%2A>\
<xref:System.Xaml.XamlReaderSettings.BaseUri%2A>\
<xref:System.Xaml.XamlReaderSettings.IgnoreUidsOnPropertyElements%2A>\
<xref:System.Xaml.XamlReaderSettings.LocalAssembly%2A>\
<xref:System.Xaml.XamlReaderSettings.ValuesMustBeString%2A>.

Il reader predefinito di <xref:System.Xaml.XamlServices> è <xref:System.Xaml.XamlXmlReader>. Se si forniscono impostazioni personalizzate, <xref:System.Xaml.XamlXmlReader> di seguito sono <xref:System.Xaml.XamlXmlReaderSettings>riportate le proprietà da impostare non predefinite:

<xref:System.Xaml.XamlXmlReaderSettings.CloseInput%2A>\
<xref:System.Xaml.XamlXmlReaderSettings.SkipXmlCompatibilityProcessing%2A>\
<xref:System.Xaml.XamlXmlReaderSettings.XmlLang%2A>\
<xref:System.Xaml.XamlXmlReaderSettings.XmlSpacePreserve%2A>

## <a name="parse"></a>Analizza

<xref:System.Xaml.XamlServices.Parse%2A> è analogo a `Load` in quanto è un'API del percorso di caricamento che crea un flusso del nodo XAML da un input XAML. In questo caso l'input XAML viene fornito direttamente come una stringa che contiene tutto il codice XAML da caricare. <xref:System.Xaml.XamlServices.Parse%2A> è un approccio leggero più adatto a scenari di applicazioni che a quelli di framework. Per altre informazioni, vedere <xref:System.Xaml.XamlServices.Parse%2A>. <xref:System.Xaml.XamlServices.Parse%2A>è solo <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29> una chiamata <xref:System.IO.StringReader> avvolta che coinvolge un internamente.

## <a name="save"></a>Salvare

Vari overload <xref:System.Xaml.XamlServices.Save%2A> di implementare il percorso di salvataggio. Tutte i metodi <xref:System.Xaml.XamlServices.Save%2A> accettano un oggetto grafico come input e producono l'output come flusso, file o istanza di <xref:System.Xml.XmlWriter>/<xref:System.IO.TextWriter> .

L'oggetto di input deve essere l'oggetto radice di alcune rappresentazioni dell'oggetto. Potrebbe trattarsi della radice di un oggetto business, della radice di un albero degli oggetti per una pagina in un scenario di interfaccia utente, della superficie di modifica di lavoro di un strumento di progettazione oppure di altri concetti dell'oggetto radice appropriati per gli scenari.

In molti scenari, la struttura ad albero di oggetti salvata <xref:System.Xaml.XamlServices.Load%2A> è correlata a un'operazione originale che ha caricato XAML con o con altre API implementate da un modello di framework/applicazione. L'albero degli oggetti potrebbe presentare differenze determinate da cambiamenti di stato, modifiche nel punto in cui l'applicazione ha acquisito le impostazioni di runtime di un utente, codice XAML modificato perché l'applicazione è un'area di progettazione XAML e così via. Con o senza modifiche, il concetto di caricamento iniziale del codice XAML dal markup e del suo successivo ulteriore salvataggio, seguito dal confronto dei due formati di markup XAML, viene talvolta definito come una rappresentazione di round trip del codice XAML.

Quando si salva e si serializza un oggetto complesso impostato in un formato di markup, la sfida consiste nel raggiungere un bilanciamento ottimale tra una rappresentazione completa senza perdita di informazioni e l'eccesso di dettagli che rendono il codice XAML difficilmente leggibile. Inoltre, clienti di XAML diversi potrebbero oltretutto usare definizioni diverse o avere altre aspettative rispetto a tale modalità di bilanciamento. Le API <xref:System.Xaml.XamlServices.Save%2A> rappresentano una definizione di tale bilanciamento. Le API <xref:System.Xaml.XamlServices.Save%2A> usano il contesto dello schema XAML disponibile e le caratteristiche basate su CLR predefinite di <xref:System.Xaml.XamlType>, <xref:System.Xaml.XamlMember>, nonché altri concetti intrinseci di XAML e del sistema di tipi XAML per determinare la posizione in cui costrutti del flusso del nodo XAML specifici possono essere ottimizzati quando vengono nuovamente salvati nel markup. Ad esempio,i percorsi di salvataggio <xref:System.Xaml.XamlServices> possono usare il contesto dello schema XAML predefinito basato su CLR per risolvere <xref:System.Xaml.XamlType> per gli oggetti, determinare un oggetto <xref:System.Xaml.XamlType.ContentProperty%2A?displayProperty=nameWithType>e quindi omettere tag di elementi proprietà durante la scrittura della proprietà del contenuto XAML dell'oggetto.

<a name="transform"></a>
## <a name="transform"></a>Trasformare

<xref:System.Xaml.XamlServices.Transform%2A> esegue la conversione o la trasformazione di XAML tramite il collegamento a un percorso di caricamento e a un percorso di salvataggio come una sola operazione. Per <xref:System.Xaml.XamlReader> e <xref:System.Xaml.XamlWriter>è possibile usare un contesto dello schema diverso o un sistema di tipi di supporto diverso, essendo questi gli elementi che influenzano il modo in cui il codice XAML risultante viene trasformato. Si tratta di una soluzione appropriata per le operazioni di trasformazione ampie.

Per le operazioni che si basano sull'esame di ogni nodo in un flusso del nodo XAML, il metodo <xref:System.Xaml.XamlServices.Transform%2A>non viene in genere usato. È invece necessario definire una serie di operazioni del percorso di caricamento e di salvataggio personalizzate, quindi inserire la logica personalizzata. In uno dei percorsi, usare una coppia di writer XAML reader XAML intorno al ciclo del nodo. Ad esempio, caricare il codice XAML iniziale usando <xref:System.Xaml.XamlXmlReader> e avanzare nei nodi con chiamate <xref:System.Xaml.XamlXmlReader.Read%2A> successive. Operando a livello del flusso del nodo XAML, è ora possibile regolare i singoli nodi (tipi, membri, altri nodi) per applicare una trasformazione oppure lasciare il nodo invariato. Il nodo verrà quindi inviato in avanti all'API `Write` pertinente di un oggetto <xref:System.Xaml.XamlObjectWriter> e si scriverà l'oggetto. Per altre informazioni, vedere [Understanding XAML Node Stream Structures and Concepts](understanding-xaml-node-stream-structures-and-concepts.md).

## <a name="see-also"></a>Vedere anche

- <xref:System.Xaml.XamlObjectWriter>
- <xref:System.Xaml.XamlServices>
- [Servizi XAML](../../../api/index.md)

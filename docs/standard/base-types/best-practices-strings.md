---
title: Procedure consigliate per l'uso delle stringhe in .NET
description: Informazioni su come usare le stringhe in modo efficace in applicazioni .NET.
ms.date: 05/01/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [.NET Framework],searching
- best practices,string comparison and sorting
- strings [.NET Framework],best practices
- strings [.NET Framework],basic string operations
- sorting strings
- strings [.NET Framework],sorting
- string comparison [.NET Framework],best practices
- string sorting
- comparing strings
- strings [.NET Framework],comparing
ms.assetid: b9f0bf53-e2de-4116-8ce9-d4f91a1df4f7
ms.openlocfilehash: 28c1397c71debeed181acb2c1acb01b0f8cee7c9
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289365"
---
# <a name="best-practices-for-using-strings-in-net"></a>Procedure consigliate per l'uso delle stringhe in .NET

.NET offre un ampio supporto per lo sviluppo di applicazioni localizzate e globalizzate e semplifica l'applicazione delle convenzioni relative alle impostazioni cultura correnti o alle impostazioni cultura specifiche quando si eseguono operazioni comuni come l'ordinamento e la visualizzazione delle stringhe. Tuttavia, l'ordinamento o il confronto delle stringhe non è sempre un'operazione con distinzione delle impostazioni cultura. Ad esempio, le stringhe usate internamente da un'applicazione in genere devono essere gestite in modo identico in tutte le impostazioni cultura. Quando i dati di stringa indipendenti dalle impostazioni cultura, ad esempio i tag XML, i tag HTML, i nomi utente, i percorsi di file e i nomi degli oggetti di sistema, vengono interpretati come dati con distinzione delle impostazioni cultura, nel codice dell'applicazione possono verificarsi bug complessi, riduzioni delle prestazioni e, in alcuni casi, problemi di sicurezza.

Questo argomento esamina i metodi di ordinamento, confronto e uso di maiuscole e minuscole nelle stringhe in .NET, offre raccomandazioni per selezionare il metodo di gestione delle stringhe appropriato e fornisce informazioni aggiuntive sui metodi di gestione delle stringhe. Inoltre, esamina come vengono gestiti i file formattati, ad esempio i dati numerici e i dati relativi a data e ora, per la visualizzazione e l'archiviazione.

## <a name="recommendations-for-string-usage"></a>Suggerimenti per l'uso delle stringhe

Quando si sviluppa con .NET, seguire queste semplici raccomandazione quando si usano le stringhe:

- Usare gli overload che specificano esplicitamente le regole di confronto tra stringhe per le operazioni di stringa. In genere, questo implica chiamare un overload del metodo con un parametro di tipo <xref:System.StringComparison>.
- Usare <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> o <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> per i confronti come impostazioni di sicurezza predefinite per la corrispondenza tra stringhe indipendente dalle impostazioni cultura.
- Usare i confronti con <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> o <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> per prestazioni migliori.
- Usare le operazioni di stringa basate su <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType> quando si visualizza l'output all'utente.
- Usare i valori non linguistici <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> o <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> al posto delle operazioni di stringa basate su <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> quando il confronto non è linguisticamente rilevante (ad esempio, simbolico).
- Usare il metodo <xref:System.String.ToUpperInvariant%2A?displayProperty=nameWithType> invece di <xref:System.String.ToLowerInvariant%2A?displayProperty=nameWithType> quando si normalizzano le stringhe per il confronto.
- Usare un overload del metodo <xref:System.String.Equals%2A?displayProperty=nameWithType> per controllare se due stringhe sono uguali.
- Usare i metodi <xref:System.String.Compare%2A?displayProperty=nameWithType> e <xref:System.String.CompareTo%2A?displayProperty=nameWithType> per ordinare le stringhe, non per controllare l'uguaglianza.
- Usare la formattazione con distinzione delle impostazioni cultura per visualizzare i dati non di tipo stringa, ad esempio numeri e dati, in un'interfaccia utente. Usare la formattazione con le [impostazioni cultura inglese non dipendenti da paese/area geografica](xref:System.Globalization.CultureInfo.InvariantCulture) per salvare in modo permanente i dati non di tipo stringa in formato stringa.

Evitare le operazioni seguenti quando si usano le stringhe:

- Non usare overload che non specificano in modo esplicito o implicito le regole di confronto tra stringhe per le operazioni di stringa.
- Non usare operazioni di stringa basate su <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> nella maggior parte dei casi. Una delle poche eccezioni riguarda la conservazione di dati significativi a livello linguistico, ma indipendenti dalle impostazioni cultura.
- Non usare un overload del metodo <xref:System.String.Compare%2A?displayProperty=nameWithType> o <xref:System.String.CompareTo%2A> ed eseguire un test per il valore restituito zero per determinare se due stringhe sono uguali.
- Non usare la formattazione con distinzione delle impostazioni cultura per conservare i dati numerici o di data e ora in formato stringa.

## <a name="specifying-string-comparisons-explicitly"></a>Specifica esplicita per il confronto tra stringhe

Molti dei metodi di modifica delle stringhe in .NET sono di tipo overload. In genere, uno o più overload accettano le impostazioni predefinite, mentre altri accettano le impostazioni non predefinite, specificando invece una determinata procedura di confronto o modifica delle stringhe. La maggior parte dei metodi che non si basano sulle impostazioni predefinite include un parametro di tipo <xref:System.StringComparison>, che corrisponde a un'enumerazione che specifica in modo esplicito le regole per il confronto tra stringhe in base alle impostazioni cultura e alle maiuscole e minuscole. La tabella seguente descrive i membri dell'enumerazione <xref:System.StringComparison> .

|Membro StringComparison|Descrizione|
|-----------------------------|-----------------|
|<xref:System.StringComparison.CurrentCulture>|Esegue un confronto con distinzione tra maiuscole e minuscole usando le impostazioni cultura correnti.|
|<xref:System.StringComparison.CurrentCultureIgnoreCase>|Esegue un confronto senza distinzione tra maiuscole e minuscole usando le impostazioni cultura correnti.|
|<xref:System.StringComparison.InvariantCulture>|Esegue un confronto con distinzione tra maiuscole e minuscole usando la lingua inglese.|
|<xref:System.StringComparison.InvariantCultureIgnoreCase>|Esegue un confronto senza distinzione tra maiuscole e minuscole usando la lingua inglese.|
|<xref:System.StringComparison.Ordinal>|Esegue un confronto ordinale.|
|<xref:System.StringComparison.OrdinalIgnoreCase>|Esegue un confronto ordinale senza distinzione tra maiuscole e minuscole.|

Ad esempio, il metodo <xref:System.String.IndexOf%2A> , che restituisce l'indice di una sottostringa in un oggetto <xref:System.String> che corrisponde a un carattere o a una stringa, ha nove overload:

- <xref:System.String.IndexOf%28System.Char%29>, <xref:System.String.IndexOf%28System.Char%2CSystem.Int32%29>e <xref:System.String.IndexOf%28System.Char%2CSystem.Int32%2CSystem.Int32%29>, che per impostazione predefinita eseguono una ricerca ordinale (con distinzione tra maiuscole e minuscole e senza distinzione delle impostazioni cultura) per un carattere nella stringa.
- <xref:System.String.IndexOf%28System.String%29>, <xref:System.String.IndexOf%28System.String%2CSystem.Int32%29>e <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.Int32%29>, che per impostazione predefinita eseguono una ricerca con distinzione tra maiuscole e minuscole e con distinzione delle impostazioni cultura per una sottostringa nella stringa.
- <xref:System.String.IndexOf%28System.String%2CSystem.StringComparison%29>, <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.StringComparison%29>e <xref:System.String.IndexOf%28System.String%2CSystem.Int32%2CSystem.Int32%2CSystem.StringComparison%29>, che includono in parametro di tipo <xref:System.StringComparison> che consente di specificare il formato del confronto.

Si consiglia di selezione un overload che non uso i valori predefiniti, per i seguenti motivi:

- Alcuni overload con parametri predefiniti (quelli che cercano <xref:System.Char> nell'istanza della stringa) eseguono un confronto ordinale, mentre altri (quelli che cercano una stringa nell'istanza della stringa) applicano la distinzione delle impostazioni cultura. È difficile ricordare quale valore predefinito viene usato dai diversi metodi ed è facile confondere gli overload.
- Lo scopo del codice basato sui valori predefiniti per le chiamate al metodo non è chiaro. Nell'esempio seguente, che si basa su impostazioni predefinite, è difficile capire se lo sviluppatore intendeva eseguire un confronto ordinale o linguistico tra due stringhe o se la differenza tra maiuscole e minuscole tra `protocol` e "http" può causare la restituzione di `false`.

     [!code-csharp[Conceptual.Strings.BestPractices#1](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/explicitargs1.cs#1)]
     [!code-vb[Conceptual.Strings.BestPractices#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/explicitargs1.vb#1)]

In generale, si consiglia di chiamare un metodo non basato sulle impostazioni predefinite perché disambigua lo scopo del codice. In questo modo, anche il codice diventa più leggibile ed è più facile eseguirne il debug e la manutenzione. L'esempio seguente riguarda le domande relative all'esempio precedente. Viene specificato che viene utilizzato il confronto ordinale e che le differenze tra maiuscole e minuscole vengono ignorate.

[!code-csharp[Conceptual.Strings.BestPractices#2](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/explicitargs1.cs#2)]
[!code-vb[Conceptual.Strings.BestPractices#2](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/explicitargs1.vb#2)]

## <a name="the-details-of-string-comparison"></a>Dettagli sul confronto tra stringhe

Il confronto tra stringhe è la base di molte operazioni relative alle stringhe, in particolare l'ordinamento e il test di uguaglianza. L'ordinamento delle stringhe viene eseguito in un modo specifico: se "my" compare prima di "string" in un elenco ordinato di stringhe, nel confronto "my" deve essere minore o uguale a "string". Inoltre, il confronto definisce implicitamente l'uguaglianza. L'operazione di confronto restituisce zero per le stringhe che considera uguali. In altre parole, nessuna stringa viene considerata minore delle altre. Le operazioni più significative relative alle stringhe includono una o più delle seguenti procedure: confronto con un'altra stringa ed esecuzione di un'operazione di ordinamento definita correttamente.

> [!NOTE]
> È possibile scaricare le [tabelle di ordinamento spessore](https://www.microsoft.com/download/details.aspx?id=10921), un set di file di testo che contengono informazioni sugli spessori dei caratteri usati nelle operazioni di ordinamento e confronto per i sistemi operativi Windows, e la [tabella degli elementi delle regole di confronto Unicode predefinite](https://www.unicode.org/Public/UCA/latest/allkeys.txt), la versione più recente della tabella di ordinamento spessore per Linux e MacOS. La versione specifica della tabella di ordinamento spessore in Linux e macOS dipende dalla versione delle librerie [International Components for Unicode](http://site.icu-project.org/) installate nel sistema. Per informazioni sulle versioni ICU e sulle versioni Unicode implementate, vedere [Downloading ICU](http://site.icu-project.org/download) (Download di ICU).

Tuttavia, la valutazione di due stringhe per l'uguaglianza e l'ordinamento non produce un unico risultato corretto; l'esito dipende dai criteri usati per il confronto delle stringhe. In particolare, i confronti tra stringhe ordinali o basati sulle convenzioni di uso di maiuscole e minuscole e di ordinamento delle impostazioni cultura correnti o delle [impostazioni cultura inglese non dipendenti da paese/area geografica](xref:System.Globalization.CultureInfo.InvariantCulture) possono produrre risultati diversi.

I confronti di stringhe tramite versioni diverse di .NET oppure tramite .NET in sistemi operativi o versioni del sistema operativo diverse possono inoltre restituire risultati diversi. Per altre informazioni, vedere [Stringhe e standard Unicode](xref:System.String#Unicode).

### <a name="string-comparisons-that-use-the-current-culture"></a>Confronti tra stringhe che usano le impostazioni cultura correnti

Un criterio prevede l'uso delle convenzioni delle impostazioni cultura correnti quando si confrontano le stringhe. I confronti basati sulle impostazioni cultura correnti usano le impostazioni cultura o le impostazioni locali correnti del thread. Se le impostazioni cultura non vengono impostate dall'utente, vengono usate le impostazioni predefinite della finestra **Opzioni internazionali** nel Pannello di controllo. È necessario usare sempre i confronti basati sulle impostazioni cultura correnti quando i dati sono linguisticamente rilevanti e quando riflettono un'interazione utente con distinzione delle impostazioni cultura.

Tuttavia, il comportamento di confronto e di utilizzo di maiuscole e minuscole in .NET cambia quando vengono modificate le impostazioni cultura. Ciò accade quando un'applicazione viene eseguita in un computer con impostazioni cultura diverse da quelle del computer in cui è stata sviluppata oppure quando il thread di esecuzione modifica le proprie impostazioni cultura. Questo comportamento è intenzionale, tuttavia resta poco chiaro per molti sviluppatori. L'esempio seguente illustra le differenze nell'ordinamento tra le impostazioni cultura della lingua inglese per gli Stati Uniti ("en-US") e di quella svedese ("sv-SE"). Si noti che le parole "ångström", "Windows" e "Visual Studio" vengono visualizzate in posizioni diverse nelle matrici di stringhe ordinate.

[!code-csharp[Conceptual.Strings.BestPractices#3](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison1.cs#3)]
[!code-vb[Conceptual.Strings.BestPractices#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison1.vb#3)]

I confronti senza distinzione tra maiuscole e minuscole che usano le impostazioni cultura correnti sono uguali a quelli con distinzione delle impostazioni cultura, ma ignorano la distinzione tra maiuscole e minuscole come indicato dalle impostazioni cultura correnti del thread. Questo comportamento può manifestarsi anche negli ordinamenti.

I confronti che usano la semantica delle impostazioni cultura correnti sono i confronti predefiniti per i seguenti metodi:

- Overload<xref:System.String.Compare%2A?displayProperty=nameWithType> che non includono un parametro <xref:System.StringComparison> .
- Overload<xref:System.String.CompareTo%2A?displayProperty=nameWithType> .
- Metodo <xref:System.String.StartsWith%28System.String%29?displayProperty=nameWithType> predefinito e metodo <xref:System.String.StartsWith%28System.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType> con un parametro `null`<xref:System.Globalization.CultureInfo> .
- Metodo <xref:System.String.EndsWith%28System.String%29?displayProperty=nameWithType> predefinito e metodo <xref:System.String.EndsWith%28System.String%2CSystem.Boolean%2CSystem.Globalization.CultureInfo%29?displayProperty=nameWithType> con un parametro `null`<xref:System.Globalization.CultureInfo> .
- Overload<xref:System.String.IndexOf%2A?displayProperty=nameWithType> che accettano <xref:System.String> come parametro di ricerca e che non hanno un parametro <xref:System.StringComparison> .
- Overload<xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> che accettano <xref:System.String> come parametro di ricerca e che non hanno un parametro <xref:System.StringComparison> .

In ogni caso, si consiglia di chiamare un overload con il parametro <xref:System.StringComparison> per rendere chiaro lo scopo della chiamata al metodo.

È possibile che vengano generati bug complessi e meno complessi quando i dati non linguistici della stringa vengono interpretati linguisticamente oppure quando i dati della stringa di specifiche impostazioni cultura vengono interpretati usando le convenzioni di altre impostazioni cultura. L'esempio canonico è il problema della I turca.

Per quasi tutti gli alfabeti latini, incluso l'inglese (Stati Uniti), il carattere "i" (\u0069) corrisponde alla versione minuscola del carattere "I" (\u0049). Questa regola di utilizzo di maiuscole e minuscole diventa rapidamente l'impostazione predefinita per chi programma queste impostazioni cultura. Tuttavia, l'alfabeto turco ("tr-TR") include una "I con punto", "İ" (\u0130), che è la versione maiuscola di "i". In turco esiste anche un carattere minuscolo "i senza punto", "ı" (\u0131), la cui versione maiuscola è "I". Questo comportamento si verifica anche con le impostazioni cultura azerbaigiana ("az").

Pertanto, i presupposti relativi all'uso della maiuscola per "i" o della minuscola per "I" non sono validi in tutte le impostazioni cultura. Se si usano gli overload predefiniti per le routine di confronto tra stringhe, questi saranno soggetti a variazioni tra le diverse impostazioni cultura. Se i dati da confrontare sono di tipo non linguistico, l'uso degli overload predefiniti può produrre risultati indesiderati, come illustrato in questo tentativo di eseguire un confronto senza distinzione tra maiuscole e minuscole delle stringhe "file" e "FILE".

[!code-csharp[Conceptual.Strings.BestPractices#11](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#11)]
[!code-vb[Conceptual.Strings.BestPractices#11](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#11)]

Questo confronto può causare problemi significativi se le impostazioni cultura vengono usate inavvertitamente in impostazioni relative alla sicurezza, come nel seguente esempio. Una chiamata al metodo come `IsFileURI("file:")` restituisce `true` , se le impostazioni cultura correnti sono per la lingua inglese (Stati Uniti) oppure `false` se le impostazioni cultura correnti sono per la lingua turca. Quindi, nei sistemi turchi, qualcuno potrebbe aggirare le misure di sicurezza che bloccano l'accesso agli URI senza distinzione tra maiuscole e minuscole che iniziano con "FILE:".

[!code-csharp[Conceptual.Strings.BestPractices#12](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#12)]
[!code-vb[Conceptual.Strings.BestPractices#12](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#12)]

In questo caso, poiché "file:" deve essere interpretato come un identificatore non linguistico, indipendente dalle impostazioni cultura, il codice deve essere scritto come illustrato nell'esempio seguente:

[!code-csharp[Conceptual.Strings.BestPractices#13](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/turkish1.cs#13)]
[!code-vb[Conceptual.Strings.BestPractices#13](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/turkish1.vb#13)]

### <a name="ordinal-string-operations"></a>Operazioni di stringa ordinali

La specifica del valore <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> o <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> in una chiamata al metodo indica un confronto non linguistico in cui le funzionalità dei linguaggi naturali vengono ignorate. I metodi richiamati con questi valori <xref:System.StringComparison> basano le decisioni relative alle operazioni di stringa su confronti di byte semplici invece che sull'utilizzo di maiuscole e minuscole o di tabelle di equivalenza parametrizzate dalle impostazioni cultura. In molti casi, questo approccio risulta più adatto per l'interpretazione desiderata delle stringhe e rende il codice più veloce e affidabile.

I confronti ordinali sono confronti tra stringhe in cui ogni byte di ogni stringa viene confrontato senza interpretazione linguistica, ad esempio "windows" non corrisponde a "Windows". Si tratta essenzialmente di una chiamata alla funzione `strcmp` di C Runtime. Usare questo confronto quando il contesto impone l'esatta corrispondenza delle stringhe o richiede un criterio di corrispondenza conservativo. Inoltre, il confronto ordinale è l'operazione di confronto più rapida perché non applica regole linguistiche quando determina un risultato.

Le stringhe in .NET possono contenere caratteri null incorporati. Una delle differenze più evidenti tra il confronto ordinale e quello con distinzione delle impostazioni cultura (inclusi i confronti che usano la lingua inglese) riguarda la gestione dei caratteri null incorporati in una stringa. Questi caratteri vengono ignorati quando si usano i metodi <xref:System.String.Compare%2A?displayProperty=nameWithType> e <xref:System.String.Equals%2A?displayProperty=nameWithType> per eseguire confronti con distinzione delle impostazioni cultura (inclusi i confronti che usano la lingua inglese). Di conseguenza, nei confronti con distinzione delle impostazioni cultura, le stringhe che contengono caratteri null incorporati e quelle che non li contengono possono essere considerate uguali.

> [!IMPORTANT]
> Anche se i metodi di confronto tra stringhe ignorano i caratteri null incorporati, i metodi di ricerca di stringhe come <xref:System.String.Contains%2A?displayProperty=nameWithType>, <xref:System.String.EndsWith%2A?displayProperty=nameWithType>, <xref:System.String.IndexOf%2A?displayProperty=nameWithType>, <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType>e <xref:System.String.StartsWith%2A?displayProperty=nameWithType> li prendono in considerazione.

Nell'esempio seguente viene eseguito un confronto con distinzione delle impostazioni cultura della stringa "AA" con una stringa simile che contiene diversi caratteri null incorporati tra "A" e "a" e Mostra in che modo le due stringhe vengono considerate uguali:

[!code-csharp[Conceptual.Strings.BestPractices#19](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/embeddednulls1.cs#19)]
 [!code-vb[Conceptual.Strings.BestPractices#19](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/embeddednulls1.vb#19)]

Tuttavia, le stringhe non sono considerate uguali quando si usa il confronto ordinale, come illustrato nell'esempio seguente:
  
[!code-csharp[Conceptual.Strings.BestPractices#20](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/embeddednulls2.cs#20)]
[!code-vb[Conceptual.Strings.BestPractices#20](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/embeddednulls2.vb#20)]

I confronti ordinali senza distinzione tra maiuscole e minuscole rappresentano il secondo approccio più conservativo. Questi confronti ignorano quasi del tutto l'utilizzo di maiuscole e minuscole, ad esempio "windows" corrisponde a "Windows". Quando si usano i caratteri ASCII, questo criterio è equivalente a <xref:System.StringComparison.Ordinal?displayProperty=nameWithType>, ma ignora il normale utilizzo di maiuscole e minuscole ASCII. Quindi, qualsiasi carattere in [A, Z] (\u0041-\u005A) corrisponde al carattere corrispondente in [a,z] (\u0061-\007A). L'utilizzo di maiuscole e minuscole al di fuori dell'intervallo ASCII usa le tabelle in lingua inglese. Pertanto, il confronto seguente:

[!code-csharp[Conceptual.Strings.BestPractices#4](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison2.cs#4)]
[!code-vb[Conceptual.Strings.BestPractices#4](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison2.vb#4)]

è equivalente (ma più rapido) rispetto al confronto:

[!code-csharp[Conceptual.Strings.BestPractices#5](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison2.cs#5)]
[!code-vb[Conceptual.Strings.BestPractices#5](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison2.vb#5)]

Questi confronti sono comunque molto rapidi.

> [!NOTE]
> Il comportamento delle stringhe del file system, delle chiavi e dei valori del Registro di sistema e delle variabili di ambiente viene rappresentato in modo efficace da <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType>.

<xref:System.StringComparison.Ordinal?displayProperty=nameWithType> e <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> usano direttamente i valori binari e sono i più adatti per la corrispondenza. Se non si è sicuri delle impostazioni di confronto, usare uno di questi due valori. Tuttavia, poiché eseguono un confronto byte per byte, l'ordinamento non viene eseguito linguisticamente (come in un dizionario inglese), ma in modo binario. Se visualizzati dagli utenti, i risultati possono sembrare strani in molti contesti.

La semantica ordinale è l'impostazione predefinita per gli overload <xref:System.String.Equals%2A?displayProperty=nameWithType> che non includono un argomento <xref:System.StringComparison> (incluso l'operatore di uguaglianza). In ogni caso, si consiglia di chiamare un overload con un parametro <xref:System.StringComparison> .

### <a name="string-operations-that-use-the-invariant-culture"></a>operazioni di stringa che usano la lingua inglese

I confronti con la lingua inglese usano la proprietà <xref:System.Globalization.CultureInfo.CompareInfo%2A> restituita dalla proprietà statica <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> . Questo comportamento è uguale in tutti i sistemi. Converte i caratteri al di fuori dell'intervallo in quelli che considera caratteri equivalenti in lingua inglese. Questo criterio può essere utile per gestire il comportamento di un set di stringhe nelle impostazioni cultura, ma spesso produce risultati imprevisti.

I confronti senza distinzione tra maiuscole e minuscole con la lingua inglese usano la proprietà statica <xref:System.Globalization.CultureInfo.CompareInfo%2A> restituita dalla proprietà statica <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> anche per le informazioni sul confronto. Le differenze tra maiuscole e minuscole in questi caratteri convertiti vengono ignorate.

I confronti che usano <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> e <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> funzionano in modo identico nelle stringhe ASCII. Tuttavia, <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> prende decisioni linguistiche che potrebbero non essere appropriate per le stringhe che devono essere interpretate come set di byte. L'oggetto `CultureInfo.InvariantCulture.CompareInfo` fa sì che il metodo <xref:System.String.Compare%2A> interpreti alcuni set di caratteri come equivalenti. Ad esempio, la seguente equivalenza è valida in lingua inglese:

InvariantCulture: a + ̊ = å

La LETTERA A MINUSCOLA LATINA "a" (\u0061), quando si trova accanto al carattere CERCHIO IN ALTO "+ " ̊" (\u030a), viene interpretata come LETTERA A MINUSCOLA LATINA CON CERCHIO IN ALTO "å" (\u00e5). Come mostrato nell'esempio seguente, questo comportamento è diverso dal confronto ordinale.

[!code-csharp[Conceptual.Strings.BestPractices#15](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/comparison3.cs#15)]
[!code-vb[Conceptual.Strings.BestPractices#15](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/comparison3.vb#15)]

Quando si interpretano i nomi di file, i cookie o qualsiasi altro elemento che può contenere un carattere come "å", i confronti ordinali offrono il comportamento più trasparente e appropriato.

In realtà la lingua inglese ha poche proprietà che la rendono utile per il confronto. Esegue il confronto in un modo linguisticamente rilevante, che non assicura un'equivalenza simbolica completa, ma non rappresenta la scelta ottimale per la visualizzazione nelle impostazioni cultura. Uno dei pochi motivi per usare <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType> per il confronto riguarda la possibilità di conservare i dati ordinati per visualizzarli in modo identico nelle varie impostazioni cultura. Ad esempio, se un file di dati di grandi dimensioni che contiene un elenco di identificatori ordinati per la visualizzazione viene associato a un'applicazione, per aggiungere elementi all'elenco è necessario l'inserimento con un ordinamento in lingua inglese.

## <a name="choosing-a-stringcomparison-member-for-your-method-call"></a>Scelta di un membro StringComparison per la chiamata al metodo

La tabella seguente illustra il mapping tra il contesto di stringa semantico e un <xref:System.StringComparison> membro di enumerazione:

|Data|Comportamento|System.StringComparison corrispondente<br /><br /> Valore|
|----------|--------------|-----------------------------------------------------|
|Identificatori interni con distinzione tra maiuscole e minuscole.<br /><br /> Identificatori con distinzione tra maiuscole e minuscole in standard come XML e HTTP.<br /><br /> Impostazioni relative alla sicurezza con distinzione tra maiuscole e minuscole.|Identificatore non linguistico, con una corrispondenza esatta dei byte.|<xref:System.StringComparison.Ordinal>|
|Identificatori interni senza distinzione tra maiuscole e minuscole.<br /><br /> Identificatori senza distinzione tra maiuscole e minuscole in standard come XML e HTTP.<br /><br /> Percorsi di file.<br /><br /> Chiavi e valori del Registro di sistema.<br /><br /> Variabili di ambiente.<br /><br /> Identificatori di risorse (ad esempio, nomi di handle).<br /><br /> Impostazioni relative alla sicurezza senza distinzione tra maiuscole e minuscole.|Identificatore non linguistico, in cui la distinzione tra maiuscole e minuscole non è rilevante. In particolare, dati archiviati nella maggior parte dei servizi di sistema Windows.|<xref:System.StringComparison.OrdinalIgnoreCase>|
|Alcuni dati persistenti e linguisticamente rilevanti.<br /><br /> Visualizzazione di dati linguistici che richiedono un ordinamento fisso.|Dati indipendenti dalle impostazioni cultura, ma ancora linguisticamente rilevanti.|<xref:System.StringComparison.InvariantCulture><br /><br /> -oppure-<br /><br /> <xref:System.StringComparison.InvariantCultureIgnoreCase>|
|Dati visualizzati dall'utente.<br /><br /> La maggior parte dell'input utente.|Dati che richiedono personalizzazioni linguistiche locali.|<xref:System.StringComparison.CurrentCulture><br /><br /> -oppure-<br /><br /> <xref:System.StringComparison.CurrentCultureIgnoreCase>|

## <a name="common-string-comparison-methods-in-net"></a>Metodi comuni per il confronto tra stringhe in .NET

Le sezioni seguenti descrivono i metodi più comuni per il confronto tra stringhe.

### <a name="stringcompare"></a>String.Compare

Interpretazione predefinita: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.

Poiché si tratta dell'operazione più importante per l'interpretazione della stringa, tutte le istanze di queste chiamate al metodo devono essere esaminate per determinare se le stringhe devono essere interpretate in base alle impostazioni cultura correnti o devono essere dissociate dalle impostazioni cultura (simbolicamente). In genere, si tratta del secondo caso e deve pertanto essere utilizzato un confronto <xref:System.StringComparison.Ordinal?displayProperty=nameWithType> .

La classe <xref:System.Globalization.CompareInfo?displayProperty=nameWithType> , restituita dalla proprietà <xref:System.Globalization.CultureInfo.CompareInfo%2A?displayProperty=nameWithType> , include anche un metodo <xref:System.Globalization.CompareInfo.Compare%2A> che fornisce numerose opzioni di corrispondenza (ordinale, con esclusione degli spazi vuoti, con esclusione del tipo Kana e così via) mediante l'enumerazione flag <xref:System.Globalization.CompareOptions> .

### <a name="stringcompareto"></a>String.CompareTo

Interpretazione predefinita: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.

Questo metodo attualmente non offre un overload che specifica un tipo <xref:System.StringComparison> . In genere è possibile convertire questo metodo nel formato <xref:System.String.Compare%28System.String%2CSystem.String%2CSystem.StringComparison%29?displayProperty=nameWithType> consigliato.

I tipi che implementano le interfacce <xref:System.IComparable> e <xref:System.IComparable%601> implementano questo metodo. Poiché non offre l'opzione di un parametro <xref:System.StringComparison> , l'implementazione dei tipi spesso lascia specificare all'utente <xref:System.StringComparer> nel proprio costruttore. L'esempio seguente definisce una classe `FileName` il cui costruttore include un parametro <xref:System.StringComparer> . L'oggetto <xref:System.StringComparer> viene quindi usato nel metodo `FileName.CompareTo` .

[!code-csharp[Conceptual.Strings.BestPractices#6](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/api1.cs#6)]
[!code-vb[Conceptual.Strings.BestPractices#6](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/api1.vb#6)]

### <a name="stringequals"></a>String.Equals

Interpretazione predefinita: <xref:System.StringComparison.Ordinal?displayProperty=nameWithType>.

La classe <xref:System.String> consente di eseguire un test di uguaglianza chiamando gli overload del metodo <xref:System.String.Equals%2A> dell'istanza o statici oppure usando l'operatore di uguaglianza statico. Gli overload e l'operatore usano il confronto ordinale per impostazione predefinita. Tuttavia, si consiglia di chiamare comunque un overload che specifichi esplicitamente il tipo <xref:System.StringComparison> anche se si vuole eseguire un confronto ordinale; questo semplifica la ricerca di codice per una determinata interpretazione della stringa.

### <a name="stringtoupper-and-stringtolower"></a>String.ToUpper e String.ToLower

Interpretazione predefinita: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.

Prestare attenzione quando si usano questi metodi perché l'utilizzo forzato di maiuscole o minuscole in una stringa è una procedura usata spesso come normalizzazione minore per confrontare stringhe indipendentemente dalla distinzione tra maiuscole e minuscole. In questo caso, valutare l'uso di un confronto senza distinzione tra maiuscole e minuscole.

Sono disponibili anche i metodi <xref:System.String.ToUpperInvariant%2A?displayProperty=nameWithType> e <xref:System.String.ToLowerInvariant%2A?displayProperty=nameWithType> . <xref:System.String.ToUpperInvariant%2A> è la modalità standard di normalizzazione dei caratteri maiuscoli e minuscoli. A livello di comportamento, i confronti eseguiti con <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> corrispondono alla composizione di due chiamate: la chiamata a <xref:System.String.ToUpperInvariant%2A> in entrambi gli argomenti di stringa e l'esecuzione di un confronto con <xref:System.StringComparison.Ordinal?displayProperty=nameWithType>.

Sono disponibili anche overload per la conversione in maiuscole e minuscole in determinate impostazioni cultura, passando un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le specifiche impostazioni cultura al metodo.

### <a name="chartoupper-and-chartolower"></a>Char.ToUpper e Char.ToLower

Interpretazione predefinita: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.

Questi metodi funzionano in modo simile ai metodi <xref:System.String.ToUpper%2A?displayProperty=nameWithType> e <xref:System.String.ToLower%2A?displayProperty=nameWithType> descritti nella sezione precedente.

### <a name="stringstartswith-and-stringendswith"></a>String.StartsWith e String.EndsWith

Interpretazione predefinita: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.

Per impostazione predefinita, entrambi i metodi eseguono un confronto con distinzione delle impostazioni cultura.

### <a name="stringindexof-and-stringlastindexof"></a>String.IndexOf e String.LastIndexOf

Interpretazione predefinita: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.

La modalità di esecuzione dei confronti con gli overload predefiniti di questi metodi manca di coerenza. Tutti i metodi <xref:System.String.IndexOf%2A?displayProperty=nameWithType> e <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> che includono un parametro <xref:System.Char> eseguono un confronto ordinale, ma i metodi predefiniti <xref:System.String.IndexOf%2A?displayProperty=nameWithType> e <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> che includono un parametro <xref:System.String> eseguono un confronto con distinzione delle impostazioni cultura.

Se si chiama il metodo <xref:System.String.IndexOf%28System.String%29?displayProperty=nameWithType> o <xref:System.String.LastIndexOf%28System.String%29?displayProperty=nameWithType> e si passa una stringa da individuare nell'istanza corrente, si consiglia di chiamare un overload che specifichi esplicitamente il tipo <xref:System.StringComparison> . Gli overload che includono un argomento <xref:System.Char> non consentono di specificare un tipo <xref:System.StringComparison> .

## <a name="methods-that-perform-string-comparison-indirectly"></a>Metodi che eseguono indirettamente il confronto tra stringhe

Alcuni metodi non di tipo stringa in cui il confronto tra stringhe rappresenta l'operazione più importante usano il tipo <xref:System.StringComparer> . La classe <xref:System.StringComparer> include sei proprietà statiche che restituiscono istanze <xref:System.StringComparer> i cui metodi <xref:System.StringComparer.Compare%2A?displayProperty=nameWithType> eseguono i tipi di confronto tra stringhe seguenti:

- Confronti tra stringhe con distinzione delle impostazioni cultura usando le impostazioni cultura correnti. L'oggetto <xref:System.StringComparer> viene restituito dalla proprietà <xref:System.StringComparer.CurrentCulture%2A?displayProperty=nameWithType> .
- Confronti senza distinzione tra maiuscole e minuscole usando le impostazioni cultura correnti. L'oggetto <xref:System.StringComparer> viene restituito dalla proprietà <xref:System.StringComparer.CurrentCultureIgnoreCase%2A?displayProperty=nameWithType> .
- Confronti tra stringhe senza distinzione delle impostazioni cultura usando le regole di confronto per parola della lingua inglese. L'oggetto <xref:System.StringComparer> viene restituito dalla proprietà <xref:System.StringComparer.InvariantCulture%2A?displayProperty=nameWithType> .
- Confronti senza distinzione tra maiuscole e minuscole e senza distinzione delle impostazioni cultura usando le regole di confronto per parola della lingua inglese. L'oggetto <xref:System.StringComparer> viene restituito dalla proprietà <xref:System.StringComparer.InvariantCultureIgnoreCase%2A?displayProperty=nameWithType> .
- Confronto ordinale. L'oggetto <xref:System.StringComparer> viene restituito dalla proprietà <xref:System.StringComparer.Ordinal%2A?displayProperty=nameWithType> .
- Confronto ordinale senza distinzione tra maiuscole e minuscole. L'oggetto <xref:System.StringComparer> viene restituito dalla proprietà <xref:System.StringComparer.OrdinalIgnoreCase%2A?displayProperty=nameWithType> .

### <a name="arraysort-and-arraybinarysearch"></a>Array.Sort e Array.BinarySearch

Interpretazione predefinita: <xref:System.StringComparison.CurrentCulture?displayProperty=nameWithType>.

Quando si archiviano dati in una raccolta o si leggono dati persistenti da un file o da un database nella raccolta, la modifica delle impostazioni cultura correnti può invalidare le invarianti nella raccolta. Il metodo <xref:System.Array.BinarySearch%2A?displayProperty=nameWithType> presuppone che gli elementi nella matrice da cercare siano già ordinati. Per ordinare qualsiasi elemento di tipo stringa nella matrice, il metodo <xref:System.Array.Sort%2A?displayProperty=nameWithType> chiama il metodo <xref:System.String.Compare%2A?displayProperty=nameWithType> per ordinare i singoli elementi. L'uso di un operatore di confronto con distinzione delle impostazioni cultura può essere pericoloso se le impostazioni cultura vengono modificate tra l'ordinamento della matrice e la ricerca dei contenuti. Nel codice seguente, ad esempio, le operazioni di archiviazione e recupero vengono eseguite sull'operatore di confronto fornito in modo implicito dalla proprietà `Thread.CurrentThread.CurrentCulture` . Se le impostazioni cultura possono cambiare tra le chiamate a `StoreNames` e `DoesNameExist`e, in particolare, se il contenuto della matrice viene conservato tra le due chiamate al metodo, è possibile che la ricerca binaria non riesca.

[!code-csharp[Conceptual.Strings.BestPractices#7](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#7)]
 [!code-vb[Conceptual.Strings.BestPractices#7](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#7)]

L'esempio seguente mostra una variazione consigliata che usa lo stesso metodo di confronto ordinale (senza distinzione delle impostazioni cultura) sia per l'ordinamento che per la ricerca nella matrice. Il codice modificato si riflette nelle righe identificate con `Line A` e `Line B` nei due esempi.

[!code-csharp[Conceptual.Strings.BestPractices#8](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#8)]
[!code-vb[Conceptual.Strings.BestPractices#8](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#8)]

Se i dati vengono conservati e spostati nelle impostazioni cultura e l'ordinamento viene usato per presentare i dati all'utente, potrebbe esser opportuno usare <xref:System.StringComparison.InvariantCulture?displayProperty=nameWithType>, che garantisce un output utente migliore dal punto di vista linguistico ma non viene interessato dalle modifiche nelle impostazioni cultura. L'esempio seguente modifica i due esempi precedenti per usare la lingua inglese per l'ordinamento e la ricerca della matrice.

[!code-csharp[Conceptual.Strings.BestPractices#9](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect1.cs#9)]
[!code-vb[Conceptual.Strings.BestPractices#9](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect1.vb#9)]

### <a name="collections-example-hashtable-constructor"></a>Esempio di raccolte: Costruttore Hashtable

L'esecuzione dell'hashing nelle stringhe fornisce un secondo esempio di operazione interessata dal modo in cui vengono confrontate le stringhe.

L'esempio seguente crea un'istanza di un oggetto <xref:System.Collections.Hashtable> passando l'oggetto <xref:System.StringComparer> restituito dalla proprietà <xref:System.StringComparer.OrdinalIgnoreCase%2A?displayProperty=nameWithType> . Poiché una classe <xref:System.StringComparer> derivata da <xref:System.StringComparer> implementa l'interfaccia <xref:System.Collections.IEqualityComparer> , il metodo <xref:System.Collections.IEqualityComparer.GetHashCode%2A> viene usato per calcolare il codice hash delle stringhe nella tabella hash.

[!code-csharp[Conceptual.Strings.BestPractices#10](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/indirect2.cs#10)]
[!code-vb[Conceptual.Strings.BestPractices#10](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/indirect2.vb#10)]

## <a name="displaying-and-persisting-formatted-data"></a>Visualizzazione e conservazione dei dati formattati

Quando si consente agli utenti di visualizzare dati non di tipo stringa, come numeri e date e ore, formattarli usando le impostazioni cultura dell'utente. Per impostazione predefinita, nei casi seguenti si usano impostazioni cultura del thread corrente nelle operazioni di formattazione:

- Stringhe interpolate supportate da compilatori [C#](../../csharp/language-reference/tokens/interpolated.md) e [Visual Basic](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md).
- Operazioni di concatenazione di stringhe che usano operatori di concatenazione [ C# ](../../csharp/language-reference/operators/addition-operator.md#string-concatenation) o [Visual Basic](../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md) o che chiamano il metodo <xref:System.String.Concat%2A?displayProperty=nameWithType> direttamente.
- Metodo <xref:System.String.Format%2A?displayProperty=nameWithType> .
- Metodi `ToString` dei tipi numerici e dei tipi data e ora.

Per specificare in modo esplicito che una stringa deve essere formattata usando le convenzioni delle impostazioni cultura definite o le [impostazioni cultura inglese non dipendenti da paese/area geografica](xref:System.Globalization.CultureInfo.InvariantCulture), è possibile eseguire le operazioni seguenti:

- Quando si usano i metodi <xref:System.String.Format%2A?displayProperty=nameWithType> e `ToString`, chiamare un overload con un parametro `provider`, ad esempio <xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=nameWithType> o <xref:System.DateTime.ToString%28System.IFormatProvider%29?displayProperty=nameWithType> e passarlo alla proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>, un'istanza di <xref:System.Globalization.CultureInfo> che rappresenta il valore desiderato delle impostazioni cultura, o proprietà <xref:System.Globalization.CultureInfo.InvariantCulture?displayProperty=nameWithType>.

- Per la concatenazione di stringhe, non consentire al compilatore di eseguire tutte le conversioni implicite. In alternativa, eseguire una conversione esplicita tramite la chiamata a un overload di `ToString` che abbia un parametro `provider`. Il compilatore, ad esempio, utilizza in modo implicito le impostazioni cultura correnti durante <xref:System.Double> la conversione di un valore in una stringa nel codice seguente:

  [!code-csharp[Implicit String Conversion](./snippets/best-practices-strings/csharp/tostring/Program.cs#1)]
  [!code-vb[Implicit String Conversion](./snippets/best-practices-strings/vb/tostring/Program.vb#1)]

  In alternativa, è possibile specificare in modo esplicito le impostazioni cultura le cui convenzioni di formattazione vengono utilizzate nella conversione chiamando il <xref:System.Double.ToString(System.IFormatProvider)?displayProperty=nameWithType> metodo, come il codice seguente:

  [!code-csharp[Explicit String Conversion](./snippets/best-practices-strings/csharp/tostring/Program.cs#2)]
  [!code-vb[Implicit String Conversion](./snippets/best-practices-strings/vb/tostring/Program.vb#2)]

- Per l'interpolazione di stringhe, anziché assegnare una stringa interpolata a un'istanza di <xref:System.String>, assegnarla a un'istanza di <xref:System.FormattableString>. È quindi possibile chiamare il metodo <xref:System.FormattableString.ToString?displayProperty=nameWithType> per produrre una stringa di risultato che rifletta le convenzioni delle impostazioni cultura correnti, oppure è possibile chiamare il metodo <xref:System.FormattableString.ToString(System.IFormatProvider)?displayProperty=nameWithType> per produrre una stringa di risultato che rifletta le convenzioni delle impostazioni cultura specificate. È anche possibile passare la stringa formattabile al metodo statico <xref:System.FormattableString.Invariant%2A?displayProperty=nameWithType> per produrre una stringa di risultato che rifletta le convenzioni delle impostazioni cultura inglese non dipendenti da paese/area geografica. Questo approccio viene illustrato nell'esempio seguente: L'output dell'esempio riflette le impostazioni cultura correnti en-US.

  [!code-csharp[String interpolation](./snippets/best-practices-strings/csharp/formattable/Program.cs)]
  [!code-vb[String interpolation](./snippets/best-practices-strings/vb/formattable/Program.vb)]

È possibile conservare i dati non di tipo stringa come dati binari o formattati. Se si sceglie di salvarli come dati formattati, è necessario chiamare un overload del metodo di formattazione che include un parametro `provider` e passare la proprietà <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> . La lingua inglese fornisce un formato coerente per i dati formattati, indipendente dalle impostazioni cultura e dal computer. Al contrario, conservare i dati formattati con impostazioni cultura diverse dalla lingua inglese presenta diverse limitazioni:

- È probabile che i dati non saranno utilizzabili se vengono recuperati in un sistema con impostazioni cultura diverse oppure se l'utente del sistema corrente modifica le impostazioni cultura correnti e prova a recuperare i dati.
- Le proprietà delle impostazioni cultura in uno specifico computer possono essere diverse rispetto ai valori standard. Un utente può personalizzare in qualsiasi momento le impostazioni di visualizzazione con distinzione delle impostazioni cultura. Per questo motivo, i dati formattati salvati in un sistema potrebbero non essere leggibili dopo che un utente personalizza le impostazioni cultura. La portabilità dei dati formattati tra i vari computer potrebbe risultare ancora più limitata.
- Gli standard internazionali, regionali o nazionali che regolano la formattazione dei numeri o delle date e delle ore cambiano nel tempo e queste modifiche vengono incorporate negli aggiornamenti del sistema operativo Windows. Quando le convenzioni di formattazione vengono modificate, i dati formattati con le convenzioni precedenti possono diventare illeggibili.

L'esempio seguente illustra la limitazione della portabilità causata dall'uso della formattazione con distinzione delle impostazioni cultura per la persistenza dei dati. L'esempio salva una matrice di valori di data e ora in un file. Questi vengono formattati usando le convenzioni delle impostazioni cultura per la lingua inglese (Stati Uniti) . Quando l'applicazione modifica le impostazioni cultura del thread corrente in francese (Svizzera), tenta di leggere i valori salvati usando le convenzioni di formattazione delle impostazioni cultura correnti. Il tentativo di lettura di due elementi di dati genera un'eccezione <xref:System.FormatException> , quindi la matrice di date conterrà due elementi non corretti uguali a <xref:System.DateTime.MinValue>.

[!code-csharp[Conceptual.Strings.BestPractices#21](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.strings.bestpractices/cs/persistence.cs#21)]
[!code-vb[Conceptual.Strings.BestPractices#21](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.strings.bestpractices/vb/persistence.vb#21)]

Tuttavia, se si sostituisce la <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> proprietà con <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> nelle chiamate a <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> e <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> , i dati di data e ora salvati vengono ripristinati correttamente, come illustrato nell'output seguente:

```console
06.05.1758 21:26
05.05.1818 07:19
22.04.1870 23:54
08.09.1890 06:47
18.02.1905 15:12
```

---
title: Resgen.exe (generatore di file di risorse)
ms.date: 03/30/2017
helpviewer_keywords:
- resource files, .resources files
- resource files, .resx files
- resx files (resource files)
- .resources files
- files, converting
- Resource File Generator
- .resx files
- Resgen.exe
- resource files, converting
- converting files, Resource File Generator
- binary resources files
- embedding files in runtime binary executable
ms.assetid: 8ef159de-b660-4bec-9213-c3fbc4d1c6f4
ms.openlocfilehash: b9be030689ecf78b3482743e486e32012e9ca5d4
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/29/2020
ms.locfileid: "84201111"
---
# <a name="resgenexe-resource-file-generator"></a>Resgen.exe (generatore di file di risorse)
Il generatore di file di risorse (Resgen.exe) converte i file di testo (.txt o .restext) e i file di risorse basati su XML (.resx) in file binari Common Language Runtime (.resources) incorporabili in un eseguibile binario o in un assembly satellite di runtime. Vedere [Creazione di file di risorse](../resources/creating-resource-files-for-desktop-apps.md).  
  
 Resgen.exe è un'utilità generica di conversione delle risorse che esegue le seguenti attività:  
  
- Converte i file .txt o .restext in file .resources o .resx. Il formato dei file .restext è identico al formato dei file .txt, Tuttavia, l'estensione .restext consente di identificare più facilmente i file di testo che contengono definizioni di risorse.  
  
- Converte i file .resources in file di testo o .resx.  
  
- Converte i file .resx in file di testo o .resources.  
  
- Estrae le risorse di stringa da un assembly in un file con estensione resw adatto per l'uso in un'app di Windows 8. x Store.  
  
- Crea una classe fortemente tipizzata che fornisce accesso alle singole risorse denominate e all'istanza <xref:System.Resources.ResourceManager>.  
  
 Se l'esecuzione di Resgen.exe non riesce per qualsiasi motivo, il valore restituito è -1.  
  
 Per ottenere informazioni su Resgen. exe, è possibile utilizzare il comando seguente, senza opzioni specificate, per visualizzare la sintassi del comando e le opzioni per Resgen. exe:  
  
```console  
resgen  
```  
  
 È inoltre possibile utilizzare l'opzione `/?`:  
  
```console  
resgen /?  
```  
  
 Se si utilizza Resgen. exe per generare file binari con estensione resources, è possibile utilizzare un compilatore di linguaggio per incorporare i file binari in assembly eseguibili oppure è possibile utilizzare [assembly linker (al. exe)](al-exe-assembly-linker.md) per compilarli in assembly satellite.  
  
 Viene installato automaticamente con Visual Studio. Per eseguire lo strumento, usare il Prompt dei comandi per gli sviluppatori per Visual Studio (o il prompt dei comandi di Visual Studio in Windows 7). Per altre informazioni, vedere [Prompt dei comandi](developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## <a name="syntax"></a>Sintassi  
  
```console  
resgen  [-define:symbol1[,symbol2,...]] [/useSourcePath] filename.extension  | /compile filename.extension... [outputFilename.extension] [/r:assembly] [/str:lang[,namespace[,class[,file]]] [/publicclass]]
```  
  
```console  
resgen filename.extension [outputDirectory]  
```  
  
## <a name="parameters"></a>Parametri  
  
|Parametro o opzione|Descrizione|  
|-------------------------|-----------------|  
|`/define:` *simbolo1*[, *simbolo2*,...]|A partire da .NET Framework 4.5, supporta la compilazione condizionale in file di risorse basati su testo, con estensione txt o restext. Se *simbolo* corrisponde ad un simbolo incluso nel file di testo di input all'interno di un costrutto `#ifdef`, la risorsa di tipo stringa associata viene inclusa nel file RESOURCES. Se il file di testo di input include un'istruzione `#if !` con un simbolo non definito dall'opzione `/define`, la risorsa di tipo stringa associata viene inclusa nel file di risorse.<br /><br /> `/define` viene ignorato se è utilizzato con file non di testo. Nei simboli viene fatta distinzione tra maiuscole e minuscole.<br /><br /> Per altre informazioni su questa opzione, vedere [Compilazione condizionale di risorse](#Conditional) più avanti in questo argomento.|  
|`useSourcePath`|Specifica che è necessario usare la directory corrente del file di input per risolvere i percorsi di file relativi.|  
|`/compile`|Consente di specificare più file di testo o .resx da convertire in più file .resources con una singola operazione di massa. Se non si specifica questa opzione, sarà possibile specificare un solo argomento di file di input. I file di output sono denominati *nomefile*.resources.<br /><br /> Non è possibile usare questa opzione con l'opzione `/str:`.<br /><br /> Per altre informazioni su questa opzione, vedere [Compilazione o conversione di più file](#Multiple) più avanti in questo argomento.|  
|`/r:` `assembly`|Fa riferimento ai metadati dell'assembly specificato. Utilizzata quando si convertono i file .resx, consente a Resgen.exe di serializzare o deserializzare risorse di tipo oggetto. È simile alle opzioni `/reference:` o `/r:` per i compilatori C# e Visual Basic.|  
|`filename.extension`|Specifica il nome del file di input da convertire. Se si utilizza la prima, più lunga sintassi della riga di comando presentata prima di questa tabella, `extension` deve essere una delle seguenti:<br /><br /> .txt o .restext<br /> Un file di testo da convertire in un file .resources o .resx. I file di testo possono contenere solo risorse di tipo stringa. Per informazioni sul formato del file, vedere la sezione "Risorse in file di testo" in [Creazione di file di risorse](../resources/creating-resource-files-for-desktop-apps.md).<br /><br /> resx<br /> Un file di risorse basato su XML da convertire in un file .resources o in un file di testo (.txt o .restext).<br /><br /> .resources<br /> Un file di risorse binario da convertire in un file .resx o di testo (.txt o .restext).<br /><br /> Se si utilizza la seconda, più breve sintassi della riga di comando presentata prima di questa tabella, `extension` deve essere la seguente:<br /><br /> .exe o .dll<br /> Assembly .NET Framework (eseguibile o libreria) le cui risorse di stringa devono essere estratte in un file con estensione resw da utilizzare per lo sviluppo di app di Windows 8. x Store.|  
|`outputFilename.extension`|Specifica il nome e il tipo del file di risorse da creare.<br /><br /> Questo argomento è facoltativo quando si esegue la conversione da un file .txt, .restext o .resx in un file .resources. Se non si specifica `outputFilename`, viene automaticamente aggiunta l'estensione .resources al `filename` di input e il file viene scritto nella directory contenente `filename,extension`.<br /><br /> L'argomento `outputFilename.extension` è obbligatorio quando si esegue la conversione da un file .resources. Specificare un nome file con l'estensione .resx quando si converte un file .resources in un file di risorse basato su XML. Specificare un nome file con l'estensione .txt o .restext quando si converte un file .resources in un file di testo. È consigliabile convertire un file .resources in un file .txt solo quando il file .resources contiene unicamente valori di tipo stringa.|  
|`outputDirectory`|Per le app di Windows 8. x Store, specifica la directory in cui verrà scritto un file con estensione resw che contiene le risorse di stringa in `filename.extension` . `outputDirectory` deve già esistere.|  
|`/str:` `language[,namespace[,classname[,filename]]]`|Crea un file di classe di risorse fortemente tipizzato nel linguaggio di programmazione specificato nell'opzione `language`. `language` può consistere in uno dei seguenti valori letterali:<br /><br /> -   Per C#: `c#`, `cs` o `csharp`.<br />-   Per Visual Basic: `vb` o `visualbasic`.<br />-   Per VBScript: `vbs` o `vbscript`.<br />-   Per C++: `c++`, `mc` o `cpp`.<br />-   Per JavaScript: `js`, `jscript` o `javascript`.<br /><br /> L'opzione `namespace` specifica lo spazio dei nomi predefinito del progetto, l'opzione `classname` specifica il nome della classe generata e l'opzione `filename` specifica il nome del file di classe.<br /><br /> L'opzione `/str:` consente un solo file di input, pertanto non può essere utilizzata con l'opzione `/compile`.<br /><br /> Se viene specificato `namespace`, ma non `classname`, il nome della classe deriva dal nome del file di output; ad esempio, le sottolineature vengono sostituite ai punti. Di conseguenza è possibile che le risorse fortemente tipizzate non funzionino correttamente. Per ovviare a questo problema, specificare sia il nome della classe che il nome del file di output.<br /><br /> Per altre informazioni su questa opzione, vedere [Generazione di una classe di risorse fortemente tipizzata](#Strong) più avanti in questo argomento.|  
|`/publicClass`|Crea una classe di risorse fortemente tipizzata come classe pubblica. Per impostazione predefinita, la classe di risorse è `internal` in C# e `Friend` in Visual Basic.<br /><br /> Questa opzione viene ignorata se non si utilizza l'opzione `/str:`.|  
  
## <a name="resgenexe-and-resource-file-types"></a>Resgen.exe e i tipi di file di risorse  
 Per una corretta conversione delle risorse tramite Resgen.exe, è necessario che i file di testo e .resx abbiano il formato corretto.  
  
### <a name="text-txt-and-restext-files"></a>File di testo (.txt e .restext)  
 I file di testo (.txt o .restext) possono contenere solo risorse di tipo stringa. Le risorse di tipo stringa sono utili se si scrive un'applicazione contenente stringhe che dovranno essere tradotte in varie lingue. È ad esempio possibile localizzare facilmente le stringhe dei menu utilizzando la risorsa di tipo stringa appropriata. Resgen.exe legge i file di testo che contengono coppie nome/valore, dove il nome è una stringa che descrive la risorsa e il valore è la stringa risorsa stessa.  
  
> [!NOTE]
> Per informazioni sul formato dei file TXT e RESTEXT, vedere la sezione "Risorse in file di testo" in [Creazione di file di risorse](../resources/creating-resource-files-for-desktop-apps.md).  
  
 Un file di testo contenente risorse deve essere salvato con codifica UTF-8 o Unicode (UTF-16) a meno che contenga solo caratteri nell'intervallo Latino di base (fino a U+007F). Resgen.exe rimuove i caratteri ANSI estesi quando elabora un file di testo che viene salvato utilizzando la codifica ANSI.  
  
 Resgen.exe controlla che il file di testo non contenga nomi di risorsa duplicati. Se sono presenti nomi di risorsa duplicati, verrà generato un avviso e i valori duplicati verranno ignorati.  
  
### <a name="resx-files"></a>File .resx  
 Il formato dei file di risorse .resx è composto da voci XML. Analogamente ai file di testo, è possibile specificare risorse di tipo stringa in tali voci. Uno dei principali vantaggi dei file .resx rispetto ai file di testo consiste nel fatto che i file .resx consentono anche di specificare o incorporare oggetti. Quando si visualizza un file .resx, è effettivamente possibile vedere il formato binario di un oggetto incorporato (ad esempio un'immagine) quando queste informazioni binarie fanno parte del manifesto della risorsa. Come per i file di testo, è possibile aprire un file .resx con un editor di testo (come il Blocco note o Microsoft Word) e scrivere, analizzare e modificare il contenuto. Tenere presente che questa operazione richiede una buona conoscenza dei tag XML e della struttura dei file .resx. Per altre informazioni sul formato dei file RESX, vedere la sezione "Risorse in file RESX" in [Creazione di file di risorse](../resources/creating-resource-files-for-desktop-apps.md).  
  
 Al fine di creare un file .resources contenente oggetti incorporati non di tipo stringa, è necessario convertire, mediante Resgen.exe, un file .resx contenente oggetti oppure aggiungere le risorse di tipo oggetto al file direttamente dal codice, chiamando i metodi forniti dalla classe <xref:System.Resources.ResourceWriter>.  
  
 Se il file di risorse .resx o .resources contiene oggetti e si utilizza Resgen.exe per convertirli in un file di testo, tutte le risorse di tipo stringa verranno convertite correttamente, ma anche gli oggetti non di tipo stringa verranno scritti nel file sotto forma di stringhe. Gli oggetti incorporati andranno quindi persi nella conversione e verrà segnalato dallo strumento che si è verificato un errore nel recupero delle risorse.  
  
### <a name="converting-between-resources-file-types"></a>Conversione tra tipi di file di risorse  
 Quando si esegue la conversione tra tipi di file di risorse diverse, potrebbe non essere possibile eseguire la conversione con Resgen.exe o potrebbero andare perse informazioni su risorse specifiche, a seconda dei tipi di file di origine e di destinazione. Nella tabella seguente vengono specificati i tipi di conversione da un tipo di file di risorse ad un altro effettuabili senza problemi.  
  
|Conversione da|A file di testo|A file .resx|A file .resw|A file .resources|  
|------------------|------------------|-------------------|-------------------|------------------------|  
|File di testo (.txt o .restext)|--|Senza problemi|Non supportata|Senza problemi|  
|File .resx|La conversione non riesce se il file contiene risorse non di tipo stringa (inclusi i collegamenti a file)|--|Non supportata|Senza problemi|  
|File .resources|La conversione non riesce se il file contiene risorse non di tipo stringa (inclusi i collegamenti a file)|Senza problemi|Non supportata|--|  
|assembly .exe o .dll|Non supportate|Non supportate|Solo le risorse di tipo stringa (inclusi i nomi di percorso) vengono riconosciute come risorse|Non supportata|  
  
## <a name="performing-specific-resgenexe-tasks"></a>Esecuzione di specifiche attività di Resgen.exe  
 È possibile utilizzare Resgen.exe per diversi scopi: per la compilazione di un file di risorse basato su testo o su XML in un file binario, per la conversione tra formati di file di risorse e per la generazione di una classe che esegue il wrapping della funzionalità <xref:System.Resources.ResourceManager> e fornisce accesso alle risorse. In questa sezione vengono fornite informazioni dettagliate su ogni attività:  
  
- [Compilazione di risorse in un file binario](resgen-exe-resource-file-generator.md#Compiling)  
  
- [Conversione tra tipi di file di risorse](resgen-exe-resource-file-generator.md#Convert)  
  
- [Compilazione o conversione di più file](resgen-exe-resource-file-generator.md#Multiple)  
  
- [Esportazione di risorse in un file RESW](resgen-exe-resource-file-generator.md#Exporting)  
  
- [Compilazione condizionale di risorse](resgen-exe-resource-file-generator.md#Conditional)  
  
- [Generazione di una classe di risorse fortemente tipizzata](resgen-exe-resource-file-generator.md#Strong)  
  
<a name="Compiling"></a>
### <a name="compiling-resources-into-a-binary-file"></a>Compilazione di risorse in un file binario  
 L'utilizzo più comune di Resgen.exe consiste nel compilare un file di risorse basato su testo (file .restext o .txt) o un file di risorse basato su XML (file .resx) in un file .resources binario. Il file di output può quindi essere incorporato in un assembly principale tramite un compilatore di linguaggio o in un assembly satellite tramite [Assembly Linker (AL.exe)](al-exe-assembly-linker.md).  
  
 La sintassi per compilare un file di risorse è:  
  
```console  
resgen inputFilename [outputFilename]
```  
  
 dove i parametri sono:  
  
 `inputFilename`  
 Nome file, inclusa l'estensione, del file di risorse da compilare. Resgen.exe compila solo i file con estensione .txt, .restext o .resx.  
  
 `outputFilename`  
 Nome del file di output. Se si omette `outputFilename`, Resgen.exe crea un file .resources con il nome file radice di `inputFilename` nella stessa directory di `inputFilename`. Se `outputFilename` include un percorso di directory, la directory deve esistere.  
  
 Fornire uno spazio dei nomi completo per il file .resources specificandolo nel nome file e separandolo dal nome file radice con un punto. Ad esempio, se `outputFilename` è `MyCompany.Libraries.Strings.resources`, lo spazio dei nomi è MyCompany.Libraries.  
  
 Il seguente comando legge le coppie nome/valore in Resources.txt e scrive un file .resources binario denominato Resources.resources. Poiché il nome del file di output non viene specificato in modo esplicito, per impostazione predefinita assume lo stesso nome del file di input.  
  
```console  
resgen Resources.txt
```  
  
 Il seguente comando legge le coppie nome/valore in Resources.restext e scrive un file di risorse binario denominato StringResources.resources.  
  
```console  
resgen Resources.restext StringResources.resources  
```  
  
 Il seguente comando legge un file di input basato su XML denominato Resources.resx e scrive un file .resources binario denominato Resources.resources.  
  
```console  
resgen Resources.resx Resources.resources  
```  
  
<a name="Convert"></a>
### <a name="converting-between-resource-file-types"></a>Conversione tra tipi di file di risorse  
 Oltre a compilare file di risorse basati su testo o su XML in file .resources binari, Resgen.exe può convertire qualsiasi tipo di file supportato in qualsiasi altro tipo di file supportato. Ciò significa che è possibile effettuare le seguenti conversioni:  
  
- file .txt e .restext in file .resx  
  
- file .resx in file .txt e .restext  
  
- file .resources in file .txt e .restext  
  
- file .resources in file .resx  
  
 La sintassi è identica a quella mostrata nella sezione precedente.  
  
 Inoltre, è possibile utilizzare Resgen. exe per convertire le risorse incorporate in un assembly .NET Framework in un file con estensione resw Tor app Windows 8. x Store.  
  
 Il seguente comando legge un file di risorse binario Resources.resources e scrive un file di output basato su XML denominato Resources.resx.  
  
```console  
resgen Resources.resources Resources.resx  
```  
  
 Il seguente comando legge un file di risorse basato su testo denominato StringResources.txt e scrive un file di risorse basato su XML denominato LibraryResources.resx. Oltre a contenere le risorse di tipo stringa, il file .resx potrebbe anche essere utilizzato per archiviare risorse non di tipo stringa.  
  
```console  
resgen StringResources.txt LibraryResources.resx  
```  
  
 I seguenti due comandi leggono un file di risorse basato su XML denominato Resources.resx e scrivono file di testo denominati Resources.txt e Resources.restext. Tenere presente che, se il file .resx contiene oggetti incorporati, questi ultimi non verranno convertiti correttamente nei file di testo.  
  
```console  
resgen Resources.resx Resources.txt  
resgen Resources.resx Resources.restext  
```  
  
<a name="Multiple"></a>
### <a name="compiling-or-converting-multiple-files"></a>Compilazione o conversione di più file  
 È possibile utilizzare l'opzione `/compile` per convertire un elenco di file di risorse da un formato ad un altro con un'unica operazione. La sintassi è:  
  
```console  
resgen /compile filename.extension [filename.extension...]  
```  
  
 Il seguente comando compila tre file, StringResources.txt, TableResources.resw e ImageResources.resw, in file .resources separati denominati StringResources.resources, TableResources.resources e ImageResources.resources.  
  
```console  
resgen /compile StringResources.txt TableResources.resx ImageResources.resx  
```  
  
<a name="Exporting"></a>
### <a name="exporting-resources-to-a-resw-file"></a>Esportazione di risorse in un file .resw  
 Se stai sviluppando un'app di Windows 8. x Store, potresti voler usare le risorse di un'app desktop esistente. Tuttavia, i due tipi di applicazioni supportano formati di file diversi. Nelle app desktop, le risorse di testo (.txt o .restext) o i file .resx vengono compilati in file .resources binari. Nelle app di Windows 8. x Store, i file con estensione resw vengono compilati in file di indice delle risorse del pacchetto binario (PRI). È possibile utilizzare Resgen. exe per colmare questo gap estraendo le risorse da un file eseguibile o un assembly satellite e scrivendole in uno o più file con estensione resw che possono essere utilizzati durante lo sviluppo di un'app di Windows 8. x Store.  
  
> [!IMPORTANT]
> Visual Studio gestisce automaticamente tutte le conversioni necessarie per incorporare le risorse in una libreria portabile in un'app di Windows 8. x Store. L'utilizzo diretto di Resgen. exe per convertire le risorse in un assembly in un file con estensione resw è di grande interesse solo per gli sviluppatori che desiderano sviluppare un'app di Windows 8. x Store all'esterno di Visual Studio.  
  
 La sintassi per generare file .resw da un assembly è:  
  
```console  
resgen filename.extension  [outputDirectory]  
```  
  
 dove i parametri sono:  
  
 `filename.extension`  
 Nome di un assembly .NET Framework (file eseguibile o .DLL). Se il file non contiene risorse, non viene creato alcun file.  
  
 `outputDirectory`  
 Directory esistente in cui scrivere i file .resw. Se `outputDirectory` viene omesso, i file .resw vengono scritti nella directory corrente. Resgen.exe crea un file .resw per ogni file .resources nell'assembly. Il nome file radice del file .resw è uguale al nome radice del file .resources.  
  
 Il seguente comando crea un file .resw nella directory Win8Resources per ogni file .resources incorporato in MyApp.exe:  
  
```console  
resgen MyApp.exe Win8Resources  
```  
  
<a name="Conditional"></a>
### <a name="conditionally-compiling-resources"></a>Compilazione condizionale di risorse  
 A partire da .NET Framework 4.5, Resgen.exe supporta la compilazione condizionale delle risorse di tipo stringa in file di testo con estensione txt o restext. Questo consente di utilizzare un unico file di risorse basato su testo in più configurazioni della build.  
  
 In un file TXT o RESTEXT usare i costrutti `#ifdef`…`#endif` per includere una risorsa nel file RESOURCES binario se è definito un simbolo e usare il costrutto `#if !`... `#endif` per includere una risorsa se non è definito un simbolo. In fase di compilazione si definiscono quindi i simboli tramite l'opzione `/define:` seguita da un elenco di simboli delimitato da virgole. Nel confronto si fa distinzione tra maiuscole e minuscole; l'uso delle maiuscole/minuscole nei simboli definiti da `/define` deve corrispondere a quello nei simboli nei file di testo da compilare.  
  
 Ad esempio, il seguente file denominato UIResources.rext include una risorsa di tipo stringa denominata `AppTitle` che può assumere uno di tre valori, a seconda che siano definiti simboli denominati `PRODUCTION`, `CONSULT` o `RETAIL`.  
  
```text
#ifdef PRODUCTION  
AppTitle=My Software Company Project Manager
#endif  
#ifdef CONSULT  
AppTitle=My Consulting Company Project Manager  
#endif  
#ifdef RETAIL  
AppTitle=My Retail Store Project Manager  
#endif  
FileMenuName=File  
```  
  
 Il file può quindi essere compilato in un file .resources binario con il comando seguente:  
  
```console  
resgen /define:CONSULT UIResources.restext  
```  
  
 Viene generato un file .resources che contiene due risorse di tipo stringa. Il valore della risorsa `AppTitle` è "My Consulting Company Project Manager".  
  
<a name="Strong"></a>
### <a name="generating-a-strongly-typed-resource-class"></a>Generazione di una classe di risorse fortemente tipizzata  
 Resgen.ex supporta le risorse fortemente tipizzate, che incapsulano l'accesso alle risorse creando classi che contengono un set di proprietà statiche di sola lettura. Ciò costituisce un'alternativa alla chiamata diretta dei metodi della classe <xref:System.Resources.ResourceManager> per recuperare le risorse. È possibile abilitare il supporto per le risorse fortemente tipizzate utilizzando l'opzione `/str` in Resgen.exe, che esegue il wrapping della funzionalità della classe <xref:System.Resources.Tools.StronglyTypedResourceBuilder>. Quando si specifica l'opzione `/str`, l'output è una classe che contiene le proprietà fortemente tipizzate corrispondenti alle risorse a cui si fa riferimento nel parametro di input. Questa classe fornisce accesso fortemente tipizzato e in sola lettura alle risorse disponibili nel file elaborato.  
  
 La sintassi per creare una risorsa fortemente tipizzata è:  
  
```console  
resgen inputFilename [outputFilename] /str:language[,namespace,[classname[,filename]]] [/publicClass]  
```  
  
 I parametri e le opzioni sono:  
  
 `inputFilename`  
 Nome file, inclusa l'estensione, del file di risorse per il quale generare una classe di risorse fortemente tipizzata. Il file può essere basato su testo o su XML o può essere un file .resources binario; può avere l'estensione .txt, .restext, .resw o .resources.  
  
 `outputFilename`  
 Nome del file di output. Se `outputFilename` include un percorso di directory, la directory deve esistere. Se si omette `outputFilename`, Resgen.exe crea un file .resources con il nome file radice di `inputFilename` nella stessa directory di `inputFilename`.  
  
 `outputFilename` può essere un file basato su testo o su XML o un file .resources binario. Se l'estensione del file `outputFilename` è diversa dall'estensione del file `inputFilename`, Resgen.exe esegue la conversione del file.  
  
 Se `inputFilename` è un file .resources, Resgen.exe copia il file .resources se anche `outputFilename` è un file .resources. Se `outputFilename` viene omesso, Resgen.exe sovrascrive `inputFilename` con un file .resources identico.  
  
 *lingua*  
 Linguaggio in cui generare il codice sorgente per la classe di risorse fortemente tipizzata. I valori possibili sono `cs`, `C#` e `csharp` per il codice C#, `vb` e `visualbasic` per il codice Visual Basic, `vbs` e `vbscript` per il codice VBScript, `c++`, `mc` e `cpp` per il codice C++.  
  
 *namespace*  
 Spazio dei nomi che contiene la classe di risorse fortemente tipizzata. Il file .resources e la classe di risorse devono avere lo stesso spazio dei nomi. Per informazioni su come specificare lo spazio dei nomi in `outputFilename`, vedere [Compilazione di risorse in un file binario](resgen-exe-resource-file-generator.md#Compiling). Se *spazionomi* viene omesso, la classe di risorse non viene inclusa in uno spazio dei nomi.  
  
 *ClassName*  
 Nome della classe di risorse fortemente tipizzata. Deve corrispondere al nome radice del file .resources. Se ad esempio Resgen.exe genera un file .resources denominato MyCompany.Libraries.Strings.resources, il nome della classe di risorse fortemente tipizzata è Strings. Se *nomeclasse* viene omesso, la classe generata viene derivata dal nome radice di `outputFilename`. Se `outputFilename` viene omesso, la classe generata viene derivata dal nome radice di `inputFilename`.  
  
 *nomeclasse* non può contenere caratteri non validi, ad esempio spazi incorporati. Se *NomeClasse* contiene spazi incorporati o se *NomeClasse* viene generato per impostazione predefinita da *inputFilename*e *inputFilename* contiene spazi incorporati, Resgen. exe sostituisce tutti i caratteri non validi con un carattere di sottolineatura ( \_ ).  
  
 *filename*  
 Nome del file della classe.  
  
 `/publicclass`  
 Rende pubblica la classe di risorse fortemente tipizzata anziché `internal` (in C#) o `Friend` (in Visual Basic). In tal modo è possibile accedere alle risorse dall'esterno dell'assembly in cui sono incorporate.  
  
> [!IMPORTANT]
> Quando si crea una classe di risorse fortemente tipizzata, il nome del file .resources deve corrispondere a quello dello spazio dei nomi e della classe del codice generato. Tuttavia, Resgen.exe consente di specificare opzioni che generano un file .resources con un nome non compatibile. Per ovviare a questo problema, rinominare il file di output dopo che è stato generato.  
  
 La classe di risorse fortemente tipizzata include i seguenti membri:  
  
- Un costruttore senza parametri, che può essere usato per creare un'istanza della classe di risorse fortemente tipizzata.  
  
- Una proprietà `static``Shared` (C#) o `ResourceManager` (Visual Basic) e di sola lettura, che restituisce l'istanza di <xref:System.Resources.ResourceManager> che gestisce la risorsa fortemente tipizzata.  
  
- Una proprietà `Culture` statica, che consente di configurare le impostazioni cultura utilizzate per il recupero delle risorse. Per impostazione predefinita, il valore è `null`, che indica che vengono usate le impostazioni cultura dell'interfaccia utente correnti.  
  
- Una proprietà `static` (C#) o `Shared` (Visual Basic) di sola lettura per ogni risorsa nel file .resources. Il nome della proprietà è il nome della risorsa.  
  
 Ad esempio, il seguente comando compila un file di risorse denominato StringResources.txt in StringResources.resources e genera una classe denominata `StringResources` in un file di codice sorgente Visual Basic denominato StringResources.vb utilizzabile per accedere a Gestione risorse.  
  
```console  
resgen StringResources.txt /str:vb,,StringResources
```  
  
## <a name="see-also"></a>Vedere anche

- [Strumenti](index.md)
- [Risorse nelle applicazioni desktop](../resources/index.md)
- [Creazione dei file di risorsa](../resources/creating-resource-files-for-desktop-apps.md)
- [Al. exe (assembly linker)](al-exe-assembly-linker.md)
- [Prompt dei comandi](developer-command-prompt-for-vs.md)

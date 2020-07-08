---
title: 'Procedura: Creare, inizializzare e configurare opzioni di traccia'
description: Creare, inizializzare e configurare opzioni di traccia usando le classi System. Diagnostics. BooleanSwitch e System. Diagnostics. TraceSwitch in .NET.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- trace switches, configuring
- tracing [.NET Framework], trace switches
- switches, trace
- tracing [.NET Framework], enabling or disabling
- Web.config configuration file, trace switches
ms.assetid: 5a0e41bf-f99c-4692-8799-f89617f5bcf9
ms.openlocfilehash: 6a43e143abba96c841f04b7be9d482c55e78aa8f
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051324"
---
# <a name="how-to-create-initialize-and-configure-trace-switches"></a>Procedura: Creare, inizializzare e configurare opzioni di traccia
Le opzioni di traccia consentono di abilitare, disabilitare e filtrare l'output di traccia.  
  
<a name="create"></a>
## <a name="creating-and-initializing-a-trace-switch"></a>Creazione e inizializzazione di un'opzione di traccia  
 Per usare le opzioni di traccia, è necessario prima di tutto crearle e inserirle nel codice. Sono presenti due classi predefinite da cui è possibile creare oggetti opzione: <xref:System.Diagnostics.BooleanSwitch?displayProperty=nameWithType> e <xref:System.Diagnostics.TraceSwitch?displayProperty=nameWithType>. Si utilizza l'oggetto <xref:System.Diagnostics.BooleanSwitch> solo se è necessario stabilire se i messaggi di traccia vengono visualizzati; l'oggetto <xref:System.Diagnostics.TraceSwitch> viene invece utilizzato se è necessario distinguere tra i livelli di traccia. Se si utilizza un oggetto <xref:System.Diagnostics.TraceSwitch> è possibile definire messaggi di debug personalizzati e associarli a diversi livelli di traccia. È possibile usare entrambi i tipi di opzioni sia per la traccia sia per il debug. Per impostazione predefinita, un oggetto <xref:System.Diagnostics.BooleanSwitch> è disabilitato e un oggetto <xref:System.Diagnostics.TraceSwitch> è impostato sul livello <xref:System.Diagnostics.TraceLevel.Off?displayProperty=nameWithType>. È possibile creare e inserire opzioni di traccia in un punto qualsiasi del codice in cui possano essere usate.  
  
 Nonostante sia possibile impostare i livelli di traccia e altre opzioni di configurazione all'interno del codice, è consigliabile utilizzare il file di configurazione per gestire lo stato delle opzioni. Questo perché la gestione della configurazione delle opzioni nel sistema di configurazione consente una maggiore flessibilità: è infatti possibile attivare e disattivare diverse opzioni e modificare i livelli senza ricompilare l'applicazione.  
  
#### <a name="to-create-and-initialize-a-trace-switch"></a>Per creare e inizializzare un'opzione di traccia  
  
1. Definire un'opzione di tipo <xref:System.Diagnostics.BooleanSwitch?displayProperty=nameWithType> o <xref:System.Diagnostics.TraceSwitch?displayProperty=nameWithType> e impostare il nome e la descrizione dell'opzione.  
  
2. Configurare l'opzione di traccia. Per ulteriori informazioni, vedere [configurazione delle opzioni di traccia](#configure).  
  
     Il codice seguente crea due opzioni, una per ogni tipo:  
  
    ```vb  
    Dim dataSwitch As New BooleanSwitch("Data", "DataAccess module")  
    Dim generalSwitch As New TraceSwitch("General", "Entire application")  
    ```  
  
    ```csharp  
    System.Diagnostics.BooleanSwitch dataSwitch =
       new System.Diagnostics.BooleanSwitch("Data", "DataAccess module");  
    System.Diagnostics.TraceSwitch generalSwitch =
       new System.Diagnostics.TraceSwitch("General",
       "Entire application");  
    ```  
  
<a name="configure"></a>
## <a name="configuring-trace-switches"></a>Configurazione di opzioni di traccia  
 Una volta distribuita l'applicazione, è ancora possibile attivare o disabilitare l'output di traccia configurando le opzioni di traccia dell'applicazione. Configurare un'opzione significa modificarne il valore da un'origine esterna una volta inizializzata. È possibile modificare i valori degli oggetti opzione mediante il file di configurazione. Si configura un'opzione di traccia per attivarla e disabilitarla oppure per impostarne il livello, determinando la quantità e il tipo di messaggi da inviare ai listener.  
  
 Le opzioni vengono configurate tramite il file CONFIG. In caso di applicazioni Web si tratta del file Web.config associato al progetto. In un'applicazione Windows, questo file è denominato (nome applicazione) .exe.config. In un'applicazione distribuita, questo file deve trovarsi nella stessa cartella del file eseguibile.  
  
 Quando l'applicazione esegue il codice che crea un'istanza di un'opzione per la prima volta, viene verificata la presenza nel file di configurazione di informazioni sul livello di traccia relative all'opzione denominata. Il file di configurazione viene esaminato dal sistema di tracciatura solo una volta per ogni opzione, la prima volta che l'opzione in questione viene creata dall'applicazione.  
  
 In un'applicazione distribuita, il codice di traccia viene abilitato riconfigurando gli oggetti opzione quando l'applicazione non è in esecuzione. In genere questo implica l'attivazione e la disattivazione degli oggetti opzione o la modifica dei livelli di traccia, quindi il riavvio dell'applicazione.  
  
 Quando si crea un'istanza di un'opzione, la si inizializza anche specificando due argomenti: un argomento *displayName* e un argomento *description*. L'argomento *displayName* del costruttore imposta la proprietà <xref:System.Diagnostics.Switch.DisplayName%2A?displayProperty=nameWithType> dell'istanza della classe <xref:System.Diagnostics.Switch>. L'argomento* displayName* rappresenta il nome usato per configurare l'opzione nel file CONFIG, mentre l'argomento *description* restituisce una breve descrizione dell'opzione e dei messaggi che controlla.  
  
 Oltre a specificare il nome di un'opzione da configurare, è necessario specificare un valore per l'opzione.  Tale valore deve essere Integer. Per <xref:System.Diagnostics.BooleanSwitch>, un valore pari a 0 corrisponde a **Off**, mentre un valore diverso da 0 corrisponde a **On**. Per la classe <xref:System.Diagnostics.TraceSwitch>, 0,1,2,3 e 4 corrispondono rispettivamente a **Off**, **Error**, **Warning**, **Info** e **Verbose**. Tutti i numeri maggiori di 4 vengono considerati come **Verbose**, tutti i numeri minori di zero vengono considerati **Off**.  
  
> [!NOTE]
> In .NET Framework versione 2.0 è possibile usare testo per specificare il valore di un'opzione, ad esempio `true` per la classe <xref:System.Diagnostics.BooleanSwitch> o il testo che rappresenta un valore di enumerazione, come `Error` per la classe <xref:System.Diagnostics.TraceSwitch>. La riga `<add name="myTraceSwitch" value="Error" />` equivale a `<add name="myTraceSwitch" value="1" />`.  
  
 Per consentire all'utente finale di configurare un'opzione di traccia di un'applicazione, è necessario fornire una documentazione dettagliata delle opzioni nell'applicazione. Devono essere descritte in dettaglio le opzioni, ciò che controllano e le modalità di attivazione e disattivazione. È inoltre necessario fornire all'utente finale un file CONFIG dotato di una Guida adeguata nei commenti.  
  
#### <a name="to-configure-trace-switches"></a>Per configurare opzioni di traccia  
  
1. Per usare le opzioni di traccia, è necessario prima di tutto crearle e inserirle nel codice, come descritto nella sezione [Creazione e inizializzazione di un'opzione di traccia](#create).  
  
2. Se il progetto non contiene un file di configurazione (app.config o Web.config), scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
    - **Visual Basic:** nella finestra di dialogo **Aggiungi nuovo elemento** scegliere **File di configurazione dell'applicazione**.  
  
         Verrà creato e aperto il file di configurazione dell'applicazione. Si tratta di un documento XML il cui elemento radice è `<configuration>.`  
  
    - **Visual C#:** nella finestra di dialogo **Aggiungi nuovo elemento** fare clic su **File XML**. Assegnare al file il nome **app.config**. Nell'editor XML, dopo la dichiarazione XML, aggiungere il codice XML seguente:  
  
        ```xml  
        <configuration>  
        </configuration>  
        ```  
  
         Una volta compilato il progetto, il file app.config viene copiato nella cartella di output del progetto e rinominato *nomeapplicazione*.exe.config.  
  
3. Dopo il tag `<configuration>`, ma prima del tag `</configuration>`, aggiungere il codice XML appropriato per la configurazione delle opzioni. Gli esempi seguenti illustrano un oggetto **BooleanSwitch** con una proprietà **DisplayName** di `DataMessageSwitch` e un oggetto **TraceSwitch** con una proprietà **DisplayName** di `TraceLevelSwitch`.  
  
    ```xml  
    <system.diagnostics>  
       <switches>  
          <add name="DataMessagesSwitch" value="0" />  
          <add name="TraceLevelSwitch" value="0" />  
       </switches>  
    </system.diagnostics>  
    ```  
  
     In questa configurazione entrambe le opzioni sono disabilitate.  
  
4. Se è necessario attivare un **BooleanSwitch**, come `DataMessagesSwitch` illustrato nell'esempio precedente, impostare **Value** su qualsiasi intero diverso da 0.  
  
5. Se è necessario attivare un **TraceSwitch**, come `TraceLevelSwitch` illustrato nell'esempio precedente, impostare **Value** sul livello appropriato (da 1 a 4).  
  
6. Aggiungere commenti al file CONFIG in modo che l'utente possa comprendere chiaramente quali valori modificare per configurare correttamente le opzioni.  
  
     L'esempio seguente mostra come può apparire il codice finale, comprensivo di commenti:  
  
    ```xml  
    <system.diagnostics>  
       <switches>  
          <!-- This switch controls data messages. In order to receive data   
             trace messages, change value="0" to value="1" -->  
          <add name="DataMessagesSwitch" value="0" />  
          <!-- This switch controls general messages. In order to   
             receive general trace messages change the value to the   
             appropriate level. "1" gives error messages, "2" gives errors   
             and warnings, "3" gives more detailed error information, and   
             "4" gives verbose trace information -->  
          <add name="TraceLevelSwitch" value="0" />  
       </switches>  
    </system.diagnostics>  
    ```  
  
## <a name="see-also"></a>Vedere anche

- [Traccia e strumentazione di applicazioni](tracing-and-instrumenting-applications.md)
- [Procedura: aggiungere istruzioni di traccia al codice dell'applicazione](how-to-add-trace-statements-to-application-code.md)
- [Opzioni di traccia](trace-switches.md)
- [Schema delle impostazioni di traccia e debug](../configure-apps/file-schema/trace-debug/index.md)

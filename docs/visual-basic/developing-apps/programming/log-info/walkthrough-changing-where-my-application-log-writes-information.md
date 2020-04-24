---
title: Modifica della posizione di inserimento delle informazioni con My.Application.Log
ms.date: 07/20/2015
helpviewer_keywords:
- My.Application.Log object, walkthroughs
- event logs, changing output location
ms.assetid: ecc74f95-743c-450d-93f6-09a30db0fe4a
ms.openlocfilehash: bdee0a91360580b156c1734ef4c82139b18ce2b5
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2020
ms.locfileid: "74336728"
---
# <a name="walkthrough-changing-where-myapplicationlog-writes-information-visual-basic"></a>Procedura dettagliata: modifica della posizione di inserimento delle informazioni con My.Application.Log (Visual Basic)

È possibile usare gli oggetti `My.Application.Log` e `My.Log` per registrare informazioni sugli eventi che si verificano nell'applicazione. Questa procedura dettagliata mostra come eseguire l'override delle impostazioni predefinite e fare in modo che l'oggetto `Log` scriva le informazioni in altri listener di log.

## <a name="prerequisites"></a>Prerequisiti

L'oggetto `Log` può scrivere le informazioni in diversi listener di log. Prima di modificare le configurazioni dei listener di log è necessario determinarne la configurazione corrente. Per altre informazioni, vedere [Procedura dettagliata: Individuazione della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md).

Si consiglia di consultare la [Procedura: Scrivere informazioni sugli eventi in un file di testo](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-event-information-to-a-text-file.md) o [Procedura: Scrivere nel registro eventi di un'applicazione](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-to-an-application-event-log.md).

### <a name="to-add-listeners"></a>Per aggiungere listener

1. Fare clic con il pulsante destro del mouse sul file app.config in **Esplora soluzioni** , quindi scegliere **Apri**.

     \- - oppure -

     Se non è presente alcun file app.config:

    1. Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.

    2. Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **File di configurazione dell'applicazione**.

    3. Fare clic su **Aggiungi**.

2. Individuare la sezione `<listeners>` all'interno della sezione `<source>` con l'attributo `name` "DefaultSource" che si trova nella sezione `<sources>` . La sezione `<sources>` si trova nella sezione `<system.diagnostics>` all'interno della sezione di primo livello `<configuration>` .

3. Aggiungere gli elementi seguenti alla sezione `<listeners>` .

    ```xml
    <!-- Uncomment to connect the application file log. -->
    <!-- <add name="FileLog" /> -->
    <!-- Uncomment to connect the event log. -->
    <!-- <add name="EventLog" /> -->
    <!-- Uncomment to connect the event log. -->
    <!-- <add name="Delimited" /> -->
    <!-- Uncomment to connect the XML log. -->
    <!-- <add name="XmlWriter" /> -->
    <!-- Uncomment to connect the console log. -->
    <!-- <add name="Console" /> -->
    ```

4. Rimuovere il commento dai listener di log per i quali si vuole ricevere i messaggi di `Log` .

5. Individuare la sezione `<sharedListeners>` nella sezione `<system.diagnostics>` all'interno della sezione di primo livello `<configuration>` .

6. Aggiungere gli elementi seguenti alla sezione `<sharedListeners>` .

    ```xml
    <add name="FileLog"
         type="Microsoft.VisualBasic.Logging.FileLogTraceListener,
               Microsoft.VisualBasic, Version=8.0.0.0,
               Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"
         initializeData="FileLogWriter" />
    <add name="EventLog"
         type="System.Diagnostics.EventLogTraceListener,
               System, Version=2.0.0.0,
               Culture=neutral, PublicKeyToken=b77a5c561934e089"
         initializeData="sample application"/>
    <add name="Delimited"
         type="System.Diagnostics.DelimitedListTraceListener,
               System, Version=2.0.0.0,
               Culture=neutral, PublicKeyToken=b77a5c561934e089"
         initializeData="c:\temp\sampleDelimitedFile.txt"
         traceOutputOptions="DateTime" />
    <add name="XmlWriter"
         type="System.Diagnostics.XmlWriterTraceListener,
               System, Version=2.0.0.0,
               Culture=neutral, PublicKeyToken=b77a5c561934e089"
         initializeData="c:\temp\sampleLogFile.xml" />
    <add name="Console"
         type="System.Diagnostics.ConsoleTraceListener,
               System, Version=2.0.0.0,
               Culture=neutral, PublicKeyToken=b77a5c561934e089"
         initializeData="true" />
    ```

7. Il contenuto del file app.config dovrebbe essere simile al codice XML seguente.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <system.diagnostics>
        <sources>
          <!-- This section configures My.Application.Log -->
          <source name="DefaultSource" switchName="DefaultSwitch">
            <listeners>
              <add name="FileLog"/>
              <!-- Uncomment to connect the application file log. -->
              <!-- <add name="FileLog" /> -->
              <!-- Uncomment to connect the event log. -->
              <!-- <add name="EventLog" /> -->
              <!-- Uncomment to connect the event log. -->
              <!-- <add name="Delimited" /> -->
              <!-- Uncomment to connect the XML log. -->
              <!-- <add name="XmlWriter" /> -->
              <!-- Uncomment to connect the console log. -->
              <!-- <add name="Console" /> -->
            </listeners>
          </source>
        </sources>
        <switches>
          <add name="DefaultSwitch" value="Information" />
        </switches>
        <sharedListeners>
          <add name="FileLog"
               type="Microsoft.VisualBasic.Logging.FileLogTraceListener,
                     Microsoft.VisualBasic, Version=8.0.0.0,
                     Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"
               initializeData="FileLogWriter" />
          <add name="EventLog"
               type="System.Diagnostics.EventLogTraceListener,
                     System, Version=2.0.0.0,
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"
               initializeData="sample application"/>
          <add name="Delimited"
               type="System.Diagnostics.DelimitedListTraceListener,
                     System, Version=2.0.0.0,
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"
               initializeData="c:\temp\sampleDelimitedFile.txt"
               traceOutputOptions="DateTime" />
          <add name="XmlWriter"
               type="System.Diagnostics.XmlWriterTraceListener,
                     System, Version=2.0.0.0,
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"
               initializeData="c:\temp\sampleLogFile.xml" />
          <add name="Console"
               type="System.Diagnostics.ConsoleTraceListener,
                     System, Version=2.0.0.0,
                     Culture=neutral, PublicKeyToken=b77a5c561934e089"
               initializeData="true" />
        </sharedListeners>
      </system.diagnostics>
    </configuration>
    ```

### <a name="to-reconfigure-a-listener"></a>Per riconfigurare un listener

1. Individuare l'elemento `<add>` del listener nella sezione `<sharedListeners>` .

2. L'attributo `type` fornisce il nome del tipo di listener. Questo tipo deve ereditare dalla classe <xref:System.Diagnostics.TraceListener> . Usare il tipo con nome sicuro per assicurarsi di usare il tipo corretto. Per altre informazioni, vedere la sezione seguente "Per aggiungere riferimenti a un tipo con nome sicuro".

     Di seguito sono riportati alcuni esempi di listener che si possono usare.

    - Il listener <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=nameWithType> , che scrive le informazioni in un log file.

    - Il listener <xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType> , che scrive le informazioni nel log eventi del computer specificato dal parametro `initializeData` .

    - I listener <xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=nameWithType> e <xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType> , che scrivono le informazioni nel file specificato nel parametro `initializeData` .

    - Il listener <xref:System.Diagnostics.ConsoleTraceListener?displayProperty=nameWithType> , che scrive le informazioni nella console della riga di comando.

     Per sapere dove gli altri tipi di listener di log scrivono le informazioni, consultare la documentazione relativa al tipo di listener desiderato.

3. Quando crea l'oggetto listener di log, l'applicazione passa l'attributo `initializeData` come parametro del costruttore. Il significato dell'attributo `initializeData` dipende dal listener di traccia.

4. Dopo aver creato il listener di log, l'applicazione imposta le proprietà del listener. Tali proprietà sono definite dagli altri attributi contenuti nell'elemento `<add>` . Per altre informazioni sulle proprietà di un determinato listener, consultare la documentazione relativa al tipo di listener corrispondente.

### <a name="to-reference-a-strongly-named-type"></a>Per aggiungere riferimenti a un tipo con nome sicuro

1. Per assicurarsi di usare il tipo di listener di log appropriato, usare il nome di tipo completo e il nome di assembly sicuro. La sintassi di un tipo con nome sicuro è la seguente:

     \<*nome tipo*>, \<*nome assembly*>, \<*numero versione*>, \<*impostazioni cultura*>, \<*nome sicuro*>

2. L'esempio di codice seguente mostra come determinare il tipo con nome sicuro per un tipo completo, in questo caso "System.Diagnostics.FileLogTraceListener".

     [!code-vb[VbVbalrMyApplicationLog#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#15)]

     Questo è l'output, e può essere usato per aggiungere riferimenti univoci a un tipo con nome sicuro, come nella procedura "Per aggiungere listener" precedente.

     `Microsoft.VisualBasic.Logging.FileLogTraceListener, Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a`

## <a name="see-also"></a>Vedi anche

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:System.Diagnostics.TraceListener>
- <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener?displayProperty=nameWithType>
- <xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType>
- [Procedura: Scrivere informazioni sugli eventi in un file di testo](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-event-information-to-a-text-file.md)
- [Procedura: Scrivere nel log eventi di un'applicazione](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-to-an-application-event-log.md)

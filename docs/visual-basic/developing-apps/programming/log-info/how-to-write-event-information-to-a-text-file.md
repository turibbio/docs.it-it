---
title: 'Procedura: Scrivere informazioni sugli eventi in un file di testo'
ms.date: 07/20/2015
helpviewer_keywords:
- event logs [Visual Studio], writing event information
- text files [Visual Basic], writing event information to a text file
- events [Visual Basic], writing event information to a text file
ms.assetid: 9ca7cc03-bf99-4933-9e5e-61ee28e9a6b4
ms.openlocfilehash: c3c81e331eb3d8ee450ba0cac38e57976846ee63
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2020
ms.locfileid: "74352078"
---
# <a name="how-to-write-event-information-to-a-text-file-visual-basic"></a>Procedura: scrivere informazioni sugli eventi in un file di testo (Visual Basic)

È possibile usare gli oggetti `My.Application.Log` e `My.Log` per registrare informazioni sugli eventi che si verificano nell'applicazione. Questo esempio illustra come usare il metodo `My.Application.Log.WriteEntry` per registrare le informazioni di traccia in un file di log.

### <a name="to-add-and-configure-the-file-log-listener"></a>Per aggiungere e configurare il listener di log del file

1. Fare clic con il pulsante destro del mouse sul file app.config in **Esplora soluzioni** , quindi scegliere **Apri**.

     \- - oppure -

     Se non è presente alcun file app.config:

    1. Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.

    2. Nella finestra di dialogo **Aggiungi nuovo elemento** scegliere **File di configurazione dell'applicazione**.

    3. Fare clic su **Aggiungi**.

2. Individuare la sezione `<listeners>` nel file di configurazione dell'applicazione.

     La sezione \<listeners> si trova nella sezione \<source> con l'attributo del nome "DefaultSource" annidato sotto la sezione \<system.diagnostics>, a sua volta annidata sotto la sezione \<configuration> di primo livello.

3. Aggiungere l'elemento seguente alla sezione `<listeners>` :

    ```xml
    <add name="FileLogListener" />
    ```

4. Individuare la sezione `<sharedListeners>` nella sezione `<system.diagnostics>` annidata sotto la sezione `<configuration>` di primo livello.

5. Aggiungere l'elemento seguente alla sezione `<sharedListeners>` :

    ```xml
    <add name="FileLogListener"
        type="Microsoft.VisualBasic.Logging.FileLogTraceListener,
              Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral,
              PublicKeyToken=b03f5f7f11d50a3a"
        initializeData="FileLogListenerWriter"
        location="Custom"
        customlocation="c:\temp\" />
    ```

     Modificare il valore dell'attributo `customlocation` impostandolo sulla directory del log.

    > [!NOTE]
    > Per impostare il valore di una proprietà del listener, usare un attributo con lo stesso nome della proprietà e con tutte le lettere nel nome scritte in minuscolo. Ad esempio, gli attributi `location` e `customlocation` consentono di impostare i valori delle proprietà <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.Location%2A> e <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.CustomLocation%2A>.

### <a name="to-write-event-information-to-the-file-log"></a>Per scrivere le informazioni sugli eventi nel log del file

Usare il metodo `My.Application.Log.WriteEntry` o `My.Application.Log.WriteException` per scrivere le informazioni nel log del file. Per altre informazioni, vedere [Procedura: Scrivere messaggi di log ](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md) e [Procedura: Registrare eccezioni](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md).

Dopo aver configurato il listener del log del file per un assembly, vengono ricevuti tutti i messaggi che `My.Application.Log` scrive da tale assembly.

## <a name="see-also"></a>Vedi anche

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)
- [Procedura: Registrare eccezioni](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)

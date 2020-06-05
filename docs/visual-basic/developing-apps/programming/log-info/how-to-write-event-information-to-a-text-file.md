---
title: 'Procedura: Scrivere informazioni sugli eventi in un file di testo'
ms.date: 07/20/2015
helpviewer_keywords:
- event logs [Visual Studio], writing event information
- text files [Visual Basic], writing event information to a text file
- events [Visual Basic], writing event information to a text file
ms.assetid: 9ca7cc03-bf99-4933-9e5e-61ee28e9a6b4
ms.openlocfilehash: 6e83f8450ca7be8a2dcd5ff43eab3dd2ec0d2f1b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410062"
---
# <a name="how-to-write-event-information-to-a-text-file-visual-basic"></a><span data-ttu-id="026c2-102">Procedura: scrivere informazioni sugli eventi in un file di testo (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="026c2-102">How to: Write Event Information to a Text File (Visual Basic)</span></span>

<span data-ttu-id="026c2-103">È possibile usare gli oggetti `My.Application.Log` e `My.Log` per registrare informazioni sugli eventi che si verificano nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="026c2-103">You can use the `My.Application.Log` and `My.Log` objects to log information about events that occur in your application.</span></span> <span data-ttu-id="026c2-104">Questo esempio illustra come usare il metodo `My.Application.Log.WriteEntry` per registrare le informazioni di traccia in un file di log.</span><span class="sxs-lookup"><span data-stu-id="026c2-104">This example shows how to use the `My.Application.Log.WriteEntry` method to log tracing information to a log file.</span></span>

### <a name="to-add-and-configure-the-file-log-listener"></a><span data-ttu-id="026c2-105">Per aggiungere e configurare il listener di log del file</span><span class="sxs-lookup"><span data-stu-id="026c2-105">To add and configure the file log listener</span></span>

1. <span data-ttu-id="026c2-106">Fare clic con il pulsante destro del mouse sul file app.config in **Esplora soluzioni** , quindi scegliere **Apri**.</span><span class="sxs-lookup"><span data-stu-id="026c2-106">Right-click app.config in **Solution Explorer** and choose **Open**.</span></span>

     <span data-ttu-id="026c2-107">\- - oppure -</span><span class="sxs-lookup"><span data-stu-id="026c2-107">\- or -</span></span>

     <span data-ttu-id="026c2-108">Se non è presente alcun file app.config:</span><span class="sxs-lookup"><span data-stu-id="026c2-108">If there is no app.config file:</span></span>

    1. <span data-ttu-id="026c2-109">Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="026c2-109">On the **Project** menu, choose **Add New Item**.</span></span>

    2. <span data-ttu-id="026c2-110">Nella finestra di dialogo **Aggiungi nuovo elemento** scegliere **File di configurazione dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="026c2-110">From the **Add New Item** dialog box, choose **Application Configuration File**.</span></span>

    3. <span data-ttu-id="026c2-111">Scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="026c2-111">Click **Add**.</span></span>

2. <span data-ttu-id="026c2-112">Individuare la sezione `<listeners>` nel file di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="026c2-112">Locate the `<listeners>` section in the application configuration file.</span></span>

     <span data-ttu-id="026c2-113">La sezione \<listeners> si trova nella sezione \<source> con l'attributo del nome "DefaultSource" annidato sotto la sezione \<system.diagnostics> a sua volta annidata sotto la sezione di primo livello \<configuration> .</span><span class="sxs-lookup"><span data-stu-id="026c2-113">You will find the \<listeners> section in the \<source> section with the name attribute "DefaultSource", which is nested under the \<system.diagnostics> section, which is nested under the top-level \<configuration> section.</span></span>

3. <span data-ttu-id="026c2-114">Aggiungere l'elemento seguente alla sezione `<listeners>` :</span><span class="sxs-lookup"><span data-stu-id="026c2-114">Add this element to that `<listeners>` section:</span></span>

    ```xml
    <add name="FileLogListener" />
    ```

4. <span data-ttu-id="026c2-115">Individuare la sezione `<sharedListeners>` nella sezione `<system.diagnostics>` annidata sotto la sezione `<configuration>` di primo livello.</span><span class="sxs-lookup"><span data-stu-id="026c2-115">Locate the `<sharedListeners>` section in the `<system.diagnostics>` section, nested under the top-level `<configuration>` section.</span></span>

5. <span data-ttu-id="026c2-116">Aggiungere l'elemento seguente alla sezione `<sharedListeners>` :</span><span class="sxs-lookup"><span data-stu-id="026c2-116">Add this element to that `<sharedListeners>` section:</span></span>

    ```xml
    <add name="FileLogListener"
        type="Microsoft.VisualBasic.Logging.FileLogTraceListener,
              Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral,
              PublicKeyToken=b03f5f7f11d50a3a"
        initializeData="FileLogListenerWriter"
        location="Custom"
        customlocation="c:\temp\" />
    ```

     <span data-ttu-id="026c2-117">Modificare il valore dell'attributo `customlocation` impostandolo sulla directory del log.</span><span class="sxs-lookup"><span data-stu-id="026c2-117">Change the value of the `customlocation` attribute to the log directory.</span></span>

    > [!NOTE]
    > <span data-ttu-id="026c2-118">Per impostare il valore di una proprietà del listener, usare un attributo con lo stesso nome della proprietà e con tutte le lettere nel nome scritte in minuscolo.</span><span class="sxs-lookup"><span data-stu-id="026c2-118">To set the value of a listener property, use an attribute that has the same name as the property, with all letters in the name lowercase.</span></span> <span data-ttu-id="026c2-119">Ad esempio, gli attributi `location` e `customlocation` consentono di impostare i valori delle proprietà <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.Location%2A> e <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.CustomLocation%2A>.</span><span class="sxs-lookup"><span data-stu-id="026c2-119">For example, the `location` and `customlocation` attributes set the values of the <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.Location%2A> and <xref:Microsoft.VisualBasic.Logging.FileLogTraceListener.CustomLocation%2A> properties.</span></span>

### <a name="to-write-event-information-to-the-file-log"></a><span data-ttu-id="026c2-120">Per scrivere le informazioni sugli eventi nel log del file</span><span class="sxs-lookup"><span data-stu-id="026c2-120">To write event information to the file log</span></span>

<span data-ttu-id="026c2-121">Usare il metodo `My.Application.Log.WriteEntry` o `My.Application.Log.WriteException` per scrivere le informazioni nel log del file.</span><span class="sxs-lookup"><span data-stu-id="026c2-121">Use the `My.Application.Log.WriteEntry` or `My.Application.Log.WriteException` method to write information to the file log.</span></span> <span data-ttu-id="026c2-122">Per altre informazioni, vedere [Procedura: Scrivere messaggi di log ](how-to-write-log-messages.md) e [Procedura: Registrare eccezioni](how-to-log-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="026c2-122">For more information, see [How to: Write Log Messages](how-to-write-log-messages.md) and [How to: Log Exceptions](how-to-log-exceptions.md).</span></span>

<span data-ttu-id="026c2-123">Dopo aver configurato il listener del log del file per un assembly, vengono ricevuti tutti i messaggi che `My.Application.Log` scrive da tale assembly.</span><span class="sxs-lookup"><span data-stu-id="026c2-123">After you configure the file log listener for an assembly, it receives all messages that `My.Application.Log` writes from that assembly.</span></span>

## <a name="see-also"></a><span data-ttu-id="026c2-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="026c2-124">See also</span></span>

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [<span data-ttu-id="026c2-125">Utilizzo dei log applicazione</span><span class="sxs-lookup"><span data-stu-id="026c2-125">Working with Application Logs</span></span>](working-with-application-logs.md)
- [<span data-ttu-id="026c2-126">Procedura: Registrare eccezioni</span><span class="sxs-lookup"><span data-stu-id="026c2-126">How to: Log Exceptions</span></span>](how-to-log-exceptions.md)

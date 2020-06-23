---
title: 'Codificatore di messaggi personalizzati: Codificatore di testo personalizzato'
description: Utilizzare questo esempio per implementare un codificatore di messaggi di testo personalizzato tramite WCF. Questo codificatore supporta tutte le codifiche dei caratteri supportate dalla piattaforma per l'interoperabilità.
ms.date: 03/30/2017
ms.assetid: 68ff5c74-3d33-4b44-bcae-e1d2f5dea0de
ms.openlocfilehash: 88ddc79e6cc1df654aea851cedb0e60c6fbcd017
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246272"
---
# <a name="custom-message-encoder-custom-text-encoder"></a><span data-ttu-id="dc873-104">Codificatore di messaggi personalizzati: Codificatore di testo personalizzato</span><span class="sxs-lookup"><span data-stu-id="dc873-104">Custom Message Encoder: Custom Text Encoder</span></span>

<span data-ttu-id="dc873-105">In questo esempio viene illustrato come implementare un codificatore di messaggi di testo personalizzato utilizzando Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="dc873-105">This sample demonstrates how to implement a custom text message encoder using Windows Communication Foundation (WCF).</span></span>

> [!WARNING]
> <span data-ttu-id="dc873-106">È possibile che gli esempi siano già installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="dc873-106">The samples may already be installed on your machine.</span></span> <span data-ttu-id="dc873-107">Verificare la directory seguente (impostazione predefinita) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="dc873-107">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="dc873-108">Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) ed [!INCLUDE[wf1](../../../../includes/wf1-md.md)] esempi.</span><span class="sxs-lookup"><span data-stu-id="dc873-108">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="dc873-109">Questo esempio si trova nella directory seguente.</span><span class="sxs-lookup"><span data-stu-id="dc873-109">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\MessageEncoder\Text`

<span data-ttu-id="dc873-110"><xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>Di WCF supporta solo le codifiche Unicode UTF-8, UTF-16 e Big-endian.</span><span class="sxs-lookup"><span data-stu-id="dc873-110">The <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> of WCF supports only the UTF-8, UTF-16 and big-endian Unicode encodings.</span></span> <span data-ttu-id="dc873-111">Il codificatore di messaggi di testo personalizzato in questo esempio supporta tutte le codifiche dei caratteri supportate dalla piattaforma che potrebbero essere necessarie per l'interoperabilità.</span><span class="sxs-lookup"><span data-stu-id="dc873-111">The custom text message encoder in this sample supports all platform-supported character encodings that may be required for interoperability.</span></span> <span data-ttu-id="dc873-112">L'esempio è costituito da un programma di console client (con estensione exe), da una libreria di servizi (. dll) ospitata da Internet Information Services (IIS) e da una libreria del codificatore di messaggi di testo (con estensione dll).</span><span class="sxs-lookup"><span data-stu-id="dc873-112">The sample consists of a client console program (.exe), a service library (.dll) hosted by Internet Information Services (IIS), and a text message encoder library (.dll).</span></span> <span data-ttu-id="dc873-113">Il servizio implementa un contratto che definisce un modello di comunicazione richiesta/risposta.</span><span class="sxs-lookup"><span data-stu-id="dc873-113">The service implements a contract that defines a request-reply communication pattern.</span></span> <span data-ttu-id="dc873-114">Il contratto è definito dall'interfaccia `ICalculator`, che espone operazioni matematiche (somma, sottrazione, moltiplicazione e divisione).</span><span class="sxs-lookup"><span data-stu-id="dc873-114">The contract is defined by the `ICalculator` interface, which exposes math operations (Add, Subtract, Multiply, and Divide).</span></span> <span data-ttu-id="dc873-115">Il client esegue richieste sincrone a un'operazione matematica specificata e il servizio risponde fornendo il risultato.</span><span class="sxs-lookup"><span data-stu-id="dc873-115">The client makes synchronous requests to a given math operation and the service replies with the result.</span></span> <span data-ttu-id="dc873-116">Il client e il servizio utilizzano `CustomTextMessageEncoder` anziché la classe <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> predefinita.</span><span class="sxs-lookup"><span data-stu-id="dc873-116">Both client and service uses the `CustomTextMessageEncoder` instead of the default <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>.</span></span>

<span data-ttu-id="dc873-117">L'implementazione del codificatore personalizzato è costituita da una factory del codificatore di messaggi, un codificatore di messaggi, un messaggio che codifica l'elemento di associazione e un gestore di configurazione, e illustra quanto segue:</span><span class="sxs-lookup"><span data-stu-id="dc873-117">The custom encoder implementation consists of a message encoder factory, a message encoder, a message encoding binding element and a configuration handler, and demonstrates the following:</span></span>

- <span data-ttu-id="dc873-118">Compilazione di un codificatore personalizzato e di una factory del codificatore.</span><span class="sxs-lookup"><span data-stu-id="dc873-118">Building a custom encoder and encoder factory.</span></span>

- <span data-ttu-id="dc873-119">Creazione di un elemento di associazione per un codificatore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc873-119">Creating a binding element for a custom encoder.</span></span>

- <span data-ttu-id="dc873-120">Utilizzo della configurazione dell'associazione personalizzata per l'integrazione di elementi di associazione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="dc873-120">Using the custom binding configuration for integrating custom binding elements.</span></span>

- <span data-ttu-id="dc873-121">Sviluppo di un gestore di configurazione personalizzato per consentire la configurazione del file di un elemento di associazione personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc873-121">Developing a custom configuration handler to allow file configuration of a custom binding element.</span></span>

## <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="dc873-122">Per impostare, compilare ed eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="dc873-122">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="dc873-123">Installare ASP.NET 4,0 usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="dc873-123">Install ASP.NET 4.0 using the following command.</span></span>

    ```console
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable
    ```

2. <span data-ttu-id="dc873-124">Assicurarsi di avere eseguito la [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dc873-124">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

3. <span data-ttu-id="dc873-125">Per compilare la soluzione, seguire le istruzioni riportate in [compilazione degli esempi di Windows Communication Foundation](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dc873-125">To build the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

4. <span data-ttu-id="dc873-126">Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [esecuzione degli esempi di Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dc873-126">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>

## <a name="message-encoder-factory-and-the-message-encoder"></a><span data-ttu-id="dc873-127">Factory di codificatori di messaggi e codificatori dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="dc873-127">Message Encoder Factory and the Message Encoder</span></span>

<span data-ttu-id="dc873-128">Quando la classe <xref:System.ServiceModel.ServiceHost> o il canale client vengono aperti, il componente della fase di progettazione `CustomTextMessageBindingElement` crea `CustomTextMessageEncoderFactory`.</span><span class="sxs-lookup"><span data-stu-id="dc873-128">When the <xref:System.ServiceModel.ServiceHost> or the client channel is opened, the design time component `CustomTextMessageBindingElement` creates the `CustomTextMessageEncoderFactory`.</span></span> <span data-ttu-id="dc873-129">La factory crea `CustomTextMessageEncoder`.</span><span class="sxs-lookup"><span data-stu-id="dc873-129">The factory creates the `CustomTextMessageEncoder`.</span></span> <span data-ttu-id="dc873-130">Il codificatore di messaggi aziona entrambi in modalità di trasmissione e in modalità di memorizzazione nel buffer.</span><span class="sxs-lookup"><span data-stu-id="dc873-130">The message encoder operates both in the streaming mode and the buffered mode.</span></span> <span data-ttu-id="dc873-131">Utilizza le classi <xref:System.Xml.XmlReader> e <xref:System.Xml.XmlWriter> per leggere e scrivere i messaggi, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="dc873-131">It uses the <xref:System.Xml.XmlReader> and <xref:System.Xml.XmlWriter> to read and write the messages respectively.</span></span> <span data-ttu-id="dc873-132">Rispetto ai Reader e ai writer XML ottimizzati di WCF che supportano solo UTF-8, UTF-16 e Big-Endian Unicode, i lettori e i writer supportano tutta la codifica supportata dalla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="dc873-132">As opposed to the optimized XML readers and writers of WCF that support only UTF-8, UTF-16 and big-endian Unicode, these readers and writers support all platform-supported encoding.</span></span>

<span data-ttu-id="dc873-133">Nel codice seguente viene illustrato il codificatore di messaggio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc873-133">The following code example shows the CustomTextMessageEncoder.</span></span>

```csharp
public class CustomTextMessageEncoder : MessageEncoder
{
    private CustomTextMessageEncoderFactory factory;
    private XmlWriterSettings writerSettings;
    private string contentType;

    public CustomTextMessageEncoder(CustomTextMessageEncoderFactory factory)
    {
        this.factory = factory;

        this.writerSettings = new XmlWriterSettings();
        this.writerSettings.Encoding = Encoding.GetEncoding(factory.CharSet);
        this.contentType = $"{this.factory.MediaType}; charset={this.writerSettings.Encoding.HeaderName}";
    }

    public override string ContentType
    {
        get
        {
            return this.contentType;
        }
    }

    public override string MediaType
    {
        get
        {
            return factory.MediaType;
        }
    }

    public override MessageVersion MessageVersion
    {
        get
        {
            return this.factory.MessageVersion;
        }
    }

    public override Message ReadMessage(ArraySegment<byte> buffer, BufferManager bufferManager, string contentType)
    {
        byte[] msgContents = new byte[buffer.Count];
        Array.Copy(buffer.Array, buffer.Offset, msgContents, 0, msgContents.Length);
        bufferManager.ReturnBuffer(buffer.Array);

        MemoryStream stream = new MemoryStream(msgContents);
        return ReadMessage(stream, int.MaxValue);
    }

    public override Message ReadMessage(Stream stream, int maxSizeOfHeaders, string contentType)
    {
        XmlReader reader = XmlReader.Create(stream);
        return Message.CreateMessage(reader, maxSizeOfHeaders, this.MessageVersion);
    }

    public override ArraySegment<byte> WriteMessage(Message message, int maxMessageSize, BufferManager bufferManager, int messageOffset)
    {
        MemoryStream stream = new MemoryStream();
        XmlWriter writer = XmlWriter.Create(stream, this.writerSettings);
        message.WriteMessage(writer);
        writer.Close();

        byte[] messageBytes = stream.GetBuffer();
        int messageLength = (int)stream.Position;
        stream.Close();

        int totalLength = messageLength + messageOffset;
        byte[] totalBytes = bufferManager.TakeBuffer(totalLength);
        Array.Copy(messageBytes, 0, totalBytes, messageOffset, messageLength);

        ArraySegment<byte> byteArray = new ArraySegment<byte>(totalBytes, messageOffset, messageLength);
        return byteArray;
    }

    public override void WriteMessage(Message message, Stream stream)
    {
        XmlWriter writer = XmlWriter.Create(stream, this.writerSettings);
        message.WriteMessage(writer);
        writer.Close();
    }
}
```

<span data-ttu-id="dc873-134">Nell'esempio di codice seguente viene illustrato come compilare la factory del codificatore di messaggi.</span><span class="sxs-lookup"><span data-stu-id="dc873-134">The following code example shows how to build the message encoder factory.</span></span>

```csharp
public class CustomTextMessageEncoderFactory : MessageEncoderFactory
{
    private MessageEncoder encoder;
    private MessageVersion version;
    private string mediaType;
    private string charSet;

    internal CustomTextMessageEncoderFactory(string mediaType, string charSet,
        MessageVersion version)
    {
        this.version = version;
        this.mediaType = mediaType;
        this.charSet = charSet;
        this.encoder = new CustomTextMessageEncoder(this);
    }

    public override MessageEncoder Encoder
    {
        get
        {
            return this.encoder;
        }
    }

    public override MessageVersion MessageVersion
    {
        get
        {
            return this.version;
        }
    }

    internal string MediaType
    {
        get
        {
            return this.mediaType;
        }
    }

    internal string CharSet
    {
        get
        {
            return this.charSet;
        }
    }
}
```

## <a name="message-encoding-binding-element"></a><span data-ttu-id="dc873-135">Elemento di associazione di codifica dei messaggi</span><span class="sxs-lookup"><span data-stu-id="dc873-135">Message Encoding Binding Element</span></span>

<span data-ttu-id="dc873-136">Gli elementi di associazione consentono la configurazione dello stack di runtime WCF.</span><span class="sxs-lookup"><span data-stu-id="dc873-136">The binding elements allow the configuration of the WCF run-time stack.</span></span> <span data-ttu-id="dc873-137">Per utilizzare il codificatore di messaggi personalizzato in un'applicazione WCF, è necessario un elemento di associazione che crea la factory del codificatore di messaggi con le impostazioni appropriate al livello appropriato nello stack di Runtime.</span><span class="sxs-lookup"><span data-stu-id="dc873-137">To use the custom message encoder in a WCF application, a binding element is required that creates the message encoder factory with the appropriate settings at the appropriate level in the run-time stack.</span></span>

<span data-ttu-id="dc873-138">La classe `CustomTextMessageBindingElement` deriva dalla classe base <xref:System.ServiceModel.Channels.BindingElement> ed eredita dalla classe <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>.</span><span class="sxs-lookup"><span data-stu-id="dc873-138">The `CustomTextMessageBindingElement` derives from the <xref:System.ServiceModel.Channels.BindingElement> base class and inherits from the <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> class.</span></span> <span data-ttu-id="dc873-139">Ciò consente ad altri componenti WCF di riconoscere questo elemento di associazione come elemento di associazione di codifica dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="dc873-139">This allows other WCF components to recognize this binding element as being a message encoding binding element.</span></span> <span data-ttu-id="dc873-140">L'implementazione del metodo <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A> restituisce un'istanza della factory del codificatore di messaggi corrispondente con le impostazioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="dc873-140">The implementation of <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A> returns an instance of the matching message encoder factory with appropriate settings.</span></span>

<span data-ttu-id="dc873-141">`CustomTextMessageBindingElement` espone impostazioni per `MessageVersion`, `ContentType` e `Encoding` tramite proprietà.</span><span class="sxs-lookup"><span data-stu-id="dc873-141">The `CustomTextMessageBindingElement` exposes settings for `MessageVersion`, `ContentType`, and `Encoding` through properties.</span></span> <span data-ttu-id="dc873-142">Il codificatore supporta le versioni Soap11Addressing e Soap12Addressing1.</span><span class="sxs-lookup"><span data-stu-id="dc873-142">The encoder supports both Soap11Addressing and Soap12Addressing1 versions.</span></span> <span data-ttu-id="dc873-143">L'impostazione predefinita è Soap11Addressing1.</span><span class="sxs-lookup"><span data-stu-id="dc873-143">The default is Soap11Addressing1.</span></span> <span data-ttu-id="dc873-144">Il valore predefinito della proprietà `ContentType` è "text/xml".</span><span class="sxs-lookup"><span data-stu-id="dc873-144">The default value of the `ContentType` is "text/xml".</span></span> <span data-ttu-id="dc873-145">La proprietà `Encoding` consente di impostare il valore della codifica dei caratteri desiderata.</span><span class="sxs-lookup"><span data-stu-id="dc873-145">The `Encoding` property allows you to set the value of the desired character encoding.</span></span> <span data-ttu-id="dc873-146">Il client e il servizio di esempio usano la codifica dei caratteri ISO-8859-1 (Latin1), che non è supportata da <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> WCF.</span><span class="sxs-lookup"><span data-stu-id="dc873-146">The sample client and service uses the ISO-8859-1 (Latin1) character encoding, which is not supported by the <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> of WCF.</span></span>

<span data-ttu-id="dc873-147">Nel codice seguente viene illustrato come creare l'associazione a livello di codice utilizzando il codificatore del messaggio di testo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="dc873-147">The following code shows how to programmatically create the binding using the custom text message encoder.</span></span>

```csharp
ICollection<BindingElement> bindingElements = new List<BindingElement>();
HttpTransportBindingElement httpBindingElement = new HttpTransportBindingElement();
CustomTextMessageBindingElement textBindingElement = new CustomTextMessageBindingElement();
bindingElements.Add(textBindingElement);
bindingElements.Add(httpBindingElement);
CustomBinding binding = new CustomBinding(bindingElements);
```

## <a name="adding-metadata-support-to-the-message-encoding-binding-element"></a><span data-ttu-id="dc873-148">Aggiunta del supporto dei metadati per un elemento di associazione di codifica dei messaggi</span><span class="sxs-lookup"><span data-stu-id="dc873-148">Adding Metadata Support to the Message Encoding Binding Element</span></span>

<span data-ttu-id="dc873-149">Qualsiasi tipo che deriva da <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> deve eseguire l'aggiornamento della versione dell'associazione SOAP nel documento WSDL generato per il servizio.</span><span class="sxs-lookup"><span data-stu-id="dc873-149">Any type that derives from <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> is responsible for updating the version of the SOAP binding in the WSDL document generated for the service.</span></span> <span data-ttu-id="dc873-150">Ciò viene fatto implementando il metodo `ExportEndpoint` sull'interfaccia <xref:System.ServiceModel.Description.IWsdlExportExtension> e modificando quindi il WSDL generato.</span><span class="sxs-lookup"><span data-stu-id="dc873-150">This is done by implementing the `ExportEndpoint` method on the <xref:System.ServiceModel.Description.IWsdlExportExtension> interface and then modifying the generated WSDL.</span></span> <span data-ttu-id="dc873-151">In questo esempio, `CustomTextMessageBindingElement` utilizza la logica di esportazione WSDL di `TextMessageEncodingBindingElement`.</span><span class="sxs-lookup"><span data-stu-id="dc873-151">In this sample, the `CustomTextMessageBindingElement` uses the WSDL export logic from the `TextMessageEncodingBindingElement`.</span></span>

<span data-ttu-id="dc873-152">Per questo esempio, la configurazione del client è manuale.</span><span class="sxs-lookup"><span data-stu-id="dc873-152">For this sample, the client configuration is hand configured.</span></span> <span data-ttu-id="dc873-153">Non è possibile utilizzare Svcutil.exe per generare la configurazione del client perché `CustomTextMessageBindingElement` non esporta un'asserzione di criteri per descrivere il comportamento.</span><span class="sxs-lookup"><span data-stu-id="dc873-153">You cannot use Svcutil.exe to generate the client configuration because the `CustomTextMessageBindingElement` does not export a policy assertion to describe its behavior.</span></span> <span data-ttu-id="dc873-154">Generalmente si deve implementare l'interfaccia <xref:System.ServiceModel.Description.IPolicyExportExtension> su un elemento di associazione personalizzato per esportare un'asserzione di criteri personalizzata che descrive il comportamento o la funzionalità implementata dall'elemento di associazione.</span><span class="sxs-lookup"><span data-stu-id="dc873-154">You should generally implement the <xref:System.ServiceModel.Description.IPolicyExportExtension> interface on a custom binding element to export a custom policy assertion that describes the behavior or capability implemented by the binding element.</span></span> <span data-ttu-id="dc873-155">Per un esempio di come esportare un'asserzione di criteri per un elemento di associazione personalizzato, vedere l'esempio [Transport: UDP](transport-udp.md) .</span><span class="sxs-lookup"><span data-stu-id="dc873-155">For an example of how to export a policy assertion for a custom binding element, see the [Transport: UDP](transport-udp.md) sample.</span></span>

## <a name="message-encoding-binding-configuration-handler"></a><span data-ttu-id="dc873-156">Gestore di configurazione dell'associazione di codifica dei messaggi</span><span class="sxs-lookup"><span data-stu-id="dc873-156">Message Encoding Binding Configuration Handler</span></span>
<span data-ttu-id="dc873-157">La sezione precedente mostra come utilizzare il codificatore dei messaggi di testo personalizzato a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="dc873-157">The previous section shows how to use the custom text message encoder programmatically.</span></span> <span data-ttu-id="dc873-158">`CustomTextMessageEncodingBindingSection` implementa un gestore di configurazione che consente di specificare l'utilizzo di un codificatore dei messaggi di testo personalizzato all'interno di un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="dc873-158">The `CustomTextMessageEncodingBindingSection` implements a configuration handler that allows you to specify the use of a custom text message encoder within a configuration file.</span></span> <span data-ttu-id="dc873-159">La classe `CustomTextMessageEncodingBindingSection` deriva dalla classe <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> .</span><span class="sxs-lookup"><span data-stu-id="dc873-159">The `CustomTextMessageEncodingBindingSection` class derives from the <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> class.</span></span> <span data-ttu-id="dc873-160">La proprietà `BindingElementType` informa il sistema di configurazione del tipo di elemento di associazione da creare per questa sezione.</span><span class="sxs-lookup"><span data-stu-id="dc873-160">The `BindingElementType` property informs the configuration system of the type of binding element to create for this section.</span></span>

<span data-ttu-id="dc873-161">Tutte le impostazioni definite da `CustomTextMessageBindingElement` sono esposte come proprietà in `CustomTextMessageEncodingBindingSection`.</span><span class="sxs-lookup"><span data-stu-id="dc873-161">All of the settings defined by `CustomTextMessageBindingElement` are exposed as the properties in the `CustomTextMessageEncodingBindingSection`.</span></span> <span data-ttu-id="dc873-162">La classe <xref:System.Configuration.ConfigurationPropertyAttribute> assiste nell'eseguire il mapping degli attributi dell'elemento di configurazione alle proprietà e nell'impostazione dei valori predefiniti se l'attributo non è impostato.</span><span class="sxs-lookup"><span data-stu-id="dc873-162">The <xref:System.Configuration.ConfigurationPropertyAttribute> assists in mapping the configuration element attributes to the properties and setting default values if the attribute is not set.</span></span> <span data-ttu-id="dc873-163">Dopo i valori della configurazione sono caricati e applicati alle proprietà del tipo, e viene chiamato il metodo <xref:System.ServiceModel.Configuration.BindingElementExtensionElement.CreateBindingElement%2A>. Esso converte le proprietà in un'istanza concreta di un elemento di associazione.</span><span class="sxs-lookup"><span data-stu-id="dc873-163">After the values from configuration are loaded and applied to the properties of the type, the <xref:System.ServiceModel.Configuration.BindingElementExtensionElement.CreateBindingElement%2A> method is called, which converts the properties into a concrete instance of a binding element.</span></span>

<span data-ttu-id="dc873-164">Questo gestore di configurazione esegue il mapping alla rappresentazione seguente in App.config o Web.config per il servizio o il client.</span><span class="sxs-lookup"><span data-stu-id="dc873-164">This configuration handler maps to the following representation in the App.config or Web.config for the service or client.</span></span>

```xml
<customTextMessageEncoding encoding="utf-8" contentType="text/xml" messageVersion="Soap11Addressing1" />
```

<span data-ttu-id="dc873-165">Nell'esempio viene utilizzata la codifica ISO-8859-1.</span><span class="sxs-lookup"><span data-stu-id="dc873-165">The sample uses the ISO-8859-1 encoding.</span></span>

<span data-ttu-id="dc873-166">Per utilizzare questo gestore di configurazione deve essere registrato utilizzando l'elemento di configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="dc873-166">To use this configuration handler it must be registered using the following configuration element.</span></span>

```xml
<extensions>
    <bindingElementExtensions>
        <add name="customTextMessageEncoding" type="
Microsoft.ServiceModel.Samples.CustomTextMessageEncodingBindingSection,
                  CustomTextMessageEncoder" />
    </bindingElementExtensions>
</extensions>
```

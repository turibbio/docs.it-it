---
title: Pubblicazione WSDL personalizzata
ms.date: 03/30/2017
ms.assetid: 3b3e8103-2c95-4db3-a05b-46aa8e9d4d29
ms.openlocfilehash: b18ac2f72d58c768b3784e1c414a71cdaec50c01
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596695"
---
# <a name="custom-wsdl-publication"></a><span data-ttu-id="1d4d8-102">Pubblicazione WSDL personalizzata</span><span class="sxs-lookup"><span data-stu-id="1d4d8-102">Custom WSDL Publication</span></span>
<span data-ttu-id="1d4d8-103">Questo esempio dimostra come:</span><span class="sxs-lookup"><span data-stu-id="1d4d8-103">This sample demonstrates how to:</span></span>  
  
- <span data-ttu-id="1d4d8-104">Implementare un'interfaccia <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=nameWithType> su un attributo <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType> personalizzato per esportare le proprietà dell'attributo come annotazioni WSDL.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-104">Implement a <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=nameWithType> on a custom <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType> attribute to export attribute properties as WSDL annotations.</span></span>  
  
- <span data-ttu-id="1d4d8-105">Implementare <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=nameWithType> per importare le annotazioni WSDL personalizzate.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-105">Implement <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=nameWithType> to import the custom WSDL annotations.</span></span>  
  
- <span data-ttu-id="1d4d8-106">Implementare <xref:System.ServiceModel.Description.IServiceContractGenerationExtension?displayProperty=nameWithType> e <xref:System.ServiceModel.Description.IOperationContractGenerationExtension?displayProperty=nameWithType> rispettivamente su un comportamento del contratto personalizzato e un comportamento dell'operazione personalizzato per scrivere le annotazioni importate come commenti in CodeDOM per il contratto e l'operazione importati.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-106">Implement <xref:System.ServiceModel.Description.IServiceContractGenerationExtension?displayProperty=nameWithType> and <xref:System.ServiceModel.Description.IOperationContractGenerationExtension?displayProperty=nameWithType> on a custom contract behavior and a custom operation behavior, respectively, to write imported annotations as comments in the CodeDom for the imported contract and operation.</span></span>  
  
- <span data-ttu-id="1d4d8-107">Usare <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> per scaricare il file WSDL, un oggetto <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> per importare il file WSDL usando l'utilità di importazione WSDL personalizzata e <xref:System.ServiceModel.Description.ServiceContractGenerator?displayProperty=nameWithType> per generare il codice client di Windows Communication Foundation (WCF) con le annotazioni WSDL come///e i commenti ''' in C# e Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-107">Use the <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> to download the WSDL, a <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> to import the WSDL using the custom WSDL importer, and the <xref:System.ServiceModel.Description.ServiceContractGenerator?displayProperty=nameWithType> to generate Windows Communication Foundation (WCF) client code with the WSDL annotations as /// and ''' comments in C# and Visual Basic.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="1d4d8-108">La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-108">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
## <a name="service"></a><span data-ttu-id="1d4d8-109">Service</span><span class="sxs-lookup"><span data-stu-id="1d4d8-109">Service</span></span>  
 <span data-ttu-id="1d4d8-110">Il servizio in questo esempio è contrassegnato con due attributi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-110">The service in this sample is marked with two custom attributes.</span></span> <span data-ttu-id="1d4d8-111">Il primo, `WsdlDocumentationAttribute`, accetta una stringa nel costruttore e può essere applicato per fornire un'interfaccia o un'operazione del contratto con una stringa che ne descrive l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-111">The first, the `WsdlDocumentationAttribute`, accepts a string in the constructor and can be applied to provide a contract interface or operation with a string that describes its usage.</span></span> <span data-ttu-id="1d4d8-112">Il secondo, `WsdlParamOrReturnDocumentationAttribute`, può essere applicato ai valori o parametri restituiti per descrivere tali valori nell'operazione.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-112">The second, `WsdlParamOrReturnDocumentationAttribute`, can be applied to return values or parameters to describe those values in the operation.</span></span> <span data-ttu-id="1d4d8-113">Nell'esempio seguente viene illustrato un contratto di servizio, `ICalculator`, descritto mediante tali attributi.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-113">The following example shows a service contract, `ICalculator`, described using these attributes.</span></span>  
  
```csharp  
// Define a service contract.
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
// Document it.  
[WsdlDocumentation("The ICalculator contract performs basic calculation services.")]  
public interface ICalculator  
{  
    [OperationContract]  
    [WsdlDocumentation("The Add operation adds two numbers and returns the result.")]  
    [return:WsdlParamOrReturnDocumentation("The result of adding the two arguments together.")]  
    double Add(  
      [WsdlParamOrReturnDocumentation("The first value to add.")]double n1,
      [WsdlParamOrReturnDocumentation("The second value to add.")]double n2  
    );  
  
    [OperationContract]  
    [WsdlDocumentation("The Subtract operation subtracts the second argument from the first.")]  
    [return:WsdlParamOrReturnDocumentation("The result of the second argument subtracted from the first.")]  
    double Subtract(  
      [WsdlParamOrReturnDocumentation("The value from which the second is subtracted.")]double n1,
      [WsdlParamOrReturnDocumentation("The value that is subtracted from the first.")]double n2  
    );  
  
    [OperationContract]  
    [WsdlDocumentation("The Multiply operation multiplies two values.")]  
    [return:WsdlParamOrReturnDocumentation("The result of multiplying the first and second arguments.")]  
    double Multiply(  
      [WsdlParamOrReturnDocumentation("The first value to multiply.")]double n1,
      [WsdlParamOrReturnDocumentation("The second value to multiply.")]double n2  
    );  
  
    [OperationContract]  
    [WsdlDocumentation("The Divide operation returns the value of the first argument divided by the second argument.")]  
    [return:WsdlParamOrReturnDocumentation("The result of dividing the first argument by the second.")]  
    double Divide(  
      [WsdlParamOrReturnDocumentation("The numerator.")]double n1,
      [WsdlParamOrReturnDocumentation("The denominator.")]double n2  
    );  
}  
```  
  
 <span data-ttu-id="1d4d8-114">`WsdlDocumentationAttribute` implementa <xref:System.ServiceModel.Description.IContractBehavior> e <xref:System.ServiceModel.Description.IOperationBehavior>, pertanto le istanze dell'attributo vengono aggiunte all'elemento <xref:System.ServiceModel.Description.ContractDescription> o <xref:System.ServiceModel.Description.OperationDescription> corrispondente quando il servizio è aperto.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-114">The `WsdlDocumentationAttribute` implements <xref:System.ServiceModel.Description.IContractBehavior> and <xref:System.ServiceModel.Description.IOperationBehavior>, so the attribute instances are added to the corresponding <xref:System.ServiceModel.Description.ContractDescription> or <xref:System.ServiceModel.Description.OperationDescription> when the service is opened.</span></span> <span data-ttu-id="1d4d8-115">L'attributo implementa anche <xref:System.ServiceModel.Description.IWsdlExportExtension>.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-115">The attribute also implements <xref:System.ServiceModel.Description.IWsdlExportExtension>.</span></span> <span data-ttu-id="1d4d8-116">Quando il metodo <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%28System.ServiceModel.Description.WsdlExporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> viene chiamato, l'elemento <xref:System.ServiceModel.Description.WsdlExporter> utilizzato per esportare i metadati e l'elemento <xref:System.ServiceModel.Description.WsdlContractConversionContext> contenente gli oggetti descrizione del servizio vengono passati come parametri che abilitano la modifica dei metadati esportati.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-116">When <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportContract%28System.ServiceModel.Description.WsdlExporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> is called, the <xref:System.ServiceModel.Description.WsdlExporter> that is used to export the metadata and the <xref:System.ServiceModel.Description.WsdlContractConversionContext> that contains the service description objects are passed in as parameters enabling the modification of the exported metadata.</span></span>  
  
 <span data-ttu-id="1d4d8-117">In questo esempio, a seconda che l'oggetto contesto di esportazione disponga di un elemento <xref:System.ServiceModel.Description.ContractDescription> o un elemento <xref:System.ServiceModel.Description.OperationDescription>, viene estratto un commento dall'attributo utilizzando la proprietà Text e viene aggiunto all'elemento annotazione WSDL, come illustrato nel codice seguente.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-117">In this sample, depending upon whether the export context object has a <xref:System.ServiceModel.Description.ContractDescription> or an <xref:System.ServiceModel.Description.OperationDescription>, a comment is extracted from the attribute using the text property and is added to the WSDL annotation element as shown in the following code.</span></span>  
  
```csharp
public void ExportContract(WsdlExporter exporter, WsdlContractConversionContext context)
{
    if (contractDescription != null)
    {
        // Inside this block it is the contract-level comment attribute.
        // This.Text returns the string for the contract attribute.
        // Set the doc element; if this isn't done first, there is no XmlElement in the
        // DocumentElement property.
        context.WsdlPortType.Documentation = string.Empty;
        // Contract comments.
        XmlDocument owner = context.WsdlPortType.DocumentationElement.OwnerDocument;
        XmlElement summaryElement = owner.CreateElement("summary");
        summaryElement.InnerText = this.Text;
        context.WsdlPortType.DocumentationElement.AppendChild(summaryElement);
    }
    else
    {
        Operation operation = context.GetOperation(operationDescription);
        if (operation != null)
        {
            // We are dealing strictly with the operation here.
            // This.Text returns the string for the operation-level attributes.
            // Set the doc element; if this isn't done first, there is no XmlElement in the
            // DocumentElement property.
            operation.Documentation = String.Empty;

            // Operation C# triple comments.
            XmlDocument owner = operation.DocumentationElement.OwnerDocument;
            XmlElement newSummaryElement = owner.CreateElement("summary");
            newSummaryElement.InnerText = this.Text;
            operation.DocumentationElement.AppendChild(newSummaryElement);
        }
    }
}
```  
  
 <span data-ttu-id="1d4d8-118">Se un'operazione viene esportata, l'esempio utilizza la reflection per ottenere qualsiasi valore `WsdlParamOrReturnDocumentationAttribute` per i parametri e i valori restituiti e li aggiunge agli elementi annotazione WSDL per tale operazione, come segue.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-118">If an operation is being exported, the sample uses reflection to obtain any `WsdlParamOrReturnDocumentationAttribute` values for parameters and return values and adds them to the WSDL annotation elements for that operation as follows.</span></span>  
  
```csharp
// Get returns information  
ParameterInfo returnValue = operationDescription.SyncMethod.ReturnParameter;  
object[] returnAttrs = returnValue.GetCustomAttributes(typeof(WsdlParamOrReturnDocumentationAttribute), false);  
if (returnAttrs.Length != 0)  
{  
    // <returns>text.</returns>  
    XmlElement returnsElement = owner.CreateElement("returns");  
    returnsElement.InnerText = ((WsdlParamOrReturnDocumentationAttribute)returnAttrs[0]).ParamComment;  
    operation.DocumentationElement.AppendChild(returnsElement);  
}  
  
// Get parameter information.  
ParameterInfo[] args = operationDescription.SyncMethod.GetParameters();  
for (int i = 0; i < args.Length; i++)  
{  
    object[] docAttrs = args[i].GetCustomAttributes(typeof(WsdlParamOrReturnDocumentationAttribute), false);  
    if (docAttrs.Length == 1)  
    {  
        // <param name="Int1">Text.</param>  
        XmlElement newParamElement = owner.CreateElement("param");  
        XmlAttribute paramName = owner.CreateAttribute("name");  
        paramName.Value = args[i].Name;  
        newParamElement.InnerText = ((WsdlParamOrReturnDocumentationAttribute)docAttrs[0]).ParamComment;  
        newParamElement.Attributes.Append(paramName);  
        operation.DocumentationElement.AppendChild(newParamElement);  
    }  
}  
```  
  
 <span data-ttu-id="1d4d8-119">Nell'esempio i metadati vengono quindi pubblicati nella modalità standard, utilizzando il file di configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-119">The sample then publishes metadata in the standard way, using the following configuration file.</span></span>  
  
```xml  
<services>  
  <service
      name="Microsoft.ServiceModel.Samples.CalculatorService"  
      behaviorConfiguration="CalculatorServiceBehavior">  
    <!-- ICalculator is exposed at the base address provided by host: http://localhost/servicemodelsamples/service.svc  -->  
    <endpoint address=""  
              binding="wsHttpBinding"  
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    <!-- the mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex -->  
    <endpoint address="mex"  
              binding="mexHttpBinding"  
              contract="IMetadataExchange" />  
  </service>  
</services>  
  
<!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
## <a name="svcutil-client"></a><span data-ttu-id="1d4d8-120">Client Svcutil</span><span class="sxs-lookup"><span data-stu-id="1d4d8-120">Svcutil client</span></span>  
 <span data-ttu-id="1d4d8-121">In questo esempio non viene utilizzato Svcutil.exe.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-121">This sample does not use Svcutil.exe.</span></span> <span data-ttu-id="1d4d8-122">Il contratto viene fornito nel file generatedClient.cs in modo che dopo che la dimostrazione dell'importazione WSDL personalizzata e della generazione di codice nell'esempio, il servizio può essere richiamato.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-122">The contract is provided in the generatedClient.cs file so that after the sample demonstrates custom WSDL import and code generation, the service can be invoked.</span></span> <span data-ttu-id="1d4d8-123">Per usare l'utilità di importazione WSDL personalizzata seguente per questo esempio, è possibile eseguire Svcutil.exe e specificare l'opzione `/svcutilConfig`, fornendo il percorso al file di configurazione client usato in questo esempio, che fa riferimento alla libreria `WsdlDocumentation.dll`.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-123">To use the following custom WSDL importer for this example, you can run Svcutil.exe and specify the `/svcutilConfig` option, giving the path to the client configuration file used in this sample, which references the `WsdlDocumentation.dll` library.</span></span> <span data-ttu-id="1d4d8-124">Per caricare `WsdlDocumentationImporter`, tuttavia, Svuctil.exe deve essere in grado di trovare e caricare la libreria `WsdlDocumentation.dll`, la quale deve pertanto essere registrata nella Global Assembly Cache nel percorso o essere inclusa nella stessa directory di Svcutil.exe.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-124">To load the `WsdlDocumentationImporter`, however, Svuctil.exe must be able to locate and load the `WsdlDocumentation.dll` library, which means either that it is registered in the global assembly cache, in the path, or is in the same directory as Svcutil.exe.</span></span> <span data-ttu-id="1d4d8-125">Per un esempio di base attinente, la procedura più facile consiste nel copiare Svcutil.exe e il file di configurazione client nella stessa directory di `WsdlDocumentation.dll` ed eseguirlo da quella posizione.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-125">For a basic sample such as this, the easiest thing to do is to copy Svcutil.exe and the client configuration file into the same directory as `WsdlDocumentation.dll` and run it from there.</span></span>  
  
## <a name="the-custom-wsdl-importer"></a><span data-ttu-id="1d4d8-126">Unità di importazione WSDL personalizzata</span><span class="sxs-lookup"><span data-stu-id="1d4d8-126">The Custom WSDL Importer</span></span>  
 <span data-ttu-id="1d4d8-127">L'oggetto <xref:System.ServiceModel.Description.IWsdlImportExtension> personalizzato, `WsdlDocumentationImporter`, implementa anche <xref:System.ServiceModel.Description.IContractBehavior> e <xref:System.ServiceModel.Description.IOperationBehavior> per essere aggiunto ai ServiceEndpoints importati e <xref:System.ServiceModel.Description.IServiceContractGenerationExtension> e <xref:System.ServiceModel.Description.IOperationContractGenerationExtension> per essere richiamato per modificare la generazione del codice quando viene creato il contratto o il codice dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-127">The custom <xref:System.ServiceModel.Description.IWsdlImportExtension> object `WsdlDocumentationImporter` also implements <xref:System.ServiceModel.Description.IContractBehavior> and <xref:System.ServiceModel.Description.IOperationBehavior> to be added to the imported ServiceEndpoints and <xref:System.ServiceModel.Description.IServiceContractGenerationExtension> and <xref:System.ServiceModel.Description.IOperationContractGenerationExtension> to be invoked to modify the code generation when the contract or operation code is being created.</span></span>  
  
 <span data-ttu-id="1d4d8-128">Innanzitutto, con il metodo <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> viene determinato se l'annotazione WSDL è a livello del contratto o dell'operazione, e viene aggiunta come un comportamento all'ambito appropriato, passando il testo dell'annotazione importato al costruttore.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-128">First, in the <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> method, the sample determines whether the WSDL annotation is at the contract or operation level, and adds itself as a behavior at the appropriate scope, passing the imported annotation text to its constructor.</span></span>  
  
```csharp
public void ImportContract(WsdlImporter importer, WsdlContractConversionContext context)  
{  
    // Contract Documentation  
    if (context.WsdlPortType.Documentation != null)  
    {  
        // System examines the contract behaviors to see whether any implement IWsdlImportExtension.  
        context.Contract.Behaviors.Add(new WsdlDocumentationImporter(context.WsdlPortType.Documentation));  
    }  
    // Operation Documentation  
    foreach (Operation operation in context.WsdlPortType.Operations)  
    {  
        if (operation.Documentation != null)  
        {  
            OperationDescription operationDescription = context.Contract.Operations.Find(operation.Name);  
            if (operationDescription != null)  
            {  
                // System examines the operation behaviors to see whether any implement IWsdlImportExtension.  
                operationDescription.Behaviors.Add(new WsdlDocumentationImporter(operation.Documentation));  
            }  
        }  
    }  
}  
```  
  
 <span data-ttu-id="1d4d8-129">Quindi, quando il codice viene generato, il sistema richiama i metodi <xref:System.ServiceModel.Description.IServiceContractGenerationExtension.GenerateContract%28System.ServiceModel.Description.ServiceContractGenerationContext%29> e <xref:System.ServiceModel.Description.IOperationContractGenerationExtension.GenerateOperation%28System.ServiceModel.Description.OperationContractGenerationContext%29>, passando le informazioni di contesto appropriate.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-129">Then, when the code is generated, the system invokes the <xref:System.ServiceModel.Description.IServiceContractGenerationExtension.GenerateContract%28System.ServiceModel.Description.ServiceContractGenerationContext%29> and <xref:System.ServiceModel.Description.IOperationContractGenerationExtension.GenerateOperation%28System.ServiceModel.Description.OperationContractGenerationContext%29> methods, passing the appropriate context information.</span></span> <span data-ttu-id="1d4d8-130">Le annotazioni WSDL personalizzate vengono formattate e inseriste come commenti in CodeDOM.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-130">The sample formats the custom WSDL annotations and inserts them as comments into the CodeDom.</span></span>  
  
```csharp
public void GenerateContract(ServiceContractGenerationContext context)  
{  
    Debug.WriteLine("In generate contract.");  
    context.ContractType.Comments.AddRange(FormatComments(text));  
}  
  
public void GenerateOperation(OperationContractGenerationContext context)  
{  
    context.SyncMethod.Comments.AddRange(FormatComments(text));  
    Debug.WriteLine("In generate operation.");  
}  
```  
  
## <a name="the-client-application"></a><span data-ttu-id="1d4d8-131">Applicazione client</span><span class="sxs-lookup"><span data-stu-id="1d4d8-131">The Client Application</span></span>  
 <span data-ttu-id="1d4d8-132">L'applicazione client carica l'unità di importazione WSDL personalizzata specificandola nel file di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-132">The client application loads the custom WSDL importer by specifying it in the application configuration file.</span></span>  
  
```xml  
<client>  
  <endpoint address="http://localhost/servicemodelsamples/service.svc"
  binding="wsHttpBinding"
  contract="ICalculator" />  
  <metadata>  
    <wsdlImporters>  
      <extension type="Microsoft.ServiceModel.Samples.WsdlDocumentationImporter, WsdlDocumentation"/>  
    </wsdlImporters>  
  </metadata>  
</client>  
```  
  
 <span data-ttu-id="1d4d8-133">Una volta specificata l'utilità di importazione personalizzata, il sistema di metadati WCF carica l'utilità di importazione personalizzata in qualsiasi <xref:System.ServiceModel.Description.WsdlImporter> oggetto creato a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-133">Once the custom importer has been specified, the WCF metadata system loads the custom importer into any <xref:System.ServiceModel.Description.WsdlImporter> created for that purpose.</span></span> <span data-ttu-id="1d4d8-134">In questo esempio viene utilizzato <xref:System.ServiceModel.Description.MetadataExchangeClient> per scaricare i metadati, l'elemento <xref:System.ServiceModel.Description.WsdlImporter> configurato correttamente per importare i metadati utilizzando l'unità di importazione personalizzata creata dall'esempio e <xref:System.ServiceModel.Description.ServiceContractGenerator> per compilare le informazioni del contratto modificate nel codice client Visual Basic e C# che possono essere utilizzate in Visual Studio per supportare Intellisense o possono essere compilate nella documentazione XML.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-134">This sample uses the <xref:System.ServiceModel.Description.MetadataExchangeClient> to download the metadata, the <xref:System.ServiceModel.Description.WsdlImporter> properly configured to import the metadata using the custom importer the sample creates, and the <xref:System.ServiceModel.Description.ServiceContractGenerator> to compile the modified contract information into both Visual Basic and C# client code that can be used in Visual Studio to support Intellisense or compiled into XML documentation.</span></span>  
  
```csharp
/// From WSDL Documentation:  
///
/// <summary>The ICalculator contract performs basic calculation
/// services.</summary>
///
[System.CodeDom.Compiler.GeneratedCodeAttribute("System.ServiceModel", "3.0.0.0")]  
[System.ServiceModel.ServiceContractAttribute(Namespace="http://Microsoft.ServiceModel.Samples", ConfigurationName="ICalculator")]  
public interface ICalculator  
{  
  
    /// From WSDL Documentation:  
    ///
    /// <summary>The Add operation adds two numbers and returns the
    /// result.</summary><returns>The result of adding the two arguments
    /// together.</returns><param name="n1">The first value to add.</param><param
    /// name="n2">The second value to add.</param>
    ///
    [System.ServiceModel.OperationContractAttribute(Action="http://Microsoft.ServiceModel.Samples/ICalculator/Add", ReplyAction="http://Microsoft.ServiceModel.Samples/ICalculator/AddResponse")]  
    double Add(double n1, double n2);  
  
    /// From WSDL Documentation:  
    ///
    /// <summary>The Subtract operation subtracts the second argument from the
    /// first.</summary><returns>The result of the second argument subtracted from the
    /// first.</returns><param name="n1">The value from which the second is
    /// subtracted.</param><param name="n2">The value that is subtracted from the
    /// first.</param>
    ///
    [System.ServiceModel.OperationContractAttribute(Action="http://Microsoft.ServiceModel.Samples/ICalculator/Subtract", ReplyAction="http://Microsoft.ServiceModel.Samples/ICalculator/SubtractResponse")]  
    double Subtract(double n1, double n2);  
  
    /// From WSDL Documentation:  
    ///
    /// <summary>The Multiply operation multiplies two values.</summary><returns>The
    /// result of multiplying the first and second arguments.</returns><param
    /// name="n1">The first value to multiply.</param><param name="n2">The second value
    /// to multiply.</param>
    ///
    [System.ServiceModel.OperationContractAttribute(Action="http://Microsoft.ServiceModel.Samples/ICalculator/Multiply", ReplyAction="http://Microsoft.ServiceModel.Samples/ICalculator/MultiplyResponse")]  
    double Multiply(double n1, double n2);  
  
    /// From WSDL Documentation:  
    ///
    /// <summary>The Divide operation returns the value of the first argument divided
    /// by the second argument.</summary><returns>The result of dividing the first
    /// argument by the second.</returns><param name="n1">The numerator.</param><param
    /// name="n2">The denominator.</param>
    ///
    [System.ServiceModel.OperationContractAttribute(Action="http://Microsoft.ServiceModel.Samples/ICalculator/Divide", ReplyAction="http://Microsoft.ServiceModel.Samples/ICalculator/DivideResponse")]  
    double Divide(double n1, double n2);  
}  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="1d4d8-135">Per impostare, compilare ed eseguire l'esempio</span><span class="sxs-lookup"><span data-stu-id="1d4d8-135">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="1d4d8-136">Assicurarsi di avere eseguito la [procedura di installazione singola per gli esempi di Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1d4d8-136">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="1d4d8-137">Per compilare l'edizione in C# o Visual Basic .NET della soluzione, seguire le istruzioni in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1d4d8-137">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
3. <span data-ttu-id="1d4d8-138">Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [esecuzione degli esempi di Windows Communication Foundation](running-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1d4d8-138">To run the sample in a single- or cross-machine configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="1d4d8-139">È possibile che gli esempi siano già installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-139">The samples may already be installed on your machine.</span></span> <span data-ttu-id="1d4d8-140">Verificare la directory seguente (impostazione predefinita) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-140">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="1d4d8-141">Se questa directory non esiste, passare a [Windows Communication Foundation (WCF) ed esempi di Windows Workflow Foundation (WF) per .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) per scaricare tutti i Windows Communication Foundation (WCF) ed [!INCLUDE[wf1](../../../../includes/wf1-md.md)] esempi.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-141">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="1d4d8-142">Questo esempio si trova nella directory seguente.</span><span class="sxs-lookup"><span data-stu-id="1d4d8-142">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Metadata\WsdlDocumentation`  

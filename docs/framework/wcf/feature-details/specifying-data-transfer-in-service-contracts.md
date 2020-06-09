---
title: Specifica del trasferimento di dati nei contratti di servizio
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service contracts [WCF], data transfer
ms.assetid: 7c5a26c8-89c9-4bcb-a4bc-7131e6d01f0c
ms.openlocfilehash: ae05fb5ea0ee4962d9889e2a29399a3913a0d9d5
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600296"
---
# <a name="specifying-data-transfer-in-service-contracts"></a>Specifica del trasferimento di dati nei contratti di servizio
Il Windows Communication Foundation (WCF) può essere considerato come un'infrastruttura di messaggistica. Le operazioni di servizio possono ricevere, elaborare e inviare messaggi. I messaggi vengono descritti tramite contratti di operazione. Si consideri ad esempio il contratto seguente:  
  
```csharp  
[ServiceContract]  
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    float GetAirfare(string fromCity, string toCity);  
}  
```  
  
```vb  
<ServiceContract()>  
Public Interface IAirfareQuoteService  
  
    <OperationContract()>  
    Function GetAirfare(fromCity As String, toCity As String) As Double  
End Interface  
```  
  
 In questo contratto, l'operazione `GetAirfare` accetta un messaggio contenente le informazioni `fromCity` e `toCity` e quindi restituisce un messaggio che contiene un numero.  
  
 In questo argomento vengono mostrati i vari modi in cui un contratto di operazione può descrivere i messaggi.  
  
## <a name="describing-messages-by-using-parameters"></a>Descrizione dei messaggi tramite parametri  
 Il modo più semplice per descrivere un messaggio è utilizzare un elenco di parametri e il valore restituito. Nell'esempio precedente, i parametri stringa `fromCity` e `toCity` vengono utilizzati per descrivere il messaggio di richiesta, mentre il valore restituito float viene utilizzato per descrivere il messaggio di risposta. Se il valore restituito non è sufficiente a descrivere un messaggio di risposta, è possibile utilizzare i parametri out. Ad esempio, l'operazione seguente contiene i parametri `fromCity` e `toCity` nel messaggio di richiesta e una coppia numero/valuta nel messaggio di risposta:  
  
```csharp  
[OperationContract]  
float GetAirfare(string fromCity, string toCity, out string currency);  
```  
  
```vb  
<OperationContract()>  
    Function GetAirfare(fromCity As String, toCity As String) As Double  
```  
  
 È inoltre possibile usare i parametri per riferimento di modo che un parametro appartenga sia al messaggio di richiesta sia al messaggio di risposta. Il tipo dei parametri deve essere serializzabile, ovvero convertibile in XML. Per impostazione predefinita, WCF utilizza un componente denominato <xref:System.Runtime.Serialization.DataContractSerializer> classe per eseguire la conversione. Il sistema supporta la maggior parte dei tipi primitivi, ad esempio `int`, `string`, `float` e `DateTime`. I tipi definiti dall'utente in genere devono presentare un contratto di dati. Per ulteriori informazioni, vedere [utilizzo di contratti dati](using-data-contracts.md).  
  
```csharp
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    float GetAirfare(Itinerary itinerary, DateTime date);  
  
    [DataContract]  
    public class Itinerary  
    {  
        [DataMember]  
        public string fromCity;  
        [DataMember]  
        public string toCity;  
   }  
}  
```  
  
```vb  
Public Interface IAirfareQuoteService  
    <OperationContract()>  
    GetAirfare(itinerary as Itinerary, date as DateTime) as Double  
  
    <DataContract()>  
    Class Itinerary  
  
        <DataMember()>  
        Public fromCity As String  
        <DataMember()>  
        Public toCity As String  
    End Class  
End Interface  
```  
  
 Talvolta il componente `DataContractSerializer` non è adatto per serializzare i tipi definiti dall'utente. WCF supporta un motore di serializzazione alternativo,, <xref:System.Xml.Serialization.XmlSerializer> che è possibile utilizzare anche per serializzare i parametri. Gli attributi del motore <xref:System.Xml.Serialization.XmlSerializer>, ad esempio `XmlAttributeAttribute`, consentono di migliorare il controllo sul codice XML risultante. Se si desidera attivare il motore <xref:System.Xml.Serialization.XmlSerializer> per una determinata operazione o per l'intero servizio, applicare l'attributo <xref:System.ServiceModel.XmlSerializerFormatAttribute> a un'operazione o al servizio. Ad esempio:  
  
```csharp  
[ServiceContract]  
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    [XmlSerializerFormat]  
    float GetAirfare(Itinerary itinerary, DateTime date);  
}  
public class Itinerary  
{  
    public string fromCity;  
    public string toCity;  
    [XmlAttribute]  
    public bool isFirstClass;  
}  
```  
  
```vb  
<ServiceContract()>  
Public Interface IAirfareQuoteService  
    <OperationContract()>  
    <XmlSerializerFormat>  
    GetAirfare(itinerary as Itinerary, date as DateTime) as Double  
  
End Interface  
  
Class Itinerary  
  
    Public fromCity As String  
    Public toCity As String  
    <XmlSerializerFormat()>  
    Public isFirstClass As Boolean  
End Class  
```  
  
 Per ulteriori informazioni, vedere [utilizzo della classe XmlSerializer](using-the-xmlserializer-class.md). Si tenga presente che è consigliabile evitare l'attivazione manuale del motore <xref:System.Xml.Serialization.XmlSerializer> appena illustrata, salvo nei casi specifici in cui questa attivazione sia effettivamente necessaria, come descritto in questo argomento.  
  
 Per isolare i nomi di parametro .NET dai nomi di contratto è possibile utilizzare l'attributo <xref:System.ServiceModel.MessageParameterAttribute>. Per impostare i nomi di contratto è possibile utilizzare la proprietà `Name`. Ad esempio, il contratto dell'operazione seguente è equivalente al primo esempio di questo argomento.  
  
```csharp  
[OperationContract]  
public float GetAirfare(  
    [MessageParameter(Name="fromCity")] string originCity,  
    [MessageParameter(Name="toCity")] string destinationCity);  
```  
  
```vb  
<OperationContract()>  
  Function GetAirfare(<MessageParameter(Name := "fromCity")> fromCity As String, <MessageParameter(Name := "toCity")> toCity As String) As Double  
```  
  
## <a name="describing-empty-messages"></a>Descrizione dei messaggi vuoti  
 Per descrivere un messaggio di richiesta vuoto è possibile non specificare alcun parametro per riferimento o di input. Ad esempio, in C#:  
  
 `[OperationContract]`  
  
 `public int GetCurrentTemperature();`  
  
 Ad esempio, in Visual Basic:  
  
 `<OperationContract()>`  
  
 `Function GetCurrentTemperature() as Integer`  
  
 Per descrivere un messaggio di risposta vuoto è possibile utilizzare un tipo restituito `void` e non specificare alcun parametro referenziato o di output. Ad esempio in:  
  
```csharp  
[OperationContract]  
public void SetTemperature(int temperature);  
```  
  
```vb  
<OperationContract()>  
Sub SetTemperature(temperature As Integer)  
```  
  
 Si noti che questa operazione è diversa da un'operazione unidirezionale:  
  
```csharp  
[OperationContract(IsOneWay=true)]  
public void SetLightbulbStatus(bool isOn);  
```  
  
```vb  
<OperationContract(IsOneWay:=True)>  
Sub SetLightbulbStatus(isOne As Boolean)  
```  
  
 L'operazione `SetTemperatureStatus` restituisce un messaggio vuoto e, se si verifica un problema durante l'elaborazione del messaggio di input, può restituire un errore. L'operazione `SetLightbulbStatus` non restituisce invece alcun valore e non è in grado di segnalare il verificarsi di una condizione di errore.  
  
## <a name="describing-messages-by-using-message-contracts"></a>Descrizione dei messaggi tramite i contratti di messaggio  
 In alcuni casi conviene utilizzare un unico tipo per rappresentare un intero messaggio. Benché a tale scopo sia possibile utilizzare un contratto di dati, è comunque consigliabile utilizzare un contratto di messaggio. Questo approccio consente infatti di evitare livelli di wrapping superflui nel codice XML risultante. Inoltre, i contratti di messaggio consentono di migliorare il controllo sui messaggi risultanti. È ad esempio possibile definire in modo specifico i tipi di informazione contenuti nel corpo e nelle intestazioni del messaggio. Nell'esempio seguente viene illustrato l'utilizzo dei contratti di messaggio.  
  
```csharp  
[ServiceContract]  
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    GetAirfareResponse GetAirfare(GetAirfareRequest request);  
}  
  
[MessageContract]  
public class GetAirfareRequest  
{  
    [MessageHeader] public DateTime date;  
    [MessageBodyMember] public Itinerary itinerary;  
}  
  
[MessageContract]  
public class GetAirfareResponse  
{  
    [MessageBodyMember] public float airfare;  
    [MessageBodyMember] public string currency;  
}  
  
[DataContract]  
public class Itinerary  
{  
    [DataMember] public string fromCity;  
    [DataMember] public string toCity;  
}  
```  
  
```vb  
<ServiceContract()>  
Public Interface IAirfareQuoteService  
    <OperationContract()>  
    Function GetAirfare(request As GetAirfareRequest) As GetAirfareResponse  
End Interface  
  
<MessageContract()>  
Public Class GetAirfareRequest  
    <MessageHeader()>
    Public Property date as DateTime  
    <MessageBodyMember()>  
    Public Property itinerary As Itinerary  
End Class  
  
<MessageContract()>  
Public Class GetAirfareResponse  
    <MessageBodyMember()>  
    Public Property airfare As Double  
    <MessageBodyMember()> Public Property currency As String  
End Class  
  
<DataContract()>  
Public Class Itinerary  
    <DataMember()> Public Property fromCity As String  
    <DataMember()> Public Property toCity As String  
End Class  
```  
  
 Per ulteriori informazioni, vedere [utilizzo dei contratti di messaggio](using-message-contracts.md).  
  
 Nell'esempio precedente la classe <xref:System.Runtime.Serialization.DataContractSerializer> viene utilizzata per impostazione predefinita. Nei contratti di messaggio è inoltre possibile utilizzare la classe <xref:System.Xml.Serialization.XmlSerializer>. A tale scopo, applicare l'attributo <xref:System.ServiceModel.XmlSerializerFormatAttribute> all'operazione oppure al contratto e quindi utilizzare tipi compatibili con la classe <xref:System.Xml.Serialization.XmlSerializer> nei membri delle intestazioni e del corpo del messaggio.  
  
## <a name="describing-messages-by-using-streams"></a>Descrizione dei messaggi tramite flussi  
 Un altro modo per descrivere i messaggi nelle operazioni consiste nell'utilizzare la classe <xref:System.IO.Stream> o una delle relative classi derivate in un contratto di operazione oppure come membro del corpo del contratto di messaggio. In quest'ultimo caso è necessario che questo membro sia l'unico. Per i messaggi in ingresso, il tipo deve essere `Stream`. Non è consentito l'utilizzo di classi derivate.  
  
 Anziché richiamare il serializzatore, WCF recupera i dati da un flusso e li inserisce direttamente in un messaggio in uscita oppure recupera i dati da un messaggio in arrivo e li inserisce direttamente in un flusso. Nell'esempio seguente viene illustrato l'utilizzo dei flussi.  
  
```csharp  
[OperationContract]  
public Stream DownloadFile(string fileName);  
```  
  
```vb  
<OperationContract()>  
Function DownloadFile(fileName As String) As String  
```  
  
 Non è consentito combinare dati `Stream` e dati non di flusso in un unico corpo di messaggio. Per aggiungere altri dati nelle intestazioni di messaggio è necessario utilizzare un contratto di messaggio. Nell'esempio seguente viene mostrato un utilizzo non corretto dei flussi quando si definisce un contratto di operazione.  
  
```csharp  
//Incorrect:  
// [OperationContract]  
// public void UploadFile (string fileName, Stream fileData);  
```  
  
```vb  
'Incorrect:  
    '<OperationContract()>  
    Public Sub UploadFile(fileName As String, fileData As StreamingContext)  
```  
  
 Nell'esempio seguente viene mostrato un utilizzo corretto dei flussi quando si definisce un contratto di operazione.  
  
```csharp  
[OperationContract]  
public void UploadFile (UploadFileMessage message);  
//code omitted  
[MessageContract]  
public class UploadFileMessage  
{  
    [MessageHeader] public string fileName;  
    [MessageBodyMember] public Stream fileData;  
}  
```  
  
```vb  
<OperationContract()>  
Public Sub UploadFile(fileName As String, fileData As StreamingContext)  
'Code Omitted  
<MessageContract()>  
Public Class UploadFileMessage  
   <MessageHeader()>  
    Public Property fileName As String  
    <MessageBodyMember()>  
    Public Property fileData As Stream  
End Class  
```  
  
 Per altre informazioni, vedere [dati di grandi dimensioni e flussi](large-data-and-streaming.md).  
  
## <a name="using-the-message-class"></a>Utilizzo della classe Message  
 Per controllare in modo completo a livello di codice lo scambio dei messaggi è possibile utilizzare direttamente la classe <xref:System.ServiceModel.Channels.Message>, come mostrato nell'esempio di codice seguente.  
  
```csharp  
[OperationContract]  
public void LogMessage(Message m);  
```  
  
```vb  
<OperationContract()>  
Sub LogMessage(m As Message)  
```  
  
 Si tratta di uno scenario avanzato, descritto in dettaglio in [utilizzo della classe Message](using-the-message-class.md).  
  
## <a name="describing-fault-messages"></a>Descrizione dei messaggi di errore  
 Oltre ai messaggi descritti in base al valore restituito e ai parametri per riferimento o di output, qualsiasi operazione non unidirezionale può restituire almeno due messaggi: il messaggio di risposta normale e un messaggio di errore. Si consideri il contratto di operazione seguente.  
  
```csharp  
[OperationContract]  
float GetAirfare(string fromCity, string toCity, DateTime date);  
```  
  
```vb  
<OperationContract()>  
Function GetAirfare(fromCity As String, toCity As String, date as DateTime)  
```  
  
 Questa operazione può restituire un messaggio normale contenente un numero `float` o un messaggio di errore contenente un codice di errore e una descrizione. A tale scopo è possibile generare un'eccezione <xref:System.ServiceModel.FaultException> nell'implementazione del servizio.  
  
 Per specificare eventuali messaggi di errore aggiuntivi è possibile utilizzare l'attributo <xref:System.ServiceModel.FaultContractAttribute>. Gli errori aggiuntivi devono essere serializzabili tramite il componente <xref:System.Runtime.Serialization.DataContractSerializer>, come mostrato nell'esempio di codice seguente.  
  
```csharp  
[OperationContract]  
[FaultContract(typeof(ItineraryNotAvailableFault))]  
float GetAirfare(string fromCity, string toCity, DateTime date);  
  
//code omitted  
  
[DataContract]  
public class ItineraryNotAvailableFault  
{  
    [DataMember]  
    public bool IsAlternativeDateAvailable;  
  
    [DataMember]  
    public DateTime alternativeSuggestedDate;  
}  
```  
  
```vb  
<OperationContract()>  
<FaultContract(GetType(ItineraryNotAvailableFault))>  
Function GetAirfare(fromCity As String, toCity As String, date as DateTime) As Double  
  
'Code Omitted  
<DataContract()>  
Public Class  
  <DataMember()>  
  Public Property IsAlternativeDateAvailable As Boolean  
  <DataMember()>  
  Public Property alternativeSuggestedDate As DateTime  
End Class  
```  
  
 Questi errori aggiuntivi possono essere generati mediante un'eccezione <xref:System.ServiceModel.FaultException%601> del tipo di contratto di dati appropriato. Per ulteriori informazioni, vedere [gestione di eccezioni ed errori](../extending/handling-exceptions-and-faults.md).  
  
 Non è consentito utilizzare la classe <xref:System.Xml.Serialization.XmlSerializer> per descrivere errori. L'attributo <xref:System.ServiceModel.XmlSerializerFormatAttribute> non ha alcun effetto sui messaggi di errore di un contratto.  
  
## <a name="using-derived-types"></a>Utilizzo di tipi derivati  
 In alcuni casi conviene utilizzare un tipo di base in un'operazione o in un contratto di messaggio e quindi utilizzare un tipo derivato per richiamare effettivamente l'operazione. In questi casi è necessario utilizzare l'attributo <xref:System.ServiceModel.ServiceKnownTypeAttribute> oppure un meccanismo alternativo per consentire l'utilizzo di tipi derivati. Si consideri l'operazione seguente.  
  
```csharp  
[OperationContract]  
public bool IsLibraryItemAvailable(LibraryItem item);  
```  
  
```vb
<OperationContract()>  
    Function IsLibraryItemAvailable(item As LibraryItem) As Boolean  
```  
  
 Si supponga che due tipi, `Book` e `Magazine`, derivino dal tipo `LibraryItem`. Per utilizzare questi tipi nell'operazione `IsLibraryItemAvailable` è possibile modificare l'operazione come segue:  
  
 `[OperationContract]`  
  
 `[ServiceKnownType(typeof(Book))]`  
  
 `[ServiceKnownType(typeof(Magazine))]`  
  
 `public bool IsLibraryItemAvailable(LibraryItem item);`  
  
 In alternativa, quando si utilizza il componente <xref:System.Runtime.Serialization.KnownTypeAttribute> predefinito, è possibile utilizzare l'attributo <xref:System.Runtime.Serialization.DataContractSerializer>, come mostrato nell'esempio di codice seguente.  
  
```csharp  
[OperationContract]  
public bool IsLibraryItemAvailable(LibraryItem item);  
  
// code omitted
  
[DataContract]  
[KnownType(typeof(Book))]  
[KnownType(typeof(Magazine))]  
public class LibraryItem  
{  
    //code omitted  
}  
```  
  
```vb  
<OperationContract()>  
Function IsLibraryItemAvailable(item As LibraryItem) As Boolean  
  
'Code Omitted  
<DataContract()>  
<KnownType(GetType(Book))>  
<KnownType(GetType(Magazine))>  
Public Class LibraryItem  
  'Code Omitted  
End Class  
```  
  
 Quando invece si utilizza il motore <xref:System.Xml.Serialization.XmlIncludeAttribute> è possibile utilizzare l'attributo <xref:System.Xml.Serialization.XmlSerializer>.  
  
 L'attributo <xref:System.ServiceModel.ServiceKnownTypeAttribute> può essere applicato a un'operazione specifica o all'intero servizio. Analogamente all'attributo <xref:System.Runtime.Serialization.KnownTypeAttribute>, tale attributo accetta un tipo o il nome del metodo da chiamare per ottenere un elenco di tipi noti. Per ulteriori informazioni, vedere [tipi noti del contratto dati](data-contract-known-types.md).  
  
## <a name="specifying-the-use-and-style"></a>Specifica delle proprietà Use e Style  
 I due stili più comunemente utilizzati per descrivere i servizi tramite Web Services Description Language (WSDL) sono Document e Remote Procedure Call (RPC). Nello stile Document, l'intero corpo del messaggio viene descritto utilizzando un unico schema e WSDL descrive le varie parti del corpo del messaggio facendo riferimento agli elementi di tale schema. Nello stile RPC, invece, WSDL descrive le varie parti del corpo del messaggio facendo riferimento a vari tipi di schema. In alcuni casi occorre selezionare manualmente uno di questi stili. A tale scopo è possibile applicare l'attributo <xref:System.ServiceModel.DataContractFormatAttribute> e impostare la proprietà `Style` (quando si utilizza il componente <xref:System.Runtime.Serialization.DataContractSerializer>) oppure impostare la proprietà `Style` dell'attributo <xref:System.ServiceModel.XmlSerializerFormatAttribute> (quando si utilizza il motore <xref:System.Xml.Serialization.XmlSerializer>).  
  
 Inoltre, l'oggetto <xref:System.Xml.Serialization.XmlSerializer> supporta due formati di XML serializzato: `Literal` e `Encoded`. `Literal` è il formato in genere più accettato ed è l'unico a essere supportato da <xref:System.Runtime.Serialization.DataContractSerializer>. `Encoded` è un formato legacy descritto nella sezione 5 della specifica SOAP ed è consigliabile evitarne l'utilizzo nei servizi più recenti. Per passare alla modalità `Encoded`, impostare la proprietà `Use` dell'attributo <xref:System.ServiceModel.XmlSerializerFormatAttribute> su `Encoded`.  
  
 Nella maggior parte dei casi è consigliabile evitare di modificare le impostazioni predefinite delle proprietà `Style` e `Use`.  
  
## <a name="controlling-the-serialization-process"></a>Controllo del processo di serializzazione  
 Sono disponibili diversi modi per personalizzare il processo di serializzazione dei dati.  
  
### <a name="changing-server-serialization-settings"></a>Modifica delle impostazioni di serializzazione del server  
 Quando si utilizza il componente <xref:System.Runtime.Serialization.DataContractSerializer> predefinito è possibile controllare alcuni aspetti del processo di serializzazione del servizio. A tale scopo è possibile applicare l'attributo <xref:System.ServiceModel.ServiceBehaviorAttribute> al servizio. In particolare, è possibile utilizzare la proprietà `MaxItemsInObjectGraph` per impostare la quota che limita il numero massimo di oggetti deserializzati dal componente <xref:System.Runtime.Serialization.DataContractSerializer>. È possibile utilizzare la proprietà `IgnoreExtensionDataObject` per disattivare la funzionalità di controllo delle versioni delle sequenze di andata e ritorno. Per altre informazioni sulle quote, vedere [Considerazioni sulla protezione per i dati](security-considerations-for-data.md). Per ulteriori informazioni sul round trip, vedere [contratti dati compatibili con](forward-compatible-data-contracts.md)le versioni successive.  
  
```csharp  
[ServiceBehavior(MaxItemsInObjectGraph=100000)]  
public class MyDataService:IDataService  
{  
    public DataPoint[] GetData()  
    {  
       // Implementation omitted  
    }  
}  
```  
  
```vb  
<ServiceBehavior(MaxItemsInObjectGraph:=100000)>  
Public Class MyDataService Implements IDataService  
  
    Function GetData() As DataPoint()  
         ‘ Implementation omitted  
    End Function  
End Interface  
```  
  
### <a name="serialization-behaviors"></a>Comportamenti di serializzazione  
 In WCF sono disponibili due comportamenti, e, <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior> che vengono automaticamente collegati a seconda del serializzatore utilizzato per una determinata operazione. Poiché questi comportamenti vengono attivati automaticamente, in genere non è necessario gestirli.  
  
 Tuttavia, le proprietà `DataContractSerializerOperationBehavior`, `MaxItemsInObjectGraph` e `IgnoreExtensionDataObject` del comportamento `DataContractSurrogate` possono essere utilizzate per personalizzare il processo di serializzazione. Come indicato nella sezione precedente, le prime due proprietà presentano lo stesso significato. La proprietà `DataContractSurrogate` può essere utilizzata per abilitare i surrogati di contratti di dati, ovvero un meccanismo avanzato di personalizzazione ed estensione del processo di serializzazione. Per ulteriori informazioni, vedere [surrogati del contratto dati](../extending/data-contract-surrogates.md).  
  
 La proprietà `DataContractSerializerOperationBehavior` consente di personalizzare la serializzazione sia del client sia del server. Nell'esempio seguente viene illustrato come aumentare la quota `MaxItemsInObjectGraph` del client.  
  
```csharp  
ChannelFactory<IDataService> factory = new ChannelFactory<IDataService>(binding, address);  
foreach (OperationDescription op in factory.Endpoint.Contract.Operations)  
{  
    DataContractSerializerOperationBehavior dataContractBehavior =  
                op.Behaviors.Find<DataContractSerializerOperationBehavior>()  
                as DataContractSerializerOperationBehavior;  
    if (dataContractBehavior != null)  
    {  
        dataContractBehavior.MaxItemsInObjectGraph = 100000;  
    }  
}  
IDataService client = factory.CreateChannel();  
```  
  
```vb  
Dim factory As ChannelFactory(Of IDataService) = New ChannelFactory(Of IDataService)(binding, address)  
For Each op As OperationDescription In factory.Endpoint.Contract.Operations  
        Dim dataContractBehavior As DataContractSerializerOperationBehavior = op.Behaviors.Find(Of DataContractSerializerOperationBehavior)()  
        If dataContractBehavior IsNot Nothing Then  
            dataContractBehavior.MaxItemsInObjectGraph = 100000  
        End If  
     Next  
    Dim client As IDataService = factory.CreateChannel  
```  
  
Di seguito è riportato il codice equivalente nel servizio, nel caso self-hosted:
  
```csharp  
ServiceHost serviceHost = new ServiceHost(typeof(IDataService))  
foreach (ServiceEndpoint ep in serviceHost.Description.Endpoints)  
{  
foreach (OperationDescription op in ep.Contract.Operations)  
{  
        DataContractSerializerOperationBehavior dataContractBehavior =  
           op.Behaviors.Find<DataContractSerializerOperationBehavior>()  
                as DataContractSerializerOperationBehavior;  
        if (dataContractBehavior != null)  
        {  
            dataContractBehavior.MaxItemsInObjectGraph = 100000;  
        }  
}  
}  
serviceHost.Open();  
```  
  
```vb  
Dim serviceHost As ServiceHost = New ServiceHost(GetType(IDataService))  
        For Each ep As ServiceEndpoint In serviceHost.Description.Endpoints  
            For Each op As OperationDescription In ep.Contract.Operations  
                Dim dataContractBehavior As DataContractSerializerOperationBehavior = op.Behaviors.Find(Of DataContractSerializerOperationBehavior)()  
  
                If dataContractBehavior IsNot Nothing Then  
                    dataContractBehavior.MaxItemsInObjectGraph = 100000  
                End If  
            Next  
        Next  
        serviceHost.Open()  
```  
  
 Nel caso di servizio ospitato su Web è invece necessario creare una nuova classe derivata `ServiceHost` e utilizzare una factory di host del servizio per attivarla.  
  
### <a name="controlling-serialization-settings-in-configuration"></a>Controllo delle impostazioni di serializzazione in configurazione  
 Le proprietà `MaxItemsInObjectGraph` e `IgnoreExtensionDataObject` possono essere controllate in configurazione tramite il comportamento di endpoint o di servizio del componente `dataContractSerializer`, come mostrato nell'esempio seguente.  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name="LargeQuotaBehavior">  
                    <dataContractSerializer  
                      maxItemsInObjectGraph="100000" />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
        <client>  
            <endpoint address="http://example.com/myservice"  
                  behaviorConfiguration="LargeQuotaBehavior"  
                binding="basicHttpBinding" bindingConfiguration=""
                            contract="IDataService"  
                name="" />  
        </client>  
    </system.serviceModel>  
</configuration>  
```  
  
### <a name="shared-type-serialization-object-graph-preservation-and-custom-serializers"></a>Serializzazione con condivisione di tipi, conservazione degli oggetti grafici e serializzatori personalizzati  
 La serializzazione eseguita dal componente <xref:System.Runtime.Serialization.DataContractSerializer> si basa su nomi di contratto di dati e non su nomi di tipo .NET. Ciò è in linea con i concetti di base dell'architettura orientata ai servizi e offre inoltre un elevato livello di flessibilità, in quanto i tipi .NET possono cambiare senza influire sul contratto di transito. In casi rari può risultare utile serializzare i nomi di tipo .NET effettivi. Questo approccio, analogamente alla tecnologia .NET Framework Remoting, comporta l'introduzione di un accoppiamento stretto fra client e server. Questa procedura non è consigliata, tranne nei casi rari che in genere si verificano quando si esegue la migrazione a WCF da .NET Framework comunicazione remota. In questo caso è necessario utilizzare la classe <xref:System.Runtime.Serialization.NetDataContractSerializer> anziché la classe <xref:System.Runtime.Serialization.DataContractSerializer>.  
  
 In genere il componente <xref:System.Runtime.Serialization.DataContractSerializer> serializza gli oggetti grafici come oggetti struttura. Ovvero, se esistono più riferimenti a uno stesso oggetto, quest'ultimo viene serializzato più volte. Si consideri ad esempio il caso di un'istanza della classe `PurchaseOrder` contenente i campi `billTo` e `shipTo` di tipo Address. Se entrambi i campi vengono impostati sulla stessa istanza di Address, dopo la serializzazione e la deserializzazione esistono due istanze identiche di Address. Ciò è dovuto al fatto che non esiste alcuna modalità standard interoperativa per rappresentare gli oggetti grafici in XML, salvo nel caso dello standard legacy con codifica SOAP disponibile nel motore <xref:System.Xml.Serialization.XmlSerializer>, come descritto nella sezione precedente relativa alle proprietà `Style` e `Use`. La serializzazione degli oggetti grafici come alberi comporta alcuni svantaggi. Ad esempio, risulta impossibile serializzare i grafici aventi riferimenti circolari. Talvolta occorre attivare la serializzazione degli oggetti grafici, anche se non è interoperativa. A tale scopo è possibile utilizzare il componente <xref:System.Runtime.Serialization.DataContractSerializer> costruito con il parametro `preserveObjectReferences` impostato su `true`.  
  
 Talvolta i serializzatori incorporati risultano insufficienti per lo scenario da gestire. Nella maggior parte dei casi è comunque possibile utilizzare l'astrazione <xref:System.Runtime.Serialization.XmlObjectSerializer> dalla quale derivano sia il serializzatore <xref:System.Runtime.Serialization.DataContractSerializer> sia il serializzatore <xref:System.Runtime.Serialization.NetDataContractSerializer>.  
  
 Per tutti e tre i casi precedenti (conservazione dei tipi .NET, conservazione degli oggetti grafici e serializzazione completamente personalizzata basata su `XmlObjectSerializer`) è necessario attivare un serializzatore personalizzato. A tale scopo, attenersi alla seguente procedura:  
  
1. Scrivere il comportamento personalizzato derivante dal comportamento <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>.  
  
2. Eseguire l'override dei due metodi `CreateSerializer` in modo che restituiscano il serializzatore personalizzato, sia esso <xref:System.Runtime.Serialization.NetDataContractSerializer>, <xref:System.Runtime.Serialization.DataContractSerializer> con il parametro `preserveObjectReferences` impostato su `true` oppure il serializzatore personalizzato <xref:System.Runtime.Serialization.XmlObjectSerializer>.  
  
3. Prima di aprire l'host del servizio o creare un canale client, rimuovere il comportamento <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> esistente e attivare la classe derivata personalizzata creata nei passaggi precedenti.  
  
 Per ulteriori informazioni sui concetti di serializzazione avanzati, vedere [serializzazione e deserializzazione](serialization-and-deserialization.md).  
  
## <a name="see-also"></a>Vedere anche

- [Utilizzo della classe XmlSerializer](using-the-xmlserializer-class.md)
- [Procedura: attivare il flusso](how-to-enable-streaming.md)
- [Procedura: creare un contratto dati di base per una classe o una struttura](how-to-create-a-basic-data-contract-for-a-class-or-structure.md)

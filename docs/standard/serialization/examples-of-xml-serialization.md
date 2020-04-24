---
title: Esempi di serializzazione XML
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XML serialization, examples
- arrays, serializing
- ICollection interface, serializing
- XmlSerializer class, serializing
- serialization, examples
- DataSet class, serializing
- XML Schema, serializing
ms.assetid: eec46337-9696-435b-a375-dc5effae6992
ms.openlocfilehash: 17ad1b4b5eae38a4f1dc90e154841b1315dea1b2
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74349769"
---
# <a name="examples-of-xml-serialization"></a><span data-ttu-id="ace7d-102">Esempi di serializzazione XML</span><span class="sxs-lookup"><span data-stu-id="ace7d-102">Examples of XML Serialization</span></span>

<span data-ttu-id="ace7d-103">La serializzazione XML può avere più di una forma, da semplice a complessa.</span><span class="sxs-lookup"><span data-stu-id="ace7d-103">XML serialization can take more than one form, from simple to complex.</span></span> <span data-ttu-id="ace7d-104">È ad esempio possibile serializzare una classe costituita semplicemente da proprietà e campi pubblici, come illustrato in [Introduzione alla serializzazione XML](../../../docs/standard/serialization/introducing-xml-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="ace7d-104">For example, you can serialize a class that simply consists of public fields and properties, as shown in [Introducing XML Serialization](../../../docs/standard/serialization/introducing-xml-serialization.md).</span></span> <span data-ttu-id="ace7d-105">Negli esempi di codice riportati di seguito vengono esaminati vari scenari avanzati, nonché come utilizzare la serializzazione XML per generare un flusso XML conforme a un documento XML Schema (XSD) specifico.</span><span class="sxs-lookup"><span data-stu-id="ace7d-105">The following code examples address various advanced scenarios, including how to use XML serialization to generate an XML stream that conforms to a specific XML Schema (XSD) document.</span></span>

## <a name="serializing-a-dataset"></a><span data-ttu-id="ace7d-106">Serializzazione di un Dataset</span><span class="sxs-lookup"><span data-stu-id="ace7d-106">Serializing a DataSet</span></span>

<span data-ttu-id="ace7d-107">Oltre a potere serializzare un'istanza di una classe pubblica, è anche possibile serializzare un'istanza di <xref:System.Data.DataSet>, come mostra l'esempio di codice riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ace7d-107">Besides serializing an instance of a public class, an instance of a <xref:System.Data.DataSet> can also be serialized, as shown in the following code example.</span></span>

```vb
Private Sub SerializeDataSet(filename As String)
    Dim ser As XmlSerializer = new XmlSerializer(GetType(DataSet))
    ' Creates a DataSet; adds a table, column, and ten rows.
    Dim ds As DataSet = new DataSet("myDataSet")
    Dim t As DataTable = new DataTable("table1")
    Dim c As DataColumn = new DataColumn("thing")
    t.Columns.Add(c)
    ds.Tables.Add(t)
    Dim r As DataRow
    Dim i As Integer
    for i = 0 to 10
        r = t.NewRow()
        r(0) = "Thing " &  i
        t.Rows.Add(r)
    Next
    Dim writer As TextWriter = new StreamWriter(filename)
    ser.Serialize(writer, ds)
    writer.Close()
End Sub
```

```csharp
private void SerializeDataSet(string filename){
    XmlSerializer ser = new XmlSerializer(typeof(DataSet));

    // Creates a DataSet; adds a table, column, and ten rows.
    DataSet ds = new DataSet("myDataSet");
    DataTable t = new DataTable("table1");
    DataColumn c = new DataColumn("thing");
    t.Columns.Add(c);
    ds.Tables.Add(t);
    DataRow r;
    for(int i = 0; i<10;i++){
        r = t.NewRow();
        r[0] = "Thing " + i;
        t.Rows.Add(r);
    }
    TextWriter writer = new StreamWriter(filename);
    ser.Serialize(writer, ds);
    writer.Close();
}
```

## <a name="serializing-an-xmlelement-and-xmlnode"></a><span data-ttu-id="ace7d-108">Serializzazione di XmlElement e XmlNode</span><span class="sxs-lookup"><span data-stu-id="ace7d-108">Serializing an XmlElement and XmlNode</span></span>

<span data-ttu-id="ace7d-109">È anche possibile serializzare le istanze <xref:System.Xml.XmlElement> di <xref:System.Xml.XmlNode> una classe o, come illustrato nell'esempio di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="ace7d-109">You can also serialize instances of an <xref:System.Xml.XmlElement> or <xref:System.Xml.XmlNode> class, as shown in the following code example.</span></span>

```vb
private Sub SerializeElement(filename As String)
    Dim ser As XmlSerializer = new XmlSerializer(GetType(XmlElement))
    Dim myElement As XmlElement = _
    new XmlDocument().CreateElement("MyElement", "ns")
    myElement.InnerText = "Hello World"
    Dim writer As TextWriter = new StreamWriter(filename)
    ser.Serialize(writer, myElement)
    writer.Close()
End Sub

Private Sub SerializeNode(filename As String)
    Dim ser As XmlSerializer = _
    new XmlSerializer(GetType(XmlNode))
    Dim myNode As XmlNode = new XmlDocument(). _
    CreateNode(XmlNodeType.Element, "MyNode", "ns")
    myNode.InnerText = "Hello Node"
    Dim writer As TextWriter = new StreamWriter(filename)
    ser.Serialize(writer, myNode)
    writer.Close()
End Sub
```

```csharp
private void SerializeElement(string filename){
    XmlSerializer ser = new XmlSerializer(typeof(XmlElement));
    XmlElement myElement=
    new XmlDocument().CreateElement("MyElement", "ns");
    myElement.InnerText = "Hello World";
    TextWriter writer = new StreamWriter(filename);
    ser.Serialize(writer, myElement);
    writer.Close();
}

private void SerializeNode(string filename){
    XmlSerializer ser = new XmlSerializer(typeof(XmlNode));
    XmlNode myNode= new XmlDocument().
    CreateNode(XmlNodeType.Element, "MyNode", "ns");
    myNode.InnerText = "Hello Node";
    TextWriter writer = new StreamWriter(filename);
    ser.Serialize(writer, myNode);
    writer.Close();
}
```

## <a name="serializing-a-class-that-contains-a-field-returning-a-complex-object"></a><span data-ttu-id="ace7d-110">Serializzazione di una classe contenente un campo che restituisce un oggetto complesso</span><span class="sxs-lookup"><span data-stu-id="ace7d-110">Serializing a Class that Contains a Field Returning a Complex Object</span></span>

<span data-ttu-id="ace7d-111">Se una proprietà o un campo restituisce un oggetto complesso (come una matrice o l'istanza di una classe), <xref:System.Xml.Serialization.XmlSerializer> lo converte in un elemento annidato nel documento XML principale.</span><span class="sxs-lookup"><span data-stu-id="ace7d-111">If a property or field returns a complex object (such as an array or a class instance), the <xref:System.Xml.Serialization.XmlSerializer> converts it to an element nested within the main XML document.</span></span> <span data-ttu-id="ace7d-112">Ad esempio, la prima classe nell'esempio di codice riportato di seguito, restituisce un'istanza della seconda classe.</span><span class="sxs-lookup"><span data-stu-id="ace7d-112">For example, the first class in the following code example returns an instance of the second class.</span></span>

```vb
Public Class PurchaseOrder
    Public MyAddress As Address
End Class

Public Class Address
    Public FirstName As String
End Class
```

```csharp
public class PurchaseOrder
{
    public Address MyAddress;
}
public class Address
{
    public string FirstName;
}
```

<span data-ttu-id="ace7d-113">L'output XML serializzato potrebbe assomigliare agli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ace7d-113">The serialized XML output might resemble the following.</span></span>

```xml
<PurchaseOrder>
    <MyAddress>
        <FirstName>George</FirstName>
    </MyAddress>
</PurchaseOrder>
```

## <a name="serializing-an-array-of-objects"></a><span data-ttu-id="ace7d-114">Serializzazione di una matrice di oggetti</span><span class="sxs-lookup"><span data-stu-id="ace7d-114">Serializing an Array of Objects</span></span>

<span data-ttu-id="ace7d-115">È inoltre possibile serializzare un campo che restituisce una matrice di oggetti, come mostra l'esempio di codice riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ace7d-115">You can also serialize a field that returns an array of objects, as shown in the following code example.</span></span>

```vb
Public Class PurchaseOrder
    public ItemsOrders () As Item
End Class

Public Class Item
    Public ItemID As String
    Public ItemPrice As decimal
End Class
```

```csharp
public class PurchaseOrder
{
    public Item [] ItemsOrders;
}

public class Item
{
    public string ItemID;
    public decimal ItemPrice;
}
```

<span data-ttu-id="ace7d-116">L'istanza della classe serializzata potrebbe assomigliare agli elementi seguenti, se due elementi sono ordinati.</span><span class="sxs-lookup"><span data-stu-id="ace7d-116">The serialized class instance might resemble the following, if two items are ordered.</span></span>

```xml
<PurchaseOrder xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <ItemsOrders>
        <Item>
            <ItemID>aaa111</ItemID>
            <ItemPrice>34.22</ItemPrice>
        </Item>
        <Item>
            <ItemID>bbb222</ItemID>
            <ItemPrice>2.89</ItemPrice>
        </Item>
    </ItemsOrders>
</PurchaseOrder>
```

## <a name="serializing-a-class-that-implements-the-icollection-interface"></a><span data-ttu-id="ace7d-117">Serializzazione di una classe che implementa l'interfaccia ICollection</span><span class="sxs-lookup"><span data-stu-id="ace7d-117">Serializing a Class that Implements the ICollection Interface</span></span>

<span data-ttu-id="ace7d-118">È possibile creare classi di raccolte mediante l'implementazione dell'interfaccia <xref:System.Collections.ICollection> e utilizzare <xref:System.Xml.Serialization.XmlSerializer> per serializzare istanze di tali classi.</span><span class="sxs-lookup"><span data-stu-id="ace7d-118">You can create your own collection classes by implementing the <xref:System.Collections.ICollection> interface, and use the <xref:System.Xml.Serialization.XmlSerializer> to serialize instances of these classes.</span></span> <span data-ttu-id="ace7d-119">Notare che quando una classe implementa l'interfaccia <xref:System.Collections.ICollection>, viene serializzato solo la raccolta contenuta dalla classe.</span><span class="sxs-lookup"><span data-stu-id="ace7d-119">Note that when a class implements the <xref:System.Collections.ICollection> interface, only the collection contained by the class is serialized.</span></span> <span data-ttu-id="ace7d-120">Le proprietà pubbliche o i campi aggiunti alla classe non verranno serializzati.</span><span class="sxs-lookup"><span data-stu-id="ace7d-120">Any public properties or fields added to the class will not be serialized.</span></span> <span data-ttu-id="ace7d-121">La classe deve includere un metodo **Add** e una proprietà **Item** (indicizzatore C#) da serializzare.</span><span class="sxs-lookup"><span data-stu-id="ace7d-121">The class must include an **Add** method and an **Item** property (C# indexer) to be serialized.</span></span>

```vb
Imports System.Collections
Imports System.IO
Imports System.Xml.Serialization

Public Class Test
    Shared Sub Main()
        Dim t As Test= new Test()
        t.SerializeCollection("coll.xml")
    End Sub

    Private Sub SerializeCollection(filename As String)
        Dim Emps As Employees  = new Employees()
        ' Note that only the collection is serialized -- not the
        ' CollectionName or any other public property of the class.
        Emps.CollectionName = "Employees"
        Dim John100 As Employee = new Employee("John", "100xxx")
        Emps.Add(John100)
        Dim x As XmlSerializer = new XmlSerializer(GetType(Employees))
        Dim writer As TextWriter = new StreamWriter(filename)
        x.Serialize(writer, Emps)
        writer.Close()
    End Sub
End Class

Public Class Employees
    Implements ICollection
    Public CollectionName As String
    Private empArray As ArrayList = new ArrayList()

    Public ReadOnly Default Overloads _
    Property Item(index As Integer) As Employee
        get
        return CType (empArray(index), Employee)
        End Get
    End Property

    Public Sub CopyTo(a As Array, index As Integer) _
    Implements ICollection.CopyTo
        empArray.CopyTo(a, index)
    End Sub

    Public ReadOnly Property Count () As integer Implements _
    ICollection.Count
        get
            Count = empArray.Count
        End Get

    End Property

    Public ReadOnly Property SyncRoot ()As Object _
    Implements ICollection.SyncRoot
        get
        return me
        End Get
    End Property

    Public ReadOnly Property IsSynchronized () As Boolean _
    Implements ICollection.IsSynchronized
        get
        return false
        End Get
    End Property

    Public Function GetEnumerator() As IEnumerator _
    Implements IEnumerable.GetEnumerator

        return empArray.GetEnumerator()
    End Function

    Public Function Add(newEmployee As Employee) As Integer
        empArray.Add(newEmployee)
        return empArray.Count
    End Function
End Class

Public Class Employee
    Public EmpName As String
    Public EmpID As String

    Public Sub New ()
    End Sub

    Public Sub New (newName As String , newID As String )
        EmpName = newName
        EmpID = newID
    End Sub
End Class
```

```csharp
using System;
using System.Collections;
using System.IO;
using System.Xml.Serialization;

public class Test {
    static void Main(){
        Test t = new Test();
        t.SerializeCollection("coll.xml");
    }

    private void SerializeCollection(string filename){
        Employees Emps = new Employees();
        // Note that only the collection is serialized -- not the
        // CollectionName or any other public property of the class.
        Emps.CollectionName = "Employees";
        Employee John100 = new Employee("John", "100xxx");
        Emps.Add(John100);
        XmlSerializer x = new XmlSerializer(typeof(Employees));
        TextWriter writer = new StreamWriter(filename);
        x.Serialize(writer, Emps);
    }
}
public class Employees:ICollection {
    public string CollectionName;
    private ArrayList empArray = new ArrayList();

    public Employee this[int index]{
        get{return (Employee) empArray[index];}
    }

    public void CopyTo(Array a, int index){
        empArray.CopyTo(a, index);
    }
    public int Count{
        get{return empArray.Count;}
    }
    public object SyncRoot{
        get{return this;}
    }
    public bool IsSynchronized{
        get{return false;}
    }
    public IEnumerator GetEnumerator(){
        return empArray.GetEnumerator();
    }

    public void Add(Employee newEmployee){
        empArray.Add(newEmployee);
    }
}

public class Employee {
    public string EmpName;
    public string EmpID;
    public Employee(){}
    public Employee(string empName, string empID){
        EmpName = empName;
        EmpID = empID;
    }
}
```

## <a name="purchase-order-example"></a><span data-ttu-id="ace7d-122">Esempio di ordine di acquisto</span><span class="sxs-lookup"><span data-stu-id="ace7d-122">Purchase Order Example</span></span>

<span data-ttu-id="ace7d-123">È possibile tagliare e incollare il codice di esempio riportato di seguito in un file di testo rinominato con un'estensione del nome file cs o vb.</span><span class="sxs-lookup"><span data-stu-id="ace7d-123">You can cut and paste the following example code into a text file renamed with a .cs or .vb file name extension.</span></span> <span data-ttu-id="ace7d-124">Utilizzare il compilatore C# o Visual Basic per compilare il file.</span><span class="sxs-lookup"><span data-stu-id="ace7d-124">Use the C# or Visual Basic compiler to compile the file.</span></span> <span data-ttu-id="ace7d-125">Quindi eseguirlo utilizzando il nome del file eseguibile.</span><span class="sxs-lookup"><span data-stu-id="ace7d-125">Then run it using the name of the executable.</span></span>

<span data-ttu-id="ace7d-126">In questo esempio viene utilizzato un semplice scenario per dimostrare come viene creata e serializzata un'istanza di un oggetto in un flusso di file tramite il metodo <xref:System.Xml.Serialization.XmlSerializer.Serialize%2A>.</span><span class="sxs-lookup"><span data-stu-id="ace7d-126">This example uses a simple scenario to demonstrate how an instance of an object is created and serialized into a file stream using the <xref:System.Xml.Serialization.XmlSerializer.Serialize%2A> method.</span></span> <span data-ttu-id="ace7d-127">Il flusso XML viene salvato in un file e lo stesso file viene riletto e ricostruito in una copia dell'oggetto originale tramite il metodo <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A>.</span><span class="sxs-lookup"><span data-stu-id="ace7d-127">The XML stream is saved to a file, and the same file is then read back and reconstructed into a copy of the original object using the <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A> method.</span></span>

<span data-ttu-id="ace7d-128">In questo esempio, viene serializzata e successivamente deserializzata una classe denominata `PurchaseOrder`.</span><span class="sxs-lookup"><span data-stu-id="ace7d-128">In this example, a class named `PurchaseOrder` is serialized and then deserialized.</span></span> <span data-ttu-id="ace7d-129">Viene inoltre inclusa una seconda classe denominata `Address`, poiché il campo pubblico denominato `ShipTo` deve essere impostato su un `Address`.</span><span class="sxs-lookup"><span data-stu-id="ace7d-129">A second class named `Address` is also included because the public field named `ShipTo` must be set to an `Address`.</span></span> <span data-ttu-id="ace7d-130">Analogamente, viene inclusa una classe `OrderedItem`, poiché è necessario impostare una matrice di oggetti `OrderedItem` nel campo `OrderedItems`.</span><span class="sxs-lookup"><span data-stu-id="ace7d-130">Similarly, an `OrderedItem` class is included because an array of `OrderedItem` objects must be set to the `OrderedItems` field.</span></span> <span data-ttu-id="ace7d-131">Infine, una classe denominata `Test` contiene il codice che serializza e deserializza le classi.</span><span class="sxs-lookup"><span data-stu-id="ace7d-131">Finally, a class named `Test` contains the code that serializes and deserializes the classes.</span></span>

<span data-ttu-id="ace7d-132">Il metodo `CreatePO` crea gli oggetti di classe `PurchaseOrder`, `Address` e `OrderedItem` e imposta i valori del campo pubblico.</span><span class="sxs-lookup"><span data-stu-id="ace7d-132">The `CreatePO` method creates the `PurchaseOrder`, `Address`, and `OrderedItem` class objects, and sets the public field values.</span></span> <span data-ttu-id="ace7d-133">Il metodo costruisce inoltre un'istanza della classe <xref:System.Xml.Serialization.XmlSerializer> utilizzata per serializzare e deserializzare `PurchaseOrder`.</span><span class="sxs-lookup"><span data-stu-id="ace7d-133">The method also constructs an instance of the <xref:System.Xml.Serialization.XmlSerializer> class that is used to serialize and deserialize the `PurchaseOrder`.</span></span> <span data-ttu-id="ace7d-134">Notare che il codice passa il tipo della classe che sarà serializzato al costruttore.</span><span class="sxs-lookup"><span data-stu-id="ace7d-134">Note that the code passes the type of the class that will be serialized to the constructor.</span></span> <span data-ttu-id="ace7d-135">Il codice crea anche un `FileStream` usato per scrivere il flusso XML in un documento XML.</span><span class="sxs-lookup"><span data-stu-id="ace7d-135">The code also creates a `FileStream` that is used to write the XML stream to an XML document.</span></span>

<span data-ttu-id="ace7d-136">Il metodo `ReadPo` è un po' più semplice.</span><span class="sxs-lookup"><span data-stu-id="ace7d-136">The `ReadPo` method is a little simpler.</span></span> <span data-ttu-id="ace7d-137">Tale metodo crea semplicemente gli oggetti da deserializzare e ne legge i valori.</span><span class="sxs-lookup"><span data-stu-id="ace7d-137">It just creates objects to deserialize and reads out their values.</span></span> <span data-ttu-id="ace7d-138">Come per il `CreatePo` metodo, è necessario prima costruire un <xref:System.Xml.Serialization.XmlSerializer>oggetto, passando il tipo della classe da deserializzare al costruttore.</span><span class="sxs-lookup"><span data-stu-id="ace7d-138">As with the `CreatePo` method, you must first construct an <xref:System.Xml.Serialization.XmlSerializer>, passing the type of the class to be deserialized to the constructor.</span></span> <span data-ttu-id="ace7d-139">Inoltre, per leggere il documento XML è necessaria una classe <xref:System.IO.FileStream>.</span><span class="sxs-lookup"><span data-stu-id="ace7d-139">Also, a <xref:System.IO.FileStream> is required to read the XML document.</span></span> <span data-ttu-id="ace7d-140">Per deserializzare gli oggetti, chiamare il metodo <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A> con la classe <xref:System.IO.FileStream> come argomento.</span><span class="sxs-lookup"><span data-stu-id="ace7d-140">To deserialize the objects, call the <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A> method with the <xref:System.IO.FileStream> as an argument.</span></span> <span data-ttu-id="ace7d-141">È necessario eseguire il cast dell'oggetto deserializzato su una variabile oggetto di tipo `PurchaseOrder`.</span><span class="sxs-lookup"><span data-stu-id="ace7d-141">The deserialized object must be cast to an object variable of type `PurchaseOrder`.</span></span> <span data-ttu-id="ace7d-142">Il codice legge quindi i valori della classe `PurchaseOrder` deserializzata.</span><span class="sxs-lookup"><span data-stu-id="ace7d-142">The code then reads the values of the deserialized `PurchaseOrder`.</span></span> <span data-ttu-id="ace7d-143">Notare che è inoltre possibile leggere il file PO.xml creato per visualizzare l'output XML effettivo.</span><span class="sxs-lookup"><span data-stu-id="ace7d-143">Note that you can also read the PO.xml file that is created to see the actual XML output.</span></span>

```vb
Imports System.IO
Imports System.Xml
Imports System.Xml.Serialization
Imports Microsoft.VisualBasic

' The XmlRoot attribute allows you to set an alternate name
' (PurchaseOrder) for the XML element and its namespace. By
' default, the XmlSerializer uses the class name. The attribute
' also allows you to set the XML namespace for the element. Lastly,
' the attribute sets the IsNullable property, which specifies whether
' the xsi:null attribute appears if the class instance is set to
' a null reference.
<XmlRoot("PurchaseOrder", _
 Namespace := "http://www.cpandl.com", IsNullable := False)> _
Public Class PurchaseOrder
    Public ShipTo As Address
    Public OrderDate As String
    ' The XmlArrayAttribute changes the XML element name
    ' from the default of "OrderedItems" to "Items".
    <XmlArray("Items")> _
    Public OrderedItems() As OrderedItem
    Public SubTotal As Decimal
    Public ShipCost As Decimal
    Public TotalCost As Decimal
End Class

Public Class Address
    ' The XmlAttribute attribute instructs the XmlSerializer to serialize the
    ' Name field as an XML attribute instead of an XML element (XML element is
    ' the default behavior).
    <XmlAttribute()> _
    Public Name As String
    Public Line1 As String

    ' Setting the IsNullable property to false instructs the
    ' XmlSerializer that the XML attribute will not appear if
    ' the City field is set to a null reference.
    <XmlElement(IsNullable := False)> _
    Public City As String
    Public State As String
    Public Zip As String
End Class

Public Class OrderedItem
    Public ItemName As String
    Public Description As String
    Public UnitPrice As Decimal
    Public Quantity As Integer
    Public LineTotal As Decimal

    ' Calculate is a custom method that calculates the price per item
    ' and stores the value in a field.
    Public Sub Calculate()
    LineTotal = UnitPrice * Quantity
    End Sub
End Class

Public Class Test
        Public Shared Sub Main()
    ' Read and write purchase orders.
    Dim t As New Test()
    t.CreatePO("po.xml")
    t.ReadPO("po.xml")
    End Sub

    Private Sub CreatePO(filename As String)
        ' Creates an instance of the XmlSerializer class;
        ' specifies the type of object to serialize.
        Dim serializer As New XmlSerializer(GetType(PurchaseOrder))
        Dim writer As New StreamWriter(filename)
        Dim po As New PurchaseOrder()

        ' Creates an address to ship and bill to.
        Dim billAddress As New Address()
        billAddress.Name = "Teresa Atkinson"
        billAddress.Line1 = "1 Main St."
        billAddress.City = "AnyTown"
        billAddress.State = "WA"
        billAddress.Zip = "00000"
        ' Set ShipTo and BillTo to the same addressee.
        po.ShipTo = billAddress
        po.OrderDate = System.DateTime.Now.ToLongDateString()

        ' Creates an OrderedItem.
        Dim i1 As New OrderedItem()
        i1.ItemName = "Widget S"
        i1.Description = "Small widget"
        i1.UnitPrice = CDec(5.23)
        i1.Quantity = 3
        i1.Calculate()

        ' Inserts the item into the array.
        Dim items(0) As OrderedItem
        items(0) = i1
        po.OrderedItems = items
        ' Calculates the total cost.
        Dim subTotal As New Decimal()
        Dim oi As OrderedItem
        For Each oi In  items
            subTotal += oi.LineTotal
        Next oi
        po.SubTotal = subTotal
        po.ShipCost = CDec(12.51)
        po.TotalCost = po.SubTotal + po.ShipCost
        ' Serializes the purchase order, and close the TextWriter.
        serializer.Serialize(writer, po)
        writer.Close()
    End Sub

    Protected Sub ReadPO(filename As String)
        ' Creates an instance of the XmlSerializer class;
        ' specifies the type of object to be deserialized.
        Dim serializer As New XmlSerializer(GetType(PurchaseOrder))
        ' If the XML document has been altered with unknown
        ' nodes or attributes, handles them with the
        ' UnknownNode and UnknownAttribute events.
        AddHandler serializer.UnknownNode, AddressOf serializer_UnknownNode
        AddHandler serializer.UnknownAttribute, AddressOf _
        serializer_UnknownAttribute

        ' A FileStream is needed to read the XML document.
        Dim fs As New FileStream(filename, FileMode.Open)
        ' Declare an object variable of the type to be deserialized.
        Dim po As PurchaseOrder
        ' Uses the Deserialize method to restore the object's state
        ' with data from the XML document.
        po = CType(serializer.Deserialize(fs), PurchaseOrder)
        ' Reads the order date.
        Console.WriteLine(("OrderDate: " & po.OrderDate))

        ' Reads the shipping address.
        Dim shipTo As Address = po.ShipTo
        ReadAddress(shipTo, "Ship To:")
        ' Reads the list of ordered items.
        Dim items As OrderedItem() = po.OrderedItems
        Console.WriteLine("Items to be shipped:")
        Dim oi As OrderedItem
        For Each oi In items
            Console.WriteLine((ControlChars.Tab & oi.ItemName & _
            ControlChars.Tab & _
                oi.Description & ControlChars.Tab & oi.UnitPrice & _
                ControlChars.Tab & _
                oi.Quantity & ControlChars.Tab & oi.LineTotal))
        Next oi
        ' Reads the subtotal, shipping cost, and total cost.
        Console.WriteLine((ControlChars.Cr & New String _
        (ControlChars.Tab, 5) & _
        " Subtotal" & ControlChars.Tab & po.SubTotal & ControlChars.Cr & _
        New String(ControlChars.Tab, 5) & " Shipping" & ControlChars.Tab & _
        po.ShipCost & ControlChars.Cr &  New String(ControlChars.Tab, 5) & _
        " Total" & New String(ControlChars.Tab, 2) & po.TotalCost))
    End Sub

    Protected Sub ReadAddress(a As Address, label As String)
        ' Reads the fields of the Address.
        Console.WriteLine(label)
        Console.Write((ControlChars.Tab & a.Name & ControlChars.Cr & _
        ControlChars.Tab & a.Line1 & ControlChars.Cr & ControlChars.Tab & _
        a.City & ControlChars.Tab & a.State & ControlChars.Cr & _
        ControlChars.Tab & a.Zip & ControlChars.Cr))
    End Sub

    Protected Sub serializer_UnknownNode(sender As Object, e As _
    XmlNodeEventArgs)
        Console.WriteLine(("Unknown Node:" & e.Name & _
        ControlChars.Tab & e.Text))
    End Sub

    Protected Sub serializer_UnknownAttribute(sender As Object, _
    e As XmlAttributeEventArgs)
        Dim attr As System.Xml.XmlAttribute = e.Attr
        Console.WriteLine(("Unknown attribute " & attr.Name & "='" & _
        attr.Value & "'"))
    End Sub 'serializer_UnknownAttribute
End Class 'Test
```

```csharp
using System;
using System.IO;
using System.Xml;
using System.Xml.Serialization;

// The XmlRoot attribute allows you to set an alternate name
// (PurchaseOrder) for the XML element and its namespace. By
// default, the XmlSerializer uses the class name. The attribute
// also allows you to set the XML namespace for the element. Lastly,
// the attribute sets the IsNullable property, which specifies whether
// the xsi:null attribute appears if the class instance is set to
// a null reference.
[XmlRoot("PurchaseOrder", Namespace="http://www.cpandl.com",
IsNullable = false)]
public class PurchaseOrder
{
    public Address ShipTo;
    public string OrderDate;
    // The XmlArray attribute changes the XML element name
    // from the default of "OrderedItems" to "Items".
    [XmlArray("Items")]
    public OrderedItem[] OrderedItems;
    public decimal SubTotal;
    public decimal ShipCost;
    public decimal TotalCost;
}

public class Address
{
    // The XmlAttribute attribute instructs the XmlSerializer to serialize the
    // Name field as an XML attribute instead of an XML element (XML element is
    // the default behavior).
    [XmlAttribute]
    public string Name;
    public string Line1;

    // Setting the IsNullable property to false instructs the
    // XmlSerializer that the XML attribute will not appear if
    // the City field is set to a null reference.
    [XmlElement(IsNullable = false)]
    public string City;
    public string State;
    public string Zip;
}

public class OrderedItem
{
    public string ItemName;
    public string Description;
    public decimal UnitPrice;
    public int Quantity;
    public decimal LineTotal;

    // Calculate is a custom method that calculates the price per item
    // and stores the value in a field.
    public void Calculate()
    {
        LineTotal = UnitPrice * Quantity;
    }
}

public class Test
{
    public static void Main()
    {
        // Read and write purchase orders.
        Test t = new Test();
        t.CreatePO("po.xml");
        t.ReadPO("po.xml");
    }

    private void CreatePO(string filename)
    {
        // Creates an instance of the XmlSerializer class;
        // specifies the type of object to serialize.
        XmlSerializer serializer =
        new XmlSerializer(typeof(PurchaseOrder));
        TextWriter writer = new StreamWriter(filename);
        PurchaseOrder po=new PurchaseOrder();

        // Creates an address to ship and bill to.
        Address billAddress = new Address();
        billAddress.Name = "Teresa Atkinson";
        billAddress.Line1 = "1 Main St.";
        billAddress.City = "AnyTown";
        billAddress.State = "WA";
        billAddress.Zip = "00000";
        // Sets ShipTo and BillTo to the same addressee.
        po.ShipTo = billAddress;
        po.OrderDate = System.DateTime.Now.ToLongDateString();

        // Creates an OrderedItem.
        OrderedItem i1 = new OrderedItem();
        i1.ItemName = "Widget S";
        i1.Description = "Small widget";
        i1.UnitPrice = (decimal) 5.23;
        i1.Quantity = 3;
        i1.Calculate();

        // Inserts the item into the array.
        OrderedItem [] items = {i1};
        po.OrderedItems = items;
        // Calculate the total cost.
        decimal subTotal = new decimal();
        foreach(OrderedItem oi in items)
        {
            subTotal += oi.LineTotal;
        }
        po.SubTotal = subTotal;
        po.ShipCost = (decimal) 12.51;
        po.TotalCost = po.SubTotal + po.ShipCost;
        // Serializes the purchase order, and closes the TextWriter.
        serializer.Serialize(writer, po);
        writer.Close();
    }

    protected void ReadPO(string filename)
    {
        // Creates an instance of the XmlSerializer class;
        // specifies the type of object to be deserialized.
        XmlSerializer serializer = new XmlSerializer(typeof(PurchaseOrder));
        // If the XML document has been altered with unknown
        // nodes or attributes, handles them with the
        // UnknownNode and UnknownAttribute events.
        serializer.UnknownNode+= new
        XmlNodeEventHandler(serializer_UnknownNode);
        serializer.UnknownAttribute+= new
        XmlAttributeEventHandler(serializer_UnknownAttribute);

        // A FileStream is needed to read the XML document.
        FileStream fs = new FileStream(filename, FileMode.Open);
        // Declares an object variable of the type to be deserialized.
        PurchaseOrder po;
        // Uses the Deserialize method to restore the object's state
        // with data from the XML document. */
        po = (PurchaseOrder) serializer.Deserialize(fs);
        // Reads the order date.
        Console.WriteLine ("OrderDate: " + po.OrderDate);

        // Reads the shipping address.
        Address shipTo = po.ShipTo;
        ReadAddress(shipTo, "Ship To:");
        // Reads the list of ordered items.
        OrderedItem [] items = po.OrderedItems;
        Console.WriteLine("Items to be shipped:");
        foreach(OrderedItem oi in items)
        {
            Console.WriteLine("\t"+
            oi.ItemName + "\t" +
            oi.Description + "\t" +
            oi.UnitPrice + "\t" +
            oi.Quantity + "\t" +
            oi.LineTotal);
        }
        // Reads the subtotal, shipping cost, and total cost.
        Console.WriteLine(
        "\n\t\t\t\t\t Subtotal\t" + po.SubTotal +
        "\n\t\t\t\t\t Shipping\t" + po.ShipCost +
        "\n\t\t\t\t\t Total\t\t" + po.TotalCost
        );
    }

    protected void ReadAddress(Address a, string label)
    {
        // Reads the fields of the Address.
        Console.WriteLine(label);
        Console.Write("\t"+
        a.Name +"\n\t" +
        a.Line1 +"\n\t" +
        a.City +"\t" +
        a.State +"\n\t" +
        a.Zip +"\n");
    }

    protected void serializer_UnknownNode
    (object sender, XmlNodeEventArgs e)
    {
        Console.WriteLine("Unknown Node:" +   e.Name + "\t" + e.Text);
    }

    protected void serializer_UnknownAttribute
    (object sender, XmlAttributeEventArgs e)
    {
        System.Xml.XmlAttribute attr = e.Attr;
        Console.WriteLine("Unknown attribute " +
        attr.Name + "='" + attr.Value + "'");
    }
}
```

<span data-ttu-id="ace7d-144">L'output XML potrebbe assomigliare agli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ace7d-144">The XML output might resemble the following.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<PurchaseOrder xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://www.cpandl.com">
    <ShipTo Name="Teresa Atkinson">
        <Line1>1 Main St.</Line1>
        <City>AnyTown</City>
        <State>WA</State>
        <Zip>00000</Zip>
    </ShipTo>
    <OrderDate>Wednesday, June 27, 2001</OrderDate>
    <Items>
        <OrderedItem>
            <ItemName>Widget S</ItemName>
            <Description>Small widget</Description>
            <UnitPrice>5.23</UnitPrice>
            <Quantity>3</Quantity>
            <LineTotal>15.69</LineTotal>
        </OrderedItem>
    </Items>
    <SubTotal>15.69</SubTotal>
    <ShipCost>12.51</ShipCost>
    <TotalCost>28.2</TotalCost>
</PurchaseOrder>
```

## <a name="see-also"></a><span data-ttu-id="ace7d-145">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="ace7d-145">See also</span></span>

- [<span data-ttu-id="ace7d-146">Introduzione alla serializzazione XML</span><span class="sxs-lookup"><span data-stu-id="ace7d-146">Introducing XML Serialization</span></span>](introducing-xml-serialization.md)
- [<span data-ttu-id="ace7d-147">Controllo della serializzazione XML mediante attributi</span><span class="sxs-lookup"><span data-stu-id="ace7d-147">Controlling XML Serialization Using Attributes</span></span>](controlling-xml-serialization-using-attributes.md)
- [<span data-ttu-id="ace7d-148">Attributi che controllano la serializzazione XML</span><span class="sxs-lookup"><span data-stu-id="ace7d-148">Attributes That Control XML Serialization</span></span>](attributes-that-control-xml-serialization.md)
- [<span data-ttu-id="ace7d-149">Classe XmlSerializer</span><span class="sxs-lookup"><span data-stu-id="ace7d-149">XmlSerializer Class</span></span>](xref:System.Xml.Serialization.XmlSerializer)
- [<span data-ttu-id="ace7d-150">Procedura: serializzare un oggetto</span><span class="sxs-lookup"><span data-stu-id="ace7d-150">How to: Serialize an Object</span></span>](how-to-serialize-an-object.md)
- [<span data-ttu-id="ace7d-151">Procedura: Deserializzare un oggetto</span><span class="sxs-lookup"><span data-stu-id="ace7d-151">How to: Deserialize an Object</span></span>](how-to-deserialize-an-object.md)

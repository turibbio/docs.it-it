---
title: XmlSchemaSet per la compilazione di schemi
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 55c4b175-3170-4071-9d60-dd5a42f79b54
ms.openlocfilehash: 44850755c41b212e88e0b90dd3b016f96a0af96d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290227"
---
# <a name="xmlschemaset-for-schema-compilation"></a><span data-ttu-id="9cd46-102">XmlSchemaSet per la compilazione di schemi</span><span class="sxs-lookup"><span data-stu-id="9cd46-102">XmlSchemaSet for Schema Compilation</span></span>
<span data-ttu-id="9cd46-103">Viene descritto <xref:System.Xml.Schema.XmlSchemaSet>, ovvero una cache in cui è possibile archiviare e convalidare gli schemi XSD (XML Schema Definition Language).</span><span class="sxs-lookup"><span data-stu-id="9cd46-103">Describes the <xref:System.Xml.Schema.XmlSchemaSet>, a cache where XML Schema definition language (XSD) schemas can be stored and validated.</span></span>  
  
## <a name="the-xmlschemaset-class"></a><span data-ttu-id="9cd46-104">La classe XmlSchemaSet</span><span class="sxs-lookup"><span data-stu-id="9cd46-104">The XmlSchemaSet Class</span></span>  
 <span data-ttu-id="9cd46-105">Il tipo <xref:System.Xml.Schema.XmlSchemaSet> è una cache in cui è possibile archiviare e convalidare gli schemi XSD (XML Schema Definition Language).</span><span class="sxs-lookup"><span data-stu-id="9cd46-105">The <xref:System.Xml.Schema.XmlSchemaSet> is a cache where XML Schema definition language (XSD) schemas can be stored and validated.</span></span>  
  
 <span data-ttu-id="9cd46-106">In <xref:System.Xml?displayProperty=nameWithType> versione 1.0, gli schemi XML venivano caricati in una classe <xref:System.Xml.Schema.XmlSchemaCollection> come una libreria di schemi.</span><span class="sxs-lookup"><span data-stu-id="9cd46-106">In <xref:System.Xml?displayProperty=nameWithType> version 1.0, XML schemas were loaded into an <xref:System.Xml.Schema.XmlSchemaCollection> class as a library of schemas.</span></span> <span data-ttu-id="9cd46-107">In <xref:System.Xml?displayProperty=nameWithType> versione 2.0, le classi <xref:System.Xml.XmlValidatingReader> e <xref:System.Xml.Schema.XmlSchemaCollection> sono obsolete e sono state sostituite dai metodi <xref:System.Xml.XmlReader.Create%2A> e dalla classe <xref:System.Xml.Schema.XmlSchemaSet> rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="9cd46-107">In <xref:System.Xml?displayProperty=nameWithType> version 2.0, the <xref:System.Xml.XmlValidatingReader> and the <xref:System.Xml.Schema.XmlSchemaCollection> classes are obsolete, and have been replaced by the <xref:System.Xml.XmlReader.Create%2A> methods, and the <xref:System.Xml.Schema.XmlSchemaSet> class respectively.</span></span>  
  
 <span data-ttu-id="9cd46-108">Il tipo <xref:System.Xml.Schema.XmlSchemaSet> è stato introdotto per risolvere una serie di problemi che includono la compatibilità con gli standard, le prestazioni e il formato obsoleto dello schema XDR (XML-Data Reduced) di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9cd46-108">The <xref:System.Xml.Schema.XmlSchemaSet> has been introduced to fix a number of issues including standards compatibility, performance, and the obsolete Microsoft XML-Data Reduced (XDR) schema format.</span></span>  
  
 <span data-ttu-id="9cd46-109">Di seguito viene riportato un confronto tra le classi <xref:System.Xml.Schema.XmlSchemaCollection> e <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-109">The following is a comparison between the <xref:System.Xml.Schema.XmlSchemaCollection> class and the <xref:System.Xml.Schema.XmlSchemaSet> class.</span></span>  
  
|<span data-ttu-id="9cd46-110">XmlSchemaCollection</span><span class="sxs-lookup"><span data-stu-id="9cd46-110">XmlSchemaCollection</span></span>|<span data-ttu-id="9cd46-111">XmlSchemaSet</span><span class="sxs-lookup"><span data-stu-id="9cd46-111">XmlSchemaSet</span></span>|  
|-------------------------|------------------|  
|<span data-ttu-id="9cd46-112">Supporta gli schemi XDR di Microsoft e gli schemi XML di W3C.</span><span class="sxs-lookup"><span data-stu-id="9cd46-112">Supports Microsoft XDR and W3C XML schemas.</span></span>|<span data-ttu-id="9cd46-113">Supporta solo gli schemi XML di W3C.</span><span class="sxs-lookup"><span data-stu-id="9cd46-113">Only supports W3C XML schemas.</span></span>|  
|<span data-ttu-id="9cd46-114">Gli schemi vengono compilati quando si chiama il metodo <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-114">Schemas are compiled when the <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> method is called.</span></span>|<span data-ttu-id="9cd46-115">Gli schemi non vengono compilati quando si chiama il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-115">Schemas are not compiled when the <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> method is called.</span></span> <span data-ttu-id="9cd46-116">Questo fornisce prestazioni migliori durante la creazione della libreria di schemi.</span><span class="sxs-lookup"><span data-stu-id="9cd46-116">This provides a performance improvement during creation of the schema library.</span></span>|  
|<span data-ttu-id="9cd46-117">Ogni schema consente di generare una singola versione compilata che può creare "isole di schemi".</span><span class="sxs-lookup"><span data-stu-id="9cd46-117">Each schema generates an individual compiled version that can result in "schema islands."</span></span> <span data-ttu-id="9cd46-118">Di conseguenza, tutte le operazioni di inclusione e importazione vengono eseguite nell'ambito di tale schema.</span><span class="sxs-lookup"><span data-stu-id="9cd46-118">As a result, all includes and imports are scoped only within that schema.</span></span>|<span data-ttu-id="9cd46-119">Gli schemi compilati consentono di generare un singolo schema logico, ovvero un "set" di schemi.</span><span class="sxs-lookup"><span data-stu-id="9cd46-119">Compiled schemas generate a single logical schema, a "set" of schemas.</span></span> <span data-ttu-id="9cd46-120">Gli schemi importati all'interno di uno schema vengono aggiunti direttamente al set.</span><span class="sxs-lookup"><span data-stu-id="9cd46-120">Any imported schemas within a schema that are added to the set are directly added to the set themselves.</span></span> <span data-ttu-id="9cd46-121">Ciò significa che tutti i tipi sono disponibili per tutti gli schemi.</span><span class="sxs-lookup"><span data-stu-id="9cd46-121">This means that all types are available to all schemas.</span></span>|  
|<span data-ttu-id="9cd46-122">Nella raccolta può essere presente solo uno schema per un determinato spazio dei nomi di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9cd46-122">Only one schema for a particular target namespace can exist in the collection.</span></span>|<span data-ttu-id="9cd46-123">È possibile aggiungere più schemi per lo stesso spazio dei nomi di destinazione, a condizione che non si verifichino conflitti di tipi.</span><span class="sxs-lookup"><span data-stu-id="9cd46-123">Multiple schemas for the same target namespace can be added as long as there are no type conflicts.</span></span>|  
  
## <a name="migrating-to-the-xmlschemaset"></a><span data-ttu-id="9cd46-124">Migrazione a XmlSchemaSet</span><span class="sxs-lookup"><span data-stu-id="9cd46-124">Migrating to the XmlSchemaSet</span></span>  
 <span data-ttu-id="9cd46-125">Nel seguente esempio di codice viene fornita una guida per eseguire la migrazione alla nuova classe <xref:System.Xml.Schema.XmlSchemaSet> dalla classe obsoleta <xref:System.Xml.Schema.XmlSchemaCollection>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-125">The following code example provides a guide to migrating to the new <xref:System.Xml.Schema.XmlSchemaSet> class from the obsolete <xref:System.Xml.Schema.XmlSchemaCollection> class.</span></span> <span data-ttu-id="9cd46-126">Nell'esempio di codice vengono illustrate le seguenti differenze principali tra le due classi.</span><span class="sxs-lookup"><span data-stu-id="9cd46-126">The code example illustrates the following major differences between the two classes.</span></span>  
  
- <span data-ttu-id="9cd46-127">A differenza del metodo <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> della classe <xref:System.Xml.Schema.XmlSchemaCollection>, gli schemi non vengono compilati quando si chiama il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-127">Unlike the <xref:System.Xml.Schema.XmlSchemaCollection.Add%2A> method of the <xref:System.Xml.Schema.XmlSchemaCollection> class, schemas are not compiled when calling the <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> method of the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span> <span data-ttu-id="9cd46-128">Il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet> viene chiamato in modo esplicito nel codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="9cd46-128">The <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> method of the <xref:System.Xml.Schema.XmlSchemaSet> is explicitly called in the example code.</span></span>  
  
- <span data-ttu-id="9cd46-129">Per scorrere un tipo <xref:System.Xml.Schema.XmlSchemaSet>, è necessario usare la proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-129">To iterate over an <xref:System.Xml.Schema.XmlSchemaSet>, you must use the <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> property of the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span>  
  
 <span data-ttu-id="9cd46-130">Di seguito è riportato l'esempio di codice obsoleto del tipo <xref:System.Xml.Schema.XmlSchemaCollection>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-130">The following is the obsolete <xref:System.Xml.Schema.XmlSchemaCollection> code example.</span></span>  
  
```vb  
Dim schemaCollection As XmlSchemaCollection = New XmlSchemaCollection()  
schemaCollection.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd")  
schemaCollection.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
  
Dim schema As XmlSchema  
  
For Each schema in schemaCollection  
  
   Console.WriteLine(schema.TargetNamespace)  
  
Next  
```  
  
```csharp  
XmlSchemaCollection schemaCollection = new XmlSchemaCollection();  
schemaCollection.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd");  
schemaCollection.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
  
foreach(XmlSchema schema in schemaCollection)  
{  
   Console.WriteLine(schema.TargetNamespace);  
}  
```  
  
 <span data-ttu-id="9cd46-131">Di seguito è riportato l'esempio di codice equivalente del tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-131">The following is the equivalent <xref:System.Xml.Schema.XmlSchemaSet> code example.</span></span>  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd")  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
schemaSet.Compile()  
  
Dim schema As XmlSchema  
  
For Each schema in schemaSet.Schemas()  
  
   Console.WriteLine(schema.TargetNamespace)  
  
Next  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd");  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
schemaSet.Compile();  
  
foreach(XmlSchema schema in schemaSet.Schemas())  
{  
   Console.WriteLine(schema.TargetNamespace);  
}  
```  
  
## <a name="adding-and-retrieving-schemas"></a><span data-ttu-id="9cd46-132">Aggiunta e recupero di schemi</span><span class="sxs-lookup"><span data-stu-id="9cd46-132">Adding and Retrieving Schemas</span></span>  
 <span data-ttu-id="9cd46-133">Gli schemi vengono aggiunti a un tipo <xref:System.Xml.Schema.XmlSchemaSet> mediante il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-133">Schemas are added to an <xref:System.Xml.Schema.XmlSchemaSet> using the <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> method of the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span> <span data-ttu-id="9cd46-134">Quando viene aggiunto a un tipo <xref:System.Xml.Schema.XmlSchemaSet>, uno schema viene associato a un URI dello spazio dei nomi di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9cd46-134">When a schema is added to an <xref:System.Xml.Schema.XmlSchemaSet>, it is associated with a target namespace URI.</span></span> <span data-ttu-id="9cd46-135">L'URI dello spazio dei nomi può essere specificato sia come parametro per il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> oppure, se non viene specificato alcuno spazio dei nomi, il tipo <xref:System.Xml.Schema.XmlSchemaSet> usa lo spazio dei nomi definito nello schema.</span><span class="sxs-lookup"><span data-stu-id="9cd46-135">The target namespace URI can either be specified as a parameter to the <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> method or if no target namespace is specified, the <xref:System.Xml.Schema.XmlSchemaSet> uses the target namespace defined in the schema.</span></span>  
  
 <span data-ttu-id="9cd46-136">Gli schemi vengono recuperati da un tipo <xref:System.Xml.Schema.XmlSchemaSet> mediante la proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-136">Schemas are retrieved from an <xref:System.Xml.Schema.XmlSchemaSet> using the <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> property of the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span> <span data-ttu-id="9cd46-137">La proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet> consente di scorrere gli oggetti <xref:System.Xml.Schema.XmlSchema> contenuti nel tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-137">The <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> property of the <xref:System.Xml.Schema.XmlSchemaSet> allows you to iterate over the <xref:System.Xml.Schema.XmlSchema> objects contained in the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span> <span data-ttu-id="9cd46-138">La proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> restituisce tutti gli oggetti <xref:System.Xml.Schema.XmlSchema> contenuti nel tipo <xref:System.Xml.Schema.XmlSchemaSet> oppure, se viene fornito un parametro per lo spazio dei nomi di destinazione, restituisce tutti gli oggetti <xref:System.Xml.Schema.XmlSchema> che appartengono allo spazio dei nomi di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9cd46-138">The <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> property either returns all the <xref:System.Xml.Schema.XmlSchema> objects contained in the <xref:System.Xml.Schema.XmlSchemaSet>, or, given a target namespace parameter, returns all the <xref:System.Xml.Schema.XmlSchema> objects that belong to the target namespace.</span></span> <span data-ttu-id="9cd46-139">Se è specificato `null` come parametro per lo spazio dei nomi di destinazione, la proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> restituisce tutti gli schemi privi di uno spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="9cd46-139">If `null` is specified as the target namespace parameter, the <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> property returns all schemas without a namespace.</span></span>  
  
 <span data-ttu-id="9cd46-140">Nell'esempio seguente viene aggiunto lo schema `books.xsd` dello spazio dei nomi `http://www.contoso.com/books` a un tipo <xref:System.Xml.Schema.XmlSchemaSet>, vengono recuperati tutti gli schemi appartenenti allo spazio dei nomi `http://www.contoso.com/books` dal tipo <xref:System.Xml.Schema.XmlSchemaSet>, quindi vengono scritti tali schemi nel tipo <xref:System.Console>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-140">The following example adds the `books.xsd` schema in the `http://www.contoso.com/books` namespace to an <xref:System.Xml.Schema.XmlSchemaSet>, retrieves all schemas that belong to the `http://www.contoso.com/books` namespace from the <xref:System.Xml.Schema.XmlSchemaSet>, and then writes those schemas to the <xref:System.Console>.</span></span>  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet  
schemaSet.Add("http://www.contoso.com/books", "books.xsd")  
  
Dim schema As XmlSchema  
  
For Each schema In schemaSet.Schemas("http://www.contoso.com/books")  
  
   schema.Write(Console.Out)  
  
Next  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/books", "books.xsd");  
  
foreach (XmlSchema schema in schemaSet.Schemas("http://www.contoso.com/books"))  
{  
   schema.Write(Console.Out);  
}  
```  
  
 <span data-ttu-id="9cd46-141">Per altre informazioni sull'aggiunta e sul recupero di schemi da un oggetto <xref:System.Xml.Schema.XmlSchemaSet>, vedere la documentazione di riferimento per il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> e per la proprietà <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-141">For more information about adding and retrieving schemas from an <xref:System.Xml.Schema.XmlSchemaSet> object, see the <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> method and the <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> property reference documentation.</span></span>  
  
## <a name="compiling-schemas"></a><span data-ttu-id="9cd46-142">Compilazione di schemi</span><span class="sxs-lookup"><span data-stu-id="9cd46-142">Compiling Schemas</span></span>  
 <span data-ttu-id="9cd46-143">Gli schemi di un tipo <xref:System.Xml.Schema.XmlSchemaSet> vengono compilati in un singolo schema logico dal metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-143">Schemas in an <xref:System.Xml.Schema.XmlSchemaSet> are compiled into one logical schema by the <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> method of the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="9cd46-144">A differenza della classe obsoleta <xref:System.Xml.Schema.XmlSchemaCollection>, gli schemi non vengono compilati quando si chiama il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-144">Unlike the obsolete <xref:System.Xml.Schema.XmlSchemaCollection> class, schemas are not compiled when the <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> method is called.</span></span>  
  
 <span data-ttu-id="9cd46-145">Se il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> viene eseguito correttamente, la proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet> viene impostata su `true`.</span><span class="sxs-lookup"><span data-stu-id="9cd46-145">If the <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> method executes successfully, the <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> property of the <xref:System.Xml.Schema.XmlSchemaSet> is set to `true`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="9cd46-146">La proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> non viene influenzata se si apportano modifiche agli schemi contenuti nel tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-146">The <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> property is not affected if schemas are edited while in the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span> <span data-ttu-id="9cd46-147">Non viene tenuta traccia degli aggiornamenti dei singoli schemi del tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-147">Updates of the individual schemas in the <xref:System.Xml.Schema.XmlSchemaSet> are not tracked.</span></span> <span data-ttu-id="9cd46-148">Di conseguenza, la proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> può essere `true` anche se viene modificato uno degli schemi contenuti nel tipo <xref:System.Xml.Schema.XmlSchemaSet>, a condizione che non venga aggiunto o rimosso alcuno schema dal tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-148">As a result, the <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> property can be `true` even though one of the schemas contained in the <xref:System.Xml.Schema.XmlSchemaSet> has been altered, as long as no schemas were added or removed from the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span>  
  
 <span data-ttu-id="9cd46-149">Nell'esempio seguente viene aggiunto il file `books.xsd` al tipo <xref:System.Xml.Schema.XmlSchemaSet>, quindi viene chiamato il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-149">The following example adds the `books.xsd` file to the <xref:System.Xml.Schema.XmlSchemaSet> and then calls the <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> method.</span></span>  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
schemaSet.Add("http://www.contoso.com/books", "books.xsd")  
schemaSet.Compile()  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/books", "books.xsd");  
schemaSet.Compile();  
```  
  
 <span data-ttu-id="9cd46-150">Per altre informazioni sulla compilazione di schemi di un tipo <xref:System.Xml.Schema.XmlSchemaSet>, vedere la documentazione di riferimento per il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-150">For more information about compiling schemas in an <xref:System.Xml.Schema.XmlSchemaSet>, see the <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> method reference documentation.</span></span>  
  
## <a name="reprocessing-schemas"></a><span data-ttu-id="9cd46-151">Rielaborazione di schemi</span><span class="sxs-lookup"><span data-stu-id="9cd46-151">Reprocessing Schemas</span></span>  
 <span data-ttu-id="9cd46-152">Nella rielaborazione di uno schema di un tipo <xref:System.Xml.Schema.XmlSchemaSet> vengono eseguiti tutti i passaggi di pre-elaborazione eseguiti su uno schema quando si chiama il metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-152">Reprocessing a schema in an <xref:System.Xml.Schema.XmlSchemaSet> performs all the preprocessing steps performed on a schema when the <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> method of the <xref:System.Xml.Schema.XmlSchemaSet> is called.</span></span> <span data-ttu-id="9cd46-153">Se la chiamata al metodo <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> viene eseguita correttamente, la proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet> viene impostata su `false`.</span><span class="sxs-lookup"><span data-stu-id="9cd46-153">If the call to the <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> method is successful, the <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> property of the <xref:System.Xml.Schema.XmlSchemaSet> is set to `false`.</span></span>  
  
 <span data-ttu-id="9cd46-154">È necessario usare il metodo <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> quando uno schema del tipo <xref:System.Xml.Schema.XmlSchemaSet> è stato modificato dopo la compilazione del tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-154">The <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> method should be used when a schema in the <xref:System.Xml.Schema.XmlSchemaSet> has been modified after the <xref:System.Xml.Schema.XmlSchemaSet> has performed compilation.</span></span>  
  
 <span data-ttu-id="9cd46-155">Nel seguente esempio viene illustrata la rielaborazione di uno schema aggiunto al tipo <xref:System.Xml.Schema.XmlSchemaSet> mediante il metodo <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-155">The following example illustrates reprocessing a schema added to the <xref:System.Xml.Schema.XmlSchemaSet> using the <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> method.</span></span> <span data-ttu-id="9cd46-156">Dopo aver compilato il tipo <xref:System.Xml.Schema.XmlSchemaSet> usando il metodo <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> e dopo aver modificato lo schema aggiunto al tipo <xref:System.Xml.Schema.XmlSchemaSet>, la proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> viene impostata su `true` benché sia stato modificato uno schema del tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-156">After the <xref:System.Xml.Schema.XmlSchemaSet> is compiled using the <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A> method, and the schema added to the <xref:System.Xml.Schema.XmlSchemaSet> is modified, the <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> property is set to `true` even though a schema in the <xref:System.Xml.Schema.XmlSchemaSet> has been modified.</span></span> <span data-ttu-id="9cd46-157">Se si chiama il metodo <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> verranno eseguiti tutti i passaggi di pre-elaborazione eseguiti dal metodo <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> e la proprietà <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> verrà impostata su `false`.</span><span class="sxs-lookup"><span data-stu-id="9cd46-157">Calling the <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> method performs all the preprocessing performed by the <xref:System.Xml.Schema.XmlSchemaSet.Add%2A> method, and sets the <xref:System.Xml.Schema.XmlSchemaSet.IsCompiled%2A> property to `false`.</span></span>  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
Dim schema As XmlSchema = schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
schemaSet.Compile()  
  
Dim element As XmlSchemaElement = New XmlSchemaElement()  
schema.Items.Add(element)  
element.Name = "book"  
element.SchemaTypeName = New XmlQualifiedName("string", "http://www.w3.org/2001/XMLSchema")  
  
schemaSet.Reprocess(schema)  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
XmlSchema schema = schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
schemaSet.Compile();  
  
XmlSchemaElement element = new XmlSchemaElement();  
schema.Items.Add(element);  
element.Name = "book";  
element.SchemaTypeName = new XmlQualifiedName("string", "http://www.w3.org/2001/XMLSchema");  
  
schemaSet.Reprocess(schema);  
```  
  
 <span data-ttu-id="9cd46-158">Per altre informazioni sulla rielaborazione di uno schema di un tipo <xref:System.Xml.Schema.XmlSchemaSet>, vedere la documentazione di riferimento per il metodo <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-158">For more information about reprocessing a schema in an <xref:System.Xml.Schema.XmlSchemaSet>, see the <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A> method reference documentation.</span></span>  
  
## <a name="checking-for-a-schema"></a><span data-ttu-id="9cd46-159">Verifica di uno schema</span><span class="sxs-lookup"><span data-stu-id="9cd46-159">Checking for a Schema</span></span>  
 <span data-ttu-id="9cd46-160">È possibile usare il metodo <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet> per verificare se uno schema è contenuto in un tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-160">You can use the <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> method of the <xref:System.Xml.Schema.XmlSchemaSet> to check if a schema is contained within an <xref:System.Xml.Schema.XmlSchemaSet>.</span></span> <span data-ttu-id="9cd46-161">Per eseguire la verifica, il metodo <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> accetta uno spazio dei nomi di destinazione oppure un oggetto <xref:System.Xml.Schema.XmlSchema>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-161">The <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> method takes either a target namespace or an <xref:System.Xml.Schema.XmlSchema> object to check for.</span></span> <span data-ttu-id="9cd46-162">In entrambi i casi, il metodo <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> restituisce `true` se lo schema è contenuto in un tipo <xref:System.Xml.Schema.XmlSchemaSet>; in caso contrario, restituisce `false`.</span><span class="sxs-lookup"><span data-stu-id="9cd46-162">In either case, the <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> method returns `true` if the schema is contained within the <xref:System.Xml.Schema.XmlSchemaSet>; otherwise, it returns `false`.</span></span>  
  
 <span data-ttu-id="9cd46-163">Per altre informazioni sulla verifica di uno schema, vedere la documentazione di riferimento per il metodo <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-163">For more information about checking for a schema, see the <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A> method reference documentation.</span></span>  
  
## <a name="removing-schemas"></a><span data-ttu-id="9cd46-164">Rimozione di schemi</span><span class="sxs-lookup"><span data-stu-id="9cd46-164">Removing Schemas</span></span>  
 <span data-ttu-id="9cd46-165">Gli schemi vengono rimossi da un tipo <xref:System.Xml.Schema.XmlSchemaSet> usando i metodi <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> e <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> del tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-165">Schemas are removed from an <xref:System.Xml.Schema.XmlSchemaSet> using the <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> and <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> methods of the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span> <span data-ttu-id="9cd46-166">Il metodo <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> consente di rimuovere dal tipo <xref:System.Xml.Schema.XmlSchemaSet> lo schema specificato, mentre il metodo <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> consente di rimuovere dal tipo <xref:System.Xml.Schema.XmlSchemaSet> lo schema specificato e tutti gli schemi da esso importati.</span><span class="sxs-lookup"><span data-stu-id="9cd46-166">The <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> method removes the specified schema from the <xref:System.Xml.Schema.XmlSchemaSet>, while the <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> method removes the specified schema and all the schemas it imports from the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span>  
  
 <span data-ttu-id="9cd46-167">Nell'esempio seguente viene illustrata l'aggiunta di schemi a un tipo <xref:System.Xml.Schema.XmlSchemaSet> e l'uso del metodo <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> per rimuovere uno degli schemi e tutti gli schemi da esso importati.</span><span class="sxs-lookup"><span data-stu-id="9cd46-167">The following example illustrates adding multiple schemas to an <xref:System.Xml.Schema.XmlSchemaSet>, then using the <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> method to remove one of the schemas and all the schemas it imports.</span></span>  
  
```vb  
Dim schemaSet As XmlSchemaSet = New XmlSchemaSet()  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd")  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd")  
schemaSet.Add("http://www.contoso.com/music", "http://www.contoso.com/music.xsd")  
  
Dim schema As XmlSchema  
  
For Each schema In schemaSet.Schemas()  
  
   If schema.TargetNamespace = "http://www.contoso.com/music" Then  
      schemaSet.RemoveRecursive(schema)  
   End If  
  
Next  
```  
  
```csharp  
XmlSchemaSet schemaSet = new XmlSchemaSet();  
schemaSet.Add("http://www.contoso.com/retail", "http://www.contoso.com/retail.xsd");  
schemaSet.Add("http://www.contoso.com/books", "http://www.contoso.com/books.xsd");  
schemaSet.Add("http://www.contoso.com/music", "http://www.contoso.com/music.xsd");  
  
foreach (XmlSchema schema in schemaSet.Schemas())  
{  
   if (schema.TargetNamespace == "http://www.contoso.com/music")  
   {  
      schemaSet.RemoveRecursive(schema);  
   }  
}  
```  
  
 <span data-ttu-id="9cd46-168">Per altre informazioni sulla rimozione di schemi da un tipo <xref:System.Xml.Schema.XmlSchemaSet>, vedere la documentazione di riferimento per i metodi <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> e <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-168">For more information about removing schemas from an <xref:System.Xml.Schema.XmlSchemaSet>, see the <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A> and <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A> methods reference documentation.</span></span>  
  
## <a name="schema-resolution-and-xsimport"></a><span data-ttu-id="9cd46-169">Risoluzione di schemi e xs:import</span><span class="sxs-lookup"><span data-stu-id="9cd46-169">Schema Resolution and xs:import</span></span>  
 <span data-ttu-id="9cd46-170">Nei seguenti esempi viene descritto il comportamento del tipo <xref:System.Xml.Schema.XmlSchemaSet> per l'importazione di schemi quando sono presenti più schemi per un determinato spazio dei nomi in <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-170">The following examples describe the <xref:System.Xml.Schema.XmlSchemaSet> behavior for importing schemas when multiple schemas for a given namespace exist in an <xref:System.Xml.Schema.XmlSchemaSet>.</span></span>  
  
 <span data-ttu-id="9cd46-171">Ad esempio, si consideri un tipo <xref:System.Xml.Schema.XmlSchemaSet> che contenga più schemi per lo spazio dei nomi `http://www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="9cd46-171">For example, consider an <xref:System.Xml.Schema.XmlSchemaSet> that contains multiple schemas for the `http://www.contoso.com` namespace.</span></span> <span data-ttu-id="9cd46-172">Verrà aggiunto al tipo `xs:import` uno schema con la seguente direttiva <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-172">A schema with the following `xs:import` directive is added to the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span>  
  
```xml  
<xs:import namespace="http://www.contoso.com" schemaLocation="http://www.contoso.com/schema.xsd" />  
```  
  
 <span data-ttu-id="9cd46-173">Il tipo <xref:System.Xml.Schema.XmlSchemaSet> tenterà di importare uno schema per lo spazio dei nomi `http://www.contoso.com` caricandolo dall'URL `http://www.contoso.com/schema.xsd`.</span><span class="sxs-lookup"><span data-stu-id="9cd46-173">The <xref:System.Xml.Schema.XmlSchemaSet> attempts to import a schema for the `http://www.contoso.com` namespace by loading it from the `http://www.contoso.com/schema.xsd` URL.</span></span> <span data-ttu-id="9cd46-174">Nello schema di importazione sono disponibili solo la dichiarazione dello schema e i tipi dichiarati nel documento dello schema, anche se sono presenti altri documenti dello schema per lo spazio dei nomi `http://www.contoso.com` nel tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-174">Only the schema declaration and types declared in the schema document are available in the importing schema, even though there are other schema documents for the `http://www.contoso.com` namespace in the <xref:System.Xml.Schema.XmlSchemaSet>.</span></span> <span data-ttu-id="9cd46-175">Se non è possibile individuare il file `schema.xsd` nell'URL `http://www.contoso.com/schema.xsd`, non verrà importato alcuno schema per lo spazio dei nomi `http://www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="9cd46-175">If the `schema.xsd` file cannot be located at the `http://www.contoso.com/schema.xsd` URL, no schema for the `http://www.contoso.com` namespace is imported into the importing schema.</span></span>  
  
## <a name="validating-xml-documents"></a><span data-ttu-id="9cd46-176">Convalida di documenti XML</span><span class="sxs-lookup"><span data-stu-id="9cd46-176">Validating XML Documents</span></span>  
 <span data-ttu-id="9cd46-177">I documenti XML possono essere convalidati in base agli schemi di un tipo <xref:System.Xml.Schema.XmlSchemaSet>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-177">XML documents can be validated against schemas in an <xref:System.Xml.Schema.XmlSchemaSet>.</span></span> <span data-ttu-id="9cd46-178">Per eseguire la convalida di un documento XML, è necessario aggiungere uno schema alla proprietà <xref:System.Xml.Schema.XmlSchemaSet> di un oggetto <xref:System.Xml.XmlReaderSettings.Schemas%2A> del tipo <xref:System.Xml.XmlReaderSettings> oppure aggiungere un tipo <xref:System.Xml.Schema.XmlSchemaSet> alla proprietà <xref:System.Xml.XmlReaderSettings.Schemas%2A> di un oggetto <xref:System.Xml.XmlReaderSettings>.</span><span class="sxs-lookup"><span data-stu-id="9cd46-178">You validate an XML document by adding a schema to the <xref:System.Xml.Schema.XmlSchemaSet><xref:System.Xml.XmlReaderSettings.Schemas%2A> property of an <xref:System.Xml.XmlReaderSettings> object, or by adding an <xref:System.Xml.Schema.XmlSchemaSet> to the <xref:System.Xml.XmlReaderSettings.Schemas%2A> property of an <xref:System.Xml.XmlReaderSettings> object.</span></span> <span data-ttu-id="9cd46-179">Quindi l'oggetto <xref:System.Xml.XmlReaderSettings> verrà usato dal metodo <xref:System.Xml.XmlReader.Create%2A> della classe <xref:System.Xml.XmlReader> per creare un oggetto <xref:System.Xml.XmlReader> e convalidare il documento XML.</span><span class="sxs-lookup"><span data-stu-id="9cd46-179">The <xref:System.Xml.XmlReaderSettings> object is then used by the <xref:System.Xml.XmlReader.Create%2A> method of the <xref:System.Xml.XmlReader> class to create an <xref:System.Xml.XmlReader> object and validate the XML document.</span></span>  
  
 <span data-ttu-id="9cd46-180">Per altre informazioni sulla convalida di documenti XML tramite <xref:System.Xml.Schema.XmlSchemaSet>, vedere [Convalida di XML Schema (XSD) con XmlSchemaSet](xml-schema-xsd-validation-with-xmlschemaset.md).</span><span class="sxs-lookup"><span data-stu-id="9cd46-180">For more information about validating XML documents using an <xref:System.Xml.Schema.XmlSchemaSet>, see [XML Schema (XSD) Validation with XmlSchemaSet](xml-schema-xsd-validation-with-xmlschemaset.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9cd46-181">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9cd46-181">See also</span></span>

- <xref:System.Xml.Schema.XmlSchemaSet.Add%2A>
- <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A>
- <xref:System.Xml.Schema.XmlSchemaSet.Contains%2A>
- <xref:System.Xml.Schema.XmlSchemaSet.Compile%2A>
- <xref:System.Xml.Schema.XmlSchemaSet.Reprocess%2A>
- <xref:System.Xml.Schema.XmlSchemaSet.Remove%2A>
- <xref:System.Xml.Schema.XmlSchemaSet.RemoveRecursive%2A>
- [<span data-ttu-id="9cd46-182">XmlSchemaSet come cache degli schemi</span><span class="sxs-lookup"><span data-stu-id="9cd46-182">XmlSchemaSet as a Schema Cache</span></span>](xmlschemaset-for-schema-compilation.md)
- [<span data-ttu-id="9cd46-183">Convalida di XML Schema (XSD) con XmlSchemaSet</span><span class="sxs-lookup"><span data-stu-id="9cd46-183">XML Schema (XSD) Validation with XmlSchemaSet</span></span>](xml-schema-xsd-validation-with-xmlschemaset.md)

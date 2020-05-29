---
title: Accesso a dati XML fortemente tipizzati con XPathNavigator
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 898e0f52-8a7c-4d1f-afcd-6ffb28b050b4
ms.openlocfilehash: afbfd516ef25eff94a9eed841f313892007c58a1
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202344"
---
# <a name="accessing-strongly-typed-xml-data-using-xpathnavigator"></a><span data-ttu-id="fa716-102">Accesso a dati XML fortemente tipizzati con XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="fa716-102">Accessing Strongly Typed XML Data Using XPathNavigator</span></span>
<span data-ttu-id="fa716-103">Come istanza del modello di dati XPath 2,0, la <xref:System.Xml.XPath.XPathNavigator> classe può contenere dati fortemente tipizzati che vengono mappati ai tipi Common Language Runtime (CLR).</span><span class="sxs-lookup"><span data-stu-id="fa716-103">As an instance of the XPath 2.0 data model, the <xref:System.Xml.XPath.XPathNavigator> class can contain strongly typed data that maps to common language runtime (CLR) types.</span></span> <span data-ttu-id="fa716-104">In base al modello di dati XPath 2,0, solo gli elementi e gli attributi possono contenere dati fortemente tipizzati.</span><span class="sxs-lookup"><span data-stu-id="fa716-104">According to the XPath 2.0 data model, only elements and attributes can contain strongly typed data.</span></span> <span data-ttu-id="fa716-105">La <xref:System.Xml.XPath.XPathNavigator> classe fornisce i meccanismi per accedere ai dati all'interno di un <xref:System.Xml.XPath.XPathDocument> <xref:System.Xml.XmlDocument> oggetto o come dati fortemente tipizzati, nonché meccanismi per la conversione da un tipo di dati a un altro.</span><span class="sxs-lookup"><span data-stu-id="fa716-105">The <xref:System.Xml.XPath.XPathNavigator> class provides mechanisms for accessing data within an <xref:System.Xml.XPath.XPathDocument> or <xref:System.Xml.XmlDocument> object as strongly typed data as well as mechanisms for converting from one data type to another.</span></span>  
  
## <a name="type-information-exposed-by-xpathnavigator"></a><span data-ttu-id="fa716-106">Informazioni sul tipo esposte da XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="fa716-106">Type Information Exposed by XPathNavigator</span></span>  
 <span data-ttu-id="fa716-107">Tecnicamente, i dati XML versione 1.0 non dispongono di tipi, a meno che non vengano elaborati tramite una DTD, uno schema XSD (XML Schema Definition Language) o un altro meccanismo.</span><span class="sxs-lookup"><span data-stu-id="fa716-107">XML 1.0 data is technically without type, unless processed with a DTD, XML schema definition language (XSD) schema, or other mechanism.</span></span> <span data-ttu-id="fa716-108">Esistono diverse categorie di informazioni sul tipo che possono essere associate con un elemento o attributo XML.</span><span class="sxs-lookup"><span data-stu-id="fa716-108">There are a number of categories of type information that can be associated with an XML element or attribute.</span></span>  
  
- <span data-ttu-id="fa716-109">Tipi CLR semplici: nessun linguaggio XML Schema supporta i tipi CLR in modo diretto.</span><span class="sxs-lookup"><span data-stu-id="fa716-109">Simple CLR Types: None of the XML Schema languages support Common Language Runtime (CLR) types directly.</span></span> <span data-ttu-id="fa716-110">Dal momento che risulta utile poter visualizzare il contenuto semplice di elementi e attributi come tipo CLR più appropriato, è possibile tipizzare l'intero contenuto semplice come tipo <xref:System.String> in assenza di informazioni sullo schema e di eventuali informazioni aggiunte che possano ottimizzare tale contenuto rendendolo un tipo più appropriato.</span><span class="sxs-lookup"><span data-stu-id="fa716-110">Because it is useful to be able to view simple element and attribute content as the most appropriate CLR type, all simple content can be typed as <xref:System.String> in the absence of schema information with any added schema information potentially refining this content to a more appropriate type.</span></span> <span data-ttu-id="fa716-111">Per individuare il tipo CLR che corrisponde maggiormente al contenuto semplice dell'elemento o attributo, usare la proprietà <xref:System.Xml.XPath.XPathNavigator.ValueType%2A>.</span><span class="sxs-lookup"><span data-stu-id="fa716-111">You can find the best matching CLR type of simple element and attribute content by using the <xref:System.Xml.XPath.XPathNavigator.ValueType%2A> property.</span></span> <span data-ttu-id="fa716-112">Per altre informazioni sul mapping dai tipi incorporati nello schema a tipi CLR, vedere [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).</span><span class="sxs-lookup"><span data-stu-id="fa716-112">For more information about the mapping from schema built-in types to CLR types, see [Type Support in the System.Xml Classes](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).</span></span>  
  
- <span data-ttu-id="fa716-113">Elenchi di tipi semplici (CLR): un elemento o attributo con contenuto semplice può contenere un elenco di valori separati da spazi vuoti.</span><span class="sxs-lookup"><span data-stu-id="fa716-113">Lists of Simple (CLR) Types: An element or attribute with simple content can contain a list of values separated by white space.</span></span> <span data-ttu-id="fa716-114">I valori sono specificati da un XML Schema come "dati di tipo list".</span><span class="sxs-lookup"><span data-stu-id="fa716-114">The values are specified by an XML Schema to be a "list type."</span></span> <span data-ttu-id="fa716-115">In assenza di un XML Schema, questo contenuto semplice verrebbe considerato come un solo nodo di tipo text.</span><span class="sxs-lookup"><span data-stu-id="fa716-115">In the absence of an XML Schema, such simple content would be treated as a single text node.</span></span> <span data-ttu-id="fa716-116">Se invece è disponibile un XML Schema, questo contenuto semplice può essere esposto come una serie di valori specifici, ognuno dei quali dispone di un tipo semplice associato a una raccolta di oggetti CLR.</span><span class="sxs-lookup"><span data-stu-id="fa716-116">When an XML Schema is available, this simple content can be exposed as a series of atomic values each having a simple type that maps to a collection of CLR objects.</span></span> <span data-ttu-id="fa716-117">Per altre informazioni sul mapping dai tipi incorporati nello schema a tipi CLR, vedere [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).</span><span class="sxs-lookup"><span data-stu-id="fa716-117">For more information about the mapping from schema built-in types to CLR types, see [Type Support in the System.Xml Classes](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).</span></span>  
  
- <span data-ttu-id="fa716-118">Valore tipizzato: un attributo o un elemento con un tipo semplice convalidato in base a uno schema presenta un valore tipizzato.</span><span class="sxs-lookup"><span data-stu-id="fa716-118">Typed Value: A schema-validated attribute or element with a simple type has a typed value.</span></span> <span data-ttu-id="fa716-119">Questo valore è un tipo primitivo, ad esempio un tipo di dati numerico, di stringa o relativo alla data.</span><span class="sxs-lookup"><span data-stu-id="fa716-119">This value is a primitive type such as a numeric, string, or date type.</span></span> <span data-ttu-id="fa716-120">È possibile eseguire il mapping di tutti i tipi semplici incorporati in XSD a tipi CLR che consentono l'accesso al valore di un nodo come un tipo più appropriato anziché come un tipo <xref:System.String>.</span><span class="sxs-lookup"><span data-stu-id="fa716-120">All the built-in simple types in XSD can be mapped to CLR types that provide access to the value of a node as a more appropriate type instead of just as a <xref:System.String>.</span></span> <span data-ttu-id="fa716-121">Un elemento che presenta attributi o elementi figlio è considerato un tipo complesso.</span><span class="sxs-lookup"><span data-stu-id="fa716-121">An element with attributes or element children is considered to be a complex type.</span></span> <span data-ttu-id="fa716-122">Il valore tipizzato di un tipo complesso che presenta contenuto semplice, ovvero solo nodi di tipo text come nodi figlio, è uguale a quello del tipo semplice del relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="fa716-122">The typed value of a complex type with simple content (only text nodes as children) is the same as that of the simple type of its content.</span></span> <span data-ttu-id="fa716-123">Il valore tipizzato di un tipo complesso che presenta contenuto complesso, ovvero più di un elemento figlio, è il valore di stringa della concatenazione di tutti i nodi figlio di tipo text restituiti come tipo <xref:System.String>.</span><span class="sxs-lookup"><span data-stu-id="fa716-123">The typed value of a complex type with complex content (one or more child elements) is the string value of the concatenation of all its child text nodes returned as a <xref:System.String>.</span></span> <span data-ttu-id="fa716-124">Per altre informazioni sul mapping dai tipi incorporati nello schema a tipi CLR, vedere [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).</span><span class="sxs-lookup"><span data-stu-id="fa716-124">For more information about the mapping from schema built-in types to CLR types, see [Type Support in the System.Xml Classes](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).</span></span>  
  
- <span data-ttu-id="fa716-125">Nome del tipo specifico per il linguaggio di schema: nella maggior parte dei casi, i tipi CLR, impostati come effetto collaterale dell'applicazione di uno schema esterno, vengono usati per consentire l'accesso al valore di un nodo.</span><span class="sxs-lookup"><span data-stu-id="fa716-125">Schema-Language Specific Type Name: In most cases, the CLR types, which are set as a side-effect of applying an external schema, are used to provide access to the value of a node.</span></span> <span data-ttu-id="fa716-126">Tuttavia, in alcune situazioni è possibile che si desideri esaminare il tipo associato a uno schema particolare applicato a un documento XML.</span><span class="sxs-lookup"><span data-stu-id="fa716-126">However, there may be situations where you may want to examine the type associated with a particular schema applied to an XML document.</span></span> <span data-ttu-id="fa716-127">Ad esempio, è possibile che si desideri eseguire una ricerca nel documento XML ed estrarre tutti gli elementi per i quali è stato determinato un contenuto di tipo "PurchaseOrder" in base a uno schema associato.</span><span class="sxs-lookup"><span data-stu-id="fa716-127">For example, you may wish to search through an XML document, extracting all elements that are determined to have content of type "PurchaseOrder" according to an attached schema.</span></span> <span data-ttu-id="fa716-128">Queste informazioni sul tipo possono essere impostate solo in seguito alla convalida dello schema ed è possibile accedervi tramite le proprietà <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> e <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.</span><span class="sxs-lookup"><span data-stu-id="fa716-128">Such type information can be set only as a result of schema validation and this information is accessed through the <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> and <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> properties of the <xref:System.Xml.XPath.XPathNavigator> class.</span></span> <span data-ttu-id="fa716-129">Per altre informazioni, vedere di seguito la sezione relativa all'infoset sulla convalida post-schema.</span><span class="sxs-lookup"><span data-stu-id="fa716-129">For more information, see The Post Schema Validation Infoset (PSVI) section below.</span></span>  
  
- <span data-ttu-id="fa716-130">Reflection sul tipo specifico per il linguaggio di schema: in altri casi, è possibile che si desideri ottenere ulteriori informazioni sul tipo specifico per lo schema applicato a un documento XML.</span><span class="sxs-lookup"><span data-stu-id="fa716-130">Schema-Language Specific Type Reflection: In other cases, you may want to obtain further details of the schema-specific type applied to an XML document.</span></span> <span data-ttu-id="fa716-131">Ad esempio, durante la lettura di un file XML, è possibile che si desideri estrarre l'attributo `maxOccurs` per ciascun nodo valido nel documento XML per eseguire calcoli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="fa716-131">For example, when reading an XML file, you may want to extract the `maxOccurs` attribute for each valid node in the XML document in order to perform some custom calculation.</span></span> <span data-ttu-id="fa716-132">Dal momento che queste informazioni vengono impostate solo in seguito alla convalida dello schema, è possibile accedervi tramite la proprietà <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.</span><span class="sxs-lookup"><span data-stu-id="fa716-132">Because this information is set only through schema validation, it is accessed through the <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> property of the <xref:System.Xml.XPath.XPathNavigator> class.</span></span> <span data-ttu-id="fa716-133">Per altre informazioni, vedere di seguito la sezione relativa all'infoset sulla convalida post-schema.</span><span class="sxs-lookup"><span data-stu-id="fa716-133">For more information, see The Post Schema Validation Infoset (PSVI) section below.</span></span>  
  
## <a name="xpathnavigator-typed-accessors"></a><span data-ttu-id="fa716-134">Funzioni di accesso tipizzate di XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="fa716-134">XPathNavigator Typed Accessors</span></span>  
 <span data-ttu-id="fa716-135">Nella tabella seguente vengono illustrate le diverse proprietà e i diversi metodi della classe <xref:System.Xml.XPath.XPathNavigator> che possono essere usati per accedere alle informazioni sul tipo di un nodo.</span><span class="sxs-lookup"><span data-stu-id="fa716-135">The following table shows the various properties and methods of the <xref:System.Xml.XPath.XPathNavigator> class that can be used to access the type information about a node.</span></span>  
  
|<span data-ttu-id="fa716-136">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fa716-136">Property</span></span>|<span data-ttu-id="fa716-137">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fa716-137">Description</span></span>|  
|--------------|-----------------|  
|<xref:System.Xml.XPath.XPathNavigator.XmlType%2A>|<span data-ttu-id="fa716-138">Contiene le informazioni sul tipo di schema XML per il nodo se questo è valido.</span><span class="sxs-lookup"><span data-stu-id="fa716-138">This contains the XML schema type information for the node if it is valid.</span></span>|  
|<xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A>|<span data-ttu-id="fa716-139">Contiene l'infoset sulla convalida post-schema del nodo aggiunte dopo la convalida.</span><span class="sxs-lookup"><span data-stu-id="fa716-139">This contains the Post Schema Validation Infoset of the node that is added after validation.</span></span> <span data-ttu-id="fa716-140">Sono incluse le informazioni sul tipo di schema XML e le informazioni sulla validità.</span><span class="sxs-lookup"><span data-stu-id="fa716-140">This includes the XML schema type information, as well as validity information.</span></span>|  
|<xref:System.Xml.XPath.XPathNavigator.ValueType%2A>|<span data-ttu-id="fa716-141">Il tipo CLR del valore tipizzato del nodo.</span><span class="sxs-lookup"><span data-stu-id="fa716-141">The CLR type of the typed value of the node.</span></span>|  
|<xref:System.Xml.XPath.XPathNavigator.TypedValue%2A>|<span data-ttu-id="fa716-142">Il contenuto del nodo come uno o più valori CLR il cui tipo corrisponde maggiormente al tipo di schema XML del nodo.</span><span class="sxs-lookup"><span data-stu-id="fa716-142">The content of the node as one or more CLR values whose type is the closest match to the XML schema type of the node.</span></span>|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsBoolean%2A>|<span data-ttu-id="fa716-143">Il valore <xref:System.String> del nodo corrente di cui viene eseguito il cast in un valore <xref:System.Boolean>, in base alle regole di XPath versione 2.0 per l'esecuzione del cast in `xs:boolean`.</span><span class="sxs-lookup"><span data-stu-id="fa716-143">The <xref:System.String> value of the current node cast to a <xref:System.Boolean> value, according to the XPath 2.0 casting rules for `xs:boolean`.</span></span>|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsDateTime%2A>|<span data-ttu-id="fa716-144">Il valore <xref:System.String> del nodo corrente di cui viene eseguito il cast in un valore <xref:System.DateTime>, in base alle regole di XPath versione 2.0 per l'esecuzione del cast in `xs:datetime`.</span><span class="sxs-lookup"><span data-stu-id="fa716-144">The <xref:System.String> value of the current node cast to a <xref:System.DateTime> value, according to the XPath 2.0 casting rules for `xs:datetime`.</span></span>|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsDouble%2A>|<span data-ttu-id="fa716-145">Il valore <xref:System.String> del nodo corrente di cui viene eseguito il cast in un valore <xref:System.Double>, in base alle regole di XPath versione 2.0 per l'esecuzione del cast in `xsd:double`.</span><span class="sxs-lookup"><span data-stu-id="fa716-145">The <xref:System.String> value of the current node cast to a <xref:System.Double> value, according to the XPath 2.0 casting rules for `xsd:double`.</span></span>|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsInt%2A>|<span data-ttu-id="fa716-146">Il valore <xref:System.String> del nodo corrente di cui viene eseguito il cast in un valore <xref:System.Int32>, in base alle regole di XPath versione 2.0 per l'esecuzione del cast in `xs:integer`.</span><span class="sxs-lookup"><span data-stu-id="fa716-146">The <xref:System.String> value of the current node cast to a <xref:System.Int32> value, according to the XPath 2.0 casting rules for `xs:integer`.</span></span>|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAsLong%2A>|<span data-ttu-id="fa716-147">Il valore <xref:System.String> del nodo corrente di cui viene eseguito il cast in un valore <xref:System.Int64>, in base alle regole di XPath versione 2.0 per l'esecuzione del cast in `xs:integer`.</span><span class="sxs-lookup"><span data-stu-id="fa716-147">The <xref:System.String> value of the current node cast to a <xref:System.Int64> value, according to the XPath 2.0 casting rules for `xs:integer`.</span></span>|  
|<xref:System.Xml.XPath.XPathNavigator.ValueAs%2A>|<span data-ttu-id="fa716-148">Il contenuto del nodo di cui viene eseguito il cast nel tipo di destinazione in base alle regole di XPath 2.0 per l'esecuzione del cast.</span><span class="sxs-lookup"><span data-stu-id="fa716-148">The contents of the node cast to the target type according to the XPath 2.0 casting rules.</span></span>|  
  
 <span data-ttu-id="fa716-149">Per altre informazioni sul mapping dai tipi incorporati nello schema a tipi CLR, vedere [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).</span><span class="sxs-lookup"><span data-stu-id="fa716-149">For more information about the mapping from schema built-in types to CLR types, see [Type Support in the System.Xml Classes](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).</span></span>  
  
## <a name="the-post-schema-validation-infoset-psvi"></a><span data-ttu-id="fa716-150">Infoset sulla convalida post-schema (PSVI, Post Schema Validation Infoset)</span><span class="sxs-lookup"><span data-stu-id="fa716-150">The Post Schema Validation Infoset (PSVI)</span></span>  
 <span data-ttu-id="fa716-151">In un processore di XML Schema, un infoset XML viene accettato come input e viene convertito in un infoset sulla convalida post-schema.</span><span class="sxs-lookup"><span data-stu-id="fa716-151">An XML Schema processor accepts an XML Infoset as input and converts it into a Post Schema Validation Infoset (PSVI).</span></span> <span data-ttu-id="fa716-152">Un PSVI rappresenta l'infoset XML di input originale con nuovi elementi informazioni e nuove proprietà aggiunti agli elementi informazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="fa716-152">A PSVI is the original input XML infoset with new information items added and new properties added to existing information items.</span></span> <span data-ttu-id="fa716-153">Le informazioni aggiunte all'infoset XML nel PVSI possono essere suddivise in tre grandi classi che vengono esposte dal tipo <xref:System.Xml.XPath.XPathNavigator>.</span><span class="sxs-lookup"><span data-stu-id="fa716-153">There are three broad classes of information added to the XML Infoset in the PSVI that are exposed by the <xref:System.Xml.XPath.XPathNavigator>.</span></span>  
  
1. <span data-ttu-id="fa716-154">Risultati della convalida: informazioni relative all'esito della convalida di un elemento o di un attributo.</span><span class="sxs-lookup"><span data-stu-id="fa716-154">Validation Outcomes: Information as to whether an element or attribute was successfully validated or not.</span></span> <span data-ttu-id="fa716-155">Tali informazioni vengono esposte dalla proprietà <xref:System.Xml.Schema.IXmlSchemaInfo.Validity%2A> della proprietà <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.</span><span class="sxs-lookup"><span data-stu-id="fa716-155">This is exposed by the <xref:System.Xml.Schema.IXmlSchemaInfo.Validity%2A> property of the <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> property of the <xref:System.Xml.XPath.XPathNavigator> class.</span></span>  
  
2. <span data-ttu-id="fa716-156">Informazioni predefinite: viene indicato se il valore dell'elemento o dell'attributo sia stato ottenuto o meno mediante i valori predefiniti specificati nello schema.</span><span class="sxs-lookup"><span data-stu-id="fa716-156">Default Information: Indications as to whether the value of the element or attribute was obtained via default values specified in the schema or not.</span></span> <span data-ttu-id="fa716-157">Tali informazioni vengono esposte dalla proprietà <xref:System.Xml.Schema.IXmlSchemaInfo.IsDefault%2A> della proprietà <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.</span><span class="sxs-lookup"><span data-stu-id="fa716-157">This is exposed by the <xref:System.Xml.Schema.IXmlSchemaInfo.IsDefault%2A> property of the <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> property of the <xref:System.Xml.XPath.XPathNavigator> class.</span></span>  
  
3. <span data-ttu-id="fa716-158">Annotazioni di tipi: riferimenti a componenti dello schema che potrebbero essere definizioni di tipi o dichiarazioni di attributo o elemento.</span><span class="sxs-lookup"><span data-stu-id="fa716-158">Type Annotations: References to schema components that may be type definitions or element and attribute declarations.</span></span> <span data-ttu-id="fa716-159">La proprietà <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> del tipo <xref:System.Xml.XPath.XPathNavigator> contiene le informazioni sul tipo specifiche del nodo se questo è valido.</span><span class="sxs-lookup"><span data-stu-id="fa716-159">The <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> property of the <xref:System.Xml.XPath.XPathNavigator> contains the specific type information of the node if it is valid.</span></span> <span data-ttu-id="fa716-160">Se la validità di un nodo è sconosciuta, ad esempio nel caso in cui il nodo sia stato convalidato e modificato successivamente,</span><span class="sxs-lookup"><span data-stu-id="fa716-160">If the validity of a node is unknown, such as when it was validated then subsequently edited.</span></span> <span data-ttu-id="fa716-161">la proprietà <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> sarà impostata su `null` ma le informazioni sul tipo saranno ancora disponibili mediante diverse proprietà della proprietà <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> della classe <xref:System.Xml.XPath.XPathNavigator>.</span><span class="sxs-lookup"><span data-stu-id="fa716-161">then the <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> property is set to `null` but type information is still available from the various properties of the <xref:System.Xml.XPath.XPathNavigator.SchemaInfo%2A> property of the <xref:System.Xml.XPath.XPathNavigator> class.</span></span>  
  
 <span data-ttu-id="fa716-162">Nell'esempio seguente viene illustrato l'uso delle informazioni nell'infoset sulla convalida post-schema esposto dal tipo <xref:System.Xml.XPath.XPathNavigator>.</span><span class="sxs-lookup"><span data-stu-id="fa716-162">The following example illustrates using information in the Post Schema Validation Infoset exposed by the <xref:System.Xml.XPath.XPathNavigator>.</span></span>  
  
```vb  
Dim settings As XmlReaderSettings = New XmlReaderSettings()  
settings.Schemas.Add("http://www.contoso.com/books", "books.xsd")  
settings.ValidationType = ValidationType.Schema  
  
Dim reader As XmlReader = XmlReader.Create("books.xml", settings)  
  
Dim document As XmlDocument = New XmlDocument()  
document.Load(reader)  
Dim navigator As XPathNavigator = document.CreateNavigator()  
navigator.MoveToChild("books", "http://www.contoso.com/books")  
navigator.MoveToChild("book", "http://www.contoso.com/books")  
navigator.MoveToChild("published", "http://www.contoso.com/books")  
  
Console.WriteLine(navigator.SchemaInfo.SchemaType.Name)  
Console.WriteLine(navigator.SchemaInfo.Validity)  
Console.WriteLine(navigator.SchemaInfo.SchemaElement.MinOccurs)  
```  
  
```csharp  
XmlReaderSettings settings = new XmlReaderSettings();  
settings.Schemas.Add("http://www.contoso.com/books", "books.xsd");  
settings.ValidationType = ValidationType.Schema;  
  
XmlReader reader = XmlReader.Create("books.xml", settings);  
  
XmlDocument document = new XmlDocument();  
document.Load(reader);  
XPathNavigator navigator = document.CreateNavigator();  
navigator.MoveToChild("books", "http://www.contoso.com/books");  
navigator.MoveToChild("book", "http://www.contoso.com/books");  
navigator.MoveToChild("published", "http://www.contoso.com/books");  
  
Console.WriteLine(navigator.SchemaInfo.SchemaType.Name);  
Console.WriteLine(navigator.SchemaInfo.Validity);  
Console.WriteLine(navigator.SchemaInfo.SchemaElement.MinOccurs);  
```  
  
 <span data-ttu-id="fa716-163">Nell'esempio il file `books.xml` viene considerato come input.</span><span class="sxs-lookup"><span data-stu-id="fa716-163">The example takes the `books.xml` file as input.</span></span>  
  
```xml  
<books xmlns="http://www.contoso.com/books">  
    <book>  
        <title>Title</title>  
        <price>10.00</price>  
        <published>2003-12-31</published>  
    </book>  
</books>  
```  
  
 <span data-ttu-id="fa716-164">Anche lo schema `books.xsd` viene considerato come input.</span><span class="sxs-lookup"><span data-stu-id="fa716-164">The example also takes the `books.xsd` schema as input.</span></span>  
  
```xml  
<xs:schema xmlns="http://www.contoso.com/books"
attributeFormDefault="unqualified" elementFormDefault="qualified"
targetNamespace="http://www.contoso.com/books"
xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <xs:simpleType name="publishedType">  
        <xs:restriction base="xs:date">  
            <xs:minInclusive value="2003-01-01" />  
            <xs:maxInclusive value="2003-12-31" />  
        </xs:restriction>  
    </xs:simpleType>  
    <xs:complexType name="bookType">  
        <xs:sequence>  
            <xs:element name="title" type="xs:string"/>  
            <xs:element name="price" type="xs:decimal"/>  
            <xs:element name="published" type="publishedType"/>  
        </xs:sequence>  
    </xs:complexType>  
    <xs:complexType name="booksType">  
        <xs:sequence>  
            <xs:element name="book" type="bookType" />  
        </xs:sequence>  
    </xs:complexType>  
    <xs:element name="books" type="booksType" />  
</xs:schema>  
```  
  
## <a name="obtain-typed-values-using-valueas-properties"></a><span data-ttu-id="fa716-165">Recupero di valori tipizzati mediante le proprietà ValueAs</span><span class="sxs-lookup"><span data-stu-id="fa716-165">Obtain Typed Values Using ValueAs Properties</span></span>  
 <span data-ttu-id="fa716-166">Il valore tipizzato di un nodo può essere recuperato accedendo alla proprietà <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> del tipo <xref:System.Xml.XPath.XPathNavigator>.</span><span class="sxs-lookup"><span data-stu-id="fa716-166">The typed value of a node can be retrieved by accessing the <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> property of the <xref:System.Xml.XPath.XPathNavigator>.</span></span> <span data-ttu-id="fa716-167">In alcuni casi, è possibile che si desideri convertire il valore tipizzato di un nodo in un tipo diverso.</span><span class="sxs-lookup"><span data-stu-id="fa716-167">In certain cases you may want to convert the typed value of a node to a different type.</span></span> <span data-ttu-id="fa716-168">Un esempio comune è rappresentato dal recupero di un valore numerico da un nodo XML.</span><span class="sxs-lookup"><span data-stu-id="fa716-168">A common example is to get a numeric value from an XML node.</span></span> <span data-ttu-id="fa716-169">Si consideri, ad esempio, il seguente documento XML non convalidato né tipizzato:</span><span class="sxs-lookup"><span data-stu-id="fa716-169">For example, consider the following unvalidated and untyped XML document.</span></span>  
  
```xml  
<books>  
    <book>  
        <title>Title</title>  
        <price>10.00</price>  
        <published>2003-12-31</published>  
    </book>  
</books>  
```  
  
 <span data-ttu-id="fa716-170">Se il tipo <xref:System.Xml.XPath.XPathNavigator> è posizionato sull'elemento `price`, la proprietà <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> sarà `null`, la proprietà <xref:System.Xml.XPath.XPathNavigator.ValueType%2A> sarà <xref:System.String> e la proprietà <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> sarà la stringa `10.00`.</span><span class="sxs-lookup"><span data-stu-id="fa716-170">If the <xref:System.Xml.XPath.XPathNavigator> is positioned on the `price` element the <xref:System.Xml.XPath.XPathNavigator.XmlType%2A> property would be `null`, the <xref:System.Xml.XPath.XPathNavigator.ValueType%2A> property would be <xref:System.String>, and the <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> property would be the string `10.00`.</span></span>  
  
 <span data-ttu-id="fa716-171">Tuttavia, è possibile estrarre il valore come valore numerico usando il metodo <xref:System.Xml.XPath.XPathItem.ValueAs%2A> oppure la proprietà <xref:System.Xml.XPath.XPathNavigator.ValueAsDouble%2A>, <xref:System.Xml.XPath.XPathNavigator.ValueAsInt%2A> o <xref:System.Xml.XPath.XPathNavigator.ValueAsLong%2A>.</span><span class="sxs-lookup"><span data-stu-id="fa716-171">However, it is still possible to extract the value as a numeric value using the <xref:System.Xml.XPath.XPathItem.ValueAs%2A>, <xref:System.Xml.XPath.XPathNavigator.ValueAsDouble%2A>, <xref:System.Xml.XPath.XPathNavigator.ValueAsInt%2A>, or <xref:System.Xml.XPath.XPathNavigator.ValueAsLong%2A> method and properties.</span></span> <span data-ttu-id="fa716-172">Nell'esempio seguente viene illustrata l'esecuzione di questo cast usando il metodo <xref:System.Xml.XPath.XPathItem.ValueAs%2A>.</span><span class="sxs-lookup"><span data-stu-id="fa716-172">The following example illustrates performing such a cast using the <xref:System.Xml.XPath.XPathItem.ValueAs%2A> method.</span></span>  
  
```vb  
Dim document As New XmlDocument()  
document.Load("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
navigator.MoveToChild("books", "")  
navigator.MoveToChild("book", "")  
navigator.MoveToChild("price", "")  
  
Dim price = navigator.ValueAs(GetType(Decimal))  
Dim discount As Decimal = 0.2  
  
Console.WriteLine("The price of the book has been dropped 20% from {0:C} to {1:C}", navigator.Value, (price - price * discount))  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
navigator.MoveToChild("books", "");  
navigator.MoveToChild("book", "");  
navigator.MoveToChild("price", "");  
  
Decimal price = (decimal)navigator.ValueAs(typeof(decimal));  
  
Console.WriteLine("The price of the book has been dropped 20% from {0:C} to {1:C}", navigator.Value, (price - price * (decimal)0.20));  
```  
  
 <span data-ttu-id="fa716-173">Per altre informazioni sul mapping dai tipi incorporati nello schema a tipi CLR, vedere [Supporto di tipi di dati nelle classi System.Xml](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).</span><span class="sxs-lookup"><span data-stu-id="fa716-173">For more information about the mapping from schema built-in types to CLR types, see [Type Support in the System.Xml Classes](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fa716-174">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="fa716-174">See also</span></span>

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [<span data-ttu-id="fa716-175">Supporto di tipi di dati nelle classi System.Xml</span><span class="sxs-lookup"><span data-stu-id="fa716-175">Type Support in the System.Xml Classes</span></span>](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)
- [<span data-ttu-id="fa716-176">Elaborazione di dati XML con il modello di dati XPath</span><span class="sxs-lookup"><span data-stu-id="fa716-176">Process XML Data Using the XPath Data Model</span></span>](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [<span data-ttu-id="fa716-177">Navigazione del set di nodi con XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="fa716-177">Node Set Navigation Using XPathNavigator</span></span>](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)
- [<span data-ttu-id="fa716-178">Navigazione dei nodi di attributi e dello spazio dei nomi con XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="fa716-178">Attribute and Namespace Node Navigation Using XPathNavigator</span></span>](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)
- [<span data-ttu-id="fa716-179">Estrazione di dati XML con XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="fa716-179">Extract XML Data Using XPathNavigator</span></span>](../../../../docs/standard/data/xml/extract-xml-data-using-xpathnavigator.md)

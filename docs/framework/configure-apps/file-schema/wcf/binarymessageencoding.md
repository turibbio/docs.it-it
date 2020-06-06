---
title: <binaryMessageEncoding>
ms.date: 03/30/2017
ms.assetid: e4ae3cd4-6b67-4ce1-af4b-9400e0a38dba
ms.openlocfilehash: afe0479d9cbf6d754b309c18e23d3a479870177c
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "73739080"
---
# \<binaryMessageEncoding>
<span data-ttu-id="7a8ec-101">Definisce un codificatore di messaggi binario che codifica messaggi di Windows Communication Foundation (WCF) in transito in formato binario.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-101">Defines a binary message encoder that encodes Windows Communication Foundation (WCF) messages in binary on the wire.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binaryMessageEncoding>**  
  
## <a name="syntax"></a><span data-ttu-id="7a8ec-102">Sintassi</span><span class="sxs-lookup"><span data-stu-id="7a8ec-102">Syntax</span></span>  
  
```xml  
<binaryMessageEncoding maxReadPoolSize="Integer"
                       maxSessionSize="Integer"
                       maxWritePoolSize="Integer"
                       messageVersion="Soap11Addressing10/Soap12Addressing10" />
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="7a8ec-103">Attributi ed elementi</span><span class="sxs-lookup"><span data-stu-id="7a8ec-103">Attributes and Elements</span></span>  
 <span data-ttu-id="7a8ec-104">Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-104">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="7a8ec-105">Attributi</span><span class="sxs-lookup"><span data-stu-id="7a8ec-105">Attributes</span></span>  
  
|<span data-ttu-id="7a8ec-106">Attributo</span><span class="sxs-lookup"><span data-stu-id="7a8ec-106">Attribute</span></span>|<span data-ttu-id="7a8ec-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7a8ec-107">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="7a8ec-108">maxReadPoolSize</span><span class="sxs-lookup"><span data-stu-id="7a8ec-108">maxReadPoolSize</span></span>|<span data-ttu-id="7a8ec-109">Numero intero che definisce il numero di messaggi che possono essere letti contemporaneamente senza allocare nuovi lettori.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-109">An integer that defines how many messages can be read simultaneously without allocating new readers.</span></span> <span data-ttu-id="7a8ec-110">Dimensioni maggiori del pool rendono il sistema più tollerante ai picchi di attività al costo di un working set superiore.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-110">Larger pool sizes make the system more tolerant to activity spikes at the cost of a larger working set.</span></span> <span data-ttu-id="7a8ec-111">Il valore predefinito è 64.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-111">The default is 64.</span></span>|  
|<span data-ttu-id="7a8ec-112">maxSessionSize</span><span class="sxs-lookup"><span data-stu-id="7a8ec-112">maxSessionSize</span></span>|<span data-ttu-id="7a8ec-113">Numero intero positivo che imposta la dimensione, in byte, del buffer usato per la codifica.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-113">A positive integer that sets the size, in bytes, of the buffer used for encoding.</span></span> <span data-ttu-id="7a8ec-114">Un buffer più grande aumenta la velocità di codifica a spese della dimensione del working set.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-114">A larger buffer increases encoding speed at the expense of the size of the working set.</span></span> <span data-ttu-id="7a8ec-115">Il valore predefinito è 2048.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-115">The default is 2048.</span></span>|  
|<span data-ttu-id="7a8ec-116">maxWritePoolSize</span><span class="sxs-lookup"><span data-stu-id="7a8ec-116">maxWritePoolSize</span></span>|<span data-ttu-id="7a8ec-117">Numero intero che definisce il numero di messaggi che possono essere inviati contemporaneamente senza allocare nuovi writer.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-117">An integer that defines how many messages can be sent simultaneously without allocating new writers.</span></span> <span data-ttu-id="7a8ec-118">Dimensioni maggiori del pool rendono il sistema più tollerante ai picchi di attività al costo di un working set superiore.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-118">Larger pool sizes make the system more tolerant to activity spikes at the cost of a larger working set.</span></span> <span data-ttu-id="7a8ec-119">Il valore predefinito è 16.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-119">The default is 16.</span></span>|  
|<span data-ttu-id="7a8ec-120">messageVersion</span><span class="sxs-lookup"><span data-stu-id="7a8ec-120">messageVersion</span></span>|<span data-ttu-id="7a8ec-121">Specifica le versioni del messaggio SOAP e WS-Addressing usate o previste.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-121">Specifies the SOAP message and WS-Addressing versions that are used or expected.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="7a8ec-122">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="7a8ec-122">Child Elements</span></span>  
  
|<span data-ttu-id="7a8ec-123">Elemento</span><span class="sxs-lookup"><span data-stu-id="7a8ec-123">Element</span></span>|<span data-ttu-id="7a8ec-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7a8ec-124">Description</span></span>|  
|-------------|-----------------|  
|[\<readerQuotas>](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|<span data-ttu-id="7a8ec-125">Definisce i vincoli sulla complessità dei messaggi SOAP che possono essere elaborati dagli endpoint configurati con questa associazione.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-125">Defines the constraints on the complexity of SOAP messages that can be processed by endpoints configured with this binding.</span></span> <span data-ttu-id="7a8ec-126">L'elemento è di tipo <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-126">This element is of type <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="7a8ec-127">Elementi padre</span><span class="sxs-lookup"><span data-stu-id="7a8ec-127">Parent Elements</span></span>  
  
|<span data-ttu-id="7a8ec-128">Elemento</span><span class="sxs-lookup"><span data-stu-id="7a8ec-128">Element</span></span>|<span data-ttu-id="7a8ec-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7a8ec-129">Description</span></span>|  
|-------------|-----------------|  
|[\<binding>](bindings.md)|<span data-ttu-id="7a8ec-130">Definisce tutte le funzionalità di associazione dell'associazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-130">Defines all binding capabilities of the custom binding.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="7a8ec-131">Commenti</span><span class="sxs-lookup"><span data-stu-id="7a8ec-131">Remarks</span></span>  
 <span data-ttu-id="7a8ec-132">La codifica è il processo di trasformazione di un messaggio in una sequenza di byte.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-132">Encoding is the process of transforming a message into a sequence of bytes.</span></span> <span data-ttu-id="7a8ec-133">La decodifica è il processo inverso.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-133">Decoding is the reverse process.</span></span> <span data-ttu-id="7a8ec-134">Windows Communication Foundation (WCF) include tre tipi di codifica per i messaggi SOAP, ovvero testo, binaria e MTOM (Message Transmission Optimization Mechanism).</span><span class="sxs-lookup"><span data-stu-id="7a8ec-134">Windows Communication Foundation (WCF) includes three types of encoding for SOAP messages: Text, Binary and Message Transmission Optimization Mechanism (MTOM).</span></span>  
  
 <span data-ttu-id="7a8ec-135">L'elemento `binaryMessageEncoding` specifica il formato binario .NET per XML e dispone delle opzioni che consentono di specificare la codifica dei caratteri e le versioni SOAP e WS-Addressing da usare.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-135">The `binaryMessageEncoding` element specifies the .NET Binary Format for XML and has options to specify the character encoding and the SOAP and WS-Addressing version to be used.</span></span> <span data-ttu-id="7a8ec-136">Il codificatore di messaggi binario codifica messaggi di Windows Communication Foundation (WCF) in transito in formato binario.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-136">The binary message encoder encodes Windows Communication Foundation (WCF) messages in binary on the wire.</span></span> <span data-ttu-id="7a8ec-137">Se da un lato questa codifica comporta una trasmissione molto veloce dei messaggi, dall'altro si perde l'interoperabilità basata sugli standard WS - \*.</span><span class="sxs-lookup"><span data-stu-id="7a8ec-137">While this encoding results in very fast transmission of messages, interoperability based on the WS-\* standards is lost.</span></span>  
  
## <a name="example"></a><span data-ttu-id="7a8ec-138">Esempio</span><span class="sxs-lookup"><span data-stu-id="7a8ec-138">Example</span></span>  
  
```xml  
<binaryMessageEncoding maxReadPoolSize="211"
                       maxWritePoolSize="2132"
                       maxSessionSize="3141" />
```  
  
## <a name="see-also"></a><span data-ttu-id="7a8ec-139">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7a8ec-139">See also</span></span>

- <xref:System.ServiceModel.Configuration.BinaryMessageEncodingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>
- <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>
- [<span data-ttu-id="7a8ec-140">Codifica dei messaggi</span><span class="sxs-lookup"><span data-stu-id="7a8ec-140">Message Encoding</span></span>](message-encoding.md)
- [<span data-ttu-id="7a8ec-141">Scelta di un codificatore di messaggi</span><span class="sxs-lookup"><span data-stu-id="7a8ec-141">Choosing a Message Encoder</span></span>](../../../wcf/feature-details/choosing-a-message-encoder.md)
- [<span data-ttu-id="7a8ec-142">Binding</span><span class="sxs-lookup"><span data-stu-id="7a8ec-142">Bindings</span></span>](../../../wcf/bindings.md)
- [<span data-ttu-id="7a8ec-143">Estensione delle associazioni</span><span class="sxs-lookup"><span data-stu-id="7a8ec-143">Extending Bindings</span></span>](../../../wcf/extending/extending-bindings.md)
- [<span data-ttu-id="7a8ec-144">Associazioni personalizzate</span><span class="sxs-lookup"><span data-stu-id="7a8ec-144">Custom Bindings</span></span>](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)

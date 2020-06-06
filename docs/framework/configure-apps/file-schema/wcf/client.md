---
title: <client>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.ServiceModel/client
- http://schemas.microsoft.com/.NetConfiguration/v2.0#client
ms.assetid: bf0f7031-76c8-4e7e-a6c6-9ad9119134be
ms.openlocfilehash: 7aa3755be97a839cb576d53852b75cfe50e39276
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "72773938"
---
# \<client>
<span data-ttu-id="42edf-101">L'elemento `client` definisce un elenco di endpoint ai quali può connettersi un client.</span><span class="sxs-lookup"><span data-stu-id="42edf-101">The `client` element defines a list of endpoints that a client can connect to.</span></span>

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<client>**

## <a name="syntax"></a><span data-ttu-id="42edf-102">Sintassi</span><span class="sxs-lookup"><span data-stu-id="42edf-102">Syntax</span></span>

```xml
<system.serviceModel>
  <client>
    <endpoint>
    </endpoint>
    <metadata>
    </metadata>
  </client>
</system.serviceModel>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="42edf-103">Attributi ed elementi</span><span class="sxs-lookup"><span data-stu-id="42edf-103">Attributes and Elements</span></span>
 <span data-ttu-id="42edf-104">Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="42edf-104">The following sections describe attributes, child elements, and parent elements.</span></span>

### <a name="attributes"></a><span data-ttu-id="42edf-105">Attributi</span><span class="sxs-lookup"><span data-stu-id="42edf-105">Attributes</span></span>
 <span data-ttu-id="42edf-106">nessuno</span><span class="sxs-lookup"><span data-stu-id="42edf-106">None</span></span>

### <a name="child-elements"></a><span data-ttu-id="42edf-107">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="42edf-107">Child Elements</span></span>

|<span data-ttu-id="42edf-108">Elemento</span><span class="sxs-lookup"><span data-stu-id="42edf-108">Element</span></span>|<span data-ttu-id="42edf-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="42edf-109">Description</span></span>|
|-------------|-----------------|
|[\<endpoint>](endpoint-of-client.md)|<span data-ttu-id="42edf-110">Contiene una raccolta di elementi endpoint che specificano gli endpoint a cui il client può connettersi.</span><span class="sxs-lookup"><span data-stu-id="42edf-110">Contains a collection of endpoint elements that specify the endpoints that this client can connect to.</span></span>|
|[\<metadata>](metadata.md)|<span data-ttu-id="42edf-111">Contiene impostazioni per l'elaborazione di metadati.</span><span class="sxs-lookup"><span data-stu-id="42edf-111">Contains settings for processing metadata.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="42edf-112">Elementi padre</span><span class="sxs-lookup"><span data-stu-id="42edf-112">Parent Elements</span></span>

|<span data-ttu-id="42edf-113">Elemento</span><span class="sxs-lookup"><span data-stu-id="42edf-113">Element</span></span>|<span data-ttu-id="42edf-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="42edf-114">Description</span></span>|
|-------------|-----------------|
|[\<system.serviceModel>](system-servicemodel.md)|<span data-ttu-id="42edf-115">L'elemento radice di tutti gli elementi di configurazione di Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="42edf-115">The root element of all Windows Communication Foundation (WCF) configuration elements.</span></span>|

## <a name="remarks"></a><span data-ttu-id="42edf-116">Commenti</span><span class="sxs-lookup"><span data-stu-id="42edf-116">Remarks</span></span>
 <span data-ttu-id="42edf-117">La sezione `client` definisce un elenco di endpoint ai quali può connettersi un client.</span><span class="sxs-lookup"><span data-stu-id="42edf-117">The `client` section defines a list of endpoints that a client can connect to.</span></span> <span data-ttu-id="42edf-118">Ogni endpoint elencato nella sezione client definisce la propria associazione, comportamento e contratto.</span><span class="sxs-lookup"><span data-stu-id="42edf-118">Each endpoint listed in the client section defines its own binding, behavior, and contract.</span></span> <span data-ttu-id="42edf-119">È identificato in modo univoco dalla combinazione degli attributi `name` e `contract`.</span><span class="sxs-lookup"><span data-stu-id="42edf-119">It is uniquely identified by the combination of the `name` and `contract` attributes.</span></span> <span data-ttu-id="42edf-120">Il codice client specifica il `name` al quale connettere un endpoint per il servizio implementato dal client.</span><span class="sxs-lookup"><span data-stu-id="42edf-120">The client code specifies the `name` to connect to an endpoint for the service that the client implements.</span></span> <span data-ttu-id="42edf-121">Se l'attributo `name` è omesso, l'endpoint si comporta come endpoint predefinito per il contratto che implementa.</span><span class="sxs-lookup"><span data-stu-id="42edf-121">If the `name` attribute is omitted, the endpoint acts as the default endpoint for the contract it implements.</span></span>

 <span data-ttu-id="42edf-122">In aggiunta, questa sezione specifica anche impostazioni per l'elaborazione di metadati.</span><span class="sxs-lookup"><span data-stu-id="42edf-122">In addition, this section also specifies settings for processing metadata.</span></span>

## <a name="example"></a><span data-ttu-id="42edf-123">Esempio</span><span class="sxs-lookup"><span data-stu-id="42edf-123">Example</span></span>

```xml
<client>
  <endpoint address="/HelloWorld/"
            bindingConfiguration="usingDefaults"
            name="MyBinding"
            binding="customBinding"
            contract="HelloWorld">
    <addressProperties actingAs="http://www.microsoft.com/TestActor"
                       identityData="BasicReadWrite"
                       identityType="Spn"
                       isAddressPrivate="false">
  </endpoint>
</client>
```

## <a name="see-also"></a><span data-ttu-id="42edf-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="42edf-124">See also</span></span>

- <xref:System.ServiceModel.Configuration.ClientSection>
- <xref:System.ServiceModel.Configuration.MetadataElement>
- [<span data-ttu-id="42edf-125">Configurazione del client WCF</span><span class="sxs-lookup"><span data-stu-id="42edf-125">WCF Client Configuration</span></span>](../../../wcf/feature-details/client-configuration.md)
- [<span data-ttu-id="42edf-126">Client</span><span class="sxs-lookup"><span data-stu-id="42edf-126">Clients</span></span>](../../../wcf/feature-details/clients.md)

---
title: <callbackDebug>
ms.date: 03/30/2017
ms.assetid: 4073feda-1857-4be4-9947-227afb847ced
ms.openlocfilehash: 92a8fa83b5cf5f429278ac8edc8439b627839aad
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "70400562"
---
# \<callbackDebug>
<span data-ttu-id="e7040-101">Specifica il debug del servizio per un oggetto callback di Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="e7040-101">Specifies service debugging for a Windows Communication Foundation (WCF) callback object.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<callbackDebug>**  
  
## <a name="syntax"></a><span data-ttu-id="e7040-102">Sintassi</span><span class="sxs-lookup"><span data-stu-id="e7040-102">Syntax</span></span>  
  
```xml  
<callbackDebug includeExceptionDetailInFaults="Boolean" />
```  
  
## <a name="type"></a><span data-ttu-id="e7040-103">Tipo</span><span class="sxs-lookup"><span data-stu-id="e7040-103">Type</span></span>  
 `Type`  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="e7040-104">Attributi ed elementi</span><span class="sxs-lookup"><span data-stu-id="e7040-104">Attributes and Elements</span></span>  
 <span data-ttu-id="e7040-105">Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="e7040-105">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="e7040-106">Attributi</span><span class="sxs-lookup"><span data-stu-id="e7040-106">Attributes</span></span>  
  
|<span data-ttu-id="e7040-107">Attributo</span><span class="sxs-lookup"><span data-stu-id="e7040-107">Attribute</span></span>|<span data-ttu-id="e7040-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e7040-108">Description</span></span>|  
|---------------|-----------------|  
|`includeExceptionDetailInFaults`|<span data-ttu-id="e7040-109">Valore che specifica se oggetti callback del client restituiscono al servizio informazioni sulle eccezioni gestite negli errori SOAP.</span><span class="sxs-lookup"><span data-stu-id="e7040-109">A value that specifies whether client callback objects return managed exception information in SOAP faults back to the service.</span></span><br /><br /> <span data-ttu-id="e7040-110">Se questo attributo viene impostato su `true` a livello di programmazione, è possibile abilitare il flusso di informazioni sulle eccezioni gestite in un oggetto callback del client nel servizio a fini di debug.</span><span class="sxs-lookup"><span data-stu-id="e7040-110">If you set this attribute to `true` programmatically, you can enable the flow of managed exception information in a client callback object back to the service for debugging purposes.</span></span> <span data-ttu-id="e7040-111">**Attenzione:**  La restituzione di informazioni sulle eccezioni gestite ai client può costituire un rischio per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="e7040-111">**Caution:**  Returning managed exception information to clients can be a security risk.</span></span> <span data-ttu-id="e7040-112">Questo perché i dettagli delle eccezioni espongono informazioni sull'implementazione interna del servizio che potrebbero venire usate da client non autorizzati.</span><span class="sxs-lookup"><span data-stu-id="e7040-112">This is because exception details expose information about the internal service implementation that could be used by unauthorized clients.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="e7040-113">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="e7040-113">Child Elements</span></span>  
 <span data-ttu-id="e7040-114">No.</span><span class="sxs-lookup"><span data-stu-id="e7040-114">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="e7040-115">Elementi padre</span><span class="sxs-lookup"><span data-stu-id="e7040-115">Parent Elements</span></span>  
  
|<span data-ttu-id="e7040-116">Elemento</span><span class="sxs-lookup"><span data-stu-id="e7040-116">Element</span></span>|<span data-ttu-id="e7040-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e7040-117">Description</span></span>|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|<span data-ttu-id="e7040-118">Specifica un comportamento dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="e7040-118">Specifies an endpoint behavior.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="e7040-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e7040-119">See also</span></span>

- <xref:System.ServiceModel.Configuration.CallbackDebugElement>
- <xref:System.ServiceModel.Description.CallbackDebugBehavior>

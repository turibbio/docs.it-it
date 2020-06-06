---
title: <enableWebScript>
ms.date: 03/30/2017
ms.assetid: 9c7e96e1-af70-4e6e-ac5c-d67929dddbaa
ms.openlocfilehash: 20c0057c80b668df97379d0168bb7c005d9927ce
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "70400379"
---
# \<enableWebScript>
<span data-ttu-id="fe250-101">Questo elemento attiva il comportamento dell'endpoint che rende possibile l'uso del servizio da pagine Web ASP.NET AJAX.</span><span class="sxs-lookup"><span data-stu-id="fe250-101">This element enables the endpoint behavior that makes it possible to consume the service from ASP.NET AJAX web pages.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<enableWebScript>**  
  
## <a name="syntax"></a><span data-ttu-id="fe250-102">Sintassi</span><span class="sxs-lookup"><span data-stu-id="fe250-102">Syntax</span></span>  
  
```xml  
<enableWebScript />
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="fe250-103">Attributi ed elementi</span><span class="sxs-lookup"><span data-stu-id="fe250-103">Attributes and Elements</span></span>  
 <span data-ttu-id="fe250-104">Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="fe250-104">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="fe250-105">Attributi</span><span class="sxs-lookup"><span data-stu-id="fe250-105">Attributes</span></span>  
 <span data-ttu-id="fe250-106">No.</span><span class="sxs-lookup"><span data-stu-id="fe250-106">None.</span></span>  
  
### <a name="child-elements"></a><span data-ttu-id="fe250-107">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="fe250-107">Child Elements</span></span>  
 <span data-ttu-id="fe250-108">No.</span><span class="sxs-lookup"><span data-stu-id="fe250-108">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="fe250-109">Elementi padre</span><span class="sxs-lookup"><span data-stu-id="fe250-109">Parent Elements</span></span>  
  
|<span data-ttu-id="fe250-110">Elemento</span><span class="sxs-lookup"><span data-stu-id="fe250-110">Element</span></span>|<span data-ttu-id="fe250-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fe250-111">Description</span></span>|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|<span data-ttu-id="fe250-112">Specifica l'insieme di comportamenti dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="fe250-112">Specifies the set of endpoint behaviors.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="fe250-113">Commenti</span><span class="sxs-lookup"><span data-stu-id="fe250-113">Remarks</span></span>  
 <span data-ttu-id="fe250-114">Questo comportamento deve essere usato solo in combinazione con l' [\<webHttpBinding>](webhttpbinding.md) associazione standard o con l' [\<webMessageEncoding>](webmessageencoding.md) elemento di associazione.</span><span class="sxs-lookup"><span data-stu-id="fe250-114">This behavior should only be used in conjunction with either the [\<webHttpBinding>](webhttpbinding.md) standard binding, or the [\<webMessageEncoding>](webmessageencoding.md) binding element.</span></span>  <span data-ttu-id="fe250-115">Per altre informazioni su questo comportamento, vedere <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>.</span><span class="sxs-lookup"><span data-stu-id="fe250-115">For more information on this behavior, see <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fe250-116">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="fe250-116">See also</span></span>

- <xref:System.ServiceModel.Configuration.WebScriptEnablingElement>
- <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>
- [<span data-ttu-id="fe250-117">Integrazione AJAX e supporto JSON</span><span class="sxs-lookup"><span data-stu-id="fe250-117">AJAX Integration and JSON Support</span></span>](../../../wcf/feature-details/ajax-integration-and-json-support.md)
- [\<webHttp>](webhttp.md)

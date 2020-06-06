---
title: Elemento <performanceCounter> (impostazioni di rete)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/performanceCounters
- http://schemas.microsoft.com/.NetConfiguration/v2.0#performanceCounters
helpviewer_keywords:
- performanceCounter element
- <performanceCounter> element
ms.assetid: 3afa1586-e1b8-473d-8985-c3fc90cf561b
ms.openlocfilehash: 58a2bf5118a3a2cd9c33301eca5dcc751c2351bf
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "74283086"
---
# <a name="performancecounter-element-network-settings"></a><span data-ttu-id="703b6-102">Elemento \<performanceCounter> (impostazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="703b6-102">\<performanceCounter> Element (Network Settings)</span></span>
<span data-ttu-id="703b6-103">Abilita o Disabilita i contatori delle prestazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="703b6-103">Enables or disables networking performance counters.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<settings>**](settings-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<performanceCounters>**

## <a name="syntax"></a><span data-ttu-id="703b6-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="703b6-104">Syntax</span></span>  
  
```xml  
<performanceCounters  
  enabled="true|false"  
/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="703b6-105">Attributi ed elementi</span><span class="sxs-lookup"><span data-stu-id="703b6-105">Attributes and Elements</span></span>  
 <span data-ttu-id="703b6-106">Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="703b6-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="703b6-107">Attributi</span><span class="sxs-lookup"><span data-stu-id="703b6-107">Attributes</span></span>  
  
|<span data-ttu-id="703b6-108">Attributo</span><span class="sxs-lookup"><span data-stu-id="703b6-108">Attribute</span></span>|<span data-ttu-id="703b6-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="703b6-109">Description</span></span>|  
|---------------|-----------------|  
|`enabled`|<span data-ttu-id="703b6-110">Specifica se i contatori delle prestazioni di rete sono abilitati.</span><span class="sxs-lookup"><span data-stu-id="703b6-110">Specifies whether the networking performance counters are enabled.</span></span> <span data-ttu-id="703b6-111">Il valore predefinito è `false`.</span><span class="sxs-lookup"><span data-stu-id="703b6-111">The default value is `false`.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="703b6-112">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="703b6-112">Child Elements</span></span>  
 <span data-ttu-id="703b6-113">No.</span><span class="sxs-lookup"><span data-stu-id="703b6-113">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="703b6-114">Elementi padre</span><span class="sxs-lookup"><span data-stu-id="703b6-114">Parent Elements</span></span>  
  
|<span data-ttu-id="703b6-115">Elemento</span><span class="sxs-lookup"><span data-stu-id="703b6-115">Element</span></span>|<span data-ttu-id="703b6-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="703b6-116">Description</span></span>|  
|-------------|-----------------|  
|[<span data-ttu-id="703b6-117">impostazioni</span><span class="sxs-lookup"><span data-stu-id="703b6-117">settings</span></span>](settings-element-network-settings.md)|<span data-ttu-id="703b6-118">Configura le opzioni di rete di base per lo spazio dei nomi <xref:System.Net>.</span><span class="sxs-lookup"><span data-stu-id="703b6-118">Configures basic network options for the <xref:System.Net> namespace.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="703b6-119">Commenti</span><span class="sxs-lookup"><span data-stu-id="703b6-119">Remarks</span></span>  
 <span data-ttu-id="703b6-120">Questo elemento può essere usato nel file di configurazione dell'applicazione o nel file di configurazione del computer (Machine.config).</span><span class="sxs-lookup"><span data-stu-id="703b6-120">This element can be used in the application configuration file or the machine configuration file (Machine.config).</span></span>  
  
 <span data-ttu-id="703b6-121">I contatori delle prestazioni della rete devono essere abilitati nel file di configurazione da usare.</span><span class="sxs-lookup"><span data-stu-id="703b6-121">Networking performance counters need to be enabled in the configuration file to be used.</span></span> <span data-ttu-id="703b6-122">Tutti i contatori delle prestazioni della rete vengono abilitati o disabilitati con una singola impostazione nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="703b6-122">All networking performance counters are enabled or disabled with a single setting in the configuration file.</span></span> <span data-ttu-id="703b6-123">Non è possibile abilitare o disabilitare singoli contatori delle prestazioni della rete.</span><span class="sxs-lookup"><span data-stu-id="703b6-123">Individual networking performance counters cannot be enabled or disabled.</span></span> <span data-ttu-id="703b6-124">Per ulteriori informazioni sui contatori delle prestazioni di rete specifici, vedere [contatori delle prestazioni di rete](../../../debug-trace-profile/performance-counters.md#networking-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="703b6-124">For more information on the specific networking performance counters, see [Networking performance counters](../../../debug-trace-profile/performance-counters.md#networking-performance-counters).</span></span>  
  
 <span data-ttu-id="703b6-125">Il valore predefinito è che i contatori delle prestazioni di rete sono disabilitati.</span><span class="sxs-lookup"><span data-stu-id="703b6-125">The default value is that networking performance counters are disabled.</span></span>  
  
 <span data-ttu-id="703b6-126"><xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=nameWithType>È possibile utilizzare la proprietà per ottenere il valore corrente dell'attributo **Enabled** dai file di configurazione applicabili.</span><span class="sxs-lookup"><span data-stu-id="703b6-126">The <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=nameWithType> property can be used to get the current value of the **enabled** attribute from applicable configuration files.</span></span>  
  
## <a name="example"></a><span data-ttu-id="703b6-127">Esempio</span><span class="sxs-lookup"><span data-stu-id="703b6-127">Example</span></span>  
 <span data-ttu-id="703b6-128">Nell'esempio seguente viene illustrato come configurare gli <xref:System.Net> spazi dei nomi e correlati per abilitare i contatori delle prestazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="703b6-128">The following example shows how to configure the <xref:System.Net> and related namespaces to enable networking performance counters.</span></span>  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <performanceCounters  
        enabled="true"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="703b6-129">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="703b6-129">See also</span></span>

- <xref:System.Net.Configuration.PerformanceCountersElement?displayProperty=nameWithType>
- <xref:System.Net.Configuration.PerformanceCountersElement.Enabled%2A?displayProperty=nameWithType>
- [<span data-ttu-id="703b6-130">Schema delle impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="703b6-130">Network Settings Schema</span></span>](index.md)
- [<span data-ttu-id="703b6-131">Contatori delle prestazioni di rete</span><span class="sxs-lookup"><span data-stu-id="703b6-131">Networking Performance Counters</span></span>](../../../debug-trace-profile/performance-counters.md#networking-performance-counters)

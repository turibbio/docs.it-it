---
title: <clear>Elemento per <listeners> per<trace>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/clear
helpviewer_keywords:
- clear element for <listeners> for <trace>
- <clear> element for <listeners> for <trace>
ms.assetid: b44732a8-271f-4a06-ba9e-fe3298d6f192
ms.openlocfilehash: 905dad8274fede80f4809ff3c7a014049f9df450
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153542"
---
# <a name="clear-element-for-listeners-for-trace"></a><span data-ttu-id="144cc-102">\<clear>Elemento per \<listeners> per\<trace></span><span class="sxs-lookup"><span data-stu-id="144cc-102">\<clear> Element for \<listeners> for \<trace></span></span>
<span data-ttu-id="144cc-103">Cancella la raccolta `Listeners` per una traccia.</span><span class="sxs-lookup"><span data-stu-id="144cc-103">Clears the `Listeners` collection for trace.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<trace>**](trace-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<listeners>**](listeners-element-for-trace.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<clear>**

## <a name="syntax"></a><span data-ttu-id="144cc-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="144cc-104">Syntax</span></span>  
  
```xml  
<clear/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="144cc-105">Attributi ed elementi</span><span class="sxs-lookup"><span data-stu-id="144cc-105">Attributes and Elements</span></span>  
 <span data-ttu-id="144cc-106">Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="144cc-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="144cc-107">Attributi</span><span class="sxs-lookup"><span data-stu-id="144cc-107">Attributes</span></span>  
 <span data-ttu-id="144cc-108">No.</span><span class="sxs-lookup"><span data-stu-id="144cc-108">None.</span></span>  
  
### <a name="child-elements"></a><span data-ttu-id="144cc-109">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="144cc-109">Child Elements</span></span>  
 <span data-ttu-id="144cc-110">No.</span><span class="sxs-lookup"><span data-stu-id="144cc-110">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="144cc-111">Elementi padre</span><span class="sxs-lookup"><span data-stu-id="144cc-111">Parent Elements</span></span>  
  
|<span data-ttu-id="144cc-112">Elemento</span><span class="sxs-lookup"><span data-stu-id="144cc-112">Element</span></span>|<span data-ttu-id="144cc-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="144cc-113">Description</span></span>|  
|-------------|-----------------|  
|`configuration`|<span data-ttu-id="144cc-114">Elemento radice in ciascun file di configurazione usato in Common Language Runtime e nelle applicazioni .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="144cc-114">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span>|  
|`system.diagnostics`|<span data-ttu-id="144cc-115">Specifica i listener di traccia per raccogliere, archiviare e indirizzare i messaggi, oltre al livello di impostazione di un'opzione di traccia.</span><span class="sxs-lookup"><span data-stu-id="144cc-115">Specifies trace listeners that collect, store, and route messages and the level where a trace switch is set.</span></span>|  
|`trace`|<span data-ttu-id="144cc-116">Contiene i listener che raccolgono, archiviano e indirizzano i messaggi di traccia.</span><span class="sxs-lookup"><span data-stu-id="144cc-116">Contains listeners that collect, store, and route tracing messages.</span></span>|  
|`listeners`|<span data-ttu-id="144cc-117">Contiene i listener che raccolgono, archiviano e indirizzano i messaggi.</span><span class="sxs-lookup"><span data-stu-id="144cc-117">Contains listeners that collect, store, and route messages.</span></span> <span data-ttu-id="144cc-118">I listener indirizzano l'output di traccia a una destinazione appropriata.</span><span class="sxs-lookup"><span data-stu-id="144cc-118">Listeners direct the tracing output to an appropriate target.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="144cc-119">Commenti</span><span class="sxs-lookup"><span data-stu-id="144cc-119">Remarks</span></span>  
 <span data-ttu-id="144cc-120">L' `<clear>` elemento rimuove tutti i listener dalla `Listeners` raccolta per Trace.</span><span class="sxs-lookup"><span data-stu-id="144cc-120">The `<clear>` element removes all listeners from the `Listeners` collection for trace.</span></span> <span data-ttu-id="144cc-121">È possibile usare l' `<clear>` elemento prima di usare l' `<add>` elemento per assicurarsi che non ci siano altri listener attivi nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="144cc-121">You can use the `<clear>` element before using the `<add>` element to be certain there are no other active listeners in the collection.</span></span>  
  
 <span data-ttu-id="144cc-122">È possibile cancellare la `Listeners` raccolta a livello di codice chiamando il <xref:System.Diagnostics.TraceListenerCollection.Clear%2A> Metodo sulla <xref:System.Diagnostics.Trace.Listeners%2A?displayProperty=nameWithType> Proprietà ( `System.Diagnostics.Trace.Listeners.Clear()` ).</span><span class="sxs-lookup"><span data-stu-id="144cc-122">You can clear the `Listeners` collection programmatically by calling the <xref:System.Diagnostics.TraceListenerCollection.Clear%2A> method on the <xref:System.Diagnostics.Trace.Listeners%2A?displayProperty=nameWithType> property (`System.Diagnostics.Trace.Listeners.Clear()`).</span></span>  
  
 <span data-ttu-id="144cc-123">Questo elemento può essere utilizzato nel file di configurazione del computer (Machine. config) e nel file di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="144cc-123">This element can be used in the machine configuration file (Machine.config) and the application configuration file.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="144cc-124">L' `<clear>` elemento rimuove <xref:System.Diagnostics.DefaultTraceListener> dalla `Listeners` raccolta, modificando il comportamento dei <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> metodi,, <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType> <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType> e <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=nameWithType> .</span><span class="sxs-lookup"><span data-stu-id="144cc-124">The `<clear>` element removes the <xref:System.Diagnostics.DefaultTraceListener> from the `Listeners` collection, altering the behavior of the <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>, <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType>, <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType>, and <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=nameWithType> methods.</span></span> <span data-ttu-id="144cc-125">La chiamata `Assert` `Fail` di un metodo o determina in genere la visualizzazione di una finestra di messaggio.</span><span class="sxs-lookup"><span data-stu-id="144cc-125">Calling an `Assert` or `Fail` method normally results in the display of a message box.</span></span> <span data-ttu-id="144cc-126">Tuttavia, la finestra di messaggio non viene visualizzata se l'oggetto <xref:System.Diagnostics.DefaultTraceListener> non è presente nella `Listeners` raccolta.</span><span class="sxs-lookup"><span data-stu-id="144cc-126">However, the message box is not displayed if the <xref:System.Diagnostics.DefaultTraceListener> is not in the `Listeners` collection.</span></span>  
  
## <a name="example"></a><span data-ttu-id="144cc-127">Esempio</span><span class="sxs-lookup"><span data-stu-id="144cc-127">Example</span></span>  
 <span data-ttu-id="144cc-128">Nell'esempio seguente viene illustrato come utilizzare l' `<clear>` elemento prima di utilizzare l' `<add>` elemento per aggiungere il listener `console` alla `Listeners` raccolta per Trace.</span><span class="sxs-lookup"><span data-stu-id="144cc-128">The following example shows how to use the `<clear>` element before using the `<add>` element to add the listener `console` to the `Listeners` collection for trace.</span></span>  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="false" indentsize="4">  
      <listeners>  
        <clear/>  
        <add name="console"
          type="System.Diagnostics.ConsoleTraceListener" >  
          <filter type="System.Diagnostics.EventTypeFilter"
            initializeData="Error" />  
        </add>  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>
```  
  
## <a name="see-also"></a><span data-ttu-id="144cc-129">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="144cc-129">See also</span></span>

- <xref:System.Diagnostics.Trace.Listeners%2A>
- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.Debug>
- <xref:System.Diagnostics.TraceSource>
- [<span data-ttu-id="144cc-130">Schema delle impostazioni di traccia e debug</span><span class="sxs-lookup"><span data-stu-id="144cc-130">Trace and Debug Settings Schema</span></span>](index.md)
- [\<remove>](remove-element-for-listeners-for-trace.md)
- [<span data-ttu-id="144cc-131">Listener di traccia</span><span class="sxs-lookup"><span data-stu-id="144cc-131">Trace Listeners</span></span>](../../../debug-trace-profile/trace-listeners.md)

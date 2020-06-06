---
title: <behaviorExtensions>
ms.date: 03/30/2017
ms.assetid: 59f2791a-c78f-40d7-aa80-0d9cd10135d9
ms.openlocfilehash: 39dc92d65a41d223ebd39aec3dc59871ad1fd101
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "77448685"
---
# \<behaviorExtensions>
<span data-ttu-id="e9594-101">Le estensioni di comportamento consentono all'utente di creare elementi di comportamento definiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="e9594-101">Behavior extensions enable the user to create user-defined behavior elements.</span></span> <span data-ttu-id="e9594-102">Questi elementi possono essere usati insieme agli elementi di comportamento standard di Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="e9594-102">These elements can be used alongside the standard Windows Communication Foundation (WCF) behavior elements.</span></span> <span data-ttu-id="e9594-103">Nella sezione `behaviorExtensions` l'elemento viene definito in modo tale che possa essere usato nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9594-103">The `behaviorExtensions` section defines the element such that it can be used in configuration.</span></span> <span data-ttu-id="e9594-104">Di seguito viene fornito l'esempio di una tipica estensione di comportamento.</span><span class="sxs-lookup"><span data-stu-id="e9594-104">Here is an example of a typical behavior extension.</span></span>  
  
```xml  
<system.serviceModel>
  <extensions>
    <behaviorExtensions>
      <add name="myBehavior"
           type="Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
                 Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    </behaviorExtensions>
  </extensions>
</system.serviceModel>
```  
  
 <span data-ttu-id="e9594-105">Per aggiungere capacità di configurazione all'elemento è necessario scrivere e registrare un elemento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e9594-105">To add configuration abilities to the element, you need to write and register a configuration element.</span></span> <span data-ttu-id="e9594-106">Per altre informazioni a tal proposito, vedere la documentazione di <xref:System.Configuration>.</span><span class="sxs-lookup"><span data-stu-id="e9594-106">For more information on this, see the <xref:System.Configuration> documentation.</span></span>  
  
 <span data-ttu-id="e9594-107">Dopo che l'elemento e il relativo tipo di configurazione sono stati definiti, è possibile usare l'estensione come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="e9594-107">After the element and its configuration type are defined, the extension can be used, as shown in the following example.</span></span>  
  
```xml  
<behaviors>
  <behavior configurationName="testChannelBehavior">
    <myBehavior />
    <channelSecurity cacheCookies="false"
                     detectReplays="false"
                     maxCachedNonces="9"
                     maxClockSkew="00:00:03"
                     maxCookieCachingTime="00:07:24"
                     replayWindow="00:07:22.2190000" />
  </behavior>
</behaviors>
```  
  
## <a name="security"></a><span data-ttu-id="e9594-108">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="e9594-108">Security</span></span>  
 <span data-ttu-id="e9594-109">È consigliato fortemente l'uso di nomi di assembly completi per la registrazione di tipi nei file `machine.config` e `app.config`.</span><span class="sxs-lookup"><span data-stu-id="e9594-109">It is strongly recommended that you use fully qualified assembly names when registering types in the `machine.config` and `app.config` files.</span></span> <span data-ttu-id="e9594-110">Se il tipo non è definito in modo univoco, il caricatore dei tipi CLR lo cerca nei percorsi seguenti nell'ordine specificato:</span><span class="sxs-lookup"><span data-stu-id="e9594-110">If the type is not uniquely defined, the CLR type loader searches for it in the following locations in the specified order:</span></span>  
  
 <span data-ttu-id="e9594-111">Se l'assembly del tipo è conosciuto, il caricatore esegue una ricerca nei percorsi di reindirizzamento del file di configurazione, in GAC, nell'assembly corrente usando le informazioni di configurazione e la directory base dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e9594-111">If the assembly of the type is known, the loader searches the configuration file's redirect locations, GAC, the current assembly using configuration information, and the application base directory.</span></span> <span data-ttu-id="e9594-112">Se l'assembly è sconosciuto, il caricatore esegue una ricerca nell'assembly corrente, in mscorlib e nel percorso restituito dal gestore eventi `TypeResolve`.</span><span class="sxs-lookup"><span data-stu-id="e9594-112">If the assembly is unknown, the loader searches the current assembly, mscorlib, and the location returned by the `TypeResolve` event handler.</span></span> <span data-ttu-id="e9594-113">Questo ordine di ricerca CLR può essere modificato con hook quali il meccanismo di inoltro dei tipi e l'evento AppDomain.TypeResolve.</span><span class="sxs-lookup"><span data-stu-id="e9594-113">This CLR search order can be modified with hooks such as the Type Forwarding mechanism and the AppDomain.TypeResolve event.</span></span>  
  
 <span data-ttu-id="e9594-114">Un autore di un attacco può sfruttare l'ordine di ricerca CLR ed eseguire codice non autorizzato.</span><span class="sxs-lookup"><span data-stu-id="e9594-114">An attacker can exploit the CLR search order and execute unauthorized code.</span></span> <span data-ttu-id="e9594-115">L'uso di nomi completi (sicuri) identifica un tipo in modo univoco e aumenta la sicurezza del sistema.</span><span class="sxs-lookup"><span data-stu-id="e9594-115">Using fully qualified (strong) names uniquely identifies a type and further increases security of your system.</span></span>  
  
 <span data-ttu-id="e9594-116">Per ulteriori informazioni, vedere [come il runtime individua gli assembly](../../../deployment/how-the-runtime-locates-assemblies.md) e <xref:System.AppDomain.TypeResolve> .</span><span class="sxs-lookup"><span data-stu-id="e9594-116">For more information, see [How the Runtime Locates Assemblies](../../../deployment/how-the-runtime-locates-assemblies.md) and <xref:System.AppDomain.TypeResolve>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e9594-117">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="e9594-117">See also</span></span>

- <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>
- [<span data-ttu-id="e9594-118">Configurazione ed estensione del runtime con i comportamenti</span><span class="sxs-lookup"><span data-stu-id="e9594-118">Configuring and Extending the Runtime with Behaviors</span></span>](../../../wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)

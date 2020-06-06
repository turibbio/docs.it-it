---
title: Elemento <remove> per authenticationModules (impostazioni di rete)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/authenticationModules/remove
- http://schemas.microsoft.com/.NetConfiguration/v2.0#remove
helpviewer_keywords:
- remove element, authenticationModules
- <authenticationModules>, remove element
- <remove> element, authenticationModules
- authenticationModules, remove element
ms.assetid: abf79949-b05c-465a-b51c-bbeda9a74173
ms.openlocfilehash: d171fea193bbae068e69b8976abb8e56a5623f02
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "79154777"
---
# <a name="remove-element-for-authenticationmodules-network-settings"></a><span data-ttu-id="55c67-102">Elemento \<remove> per authenticationModules (impostazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="55c67-102">\<remove> Element for authenticationModules (Network Settings)</span></span>
<span data-ttu-id="55c67-103">Rimuove un modulo di autenticazione dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="55c67-103">Removes an authentication module from the application.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<authenticationModules>**](authenticationmodules-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<remove>**

## <a name="syntax"></a><span data-ttu-id="55c67-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="55c67-104">Syntax</span></span>  
  
```xml  
<remove
   type="authentication module name"
/>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="55c67-105">Attributi ed elementi</span><span class="sxs-lookup"><span data-stu-id="55c67-105">Attributes and Elements</span></span>  
 <span data-ttu-id="55c67-106">Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="55c67-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="55c67-107">Attributi</span><span class="sxs-lookup"><span data-stu-id="55c67-107">Attributes</span></span>  
  
|<span data-ttu-id="55c67-108">**Attributo**</span><span class="sxs-lookup"><span data-stu-id="55c67-108">**Attribute**</span></span>|<span data-ttu-id="55c67-109">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="55c67-109">**Description**</span></span>|  
|-------------------|---------------------|  
|<span data-ttu-id="55c67-110">**type**</span><span class="sxs-lookup"><span data-stu-id="55c67-110">**type**</span></span>|<span data-ttu-id="55c67-111">Nome del modulo di autenticazione da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="55c67-111">The name of the authentication module to remove.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="55c67-112">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="55c67-112">Child Elements</span></span>  
 <span data-ttu-id="55c67-113">No.</span><span class="sxs-lookup"><span data-stu-id="55c67-113">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="55c67-114">Elementi padre</span><span class="sxs-lookup"><span data-stu-id="55c67-114">Parent Elements</span></span>  
  
|<span data-ttu-id="55c67-115">**Elemento**</span><span class="sxs-lookup"><span data-stu-id="55c67-115">**Element**</span></span>|<span data-ttu-id="55c67-116">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="55c67-116">**Description**</span></span>|  
|-----------------|---------------------|  
|[<span data-ttu-id="55c67-117">authenticationModules</span><span class="sxs-lookup"><span data-stu-id="55c67-117">authenticationModules</span></span>](authenticationmodules-element-network-settings.md)|<span data-ttu-id="55c67-118">Specifica i moduli usati per autenticare le richieste di rete.</span><span class="sxs-lookup"><span data-stu-id="55c67-118">Specifies modules used to authenticate network requests.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="55c67-119">Commenti</span><span class="sxs-lookup"><span data-stu-id="55c67-119">Remarks</span></span>  
 <span data-ttu-id="55c67-120">L' `remove` elemento rimuove i moduli di autenticazione definiti in precedenza nel file di configurazione o a un livello superiore nella gerarchia di configurazione.</span><span class="sxs-lookup"><span data-stu-id="55c67-120">The `remove` element removes authentication modules that were defined earlier in the configuration file or at a higher level in the configuration hierarchy.</span></span>  
  
 <span data-ttu-id="55c67-121">Il valore dell' `type` attributo deve essere un nome di classe valido.</span><span class="sxs-lookup"><span data-stu-id="55c67-121">The value for the `type` attribute should be a valid class name.</span></span>  
  
## <a name="configuration-files"></a><span data-ttu-id="55c67-122">File di configurazione</span><span class="sxs-lookup"><span data-stu-id="55c67-122">Configuration Files</span></span>  
 <span data-ttu-id="55c67-123">Questo elemento può essere usato nel file di configurazione dell'applicazione o nel file di configurazione del computer (Machine.config).</span><span class="sxs-lookup"><span data-stu-id="55c67-123">This element can be used in the application configuration file or the machine configuration file (Machine.config).</span></span>  
  
## <a name="example"></a><span data-ttu-id="55c67-124">Esempio</span><span class="sxs-lookup"><span data-stu-id="55c67-124">Example</span></span>  
 <span data-ttu-id="55c67-125">Nell'esempio seguente viene rimosso un modulo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="55c67-125">The following example removes an authentication module.</span></span>  
  
```xml  
<configuration>  
  <system.net>  
    <authenticationModules>  
      <remove type="System.Net.NtlmClient" />  
    </authenticationModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="55c67-126">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="55c67-126">See also</span></span>

- <xref:System.Net.IAuthenticationModule>
- <xref:System.Net.AuthenticationManager>
- [<span data-ttu-id="55c67-127">Schema delle impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="55c67-127">Network Settings Schema</span></span>](index.md)

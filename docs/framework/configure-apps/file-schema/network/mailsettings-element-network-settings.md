---
title: Elemento <mailSettings> (impostazioni di rete)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#mailSettings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings
helpviewer_keywords:
- mailSettings element
- <mailSettings> element
ms.assetid: 54f0f153-17e5-4f49-afdc-deadb940c9c1
ms.openlocfilehash: 4e8bf23ce39edadf80f019315c690b597b3d7361
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "74089225"
---
# <a name="mailsettings-element-network-settings"></a><span data-ttu-id="f7dbc-102">Elemento \<mailSettings> (impostazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="f7dbc-102">\<mailSettings> Element (Network Settings)</span></span>
<span data-ttu-id="f7dbc-103">Configura le opzioni di invio della posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="f7dbc-103">Configures mail sending options.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<mailSettings>**

## <a name="syntax"></a><span data-ttu-id="f7dbc-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="f7dbc-104">Syntax</span></span>  
  
```xml  
<mailSettings>
  <smtp>...</smtp>  
</mailSettings>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="f7dbc-105">Attributi ed elementi</span><span class="sxs-lookup"><span data-stu-id="f7dbc-105">Attributes and Elements</span></span>  
 <span data-ttu-id="f7dbc-106">Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="f7dbc-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="f7dbc-107">Attributi</span><span class="sxs-lookup"><span data-stu-id="f7dbc-107">Attributes</span></span>  
 <span data-ttu-id="f7dbc-108">No.</span><span class="sxs-lookup"><span data-stu-id="f7dbc-108">None.</span></span>  
  
### <a name="child-elements"></a><span data-ttu-id="f7dbc-109">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="f7dbc-109">Child Elements</span></span>  
  
|<span data-ttu-id="f7dbc-110">Attributo</span><span class="sxs-lookup"><span data-stu-id="f7dbc-110">Attribute</span></span>|<span data-ttu-id="f7dbc-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7dbc-111">Description</span></span>|  
|---------------|-----------------|  
|[<span data-ttu-id="f7dbc-112">\<smtp>Elemento (impostazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="f7dbc-112">\<smtp> Element (Network Settings)</span></span>](smtp-element-network-settings.md)|<span data-ttu-id="f7dbc-113">Configura le opzioni del protocollo di trasporto di posta elettronica semplice.</span><span class="sxs-lookup"><span data-stu-id="f7dbc-113">Configures Simple Mail Transport Protocol options.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="f7dbc-114">Elementi padre</span><span class="sxs-lookup"><span data-stu-id="f7dbc-114">Parent Elements</span></span>  
  
|<span data-ttu-id="f7dbc-115">**Elemento**</span><span class="sxs-lookup"><span data-stu-id="f7dbc-115">**Element**</span></span>|<span data-ttu-id="f7dbc-116">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="f7dbc-116">**Description**</span></span>|  
|-----------------|---------------------|  
|[<span data-ttu-id="f7dbc-117">\<system.Net>Elemento (impostazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="f7dbc-117">\<system.Net> Element (Network Settings)</span></span>](system-net-element-network-settings.md)|<span data-ttu-id="f7dbc-118">Contiene le impostazioni di rete che specificano la modalità di connessione alla rete di .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f7dbc-118">Contains settings that specify how the .NET Framework connects to the network.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="f7dbc-119">Esempio</span><span class="sxs-lookup"><span data-stu-id="f7dbc-119">Example</span></span>  
 <span data-ttu-id="f7dbc-120">Nell'esempio seguente vengono specificati i parametri SMTP appropriati per inviare messaggi di posta elettronica utilizzando le credenziali di rete predefinite.</span><span class="sxs-lookup"><span data-stu-id="f7dbc-120">The following example specifies the appropriate SMTP parameters to send email using the default network credentials.</span></span>  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="Network">  
        <network  
          host="localhost"  
          port="25"  
          defaultCredentials="true"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="f7dbc-121">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="f7dbc-121">See also</span></span>

- <xref:System.Net.Mail.SmtpClient>
- [<span data-ttu-id="f7dbc-122">Schema delle impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="f7dbc-122">Network Settings Schema</span></span>](index.md)

---
title: <security> di <basicHttpBinding>
ms.date: 03/30/2017
ms.assetid: 6432708d-5465-4bd9-bfc2-466742db99cb
ms.openlocfilehash: c8e4f2d000a155eecd2a6c7faaaf4af525b24ca3
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "73738711"
---
# <a name="security-of-basichttpbinding"></a>\<security> di \<basicHttpBinding>
Definisce le funzionalità di sicurezza di [\<basicHttpBinding>](basichttpbinding.md) .  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<basicHttpBinding>**](basichttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<security>**  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
<security mode="Message/None/Transport/TransportWithCredential">
  <transport clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"
             proxyCredentialType="Basic/Digest/None/Ntlm/Windows"
             realm="string" />
  <message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
           clientCredentialType="Certificate/IssuedToken/None/UserName/Windows" />
</security>
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti attributi, elementi figlio ed elementi padre.  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|mode|Facoltativa. Specifica il tipo di sicurezza usata. Il valore predefinito è `None`. L'attributo è di tipo <xref:System.ServiceModel.BasicHttpSecurityMode>.|  
  
## <a name="mode-attribute"></a>Attributo mode  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|nessuno|-I messaggi non vengono protetti durante il trasferimento.|  
|Trasporto|La sicurezza è fornita mediante il trasporto HTTPS. I messaggi SOAP vengono protetti utilizzando HTTPS. Il servizio viene autenticato sul client mediante il certificato X.509 del servizio. Il client viene autenticato mediante il ClientCredentialType  fornito. Vedere [\<transport>](transport-of-basichttpbinding.md) .|  
|Message|La sicurezza è fornita mediante la sicurezza dei messaggi SOAP. Per impostazione predefinita, il corpo viene crittografato e firmato. Per questa associazione, il sistema richiede che il certificato server sia fornito al client fuori banda. L'unico valore `ClientCredentialType` valido per questa associazione è `Certificate`.|  
|TransportWithMessageCredential|Integrità, riservatezza e autenticazione server sono fornite dalla sicurezza del trasporto. L'autenticazione del client è fornita per mezzo della sicurezza del messaggio SOAP. Questa modalità è appropriata quando l'utente esegue l'autenticazione usando nome utente/password in presenza di una distribuzione HTTP esistente per la sicurezza del trasferimento dei messaggi.|  
|TransportCredentialOnly|Questa modalità non fornisce l'integrità e la riservatezza dei messaggi, Fornisce autenticazione client basata su HTTP. Tale modalità deve essere usata con cautela. Deve essere utilizzato in ambienti in cui la sicurezza del trasporto viene fornita tramite altri mezzi (ad esempio IPSec) e l'infrastruttura WCF fornisce solo l'autenticazione client.|  
  
### <a name="child-elements"></a>Elementi figlio  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|[\<transport>](transport-of-basichttpbinding.md)|Definisce le impostazioni di sicurezza del trasporto per un servizio HTTP di base. L'elemento corrisponde a <xref:System.ServiceModel.HttpTransportSecurity>.|  
|[\<message>](message-of-basichttpbinding.md)|Definisce le impostazioni di sicurezza del messaggio per un servizio HTTP di base. L'elemento corrisponde a <xref:System.ServiceModel.BasicHttpMessageSecurity>.|  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|binding|Elemento di associazione di [\<basicHttpBinding>](basichttpbinding.md) .|  
  
## <a name="remarks"></a>Commenti  
 Per impostazione predefinita, il messaggio SOAP non è protetto e il client non viene autenticato. Questo elemento consente di configurare impostazioni di sicurezza aggiuntive per l'elemento `basicHttpBinding`.  
  
## <a name="see-also"></a>Vedi anche

- <xref:System.ServiceModel.BasicHttpBinding.Security%2A>
- <xref:System.ServiceModel.Configuration.BasicHttpBindingElement.Security%2A>
- <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement>
- <xref:System.ServiceModel.BasicHttpSecurity>
- [Securing Services and Clients](../../../wcf/feature-details/securing-services-and-clients.md)
- [Selezione di un tipo di credenziale](../../../wcf/feature-details/selecting-a-credential-type.md)
- [Binding](../../../wcf/bindings.md)
- [Configurazione di associazioni fornite dal sistema](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [Uso di associazioni per configurare servizi e client](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)

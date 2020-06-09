---
title: Debug degli errori di autenticazione di Windows
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, authentication
- WCF, Windows authentication
ms.assetid: 181be4bd-79b1-4a66-aee2-931887a6d7cc
ms.openlocfilehash: eb3274b98234324bd47aa456feb4845da5a7f3a9
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599282"
---
# <a name="debug-windows-authentication-errors"></a>Debug degli errori di autenticazione di Windows

Quando si utilizza l'autenticazione di Windows come meccanismo di sicurezza, i processi di sicurezza vengono gestiti dall'interfaccia SSPI (Security Support Provider Interface). Quando si verificano errori di sicurezza a livello di SSPI, vengono esposti da Windows Communication Foundation (WCF). In questo argomento viene fornito un framework e un insieme di domande per facilitare la diagnosi degli errori.  
  
 Per una panoramica del protocollo Kerberos, vedere la pagina relativa alla [spiegazione di Kerberos](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742516(v=technet.10)). per una panoramica di SSPI, vedere [SSPI](/windows/win32/secauthn/sspi).  
  
 Per l'autenticazione di Windows, WCF USA in genere *Negotiate* Security Support Provider (SSP), che esegue l'autenticazione reciproca Kerberos tra il client e il servizio. Se il protocollo Kerberos non è disponibile, per impostazione predefinita WCF esegue il fallback a NT LAN Manager (NTLM). Tuttavia, è possibile configurare WCF in modo che utilizzi solo il protocollo Kerberos (e per generare un'eccezione se Kerberos non è disponibile). È inoltre possibile configurare WCF per l'utilizzo di forme limitate del protocollo Kerberos.  
  
## <a name="debugging-methodology"></a>Metodologia di debug  
 Il metodo di base è il seguente:  
  
1. Determinare se si sta utilizzando l'autenticazione di Windows. Se si sta utilizzando qualsiasi altro schema, questo argomento non è applicabile.  
  
2. Se si è certi di utilizzare l'autenticazione di Windows, determinare se la configurazione WCF utilizza Kerberos Direct o Negotiate.  
  
3. Una volta determinato se la configurazione utilizza il protocollo Kerberos o NTLM, è possibile comprendere i messaggi di errore nel contesto giusto.  
  
### <a name="availability-of-the-kerberos-protocol-and-ntlm"></a>Disponibilità del protocollo Kerberos e NTLM  
 Per l'SSP Kerberos è necessario un controller di dominio che agisca da Centro di distribuzione chiave Kerberos (KDC, Kerberos Key Distribution Center). Il protocollo Kerberos è disponibile solo quando sia il client che il servizio utilizzano identità di dominio. In altre combinazioni di account, viene utilizzato il protocollo NTLM, come riepilogato nella tabella seguente.  
  
 Nelle intestazioni della tabella vengono riportati i possibili tipi di account utilizzati dal server, mentre nella colonna sinistra vengono indicati i possibili tipi di account utilizzati dal client.  
  
||Utente locale|Sistema locale|Utente del dominio|Computer del dominio|  
|-|----------------|------------------|-----------------|--------------------|  
|Utente locale|NTLM|NTLM|NTLM|NTLM|  
|Sistema locale|NTLM anonimo|NTLM anonimo|NTLM anonimo|NTLM anonimo|  
|Utente del dominio|NTLM|NTLM|Kerberos|Kerberos|  
|Computer del dominio|NTLM|NTLM|Kerberos|Kerberos|  
  
 In particolare, i quattro tipi di account includono:  
  
- Utente locale: profilo utente del computer. Ad esempio, `MachineName\Administrator` o `MachineName\ProfileName`.  
  
- Sistema locale: account predefinito SYSTEM in un computer non associato a un dominio.  
  
- Utente del dominio: account utente in un dominio Windows. Ad esempio: `DomainName\ProfileName`.  
  
- Computer del dominio: processo con identità di computer in esecuzione in un computer associato a un dominio Windows. Ad esempio: `MachineName\Network Service`.  
  
> [!NOTE]
> La credenziale del servizio viene acquisita quando viene chiamato il metodo <xref:System.ServiceModel.ICommunicationObject.Open%2A> della classe <xref:System.ServiceModel.ServiceHost>. La credenziale del client viene letta ogni volta che il client invia un messaggio.  
  
## <a name="common-windows-authentication-problems"></a>Problemi di autenticazione di Windows comuni  
 Contenuto della sezione vengono illustrati alcuni problemi di autenticazione di Windows comuni e le possibili soluzioni.  
  
### <a name="kerberos-protocol"></a>Protocollo Kerberos  
  
#### <a name="spnupn-problems-with-the-kerberos-protocol"></a>Problemi SPN/UPN con il protocollo Kerberos  
 Quando si utilizza l'autenticazione di Windows unitamente al protocollo Kerberos diretto o negoziato mediante SSPI, l'URL utilizzato dall'endpoint client deve includere il nome di dominio completo dell'host del servizio presente nell'URL del servizio. Questo presuppone che l'account utilizzato per l'esecuzione del servizio abbia accesso alla chiave del nome dell'entità servizio (SPN) del computer (impostazione predefinita) creata quando il computer viene aggiunto al dominio di Active Directory, generalmente eseguendo il servizio con l'account Servizio di rete. Se il servizio non ha accesso alla chiave dell'SPN del computer, è necessario fornire l'SPN corretto o il nome dell'entità utente (UPN) dell'account utilizzato per l'esecuzione del servizio nell'identità dell'endpoint del client. Per ulteriori informazioni sul funzionamento di WCF con SPN e UPN, vedere [identità e autenticazione del servizio](service-identity-and-authentication.md).  
  
 In scenari di bilanciamento del carico, ad esempio Web farm o Web garden, viene comunemente definito un account univoco per ogni applicazione, viene assegnato un SPN a tale account e viene verificato che tutti i servizi dell'applicazione siano eseguiti in tale account.  
  
 Per ottenere un SPN per l'account del servizio, è necessario essere amministratore di dominio di Active Directory. Per ulteriori informazioni, vedere la pagina relativa al [supplemento tecnico Kerberos per Windows](https://docs.microsoft.com/previous-versions/msp-n-p/ff649429(v=pandp.10)).  
  
#### <a name="kerberos-protocol-direct-requires-the-service-to-run-under-a-domain-machine-account"></a>Per il protocollo Kerberos diretto è necessario che il servizio venga eseguito utilizzando un account di tipo computer del dominio  
 Questo si verifica quando la proprietà `ClientCredentialType` è impostata su `Windows` e la proprietà <xref:System.ServiceModel.MessageSecurityOverHttp.NegotiateServiceCredential%2A> è impostata su `false`, come illustrato nel codice seguente.  
  
 [!code-csharp[C_DebuggingWindowsAuth#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#1)]
 [!code-vb[C_DebuggingWindowsAuth#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#1)]  
  
 Per risolvere questo problema, eseguire il servizio utilizzando un account di tipo computer del dominio, ad esempio Servizio di rete, in un computer associato al dominio.  
  
### <a name="delegation-requires-credential-negotiation"></a>Requisito di negoziazione della credenziale in caso di delega  
 Per poter essere utilizzato con la funzionalità di delega, il protocollo di autenticazione Kerberos deve essere implementato con la negoziazione della credenziale. Questa versione di Kerberos è nota come Kerberos multifase o multipassaggio. Se si implementa l'autenticazione Kerberos senza negoziazione della credenziale (ovvero una versione di Kerberos anche nota come "monofase" o "monopassaggio), verrà generata un'eccezione.  
  
 Per implementare Kerberos con negoziazione della credenziale, eseguire le operazioni seguenti:  
  
1. Implementare la delega impostando <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> su <xref:System.Security.Principal.TokenImpersonationLevel.Delegation>.  
  
2. Richiedere la negoziazione SSPI:  
  
    1. Se si utilizzano associazioni standard, impostare la proprietà `NegotiateServiceCredential` su `true`.  
  
    2. Se si utilizzano associazioni personalizzate, impostare l'attributo `AuthenticationMode` dell'elemento `Security` su `SspiNegotiated`.  
  
3. Richiedere che la negoziazione SSPI utilizzi Kerberos impedendo l'utilizzo di NTLM:  
  
    1. È possibile eseguire questa operazione nel codice utilizzando l'istruzione seguente: `ChannelFactory.Credentials.Windows.AllowNtlm = false`  
  
    2. In alternativa, è possibile operare nel file di configurazione impostando l'attributo `allowNtlm` su `false`. Questo attributo è contenuto nell'oggetto [\<windows>](../../configure-apps/file-schema/wcf/windows-of-clientcredentials-element.md) .  
  
### <a name="ntlm-protocol"></a>Protocollo NTLM  
  
#### <a name="negotiate-ssp-falls-back-to-ntlm-but-ntlm-is-disabled"></a>Il provider SSP Negotiate esegue il fallback a NTLM, ma NTLM è disabilitato  
 La <xref:System.ServiceModel.Security.WindowsClientCredential.AllowNtlm%2A> proprietà è impostata su `false` , che fa sì che Windows Communication Foundation (WCF) faccia un tentativo ottimale di generare un'eccezione se viene utilizzata l'autenticazione NTLM. L'impostazione di questa proprietà su `false` potrebbe non impedire l'invio di credenziali NTLM attraverso la rete.  
  
 Nel codice seguente viene illustrato come disabilitare il fallback a NTLM.  
  
 [!code-csharp[C_DebuggingWindowsAuth#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#4)]
 [!code-vb[C_DebuggingWindowsAuth#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#4)]  
  
#### <a name="ntlm-logon-fails"></a>Impossibile accedere a NTLM  
 Le credenziali client non sono valide per il servizio. Verificare che il nome utente e la password siano impostati correttamente e che corrispondano a un account noto al computer in cui viene eseguito il servizio. Per accedere al computer del servizio, NTLM utilizza le credenziali specificate. Anche se le credenziali possono essere valide nel computer in cui il client è in esecuzione, l'accesso non riuscirà se le credenziali non sono valide nel computer del servizio.  
  
#### <a name="anonymous-ntlm-logon-occurs-but-anonymous-logons-are-disabled-by-default"></a>Si verifica un accesso NTLM anonimo, ma gli accessi anonimi sono disabilitati per impostazione predefinita  
 Quando si crea un client, la proprietà <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> viene impostata su <xref:System.Security.Principal.TokenImpersonationLevel.Anonymous>, come illustrato nell'esempio seguente, ma per impostazione predefinita il server impedisce gli accessi anonimi. Tale situazione si verifica perché il valore predefinito della proprietà <xref:System.ServiceModel.Security.WindowsServiceCredential.AllowAnonymousLogons%2A> della classe <xref:System.ServiceModel.Security.WindowsServiceCredential> è `false`.  
  
 Nel codice client seguente viene tentata l'abilitazione degli accessi anonimi (si noti che la proprietà predefinita è `Identification`).  
  
 [!code-csharp[C_DebuggingWindowsAuth#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#5)]
 [!code-vb[C_DebuggingWindowsAuth#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#5)]  
  
 Nel codice del servizio seguente viene modificata l'impostazione predefinita per consentire gli accessi anonimi.  
  
 [!code-csharp[C_DebuggingWindowsAuth#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#6)]
 [!code-vb[C_DebuggingWindowsAuth#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#6)]  
  
 Per ulteriori informazioni sulla rappresentazione, vedere [delega e rappresentazione](delegation-and-impersonation-with-wcf.md).  
  
 In alternativa, il client viene eseguito come un servizio Windows, utilizzando l'account predefinito System.  
  
### <a name="other-problems"></a>Altri problemi  
  
#### <a name="client-credentials-are-not-set-correctly"></a>Le credenziali client non sono impostate correttamente  
 L'autenticazione di Windows utilizza l'istanza <xref:System.ServiceModel.Security.WindowsClientCredential> restituita dalla proprietà <xref:System.ServiceModel.ClientBase%601.ClientCredentials%2A> della classe <xref:System.ServiceModel.ClientBase%601>, non l'istanza <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>. Nel codice seguente viene illustrato un esempio non corretto.  
  
 [!code-csharp[C_DebuggingWindowsAuth#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#2)]
 [!code-vb[C_DebuggingWindowsAuth#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#2)]  
  
 Nel codice seguente viene illustrato l'esempio corretto.  
  
 [!code-csharp[C_DebuggingWindowsAuth#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_debuggingwindowsauth/cs/source.cs#3)]
 [!code-vb[C_DebuggingWindowsAuth#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_debuggingwindowsauth/vb/source.vb#3)]  
  
#### <a name="sspi-is-not-available"></a>L'interfaccia SSPI non è disponibile  
 I sistemi operativi seguenti non supportano l'autenticazione di Windows se utilizzati come server: Windows XP Home Edition, Windows XP Media Center Edition e Windows Vista Home Edition.  
  
#### <a name="developing-and-deploying-with-different-identities"></a>Sviluppo e distribuzione con identità diverse  
 Se l'applicazione viene sviluppata in un computer e distribuita in un altro e si utilizzano diversi tipi di account per l'autenticazione in ogni computer, potrebbe verificarsi un comportamento diverso. Si supponga, ad esempio, di sviluppare l'applicazione in un computer Windows XP Pro utilizzando la modalità di autenticazione `SSPI Negotiated`. Se si utilizza un account utente locale per l'autenticazione, verrà utilizzato il protocollo NTLM. Una volta sviluppata l'applicazione, il servizio viene distribuito in un computer Windows Server 2003 in cui è in esecuzione un account di dominio. A questo punto, il client non sarà in grado di autenticare il servizio perché utilizzerà Kerberos e un controller di dominio.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.ServiceModel.Security.WindowsClientCredential>
- <xref:System.ServiceModel.Security.WindowsServiceCredential>
- <xref:System.ServiceModel.Security.WindowsClientCredential>
- <xref:System.ServiceModel.ClientBase%601>
- [Delega e rappresentazione](delegation-and-impersonation-with-wcf.md)
- [Scenari non supportati](unsupported-scenarios.md)

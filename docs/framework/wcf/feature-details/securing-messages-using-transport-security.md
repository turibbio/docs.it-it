---
title: Protezione dei messaggi mediante protezione del trasporto
ms.date: 03/30/2017
ms.assetid: 9029771a-097e-448a-a13a-55d2878330b8
ms.openlocfilehash: 7d160f6f0d1d29e34ca3365501b86d1a736de67b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84589942"
---
# <a name="securing-messages-using-transport-security"></a>Protezione dei messaggi mediante protezione del trasporto
Contenuto della sezione viene descritta la protezione del trasporto di Accodamento messaggi (MSMQ), che è possibile utilizzare per proteggere messaggi inviati a una coda.  
  
> [!NOTE]
> Prima di leggere questo argomento, è consigliabile leggere i [concetti relativi alla sicurezza](security-concepts.md).  
  
 Nella figura seguente viene illustrato un modello concettuale della comunicazione in coda con Windows Communication Foundation (WCF). L'illustrazione e la terminologia vengono utilizzate per spiegare i concetti di sicurezza del trasporto.  
  
 ![Diagramma di applicazioni in coda](media/distributed-queue-figure.jpg "Distributed-Queue-Figure")  
  
 Quando si inviano messaggi in coda utilizzando WCF con <xref:System.ServiceModel.NetMsmqBinding> , il messaggio WCF viene allegato come corpo del messaggio MSMQ. La protezione del trasporto rende sicuro l'intero messaggio MSMQ: intestazioni o proprietà del messaggio MSMQ e corpo del messaggio. Poiché è il corpo del messaggio MSMQ, l'utilizzo della sicurezza del trasporto protegge anche il messaggio WCF.  
  
 Il concetto chiave della protezione del trasporto consiste nell'esigenza per il client di soddisfare requisiti di sicurezza per inviare il messaggio alla coda di destinazione, diversamente dalla protezione dei messaggi, in cui il messaggio viene protetto per l'applicazione che lo riceve.  
  
 La protezione del trasporto che utilizza <xref:System.ServiceModel.NetMsmqBinding> e <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> influenza il modo in cui i messaggi MSMQ sono protetti in transito tra la coda di trasmissione e la coda di destinazione, dove per protezione si intende:  
  
- Firma del messaggio per avere la certezza che non sia manomesso.  
  
- Crittografia del messaggio per avere la certezza che non venga visto o manomesso. Operazione consigliata ma facoltativa.  
  
- Il gestore delle code di destinazione che identifica il mittente del messaggio per non-ripudio.  
  
 In MSMQ, indipendentemente dall'autenticazione, la coda di destinazione dispone di un elenco di controllo di accesso (ACL) per verificare se il client dispone delle autorizzazioni per inviare il messaggio alla coda di destinazione. Viene inoltre verificato se l'applicazione ricevente è autorizzata a ricevere il messaggio dalla coda di destinazione.  
  
## <a name="wcf-msmq-transport-security-properties"></a>Proprietà della protezione del trasporto MSMQ WCF  
 In MSMQ viene utilizzata la protezione di Windows per l'autenticazione. Durante l'autenticazione del client vengono utilizzati l'ID di sicurezza di Windows (SID) per identificare il client e Active Directory come autorità di certificazione. È necessario che MSMQ sia installato con l'integrazione di Active Directory. Poiché il SID del dominio Windows viene utilizzato per identificare il client, questa opzione di sicurezza è significativa solo quando sia il client che servizio fanno parte dello stesso dominio Windows.  
  
 In MSMQ è inoltre disponibile la possibilità di allegare un certificato al messaggio non registrato con Active Directory. In questo caso, si garantisce che il messaggio è stato firmato utilizzando il certificato allegato.  
  
 In WCF sono disponibili entrambe le opzioni come parte della sicurezza del trasporto MSMQ, che rappresentano il perno chiave per la sicurezza del trasporto.  
  
 Per impostazione predefinita, la protezione del trasporto è attivata.  
  
 Sulla base di queste nozioni fondamentali, nelle sezioni seguenti vengono dettagliate le proprietà della protezione del trasporto incluse in <xref:System.ServiceModel.NetMsmqBinding> e in <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>.  
  
#### <a name="msmq-authentication-mode"></a>Modalità di autenticazione MSMQ  
 La proprietà <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> stabilisce se per proteggere il messaggio sia necessario utilizzare la protezione del dominio Windows o una protezione basata sui certificati esterna. In entrambe le modalità di autenticazione, il canale di trasporto in coda WCF utilizza l' `CertificateValidationMode` oggetto specificato nella configurazione del servizio. La modalità di convalida del certificato consente di specificare il meccanismo utilizzato per verificare la validità del certificato.  
  
 Quando la protezione del trasporto è attivata, l'impostazione predefinita è <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain>.  
  
#### <a name="windows-domain-authentication-mode"></a>Modalità di autenticazione del dominio Windows  
 La scelta di utilizzare la sicurezza di Windows comporta l'integrazione di Active Directory. <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain> è la modalità di sicurezza del trasporto predefinita. Quando questa proprietà è impostata, il canale WCF connette il SID di Windows al messaggio MSMQ e utilizza il certificato interno ottenuto da Active Directory. Questo certificato interno viene quindi utilizzato per proteggere il messaggio. Il gestore delle code di destinazione utilizza Active Directory per cercare e trovare un certificato corrispondente per autenticare il client e controlla inoltre che il SID corrisponda a quello del client. Questo passaggio di autenticazione viene eseguito se un certificato, generato internamente nel caso della modalità di autenticazione `WindowsDomain` o generato esternamente nel caso della modalità di autenticazione `Certificate`, è allegato al messaggio anche se la coda di destinazione non è contrassegnata per l'autenticazione.  
  
> [!NOTE]
> Durante la creazione di una coda, è possibile contrassegnare la coda come autenticata per indicare che richiede l'autenticazione del client che invia messaggi alla coda. In questo modo si ha la certezza che nessun messaggio non autenticato venga accettato nella coda.  
  
 Anche il SID allegato al messaggio viene utilizzato per eseguire un controllo a fronte dell'ACL della coda di destinazione per accertare se il client è autorizzato a inviare messaggi alla coda.  
  
#### <a name="certificate-authentication-mode"></a>Modalità di autenticazione con certificati  
 La scelta dell'utilizzo della modalità di autenticazione con certificati non richiede l'integrazione di Active Directory. In alcuni casi, infatti, ad esempio quando MSMQ è installato in modalità gruppo di lavoro (senza l'integrazione di Active Directory) o quando si utilizza il protocollo di trasferimento SRMP (SOAP Reliable Messaging Protocol) per inviare messaggi alla coda, solo <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate> funziona.  
  
 Quando si invia un messaggio WCF con <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate> , il canale WCF non associa un SID di Windows al messaggio MSMQ. In tal caso l'ACL della coda di destinazione deve consentire l'accesso utente `Anonymous` per l'invio alla coda. Il gestore delle code di destinazione controlla se il messaggio MSMQ è stato firmato con il certificato ma non esegue alcuna autenticazione.  
  
 Il certificato con le relative attestazioni e informazioni di identità viene popolato in <xref:System.ServiceModel.ServiceSecurityContext> dal canale di trasporto accodato WCF. Il servizio può utilizzare queste informazioni per eseguire la propria autenticazione del mittente.  
  
### <a name="msmq-protection-level"></a>Livello di protezione MSMQ  
 Il livello di protezione determina la modalità di sicurezza del messaggio MSMQ per avere la certezza che non venga manomesso. È specificato nella proprietà <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>. Il valore predefinito è <xref:System.Net.Security.ProtectionLevel.Sign>.  
  
#### <a name="sign-protection-level"></a>Livello di protezione con firma  
 Il messaggio MSMQ viene firmato utilizzando il certificato generato internamente quando si utilizza la modalità di autenticazione `WindowsDomain` o un certificato generato esternamente nel caso della modalità di autenticazione `Certificate`.  
  
#### <a name="sign-and-encrypt-protection-level"></a>Livello di protezione con firma e crittografia  
 Il messaggio MSMQ viene firmato utilizzando il certificato generato internamente quando si utilizza la modalità di autenticazione `WindowsDomain` o un certificato generato esternamente nel caso della modalità di autenticazione `Certificate`.  
  
 Oltre a essere firmato, il messaggio MSMQ viene crittografato mediante la chiave pubblica del certificato ottenuta da Active Directory appartenente al gestore delle code di destinazione in cui risiede la coda di destinazione. Il gestore delle code di origine garantisce che il messaggio MSMQ è crittografato in transito. Il gestore delle code di destinazione gestione esegue la decrittografia del messaggio MSMQ mediante la chiave privata del certificato interno e archivia il messaggio nella coda (se autenticato e autorizzato) in testo non crittografato.  
  
> [!NOTE]
> Per crittografare il messaggio è necessario l'accesso ad Active Directory (la proprietà`UseActiveDirectory` di <xref:System.ServiceModel.NetMsmqBinding> deve essere impostata su `true`) che può essere utilizzato con <xref:System.ServiceModel.MsmqAuthenticationMode.Certificate> e <xref:System.ServiceModel.MsmqAuthenticationMode.WindowsDomain>.  
  
#### <a name="none-protection-level"></a>Nessun livello di protezione  
 È implicita l'assenza di protezione quando la proprietà <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> è impostata su <xref:System.Net.Security.ProtectionLevel.None>. Non può trattarsi di un valore valido per qualsiasi altra modalità di autenticazione.  
  
> [!NOTE]
> Se il messaggio MSMQ è firmato, MSMQ controlla se è firmato con il certificato allegato (interno o esterno) indipendentemente dallo stato della coda, ovvero se autenticata o no.  
  
### <a name="msmq-encryption-algorithm"></a>Algoritmo di crittografia MSMQ  
 L'algoritmo di crittografia consente di specificare l'algoritmo da utilizzare per crittografare il messaggio MSMQ in transito. Questa proprietà viene utilizzata solo se la proprietà <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> è impostata su <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>.  
  
 Gli algoritmi supportati sono `RC4Stream` e `AES` e il valore predefinito è `RC4Stream`.  
  
 È possibile utilizzare l'algoritmo `AES` solo se nel mittente è installato MSMQ 4.0. La coda di destinazione, inoltre, deve essere ospitata su MSMQ 4.0.  
  
### <a name="msmq-hash-algorithm"></a>Algoritmo hash MSMQ  
 L'algoritmo hash consente di specificare l'algoritmo utilizzato per creare una firma digitale del messaggio MSMQ. Il gestore delle code di destinazione utilizza questo stesso algoritmo per autenticare il messaggio MSMQ. Questa proprietà viene utilizzata solo se l'oggetto <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> è impostato su <xref:System.Net.Security.ProtectionLevel.Sign> o <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>.  
  
 Gli algoritmi supportati sono `MD5`, `SHA1`, `SHA256` e `SHA512`. Il valore predefinito è `SHA1`.

 A causa di problemi di collisione con MD5/SHA1, Microsoft consiglia di SHA256 o meglio.
  
## <a name="see-also"></a>Vedere anche

- [Panoramica delle code](queues-overview.md)
- [Concetti relativi alla sicurezza](security-concepts.md)
- [Securing Services and Clients](securing-services-and-clients.md)

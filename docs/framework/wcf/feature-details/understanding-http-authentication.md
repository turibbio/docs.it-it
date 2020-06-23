---
title: Informazioni sull'autenticazione HTTP
description: Esaminare questa introduzione all'autenticazione HTTP in WCF, inclusi gli schemi di autenticazione HTTP e la scelta di uno schema di autenticazione.
ms.date: 03/30/2017
ms.assetid: 9376309a-39e3-4819-b47b-a73982b57620
ms.openlocfilehash: 761ab7a92aa26ce1437eefa360e5b46df179e32d
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246519"
---
# <a name="understanding-http-authentication"></a>Informazioni sull'autenticazione HTTP
L'autenticazione è il processo che consente di stabilire se un client è idoneo per accedere a una risorsa. Il protocollo HTTP supporta l'autenticazione come mezzo per negoziare l'accesso a una risorsa protetta.  
  
 La richiesta iniziale proveniente da un client è in genere una richiesta anonima, non contenente alcuna informazione di autenticazione. Le applicazioni server HTTP possono negare la richiesta anonima continuando a indicare che l'autenticazione è obbligatoria. L'applicazione server invia intestazioni WWW-Authenticate per indicare gli schemi di autenticazione supportati. In questo documento vengono descritti diversi schemi di autenticazione per HTTP e viene illustrato il relativo supporto in Windows Communication Foundation (WCF).  
  
## <a name="http-authentication-schemes"></a>Schemi di autenticazione HTTP  
 Il server può specificare vari schemi di autenticazione tra i quali il client ha la possibilità di scegliere. Nella tabella seguente vengono illustrati alcuni degli schemi di autenticazione più frequenti nelle applicazioni Windows.  
  
|Schema di autenticazione|Descrizione|  
|---------------------------|-----------------|  
|Anonima|Una richiesta anonima non contiene informazioni di autenticazione. Equivale a concedere l'accesso alla risorsa a qualsiasi richiedente.|  
|Basic|L'autenticazione di base invia una stringa con codifica Base64 contenente un nome utente e una password per il client. Base64 non è una forma di crittografia e deve essere considerata equivalente a inviare nome utente e password in testo non crittografato. Se è necessario proteggere una risorsa, è consigliabile prendere in considerazione uno schema di autenticazione diverso dall'autenticazione di base.|  
|Digest|L'autenticazione digest è uno schema In attesa/Risposta che sostituisce l'autenticazione di base. Il server invia una stringa di dati casuali denominata *nonce* al client come una sfida. Il client risponde con un hash che comprende, fra le altre informazioni, nome utente, password e parametro nonce. La complessità introdotta da questo scambio e l'hash dei dati fanno sì che con questo schema di autenticazione sia più difficile entrare in possesso delle credenziali dell'utente per riutilizzarle.<br /><br /> L'autenticazione digest richiede l'utilizzo di account del dominio Windows. L' *area di autenticazione* del digest è il nome di dominio di Windows. Pertanto, non è possibile utilizzare un server in esecuzione in un sistema operativo che non supporta domini Windows, ad esempio Windows XP Home Edition, con l'autenticazione digest. Quando invece il client è in esecuzione in un sistema operativo che non supporta domini Windows, è necessario specificare in modo esplicito un account di dominio durante l'autenticazione.|  
|NTLM|L'autenticazione NTLM (NT LAN Manager) è uno schema In attesa/Risposta che si presenta come una variante più protetta dell'autenticazione digest. Nello schema NTLM vengono utilizzate le credenziali di Windows, anziché nome utente e password non codificati, per trasformare i dati della richiesta. L'autenticazione NTLM richiede più scambi tra client e server. Il server e gli eventuali proxy devono supportare connessioni permanenti per completare correttamente l'autenticazione.|  
|Negotiate|L'autenticazione Negotiate sceglie automaticamente tra protocollo Kerberos e autenticazione NTLM a seconda della disponibilità. Il protocollo Kerberos viene utilizzato se disponibile, in caso contrario viene scelta l'autenticazione NTLM. L'autenticazione Kerberos è significativamente migliore di NTLM. È più veloce e consente l'utilizzo reciproco dell'autenticazione e della delega di credenziali ai computer remoti.|  
|Windows Live ID|Il servizio HTTP Windows sottostante comprende l'autenticazione realizzata con protocolli federati. Tuttavia, i trasporti HTTP standard in WCF non supportano l'utilizzo di schemi di autenticazione federati, ad esempio Microsoft Windows Live ID. Il supporto di questa funzionalità è attualmente disponibile mediante l'utilizzo della protezione dei messaggi. Per altre informazioni, vedere [Federazione e token emessi](federation-and-issued-tokens.md).|  
  
## <a name="choosing-an-authentication-scheme"></a>Scelta di uno schema di autenticazione  
 Quando si scelgono i potenziali schemi di autenticazione per un server HTTP, è necessario prendere in considerazione alcuni elementi:  
  
- Decidere se è necessario proteggere la risorsa. L'utilizzo dell'autenticazione HTTP implica la trasmissione di più dati e può limitare l'interoperabilità con i client. Consentire l'accesso anonimo alle risorse per le quali la protezione non è necessaria.  
  
- Se la protezione è necessaria per la risorsa, individuare lo schema di autenticazione che fornisce il livello di sicurezza opportuno. Lo schema di autenticazione standard più debole descritto in questo argomento è l'autenticazione di base, che non protegge le credenziali dell'utente. Lo schema di autenticazione standard più forte è Negotiate, che comporta il protocollo Kerberos.  
  
- Un server non deve presentare (nelle intestazioni WWW-Authenticate) schemi che non sono in grado di accettare o che non proteggono adeguatamente la risorsa in questione. I client hanno la possibilità di scegliere uno qualsiasi degli schemi di autenticazione presentati dal server. Alcuni client scelgono per impostazione predefinita uno schema di autenticazione debole o il primo schema di autenticazione nell'elenco del server.  
  
## <a name="see-also"></a>Vedere anche

- [Panoramica sulla sicurezza del trasporto](transport-security-overview.md)
- [Utilizzo della rappresentazione con la sicurezza del trasporto](using-impersonation-with-transport-security.md)
- [Delega e rappresentazione](delegation-and-impersonation-with-wcf.md)

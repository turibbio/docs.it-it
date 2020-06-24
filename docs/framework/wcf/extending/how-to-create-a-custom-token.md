---
title: 'Procedura: creare un token personalizzato'
description: Informazioni su come creare un token di sicurezza personalizzato in WCF usando la classe SecurityToken e su come integrarlo con un provider di token di sicurezza e un autenticatore.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SecurityTokenParameters class
- security [WCF], creating custom tokens
- WSSecurityTokenSerializer class
- SecurityToken class
ms.assetid: 6d892973-1558-4115-a9e1-696777776125
ms.openlocfilehash: a95d663c2669186fcb3eb1fb2f0c426ade945f1c
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247533"
---
# <a name="how-to-create-a-custom-token"></a>Procedura: creare un token personalizzato
Questo argomento illustra come creare un token di sicurezza personalizzato utilizzando la classe <xref:System.IdentityModel.Tokens.SecurityToken> e come integrarlo in un provider e un autenticatore di token di sicurezza personalizzati. Per un esempio di codice completo, vedere l'esempio di [token personalizzato](../samples/custom-token.md) .  
  
 Un *token di sicurezza* è essenzialmente un elemento XML utilizzato dal framework di sicurezza Windows Communication Foundation (WCF) per rappresentare le attestazioni relative a un mittente nel messaggio SOAP. La sicurezza WCF fornisce vari token per le modalità di autenticazione fornite dal sistema. Alcuni esempi sono il token di sicurezza basato su certificato X.509 rappresentato dalla classe <xref:System.IdentityModel.Tokens.X509SecurityToken> o il token di sicurezza del nome utente rappresentato dalla classe <xref:System.IdentityModel.Tokens.UserNameSecurityToken>.  
  
 Talvolta una determinata modalità di autenticazione o credenziale non è supportata dai tipi di token disponibili. In tal caso è necessario creare un token di sicurezza personalizzato per fornire una rappresentazione XML della credenziale personalizzata nel messaggio SOAP.  
  
 Nelle procedure riportate di seguito viene illustrato come creare un token di sicurezza personalizzato e come integrarlo con l'infrastruttura di sicurezza di WCF. In particolare, questo argomento illustra la creazione di un token di carta di credito utilizzato per passare al server le informazioni della carta di credito del client.  
  
 Per ulteriori informazioni sulle credenziali personalizzate e sul gestore del token di sicurezza, vedere [procedura dettagliata: creazione di credenziali client e del servizio personalizzate](walkthrough-creating-custom-client-and-service-credentials.md).  
  
 Per un elenco di altre classi utilizzate per rappresentare token di sicurezza, vedere lo spazio dei nomi <xref:System.IdentityModel.Tokens>.  
  
## <a name="procedures"></a>Procedure  
 È necessario fornire a un'applicazione client un modo per specificare le informazioni sulla carta di credito per l'infrastruttura di sicurezza. Per consentire all'applicazione di specificare queste informazioni viene utilizzata una classe di credenziali client personalizzata. Il primo passaggio consiste nel creare una classe che rappresenta le informazioni di carta di credito come credenziali client personalizzate.  
  
#### <a name="to-create-a-class-that-represents-credit-card-information-inside-client-credentials"></a>Per creare una classe che rappresenta informazioni di carta di credito come credenziali client  
  
1. Definire una nuova classe che rappresenta le informazioni di carta di credito dell'applicazione. Nell'esempio seguente tale classe viene denominata `CreditCardInfo`.  
  
2. Aggiungere alla classe le proprietà appropriate per consentire a un'applicazione di impostare le informazioni necessarie per il token personalizzato. In questo esempio la classe presenta tre proprietà: `CardNumber`, `CardIssuer` e `ExpirationDate`.  
  
     [!code-csharp[c_CustomToken#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#4)]
     [!code-vb[c_CustomToken#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#4)]  
  
 È quindi necessario creare una classe che rappresenti il token di sicurezza personalizzato. Questa classe viene utilizzata dalle classi del provider di token di sicurezza, dell'autenticatore e del serializzatore per passare informazioni sul token di sicurezza da e verso l'infrastruttura di sicurezza di WCF.  
  
#### <a name="to-create-a-custom-security-token-class"></a>Per creare una classe di token di sicurezza personalizzato  
  
1. Definire una nuova classe derivata dalla classe <xref:System.IdentityModel.Tokens.SecurityToken>. In questo esempio viene creata una classe denominata `CreditCardToken`.  
  
2. Eseguire l'override della proprietà <xref:System.IdentityModel.Tokens.SecurityToken.Id%2A>. Questa proprietà viene utilizzata per ottenere l'identificatore locale del token di sicurezza utilizzato dagli altri elementi contenuti nel messaggio SOAP per puntare alla rappresentazione XML del token di sicurezza. In questo esempio è possibile passare ad esso un identificatore del token come un parametro di costruttore oppure generarne uno casuale ogni volta che viene creata un'istanza del token di sicurezza.  
  
3. Implementare la proprietà <xref:System.IdentityModel.Tokens.SecurityToken.SecurityKeys%2A>. Questa proprietà restituisce una raccolta di chiavi di sicurezza rappresentate dall'istanza del token di sicurezza. Tali chiavi possono essere utilizzate da WCF per firmare o crittografare parti del messaggio SOAP. In questo esempio, il token di sicurezza della carta di credito non può contenere chiavi di sicurezza. Pertanto, l'implementazione restituisce sempre una raccolta vuota.  
  
4. Eseguire l'override delle proprietà <xref:System.IdentityModel.Tokens.SecurityToken.ValidFrom%2A> e <xref:System.IdentityModel.Tokens.SecurityToken.ValidTo%2A>. Queste proprietà vengono utilizzate da WCF per determinare la validità dell'istanza del token di sicurezza. In questo esempio, il token di sicurezza della carta di credito presenta solo una data di scadenza ("ValidTo"), pertanto la proprietà `ValidFrom` restituisce un oggetto <xref:System.DateTime> che rappresenta la data e l'ora di creazione dell'istanza.  
  
     [!code-csharp[c_CustomToken#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#1)]
     [!code-vb[c_CustomToken#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#1)]  
  
 Quando si crea un nuovo tipo di token di sicurezza è necessario implementare per tale tipo la classe <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters>. Questa implementazione viene utilizzata nella configurazione dell'elemento di associazione di sicurezza per rappresentare il nuovo tipo di token. La classe dei parametri del token di sicurezza rappresenta il modello rispetto a cui confrontare l'istanza effettiva del token di sicurezza quando viene elaborato un messaggio. Nel modello vengono fornite proprietà aggiuntive che un'applicazione può utilizzare per specificare i criteri che il token di sicurezza deve soddisfare per essere utilizzato o autenticato. Nell'esempio seguente non vengono aggiunte proprietà aggiuntive, pertanto viene eseguita una corrispondenza solo per il tipo di token di sicurezza quando l'infrastruttura WCF cerca un'istanza del token di sicurezza da utilizzare o per convalidare.  
  
#### <a name="to-create-a-custom-security-token-parameters-class"></a>Per creare una classe di parametri del token di sicurezza personalizzato  
  
1. Definire una nuova classe derivata dalla classe <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters>.  
  
2. Implementare il metodo <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.CloneCore%2A>. Copiare tutti i campi interni definiti nella classe, se presenti. In questo esempio non viene definito alcun campo aggiuntivo.  
  
3. Implementare la proprietà di sola lettura <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.SupportsClientAuthentication%2A>. Questa proprietà restituisce `true` se il tipo di token di sicurezza rappresentato da questa classe può essere utilizzato per autenticare un client presso un servizio. In questo esempio, il token di sicurezza della carta di credito può essere utilizzato a tale scopo.  
  
4. Implementare la proprietà di sola lettura <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.SupportsServerAuthentication%2A>. Questa proprietà restituisce `true` se il tipo di token di sicurezza rappresentato da questa classe può essere utilizzato per autenticare un servizio presso un client. In questo esempio, il token di sicurezza della carta di credito non può essere utilizzato a tale scopo.  
  
5. Implementare la proprietà di sola lettura <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.SupportsClientWindowsIdentity%2A>. Questa proprietà restituisce `true` se il tipo di token di sicurezza rappresentato da questa classe può essere associato a un account Windows. In questo caso, il risultato dell'autenticazione è rappresentato da un'istanza della classe <xref:System.Security.Principal.WindowsIdentity>. In questo esempio, il token non può essere associato a un account Windows.  
  
6. Implementare il metodo <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.CreateKeyIdentifierClause%28System.IdentityModel.Tokens.SecurityToken%2CSystem.ServiceModel.Security.Tokens.SecurityTokenReferenceStyle%29>. Questo metodo viene chiamato dal framework di sicurezza WCF quando richiede un riferimento all'istanza del token di sicurezza rappresentata da questa classe di parametri del token di sicurezza. Sia l'istanza del token di sicurezza effettivo sia lo stile <xref:System.ServiceModel.Security.Tokens.SecurityTokenReferenceStyle> che specifica il tipo del riferimento richiesto vengono passati a questo metodo come argomenti. In questo esempio, il token di sicurezza della carta di credito supporta soltanto riferimenti interni. Poiché la classe <xref:System.IdentityModel.Tokens.SecurityToken> offre funzionalità in grado di creare riferimenti interni, l'implementazione non richiede codice aggiuntivo.  
  
7. Implementare il metodo <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters.InitializeSecurityTokenRequirement%28System.IdentityModel.Selectors.SecurityTokenRequirement%29>. Questo metodo viene chiamato da WCF per convertire l'istanza della classe dei parametri del token di sicurezza in un'istanza della <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> classe. Il risultato della conversione viene utilizzato dai provider di token di sicurezza per creare l'istanza appropriata del token di sicurezza.  
  
     [!code-csharp[c_CustomToken#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#2)]
     [!code-vb[c_CustomToken#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#2)]  
  
 I token di sicurezza vengono trasmessi all'interno di messaggi SOAP. Ciò richiede un meccanismo di conversione fra la rappresentazione dei token di sicurezza in memoria e la rappresentazione dei token di sicurezza trasmessi. Per eseguire questa attività, WCF utilizza un serializzatore di token di sicurezza. A ogni token personalizzato è necessario associare un serializzatore di token di sicurezza personalizzato in grado di serializzare il token di sicurezza personalizzato nel messaggio SOAP nonché di eseguire l'operazione inversa.  
  
> [!NOTE]
> Le chiavi derivate sono attivate per impostazione predefinita. Se si crea un token di sicurezza personalizzato e lo si usa come token primario, WCF ne deriva una chiave. Durante questa operazione, viene chiamato il serializzatore del token di sicurezza per scrivere <xref:System.IdentityModel.Tokens.SecurityKeyIdentifierClause> per il token di sicurezza personalizzato durante la serializzazione di `DerivedKeyToken` in rete. Sul lato ricevente, durante la deserializzazione del token all'esterno della rete, il serializzatore `DerivedKeyToken` prevede sotto di sé un elemento `SecurityTokenReference` come elemento figlio di livello superiore. Se il serializzatore del token di sicurezza personalizzato non ha aggiunto un elemento `SecurityTokenReference` durante la serializzazione del relativo tipo di clausola, viene generata un'eccezione.  
  
#### <a name="to-create-a-custom-security-token-serializer"></a>Per creare un serializzatore di token di sicurezza personalizzato  
  
1. Definire una nuova classe derivata dalla classe <xref:System.ServiceModel.Security.WSSecurityTokenSerializer>.  
  
2. Eseguire l'override del metodo <xref:System.ServiceModel.Security.WSSecurityTokenSerializer.CanReadTokenCore%28System.Xml.XmlReader%29> che si basa su un oggetto <xref:System.Xml.XmlReader> per leggere il flusso XML. Il metodo restituisce `true` se l'implementazione del serializzatore può deserializzare il token di sicurezza in base all'elemento corrente del lettore. In questo esempio, il metodo verifica se il nome e lo spazio dei nomi dell'elemento XML corrente del lettore XML sono corretti. In caso contrario, viene chiamata l'implementazione della classe base di questo metodo per la gestione dell'elemento XML.  
  
3. Eseguire l'override del metodo <xref:System.ServiceModel.Security.WSSecurityTokenSerializer.ReadTokenCore%28System.Xml.XmlReader%2CSystem.IdentityModel.Selectors.SecurityTokenResolver%29> . Tramite questo metodo viene letto il contenuto XML del token di sicurezza e viene creata la rappresentazione in memoria appropriata di tale token. Se non riconosce l'elemento XML correntemente esaminato dal lettore XML specificato, tale metodo chiama l'implementazione della classe di base per elaborare i tipi di token forniti dal sistema.  
  
4. Eseguire l'override del metodo <xref:System.ServiceModel.Security.WSSecurityTokenSerializer.CanWriteTokenCore%28System.IdentityModel.Tokens.SecurityToken%29> . Questo metodo restituisce `true` se può convertire la rappresentazione in memoria del token (passata come argomento) nella rappresentazione XML. In caso contrario, tale metodo chiama l'implementazione della classe di base.  
  
5. Eseguire l'override del metodo <xref:System.ServiceModel.Security.WSSecurityTokenSerializer.WriteTokenCore%28System.Xml.XmlWriter%2CSystem.IdentityModel.Tokens.SecurityToken%29> . Questo metodo converte una rappresentazione in memoria del token di sicurezza in una rappresentazione XML. Qualora questa conversione risultasse impossibile, tale metodo chiama l'implementazione della classe di base.  
  
     [!code-csharp[c_CustomToken#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#3)]
     [!code-vb[c_CustomToken#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#3)]  
  
 Dopo aver completato le quattro procedure precedenti, integrare il token di sicurezza personalizzato nel provider, nell'autenticatore e nel gestore di token di sicurezza nonché nelle credenziali client e server.  
  
#### <a name="to-integrate-the-custom-security-token-with-a-security-token-provider"></a>Per integrare il token di sicurezza personalizzato in un provider di token di sicurezza  
  
1. Il provider del token di sicurezza crea, modifica (se necessario) e restituisce un'istanza del token. Per creare un provider personalizzato per il token di sicurezza personalizzato, creare una classe che eredita dalla classe <xref:System.IdentityModel.Selectors.SecurityTokenProvider>. Nell'esempio seguente viene eseguito l'override del metodo<xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%2A> per restituire un'istanza del token `CreditCardToken`. Per ulteriori informazioni sui provider di token di sicurezza personalizzati, vedere [procedura: creare un provider di token di sicurezza personalizzato](how-to-create-a-custom-security-token-provider.md).  
  
     [!code-csharp[c_CustomToken#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#6)]
     [!code-vb[c_CustomToken#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#6)]  
  
#### <a name="to-integrate-the-custom-security-token-with-a-security-token-authenticator"></a>Per integrare il token di sicurezza personalizzato in un autenticatore del token di sicurezza  
  
1. L'autenticatore del token di sicurezza convalida il contenuto del token di sicurezza quando quest'ultimo viene estratto dal messaggio. Per creare un autenticatore personalizzato per il token di sicurezza personalizzato, creare una classe che eredita dalla classe <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator>. Nell'esempio seguente il metodo <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator.ValidateTokenCore%2A> viene sottoposto a override. Per ulteriori informazioni sugli autenticatori del token di sicurezza personalizzati, vedere [procedura: creare un autenticatore del token di sicurezza personalizzato](how-to-create-a-custom-security-token-authenticator.md).  
  
     [!code-csharp[c_CustomToken#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#7)]
     [!code-vb[c_CustomToken#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#7)]  
  
     [!code-csharp[c_CustomToken#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#12)]
     [!code-vb[c_CustomToken#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#12)]  
  
#### <a name="to-integrate-the-custom-security-token-with-a-security-token-manager"></a>Per integrare il token di sicurezza personalizzato in un gestore del token di sicurezza  
  
1. Il gestore del token di sicurezza crea le istanze del provider di token, dell'autenticatore di sicurezza e del serializzatore di token appropriati. Per creare un gestore del token personalizzato, creare una classe che eredita dalla classe <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager>. I metodi primari della classe utilizzano un oggetto <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> per creare le credenziali appropriate per il provider e il client o il servizio. Per ulteriori informazioni sui gestori dei token di sicurezza personalizzati, vedere [procedura dettagliata: creazione di credenziali client e del servizio personalizzate](walkthrough-creating-custom-client-and-service-credentials.md).  
  
     [!code-csharp[c_CustomToken#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#8)]
     [!code-vb[c_CustomToken#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#8)]  
  
     [!code-csharp[c_CustomToken#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#9)]
     [!code-vb[c_CustomToken#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#9)]  
  
#### <a name="to-integrate-the-custom-security-token-with-custom-client-and-service-credentials"></a>Per integrare il token di sicurezza personalizzato in credenziali client e server personalizzate  
  
1. È necessario aggiungere le credenziali del client e del servizio personalizzate per fornire un'API che consenta all'applicazione di specificare informazioni sul token personalizzato che l'infrastruttura dei token di sicurezza personalizzati creata in precedenza utilizza per fornire e autenticare il contenuto del token di sicurezza personalizzato. Negli esempi seguenti viene illustrato come effettuare questa operazione. Per ulteriori informazioni sulle credenziali client e del servizio personalizzate, vedere [procedura dettagliata: creazione di credenziali client e del servizio personalizzate](walkthrough-creating-custom-client-and-service-credentials.md).  
  
     [!code-csharp[c_CustomToken#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#10)]
     [!code-vb[c_CustomToken#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#10)]  
  
     [!code-csharp[c_customToken#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#11)]
     [!code-vb[c_customToken#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#11)]  
  
 La classe dei parametri del token di sicurezza personalizzata creata in precedenza viene utilizzata per indicare al Framework di sicurezza WCF che è necessario utilizzare un token di sicurezza personalizzato durante la comunicazione con un servizio. La procedura seguente illustra come eseguire questa operazione.  
  
#### <a name="to-integrate-the-custom-security-token-with-the-binding"></a>Per integrare il token di sicurezza personalizzato nell'associazione  
  
1. La classe dei parametri del token di sicurezza personalizzato deve essere specificata in una delle raccolte di parametri di token esposte nella classe <xref:System.ServiceModel.Channels.SecurityBindingElement>. Nell'esempio seguente viene utilizzata la raccolta restituita dall'elemento `SignedEncrypted`. Dopo aver crittografato e firmato automaticamente il contenuto del token personalizzato della carta di credito, il codice aggiunge quest'ultimo a ogni messaggio inviato dal client al servizio.  
  
     [!code-csharp[c_CustomToken#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtoken/cs/source.cs#13)]
     [!code-vb[c_CustomToken#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtoken/vb/source.vb#13)]  
  
 In questo argomento vengono illustrate le varie parti di codice necessarie per implementare e utilizzare un token personalizzato. Per vedere un esempio completo del modo in cui tutti questi elementi di codice si adattano, vedere [token personalizzato](../samples/custom-token.md).  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.IdentityModel.Tokens.SecurityToken>
- <xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters>
- <xref:System.ServiceModel.Security.WSSecurityTokenSerializer>
- <xref:System.IdentityModel.Selectors.SecurityTokenProvider>
- <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator>
- <xref:System.IdentityModel.Policy.IAuthorizationPolicy>
- <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>
- <xref:System.IdentityModel.Selectors.SecurityTokenManager>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ServiceCredentials>
- <xref:System.ServiceModel.Channels.SecurityBindingElement>
- [Procedura dettagliata: creazione di credenziali client e del servizio personalizzate](walkthrough-creating-custom-client-and-service-credentials.md)
- [Procedura: Creare un autenticatore del token di sicurezza personalizzato](how-to-create-a-custom-security-token-authenticator.md)
- [Procedura: creare un provider di token di sicurezza personalizzati](how-to-create-a-custom-security-token-provider.md)

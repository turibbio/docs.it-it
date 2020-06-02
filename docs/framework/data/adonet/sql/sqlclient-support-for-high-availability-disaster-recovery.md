---
title: Supporto SqlClient per disponibilità elevata, ripristino di emergenza
description: Informazioni sul supporto dell'applicazione SqlClient per il ripristino di emergenza a disponibilità elevata in SQL Server, usando Gruppi di disponibilità AlwaysOn.
ms.date: 03/30/2017
ms.assetid: 61e0b396-09d7-4e13-9711-7dcbcbd103a0
ms.openlocfilehash: eba243d37db8262970d161cfa786d3aee4462950
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286210"
---
# <a name="sqlclient-support-for-high-availability-disaster-recovery"></a>Supporto SqlClient per disponibilità elevata, ripristino di emergenza
In questo argomento viene illustrato il supporto di SqlClient (aggiunto in .NET Framework 4,5) per il ripristino di emergenza a disponibilità elevata, Gruppi di disponibilità AlwaysOn.  La funzionalità dei gruppi di disponibilità AlwaysOn è stata aggiunta in SQL Server 2012. Per altre informazioni sui gruppi di disponibilità AlwaysOn, vedere la documentazione online di SQL Server.  
  
 È ora possibile specificare il listener di un gruppo di disponibilità (AG) (disponibilità elevata, ripristino di emergenza) o l'istanza del cluster di failover di SQL Server 2012 nella proprietà di connessione. Se un'applicazione SqlClient è connessa a un database AlwaysOn che esegue il failover, dopo il failover la connessione originale viene interrotta e l'applicazione deve aprire una nuova connessione per proseguire con l'esecuzione.  
  
 Se non si stabilisce la connessione a un listener del gruppo di disponibilità o all'istanza del cluster di failover di SQL Server 2012 e se sono associati più indirizzi IP a un nome host, SqlClient scorrerà in sequenza tutti gli indirizzi IP associati alla voce DNS. Questa operazione può richiedere tempi lunghi se il primo indirizzo IP restituito dal server DNS non è associato ad alcuna scheda di interfaccia di rete. Quando si stabilisce la connessione a un listener del gruppo di disponibilità o all'istanza del cluster di failover di SQL Server 2012, SqlClient tenta di connettersi a tutti gli indirizzi IP in parallelo e se un tentativo di connessione riesce, il driver rimuove tutti i tentativi di connessione in sospeso.  
  
> [!NOTE]
> L'aumento del timeout di connessione e l'implementazione della logica di riesecuzione per le connessioni aumentano le probabilità che un'applicazione si connetta a un gruppo di disponibilità. Inoltre, poiché potrebbe non essere possibile stabilire una connessione a causa del failover, è opportuno implementare la logica di riesecuzione delle connessioni, per ripetere i tentativi finché non si ottiene la riconnessione.  
  
 Le proprietà di connessione seguenti sono state aggiunte a SqlClient in .NET Framework 4,5:  
  
- `ApplicationIntent`  
  
- `MultiSubnetFailover`  
  
 È possibile modificare a livello di codice queste parole chiave della stringa di connessione con:  
  
1. <xref:System.Data.SqlClient.SqlConnectionStringBuilder.ApplicationIntent%2A>  
  
2. <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A>  

> [!NOTE]
> L'impostazione `MultiSubnetFailover` di su `true` non è obbligatoria con .NET Framework 4.6.1 o versioni successive.
  
## <a name="connecting-with-multisubnetfailover"></a>Connessione con MultiSubnetFailover  
 Specificare sempre `MultiSubnetFailover=True` in caso di connessione a un listener del gruppo di disponibilità di SQL Server 2012 o a un'istanza del cluster di failover di SQL Server 2012. `MultiSubnetFailover` consente un failover più veloce per tutti i gruppi di disponibilità, permette di abilitare l'istanza del cluster di failover in SQL Server 2012, nonché di ridurre in modo significativo la durata del failover per le topologie AlwaysOn singole e su più subnet. Durante un failover su più subnet, verranno tentate connessioni in parallelo da parte del client. Durante un failover della subnet, ritenterà in modo insistente la connessione TCP.  
  
 La proprietà di connessione `MultiSubnetFailover` indica che l'applicazione viene distribuita in un gruppo di disponibilità o nell'istanza del cluster di failover di SQL Server 2012 e che SqlClient tenterà di connettersi al database sull'istanza principale di SQL Server, tentando di connettersi a tutti gli indirizzi IP. Quando si specifica `MultiSubnetFailover=True` per una connessione, i ripetuti tentativi di connessione TCP del client vengono eseguiti più rapidamente rispetto agli intervalli di ritrasmissione TCP predefiniti del sistema operativo. In tal modo si abilita la riconnessione a seguito di failover di un gruppo di disponibilità AlwaysOn o un'istanza del cluster di failover AlwaysOn ed è applicabile a istanze del cluster di failover o a gruppi di disponibilità su una singola subnet o su più subnet.  
  
 Per altre informazioni sulle parole chiave per le stringhe di connessione in SqlClient, vedere <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
 L'uso di `MultiSubnetFailover=True` quando si stabilisce la connessione a un elemento diverso da un listener del gruppo di disponibilità o da un'istanza del cluster di failover di SQL Server 2012, può avere un impatto negativo sulle prestazioni e non è supportato.  
  
 Usare le linee guida seguenti per connettersi a un server in un gruppo di disponibilità o nell'istanza del cluster di failover di SQL Server 2012:  
  
- Utilizzare la proprietà di connessione `MultiSubnetFailover` in caso di connessione a una subnet singola o a più subnet, in modo da migliorare le prestazioni.  
  
- Per eseguire la connessione a un gruppo di disponibilità, specificare il listener del gruppo di disponibilità come server nella stringa di connessione.  
  
- La connessione a un'istanza di SQL Server configurata con più di 64 indirizzi IP determinerà un errore di connessione.  
  
- Il comportamento di un'applicazione che usa la proprietà di connessione `MultiSubnetFailover` non è influenzato dal tipo di autenticazione, ovvero autenticazione di SQL Server, autenticazione Kerberos o autenticazione di Windows.  
  
- Aumentare il valore di `Connect Timeout` in base al tempo di failover e in modo da ridurre i ripetuti tentativi di connessione dell'applicazione.  
  
- Le transazioni distribuite non sono supportate.  
  
 Se il routing di sola lettura non è attivo, non è possibile stabilire una connessione a un percorso di replica secondaria nelle situazioni seguenti:  
  
1. Se il percorso di replica secondaria non è configurato per accettare le connessioni.  
  
2. Se in un'applicazione viene utilizzato `ApplicationIntent=ReadWrite` (già illustrato in precedenza) e il percorso di replica secondaria è configurato per l'accesso in sola lettura.  
  
 <xref:System.Data.SqlClient.SqlDependency> non è supportato per le repliche secondarie di sola lettura.  
  
 Una connessione non verrà eseguita correttamente se una replica primaria è configurata per rifiutare i carichi di lavoro in sola lettura e nella stringa di connessione è contenuto `ApplicationIntent=ReadOnly`.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Aggiornamento per l'utilizzo di cluster su più subnet dal mirroring del database  
 Si verificherà un errore di connessione (<xref:System.ArgumentException>) se nella stringa di connessione sono presenti le parole chiave di connessione `MultiSubnetFailover` e `Failover Partner` o se vengono usati `MultiSubnetFailover=True` e un protocollo diverso da TCP. Si verificherà un errore (<xref:System.Data.SqlClient.SqlException>) anche se viene usato `MultiSubnetFailover` e se SQL Server restituisce una risposta del partner di failover in cui viene indicato che fa parte di una coppia del mirroring del database.  
  
 Se si aggiorna un'applicazione SqlClient che usa il mirroring del database in uno scenario su più subnet, è necessario rimuovere la proprietà di connessione `Failover Partner` e sostituirla con `MultiSubnetFailover` impostata su `True`, nonché sostituire il nome del server nella stringa di connessione con un listener del gruppo di disponibilità. Se in una stringa di connessione vengono utilizzati `Failover Partner` e `MultiSubnetFailover=True`, verrà generato un errore dal driver. Se, tuttavia, in una stringa di connessione vengono utilizzati `Failover Partner` e `MultiSubnetFailover=False` (o `ApplicationIntent=ReadWrite`), nell'applicazione verrà utilizzato il mirroring del database.  
  
 Il driver restituirà un errore se il mirroring di database viene usato nel database primario nel gruppo di disponibilità e se si usa `MultiSubnetFailover=True` nella stringa di connessione tramite cui viene eseguita la connessione a un database primario anziché a un listener del gruppo di disponibilità.  
  
## <a name="specifying-application-intent"></a>Specificazione della finalità dell'applicazione  
 Se `ApplicationIntent=ReadOnly`, nel client viene richiesto un carico di lavoro di lettura quando si esegue la connessione a un database abilitato per AlwaysOn. Tramite il server, la finalità verrà applicata al momento della connessione e durante un'istruzione di database USE, ma solo a un database abilitato per Always On.  
  
 La parola chiave `ApplicationIntent` non funziona con i database legacy di sola lettura.  
  
 Un database può consentire o impedire carichi di lavoro di lettura nel database AlwaysOn di destinazione. Questa operazione viene eseguita con la clausola `ALLOW_CONNECTIONS` delle istruzioni Transact-SQL `PRIMARY_ROLE` e `SECONDARY_ROLE`.  
  
 La parola chiave `ApplicationIntent` è utilizzata per abilitare il routing di sola lettura.  
  
## <a name="read-only-routing"></a>Routing di sola lettura  
 Il routing di sola lettura è una funzionalità che può garantire la disponibilità di una replica di sola lettura di un database. Per abilitare il routing di sola lettura:  
  
1. È necessario connettersi a un listener del gruppo di disponibilità Always On.  
  
2. La parola chiave della stringa di connessione `ApplicationIntent` deve essere impostata su `ReadOnly`.  
  
3. Il gruppo di disponibilità deve essere configurato dall'amministratore del database per abilitare il routing di sola lettura.  
  
 È possibile che non tutte le connessioni in cui viene utilizzato il routing di sola lettura vengano stabilite alla stessa replica di sola lettura. Le modifiche nella sincronizzazione del database o nella configurazione di routing del server possono comportare connessioni client a repliche di sola lettura diverse. Per assicurare la connessione di tutte le richieste di sola lettura alla stessa replica di sola lettura, non fornire un listener del gruppo di disponibilità alla parola chiave della stringa di connessione `Data Source`. Specificare invece il nome dell'istanza di sola lettura.  
  
 Il routing di sola lettura potrebbe impiegare più tempo a connettersi rispetto alla replica primaria poiché innanzitutto viene eseguita la connessione del routing di sola lettura alla replica primaria e, successivamente, viene cercata la replica secondaria migliore dal punto di vista della lettura. Per questo motivo è necessario aumentare il timeout di accesso.  
  
## <a name="see-also"></a>Vedere anche

- [Funzionalità di SQL Server e ADO.NET](sql-server-features-and-adonet.md)
- [Panoramica di ADO.NET](../ado-net-overview.md)

---
title: Parametri con valori di tabella
description: Informazioni su come effettuare il marshalling di più righe di dati da un'applicazione client a SQL Server utilizzando parametri con valori di tabella.
ms.date: 10/12/2018
dev_langs:
- csharp
- vb
ms.assetid: 370c16d5-db7b-43e3-945b-ccaab35b739b
ms.openlocfilehash: 7b1f0a6c416f660f06cea099197ba136f84407f9
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286197"
---
# <a name="table-valued-parameters"></a>Parametri con valori di tabella
I parametri con valori di tabella offrono un modo semplice per effettuare il marshalling di più righe di dati da un'applicazione client di SQL Server senza richiedere più round trip o una logica speciale sul lato server per l'elaborazione dei dati. I parametri con valori di tabella possono essere usati per incapsulare le righe di dati in un'applicazione client e inviare i dati al server in un singolo comando con parametri. Le righe di dati in ingresso vengono archiviate in una variabile di tabella su cui è possibile operare tramite Transact-SQL.  
  
 I valori di colonna nei parametri con valori di tabella sono accessibili tramite istruzioni Transact-SQL SELECT standard. I parametri con valori di tabella sono fortemente tipizzati e la convalida della relativa struttura è automatica. La dimensione dei parametri con valori di tabella è limitata solo dalla memoria del server.  
  
> [!NOTE]
> Non è possibile restituire dati in un parametro con valori di tabella. I parametri con valori di tabella sono di solo input; la parola chiave OUTPUT non è supportata.  
  
 Per altre informazioni sui parametri con valori di tabella, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|--------------|-----------------|  
|[Utilizzare parametri con valori di tabella (Motore di database)](/sql/relational-databases/tables/use-table-valued-parameters-database-engine)|Viene descritto come creare e usare parametri con valori di tabella.|  
|[Tipi di tabella definiti dall'utente](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/bb522526(v=sql.100))|Vengono descritti i tipi di tabella definiti dall'utente usati per dichiarare parametri con valori di tabella.|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>Passaggio di più righe nelle versioni precedenti di SQL Server  
 Prima dell'introduzione dei parametri con valori di tabella in SQL Server 2008, le opzioni per passare più righe di dati a una stored procedure o a un comando SQL con parametri erano limitate. Uno sviluppatore può scegliere tra le opzioni seguenti per passare più righe al server:  
  
- usare una serie di parametri singoli per rappresentare i valori in più colonne e righe di dati. La quantità di dati che è possibile passare usando questo metodo è limitata dal numero di parametri consentiti. Le stored procedure di SQL Server possono includere al massimo 2100 parametri. La logica lato server è necessaria per assemblare questi singoli valori in una variabile di tabella o in una tabella temporanea per l'elaborazione.  
  
- Aggregare più valori di dati in stringhe delimitate o in documenti XML, quindi passare i valori di testo a una procedura o a un'istruzione. Questa operazione richiede che la routine o l'istruzione includa la logica necessaria per convalidare le strutture dei dati e disaggregare i valori.  
  
- Creare una serie di singole istruzioni SQL per le modifiche ai dati che interessano più righe, ad esempio quelle create chiamando il metodo `Update` di un <xref:System.Data.SqlClient.SqlDataAdapter>. È possibile inviare le modifiche al server singolarmente o in batch in gruppi. Tuttavia, anche in caso di invio in batch contenenti più istruzioni, ogni istruzione viene eseguita separatamente sul server.  
  
- Usare il programma di utilità `bcp` o l'oggetto <xref:System.Data.SqlClient.SqlBulkCopy> per caricare molte righe di dati in una tabella. Sebbene questa tecnica sia molto efficiente, non supporta l'elaborazione sul lato server, a meno che i dati non vengano caricati in una tabella temporanea o in una variabile di tabella.  
  
## <a name="creating-table-valued-parameter-types"></a>Creazione di tipi di parametri con valori di tabella  
 I parametri con valori di tabella sono basati su strutture di tabella fortemente tipizzate definite tramite istruzioni CREATE TYPE Transact-SQL. Per poter usare i parametri con valori di tabella nelle applicazioni client, è prima necessario creare un tipo di tabella e definire la struttura in SQL Server. Per ulteriori informazioni sulla creazione di tipi di tabella, vedere [tipi di tabella definiti dall'utente](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/bb522526(v=sql.100)).  
  
 Nell'istruzione seguente viene creato un tipo di tabella denominato CategoryTableType costituito da colonne CategoryID e CategoryName:  
  
```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
 Dopo aver creato un tipo di tabella, è possibile dichiarare i parametri con valori di tabella in base a tale tipo. Nel frammento Transact-SQL seguente viene illustrato come dichiarare un parametro con valori di tabella in una definizione di stored procedure. Si noti che la parola chiave READONLY è obbligatoria per dichiarare un parametro con valori di tabella.  
  
```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>Modifica di dati con i parametri con valori di tabella (Transact-SQL)  
 I parametri con valori di tabella possono essere usati nelle modifiche ai dati basate su set che interessano più righe eseguendo un'unica istruzione. È possibile, ad esempio, selezionare tutte le righe in un parametro con valori di tabella e inserirle in una tabella di database oppure creare un'istruzione di aggiornamento tramite l'aggiunta di un parametro con valori di tabella alla tabella che si desidera aggiornare.  
  
 L'istruzione UPDATE Transact-SQL seguente illustra come usare un parametro con valori di tabella tramite la sua unione in join con la tabella Categories. Quando si usa un parametro con valori di tabella con un JOIN in una clausola FROM, è anche necessario usare un alias per il parametro, come illustrato di seguito, dove per il parametro con valori di tabella viene usato l'alias "ec":  
  
```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
 In questo esempio Transact-SQL viene illustrato come selezionare le righe da un parametro con valori di tabella per eseguire un'istruzione INSERT in una singola operazione basata su set.  
  
```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>Limitazioni relative ai parametri con valori di tabella  
 Esistono diverse limitazioni per i parametri con valori di tabella:  
  
- Non è possibile passare parametri con valori di tabella a [funzioni CLR definite dall'utente](/sql/relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions).  
  
- I parametri con valori di tabella possono essere indicizzati solo per supportare vincoli UNIQUE o PRIMARY KEY. SQL Server non gestisce statistiche su parametri con valori di tabella.  
  
- I parametri con valori di tabella sono di sola lettura nel codice Transact-SQL. Non è possibile aggiornare i valori delle colonne nelle righe di un parametro con valori di tabella e non è possibile inserire o eliminare righe. Per modificare i dati trasferiti a un'istruzione stored procedure o parametrizzata in un parametro con valori di tabella, è necessario inserire i dati in una tabella temporanea o in una variabile di tabella.  
  
- Non è possibile usare le istruzioni ALTER TABLE per modificare la progettazione dei parametri con valori di tabella.  
  
## <a name="configuring-a-sqlparameter-example"></a>Configurazione di un esempio SqlParameter  
 <xref:System.Data.SqlClient> supporta il popolamento di parametri con valori di tabella da oggetti <xref:System.Data.DataTable>, <xref:System.Data.Common.DbDataReader> o <xref:System.Collections.Generic.IEnumerable%601> \ <xref:Microsoft.SqlServer.Server.SqlDataRecord>. È necessario specificare un nome di tipo per il parametro con valori di tabella usando la proprietà <xref:System.Data.SqlClient.SqlParameter.TypeName%2A> di <xref:System.Data.SqlClient.SqlParameter>. Il `TypeName` deve corrispondere al nome di un tipo compatibile creato in precedenza nel server. Il frammento di codice seguente illustra come configurare <xref:System.Data.SqlClient.SqlParameter> per inserire dati.  

Nell'esempio seguente la variabile `addedCategories` contiene un oggetto <xref:System.Data.DataTable>. Per vedere come viene popolata la variabile, vedere gli esempi nella sezione successiva [Passaggio di un parametro con valori di tabella a una stored procedure](#passing).

```csharp  
// Configure the command and parameter.  
SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
tvpParam.SqlDbType = SqlDbType.Structured;  
tvpParam.TypeName = "dbo.CategoryTableType";  
```  
  
```vb  
' Configure the command and parameter.  
Dim insertCommand As New SqlCommand(sqlInsert, connection)  
Dim tvpParam As SqlParameter = _  
   insertCommand.Parameters.AddWithValue( _  
  "@tvpNewCategories", addedCategories)  
tvpParam.SqlDbType = SqlDbType.Structured  
tvpParam.TypeName = "dbo.CategoryTableType"  
```  
  
 È anche possibile usare qualsiasi oggetto derivato da <xref:System.Data.Common.DbDataReader> per trasmettere righe di dati a un parametro con valori di tabella, come illustrato in questo frammento:  
  
```csharp  
// Configure the SqlCommand and table-valued parameter.  
SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
insertCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", dataReader);  
tvpParam.SqlDbType = SqlDbType.Structured;  
```  
  
```vb  
' Configure the SqlCommand and table-valued parameter.  
Dim insertCommand As New SqlCommand("usp_InsertCategories", connection)  
insertCommand.CommandType = CommandType.StoredProcedure  
Dim tvpParam As SqlParameter = _  
  insertCommand.Parameters.AddWithValue("@tvpNewCategories", _  
  dataReader)  
tvpParam.SqlDbType = SqlDbType.Structured  
```  
  
## <a name="passing-a-table-valued-parameter-to-a-stored-procedure"></a><a name="passing"></a>Passaggio di un parametro con valori di tabella a una stored procedure  
 In questo esempio viene illustrato come trasferire i dati dei parametri con valori di tabella a una stored procedure. Il codice estrae le righe aggiunte in una nuova <xref:System.Data.DataTable> usando il metodo <xref:System.Data.DataTable.GetChanges%2A>. Il codice definisce quindi un <xref:System.Data.SqlClient.SqlCommand>, impostando la proprietà <xref:System.Data.SqlClient.SqlCommand.CommandType%2A> su <xref:System.Data.CommandType.StoredProcedure>. Il <xref:System.Data.SqlClient.SqlParameter> viene popolato usando il metodo <xref:System.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> e <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> viene impostato su `Structured`. <xref:System.Data.SqlClient.SqlCommand> viene eseguito quindi usando il metodo <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A>.  
  
```csharp  
// Assumes connection is an open SqlConnection object.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Configure the SqlCommand and SqlParameter.  
  SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
  insertCommand.CommandType = CommandType.StoredProcedure;  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
```vb  
' Assumes connection is an open SqlConnection object.  
Using connection  
   '  Create a DataTable with the modified rows.  
   Dim addedCategories As DataTable = _  
     CategoriesDataTable.GetChanges(DataRowState.Added)  
  
  ' Configure the SqlCommand and SqlParameter.  
   Dim insertCommand As New SqlCommand( _  
     "usp_InsertCategories", connection)  
   insertCommand.CommandType = CommandType.StoredProcedure  
   Dim tvpParam As SqlParameter = _  
     insertCommand.Parameters.AddWithValue( _  
     "@tvpNewCategories", addedCategories)  
   tvpParam.SqlDbType = SqlDbType.Structured  
  
   '  Execute the command.  
   insertCommand.ExecuteNonQuery()  
End Using  
```  
  
### <a name="passing-a-table-valued-parameter-to-a-parameterized-sql-statement"></a>Passaggio di un parametro con valori di tabella a un'istruzione SQL con parametri  
 Nell'esempio seguente viene illustrato come inserire dati nella tabella dbo.Categories tramite un'istruzione INSERT con una sottoquery SELECT che dispone di un parametro con valori di tabella come origine dati. Quando si trasferisce un parametro con valori di tabella a un'istruzione SQL con parametri, è necessario specificare un nome di tipo per il parametro con valori di tabella tramite la nuova proprietà <xref:System.Data.SqlClient.SqlParameter.TypeName%2A> di un <xref:System.Data.SqlClient.SqlParameter>. Questo `TypeName` deve corrispondere al nome di un tipo compatibile creato in precedenza nel server. Il codice in questo esempio usa la proprietà `TypeName` per fare riferimento alla struttura del tipo definita in dbo.CategoryTableType.  
  
> [!NOTE]
> Se si fornisce un valore per una colonna Identity in un parametro con valori di tabella, è necessario eseguire l'istruzione SET IDENTITY_INSERT per la sessione.  
  
```csharp  
// Assumes connection is an open SqlConnection.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Define the INSERT-SELECT statement.  
  string sqlInsert =
      "INSERT INTO dbo.Categories (CategoryID, CategoryName)"  
      + " SELECT nc.CategoryID, nc.CategoryName"  
      + " FROM @tvpNewCategories AS nc;"  

  // Configure the command and parameter.  
  SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  
  tvpParam.TypeName = "dbo.CategoryTableType";  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
```vb  
' Assumes connection is an open SqlConnection.  
Using connection  
  ' Create a DataTable with the modified rows.  
  Dim addedCategories As DataTable = _  
    CategoriesDataTable.GetChanges(DataRowState.Added)  
  
  ' Define the INSERT-SELECT statement.  
  Dim sqlInsert As String = _  
  "INSERT INTO dbo.Categories (CategoryID, CategoryName)" _  
  & " SELECT nc.CategoryID, nc.CategoryName" _  
  & " FROM @tvpNewCategories AS nc;"  
  
  ' Configure the command and parameter.  
  Dim insertCommand As New SqlCommand(sqlInsert, connection)  
  Dim tvpParam As SqlParameter = _  
     insertCommand.Parameters.AddWithValue( _  
    "@tvpNewCategories", addedCategories)  
  tvpParam.SqlDbType = SqlDbType.Structured  
  tvpParam.TypeName = "dbo.CategoryTableType"  
  
  ' Execute the query  
  insertCommand.ExecuteNonQuery()  
End Using  
```  
  
## <a name="streaming-rows-with-a-datareader"></a>Trasmissione di flussi di righe con un oggetto DataReader  
 È anche possibile usare qualsiasi oggetto derivato da <xref:System.Data.Common.DbDataReader> per trasmettere righe di dati a un parametro con valori di tabella. Nel frammento di codice seguente viene illustrato il recupero di dati da un database Oracle tramite un <xref:System.Data.OracleClient.OracleCommand> e un <xref:System.Data.OracleClient.OracleDataReader>. Il codice configura quindi un <xref:System.Data.SqlClient.SqlCommand> per richiamare una stored procedure con un singolo parametro di input. La proprietà <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> del <xref:System.Data.SqlClient.SqlParameter> è impostata su `Structured`. <xref:System.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> trasferisce il set di risultati `OracleDataReader` alla stored procedure come parametro con valori di tabella.  
  
```csharp  
// Assumes connection is an open SqlConnection.  
// Retrieve data from Oracle.  
OracleCommand selectCommand = new OracleCommand(  
   "Select CategoryID, CategoryName FROM Categories;",  
   oracleConnection);  
OracleDataReader oracleReader = selectCommand.ExecuteReader(  
   CommandBehavior.CloseConnection);  
  
 // Configure the SqlCommand and table-valued parameter.  
 SqlCommand insertCommand = new SqlCommand(  
   "usp_InsertCategories", connection);  
 insertCommand.CommandType = CommandType.StoredProcedure;  
 SqlParameter tvpParam =  
    insertCommand.Parameters.AddWithValue(  
    "@tvpNewCategories", oracleReader);  
 tvpParam.SqlDbType = SqlDbType.Structured;  
  
 // Execute the command.  
 insertCommand.ExecuteNonQuery();  
```  
  
```vb  
' Assumes connection is an open SqlConnection.  
' Retrieve data from Oracle.  
Dim selectCommand As New OracleCommand( _  
  "Select CategoryID, CategoryName FROM Categories;", _  
  oracleConnection)  
Dim oracleReader As OracleDataReader = _  
  selectCommand.ExecuteReader(CommandBehavior.CloseConnection)  
  
' Configure SqlCommand and table-valued parameter.  
Dim insertCommand As New SqlCommand("usp_InsertCategories", connection)  
insertCommand.CommandType = CommandType.StoredProcedure  
Dim tvpParam As SqlParameter = _  
  insertCommand.Parameters.AddWithValue("@tvpNewCategories", _  
  oracleReader)  
tvpParam.SqlDbType = SqlDbType.Structured  
  
' Execute the command.  
insertCommand.ExecuteNonQuery()  
```  
  
## <a name="see-also"></a>Vedere anche

- [Configurazione di parametri e tipi di dati dei parametri](../configuring-parameters-and-parameter-data-types.md)
- [Comandi e parametri](../commands-and-parameters.md)
- [Parametri DataAdapter](../dataadapter-parameters.md)
- [SQL Server operazioni sui dati in ADO.NET](sql-server-data-operations.md)
- [Panoramica di ADO.NET](../ado-net-overview.md)

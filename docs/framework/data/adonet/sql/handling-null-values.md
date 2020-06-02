---
title: Gestione dei valori null
description: Informazioni sul modo in cui il .NET Framework provider di dati per SQL Server gestisce null e su null e SqlBoolean, sulla logica a tre valori e sull'assegnazione di valori null.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.openlocfilehash: a4d086d81f1c2c959780366cfeb59f2d265bc40c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286455"
---
# <a name="handling-null-values"></a>Gestione dei valori null
Se il valore di una colonna è sconosciuto o mancante, viene usato un valore Null in un database relazionale. Un valore Null non è né una stringa vuota (per i tipi di dati character o datetime) né un valore zero (per i tipi di dati numerici). La specifica ANSI SQL-92 indica che un valore Null deve essere lo stesso per tutti i tipi di dati, in modo che tutti i valori Null vengano gestiti in modo coerente. Lo spazio dei nomi <xref:System.Data.SqlTypes> specifica la semantica Null implementando l'interfaccia <xref:System.Data.SqlTypes.INullable>. Ogni tipo di dati in <xref:System.Data.SqlTypes> ha una propria proprietà `IsNull` e un valore `Null` che può essere assegnato a un'istanza di tale tipo di dati.  
  
> [!NOTE]
> In .NET Framework versione 2,0 è stato introdotto il supporto per i tipi di valore Nullable, che consentono ai programmatori di estendere un tipo di valore per rappresentare tutti i valori del tipo sottostante. Questi tipi di valore nullable CLR rappresentano un'istanza della <xref:System.Nullable> struttura. Questa funzionalità è particolarmente utile quando i tipi di valore sono boxed e unboxed, garantendo una maggiore compatibilità con i tipi di oggetto. I tipi di valore nullable CLR non sono destinati all'archiviazione di valori null di database perché un valore Null ANSI SQL non si comporta in modo analogo a un `null` riferimento (o `Nothing` in Visual Basic). Per usufruire dei valori Null SQL ANSI del database, usare valori Null <xref:System.Data.SqlTypes> anziché <xref:System.Nullable>. Per ulteriori informazioni sull'utilizzo dei tipi nullable di valori CLR in Visual Basic vedere [tipi di valore Nullable](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)e per C# vedere [tipi di valore Nullable](../../../../csharp/language-reference/builtin-types/nullable-value-types.md).  
  
## <a name="nulls-and-three-valued-logic"></a>Valori null e logica con tre valori  
 Consentendo i valori Null nelle definizioni di colonna si introduce una logica a tre valori nell'applicazione. Un confronto può restituire una delle tre condizioni seguenti:  
  
- True   
  
- False  
  
- Sconosciuto  
  
 Poiché il valore Null è considerato sconosciuto, due valori Null confrontati tra loro non sono considerati uguali. Nelle espressioni che usano operatori aritmetici, se uno degli operandi è Null, anche il risultato è Null.  
  
## <a name="nulls-and-sqlboolean"></a>Valori Null e SqlBoolean  
 Il confronto tra qualsiasi <xref:System.Data.SqlTypes> restituisce un elemento <xref:System.Data.SqlTypes.SqlBoolean>. La funzione `IsNull` per ogni `SqlType` restituisce un elemento <xref:System.Data.SqlTypes.SqlBoolean> e può essere usata per verificare la presenza di valori Null. Le seguenti tabelle di veridicità illustrano la funzione degli operatori AND, OR e NOT in presenza di un valore Null. (T=true, F=false e U=unknown o Null)  
  
 ![Tabella Truth](./media/truthtable-bpuedev11.gif "TruthTable_bpuedev11")  
  
### <a name="understanding-the-ansi_nulls-option"></a>Nozioni di base sull'opzione ANSI_NULLS  
 <xref:System.Data.SqlTypes> offre la stessa semantica di quando si imposta l'opzione ANSI_NULLS in SQL Server. Tutti gli operatori aritmetici (+,-, \* ,/,%), gli operatori bit per bit (~, &, \| ) e la maggior parte delle funzioni restituiscono null se uno degli operandi o degli argomenti è null, ad eccezione della proprietà `IsNull` .  
  
 Lo standard ANSI SQL-92 non supporta *columnName* = NULL in una clausola WHERE. In SQL Server l'opzione ANSI_NULLS controlla sia il supporto di valori Null predefinito nel database, sia la valutazione dei confronti con i valori Null. Se l'opzione ANSI_NULLS è attivata (impostazione predefinita), è necessario usare l'operatore IS NULL nelle espressioni quando si effettuano test dei valori Null. Ad esempio, se l'opzione ANSI_NULLS è impostata su ON, il confronto seguente restituisce sempre UNKNOWN:  
  
```sql
colname > NULL  
```  
  
 Il confronto con una variabile che contiene un valore Null restituisce anche Unknown:  
  
```sql
colname > @MyVariable  
```  
  
 Per verificare la presenza di un valore Null, usare il predicato IS NULL o IS NOT NULL. La clausola WHERE potrebbe risultare in tal modo più complessa. Ad esempio, la colonna TerritoryID nella tabella Customer di AdventureWorks consente i valori Null. Un'istruzione SELECT che oltre ad altri valori deve verificare i valori Null deve includere il predicato IS NULL:  
  
```sql
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
 Se si imposta ANSI_NULLS come disattivata in SQL Server, è possibile creare espressioni che usano l'operatore di uguaglianza per eseguire il confronto con il valore Null. Tuttavia, non è possibile impedire a diverse connessioni di impostare opzioni Null per tale connessione. L'uso di IS NULL per testare i valori Null funziona sempre, indipendentemente dalle impostazioni di ANSI_NULLS per una connessione.  
  
 L'impostazione di ANSI_NULLS come disattivata non è supportata in un oggetto `DataSet`, che segue sempre lo standard ANSI SQL-92 per la gestione dei valori Null in <xref:System.Data.SqlTypes>.  
  
## <a name="assigning-null-values"></a>Assegnazione di valori null  
 I valori Null sono speciali e la relativa semantica di archiviazione e assegnazione varia tra sistemi di tipi e sistemi di archiviazione diversi. Un oggetto `Dataset` è progettato per essere usato con sistemi di tipi e di archiviazione diversi.  
  
 In questa sezione viene descritta la semantica Null per l'assegnazione di valori Null a un <xref:System.Data.DataColumn> in un <xref:System.Data.DataRow> nei diversi sistemi di tipi.  
  
 `DBNull.Value`  
 Questa assegnazione è valida per un `DataColumn` di qualsiasi tipo. Se il tipo implementa `INullable`, `DBNull.Value` viene assegnato forzatamente al valore Null fortemente tipizzato appropriato.  
  
 `SqlType.Null`  
 Tutti i tipi di dati <xref:System.Data.SqlTypes> implementano `INullable`. Se il valore Null fortemente tipizzato può essere convertito nel tipo di dati della colonna usando gli operatori di cast impliciti, l'assegnazione ha esito positivo. In caso contrario, viene generata un'eccezione di cast non valido.  
  
 `null`  
 Se "null" è un valore valido per il tipo di dati `DataColumn` specificato, viene assegnato forzatamente all'oggetto `DbNull.Value` o `Null` appropriato associato al tipo `INullable` (`SqlType.Null`)  
  
 `derivedUdt.Null`  
 Per le colonne con tipo definito dall'utente (UDT), i valori Null vengono sempre archiviati in base al tipo associato a `DataColumn`. Si consideri il caso di un UDT associato a un `DataColumn` che non implementa un elemento `INullable` mentre la relativa sottoclasse lo implementa. In questo caso, se viene assegnato un valore Null fortemente tipizzato associato alla classe derivata, viene archiviato come `DbNull.Value` non tipizzato, perché l'archiviazione Null è sempre coerente con il tipo di dati di DataColumn.  
  
> [!NOTE]
> La struttura di `Nullable<T>` o <xref:System.Nullable> non è attualmente supportata in `DataSet`.  
  
### <a name="multiple-column-row-assignment"></a>Assegnazione di più colonne (riga)  
 `DataTable.Add`, `DataTable.LoadDataRow` o altre API che accettano un elemento <xref:System.Data.DataRow.ItemArray%2A> che viene mappato a una riga, eseguono il mapping di "null" al valore predefinito di DataColumn. Se un oggetto nella matrice contiene `DbNull.Value` o la relativa controparte fortemente tipizzata, vengono applicate le stesse regole descritte sopra.  
  
 Per un'istanza di assegnazioni di valori Null di `DataRow.["columnName"]` si applicano inoltre le regole seguenti:  
  
1. Il valore predefinito *default* è `DbNull.Value` per tutte le colonne ad eccezione di quelle Null fortemente tipizzate, alle quali si applica il valore Null fortemente tipizzato appropriato.  
  
2. I valori Null non vengono mai scritti durante la serializzazione nei file XML (come in "xsi:nil").  
  
3. Tutti i valori non Null, incluse le impostazioni predefinite, vengono sempre scritti durante la serializzazione in XML, a differenza della semantica XSD/XML in cui un valore Null (xsi:nil) è esplicito e il valore predefinito è implicito (se non è presente in XML, un parser di convalida può ottenerlo da uno schema XSD associato). Per un oggetto `DataTable` è vero il contrario: un valore Null è implicito e il valore predefinito è esplicito.  
  
4. A tutti i valori di colonna mancanti per le righe lette dall'input XML viene assegnato NULL. Alle righe create con <xref:System.Data.DataTable.NewRow%2A> o metodi simili viene assegnato il valore predefinito di DataColumn.  
  
5. Il metodo <xref:System.Data.DataRow.IsNull%2A> restituisce `true` sia per `DbNull.Value` che per `INullable.Null`.  
  
## <a name="assigning-null-values"></a>Assegnazione di valori null  
 Il valore predefinito per qualsiasi istanza di <xref:System.Data.SqlTypes> è Null.  
  
 I valori Null in <xref:System.Data.SqlTypes> sono specifici del tipo e non possono essere rappresentati da un singolo valore, ad esempio `DbNull`. Usare la proprietà `IsNull` per verificare la presenza di valori Null.  
  
 È possibile assegnare valori Null a un <xref:System.Data.DataColumn> come illustrato nell'esempio di codice seguente. È possibile assegnare direttamente i valori Null alle variabili `SqlTypes` senza generare un'eccezione.  
  
### <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene creato un <xref:System.Data.DataTable> con due colonne definite come <xref:System.Data.SqlTypes.SqlInt32> e <xref:System.Data.SqlTypes.SqlString>. Il codice aggiunge una riga di valori noti, una riga di valori Null e quindi scorre esegue l'iterazione in <xref:System.Data.DataTable>, assegnando i valori alle variabili e visualizzando l'output nella finestra della console.  
  
 [!code-csharp[DataWorks SqlTypes.IsNull#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.IsNull/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.IsNull#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.IsNull/VB/source.vb#1)]  
  
 L'esempio visualizza i risultati seguenti:  
  
```output
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a>Confronto di valori null con SqlTypes e tipi CLR  
 Quando si confrontano i valori Null, è importante comprendere la differenza tra il modo in cui il metodo `Equals` valuta i valori Null in <xref:System.Data.SqlTypes> e il modo in cui funziona con i tipi CLR. Tutti i metodi <xref:System.Data.SqlTypes>`Equals` usano la semantica del database per valutare i valori Null: se uno o entrambi i valori sono Null, il confronto restituisce Null. D'altra parte, l'uso del metodo CLR `Equals` per due <xref:System.Data.SqlTypes> genera True se entrambi i valori sono Null. Ciò riflette la differenza tra l'uso di un metodo di istanza, ad esempio il metodo CLR `String.Equals`, e l'uso del metodo statico/condiviso, `SqlString.Equals`.  
  
 Nell'esempio seguente viene illustrata la differenza nei risultati tra il metodo `SqlString.Equals` e il metodo `String.Equals` quando a ognuno viene passata una coppia di valori Null e quindi una coppia di stringhe vuote.  
  
 [!code-csharp[DataWorks SqlTypes.CompareNulls#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.CompareNulls/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.CompareNulls#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.CompareNulls/VB/source.vb#1)]  
  
 Il codice produce l'output seguente:  
  
```output
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True
```  
  
## <a name="see-also"></a>Vedere anche

- [Tipi di dati SQL Server e ADO.NET](sql-server-data-types.md)
- [Panoramica di ADO.NET](../ado-net-overview.md)

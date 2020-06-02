---
title: LINQ to SQL
description: LINQ to SQL è un componente del .NET Framework che fornisce un'infrastruttura in fase di esecuzione per la gestione di dati relazionali come oggetti.
ms.date: 03/30/2017
ms.assetid: 73d13345-eece-471a-af40-4cc7a2f11655
ms.openlocfilehash: 13502bfee3ee24764d190dace1512bc958343973
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286314"
---
# <a name="linq-to-sql"></a>LINQ to SQL
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]è un componente di .NET Framework versione 3,5 che fornisce un'infrastruttura in fase di esecuzione per la gestione di dati relazionali come oggetti.  
  
> [!NOTE]
> I dati relazionali vengono visualizzati come una raccolta di tabelle bidimensionali (*relazioni* o *file flat*), in cui le colonne comuni collegano tra loro le tabelle. Per usare [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] in modo efficiente, è necessario avere familiarità con i principi di base dei database relazionali.  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene eseguito il mapping del modello dati di un database relazionale a un modello a oggetti espresso nel linguaggio di programmazione dello sviluppatore. Quando viene eseguita l'applicazione, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] converte in SQL le query LINQ (Language Integrated Query) nel modello a oggetti e le invia al database per l'esecuzione. Quando il database restituisce i risultati, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] li converte di nuovo in oggetti che possono essere utilizzati nel linguaggio di programmazione dello sviluppatore.  
  
 Gli sviluppatori che usano Visual Studio in genere usano la Object Relational Designer, che fornisce un'interfaccia utente per l'implementazione di molte delle funzionalità di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] .  
  
 Nella documentazione inclusa in questa versione di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] vengono descritti i blocchi di compilazione di base, il processi e le tecniche necessari per la compilazione di applicazioni [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. È anche possibile cercare Microsoft Docs per problemi specifici ed è possibile partecipare al forum su [LINQ](https://social.msdn.microsoft.com/forums/home?forum=linqtosql), in cui è possibile discutere in dettaglio argomenti più complessi con gli esperti. Infine, il [LINQ to SQL: query integrata nel linguaggio .NET per i dati relazionali](https://docs.microsoft.com/previous-versions/dotnet/articles/bb425822(v=msdn.10)) white paper la tecnologia dei dettagli [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] , completati con esempi di codice Visual Basic e C#.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Per iniziare](getting-started.md)  
 Viene fornita una panoramica di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] e vengono fornite informazioni su come iniziare a usare [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 [Guida per programmatori](programming-guide.md)  
 Vengono descritte le procedure per eseguire il mapping, creare query, eseguire operazioni di aggiornamento e debug e attività simili.  
  
 [Riferimento](reference.md)  
 Fornisce informazioni di riferimento sui diversi aspetti di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. Tra gli argomenti vengono descritti il mapping dei tipi CLR SQL, la conversione dell'operatore di query standard e altri.  
  
 [Esempi](samples.md)  
 Vengono forniti collegamenti a Visual Basic e esempi di C#.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [LINQ (Language-Integrated Query)-C #](../../../../../csharp/programming-guide/concepts/linq/index.md)\
 Viene fornita una panoramica delle tecnologie LINQ in C#.

 [LINQ (Language-Integrated Query) - Visual Basic](../../../../../visual-basic/programming-guide/concepts/linq/index.md)  
 Viene fornita una panoramica delle tecnologie LINQ in Visual Basic.
  
 [LINQ](../../../../../visual-basic/programming-guide/language-features/linq/index.md)  
 Descrive le tecnologie LINQ per gli utenti Visual Basic.  
  
 [LINQ e ADO.NET](../../linq-and-ado-net.md)  
 Collegamenti al portale di ADO.NET.  
  
 [Procedure dettagliate relative a LINQ to SQL](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/bb386295(v=vs.90))  
 Vengono elencate le procedure dettagliate disponibili per [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 [Download di database di esempio](downloading-sample-databases.md)  
 Viene descritto come scaricare i database di esempio usati nella documentazione.  
  
 [Cenni preliminari sul controllo server Web LinqDataSource](https://docs.microsoft.com/previous-versions/aspnet/bb547113(v=vs.100))  
 Viene descritto il modo <xref:System.Web.UI.WebControls.LinqDataSource> in cui il controllo espone LINQ (Language Integrated Query) agli sviluppatori Web tramite l'architettura del controllo origine dati ASP.NET.

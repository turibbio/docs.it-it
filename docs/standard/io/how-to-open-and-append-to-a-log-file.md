---
title: 'Procedura: aprire e accodare un file di log'
ms.date: 01/21/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- log files, opening
- streams, opening and appending to log file
- log files, appending to
- I/O [.NET Framework], log files
ms.assetid: 74423362-1721-49cb-aa0a-e04005f72a06
ms.openlocfilehash: 025c35344b9262e1f2fa6da87b68e46e21a54222
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291825"
---
# <a name="how-to-open-and-append-to-a-log-file"></a>Procedura: aprire e accodare un file di log
<xref:System.IO.StreamWriter> e <xref:System.IO.StreamReader> scrivono e leggono i caratteri nei flussi. L'esempio di codice seguente apre il file *log.txt* per l'input oppure crea il file, se non esiste già, e aggiunge informazioni alla fine del file. Nell'esempio, il contenuto del file viene quindi scritto nell'output standard per la visualizzazione.

In alternativa a questo esempio, è possibile archiviare le informazioni come un'unica stringa o matrice di stringhe e usare il metodo <xref:System.IO.File.WriteAllText%2A?displayProperty=nameWithType> o <xref:System.IO.File.WriteAllLines%2A?displayProperty=nameWithType> per ottenere la stessa funzionalità.  
  
> [!NOTE]
> Gli utenti di Visual Basic possono scegliere di usare i metodi e le proprietà forniti dalla classe <xref:Microsoft.VisualBasic.Logging.Log> o dalla classe <xref:Microsoft.VisualBasic.FileIO.FileSystem> per creare file di log o scrivere al loro interno.  
  
## <a name="example"></a>Esempio  
 [!code-csharp[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source2.cs#2)]
 [!code-vb[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source2.vb#2)]  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.IO.StreamWriter>  
- <xref:System.IO.StreamReader>  
- <xref:System.IO.File.AppendText%2A?displayProperty=nameWithType>  
- <xref:System.IO.File.OpenText%2A?displayProperty=nameWithType>  
- <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType>  
- [Procedura: enumerare directory e file](how-to-enumerate-directories-and-files.md)  
- [Procedura: leggere e scrivere in un file di dati appena creato](how-to-read-and-write-to-a-newly-created-data-file.md)  
- [Procedura: leggere testo da un file](how-to-read-text-from-a-file.md)  
- [Procedura: scrivere testo in un file](how-to-write-text-to-a-file.md)  
- [Procedura: leggere caratteri da una stringa](how-to-read-characters-from-a-string.md)  
- [Procedura: scrivere caratteri in una stringa](how-to-write-characters-to-a-string.md)  
- [I/O di file e di flussi](index.md)

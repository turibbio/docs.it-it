---
title: 'Procedura: Leggere da file binari'
ms.date: 07/20/2015
helpviewer_keywords:
- binary files [Visual Basic], reading from
- I/O [Visual Basic], reading from binary files
- ReadAllBytes method [Visual Basic], reading from binary files
- My.Computer.FileSystem object, reading from binary files
ms.assetid: d2b1269e-24b6-42e0-9414-ae708db282d8
ms.openlocfilehash: 3b4108034b86d99143fff6943e68ca0077ebd21b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359929"
---
# <a name="how-to-read-from-binary-files-in-visual-basic"></a>Procedura: leggere da file binari in Visual Basic

L'oggetto `My.Computer.FileSystem` offre il metodo `ReadAllBytes` per leggere da file binari.  
  
### <a name="to-read-from-a-binary-file"></a>Per leggere da un file binario  
  
- Usare il metodo `ReadAllBytes` che restituisce il contenuto di un file sotto forma di matrice di byte. Nell'esempio riportato di seguito viene letto il file `C:/Documents and Settings/selfportrait.jpg`.  
  
     [!code-vb[VbVbcnMyFileSystem#78](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#78)]  
  
- Per file binari di grandi dimensioni, è possibile usare il metodo <xref:System.IO.FileStream.Read%2A> dell'oggetto <xref:System.IO.FileStream> per leggere solo una parte specificata del file per volta. È quindi possibile limitare la parte del file caricata nella memoria per ogni operazione di lettura. Nell'esempio di codice seguente viene copiato un file e viene consentito al chiamante di specificare la parte di file letta nella memoria per l'operazione di lettura.  
  
     [!code-vb[VbVbcnMyFileSystem#91](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#91)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  

 Le condizioni seguenti possono generare un'eccezione:  
  
- Il percorso non è valido per uno dei seguenti motivi: è una stringa di lunghezza zero, contiene solo spazi vuoti, contiene caratteri non validi o è il percorso di una periferica (<xref:System.ArgumentException>).  
  
- Il percorso non è valido in quanto è `Nothing` (<xref:System.ArgumentNullException>).  
  
- Il file non esiste (<xref:System.IO.FileNotFoundException>).  
  
- Il file è in uso in un altro processo oppure si verifica un errore di I/O (<xref:System.IO.IOException>).  
  
- La lunghezza del percorso supera la lunghezza massima definita dal sistema (<xref:System.IO.PathTooLongException>).  
  
- Il nome di un file o di una directory nel percorso contiene i due punti (:) o ha un formato non valido (<xref:System.NotSupportedException>).  
  
- La memoria disponibile non è sufficiente per la scrittura della stringa nel buffer (<xref:System.OutOfMemoryException>).  
  
- L'utente non dispone delle autorizzazioni necessarie per visualizzare il percorso (<xref:System.Security.SecurityException>).  
  
 Non basarsi sul nome del file per prendere decisioni in merito al relativo contenuto. È possibile ad esempio che il file Form1.vb non sia un file di origine di Visual Basic.  
  
 Prima di usare i dati nell'applicazione verificare tutti gli input. È possibile che il contenuto del file non corrisponda a quanto previsto e che quindi i metodi per la lettura dal file non abbiano esito positivo.  
  
## <a name="see-also"></a>Vedere anche

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllBytes%2A>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A>
- [Lettura da file](reading-from-files.md)
- [Procedura: Leggere da file di testo con più formati](how-to-read-from-text-files-with-multiple-formats.md)
- [Archiviazione e lettura di dati negli Appunti](../computer-resources/storing-data-to-and-reading-from-the-clipboard.md)

---
title: 'Procedura: Raggruppare file per estensione (LINQ)'
ms.date: 07/20/2015
ms.assetid: 904dc6d7-7162-4655-a7f4-5785d669bc5a
ms.openlocfilehash: 67c48cd735b51009835cbc8df3101ea3cb212a87
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396545"
---
# <a name="how-to-group-files-by-extension-linq-visual-basic"></a>Procedura: raggruppare file per estensione (LINQ) (Visual Basic)
Questo esempio illustra come usare LINQ per eseguire operazioni avanzate di raggruppamento e ordinamento su elenchi di file o cartelle. Illustra anche come disporre l'output nella finestra della console usando i metodi <xref:System.Linq.Enumerable.Skip%2A> e <xref:System.Linq.Enumerable.Take%2A>.  
  
## <a name="example"></a>Esempio  
 La query seguente illustra come raggruppare il contenuto di un albero di directory specificato per l'estensione dei nomi dei file.  
  
```vb  
Module GroupByExtension  
    Public Sub Main()  
  
        ' Root folder to query, along with all subfolders.  
        Dim startFolder As String = "C:\program files\Microsoft Visual Studio 9.0\VB\"  
  
        ' Used in WriteLine() to skip over startfolder in output lines.  
        Dim rootLength As Integer = startFolder.Length  
  
        'Take a snapshot of the folder contents  
        Dim dir As New System.IO.DirectoryInfo(startFolder)  
        Dim fileList = dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories)  
  
        ' Create the query.  
        Dim queryGroupByExt = From file In fileList _  
                          Group By file.Extension.ToLower() Into fileGroup = Group _  
                          Order By ToLower _  
                          Select fileGroup  
  
        ' Execute the query. By storing the result we can  
        ' page the display with good performance.  
        Dim groupByExtList = queryGroupByExt.ToList()  
  
        ' Display one group at a time. If the number of
        ' entries is greater than the number of lines  
        ' in the console window, then page the output.  
        Dim trimLength = startFolder.Length  
        PageOutput(groupByExtList, trimLength)  
  
    End Sub  
  
    ' Pages console display for large query results. No more than one group per page.  
    ' This sub specifically works with group queries of FileInfo objects  
    ' but can be modified for any type.  
    Sub PageOutput(ByVal groupQuery, ByVal charsToSkip)  
  
        ' "3" = 1 line for extension key + 1 for "Press any key" + 1 for input cursor.  
        Dim numLines As Integer = Console.WindowHeight - 3  
        ' Flag to indicate whether there are more results to display  
        Dim goAgain As Boolean = True  
  
        For Each fg As IEnumerable(Of System.IO.FileInfo) In groupQuery  
            ' Start a new extension at the top of a page.  
            Dim currentLine As Integer = 0  
  
            Do While (currentLine < fg.Count())  
                Console.Clear()  
                Console.WriteLine(fg(0).Extension)  
  
                ' Get the next page of results  
                ' No more than one filename per page  
                Dim resultPage = From file In fg _  
                                Skip currentLine Take numLines  
  
                ' Execute the query. Trim the display output.  
                For Each line In resultPage  
                    Console.WriteLine(vbTab & line.FullName.Substring(charsToSkip))  
                Next  
  
                ' Advance the current position  
                currentLine = numLines + currentLine  
  
                ' Give the user a chance to break out of the loop  
                Console.WriteLine("Press any key for next page or the 'End' key to exit.")  
                Dim key As ConsoleKey = Console.ReadKey().Key  
                If key = ConsoleKey.End Then  
                    goAgain = False  
                    Exit For  
                End If  
            Loop  
        Next  
    End Sub  
End Module  
```  
  
 L'output di questo programma può essere lungo, a seconda dei dettagli del file system locale e dell'impostazione di `startFolder`. Per abilitare la visualizzazione di tutti i risultati, in questo esempio viene illustrato come scorrere i risultati. È possibile applicare le stesse tecniche ad applicazioni Windows e Web. Si noti che, poiché il codice dispone gli elementi in un gruppo, è necessario un ciclo `For Each` annidato. È disponibile anche una logica aggiuntiva per calcolare la posizione corrente nell'elenco e per consentire all'utente di interrompere lo scorrimento e uscire dal programma. In questo caso particolare la query di scorrimento viene eseguita sui risultati memorizzati nella cache della query originale. In altri contesti, come ad esempio LINQ to SQL, la memorizzazione nella cache non è necessaria.  
  
## <a name="compile-the-code"></a>Compilare il codice  
Creare un progetto di applicazione console Visual Basic con un' `Imports` istruzione per lo spazio dei nomi System. Linq.
  
## <a name="see-also"></a>Vedere anche

- [LINQ to Objects (Visual Basic)](linq-to-objects.md)
- [LINQ and File Directories (Visual Basic)](linq-and-file-directories.md) (LINQ e directory file (Visual Basic))

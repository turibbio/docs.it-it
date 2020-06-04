---
title: 'Procedura: Eseguire una query per trovare i file con un attributo o un nome specifico'
ms.date: 07/20/2015
ms.assetid: b26026a3-3f43-448f-a582-259997af6be0
ms.openlocfilehash: 4a6a5630f4ac0eb0cb08aed0dc8a390225194675
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396415"
---
# <a name="how-to-query-for-files-with-a-specified-attribute-or-name-visual-basic"></a><span data-ttu-id="b8900-102">Procedura: eseguire una query per i file con un nome o un attributo specificato (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b8900-102">How to: Query for Files with a Specified Attribute or Name (Visual Basic)</span></span>
<span data-ttu-id="b8900-103">In questo esempio viene illustrato come trovare tutti i file con un'estensione del nome specificata, come ad esempio "txt", in un albero di directory specificato.</span><span class="sxs-lookup"><span data-stu-id="b8900-103">This example shows how to find all files that have a specified file name extension (for example ".txt") in a specified directory tree.</span></span> <span data-ttu-id="b8900-104">Viene anche illustrato come restituire il file più recente o meno recente nell'albero in base all'ora di creazione.</span><span class="sxs-lookup"><span data-stu-id="b8900-104">It also shows how to return either the newest or oldest file in the tree based on the creation time.</span></span>  
  
## <a name="example"></a><span data-ttu-id="b8900-105">Esempio</span><span class="sxs-lookup"><span data-stu-id="b8900-105">Example</span></span>  
  
```vb  
Module FindFileByExtension  
    Sub Main()  
  
        ' Change the drive\path if necessary  
        Dim root As String = "C:\Program Files\Microsoft Visual Studio 9.0"  
  
        'Take a snapshot of the folder contents  
        Dim dir As New System.IO.DirectoryInfo(root)  
  
        Dim fileList = dir.GetFiles("*.*", System.IO.SearchOption.AllDirectories)  
  
        ' This query will produce the full path for all .txt files  
        ' under the specified folder including subfolders.  
        ' It orders the list according to the file name.  
        Dim fileQuery = From file In fileList _  
                        Where file.Extension = ".txt" _  
                        Order By file.Name _  
                        Select file  
  
        For Each file In fileQuery  
            Console.WriteLine(file.FullName)  
        Next  
  
        ' Create and execute a new query by using  
        ' the previous query as a starting point.  
        ' fileQuery is not executed again until the  
        ' call to Last  
        Dim fileQuery2 = From file In fileQuery _  
                         Order By file.CreationTime _  
                         Select file.Name, file.CreationTime  
  
        ' Execute the query  
        Dim newestFile = fileQuery2.Last  
  
        Console.WriteLine("\r\nThe newest .txt file is {0}. Creation time: {1}", _  
                newestFile.Name, newestFile.CreationTime)  
  
        ' Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
  
    End Sub  
End Module  
```  
  
## <a name="compile-the-code"></a><span data-ttu-id="b8900-106">Compilare il codice</span><span class="sxs-lookup"><span data-stu-id="b8900-106">Compile the code</span></span>  
<span data-ttu-id="b8900-107">Creare un progetto di applicazione console Visual Basic con un' `Imports` istruzione per lo spazio dei nomi System. Linq.</span><span class="sxs-lookup"><span data-stu-id="b8900-107">Create a Visual Basic console application project, with an `Imports` statement for the System.Linq namespace.</span></span>
  
## <a name="see-also"></a><span data-ttu-id="b8900-108">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b8900-108">See also</span></span>

- [<span data-ttu-id="b8900-109">LINQ to Objects (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b8900-109">LINQ to Objects (Visual Basic)</span></span>](linq-to-objects.md)
- <span data-ttu-id="b8900-110">[LINQ and File Directories (Visual Basic)](linq-and-file-directories.md) (LINQ e directory file (Visual Basic))</span><span class="sxs-lookup"><span data-stu-id="b8900-110">[LINQ and File Directories (Visual Basic)](linq-and-file-directories.md)</span></span>

---
title: 'Procedura: Suddividere un file in molti file usando i gruppi (LINQ)'
ms.date: 07/20/2015
ms.assetid: 5e8b2a2b-0b1d-4933-8a2b-03e91dfaf77f
ms.openlocfilehash: f6b11ab4b4fe11dbf1cb4cf07654b5ef3f6785ad
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397713"
---
# <a name="how-to-split-a-file-into-many-files-by-using-groups-linq-visual-basic"></a><span data-ttu-id="1f729-102">Procedura: suddividere un file in molti file usando i gruppi (LINQ) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="1f729-102">How to: Split a File Into Many Files by Using Groups (LINQ) (Visual Basic)</span></span>

<span data-ttu-id="1f729-103">Questo esempio illustra un modo per unire il contenuto di due file e creare quindi un set di nuovi file in cui i dati sono organizzati in modo diverso.</span><span class="sxs-lookup"><span data-stu-id="1f729-103">This example shows one way to merge the contents of two files and then create a set of new files that organize the data in a new way.</span></span>

### <a name="to-create-the-data-files"></a><span data-ttu-id="1f729-104">Per creare i file di dati</span><span class="sxs-lookup"><span data-stu-id="1f729-104">To create the data files</span></span>

1. <span data-ttu-id="1f729-105">Copiare i nomi seguenti in un file di testo denominato names1.txt e salvarlo nella cartella del progetto:</span><span class="sxs-lookup"><span data-stu-id="1f729-105">Copy these names into a text file that is named names1.txt and save it in your project folder:</span></span>

    ```text
    Bankov, Peter
    Holm, Michael
    Garcia, Hugo
    Potra, Cristina
    Noriega, Fabricio
    Aw, Kam Foo
    Beebe, Ann
    Toyoshima, Tim
    Guy, Wey Yuan
    Garcia, Debra
    ```

2. <span data-ttu-id="1f729-106">Copiare i nomi seguenti in un file di testo denominato names2.txt e salvarlo nella cartella del progetto. Si noti che i due file hanno alcuni nomi in comune.</span><span class="sxs-lookup"><span data-stu-id="1f729-106">Copy these names into a text file that is named names2.txt and save it in your project folder: Note that the two files have some names in common.</span></span>

    ```text
    Liu, Jinghao
    Bankov, Peter
    Holm, Michael
    Garcia, Hugo
    Beebe, Ann
    Gilchrist, Beth
    Myrcha, Jacek
    Giakoumakis, Leo
    McLin, Nkenge
    El Yassir, Mehdi
    ```

## <a name="example"></a><span data-ttu-id="1f729-107">Esempio</span><span class="sxs-lookup"><span data-stu-id="1f729-107">Example</span></span>

```vb
Class SplitWithGroups

    Shared Sub Main()

        Dim fileA As String() = System.IO.File.ReadAllLines("../../../names1.txt")
        Dim fileB As String() = System.IO.File.ReadAllLines("../../../names2.txt")

        ' Concatenate and remove duplicate names based on
        Dim mergeQuery As IEnumerable(Of String) = fileA.Union(fileB)

        ' Group the names by the first letter in the last name
        Dim groupQuery = From name In mergeQuery
                     Let n = name.Split(New Char() {","})
                     Order By n(0)
                     Group By groupKey = n(0)(0)
                     Into groupName = Group

        ' Create a new file for each group that was created
        ' Note that nested foreach loops are required to access
        ' individual items with each group.
        For Each gGroup In groupQuery
            Dim fileName As String = "..'..'..'testFile_" & gGroup.groupKey & ".txt"
            Dim sw As New System.IO.StreamWriter(fileName)
            Console.WriteLine(gGroup.groupKey)
            For Each item In gGroup.groupName
                Console.WriteLine("   " & item.name)
                sw.WriteLine(item.name)
            Next
            sw.Close()
        Next

        ' Keep console window open in debug mode.
        Console.WriteLine("Files have been written. Press any key to exit.")
        Console.ReadKey()

    End Sub
End Class
' Console Output:
' A
'    Aw, Kam Foo
' B
'    Bankov, Peter
'    Beebe, Ann
' E
'    El Yassir, Mehdi
' G
'    Garcia, Hugo
'    Garcia, Debra
'    Giakoumakis, Leo
'    Gilchrist, Beth
'    Guy, Wey Yuan
' H
'    Holm, Michael
' L
'    Liu, Jinghao
' M
'    McLin, Nkenge
'    Myrcha, Jacek
' N
'    Noriega, Fabricio
' P
'    Potra, Cristina
' T
'    Toyoshima, Tim
```

<span data-ttu-id="1f729-108">Il programma scrive un file separato per ogni gruppo nella stessa cartella dei file di dati.</span><span class="sxs-lookup"><span data-stu-id="1f729-108">The program writes a separate file for each group in the same folder as the data files.</span></span>

## <a name="compile-the-code"></a><span data-ttu-id="1f729-109">Compilare il codice</span><span class="sxs-lookup"><span data-stu-id="1f729-109">Compile the code</span></span>

<span data-ttu-id="1f729-110">Creare un progetto di applicazione console Visual Basic con un' `Imports` istruzione per lo spazio dei nomi System. Linq.</span><span class="sxs-lookup"><span data-stu-id="1f729-110">Create a Visual Basic console application project, with an `Imports` statement for the System.Linq namespace.</span></span>

## <a name="see-also"></a><span data-ttu-id="1f729-111">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1f729-111">See also</span></span>

- <span data-ttu-id="1f729-112">[LINQ and Strings (Visual Basic)](linq-and-strings.md) (LINQ e le stringhe (Visual Basic))</span><span class="sxs-lookup"><span data-stu-id="1f729-112">[LINQ and Strings (Visual Basic)](linq-and-strings.md)</span></span>
- <span data-ttu-id="1f729-113">[LINQ and File Directories (Visual Basic)](linq-and-file-directories.md) (LINQ e directory file (Visual Basic))</span><span class="sxs-lookup"><span data-stu-id="1f729-113">[LINQ and File Directories (Visual Basic)](linq-and-file-directories.md)</span></span>

---
title: 'Procedura: Eseguire una query per trovare frasi che contengono un set definito di parole (LINQ)'
ms.date: 07/20/2015
ms.assetid: a5ae8ced-61fe-4c10-bb8a-95630e50f603
ms.openlocfilehash: ce88bf001346f90eb9b08ca1ff14afc7dcb04fa0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397960"
---
# <a name="how-to-query-for-sentences-that-contain-a-specified-set-of-words-linq-visual-basic"></a>Procedura: eseguire una query per trovare frasi che contengono un set definito di parole (LINQ) (Visual Basic)

Questo esempio illustra come trovare frasi in un file di testo che contengono corrispondenze per ogni set di parole specificato. Sebbene la matrice dei termini di ricerca sia hardcoded in questo esempio, può essere anche popolata in modo dinamico durante il runtime. In questo esempio la query restituisce le frasi che contengono le parole "Historically", "data" e "integrated".

## <a name="example"></a>Esempio

```vb
Class FindSentences

    Shared Sub Main()
        Dim text As String = "Historically, the world of data and the world of objects " &
        "have not been well integrated. Programmers work in C# or Visual Basic " &
        "and also in SQL or XQuery. On the one side are concepts such as classes, " &
        "objects, fields, inheritance, and .NET Framework APIs. On the other side " &
        "are tables, columns, rows, nodes, and separate languages for dealing with " &
        "them. Data types often require translation between the two worlds; there are " &
        "different standard functions. Because the object world has no notion of query, a " &
        "query can only be represented as a string without compile-time type checking or " &
        "IntelliSense support in the IDE. Transferring data from SQL tables or XML trees to " &
        "objects in memory is often tedious and error-prone."

        ' Split the text block into an array of sentences.
        Dim sentences As String() = text.Split(New Char() {".", "?", "!"})

        ' Define the search terms. This list could also be dynamically populated at runtime
        Dim wordsToMatch As String() = {"Historically", "data", "integrated"}

        ' Find sentences that contain all the terms in the wordsToMatch array
        ' Note that the number of terms to match is not specified at compile time
        Dim sentenceQuery = From sentence In sentences
                            Let w = sentence.Split(New Char() {" ", ",", ".", ";", ":"},
                                                   StringSplitOptions.RemoveEmptyEntries)
                            Where w.Distinct().Intersect(wordsToMatch).Count = wordsToMatch.Count()
                            Select sentence

        ' Execute the query
        For Each str As String In sentenceQuery
            Console.WriteLine(str)
        Next

        ' Keep console window open in debug mode.
        Console.WriteLine("Press any key to exit.")
        Console.ReadKey()
    End Sub

End Class
' Output:
' Historically, the world of data and the world of objects have not been well integrated
```

La query funziona suddividendo prima il testo in frasi e quindi suddividendo le frasi in una matrice di stringhe contenenti ogni parola. Per ognuna di queste matrici, il metodo <xref:System.Linq.Enumerable.Distinct%2A> rimuove tutte le parole duplicate e quindi la query esegue un'operazione <xref:System.Linq.Enumerable.Intersect%2A> sulla matrice di parole e sulla matrice `wordsToMatch`. Se il conteggio dell'intersezione corrisponde al conteggio della matrice `wordsToMatch`, significa che sono state trovate tutte le parole e viene restituita la frase originale.

Nella chiamata a <xref:System.String.Split%2A> vengono usati i segni di punteggiatura come separatori in modo da rimuoverli dalla stringa. Se questa operazione non è stata eseguita, è possibile ad esempio avere una stringa "Historically" che non corrisponde a "Historically" nella matrice `wordsToMatch`. È possibile che sia necessario usare altri separatori, a seconda dei tipi di punteggiatura individuati nel testo di origine.

## <a name="compile-the-code"></a>Compilare il codice

Creare un progetto di applicazione console Visual Basic con un' `Imports` istruzione per lo spazio dei nomi System. Linq.

## <a name="see-also"></a>Vedere anche

- [LINQ and Strings (Visual Basic)](linq-and-strings.md) (LINQ e le stringhe (Visual Basic))

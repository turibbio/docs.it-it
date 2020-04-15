---
title: Come analizzare le stringhe utilizzando String.Split (Guida di C
description: String.Split restituisce una matrice di stringhe divise da un set di delimitatori e rappresenta un modo semplice per analizzare le stringhe.
ms.date: 01/03/2018
helpviewer_keywords:
- splitting strings [C#]
- Split method [C#]
- strings [C#], splitting
- parse strings
ms.assetid: 729c2923-4169-41c6-9c90-ef176c1e2953
ms.custom: mvc
ms.openlocfilehash: cf8307517213b54041b272843232eb595660b2e9
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389500"
---
# <a name="how-to-parse-strings-using-stringsplit-in-c"></a>Come analizzare le stringhe utilizzando String.Split in CHow to parse strings using String.Split in C\#

Il metodo <xref:System.String.Split%2A?displayProperty=nameWithType> crea una matrice di sottostringhe dividendo la stringa di input in base a uno o più delimitatori. È spesso il modo più semplice per separare una stringa in corrispondenza della fine delle parole. Questo metodo viene usato anche per dividere le stringhe in corrispondenza di altri caratteri o di altre stringhe specifiche.

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

Il codice seguente divide una frase comune in una matrice di stringhe per ogni parola.

[!code-csharp-interactive[split strings on word boundaries](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#1)]

Ogni istanza di un carattere separatore genera un valore nella matrice restituita. Caratteri separatori consecutivi generano una stringa vuota come valore nella matrice restituita. È possibile vedere come viene creata una stringa vuota nell'esempio seguente, che usa il carattere spazio come separatore.

[!code-csharp-interactive[split strings with repeated separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#2)]

Questo comportamento semplifica i formati, ad esempio i file con valori delimitati da virgole (CSV) che rappresentano dati tabulari. Due virgole consecutive rappresentano una colonna vuota.

È possibile passare un parametro <xref:System.StringSplitOptions.RemoveEmptyEntries?displayProperty=nameWithType> facoltativo per escludere tutte le stringhe vuote nella matrice restituita. Per un'elaborazione più complessa della raccolta restituita, è possibile modificare la sequenza di risultati tramite [LINQ](../programming-guide/concepts/linq/index.md).

<xref:System.String.Split%2A?displayProperty=nameWithType> può usare più caratteri separatori.
L'esempio seguente usa spazi, virgole, punti, due punti e tabulazioni, tutti passati a <xref:System.String.Split%2A> in una matrice contenente questi caratteri di separazione.
Il ciclo nella parte inferiore del codice visualizza ogni parola nella matrice restituita.  

[!code-csharp-interactive[split strings using multiple separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#3)]

Istanze consecutive di un separatore generano una stringa vuota nella matrice di output:

[!code-csharp-interactive[split strings using multiple consecutive separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#4)]

<xref:System.String.Split%2A?displayProperty=nameWithType> può accettare una matrice di stringhe (sequenze di caratteri, anziché caratteri singoli, con la funzione di separatori per l'analisi della stringa di destinazione).  
  
[!code-csharp-interactive[split strings using strings as separators](../../../samples/snippets/csharp/how-to/strings/ParseStringsUsingSplit.cs#5)]

È possibile provare questi esempi esaminando il codice nel repository [GitHub](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/how-to/strings). Oppure è possibile scaricare gli esempi [come file ZIP](../../../samples/snippets/csharp/how-to/strings.zip).

## <a name="see-also"></a>Vedere anche

- [Guida alla programmazione in C](../programming-guide/index.md)
- [Stringhe](../programming-guide/strings/index.md)
- [Espressioni regolari .NET](../../standard/base-types/regular-expressions.md)

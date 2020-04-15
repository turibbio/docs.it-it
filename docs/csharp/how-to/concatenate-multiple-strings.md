---
title: Come concatenare più stringhe (Guida di C
description: Esistono diversi modi per concatenare le stringhe in C#. Di seguito sono descritte le opzioni e le motivazioni delle diverse scelte.
ms.date: 02/20/2018
helpviewer_keywords:
- joining strings [C#]
- concatenating strings [C#]
- strings [C#], concatenation
ms.assetid: 8e16736f-4096-4f3f-be0f-9d4c3ff63520
ms.openlocfilehash: bbdeba4ee3526140de29ac0d7c97e9a593729d47
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389528"
---
# <a name="how-to-concatenate-multiple-strings-c-guide"></a>Come concatenare più stringhe (Guida di C

La *concatenazione* è il processo di aggiunta di una stringa alla fine di un'altra stringa. Le stringhe vengono concatenate usando l'operatore `+`. Per i valori letterali e le costanti di stringa, la concatenazione viene eseguita in fase di compilazione; non viene eseguita alcuna concatenazione in fase di esecuzione. Per le variabili di stringa, la concatenazione viene eseguita solo in fase di esecuzione.

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

L'esempio seguente usa la concatenazione per suddividere un valore letterale di stringa lungo in stringhe più piccole per migliorare la leggibilità nel codice sorgente. Queste parti sono concatenate in una singola stringa in fase di compilazione. Non c'è alcun impatto sulle prestazioni in fase di esecuzione, indipendentemente dal numero di stringhe coinvolte.  
  
 [!code-csharp-interactive[Combining strings at compile time](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#1)]  

Per concatenare le variabili stringa, è possibile utilizzare gli `+` operatori `+=` o , l'interpolazione di [stringa](../language-reference/tokens/interpolated.md) o i <xref:System.String.Format%2A?displayProperty=nameWithType>metodi , <xref:System.String.Concat%2A?displayProperty=nameWithType>, <xref:System.String.Join%2A?displayProperty=nameWithType> o <xref:System.Text.StringBuilder.Append%2A?displayProperty=nameWithType> . L'operatore `+` è facile da usare e rende il codice intuitivo. Anche se si usano diversi operatori `+` in un'unica istruzione, il contenuto della stringa viene copiato una sola volta. Il codice seguente mostra esempi dell'uso degli operatori `+` e `+=` per concatenare le stringhe:

[!code-csharp-interactive[combining strings using +](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#2)]  

In alcune espressioni risulta più semplice concatenare le stringhe usando l'interpolazione di stringhe, come illustrato nel codice seguente:
  
[!code-csharp-interactive[building strings using string interpolation](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#3)]  
  
> [!NOTE]
> Nelle operazioni di concatenazione di stringhe il compilatore C# tratta una stringa Null come se fosse una stringa vuota.

Un altro metodo per concatenare le stringhe è <xref:System.String.Format%2A?displayProperty=nameWithType>. Questo metodo è utile quando si compila una stringa da un numero ridotto di stringhe dei componenti.

In altri casi, è possibile combinare stringhe in un ciclo in cui non si conosce il numero di stringhe di origine che si sta combinando e il numero effettivo di stringhe di origine può essere elevato. La classe <xref:System.Text.StringBuilder> è stata progettata per questi scenari. Il codice seguente usa il metodo <xref:System.Text.StringBuilder.Append%2A> della classe <xref:System.Text.StringBuilder> per concatenare le stringhe.  
  
[!code-csharp-interactive[string concatenation using string builder](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#4)]  

Ulteriori informazioni sui motivi per scegliere la [concatenazione `StringBuilder` di stringhe o la classe](xref:System.Text.StringBuilder#StringAndSB).

Un'altra opzione per unire le stringhe di una raccolta consiste nell'usare il metodo <xref:System.String.Concat%2A?displayProperty=nameWithType>. Utilizzare <xref:System.String.Join%2A?displayProperty=nameWithType> il metodo se le stringhe di origine devono essere separate da un delimitatore. Il codice seguente combina una matrice di parole con entrambi i metodi:

[!code-csharp-interactive[concatenation of string collection](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#5)]

Infine, è possibile usare [LINQ](../programming-guide/concepts/linq/index.md) e il metodo <xref:System.Linq.Enumerable.Aggregate%2A?displayProperty=nameWithType> per unire le stringhe di una raccolta. Questo metodo combina le stringhe di origine usando un'espressione lambda. L'espressione lambda esegue le operazioni necessarie per aggiungere ogni stringa all'accumulo esistente. L'esempio seguente combina una matrice di parole aggiungendo uno spazio tra ogni parola nella matrice:

[!code-csharp-interactive[string concatenation using LINQ expressions](../../../samples/snippets/csharp/how-to/strings/Concatenate.cs#6)]  

È possibile provare questi esempi esaminando il [codice di esempio](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/how-to/strings). In alternativa, è possibile scaricare gli esempi [come file zip](../../../samples/snippets/csharp/how-to/strings.zip).

## <a name="see-also"></a>Vedere anche

- <xref:System.String>
- <xref:System.Text.StringBuilder>
- [Guida alla programmazione in C](../programming-guide/index.md)
- [Stringhe](../programming-guide/strings/index.md)

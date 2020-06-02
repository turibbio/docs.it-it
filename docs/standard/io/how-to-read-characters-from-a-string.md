---
title: 'Procedura: leggere caratteri da una stringa'
ms.date: 01/21/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- reading characters from strings
- data streams, reading characters from string
- I/O [.NET Framework], reading characters from strings
- reading data, strings
- streams, reading characters from string
ms.assetid: 27ea5e52-6db8-42d8-980a-50bcfc7fd270
ms.openlocfilehash: 6d32e9c5f89dba7590958bae6cc0489f104cd19a
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291773"
---
# <a name="how-to-read-characters-from-a-string"></a><span data-ttu-id="83ef4-102">Procedura: leggere caratteri da una stringa</span><span class="sxs-lookup"><span data-stu-id="83ef4-102">How to: Read characters from a string</span></span>
<span data-ttu-id="83ef4-103">Gli esempi di codice seguenti illustrano come leggere i caratteri in modo sincrono o asincrono da una stringa.</span><span class="sxs-lookup"><span data-stu-id="83ef4-103">The following code examples show how to read characters synchronously or asynchronously from a string.</span></span>  
  
## <a name="example-read-characters-synchronously"></a><span data-ttu-id="83ef4-104">Esempio: leggere i caratteri in modo sincrono</span><span class="sxs-lookup"><span data-stu-id="83ef4-104">Example: Read characters synchronously</span></span>
 <span data-ttu-id="83ef4-105">Questo esempio legge 13 caratteri in modo sincrono da una stringa, li archivia in una matrice e li visualizza.</span><span class="sxs-lookup"><span data-stu-id="83ef4-105">This example reads 13 characters synchronously from a string, stores them in an array, and displays them.</span></span> <span data-ttu-id="83ef4-106">Legge quindi i caratteri rimanenti nella stringa, li archivia nella matrice a partire dal sesto elemento e visualizza il contenuto della matrice.</span><span class="sxs-lookup"><span data-stu-id="83ef4-106">The example then reads the rest of the characters in the string, stores them in the array starting at the sixth element, and displays the contents of the array.</span></span>  
  
 [!code-csharp[Conceptual.StringReader#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.stringreader/cs/source.cs#1)]
 [!code-vb[Conceptual.StringReader#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.stringreader/vb/source.vb#1)]  
  
## <a name="example-read-characters-asynchronously"></a><span data-ttu-id="83ef4-107">Esempio: leggere i caratteri in modo asincrono</span><span class="sxs-lookup"><span data-stu-id="83ef4-107">Example: Read characters asynchronously</span></span>  
 <span data-ttu-id="83ef4-108">L'esempio successivo è il code-behind di un'app WPF.</span><span class="sxs-lookup"><span data-stu-id="83ef4-108">The next example is the code behind a WPF app.</span></span> <span data-ttu-id="83ef4-109">Al caricamento della finestra, l'esempio legge in modo asincrono tutti i caratteri da un controllo <xref:System.Windows.Controls.TextBox> e li archivia in una matrice.</span><span class="sxs-lookup"><span data-stu-id="83ef4-109">On window load, the example asynchronously reads all characters from a <xref:System.Windows.Controls.TextBox> control and stores them in an array.</span></span> <span data-ttu-id="83ef4-110">Scrive quindi in modo asincrono ogni lettera o spazio su una riga separata di un controllo <xref:System.Windows.Controls.TextBlock>.</span><span class="sxs-lookup"><span data-stu-id="83ef4-110">It then asynchronously writes each letter or white-space character to a separate line of a <xref:System.Windows.Controls.TextBlock> control.</span></span>  
  
 [!code-csharp[Conceptual.StringReader#2](../../../samples/snippets/csharp/VS_Snippets_Wpf/StringReaderWriter/MainWindow.xaml.cs)]
 [!code-vb[Conceptual.StringReader#2](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StringReaderWriter/MainWindow.xaml.vb)]  
  
## <a name="see-also"></a><span data-ttu-id="83ef4-111">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="83ef4-111">See also</span></span>

- <xref:System.IO.StringReader>  
- <xref:System.IO.StringReader.Read%2A?displayProperty=nameWithType>  
- [<span data-ttu-id="83ef4-112">I/O di file asincrono</span><span class="sxs-lookup"><span data-stu-id="83ef4-112">Asynchronous file I/O</span></span>](asynchronous-file-i-o.md)  
- <span data-ttu-id="83ef4-113">[Procedura: creare un elenco di directory](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/5cf8zcfh(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="83ef4-113">[How to: Create a directory listing](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/5cf8zcfh(v=vs.100))</span></span>  
- [<span data-ttu-id="83ef4-114">Procedura: leggere e scrivere in un file di dati appena creato</span><span class="sxs-lookup"><span data-stu-id="83ef4-114">How to: Read and write to a newly created data file</span></span>](how-to-read-and-write-to-a-newly-created-data-file.md)  
- [<span data-ttu-id="83ef4-115">Procedura: aprire e accodare un file di log</span><span class="sxs-lookup"><span data-stu-id="83ef4-115">How to: Open and append to a log file</span></span>](how-to-open-and-append-to-a-log-file.md)  
- [<span data-ttu-id="83ef4-116">Procedura: leggere testo da un file</span><span class="sxs-lookup"><span data-stu-id="83ef4-116">How to: Read text from a file</span></span>](how-to-read-text-from-a-file.md)  
- [<span data-ttu-id="83ef4-117">Procedura: scrivere testo in un file</span><span class="sxs-lookup"><span data-stu-id="83ef4-117">How to: Write text to a file</span></span>](how-to-write-text-to-a-file.md)  
- [<span data-ttu-id="83ef4-118">Procedura: scrivere caratteri in una stringa</span><span class="sxs-lookup"><span data-stu-id="83ef4-118">How to: Write characters to a string</span></span>](how-to-write-characters-to-a-string.md)  
- [<span data-ttu-id="83ef4-119">I/O di file e di flussi</span><span class="sxs-lookup"><span data-stu-id="83ef4-119">File and stream I/O</span></span>](index.md)

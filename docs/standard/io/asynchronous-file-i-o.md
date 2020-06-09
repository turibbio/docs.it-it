---
title: I/O di file asincrono
description: Vedere informazioni sull'I/O di file asincrono in .NET. Informazioni sui metodi asincroni per semplificare le operazioni asincrone, ad esempio ReadAsync, WriteAsync e altro ancora.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- streams, synchronous streams
- asynchronous I/O
- synchronous I/O
- streams, asynchronous streams
- I/O [.NET Framework], asynchronous I/O
- Stream class, synchronous I/O
- data streams, asynchronous streams
- Stream class, asynchronous I/O
- multiple I/O requests
- data streams, synchronous streams
ms.assetid: dbdd55e7-d6b9-4f9e-8abb-ab0edd4457f7
ms.openlocfilehash: 9506a366b6f1e363ec13550e5ed68c7176dd4d0a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598619"
---
# <a name="asynchronous-file-io"></a>I/O di file asincrono

Le operazioni asincrone consentono di eseguire operazioni di I/O a elevato utilizzo di risorse senza bloccare il thread principale. Questa considerazione sulle prestazioni è particolarmente importante in un'app di Windows 8. x Store o in un'app desktop in cui un'operazione di flusso che richiede molto tempo può bloccare il thread dell'interfaccia utente e fare in modo che l'app appaia come se non fosse funzionante.

A partire da .NET Framework 4.5, i tipi di I/O includono metodi async per semplificare le operazioni asincrone. Un metodo asincrono contiene `Async` nel nome, ad esempio <xref:System.IO.Stream.ReadAsync%2A>, <xref:System.IO.Stream.WriteAsync%2A>, <xref:System.IO.Stream.CopyToAsync%2A>, <xref:System.IO.Stream.FlushAsync%2A>, <xref:System.IO.TextReader.ReadLineAsync%2A>e <xref:System.IO.TextReader.ReadToEndAsync%2A>. Questi metodi asincroni sono implementati nelle classi di flusso, come <xref:System.IO.Stream>, <xref:System.IO.FileStream>e <xref:System.IO.MemoryStream>, e nelle classi usate per la lettura o la scrittura nei flussi, come <xref:System.IO.TextReader> e <xref:System.IO.TextWriter>.

In .NET Framework 4 e versioni precedenti è necessario usare metodi quali <xref:System.IO.Stream.BeginRead%2A> e <xref:System.IO.Stream.EndRead%2A> per implementare operazioni di I/O asincrone. Questi metodi sono ancora disponibili in .NET Framework 4.5 per supportare il codice legacy. Tuttavia, i metodi async consentono di implementare più facilmente le operazioni di I/O asincrone.

C# e Visual Basic hanno ognuno due parole chiave per la programmazione asincrona:

- Il modificatore`Async` (Visual Basic) o `async` (C#), che viene usato per contrassegnare un metodo contenente un'operazione asincrona.

- L'operatore`Await` (Visual Basic) o `await` (C#), che viene applicato al risultato di un metodo async.

Per implementare le operazioni di I/O asincrone, usare queste parole chiave con i metodi async, come illustrato negli esempi seguenti. Per altre informazioni, vedere [Programmazione asincrona con async e await (C#)](../../csharp/programming-guide/concepts/async/index.md) o [Programmazione asincrona con Async e Await (Visual Basic)](../../visual-basic/programming-guide/concepts/async/index.md).

L'esempio seguente mostra come usare due oggetti <xref:System.IO.FileStream> per copiare i file in modo asincrono da una directory a un'altra. Si noti che il gestore eventi <xref:System.Web.UI.WebControls.Button.Click> per il controllo <xref:System.Windows.Controls.Button> è contrassegnato con il modificatore `async` perché chiama un metodo asincrono.

[!code-csharp[Asynchronous_File_IO_async#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Asynchronous_File_IO_async/cs/example.cs#1)]
[!code-vb[Asynchronous_File_IO_async#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Asynchronous_File_IO_async/vb/example.vb#1)]

L'esempio seguente è simile a quello precedente ma usa gli oggetti <xref:System.IO.StreamReader> e <xref:System.IO.StreamWriter> per leggere e scrivere il contenuto di un file di testo in modo asincrono.

[!code-csharp[Asynchronous_File_IO_async#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Asynchronous_File_IO_async/cs/example2.cs#2)]
[!code-vb[Asynchronous_File_IO_async#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Asynchronous_File_IO_async/vb/example2.vb#2)]

L'esempio seguente mostra il file code-behind e il file XAML usati per aprire un file come <xref:System.IO.Stream> in un'app di Windows 8. x Store e leggerne il contenuto usando un'istanza della <xref:System.IO.StreamReader> classe. Usa i metodi asincroni per aprire il file come flusso e leggerne il contenuto.

[!code-csharp[System.IO.WindowsRuntimeStorageExtensions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/cs/blankpage.xaml.cs#2)]
[!code-vb[System.IO.WindowsRuntimeStorageExtensions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/vb/blankpage.xaml.vb#2)]

[!code-xaml[System.IO.WindowsRuntimeStorageExtensions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/cs/blankpage.xaml#1)]

## <a name="see-also"></a>Vedere anche

- <xref:System.IO.Stream>
- [I/O di file e di flussi](index.md)
- [Programmazione asincrona con Async e await (C#)](../../csharp/programming-guide/concepts/async/index.md)
- [Programmazione asincrona con Async e Await (Visual Basic)](../../visual-basic/programming-guide/concepts/async/index.md)

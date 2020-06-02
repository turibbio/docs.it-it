---
title: 'Procedura: copiare le directory'
ms.date: 12/27/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- directory copying
- I/O [.NET Framework], copying directories
- subdirectory copying
- copying directories
- directories [.NET Framework], copying
ms.assetid: 5a969765-e5f8-4b4e-977e-90e2b0a1fe3c
ms.openlocfilehash: f71f428037f33fdbc692ca2f02a4c767998d684e
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288576"
---
# <a name="how-to-copy-directories"></a><span data-ttu-id="bd6e6-102">Procedura: copiare le directory</span><span class="sxs-lookup"><span data-stu-id="bd6e6-102">How to: Copy directories</span></span>
<span data-ttu-id="bd6e6-103">Questo argomento illustra come usare le classi di I/O per copiare in modalità sincrona il contenuto di una directory in un'altra posizione.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-103">This topic demonstrates how to use I/O classes to synchronously copy the contents of a directory to another location.</span></span>

<span data-ttu-id="bd6e6-104">Per un esempio di copia di file asincrona, vedere [I/O di file asincrono](asynchronous-file-i-o.md).</span><span class="sxs-lookup"><span data-stu-id="bd6e6-104">For an example of asynchronous file copy, see [Asynchronous file I/O](asynchronous-file-i-o.md).</span></span>

<span data-ttu-id="bd6e6-105">In questo esempio le sottodirectory vengono copiate impostando l'elemento `copySubDirs` del metodo `DirectoryCopy` su `true`.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-105">This example copies subdirectories by setting the `copySubDirs` of the `DirectoryCopy` method to `true`.</span></span> <span data-ttu-id="bd6e6-106">Il metodo `DirectoryCopy` copia le sottodirectory in modo ricorsivo chiamando se stesso in ogni sottodirectory finché non ci sono più sottodirectory da copiare.</span><span class="sxs-lookup"><span data-stu-id="bd6e6-106">The `DirectoryCopy` method recursively copies subdirectories by calling itself on each subdirectory until there are no more to copy.</span></span>  
  
## <a name="example"></a><span data-ttu-id="bd6e6-107">Esempio</span><span class="sxs-lookup"><span data-stu-id="bd6e6-107">Example</span></span>  
 [!code-csharp[System.IO.Directory_Copy#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Directory_Copy/cs/program.cs#1)]
 [!code-vb[System.IO.Directory_Copy#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Directory_Copy/vb/Program.vb#1)]  
  
[!INCLUDE [localized code comments](../../../includes/code-comments-loc.md)]

## <a name="see-also"></a><span data-ttu-id="bd6e6-108">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="bd6e6-108">See also</span></span>

- <xref:System.IO.FileInfo>
- <xref:System.IO.DirectoryInfo>
- <xref:System.IO.FileStream>
- [<span data-ttu-id="bd6e6-109">I/O di file e di flussi</span><span class="sxs-lookup"><span data-stu-id="bd6e6-109">File and stream I/O</span></span>](index.md)
- [<span data-ttu-id="bd6e6-110">Attività di I/O comuni</span><span class="sxs-lookup"><span data-stu-id="bd6e6-110">Common I/O tasks</span></span>](common-i-o-tasks.md)
- [<span data-ttu-id="bd6e6-111">I/O di file asincrono</span><span class="sxs-lookup"><span data-stu-id="bd6e6-111">Asynchronous file I/O</span></span>](asynchronous-file-i-o.md)

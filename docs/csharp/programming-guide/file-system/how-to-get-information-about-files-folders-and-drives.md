---
title: Come ottenere informazioni su file, cartelle e unità-Guida per programmatori C#
ms.date: 07/20/2015
helpviewer_keywords:
- files [C#], getting information about
ms.assetid: 22fc2da6-5494-405b-995e-c0b99142a93e
ms.openlocfilehash: 32aced17634a1406e2fce0af9c2a92f7a5eb9b40
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241617"
---
# <a name="how-to-get-information-about-files-folders-and-drives--c-programming-guide"></a><span data-ttu-id="47862-102">Come ottenere informazioni su file, cartelle e unità (Guida per programmatori C#)</span><span class="sxs-lookup"><span data-stu-id="47862-102">How to get information about files, folders, and drives  (C# Programming Guide)</span></span>
<span data-ttu-id="47862-103">In .NET è possibile accedere alle informazioni file system usando le classi seguenti:</span><span class="sxs-lookup"><span data-stu-id="47862-103">In .NET, you can access file system information by using the following classes:</span></span>  
  
- <xref:System.IO.FileInfo?displayProperty=nameWithType>  
  
- <xref:System.IO.DirectoryInfo?displayProperty=nameWithType>  
  
- <xref:System.IO.DriveInfo?displayProperty=nameWithType>  
  
- <xref:System.IO.Directory?displayProperty=nameWithType>  
  
- <xref:System.IO.File?displayProperty=nameWithType>  
  
 <span data-ttu-id="47862-104">Le classi <xref:System.IO.FileInfo> e <xref:System.IO.DirectoryInfo> rappresentano un file o una directory e contengono proprietà che espongono molti degli attributi di file supportati dal file system NTFS.</span><span class="sxs-lookup"><span data-stu-id="47862-104">The <xref:System.IO.FileInfo> and <xref:System.IO.DirectoryInfo> classes represent a file or directory and contain properties that expose many of the file attributes that are supported by the NTFS file system.</span></span> <span data-ttu-id="47862-105">Contengono anche i metodi per l'apertura, la chiusura, lo spostamento e l'eliminazione di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="47862-105">They also contain methods for opening, closing, moving, and deleting files and folders.</span></span> <span data-ttu-id="47862-106">È possibile creare istanze di queste classi passando al costruttore una stringa che rappresenta il nome del file, della cartella o dell'unità:</span><span class="sxs-lookup"><span data-stu-id="47862-106">You can create instances of these classes by passing a string that represents the name of the file, folder, or drive in to the constructor:</span></span>  
  
```csharp  
System.IO.DriveInfo di = new System.IO.DriveInfo(@"C:\");  
```  
  
 <span data-ttu-id="47862-107">È anche possibile ottenere i nomi di file, cartelle o unità tramite chiamate a <xref:System.IO.DirectoryInfo.GetDirectories%2A?displayProperty=nameWithType>, <xref:System.IO.DirectoryInfo.GetFiles%2A?displayProperty=nameWithType> e <xref:System.IO.DriveInfo.RootDirectory%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="47862-107">You can also obtain the names of files, folders, or drives by using calls to <xref:System.IO.DirectoryInfo.GetDirectories%2A?displayProperty=nameWithType>, <xref:System.IO.DirectoryInfo.GetFiles%2A?displayProperty=nameWithType>, and <xref:System.IO.DriveInfo.RootDirectory%2A?displayProperty=nameWithType>.</span></span>  
  
 <span data-ttu-id="47862-108">Le classi <xref:System.IO.Directory?displayProperty=nameWithType> e <xref:System.IO.File?displayProperty=nameWithType> forniscono metodi statici per il recupero di informazioni su file e directory.</span><span class="sxs-lookup"><span data-stu-id="47862-108">The <xref:System.IO.Directory?displayProperty=nameWithType> and <xref:System.IO.File?displayProperty=nameWithType> classes provide static methods for retrieving information about directories and files.</span></span>  
  
## <a name="example"></a><span data-ttu-id="47862-109">Esempio</span><span class="sxs-lookup"><span data-stu-id="47862-109">Example</span></span>  
 <span data-ttu-id="47862-110">L'esempio seguente illustra vari modi per accedere alle informazioni su file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="47862-110">The following example shows various ways to access information about files and folders.</span></span>  
  
 [!code-csharp[csFilesandFolders#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#6)]  
  
## <a name="robust-programming"></a><span data-ttu-id="47862-111">Programmazione efficiente</span><span class="sxs-lookup"><span data-stu-id="47862-111">Robust Programming</span></span>  
 <span data-ttu-id="47862-112">Quando si elaborano stringhe di percorso specificate dall'utente, occorre gestire anche le eccezioni per le condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="47862-112">When you process user-specified path strings, you should also handle exceptions for the following conditions:</span></span>  
  
- <span data-ttu-id="47862-113">Il nome file non è valido.</span><span class="sxs-lookup"><span data-stu-id="47862-113">The file name is malformed.</span></span> <span data-ttu-id="47862-114">Ad esempio, contiene caratteri non validi o solo spazi vuoti.</span><span class="sxs-lookup"><span data-stu-id="47862-114">For example, it contains invalid characters or only white space.</span></span>  
  
- <span data-ttu-id="47862-115">Il nome del file è Null.</span><span class="sxs-lookup"><span data-stu-id="47862-115">The file name is null.</span></span>  
  
- <span data-ttu-id="47862-116">La lunghezza del nome del file è maggiore della lunghezza massima definita nel sistema.</span><span class="sxs-lookup"><span data-stu-id="47862-116">The file name is longer than the system-defined maximum length.</span></span>  
  
- <span data-ttu-id="47862-117">Il nome del file contiene i due punti (:).</span><span class="sxs-lookup"><span data-stu-id="47862-117">The file name contains a colon (:).</span></span>  
  
 <span data-ttu-id="47862-118">Se l'applicazione non ha autorizzazioni sufficienti per leggere il file specificato, il metodo `Exists` restituisce `false` indipendentemente dal fatto che il percorso esista. Il metodo non genera un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="47862-118">If the application does not have sufficient permissions to read the specified file, the `Exists` method returns `false` regardless of whether a path exists; the method does not throw an exception.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="47862-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="47862-119">See also</span></span>

- <xref:System.IO?displayProperty=nameWithType>
- [<span data-ttu-id="47862-120">Guida per programmatori C#</span><span class="sxs-lookup"><span data-stu-id="47862-120">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="47862-121">File system e Registro di sistema (Guida per programmatori C#)</span><span class="sxs-lookup"><span data-stu-id="47862-121">File System and the Registry (C# Programming Guide)</span></span>](./index.md)

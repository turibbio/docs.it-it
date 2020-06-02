---
title: 'Procedura: Creare file e directory nello spazio di memorizzazione isolato'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- directories [.NET Framework], isolated storage
- files [.NET Framework], isolated storage
- isolated storage, creating files and directories
- data stores, creating files and directories
- data storage using isolated storage, creating files and directories
- stores, creating files and directories
- storing data using isolated storage, creating files and directories
ms.assetid: 2ca4d2a4-809b-4f00-bc08-bf4a64d3a5c3
ms.openlocfilehash: b74bf62dabe24765e07ffa6820cc1675122a9122
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288550"
---
# <a name="how-to-create-files-and-directories-in-isolated-storage"></a><span data-ttu-id="2cbc7-102">Procedura: Creare file e directory nello spazio di memorizzazione isolato</span><span class="sxs-lookup"><span data-stu-id="2cbc7-102">How to: Create Files and Directories in Isolated Storage</span></span>
<span data-ttu-id="2cbc7-103">Dopo aver ottenuto uno spazio di memorizzazione isolato, è possibile creare directory e file per l'archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-103">After you have obtained an isolated store, you can create directories and files for storing data.</span></span> <span data-ttu-id="2cbc7-104">All'interno di un archivio i nomi di file e directory vengono specificati rispetto alla radice del file system virtuale.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-104">Within a store, file and directory names are specified with respect to the root of the virtual file system.</span></span>  
  
 <span data-ttu-id="2cbc7-105">Per creare una directory, usare il metodo di istanza <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-105">To create a directory, use the <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A?displayProperty=nameWithType> instance method.</span></span> <span data-ttu-id="2cbc7-106">Se si specifica una sottodirectory di una directory che non esiste, vengono create entrambe le directory.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-106">If you specify a subdirectory of an directory that doesn't exist, both directories are created.</span></span> <span data-ttu-id="2cbc7-107">Se si specifica una directory che esiste già, il metodo restituisce risultati senza creare una directory e non viene generata alcuna eccezione.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-107">If you specify a directory that already exists, the method returns without creating a directory, and no exception is thrown.</span></span> <span data-ttu-id="2cbc7-108">Tuttavia, se si specifica un nome di directory che contiene caratteri non validi, viene generata un'eccezione <xref:System.IO.IsolatedStorage.IsolatedStorageException>.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-108">However, if you specify a directory name that contains invalid characters, an <xref:System.IO.IsolatedStorage.IsolatedStorageException> exception is thrown.</span></span>  
  
 <span data-ttu-id="2cbc7-109">Per creare un file, utilizzare il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateFile%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-109">To create a file, use  the <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateFile%2A?displayProperty=nameWithType> method.</span></span>  
  
 <span data-ttu-id="2cbc7-110">Nel sistema operativo Windows i nomi di file e directory dello spazio di memorizzazione isolato non fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-110">In the Windows operating system, isolated storage file and directory names are case-insensitive.</span></span> <span data-ttu-id="2cbc7-111">Di conseguenza, se si crea un file denominato `ThisFile.txt` e quindi un altro file denominato `THISFILE.TXT`, viene creato un solo file.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-111">That is, if you create a file named `ThisFile.txt`, and then create another file named `THISFILE.TXT`, only one file is created.</span></span> <span data-ttu-id="2cbc7-112">Il nome del file mantiene le maiuscole e minuscole originali ai fini della visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-112">The file name keeps its original casing for display purposes.</span></span>  
  
## <a name="example"></a><span data-ttu-id="2cbc7-113">Esempio</span><span class="sxs-lookup"><span data-stu-id="2cbc7-113">Example</span></span>  
 <span data-ttu-id="2cbc7-114">L'esempio di codice seguente mostra come creare file e directory in uno spazio di memorizzazione isolato.</span><span class="sxs-lookup"><span data-stu-id="2cbc7-114">The following code example illustrates how to create files and directories in an isolated store.</span></span>  
  
 [!code-csharp[Conceptual.IsolatedStorage#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source.cs#1)]
 [!code-vb[Conceptual.IsolatedStorage#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="2cbc7-115">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2cbc7-115">See also</span></span>

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>
- [<span data-ttu-id="2cbc7-116">Spazio di memorizzazione isolato</span><span class="sxs-lookup"><span data-stu-id="2cbc7-116">Isolated Storage</span></span>](isolated-storage.md)

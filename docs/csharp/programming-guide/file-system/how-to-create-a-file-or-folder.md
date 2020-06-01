---
title: Come creare un file o una cartella-Guida per programmatori C#
ms.date: 07/20/2015
helpviewer_keywords:
- folders [C#]
- creating files [C#]
- files [C#]
- creating folders [C#]
ms.assetid: 4582ee2d-d72d-4687-bcb9-08d336c62c25
ms.openlocfilehash: 5efe3b7dc600645488816d6f931df57fc236efc9
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241643"
---
# <a name="how-to-create-a-file-or-folder-c-programming-guide"></a><span data-ttu-id="f5c84-102">Come creare un file o una cartella (Guida per programmatori C#)</span><span class="sxs-lookup"><span data-stu-id="f5c84-102">How to create a file or folder (C# Programming Guide)</span></span>
<span data-ttu-id="f5c84-103">A livello di codice è possibile creare una cartella, una sottocartella e un file nella sottocartella e quindi scrivere dati nel file.</span><span class="sxs-lookup"><span data-stu-id="f5c84-103">You can programmatically create a folder on your computer, create a subfolder, create a file in the subfolder, and write data to the file.</span></span>  
  
## <a name="example"></a><span data-ttu-id="f5c84-104">Esempio</span><span class="sxs-lookup"><span data-stu-id="f5c84-104">Example</span></span>  
 [!code-csharp[csFilesandFolders#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#10)]  
  
 <span data-ttu-id="f5c84-105">Se la cartella esiste già, <xref:System.IO.Directory.CreateDirectory%2A> non esegue alcuna operazione e non viene generata alcuna eccezione.</span><span class="sxs-lookup"><span data-stu-id="f5c84-105">If the folder already exists, <xref:System.IO.Directory.CreateDirectory%2A> does nothing, and no exception is thrown.</span></span> <span data-ttu-id="f5c84-106"><xref:System.IO.File.Create%2A?displayProperty=nameWithType>, tuttavia, sostituisce un file esistente con un nuovo file.</span><span class="sxs-lookup"><span data-stu-id="f5c84-106">However, <xref:System.IO.File.Create%2A?displayProperty=nameWithType> replaces an existing file with a new file.</span></span> <span data-ttu-id="f5c84-107">Nell'esempio viene usata un'istruzione `if`-`else` per evitare la sostituzione di un file esistente.</span><span class="sxs-lookup"><span data-stu-id="f5c84-107">The example uses an `if`-`else` statement to prevent an existing file from being replaced.</span></span>  
  
 <span data-ttu-id="f5c84-108">Apportando le modifiche seguenti nell'esempio, è possibile specificare risultati diversi in base all'esistenza o meno di un file con un determinato nome.</span><span class="sxs-lookup"><span data-stu-id="f5c84-108">By making the following changes in the example, you can specify different outcomes based on whether a file with a certain name already exists.</span></span> <span data-ttu-id="f5c84-109">Se il file non esiste, il codice ne crea uno.</span><span class="sxs-lookup"><span data-stu-id="f5c84-109">If such a file doesn't exist, the code creates one.</span></span> <span data-ttu-id="f5c84-110">Se il file esiste, il codice aggiunge i dati a questo.</span><span class="sxs-lookup"><span data-stu-id="f5c84-110">If such a file exists, the code appends data to that file.</span></span>  
  
- <span data-ttu-id="f5c84-111">Specificare un nome file non casuale.</span><span class="sxs-lookup"><span data-stu-id="f5c84-111">Specify a non-random file name.</span></span>  
  
    ```csharp  
    // Comment out the following line.  
    //string fileName = System.IO.Path.GetRandomFileName();  
  
    // Replace that line with the following assignment.  
    string fileName = "MyNewFile.txt";  
    ```  
  
- <span data-ttu-id="f5c84-112">Sostituire l'istruzione `if`-`else` con l'istruzione `using` riportata nel codice seguente.</span><span class="sxs-lookup"><span data-stu-id="f5c84-112">Replace the `if`-`else` statement with the `using` statement in the following code.</span></span>  
  
    ```csharp  
    using (System.IO.FileStream fs = new System.IO.FileStream(pathString, FileMode.Append))
    {  
        for (byte i = 0; i < 100; i++)  
        {  
            fs.WriteByte(i);  
        }  
    }  
    ```  
  
 <span data-ttu-id="f5c84-113">Eseguire l'esempio più volte per verificare che i dati vengano aggiunti al file ogni volta.</span><span class="sxs-lookup"><span data-stu-id="f5c84-113">Run the example several times to verify that data is added to the file each time.</span></span>  
  
 <span data-ttu-id="f5c84-114">Per altri valori `FileMode` da provare, vedere <xref:System.IO.FileMode>.</span><span class="sxs-lookup"><span data-stu-id="f5c84-114">For more `FileMode` values that you can try, see <xref:System.IO.FileMode>.</span></span>  
  
 <span data-ttu-id="f5c84-115">Le seguenti condizioni possono generare un'eccezione:</span><span class="sxs-lookup"><span data-stu-id="f5c84-115">The following conditions may cause an exception:</span></span>  
  
- <span data-ttu-id="f5c84-116">Il formato del nome della cartella non è valido.</span><span class="sxs-lookup"><span data-stu-id="f5c84-116">The folder name is malformed.</span></span> <span data-ttu-id="f5c84-117">Ad esempio, contiene caratteri non validi o è costituito solo da spazi (classe <xref:System.ArgumentException>).</span><span class="sxs-lookup"><span data-stu-id="f5c84-117">For example, it contains illegal characters or is only white space (<xref:System.ArgumentException> class).</span></span> <span data-ttu-id="f5c84-118">Per creare nomi di percorso validi, usare la classe <xref:System.IO.Path>.</span><span class="sxs-lookup"><span data-stu-id="f5c84-118">Use the <xref:System.IO.Path> class to create valid path names.</span></span>  
  
- <span data-ttu-id="f5c84-119">La cartella padre della cartella da creare è di sola lettura (classe <xref:System.IO.IOException>).</span><span class="sxs-lookup"><span data-stu-id="f5c84-119">The parent folder of the folder to be created is read-only (<xref:System.IO.IOException> class).</span></span>  
  
- <span data-ttu-id="f5c84-120">Il nome della cartella è `null` (classe <xref:System.ArgumentNullException>).</span><span class="sxs-lookup"><span data-stu-id="f5c84-120">The folder name is `null` (<xref:System.ArgumentNullException> class).</span></span>  
  
- <span data-ttu-id="f5c84-121">Il nome della cartella è troppo lungo (classe <xref:System.IO.PathTooLongException>).</span><span class="sxs-lookup"><span data-stu-id="f5c84-121">The folder name is too long (<xref:System.IO.PathTooLongException> class).</span></span>  
  
- <span data-ttu-id="f5c84-122">Il nome della cartella è composto solo da un carattere due punti, ":" (classe <xref:System.IO.PathTooLongException>).</span><span class="sxs-lookup"><span data-stu-id="f5c84-122">The folder name is only a colon, ":" (<xref:System.IO.PathTooLongException> class).</span></span>  
  
## <a name="net-security"></a><span data-ttu-id="f5c84-123">Sicurezza .NET</span><span class="sxs-lookup"><span data-stu-id="f5c84-123">.NET Security</span></span>  
 <span data-ttu-id="f5c84-124">In situazioni di attendibilità parziale può essere generata un'istanza della classe <xref:System.Security.SecurityException>.</span><span class="sxs-lookup"><span data-stu-id="f5c84-124">An instance of the <xref:System.Security.SecurityException> class may be thrown in partial-trust situations.</span></span>  
  
 <span data-ttu-id="f5c84-125">Se non si dispone dell'autorizzazione per creare la cartella, l'esempio genera un'istanza della <xref:System.UnauthorizedAccessException> classe.</span><span class="sxs-lookup"><span data-stu-id="f5c84-125">If you don't have permission to create the folder, the example throws an instance of the <xref:System.UnauthorizedAccessException> class.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f5c84-126">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f5c84-126">See also</span></span>

- <xref:System.IO?displayProperty=nameWithType>
- [<span data-ttu-id="f5c84-127">Guida per programmatori C#</span><span class="sxs-lookup"><span data-stu-id="f5c84-127">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="f5c84-128">File system e Registro di sistema (Guida per programmatori C#)</span><span class="sxs-lookup"><span data-stu-id="f5c84-128">File System and the Registry (C# Programming Guide)</span></span>](./index.md)

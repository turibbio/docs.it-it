---
title: Eliminazione di spazi iniziali e finali e rimozione di caratteri dalle stringhe in .NET
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- strings [.NET Framework], removing characters
- Remove method
- TrimEnd method
- Trim method
- trimming characters
- TrimStart method
- removing characters
ms.assetid: ab248dab-70d4-4413-81c6-542d153fd195
ms.openlocfilehash: 0777ba7348d13697fd53f556ac69cba3f98d1e4d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290876"
---
# <a name="trimming-and-removing-characters-from-strings-in-net"></a><span data-ttu-id="b83a1-102">Eliminazione di spazi iniziali e finali e rimozione di caratteri dalle stringhe in .NET</span><span class="sxs-lookup"><span data-stu-id="b83a1-102">Trimming and Removing Characters from Strings in .NET</span></span>
<span data-ttu-id="b83a1-103">Se si sta analizzando una frase in singole parole, è possibile che si ottengano parole con spazi vuoti alle estremità.</span><span class="sxs-lookup"><span data-stu-id="b83a1-103">If you are parsing a sentence into individual words, you might end up with words that have blank spaces (also called white spaces) on either end of the word.</span></span> <span data-ttu-id="b83a1-104">In questo caso è possibile usare uno dei metodi trim della classe **System.String** per rimuovere un numero qualsiasi di spazi o altri caratteri da una posizione specificata nella stringa.</span><span class="sxs-lookup"><span data-stu-id="b83a1-104">In this situation, you can use one of the trim methods in the **System.String** class to remove any number of spaces or other characters from a specified position in the string.</span></span> <span data-ttu-id="b83a1-105">La tabella seguente illustra i metodi trim disponibili.</span><span class="sxs-lookup"><span data-stu-id="b83a1-105">The following table describes the available trim methods.</span></span>  
  
|<span data-ttu-id="b83a1-106">Nome metodo</span><span class="sxs-lookup"><span data-stu-id="b83a1-106">Method name</span></span>|<span data-ttu-id="b83a1-107">Uso</span><span class="sxs-lookup"><span data-stu-id="b83a1-107">Use</span></span>|  
|-----------------|---------|  
|<xref:System.String.Trim%2A?displayProperty=nameWithType>|<span data-ttu-id="b83a1-108">Rimuove gli spazi vuoti o i caratteri specificati in una matrice di caratteri all'inizio e alla fine di una stringa.</span><span class="sxs-lookup"><span data-stu-id="b83a1-108">Removes white spaces or characters specified in an array of characters from the beginning and end of a string.</span></span>|  
|<xref:System.String.TrimEnd%2A?displayProperty=nameWithType>|<span data-ttu-id="b83a1-109">Rimuove i caratteri specificati in una matrice di caratteri alla fine di una stringa.</span><span class="sxs-lookup"><span data-stu-id="b83a1-109">Removes characters specified in an array of characters from the end of a string.</span></span>|  
|<xref:System.String.TrimStart%2A?displayProperty=nameWithType>|<span data-ttu-id="b83a1-110">Rimuove i caratteri specificati in una matrice di caratteri all'inizio di una stringa.</span><span class="sxs-lookup"><span data-stu-id="b83a1-110">Removes characters specified in an array of characters from the beginning of a string.</span></span>|  
|<xref:System.String.Remove%2A?displayProperty=nameWithType>|<span data-ttu-id="b83a1-111">Rimuove un numero specificato di caratteri da una posizione di indice specificata in una stringa.</span><span class="sxs-lookup"><span data-stu-id="b83a1-111">Removes a specified number of characters from a specified index position in a string.</span></span>|  
  
## <a name="trim"></a><span data-ttu-id="b83a1-112">Trim</span><span class="sxs-lookup"><span data-stu-id="b83a1-112">Trim</span></span>

 <span data-ttu-id="b83a1-113">È possibile rimuovere facilmente gli spazi vuoti da entrambe le estremità di una stringa utilizzando il metodo <xref:System.String.Trim%2A?displayProperty=nameWithType>, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="b83a1-113">You can easily remove white spaces from both ends of a string by using the <xref:System.String.Trim%2A?displayProperty=nameWithType> method, as shown in the following example.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#17)]
 [!code-csharp[Conceptual.String.BasicOps#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#17)]
 [!code-vb[Conceptual.String.BasicOps#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#17)]  
  
 <span data-ttu-id="b83a1-114">È anche possibile rimuovere i caratteri specificati in una matrice di caratteri all'inizio e alla fine di una stringa.</span><span class="sxs-lookup"><span data-stu-id="b83a1-114">You can also remove characters that you specify in a character array from the beginning and end of a string.</span></span> <span data-ttu-id="b83a1-115">Nell'esempio seguente vengono rimossi gli spazi vuoti, i punti e gli asterischi.</span><span class="sxs-lookup"><span data-stu-id="b83a1-115">The following example removes white-space characters, periods, and asterisks.</span></span>  
  
 [!code-csharp[Conceptual.String.BasicOps#22](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trim2.cs#22)]
 [!code-vb[Conceptual.String.BasicOps#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trim2.vb#22)]  
  
## <a name="trimend"></a><span data-ttu-id="b83a1-116">TrimEnd</span><span class="sxs-lookup"><span data-stu-id="b83a1-116">TrimEnd</span></span>

 <span data-ttu-id="b83a1-117">Il metodo **TrimEnd** rimuove caratteri alla fine di una stringa, creando un nuovo oggetto stringa.</span><span class="sxs-lookup"><span data-stu-id="b83a1-117">The **String.TrimEnd** method removes characters from the end of a string, creating a new string object.</span></span> <span data-ttu-id="b83a1-118">Una matrice di caratteri viene passata a questo metodo per specificare i caratteri da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="b83a1-118">An array of characters is passed to this method to specify the characters to be removed.</span></span> <span data-ttu-id="b83a1-119">L'ordine degli elementi nella matrice di caratteri non influenza l'operazione di rimozione.</span><span class="sxs-lookup"><span data-stu-id="b83a1-119">The order of the elements in the character array does not affect the trim operation.</span></span> <span data-ttu-id="b83a1-120">La rimozione si interrompe quando viene trovato un carattere non specificato nella matrice.</span><span class="sxs-lookup"><span data-stu-id="b83a1-120">The trim stops when a character not specified in the array is found.</span></span>  
  
 <span data-ttu-id="b83a1-121">L'esempio seguente rimuove le ultime lettere di una stringa con il metodo **TrimEnd**.</span><span class="sxs-lookup"><span data-stu-id="b83a1-121">The following example removes the last letters of a string using the **TrimEnd** method.</span></span> <span data-ttu-id="b83a1-122">In questo esempio la posizione dei caratteri `'r'` e `'W'` viene invertita per indicare che l'ordine dei caratteri nella matrice non è importante.</span><span class="sxs-lookup"><span data-stu-id="b83a1-122">In this example, the position of the `'r'` character and the `'W'` character are reversed to illustrate that the order of characters in the array does not matter.</span></span> <span data-ttu-id="b83a1-123">Si noti che questo codice rimuove l'ultima parola di `MyString` e una parte della prima parola.</span><span class="sxs-lookup"><span data-stu-id="b83a1-123">Notice that this code removes the last word of `MyString` plus part of the first.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#18)]
 [!code-csharp[Conceptual.String.BasicOps#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#18)]
 [!code-vb[Conceptual.String.BasicOps#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#18)]  
  
 <span data-ttu-id="b83a1-124">Il codice visualizza `He` nella console.</span><span class="sxs-lookup"><span data-stu-id="b83a1-124">This code displays `He` to the console.</span></span>  
  
 <span data-ttu-id="b83a1-125">L'esempio seguente rimuove l'ultima parola di una stringa con il metodo **TrimEnd**.</span><span class="sxs-lookup"><span data-stu-id="b83a1-125">The following example removes the last word of a string using the **TrimEnd** method.</span></span> <span data-ttu-id="b83a1-126">In questo codice la parola `Hello` è seguita da una virgola: dato che la virgola non è specificata nella matrice di caratteri da tagliare, l'operazione di taglio termina in corrispondenza della virgola.</span><span class="sxs-lookup"><span data-stu-id="b83a1-126">In this code, a comma follows the word `Hello` and, because the comma is not specified in the array of characters to trim, the trim ends at the comma.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#19](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#19)]
 [!code-csharp[Conceptual.String.BasicOps#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#19)]
 [!code-vb[Conceptual.String.BasicOps#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#19)]  
  
 <span data-ttu-id="b83a1-127">Il codice visualizza `Hello,` nella console.</span><span class="sxs-lookup"><span data-stu-id="b83a1-127">This code displays `Hello,` to the console.</span></span>  
  
## <a name="trimstart"></a><span data-ttu-id="b83a1-128">TrimStart</span><span class="sxs-lookup"><span data-stu-id="b83a1-128">TrimStart</span></span>

 <span data-ttu-id="b83a1-129">Il metodo **String.TrimStart** è simile al metodo **String.TrimEnd** ma crea una nuova stringa rimuovendo caratteri dall'inizio di un oggetto stringa esistente.</span><span class="sxs-lookup"><span data-stu-id="b83a1-129">The **String.TrimStart** method is similar to the **String.TrimEnd** method except that it creates a new string by removing characters from the beginning of an existing string object.</span></span> <span data-ttu-id="b83a1-130">Una matrice di caratteri viene passata al metodo **TrimStart** per specificare i caratteri da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="b83a1-130">An array of characters is passed to the **TrimStart** method to specify the characters to be removed.</span></span> <span data-ttu-id="b83a1-131">Come per il metodo **TrimEnd**, l'ordine degli elementi nella matrice di caratteri non è importante per l'operazione di rimozione.</span><span class="sxs-lookup"><span data-stu-id="b83a1-131">As with the **TrimEnd** method, the order of the elements in the character array does not affect the trim operation.</span></span> <span data-ttu-id="b83a1-132">La rimozione si interrompe quando viene trovato un carattere non specificato nella matrice.</span><span class="sxs-lookup"><span data-stu-id="b83a1-132">The trim stops when a character not specified in the array is found.</span></span>  
  
 <span data-ttu-id="b83a1-133">L'esempio seguente rimuove la prima parola di una stringa.</span><span class="sxs-lookup"><span data-stu-id="b83a1-133">The following example removes the first word of a string.</span></span> <span data-ttu-id="b83a1-134">In questo esempio la posizione dei caratteri `'l'` e `'H'` viene invertita per indicare che l'ordine dei caratteri nella matrice non è importante.</span><span class="sxs-lookup"><span data-stu-id="b83a1-134">In this example, the position of the `'l'` character and the `'H'` character are reversed to illustrate that the order of characters in the array does not matter.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#20)]
 [!code-csharp[Conceptual.String.BasicOps#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#20)]
 [!code-vb[Conceptual.String.BasicOps#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#20)]  
  
 <span data-ttu-id="b83a1-135">Il codice visualizza `World!` nella console.</span><span class="sxs-lookup"><span data-stu-id="b83a1-135">This code displays `World!` to the console.</span></span>  
  
## <a name="remove"></a><span data-ttu-id="b83a1-136">Rimuovi</span><span class="sxs-lookup"><span data-stu-id="b83a1-136">Remove</span></span>

 <span data-ttu-id="b83a1-137">Tramite il metodo <xref:System.String.Remove%2A?displayProperty=nameWithType> viene rimosso un numero specificato di caratteri a partire da una posizione specificata in una stringa esistente.</span><span class="sxs-lookup"><span data-stu-id="b83a1-137">The <xref:System.String.Remove%2A?displayProperty=nameWithType> method removes a specified number of characters that begin at a specified position in an existing string.</span></span> <span data-ttu-id="b83a1-138">Questo metodo presuppone un indice a base zero.</span><span class="sxs-lookup"><span data-stu-id="b83a1-138">This method assumes a zero-based index.</span></span>  
  
 <span data-ttu-id="b83a1-139">L'esempio seguente rimuove dieci caratteri da una stringa a partire dalla posizione cinque di un indice a base zero della stringa.</span><span class="sxs-lookup"><span data-stu-id="b83a1-139">The following example removes ten characters from a string beginning at position five of a zero-based index of the string.</span></span>  
  
 [!code-cpp[Conceptual.String.BasicOps#21](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#21)]
 [!code-csharp[Conceptual.String.BasicOps#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#21)]
 [!code-vb[Conceptual.String.BasicOps#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#21)]  
  
## <a name="replace"></a><span data-ttu-id="b83a1-140">Replace</span><span class="sxs-lookup"><span data-stu-id="b83a1-140">Replace</span></span>

 <span data-ttu-id="b83a1-141">È anche possibile rimuovere da una stringa una sottostringa o un carattere specificato chiamando il metodo <xref:System.String.Replace%28System.String%2CSystem.String%29?displayProperty=nameWithType> e specificando, in sostituzione, una stringa vuota (<xref:System.String.Empty?displayProperty=nameWithType>).</span><span class="sxs-lookup"><span data-stu-id="b83a1-141">You can also remove a specified character or substring from a string by calling the <xref:System.String.Replace%28System.String%2CSystem.String%29?displayProperty=nameWithType> method and specifying an empty string (<xref:System.String.Empty?displayProperty=nameWithType>) as the replacement.</span></span> <span data-ttu-id="b83a1-142">Nell'esempio seguente vengono rimosse tutte le virgole da una stringa.</span><span class="sxs-lookup"><span data-stu-id="b83a1-142">The following example removes all commas from a string.</span></span>  
  
 [!code-csharp[Conceptual.String.BasicOps#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/replace1.cs#23)]
 [!code-vb[Conceptual.String.BasicOps#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/replace1.vb#23)]  
  
## <a name="see-also"></a><span data-ttu-id="b83a1-143">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b83a1-143">See also</span></span>

- [<span data-ttu-id="b83a1-144">Operazioni di base sulle stringhe</span><span class="sxs-lookup"><span data-stu-id="b83a1-144">Basic String Operations</span></span>](basic-string-operations.md)

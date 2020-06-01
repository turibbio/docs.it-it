---
title: Come usare lo spazio dei nomi My-guida per programmatori C#
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, My namespace access
ms.assetid: e7152414-0ea5-4c8e-bf02-c8d5bbe45ff4
ms.openlocfilehash: 268543980ba891b0b30f393ee8982f2863ba9a71
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241942"
---
# <a name="how-to-use-the-my-namespace-c-programming-guide"></a><span data-ttu-id="0bb78-102">Come usare lo spazio dei nomi My (Guida per programmatori C#)</span><span class="sxs-lookup"><span data-stu-id="0bb78-102">How to use the My namespace (C# Programming Guide)</span></span>

<span data-ttu-id="0bb78-103">Lo <xref:Microsoft.VisualBasic.MyServices> spazio dei nomi ( `My` in Visual Basic) consente di accedere in modo semplice e intuitivo a numerose classi .NET, consentendo di scrivere codice che interagisce con il computer, l'applicazione, le impostazioni, le risorse e così via.</span><span class="sxs-lookup"><span data-stu-id="0bb78-103">The <xref:Microsoft.VisualBasic.MyServices> namespace (`My` in Visual Basic) provides easy and intuitive access to a number of .NET classes, enabling you to write code that interacts with the computer, application, settings, resources, and so on.</span></span> <span data-ttu-id="0bb78-104">Anche se originariamente progettato per l'uso con Visual Basic, lo spazio dei nomi `MyServices` può essere usato nelle applicazioni C#.</span><span class="sxs-lookup"><span data-stu-id="0bb78-104">Although originally designed for use with Visual Basic, the `MyServices` namespace can be used in C# applications.</span></span>  
  
 <span data-ttu-id="0bb78-105">Per altre informazioni sull'uso dello spazio dei nomi `MyServices` da Visual Basic, vedere [Development with My](../../../visual-basic/developing-apps/development-with-my/index.md) (Sviluppo con My).</span><span class="sxs-lookup"><span data-stu-id="0bb78-105">For more information about using the `MyServices` namespace from Visual Basic, see [Development with My](../../../visual-basic/developing-apps/development-with-my/index.md).</span></span>  
  
## <a name="add-a-reference"></a><span data-ttu-id="0bb78-106">Aggiungere un riferimento</span><span class="sxs-lookup"><span data-stu-id="0bb78-106">Add a reference</span></span>

 <span data-ttu-id="0bb78-107">Prima di poter usare le classi `MyServices` nella soluzione, è necessario aggiungere un riferimento alla libreria di Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="0bb78-107">Before you can use the `MyServices` classes in your solution, you must add a reference to the Visual Basic library.</span></span>  
  
### <a name="add-a-reference-to-the-visual-basic-library"></a><span data-ttu-id="0bb78-108">Aggiungere un riferimento alla libreria Visual Basic</span><span class="sxs-lookup"><span data-stu-id="0bb78-108">Add a reference to the Visual Basic library</span></span>  
  
1. <span data-ttu-id="0bb78-109">In **Esplora soluzioni**fare clic con il pulsante destro del mouse sul nodo **riferimenti** e selezionare **Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="0bb78-109">In **Solution Explorer**, right-click the **References** node, and select **Add Reference**.</span></span>  
  
2. <span data-ttu-id="0bb78-110">Nella finestra di dialogo **Riferimenti** visualizzata scorrere l'elenco e selezionare Microsoft.VisualBasic.dll.</span><span class="sxs-lookup"><span data-stu-id="0bb78-110">When the **References** dialog box appears, scroll down the list, and select Microsoft.VisualBasic.dll.</span></span>  
  
     <span data-ttu-id="0bb78-111">È anche possibile includere la riga seguente nella sezione `using` all'inizio del programma.</span><span class="sxs-lookup"><span data-stu-id="0bb78-111">You might also want to include the following line in the `using` section at the start of your program.</span></span>  
  
     [!code-csharp[csProgGuideNamespaces#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces3.cs#18)]  
  
## <a name="example"></a><span data-ttu-id="0bb78-112">Esempio</span><span class="sxs-lookup"><span data-stu-id="0bb78-112">Example</span></span>  
 <span data-ttu-id="0bb78-113">Questo esempio chiama diversi metodi statici contenuti nello spazio dei nomi `MyServices`.</span><span class="sxs-lookup"><span data-stu-id="0bb78-113">This example calls various static methods contained in the `MyServices` namespace.</span></span> <span data-ttu-id="0bb78-114">Per compilare questo codice, è necessario aggiungere al progetto un riferimento a Microsoft.VisualBasic.DLL.</span><span class="sxs-lookup"><span data-stu-id="0bb78-114">For this code to compile, a reference to Microsoft.VisualBasic.DLL must be added to the project.</span></span>  
  
 [!code-csharp[csProgGuideNamespaces#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces3.cs#19)]  
  
 <span data-ttu-id="0bb78-115">Non tutte le classi incluse nello spazio dei nomi `MyServices` possono essere chiamate da un'applicazione C#. La classe <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy>, ad esempio, non è compatibile.</span><span class="sxs-lookup"><span data-stu-id="0bb78-115">Not all the classes in the `MyServices` namespace can be called from a C# application: for example, the <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy> class is not compatible.</span></span> <span data-ttu-id="0bb78-116">In questo caso specifico è possibile usare i metodi statici inclusi in <xref:Microsoft.VisualBasic.FileIO.FileSystem> e contenuti anche nel file VisualBasic.dll.</span><span class="sxs-lookup"><span data-stu-id="0bb78-116">In this particular case, the static methods that are part of <xref:Microsoft.VisualBasic.FileIO.FileSystem>, which are also contained in VisualBasic.dll, can be used instead.</span></span> <span data-ttu-id="0bb78-117">Ecco ad esempio come usare uno di questi metodi per duplicare una directory:</span><span class="sxs-lookup"><span data-stu-id="0bb78-117">For example, here is how to use one such method to duplicate a directory:</span></span>  
  
 [!code-csharp[csProgGuideNamespaces#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces3.cs#20)]  
  
## <a name="see-also"></a><span data-ttu-id="0bb78-118">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0bb78-118">See also</span></span>

- [<span data-ttu-id="0bb78-119">Guida per programmatori C#</span><span class="sxs-lookup"><span data-stu-id="0bb78-119">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="0bb78-120">Spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="0bb78-120">Namespaces</span></span>](./index.md)
- [<span data-ttu-id="0bb78-121">Uso degli spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="0bb78-121">Using Namespaces</span></span>](./using-namespaces.md)

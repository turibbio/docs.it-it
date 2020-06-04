---
title: -doc
ms.date: 03/10/2018
helpviewer_keywords:
- doc compiler option [Visual Basic]
- -doc compiler option [Visual Basic]
- /doc compiler option [Visual Basic]
ms.assetid: 5fc32ec9-a149-4648-994c-a8d0cccd0a65
ms.openlocfilehash: 57a81983278c26090c62995f4da55c5cbfd66047
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408673"
---
# <a name="-doc"></a><span data-ttu-id="fc8bf-102">-doc</span><span class="sxs-lookup"><span data-stu-id="fc8bf-102">-doc</span></span>
<span data-ttu-id="fc8bf-103">Elabora commenti sulla documentazione in un file XML.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-103">Processes documentation comments to an XML file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fc8bf-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="fc8bf-104">Syntax</span></span>  
  
```console  
-doc[+ | -]  
```

<span data-ttu-id="fc8bf-105">Oppure</span><span class="sxs-lookup"><span data-stu-id="fc8bf-105">or</span></span>  

```console
-doc:file  
```  
  
## <a name="arguments"></a><span data-ttu-id="fc8bf-106">Argomenti</span><span class="sxs-lookup"><span data-stu-id="fc8bf-106">Arguments</span></span>  
  
|<span data-ttu-id="fc8bf-107">Termine</span><span class="sxs-lookup"><span data-stu-id="fc8bf-107">Term</span></span>|<span data-ttu-id="fc8bf-108">Definizione</span><span class="sxs-lookup"><span data-stu-id="fc8bf-108">Definition</span></span>|  
|---|---|  
|<span data-ttu-id="fc8bf-109">`+` &#124; `-`</span><span class="sxs-lookup"><span data-stu-id="fc8bf-109">`+` &#124; `-`</span></span>|<span data-ttu-id="fc8bf-110">Facoltativa.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-110">Optional.</span></span> <span data-ttu-id="fc8bf-111">Se si specifica +, o semplicemente `-doc`, il compilatore genera informazioni di documentazione e le inserisce in un file XML.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-111">Specifying +, or just `-doc`, causes the compiler to generate documentation information and place it in an XML file.</span></span> <span data-ttu-id="fc8bf-112">La specifica di `-` equivale a non specificare `-doc`, quindi non vengono create informazione di documentazione.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-112">Specifying `-` is the equivalent of not specifying `-doc`, causing no documentation information to be created.</span></span>|  
|`file`|<span data-ttu-id="fc8bf-113">Richiesto se è usato `-doc:`.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-113">Required if `-doc:` is used.</span></span> <span data-ttu-id="fc8bf-114">Specifica il file di output XML, popolato con i commenti dai file del codice sorgente della compilazione.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-114">Specifies the output XML file, which is populated with the comments from the source-code files of the compilation.</span></span> <span data-ttu-id="fc8bf-115">Se il nome del file contiene uno spazio, racchiudere il nome tra virgolette doppie (" ").</span><span class="sxs-lookup"><span data-stu-id="fc8bf-115">If the file name contains a space, surround the name with quotation marks (" ").</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="fc8bf-116">Commenti</span><span class="sxs-lookup"><span data-stu-id="fc8bf-116">Remarks</span></span>  
 <span data-ttu-id="fc8bf-117">L'opzione `-doc` controlla se il compilatore genera un file XML contenente i commenti della documentazione.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-117">The `-doc` option controls whether the compiler generates an XML file containing the documentation comments.</span></span> <span data-ttu-id="fc8bf-118">Se si usa la sintassi `-doc:file`, il parametro `file` specifica il nome del file XML.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-118">If you use the `-doc:file` syntax, the `file` parameter specifies the name of the XML file.</span></span> <span data-ttu-id="fc8bf-119">Se si usa `-doc` o `-doc+`, il compilatore ottiene il nome del file XML dal file eseguibile o dalla libreria che il compilatore sta creando.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-119">If you use `-doc` or `-doc+`, the compiler takes the XML file name from the executable file or library that the compiler is creating.</span></span> <span data-ttu-id="fc8bf-120">Se si usa `-doc-` o non si specifica l'opzione `-doc`, il compilatore non crea un file XML.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-120">If you use `-doc-` or do not specify the `-doc` option, the compiler does not create an XML file.</span></span>  
  
 <span data-ttu-id="fc8bf-121">Nei file di codice sorgente, i commenti della documentazione possono precedere le definizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fc8bf-121">In source-code files, documentation comments can precede the following definitions:</span></span>  
  
- <span data-ttu-id="fc8bf-122">Tipi definiti dall'utente, ad esempio una [classe](../../language-reference/statements/class-statement.md) o [interfaccia](../../language-reference/statements/interface-statement.md)</span><span class="sxs-lookup"><span data-stu-id="fc8bf-122">User-defined types, such as a [class](../../language-reference/statements/class-statement.md) or [interface](../../language-reference/statements/interface-statement.md)</span></span>  
  
- <span data-ttu-id="fc8bf-123">Membri, ad esempio un campo, un [evento](../../language-reference/statements/event-statement.md), una [proprietà](../../language-reference/statements/property-statement.md), una [funzione](../../language-reference/statements/function-statement.md) oppure una [subroutine](../../language-reference/statements/sub-statement.md).</span><span class="sxs-lookup"><span data-stu-id="fc8bf-123">Members, such as a field, [event](../../language-reference/statements/event-statement.md), [property](../../language-reference/statements/property-statement.md), [function](../../language-reference/statements/function-statement.md), or [subroutine](../../language-reference/statements/sub-statement.md).</span></span>  
  
 <span data-ttu-id="fc8bf-124">Per usare il file XML generato con la funzionalità [IntelliSense](/visualstudio/ide/using-intellisense) di Visual Studio, usare un nome per il file XML uguale al nome dell'assembly che si vuole supportare.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-124">To use the generated XML file with the Visual Studio [IntelliSense](/visualstudio/ide/using-intellisense) feature, let the file name of the XML file be the same as the assembly you want to support.</span></span> <span data-ttu-id="fc8bf-125">Assicurarsi che il file XML sia nella stessa directory dell'assembly, in modo che quando si fa riferimento all'assembly nel progetto di Visual Studio, venga trovato anche il file XML.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-125">Make sure the XML file is in the same directory as the assembly so that when the assembly is referenced in the Visual Studio project, the .xml file is found as well.</span></span> <span data-ttu-id="fc8bf-126">I file di documentazione XML non sono necessari per il funzionamento di IntelliSense per il codice all'interno di un progetto o all'interno di progetti a cui viene fatto riferimento da un progetto.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-126">XML documentation files are not required for IntelliSense to work for code within a project or within projects referenced by a project.</span></span>  
  
 <span data-ttu-id="fc8bf-127">A meno che non si esegua la compilazione con `-target:module`, il file XML contiene i tag `<assembly></assembly>`.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-127">Unless you compile with `-target:module`, the XML file contains the tags `<assembly></assembly>`.</span></span> <span data-ttu-id="fc8bf-128">Questi tag specificano il nome del file contenente il manifesto dell'assembly per il file di output della compilazione.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-128">These tags specify the name of the file containing the assembly manifest for the output file of the compilation.</span></span>  
  
 <span data-ttu-id="fc8bf-129">Vedere [Tag XML consigliati per i commenti relativi alla documentazione](../../language-reference/xmldoc/index.md) per informazioni su come generare documentazione dai commenti nel codice.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-129">See [XML Comment Tags](../../language-reference/xmldoc/index.md) for ways to generate documentation from comments in your code.</span></span>  
  
|<span data-ttu-id="fc8bf-130">Per impostare -doc nell'ambiente di sviluppo integrato di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fc8bf-130">To set -doc in the Visual Studio integrated development environment</span></span>|  
|---|  
|<span data-ttu-id="fc8bf-131">1. è stato selezionato un progetto in **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-131">1.  Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="fc8bf-132">Scegliere **Proprietà** dal menu **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-132">On the **Project** menu, click **Properties**.</span></span> <br /><span data-ttu-id="fc8bf-133">2. fare clic sulla scheda **Compila** .</span><span class="sxs-lookup"><span data-stu-id="fc8bf-133">2.  Click the **Compile** tab.</span></span><br /><span data-ttu-id="fc8bf-134">3. impostare il valore nella casella **genera file di documentazione XML** .</span><span class="sxs-lookup"><span data-stu-id="fc8bf-134">3.  Set the value in the **Generate XML documentation file** box.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="fc8bf-135">Esempio</span><span class="sxs-lookup"><span data-stu-id="fc8bf-135">Example</span></span>  
 <span data-ttu-id="fc8bf-136">Vedere [Documentazione del codice tramite XML](../../programming-guide/program-structure/documenting-your-code-with-xml.md) per un esempio.</span><span class="sxs-lookup"><span data-stu-id="fc8bf-136">See [Documenting Your Code with XML](../../programming-guide/program-structure/documenting-your-code-with-xml.md) for a sample.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fc8bf-137">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="fc8bf-137">See also</span></span>

- [<span data-ttu-id="fc8bf-138">Compilatore della riga di comando di Visual Basic</span><span class="sxs-lookup"><span data-stu-id="fc8bf-138">Visual Basic Command-Line Compiler</span></span>](index.md)
- [<span data-ttu-id="fc8bf-139">Documentazione del codice tramite XML</span><span class="sxs-lookup"><span data-stu-id="fc8bf-139">Documenting Your Code with XML</span></span>](../../programming-guide/program-structure/documenting-your-code-with-xml.md)

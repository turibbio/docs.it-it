---
title: -optionexplicit
ms.date: 07/20/2015
f1_keywords:
- /optionexplicit
- -optionexplicit
helpviewer_keywords:
- /optionexplicit compiler option [Visual Basic]
- optionexplicit compiler option [Visual Basic]
- -optionexplicit compiler option [Visual Basic]
ms.assetid: 5d296ab3-bafe-4c4d-9887-78f162ed86c7
ms.openlocfilehash: 37ccd14dae0ebba2535185f2646e312d9bb70390
ms.sourcegitcommit: 43d10ef65f0f1fd6c3b515e363bde11a3fcd8d6d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/04/2020
ms.locfileid: "78266729"
---
# <a name="-optionexplicit"></a><span data-ttu-id="2889f-102">-optionexplicit</span><span class="sxs-lookup"><span data-stu-id="2889f-102">-optionexplicit</span></span>
<span data-ttu-id="2889f-103">Fa in modo che il compilatore segnali errori se le variabili non vengono dichiarate prima di essere utilizzate.</span><span class="sxs-lookup"><span data-stu-id="2889f-103">Causes the compiler to report errors if variables are not declared before they are used.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2889f-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="2889f-104">Syntax</span></span>  
  
```console  
-optionexplicit[+ | -]  
```  
  
## <a name="arguments"></a><span data-ttu-id="2889f-105">Argomenti</span><span class="sxs-lookup"><span data-stu-id="2889f-105">Arguments</span></span>  
 <span data-ttu-id="2889f-106">`+` &#124; `-`</span><span class="sxs-lookup"><span data-stu-id="2889f-106">`+` &#124; `-`</span></span>  
 <span data-ttu-id="2889f-107">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="2889f-107">Optional.</span></span> <span data-ttu-id="2889f-108">Specificare `-optionexplicit+` per richiedere la dichiarazione esplicita delle variabili.</span><span class="sxs-lookup"><span data-stu-id="2889f-108">Specify `-optionexplicit+` to require explicit declaration of variables.</span></span> <span data-ttu-id="2889f-109">L' `-optionexplicit+` opzione è l'impostazione predefinita ed è uguale a `-optionexplicit`.</span><span class="sxs-lookup"><span data-stu-id="2889f-109">The `-optionexplicit+` option is the default and is the same as `-optionexplicit`.</span></span> <span data-ttu-id="2889f-110">L' `-optionexplicit-` opzione consente la dichiarazione implicita delle variabili.</span><span class="sxs-lookup"><span data-stu-id="2889f-110">The `-optionexplicit-` option enables implicit declaration of variables.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="2889f-111">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="2889f-111">Remarks</span></span>  
 <span data-ttu-id="2889f-112">Se il file di codice sorgente contiene un' [istruzione Option Explicit](../../../visual-basic/language-reference/statements/option-explicit-statement.md), l'istruzione sostituisce `-optionexplicit` l'impostazione del compilatore da riga di comando.</span><span class="sxs-lookup"><span data-stu-id="2889f-112">If the source code file contains an [Option Explicit statement](../../../visual-basic/language-reference/statements/option-explicit-statement.md), the statement overrides the `-optionexplicit` command-line compiler setting.</span></span>  
  
### <a name="to-set--optionexplicit-in-the-visual-studio-ide"></a><span data-ttu-id="2889f-113">Per impostare-optionexplicit (nell'IDE di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2889f-113">To set -optionexplicit in the Visual Studio IDE</span></span>  
  
1. <span data-ttu-id="2889f-114">Selezionare un progetto in **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="2889f-114">Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="2889f-115">Scegliere **Proprietà** dal menu **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="2889f-115">On the **Project** menu, click **Properties**.</span></span>
  
2. <span data-ttu-id="2889f-116">Fare clic sulla scheda **Compila**.</span><span class="sxs-lookup"><span data-stu-id="2889f-116">Click the **Compile** tab.</span></span>  
  
3. <span data-ttu-id="2889f-117">Modificare il valore nella casella **Option Explicit** .</span><span class="sxs-lookup"><span data-stu-id="2889f-117">Modify the value in the **Option Explicit** box.</span></span>  
  
## <a name="example"></a><span data-ttu-id="2889f-118">Esempio</span><span class="sxs-lookup"><span data-stu-id="2889f-118">Example</span></span>  
 <span data-ttu-id="2889f-119">Il codice seguente viene compilato quando `-optionexplicit-` si usa.</span><span class="sxs-lookup"><span data-stu-id="2889f-119">The following code compiles when `-optionexplicit-` is used.</span></span>  
  
 [!code-vb[VbVbalrCompiler#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/OptionExplicitOff.vb#5)]  
  
## <a name="see-also"></a><span data-ttu-id="2889f-120">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="2889f-120">See also</span></span>

- [<span data-ttu-id="2889f-121">Compilatore della riga di comando di Visual Basic</span><span class="sxs-lookup"><span data-stu-id="2889f-121">Visual Basic Command-Line Compiler</span></span>](../../../visual-basic/reference/command-line-compiler/index.md)
- [<span data-ttu-id="2889f-122">-OptionCompare (</span><span class="sxs-lookup"><span data-stu-id="2889f-122">-optioncompare</span></span>](../../../visual-basic/reference/command-line-compiler/optioncompare.md)
- [<span data-ttu-id="2889f-123">-OptionStrict (</span><span class="sxs-lookup"><span data-stu-id="2889f-123">-optionstrict</span></span>](../../../visual-basic/reference/command-line-compiler/optionstrict.md)
- [<span data-ttu-id="2889f-124">-optioninfer (</span><span class="sxs-lookup"><span data-stu-id="2889f-124">-optioninfer</span></span>](../../../visual-basic/reference/command-line-compiler/optioninfer.md)
- [<span data-ttu-id="2889f-125">Esempi di righe di comando di compilazione</span><span class="sxs-lookup"><span data-stu-id="2889f-125">Sample Compilation Command Lines</span></span>](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [<span data-ttu-id="2889f-126">Istruzione Option Explicit</span><span class="sxs-lookup"><span data-stu-id="2889f-126">Option Explicit Statement</span></span>](../../../visual-basic/language-reference/statements/option-explicit-statement.md)
- [<span data-ttu-id="2889f-127">Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni</span><span class="sxs-lookup"><span data-stu-id="2889f-127">Visual Basic Defaults, Projects, Options Dialog Box</span></span>](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)

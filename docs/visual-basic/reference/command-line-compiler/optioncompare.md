---
title: -optioncompare
ms.date: 07/20/2015
f1_keywords:
- /optioncompare
- -optioncompare
helpviewer_keywords:
- optioncompare compiler option [Visual Basic]
- -optioncompare compiler option [Visual Basic]
- /optioncompare compiler option [Visual Basic]
ms.assetid: 7237b766-b44d-4cc5-9a3c-885348a7d9e4
ms.openlocfilehash: ac385880f8c13c23dffff67fc2a1ecc5609fd189
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/18/2019
ms.locfileid: "72581408"
---
# <a name="-optioncompare"></a><span data-ttu-id="4ee8b-102">-optioncompare</span><span class="sxs-lookup"><span data-stu-id="4ee8b-102">-optioncompare</span></span>

<span data-ttu-id="4ee8b-103">Specifica la modalità con cui vengono confrontate le stringhe.</span><span class="sxs-lookup"><span data-stu-id="4ee8b-103">Specifies how string comparisons are made.</span></span>

## <a name="syntax"></a><span data-ttu-id="4ee8b-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="4ee8b-104">Syntax</span></span>

```console
-optioncompare:{binary | text}
```

## <a name="remarks"></a><span data-ttu-id="4ee8b-105">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="4ee8b-105">Remarks</span></span>

<span data-ttu-id="4ee8b-106">È possibile specificare `-optioncompare` in uno dei due formati seguenti `-optioncompare:binary` : per usare i confronti di `-optioncompare:text` stringhe binarie e per usare i confronti di stringhe di testo.</span><span class="sxs-lookup"><span data-stu-id="4ee8b-106">You can specify `-optioncompare` in one of two forms: `-optioncompare:binary` to use binary string comparisons, and `-optioncompare:text` to use text string comparisons.</span></span> <span data-ttu-id="4ee8b-107">Per impostazione predefinita, il compilatore `-optioncompare:binary`utilizza.</span><span class="sxs-lookup"><span data-stu-id="4ee8b-107">By default, the compiler uses `-optioncompare:binary`.</span></span>

<span data-ttu-id="4ee8b-108">In Microsoft Windows la tabella codici corrente determina l'ordinamento binario.</span><span class="sxs-lookup"><span data-stu-id="4ee8b-108">In Microsoft Windows, the current code page determines the binary sort order.</span></span> <span data-ttu-id="4ee8b-109">Un ordinamento binario tipico è il seguente:</span><span class="sxs-lookup"><span data-stu-id="4ee8b-109">A typical binary sort order is as follows:</span></span>

`A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`

<span data-ttu-id="4ee8b-110">I confronti di stringhe basati su testo sono basati su un ordinamento del testo senza distinzione tra maiuscole e minuscole determinato dalle impostazioni locali del sistema.</span><span class="sxs-lookup"><span data-stu-id="4ee8b-110">Text-based string comparisons are based on a case-insensitive text sort order determined by your system's locale.</span></span> <span data-ttu-id="4ee8b-111">Di seguito è riportato un tipico ordinamento del testo:</span><span class="sxs-lookup"><span data-stu-id="4ee8b-111">A typical text sort order is as follows:</span></span>

`(A = a) < (À = à) < (B=b) < (E=e) < (Ê = ê) < (Z=z) < (Ø = ø)`

### <a name="to-set--optioncompare-in-the-visual-studio-ide"></a><span data-ttu-id="4ee8b-112">Per impostare-optioncompare (nell'IDE di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ee8b-112">To set -optioncompare in the Visual Studio IDE</span></span>

1. <span data-ttu-id="4ee8b-113">Selezionare un progetto in **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="4ee8b-113">Have a project selected in **Solution Explorer**.</span></span> <span data-ttu-id="4ee8b-114">Scegliere **Proprietà** dal menu **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="4ee8b-114">On the **Project** menu, click **Properties**.</span></span>

2. <span data-ttu-id="4ee8b-115">Fare clic sulla scheda **Compila**.</span><span class="sxs-lookup"><span data-stu-id="4ee8b-115">Click the **Compile** tab.</span></span>

3. <span data-ttu-id="4ee8b-116">Modificare il valore nella casella **Option Compare** .</span><span class="sxs-lookup"><span data-stu-id="4ee8b-116">Modify the value in the **Option Compare** box.</span></span>

### <a name="to-set--optioncompare-programmatically"></a><span data-ttu-id="4ee8b-117">Per impostare-optioncompare (a livello di codice</span><span class="sxs-lookup"><span data-stu-id="4ee8b-117">To set -optioncompare programmatically</span></span>

<span data-ttu-id="4ee8b-118">Vedere [istruzione Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md).</span><span class="sxs-lookup"><span data-stu-id="4ee8b-118">See [Option Compare Statement](../../../visual-basic/language-reference/statements/option-compare-statement.md).</span></span>

## <a name="example"></a><span data-ttu-id="4ee8b-119">Esempio</span><span class="sxs-lookup"><span data-stu-id="4ee8b-119">Example</span></span>

<span data-ttu-id="4ee8b-120">Il codice seguente compila `ProjFile.vb` e usa i confronti di stringhe binarie.</span><span class="sxs-lookup"><span data-stu-id="4ee8b-120">The following code compiles `ProjFile.vb` and uses binary string comparisons.</span></span>

```console
vbc -optioncompare:binary projFile.vb
```

## <a name="see-also"></a><span data-ttu-id="4ee8b-121">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="4ee8b-121">See also</span></span>

- [<span data-ttu-id="4ee8b-122">Compilatore della riga di comando di Visual Basic</span><span class="sxs-lookup"><span data-stu-id="4ee8b-122">Visual Basic Command-Line Compiler</span></span>](../../../visual-basic/reference/command-line-compiler/index.md)
- [<span data-ttu-id="4ee8b-123">-OptionExplicit (</span><span class="sxs-lookup"><span data-stu-id="4ee8b-123">-optionexplicit</span></span>](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)
- [<span data-ttu-id="4ee8b-124">-OptionStrict (</span><span class="sxs-lookup"><span data-stu-id="4ee8b-124">-optionstrict</span></span>](../../../visual-basic/reference/command-line-compiler/optionstrict.md)
- [<span data-ttu-id="4ee8b-125">-optioninfer (</span><span class="sxs-lookup"><span data-stu-id="4ee8b-125">-optioninfer</span></span>](../../../visual-basic/reference/command-line-compiler/optioninfer.md)
- [<span data-ttu-id="4ee8b-126">Esempi di righe di comando di compilazione</span><span class="sxs-lookup"><span data-stu-id="4ee8b-126">Sample Compilation Command Lines</span></span>](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [<span data-ttu-id="4ee8b-127">Istruzione Option Compare</span><span class="sxs-lookup"><span data-stu-id="4ee8b-127">Option Compare Statement</span></span>](../../../visual-basic/language-reference/statements/option-compare-statement.md)
- [<span data-ttu-id="4ee8b-128">Impostazioni predefinite di Visual Basic, Progetti, finestra di dialogo Opzioni</span><span class="sxs-lookup"><span data-stu-id="4ee8b-128">Visual Basic Defaults, Projects, Options Dialog Box</span></span>](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)

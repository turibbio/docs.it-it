---
title: Come usare le funzionalità della documentazione XML-guida per programmatori C#
ms.date: 06/01/2018
helpviewer_keywords:
- XML documentation [C#]
- C# language, XML documentation features
ms.assetid: 8f33917b-9577-4c9a-818a-640dbbb0b399
ms.openlocfilehash: b7c5a8a895271f067505496c0d13f98b66a393d9
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287363"
---
# <a name="how-to-use-the-xml-documentation-features"></a><span data-ttu-id="7e29f-102">Come usare le funzionalità relative alla documentazione XML</span><span class="sxs-lookup"><span data-stu-id="7e29f-102">How to use the XML documentation features</span></span>

<span data-ttu-id="7e29f-103">L'esempio seguente fornisce una panoramica di base di un tipo documentato.</span><span class="sxs-lookup"><span data-stu-id="7e29f-103">The following sample provides a basic overview of a type that has been documented.</span></span>

## <a name="example"></a><span data-ttu-id="7e29f-104">Esempio</span><span class="sxs-lookup"><span data-stu-id="7e29f-104">Example</span></span>

[!code-csharp[csProgGuideDocComments#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#15)]

<span data-ttu-id="7e29f-105">Nell'esempio viene generato un file con estensione *XML* con il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="7e29f-105">The example generates an *.xml* file with the following contents.</span></span>

```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>xmlsample</name>
    </assembly>
    <members>
        <member name="T:TestClass">
            <summary>
            Class level summary documentation goes here.
            </summary>
            <remarks>
            Longer comments can be associated with a type or member through
            the remarks tag.
            </remarks>
        </member>
        <member name="F:TestClass._name">
            <summary>
            Store for the Name property.
            </summary>
        </member>
        <member name="M:TestClass.#ctor">
            <summary>
            The class constructor.
            </summary>
        </member>
        <member name="P:TestClass.Name">
            <summary>
            Name property.
            </summary>
            <value>
            A value tag is used to describe the property value.
            </value>
        </member>
        <member name="M:TestClass.SomeMethod(System.String)">
            <summary>
            Description for SomeMethod.
            </summary>
            <param name="s"> Parameter description for s goes here.</param>
            <seealso cref="T:System.String">
            You can use the cref attribute on any tag to reference a type or member
            and the compiler will check that the reference exists.
            </seealso>
        </member>
        <member name="M:TestClass.SomeOtherMethod">
            <summary>
            Some other method.
            </summary>
            <returns>
            Return values are described through the returns tag.
            </returns>
            <seealso cref="M:TestClass.SomeMethod(System.String)">
            Notice the use of the cref attribute to reference a specific method.
            </seealso>
        </member>
        <member name="M:TestClass.Main(System.String[])">
            <summary>
            The entry point for the application.
            </summary>
            <param name="args"> A list of command line arguments.</param>
        </member>
        <member name="T:TestInterface">
            <summary>
            Documentation that describes the interface goes here.
            </summary>
            <remarks>
            Details about the interface go here.
            </remarks>
        </member>
        <member name="M:TestInterface.InterfaceMethod(System.Int32)">
            <summary>
            Documentation that describes the method goes here.
            </summary>
            <param name="n">
            Parameter n requires an integer argument.
            </param>
            <returns>
            The method returns an integer.
            </returns>
        </member>
    </members>
</doc>
```

## <a name="compiling-the-code"></a><span data-ttu-id="7e29f-106">Compilazione del codice</span><span class="sxs-lookup"><span data-stu-id="7e29f-106">Compiling the code</span></span>

<span data-ttu-id="7e29f-107">Per compilare l'esempio, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7e29f-107">To compile the example, enter the following command:</span></span>

`csc XMLsample.cs /doc:XMLsample.xml`

<span data-ttu-id="7e29f-108">Questo comando crea il file XML *XMLsample. XML*, che è possibile visualizzare nel browser o tramite il `TYPE` comando.</span><span class="sxs-lookup"><span data-stu-id="7e29f-108">This command creates the XML file *XMLsample.xml*, which you can view in your browser or by using the `TYPE` command.</span></span>

## <a name="robust-programming"></a><span data-ttu-id="7e29f-109">Programmazione efficiente</span><span class="sxs-lookup"><span data-stu-id="7e29f-109">Robust programming</span></span>

<span data-ttu-id="7e29f-110">La documentazione XML inizia con `///` .</span><span class="sxs-lookup"><span data-stu-id="7e29f-110">XML documentation starts with `///`.</span></span> <span data-ttu-id="7e29f-111">Quando si crea un nuovo progetto, le procedure guidate inseriscono alcune `///` righe iniziali.</span><span class="sxs-lookup"><span data-stu-id="7e29f-111">When you create a new project, the wizards put some starter `///` lines in for you.</span></span> <span data-ttu-id="7e29f-112">L'elaborazione di questi commenti presenta alcune restrizioni:</span><span class="sxs-lookup"><span data-stu-id="7e29f-112">The processing of these comments has some restrictions:</span></span>

- <span data-ttu-id="7e29f-113">La documentazione deve essere in codice XML ben formato.</span><span class="sxs-lookup"><span data-stu-id="7e29f-113">The documentation must be well-formed XML.</span></span> <span data-ttu-id="7e29f-114">Se il codice XML non è ben formato, viene generato un avviso e il file di documentazione conterrà un commento che segnalerà che si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="7e29f-114">If the XML is not well-formed, a warning is generated and the documentation file will contain a comment that says that an error was encountered.</span></span>

- <span data-ttu-id="7e29f-115">Gli sviluppatori sono liberi di creare set di tag personalizzati.</span><span class="sxs-lookup"><span data-stu-id="7e29f-115">Developers are free to create their own set of tags.</span></span> <span data-ttu-id="7e29f-116">È disponibile un [set di tag consigliato](recommended-tags-for-documentation-comments.md).</span><span class="sxs-lookup"><span data-stu-id="7e29f-116">There is a [recommended set of tags](recommended-tags-for-documentation-comments.md).</span></span> <span data-ttu-id="7e29f-117">Alcuni tag consigliati hanno un significato speciale:</span><span class="sxs-lookup"><span data-stu-id="7e29f-117">Some of the recommended tags have special meanings:</span></span>

  - <span data-ttu-id="7e29f-118">Il `<param>` tag viene usato per descrivere i parametri.</span><span class="sxs-lookup"><span data-stu-id="7e29f-118">The `<param>` tag is used to describe parameters.</span></span> <span data-ttu-id="7e29f-119">Se usato, il compilatore verifica che il parametro esista e che tutti i parametri siano descritti nella documentazione.</span><span class="sxs-lookup"><span data-stu-id="7e29f-119">If used, the compiler verifies that the parameter exists and that all parameters are described in the documentation.</span></span> <span data-ttu-id="7e29f-120">Se la verifica ha esito negativo, il compilatore genera un avviso.</span><span class="sxs-lookup"><span data-stu-id="7e29f-120">If the verification fails, the compiler issues a warning.</span></span>

  - <span data-ttu-id="7e29f-121">L' `cref` attributo può essere allegato a qualsiasi tag per fare riferimento a un elemento di codice.</span><span class="sxs-lookup"><span data-stu-id="7e29f-121">The `cref` attribute can be attached to any tag to reference a code element.</span></span> <span data-ttu-id="7e29f-122">Il compilatore verifica l'esistenza di questo elemento.</span><span class="sxs-lookup"><span data-stu-id="7e29f-122">The compiler verifies that this code element exists.</span></span> <span data-ttu-id="7e29f-123">Se la verifica ha esito negativo, il compilatore genera un avviso.</span><span class="sxs-lookup"><span data-stu-id="7e29f-123">If the verification fails, the compiler issues a warning.</span></span> <span data-ttu-id="7e29f-124">Il compilatore rispetta eventuali istruzioni `using` quando esegue la ricerca di un tipo descritto nell'attributo `cref`.</span><span class="sxs-lookup"><span data-stu-id="7e29f-124">The compiler respects any `using` statements when it looks for a type described in the `cref` attribute.</span></span>

  - <span data-ttu-id="7e29f-125">Il `<summary>` tag viene usato da IntelliSense all'interno di Visual Studio per visualizzare informazioni aggiuntive su un tipo o un membro.</span><span class="sxs-lookup"><span data-stu-id="7e29f-125">The `<summary>` tag is used by IntelliSense inside Visual Studio to display additional information about a type or member.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7e29f-126">Il file XML non fornisce informazioni complete sul tipo e sui membri, ad esempio, non contiene alcuna informazione sul tipo.</span><span class="sxs-lookup"><span data-stu-id="7e29f-126">The XML file does not provide full information about the type and members (for example, it does not contain any type information).</span></span> <span data-ttu-id="7e29f-127">Per ottenere informazioni complete su un tipo o un membro, usare il file di documentazione insieme alla reflection sul tipo o sul membro effettivo.</span><span class="sxs-lookup"><span data-stu-id="7e29f-127">To get full information about a type or member, use the documentation file together with reflection on the actual type or member.</span></span>

## <a name="see-also"></a><span data-ttu-id="7e29f-128">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7e29f-128">See also</span></span>

- [<span data-ttu-id="7e29f-129">Guida per programmatori C#</span><span class="sxs-lookup"><span data-stu-id="7e29f-129">C# programming guide</span></span>](../index.md)
- [<span data-ttu-id="7e29f-130">-DOC (opzioni del compilatore C#)</span><span class="sxs-lookup"><span data-stu-id="7e29f-130">-doc (C# compiler options)</span></span>](../../language-reference/compiler-options/doc-compiler-option.md)
- [<span data-ttu-id="7e29f-131">Commenti relativi alla documentazione XML</span><span class="sxs-lookup"><span data-stu-id="7e29f-131">XML documentation comments</span></span>](./index.md)
- [<span data-ttu-id="7e29f-132">Processore della documentazione di DocFX</span><span class="sxs-lookup"><span data-stu-id="7e29f-132">DocFX documentation processor</span></span>](https://dotnet.github.io/docfx/)
- [<span data-ttu-id="7e29f-133">Processore di documentazione Sandcastle</span><span class="sxs-lookup"><span data-stu-id="7e29f-133">Sandcastle documentation processor</span></span>](https://github.com/EWSoftware/SHFB)

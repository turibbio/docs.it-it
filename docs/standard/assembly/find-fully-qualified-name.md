---
title: 'Procedura: trovare il nome completo di un assembly'
description: Questo articolo illustra come ottenere il nome completo di un assembly .NET Framework o di un assembly .NET Core.
ms.date: 08/20/2019
helpviewer_keywords:
- names [.NET Framework], fully qualified type names
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
ms.assetid: 009dae23-e1f6-4a64-9a9a-32e4c34802b0
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 346d50dc7f279ce46c9803ad60479d3111739c25
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378941"
---
# <a name="how-to-find-an-assemblys-fully-qualified-name"></a><span data-ttu-id="2fb95-103">Procedura: trovare il nome completo di un assembly</span><span class="sxs-lookup"><span data-stu-id="2fb95-103">How to: Find an assembly's fully qualified name</span></span>

<span data-ttu-id="2fb95-104">Per individuare il nome completo di un assembly .NET Framework nella Global Assembly Cache, usare lo strumento Global Assembly Cache ([gacutil. exe](../../framework/tools/gacutil-exe-gac-tool.md)).</span><span class="sxs-lookup"><span data-stu-id="2fb95-104">To discover the fully qualified name of a .NET Framework assembly in the global assembly cache, use the Global Assembly Cache tool ([Gacutil.exe](../../framework/tools/gacutil-exe-gac-tool.md)).</span></span> <span data-ttu-id="2fb95-105">Vedere [procedura: visualizzare il contenuto del Global assembly cache](../../framework/app-domains/how-to-view-the-contents-of-the-gac.md).</span><span class="sxs-lookup"><span data-stu-id="2fb95-105">See [How to: View the contents of the global assembly cache](../../framework/app-domains/how-to-view-the-contents-of-the-gac.md).</span></span>

<span data-ttu-id="2fb95-106">Per gli assembly .NET Core e per gli assembly .NET Framework che non sono inclusi nella Global Assembly Cache, è possibile ottenere il nome completo dell'assembly in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="2fb95-106">For .NET Core assemblies, and for .NET Framework assemblies that aren't in the global assembly cache, you can get the fully qualified assembly name in a number of ways:</span></span>

- <span data-ttu-id="2fb95-107">È possibile utilizzare il codice per restituire le informazioni alla console o a una variabile oppure è possibile utilizzare [Ildasm. exe (DISASSEMBLER il)](../../framework/tools/ildasm-exe-il-disassembler.md) per esaminare i metadati dell'assembly, che contengono il nome completo.</span><span class="sxs-lookup"><span data-stu-id="2fb95-107">You can use code to output the information to the console or to a variable, or you can use the [Ildasm.exe (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md) to examine the assembly's metadata, which contains the fully qualified name.</span></span>

- <span data-ttu-id="2fb95-108">Se l'assembly è già stato caricato dall'applicazione, è possibile recuperare il valore della proprietà <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> per ottenere il nome completo.</span><span class="sxs-lookup"><span data-stu-id="2fb95-108">If the assembly is already loaded by the application, you can retrieve the value of the <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> property to get the fully qualified name.</span></span> <span data-ttu-id="2fb95-109">È possibile utilizzare la <xref:System.Type.Assembly> proprietà di un <xref:System.Type> oggetto definito in tale assembly per recuperare un riferimento all' <xref:System.Reflection.Assembly> oggetto.</span><span class="sxs-lookup"><span data-stu-id="2fb95-109">You can use the <xref:System.Type.Assembly> property of a <xref:System.Type> defined in that assembly to retrieve a reference to the <xref:System.Reflection.Assembly> object.</span></span> <span data-ttu-id="2fb95-110">Nell'esempio viene illustrata una situazione di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="2fb95-110">The example provides an illustration.</span></span>

- <span data-ttu-id="2fb95-111">Se si conosce il percorso di file system dell'assembly, è possibile chiamare il `static` Metodo (C#) o `Shared` (Visual Basic) <xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=nameWithType> per ottenere il nome completo dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="2fb95-111">If you know the assembly's file system path, you can call the `static` (C#) or `Shared` (Visual Basic) <xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=nameWithType> method to get the fully qualified assembly name.</span></span> <span data-ttu-id="2fb95-112">Di seguito è riportato un esempio semplice.</span><span class="sxs-lookup"><span data-stu-id="2fb95-112">The following is a simple example.</span></span>

  ```csharp
  using System;
  using System.Reflection;

  public class Example
  {
     public static void Main()
     {
        Console.WriteLine(AssemblyName.GetAssemblyName(@".\UtilityLibrary.dll"));
     }
  }
  // The example displays output like the following:
  //   UtilityLibrary, Version=1.1.0.0, Culture=neutral, PublicKeyToken=null
  ```

  ```vb
  Imports System.Reflection

  Public Module Example
     Public Sub Main
        Console.WriteLine(AssemblyName.GetAssemblyName(".\UtilityLibrary.dll"))
     End Sub
  End Module
  ' The example displays output like the following:
  '   UtilityLibrary, Version=1.1.0.0, Culture=neutral, PublicKeyToken=null
  ```

- <span data-ttu-id="2fb95-113">È possibile usare [Ildasm.exe (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md) per esaminare i metadati dell'assembly che contengono il nome completo.</span><span class="sxs-lookup"><span data-stu-id="2fb95-113">You can use the [Ildasm.exe (IL Disassembler)](../../framework/tools/ildasm-exe-il-disassembler.md) to examine the assembly's metadata, which contains the fully qualified name.</span></span>

<span data-ttu-id="2fb95-114">Per ulteriori informazioni sull'impostazione degli attributi dell'assembly, ad esempio la versione, la lingua e il nome dell'assembly, vedere [impostare gli attributi](set-attributes.md)dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="2fb95-114">For more information about setting assembly attributes such as version, culture, and assembly name, see [Set assembly attributes](set-attributes.md).</span></span> <span data-ttu-id="2fb95-115">Per altre informazioni su come assegnare un nome sicuro a un assembly, vedere [creare e usare assembly con nome sicuro](create-use-strong-named.md).</span><span class="sxs-lookup"><span data-stu-id="2fb95-115">For more information about giving an assembly a strong name, see [Create and use strong-named assemblies](create-use-strong-named.md).</span></span>

## <a name="example"></a><span data-ttu-id="2fb95-116">Esempio</span><span class="sxs-lookup"><span data-stu-id="2fb95-116">Example</span></span>

<span data-ttu-id="2fb95-117">Nell'esempio seguente viene illustrato come visualizzare il nome completo di un assembly contenente una classe specificata nella console.</span><span class="sxs-lookup"><span data-stu-id="2fb95-117">The following example shows how to display the fully qualified name of an assembly containing a specified class to the console.</span></span> <span data-ttu-id="2fb95-118">Usa la <xref:System.Type.Assembly?displayProperty=nameWithType> proprietà per recuperare un riferimento a un assembly da un tipo definito in tale assembly.</span><span class="sxs-lookup"><span data-stu-id="2fb95-118">It uses the <xref:System.Type.Assembly?displayProperty=nameWithType> property to retrieve a reference to an assembly from a type that's defined in that assembly.</span></span>

```cpp
#using <System.dll>
#using <System.Data.dll>

using namespace System;
using namespace System::Reflection;

ref class asmname
{
public:
    static void Main()
    {
        Type^ t = System::Data::DataSet::typeid;
        String^ s = t->Assembly->FullName->ToString();
        Console::WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s);
    }
};

int main()
{
    asmname::Main();
}
```

```csharp
using System;
using System.Reflection;

class asmname
{
    public static void Main()
    {
        Type t = typeof(System.Data.DataSet);
        string s = t.Assembly.FullName.ToString();
        Console.WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s);
    }
}
```

```vb
Imports System.Reflection

Class asmname
    Public Shared Sub Main()
        Dim t As Type = GetType(System.Data.DataSet)
        Dim s As String = t.Assembly.FullName.ToString()
        Console.WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s)
    End Sub
End Class
```

## <a name="see-also"></a><span data-ttu-id="2fb95-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2fb95-119">See also</span></span>

- [<span data-ttu-id="2fb95-120">Nomi degli assembly</span><span class="sxs-lookup"><span data-stu-id="2fb95-120">Assembly names</span></span>](names.md)
- [<span data-ttu-id="2fb95-121">Creare assembly</span><span class="sxs-lookup"><span data-stu-id="2fb95-121">Create assemblies</span></span>](create.md)
- [<span data-ttu-id="2fb95-122">Creare e usare gli assembly con nome sicuro</span><span class="sxs-lookup"><span data-stu-id="2fb95-122">Create and use strong-named assemblies</span></span>](create-use-strong-named.md)
- [<span data-ttu-id="2fb95-123">Assembly Cache globale</span><span class="sxs-lookup"><span data-stu-id="2fb95-123">Global assembly cache</span></span>](../../framework/app-domains/gac.md)
- [<span data-ttu-id="2fb95-124">Come il runtime individua gli assembly</span><span class="sxs-lookup"><span data-stu-id="2fb95-124">How the runtime locates assemblies</span></span>](../../framework/deployment/how-the-runtime-locates-assemblies.md)

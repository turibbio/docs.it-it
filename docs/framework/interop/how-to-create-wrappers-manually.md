---
title: 'Procedura: Creare wrapper manualmente'
description: Creazione manuale di wrapper di tipi COM. Utilizzare un file IDL esistente o una libreria dei tipi oppure creare dichiarazioni gestite ed esportare l'assembly in una libreria dei tipi.
ms.date: 03/30/2017
helpviewer_keywords:
- wrappers, creating manually
ms.assetid: cc2a70d8-6a58-4071-a8cf-ce28c018c09b
ms.openlocfilehash: e562a7e963ff744bf9193821d54dd898db521464
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619585"
---
# <a name="how-to-create-wrappers-manually"></a><span data-ttu-id="c2149-104">Procedura: Creare wrapper manualmente</span><span class="sxs-lookup"><span data-stu-id="c2149-104">How to: Create Wrappers Manually</span></span>
<span data-ttu-id="c2149-105">Se si decide di dichiarare manualmente i tipi COM nel codice sorgente gestito, è consigliabile iniziare con una libreria dei tipi o un file IDL esistente.</span><span class="sxs-lookup"><span data-stu-id="c2149-105">If you decide to declare COM types manually in managed source code, the best place to start is with an existing Interface Definition Language (IDL) file or type library.</span></span> <span data-ttu-id="c2149-106">Se non si ha il file IDL o non è possibile generare un file di libreria dei tipi, simulare i tipi COM mediante la creazione di dichiarazioni gestite e l'esportazione dell'assembly risultante in una libreria dei tipi.</span><span class="sxs-lookup"><span data-stu-id="c2149-106">When you do not have the IDL file or cannot generate a type library file, you can simulate the COM types by creating managed declarations and exporting the resulting assembly to a type library.</span></span>  
  
### <a name="to-simulate-com-types-from-managed-source"></a><span data-ttu-id="c2149-107">Per simulare i tipi COM dall'origine gestita</span><span class="sxs-lookup"><span data-stu-id="c2149-107">To simulate COM types from managed source</span></span>  
  
1. <span data-ttu-id="c2149-108">Dichiarare i tipi in un linguaggio conformi a Common Language Specification (CLS) e compilare il file.</span><span class="sxs-lookup"><span data-stu-id="c2149-108">Declare the types in a language that is compliant with the Common Language Specification (CLS) and compile the file.</span></span>  
  
2. <span data-ttu-id="c2149-109">Esportare l'assembly contenente i tipi con l'[utilità di esportazione della libreria dei tipi (Tlbexp.exe)](../tools/tlbexp-exe-type-library-exporter.md).</span><span class="sxs-lookup"><span data-stu-id="c2149-109">Export the assembly containing the types with the [Type Library Exporter (Tlbexp.exe)](../tools/tlbexp-exe-type-library-exporter.md).</span></span>  
  
3. <span data-ttu-id="c2149-110">Usare la libreria dei tipi COM esportata come base per la dichiarazione dei tipi gestiti orientati a COM.</span><span class="sxs-lookup"><span data-stu-id="c2149-110">Use the exported COM type library as a basis for declaring COM-oriented managed types.</span></span>  
  
### <a name="to-create-a-runtime-callable-wrapper-rcw"></a><span data-ttu-id="c2149-111">Per creare un Runtime Callable Wrapper (RCW)</span><span class="sxs-lookup"><span data-stu-id="c2149-111">To create a runtime callable wrapper (RCW)</span></span>  
  
1. <span data-ttu-id="c2149-112">Se si dispone di un file IDL o di un file di libreria dei tipi, decidere quali classi e interfacce includere nell'RCW personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c2149-112">Assuming that you have an IDL file or type library file, decide which classes and interfaces you want to include in the custom RCW.</span></span> <span data-ttu-id="c2149-113">È possibile escludere i tipi che non si intende usare direttamente o indirettamente nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c2149-113">You can exclude any types that you do not intend to use directly or indirectly in your application.</span></span>  
  
2. <span data-ttu-id="c2149-114">Creare un file di origine in un linguaggio conforme a Common Language Specification e dichiarare i tipi.</span><span class="sxs-lookup"><span data-stu-id="c2149-114">Create a source file in a CLS-compliant language and declare the types.</span></span> <span data-ttu-id="c2149-115">Per una descrizione completa del processo di conversione dell'importazione, vedere [Riepilogo della conversione della libreria dei tipi in assembly](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100)).</span><span class="sxs-lookup"><span data-stu-id="c2149-115">See [Type Library to Assembly Conversion Summary](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100)) for a complete description of the import conversion process.</span></span> <span data-ttu-id="c2149-116">In pratica, quando si crea un RCW personalizzato si esegue manualmente la conversione dei tipi fornita dall'[utilità di importazione della libreria dei tipi (Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md).</span><span class="sxs-lookup"><span data-stu-id="c2149-116">Effectively, when you create a custom RCW, you are manually performing the type conversion activity provided by the [Type Library Importer (Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md).</span></span> <span data-ttu-id="c2149-117">Nell'esempio riportato nella sezione seguente vengono illustrati i tipi di un file della libreria dei tipi o IDL e i tipi corrispondenti nel codice C#.</span><span class="sxs-lookup"><span data-stu-id="c2149-117">The example in the next section shows types in an IDL or type library file and their corresponding types in C# code.</span></span>  
  
3. <span data-ttu-id="c2149-118">Dopo aver completato le dichiarazioni, compilare il file come si compila qualunque altro codice sorgente gestito.</span><span class="sxs-lookup"><span data-stu-id="c2149-118">When the declarations are complete, compile the file as you compile any other managed source code.</span></span>  
  
4. <span data-ttu-id="c2149-119">Come per i tipi importati con Tlbimp.exe, alcuni tipi richiedono altre informazioni che è possibile aggiungere direttamente al codice.</span><span class="sxs-lookup"><span data-stu-id="c2149-119">As with the types imported with Tlbimp.exe, some require additional information, which you can add directly to your code.</span></span> <span data-ttu-id="c2149-120">Per dettagli, vedere [Procedura: Modificare assembly di interoperabilità](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8zbc969t(v=vs.100)).</span><span class="sxs-lookup"><span data-stu-id="c2149-120">For details, see [How to: Edit Interop Assemblies](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8zbc969t(v=vs.100)).</span></span>  
  
## <a name="example"></a><span data-ttu-id="c2149-121">Esempio</span><span class="sxs-lookup"><span data-stu-id="c2149-121">Example</span></span>  
 <span data-ttu-id="c2149-122">Il codice seguente mostra un esempio di interfaccia `ISATest` e di classe `SATest` in IDL e i tipi corrispondenti nel codice sorgente C#.</span><span class="sxs-lookup"><span data-stu-id="c2149-122">The following code shows an example of the `ISATest` interface and `SATest` class in IDL and the corresponding types in C# source code.</span></span>  
  
 <span data-ttu-id="c2149-123">**IDL o file di libreria dei tipi**</span><span class="sxs-lookup"><span data-stu-id="c2149-123">**IDL or type library file**</span></span>  
  
```cpp
 [  
object,  
uuid(40A8C65D-2448-447A-B786-64682CBEF133),  
dual,  
helpstring("ISATest Interface"),  
pointer_default(unique)  
 ]  
interface ISATest : IDispatch  
 {  
[id(1), helpstring("method InSArray")]
HRESULT InSArray([in] SAFEARRAY(int) *ppsa, [out,retval] int *pSum);  
 };  
 [  
uuid(116CCA1E-7E39-4515-9849-90790DA6431E),  
helpstring("SATest Class")  
 ]  
coclass SATest  
 {  
  [default] interface ISATest;  
 };  
```  
  
 <span data-ttu-id="c2149-124">**Wrapper nel codice sorgente gestito**</span><span class="sxs-lookup"><span data-stu-id="c2149-124">**Wrapper in managed source code**</span></span>  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
using System.Runtime.CompilerServices;  
  
[assembly:Guid("E4A992B8-6F5C-442C-96E7-C4778924C753")]  
[assembly:ImportedFromTypeLib("SAServerLib")]  
namespace SAServer  
{  
 [ComImport]  
 [Guid("40A8C65D-2448-447A-B786-64682CBEF133")]  
 [TypeLibType(TypeLibTypeFlags.FLicensed)]  
 public interface ISATest  
 {  
  [DispId(1)]  
  //[MethodImpl(MethodImplOptions.InternalCall,  
  // MethodCodeType=MethodCodeType.Runtime)]  
  int InSArray( [MarshalAs(UnmanagedType.SafeArray,  
      SafeArraySubType=VarEnum.VT_I4)] ref int[] param );  
 }
 [ComImport]  
 [Guid("116CCA1E-7E39-4515-9849-90790DA6431E")]  
 [ClassInterface(ClassInterfaceType.None)]  
 [TypeLibType(TypeLibTypeFlags.FCanCreate)]  
 public class SATest : ISATest  
 {  
  [DispId(1)]  
  [MethodImpl(MethodImplOptions.InternalCall,
  MethodCodeType=MethodCodeType.Runtime)]  
  extern int ISATest.InSArray( [MarshalAs(UnmanagedType.SafeArray,
  SafeArraySubType=VarEnum.VT_I4)] ref int[] param );  
 }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="c2149-125">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c2149-125">See also</span></span>

- <span data-ttu-id="c2149-126">[Personalizzazione dei Runtime Callable Wrapper](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e753eftz(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="c2149-126">[Customizing Runtime Callable Wrappers](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e753eftz(v=vs.100))</span></span>
- <span data-ttu-id="c2149-127">[Tipi di dati COM](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sak564ww(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="c2149-127">[COM Data Types](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sak564ww(v=vs.100))</span></span>
- <span data-ttu-id="c2149-128">[Procedura: Modificare assembly di interoperabilità](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8zbc969t(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="c2149-128">[How to: Edit Interop Assemblies](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8zbc969t(v=vs.100))</span></span>
- <span data-ttu-id="c2149-129">[Riepilogo della conversione da libreria dei tipi ad assembly](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="c2149-129">[Type Library to Assembly Conversion Summary](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))</span></span>
- [<span data-ttu-id="c2149-130">Tlbimp.exe (utilità di importazione della libreria di tipi)</span><span class="sxs-lookup"><span data-stu-id="c2149-130">Tlbimp.exe (Type Library Importer)</span></span>](../tools/tlbimp-exe-type-library-importer.md)
- [<span data-ttu-id="c2149-131">Tlbexp.exe (utilità di esportazione della libreria di tipi)</span><span class="sxs-lookup"><span data-stu-id="c2149-131">Tlbexp.exe (Type Library Exporter)</span></span>](../tools/tlbexp-exe-type-library-exporter.md)

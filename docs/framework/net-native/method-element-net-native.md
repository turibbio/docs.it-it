---
title: <Method>Elemento (.NET Native)
ms.date: 03/30/2017
ms.assetid: 348b49e5-589d-4eb2-a597-d6ff60ab52d1
ms.openlocfilehash: 8db32c660846b4f4071fff2a40c760a3d1ef2489
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "79180979"
---
# <a name="method-element-net-native"></a><span data-ttu-id="94df8-102">\<Method>Elemento (.NET Native)</span><span class="sxs-lookup"><span data-stu-id="94df8-102">\<Method> Element (.NET Native)</span></span>
<span data-ttu-id="94df8-103">Applica i criteri di reflection di runtime a un costruttore o a un metodo.</span><span class="sxs-lookup"><span data-stu-id="94df8-103">Applies runtime reflection policy to a constructor or method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="94df8-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="94df8-104">Syntax</span></span>  
  
```xml  
<Method Name="method_name"  
        Signature="method_signature"  
        Browse="policy_type"  
        Dynamic="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="94df8-105">Attributi ed elementi</span><span class="sxs-lookup"><span data-stu-id="94df8-105">Attributes and Elements</span></span>  
 <span data-ttu-id="94df8-106">Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="94df8-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="94df8-107">Attributi</span><span class="sxs-lookup"><span data-stu-id="94df8-107">Attributes</span></span>  
  
|<span data-ttu-id="94df8-108">Attributo</span><span class="sxs-lookup"><span data-stu-id="94df8-108">Attribute</span></span>|<span data-ttu-id="94df8-109">Tipo di attributo</span><span class="sxs-lookup"><span data-stu-id="94df8-109">Attribute type</span></span>|<span data-ttu-id="94df8-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94df8-110">Description</span></span>|  
|---------------|--------------------|-----------------|  
|`Name`|<span data-ttu-id="94df8-111">Generale</span><span class="sxs-lookup"><span data-stu-id="94df8-111">General</span></span>|<span data-ttu-id="94df8-112">Attributo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="94df8-112">Required attribute.</span></span> <span data-ttu-id="94df8-113">Specifica il nome del metodo.</span><span class="sxs-lookup"><span data-stu-id="94df8-113">Specifies the method name.</span></span>|  
|`Signature`|<span data-ttu-id="94df8-114">Generale</span><span class="sxs-lookup"><span data-stu-id="94df8-114">General</span></span>|<span data-ttu-id="94df8-115">Attributo facoltativo.</span><span class="sxs-lookup"><span data-stu-id="94df8-115">Optional attribute.</span></span> <span data-ttu-id="94df8-116">Specifica la firma del metodo.</span><span class="sxs-lookup"><span data-stu-id="94df8-116">Specifies the method signature.</span></span> <span data-ttu-id="94df8-117">Se esistono più parametri, sono separati da virgole.</span><span class="sxs-lookup"><span data-stu-id="94df8-117">If multiple parameters are present, they are separated by commas.</span></span> <span data-ttu-id="94df8-118">Ad esempio, l'elemento `<Method>` seguente definire i criteri del metodo <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29>.</span><span class="sxs-lookup"><span data-stu-id="94df8-118">For example, the following `<Method>` element defines policy for the <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29> method.</span></span><br /><br /> `<Type Name="System.DateTime">    <Method Name="ToString" Signature="System.String,System.IFormatProvider"            Dynamic="Required" /> </Type>`<br /><br /> <span data-ttu-id="94df8-119">Se l'attributo è assente, la direttiva di runtime si applica a tutti gli overload del metodo.</span><span class="sxs-lookup"><span data-stu-id="94df8-119">If the attribute is absent, the runtime directive applies to all overloads of the method.</span></span>|  
|`Browse`|<span data-ttu-id="94df8-120">Reflection</span><span class="sxs-lookup"><span data-stu-id="94df8-120">Reflection</span></span>|<span data-ttu-id="94df8-121">Attributo facoltativo.</span><span class="sxs-lookup"><span data-stu-id="94df8-121">Optional attribute.</span></span> <span data-ttu-id="94df8-122">Controlla l'esecuzione di query per informazioni sul metodo o la sua enumerazione, ma non abilita alcuna chiamata dinamica in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="94df8-122">Controls querying for information about or enumerating a method but does not enable any dynamic invocation at run time.</span></span>|  
|`Dynamic`|<span data-ttu-id="94df8-123">Reflection</span><span class="sxs-lookup"><span data-stu-id="94df8-123">Reflection</span></span>|<span data-ttu-id="94df8-124">Attributo facoltativo.</span><span class="sxs-lookup"><span data-stu-id="94df8-124">Optional attribute.</span></span> <span data-ttu-id="94df8-125">Controlla l'accesso del runtime a un costruttore o al metodo per attivare la programmazione dinamica.</span><span class="sxs-lookup"><span data-stu-id="94df8-125">Controls runtime access to a constructor or method to enable dynamic programming.</span></span> <span data-ttu-id="94df8-126">Questo criterio assicura che un membro possa essere richiamato in modo dinamico in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="94df8-126">This policy ensures that a member can be invoked dynamically at run time.</span></span>|  
  
## <a name="name-attribute"></a><span data-ttu-id="94df8-127">Name (attributo)</span><span class="sxs-lookup"><span data-stu-id="94df8-127">Name attribute</span></span>  
  
|<span data-ttu-id="94df8-128">Valore</span><span class="sxs-lookup"><span data-stu-id="94df8-128">Value</span></span>|<span data-ttu-id="94df8-129">Description</span><span class="sxs-lookup"><span data-stu-id="94df8-129">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="94df8-130">*method_name*</span><span class="sxs-lookup"><span data-stu-id="94df8-130">*method_name*</span></span>|<span data-ttu-id="94df8-131">Nome del metodo.</span><span class="sxs-lookup"><span data-stu-id="94df8-131">The method name.</span></span> <span data-ttu-id="94df8-132">Il tipo del metodo viene definito dall' [\<Type>](type-element-net-native.md) elemento padre o [\<TypeInstantiation>](typeinstantiation-element-net-native.md) .</span><span class="sxs-lookup"><span data-stu-id="94df8-132">The type of the method is defined by the parent [\<Type>](type-element-net-native.md) or [\<TypeInstantiation>](typeinstantiation-element-net-native.md) element.</span></span>|  
  
## <a name="signature-attribute"></a><span data-ttu-id="94df8-133">Attributo Signature</span><span class="sxs-lookup"><span data-stu-id="94df8-133">Signature attribute</span></span>  
  
|<span data-ttu-id="94df8-134">Valore</span><span class="sxs-lookup"><span data-stu-id="94df8-134">Value</span></span>|<span data-ttu-id="94df8-135">Description</span><span class="sxs-lookup"><span data-stu-id="94df8-135">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="94df8-136">*method_signature*</span><span class="sxs-lookup"><span data-stu-id="94df8-136">*method_signature*</span></span>|<span data-ttu-id="94df8-137">Tipi di parametri che costituiscono la firma del metodo.</span><span class="sxs-lookup"><span data-stu-id="94df8-137">The parameter types that form the method signature.</span></span> <span data-ttu-id="94df8-138">Più parametri sono separati da virgole, ad esempio `"System.String,System.Int32,System.Int32)"`.</span><span class="sxs-lookup"><span data-stu-id="94df8-138">Multiple parameters are separated by commas, for example, `"System.String,System.Int32,System.Int32)"`.</span></span> <span data-ttu-id="94df8-139">I nomi del tipo di parametro devono essere completi.</span><span class="sxs-lookup"><span data-stu-id="94df8-139">Parameter type names should be fully qualified.</span></span>|  
  
## <a name="all-other-attributes"></a><span data-ttu-id="94df8-140">Tutti gli altri attributi</span><span class="sxs-lookup"><span data-stu-id="94df8-140">All other attributes</span></span>  
  
|<span data-ttu-id="94df8-141">Valore</span><span class="sxs-lookup"><span data-stu-id="94df8-141">Value</span></span>|<span data-ttu-id="94df8-142">Description</span><span class="sxs-lookup"><span data-stu-id="94df8-142">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="94df8-143">*policy_setting*</span><span class="sxs-lookup"><span data-stu-id="94df8-143">*policy_setting*</span></span>|<span data-ttu-id="94df8-144">L'impostazione da applicare a questo tipo di criteri.</span><span class="sxs-lookup"><span data-stu-id="94df8-144">The setting to apply to this policy type.</span></span> <span data-ttu-id="94df8-145">I valori consentiti sono `Auto`, `Excluded`, `Included` e `Required`.</span><span class="sxs-lookup"><span data-stu-id="94df8-145">Possible values are `Auto`, `Excluded`, `Included`, and `Required`.</span></span> <span data-ttu-id="94df8-146">Per altre informazioni, vedere [Runtime Directive Policy Settings](runtime-directive-policy-settings.md) (Impostazioni dei criteri delle direttive di runtime).</span><span class="sxs-lookup"><span data-stu-id="94df8-146">For more information, see [Runtime Directive Policy Settings](runtime-directive-policy-settings.md).</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="94df8-147">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="94df8-147">Child Elements</span></span>  
  
|<span data-ttu-id="94df8-148">Elemento</span><span class="sxs-lookup"><span data-stu-id="94df8-148">Element</span></span>|<span data-ttu-id="94df8-149">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94df8-149">Description</span></span>|  
|-------------|-----------------|  
|[\<Parameter>](parameter-element-net-native.md)|<span data-ttu-id="94df8-150">Applica i criteri al tipo di argomento passato a un metodo.</span><span class="sxs-lookup"><span data-stu-id="94df8-150">Applies policy to the type of the argument passed to a method.</span></span>|  
|[\<GenericParameter>](genericparameter-element-net-native.md)|<span data-ttu-id="94df8-151">Applica i criteri al tipo di parametro di un tipo o di un metodo generico.</span><span class="sxs-lookup"><span data-stu-id="94df8-151">Applies policy to the parameter type of a generic type or method.</span></span>|  
|[\<ImpliesType>](impliestype-element-net-native.md)|<span data-ttu-id="94df8-152">Applica criteri a un tipo, se tale criterio è stato applicato al metodo rappresentato dall'oggetto contenente l'elemento `<Method>`.</span><span class="sxs-lookup"><span data-stu-id="94df8-152">Applies policy to a type, if that policy has been applied to the method represented by the containing `<Method>` element.</span></span>|  
|[\<TypeParameter>](typeparameter-element-net-native.md)|<span data-ttu-id="94df8-153">Applica i criteri al tipo rappresentato da un argomento <xref:System.Type> passato a un metodo.</span><span class="sxs-lookup"><span data-stu-id="94df8-153">Applies policy to the type represented by a <xref:System.Type> argument passed to a method.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="94df8-154">Elementi padre</span><span class="sxs-lookup"><span data-stu-id="94df8-154">Parent Elements</span></span>  
  
|<span data-ttu-id="94df8-155">Elemento</span><span class="sxs-lookup"><span data-stu-id="94df8-155">Element</span></span>|<span data-ttu-id="94df8-156">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94df8-156">Description</span></span>|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|<span data-ttu-id="94df8-157">Applica i criteri di reflection a un tipo e a tutti i membri.</span><span class="sxs-lookup"><span data-stu-id="94df8-157">Applies reflection policy to a type and all its members.</span></span>|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|<span data-ttu-id="94df8-158">Applica i criteri di reflection a un tipo generico costruito e a tutti i membri.</span><span class="sxs-lookup"><span data-stu-id="94df8-158">Applies reflection policy to a constructed generic type and all its members.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="94df8-159">Commenti</span><span class="sxs-lookup"><span data-stu-id="94df8-159">Remarks</span></span>  
 <span data-ttu-id="94df8-160">Un elemento `<Method>` di un metodo generico applica i relativi criteri a tutte le istanze che non dispongono di propri criteri.</span><span class="sxs-lookup"><span data-stu-id="94df8-160">A `<Method>` element of a generic method applies its policy to all instantiations that do not have their own policy.</span></span>  
  
 <span data-ttu-id="94df8-161">È possibile usare l'attributo `Signature` per specificare criteri per un overload del metodo specifico.</span><span class="sxs-lookup"><span data-stu-id="94df8-161">You can use the `Signature` attribute to specify policy for a particular method overload.</span></span> <span data-ttu-id="94df8-162">In caso contrario, se l'attributo `Signature` è assente, la direttiva di runtime si applica a tutti gli overload del metodo.</span><span class="sxs-lookup"><span data-stu-id="94df8-162">Otherwise, if the `Signature` attribute is absent, the runtime directive applies to all overloads of the method.</span></span>  
  
 <span data-ttu-id="94df8-163">Non è possibile definire i criteri di reflection di runtime per un costruttore con l'elemento `<Method>`.</span><span class="sxs-lookup"><span data-stu-id="94df8-163">You cannot define the runtime reflection policy for a constructor by using the `<Method>` element.</span></span> <span data-ttu-id="94df8-164">Usare invece l' `Activate` attributo dell' [\<Assembly>](assembly-element-net-native.md) [\<Namespace>](namespace-element-net-native.md) elemento,, [\<Type>](type-element-net-native.md) o [\<TypeInstantiation>](typeinstantiation-element-net-native.md) .</span><span class="sxs-lookup"><span data-stu-id="94df8-164">Instead, use the `Activate` attribute of the  [\<Assembly>](assembly-element-net-native.md), [\<Namespace>](namespace-element-net-native.md), [\<Type>](type-element-net-native.md), or [\<TypeInstantiation>](typeinstantiation-element-net-native.md) element.</span></span>  
  
## <a name="example"></a><span data-ttu-id="94df8-165">Esempio</span><span class="sxs-lookup"><span data-stu-id="94df8-165">Example</span></span>  
 <span data-ttu-id="94df8-166">Il metodo `Stringify` nell'esempio seguente è un metodo di formattazione generico che usa la reflection per convertire un oggetto nella relativa rappresentazione di stringa.</span><span class="sxs-lookup"><span data-stu-id="94df8-166">The `Stringify` method in the following example is a general-purpose formatting method that uses reflection to convert an object to its string representation.</span></span> <span data-ttu-id="94df8-167">Oltre a chiamare il metodo `ToString` predefinito dell'oggetto, il metodo può produrre una stringa di risultato formattata passando il metodo `ToString` di un oggetto a una stringa di formato, un'implementazione di <xref:System.IFormatProvider> o entrambi.</span><span class="sxs-lookup"><span data-stu-id="94df8-167">In addition to calling the object's default `ToString` method, the method can produce a formatted result string by passing an object's `ToString` method a format string, an <xref:System.IFormatProvider> implementation, or both.</span></span> <span data-ttu-id="94df8-168">Il metodo può anche chiamare uno degli overload <xref:System.Convert.ToString%2A?displayProperty=nameWithType> che converte un numero nella relativa rappresentazione binaria, ottale o esadecimale.</span><span class="sxs-lookup"><span data-stu-id="94df8-168">It can also call one of the <xref:System.Convert.ToString%2A?displayProperty=nameWithType> overloads that converts a number to its binary, hexadecimal, or octal representation.</span></span>  
  
 [!code-csharp[ProjectN_Reflection#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/method1.cs#7)]  
  
 <span data-ttu-id="94df8-169">Il metodo `Stringify` può essere chiamato da codice simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="94df8-169">The `Stringify` method can be called by code like the following:</span></span>  
  
 [!code-csharp[ProjectN_Reflection#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/method1.cs#7)]  
  
 <span data-ttu-id="94df8-170">Tuttavia, quando viene compilato con .NET Native, l'esempio può generare una serie di eccezioni in fase di esecuzione, incluse le eccezioni <xref:System.NullReferenceException> e [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md). Ciò si verifica perché il metodo `Stringify` è destinato principalmente a supportare la formattazione dinamica dei tipi primitivi nella libreria di classi .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="94df8-170">However, when compiled with .NET Native, the example can throw an number of exceptions at runtime, including <xref:System.NullReferenceException> and [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) exceptions, This occurs because the `Stringify` method is intended primarily to support dynamically formatting the primitive types in the .NET Framework Class Library.</span></span> <span data-ttu-id="94df8-171">Tuttavia, i metadati non vengono resi disponibili dal file di direttive predefinito.</span><span class="sxs-lookup"><span data-stu-id="94df8-171">However, their metadata is not made available by the default directives file.</span></span> <span data-ttu-id="94df8-172">Anche quando i metadati vengono resi disponibili, tuttavia, l'esempio genererà le eccezioni [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) perché le implementazioni `ToString` appropriate non sono state incluse nel codice nativo.</span><span class="sxs-lookup"><span data-stu-id="94df8-172">Even when their metadata is made available, however, the example throws [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) exceptions because the appropriate `ToString` implementations have not been include in the native code.</span></span>  
  
 <span data-ttu-id="94df8-173">Queste eccezioni possono essere eliminate usando l' [\<Type>](type-element-net-native.md) elemento per definire i tipi i cui metadati devono essere presenti e aggiungendo `<Method>` elementi per garantire che sia presente anche l'implementazione degli overload del metodo che possono essere chiamati dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="94df8-173">These exceptions can all be eliminated by using the [\<Type>](type-element-net-native.md) element to define the types whose metadata must be present, and by adding `<Method>` elements to ensure that the implementation of method overloads that can be called dynamically is also present.</span></span> <span data-ttu-id="94df8-174">Di seguito è riportato il file default.rd.xml che elimina queste eccezioni e consente l'esecuzione dell'esempio senza errori.</span><span class="sxs-lookup"><span data-stu-id="94df8-174">The following is the default.rd.xml file that eliminates these exceptions and allows the example to execute without error.</span></span>  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
     <Assembly Name="*Application*" Dynamic="Required All" />  
  
     <Type Name = "System.Convert" Browse="Required Public" Dynamic="Required Public" >  
        <Method Name="ToString"    Dynamic ="Required" />  
     </Type>  
     <Type Name="System.Double" Browse="Required Public">  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Type Name ="System.Int32" Browse="Required Public" >  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Type Name ="System.Int64" Browse="Required Public" >  
        <Method Name="ToString" Dynamic="Required" />  
     </Type>  
     <Namespace Name="System" >  
        <Type Name="Byte" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="DateTime" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Decimal" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Guid" Browse ="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Int16" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="SByte" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="Single" Browse="Required Public" >  
          <Method Name="ToString" Dynamic="Required" />
        </Type>  
        <Type Name="TimeSpan" Browse="Required Public" >  
          <Method Name="ToString" Dynamic="Required" />
        </Type>  
        <Type Name="UInt16" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="UInt32" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
        <Type Name="UInt64" Browse="Required Public" >  
           <Method Name="ToString" Dynamic="Required" />  
        </Type>  
     </Namespace>  
  </Application>  
</Directives>  
```  
  
## <a name="see-also"></a><span data-ttu-id="94df8-175">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="94df8-175">See also</span></span>

- [<span data-ttu-id="94df8-176">Riferimento a file di configurazione di direttive di runtime (rd.xml)</span><span class="sxs-lookup"><span data-stu-id="94df8-176">Runtime Directives (rd.xml) Configuration File Reference</span></span>](runtime-directives-rd-xml-configuration-file-reference.md)
- [<span data-ttu-id="94df8-177">Elementi direttiva di runtime</span><span class="sxs-lookup"><span data-stu-id="94df8-177">Runtime Directive Elements</span></span>](runtime-directive-elements.md)
- [<span data-ttu-id="94df8-178">Impostazioni dei criteri della direttiva di runtime</span><span class="sxs-lookup"><span data-stu-id="94df8-178">Runtime Directive Policy Settings</span></span>](runtime-directive-policy-settings.md)
- [<span data-ttu-id="94df8-179">\<MethodInstantiation>Elemento</span><span class="sxs-lookup"><span data-stu-id="94df8-179">\<MethodInstantiation> Element</span></span>](methodinstantiation-element-net-native.md)

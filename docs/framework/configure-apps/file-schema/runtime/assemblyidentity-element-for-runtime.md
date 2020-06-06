---
title: Elemento <assemblyIdentity> per <runtime>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/assemblyIdentity
- http://schemas.microsoft.com/.NetConfiguration/v2.0#assemblyIdentity
helpviewer_keywords:
- <assemblyIdentity> element
- container tags, <assemblyIdentity> element
- assemblyIdentity element
ms.assetid: cea4d187-6398-4da4-af09-c1abc6a349c1
ms.openlocfilehash: b026dafbde796bbd8726de56b532ed6710ba2290
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "79154309"
---
# <a name="assemblyidentity-element-for-runtime"></a>Elemento \<assemblyIdentity> per \<runtime>
Contiene informazioni di identificazione sull'assembly.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<assemblyBinding>**](assemblybinding-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<dependentAssembly>**](dependentassembly-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<assemblyIdentity>**  
  
## <a name="syntax"></a>Sintassi  
  
```xml  
   <assemblyIdentity
name="assembly name"  
publicKeyToken="public key token"  
culture="assembly culture"/>  
```  
  
## <a name="attributes-and-elements"></a>Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`name`|Attributo obbligatorio.<br /><br /> Nome dell'assembly|  
|`culture`|Attributo facoltativo.<br /><br /> Stringa che specifica la lingua e il paese/area geografica dell'assembly.|  
|`publicKeyToken`|Attributo facoltativo.<br /><br /> Valore esadecimale che specifica il nome sicuro dell'assembly.|  
|`processorArchitecture`|Attributo facoltativo.<br /><br /> Uno dei valori "x86", "amd64", "MSIL" o "ia64", che specifica l'architettura del processore per un assembly che contiene codice specifico del processore. I valori non fanno distinzione tra maiuscole e minuscole. Se all'attributo viene assegnato qualsiasi altro valore, l'intero `<assemblyIdentity>` elemento viene ignorato. Vedere <xref:System.Reflection.ProcessorArchitecture>.|  
  
## <a name="processorarchitecture-attribute"></a>Attributo processorArchitecture  
  
|Valore|Description|  
|-----------|-----------------|  
|`amd64`|Solo architettura AMD x86-64.|  
|`ia64`|Solo architettura Intel Itanium.|  
|`msil`|Neutro rispetto al processore e i bit per parola.|  
|`x86`|Un processore x86 a 32 bit, nativo o nell'ambiente Windows in Windows (WOW) su una piattaforma a 64 bit.|  
  
### <a name="child-elements"></a>Elementi figlio  
 No.  
  
### <a name="parent-elements"></a>Elementi padre  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|`assemblyBinding`|Contiene le informazioni sul reindirizzamento della versione degli assembly e i relativi percorsi.|  
|`configuration`|Elemento radice in ciascun file di configurazione usato in Common Language Runtime e nelle applicazioni .NET Framework.|  
|`dependentAssembly`|Incapsula i criteri di associazione e il percorso dell'assembly per ciascun assembly. Usare un `<dependentAssembly>` elemento per ogni assembly.|  
|`runtime`|Contiene informazioni sull'associazione degli assembly e sull'operazione di Garbage Collection.|  
  
## <a name="remarks"></a>Commenti  
 Ogni **\<dependentAssembly>** elemento deve avere un **\<assemblyIdentity>** elemento figlio.  
  
 Se l' `processorArchitecture` attributo è presente, l' `<assemblyIdentity>` elemento si applica solo all'assembly con l'architettura del processore corrispondente. Se l' `processorArchitecture` attributo non è presente, l' `<assemblyIdentity>` elemento può essere applicato a un assembly con qualsiasi architettura del processore.  
  
 Nell'esempio seguente viene illustrato un file di configurazione per due assembly con lo stesso nome che hanno come destinazione due diverse architetture del processore e le cui versioni non sono state mantenute in sincronizzazione. Quando l'applicazione viene eseguita sulla piattaforma x86 `<assemblyIdentity>` , viene applicato il primo elemento e l'altro viene ignorato. Se l'applicazione viene eseguita su una piattaforma diversa da x86 o ia64, entrambi vengono ignorati.  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="MyAssembly"  
                  publicKeyToken="14a739be0244c389"  
                  culture="neutral"  
                  processorArchitecture="x86" />  
            <bindingRedirect oldVersion= "1.0.0.0"
                  newVersion="1.1.0.0" />  
         </dependentAssembly>  
         <dependentAssembly>  
            <assemblyIdentity name="MyAssembly"  
                  publicKeyToken="14a739be0244c389"  
                  culture="neutral"
                  processorArchitecture="ia64" />  
            <bindingRedirect oldVersion="1.0.0.0"
                  newVersion="2.0.0.0" />  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 Se un file di configurazione contiene un `<assemblyIdentity>` elemento senza `processorArchitecture` attributo e non contiene un elemento che corrisponde alla piattaforma, viene utilizzato l'elemento senza l' `processorArchitecture` attributo.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come fornire informazioni su un assembly.  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <!--Redirection and codeBase policy for myAssembly.-->  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Vedi anche

- [Schema delle impostazioni di runtime](index.md)
- [Schema del file di configurazione](../index.md)
- [Reindirizzamento delle versioni di assembly](../../redirect-assembly-versions.md)

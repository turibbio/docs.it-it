---
title: Configurazione del reindirizzamento dell'associazione di assembly
description: Vedere come configurare il reindirizzamento dell'associazione di assembly in .NET usando l'attributo appliesTo nell'elemento assembly di un file di configurazione dell'applicazione.
ms.date: 03/30/2017
helpviewer_keywords:
- side-by-side execution, assembly binding redirection
- assemblies [.NET Framework], binding redirection
ms.assetid: d266cbd8-bf91-41d1-baf0-afbc481a741f
ms.openlocfilehash: 8f3e2270d92e11ea467d6cefc2b19b4faff563b4
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621730"
---
# <a name="configuring-assembly-binding-redirection"></a>Configurazione del reindirizzamento dell'associazione di assembly
Per impostazione predefinita, le applicazioni usano l'insieme di assembly .NET Framework fornito con la versione di runtime usata per compilare l'applicazione. È possibile usare l'attributo **appliesTo** [\<assemblyBinding>](../configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) nell'elemento in un file di configurazione dell'applicazione per reindirizzare i riferimenti di associazione di assembly a una versione specifica degli assembly di .NET Framework. Questo attributo facoltativo usa un numero di versione di .NET Framework per indicare la versione a cui deve essere applicato. Se non è specificato alcun attributo **appliesTo** , l' **\<assemblyBinding>** elemento si applica a tutte le versioni del .NET Framework.  
  
 L'attributo **appliesTo** è stato introdotto in .NET Framework versione 1.1 e viene ignorato dalla versione 1.0. Ciò significa che tutti **\<assemblyBinding>** gli elementi vengono applicati quando si usa la versione di .NET Framework 1,0, anche se viene specificato un attributo **appliesTo** .  
  
> [!NOTE]
> Usare l'attributo **appliesTo** per limitare il reindirizzamento dell'associazione di assembly a una specifica versione del runtime.  
  
 Ad esempio, per reindirizzare un'associazione di assembly per un assembly di .NET Framework versione 1.0, è necessario includere il codice XML seguente nel file di configurazione dell'applicazione.  
  
```xml  
<runtime>  
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
            <dependentAssembly>
               * assembly information goes here *  
            </dependentAssembly>  
       </assemblyBinding>  
</runtime>  
```  
  
 Gli **\<assemblyBinding>** elementi sono sensibili agli ordini. È necessario immettere prima le informazioni di reindirizzamento di associazione di assembly per gli assembly di .NET Framework versione 1.0, poi le informazioni di reindirizzamento di associazione di assembly per gli assembly di .NET Framework versione 1.1. Immettere infine le informazioni di reindirizzamento dell'binding di assembly per qualsiasi reindirizzamento di assembly .NET Framework in cui non viene usato l'attributo **appliesTo** e che quindi viene applicato a tutte le versioni di .NET Framework. In caso di conflitto nel reindirizzamento, verrà usata la prima istruzione di reindirizzamento corrispondente nel file di configurazione.  
  
 Per reindirizzare, ad esempio, un riferimento a un assembly di .NET Framework versione 1.0 e un altro riferimento a un assembly di .NET Framework versione 1.1, è possibile usare il modello illustrato nel frammento di codice che segue.  
  
```xml  
<assemblyBinding xmlns="..." appliesTo="v1.0.3705">
  <!-- .NET Framework version 1.0 redirects here. -->
</assemblyBinding>
  
<assemblyBinding xmlns="..." appliesTo="v1.1.4322">
  <!-- .NET Framework version 1.1 redirects here. -->
</assemblyBinding>
  
<assemblyBinding xmlns="...">
  <!-- Redirects meant for all versions of the .NET Framework. -->
</assemblyBinding>  
```  
  
## <a name="debugging-configuration-file-errors"></a>Debug degli errori del file di configurazione  
 I file di configurazione vengono analizzati nel runtime al momento della creazione di un dominio applicazione e vengono quindi caricati in tale dominio applicazione. In Common Language Runtime, gli errori in un file di configurazione vengono gestiti ignorando la voce che genera l'errore. Un file di configurazione contenente XML in formato non corretto viene ignorato completamente.  In caso di codice XML non valido, verranno ignorate solo le sezioni non valide.  
  
 È possibile determinare se un file di configurazione viene usato determinando se si verificano reindirizzamenti dell'associazione di assembly. Per visualizzare gli assembly caricati usare [Fuslogvw.exe (Visualizzatore log associazioni assembly)](../tools/fuslogvw-exe-assembly-binding-log-viewer.md). Per visualizzare tutte le associazioni di assembly è necessario impostare una voce per **ForceLog** nel Registro di sistema.  
  
## <a name="see-also"></a>Vedere anche

- [Procedura: Abilitare e disabilitare il reindirizzamento di associazione automatico](../configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)

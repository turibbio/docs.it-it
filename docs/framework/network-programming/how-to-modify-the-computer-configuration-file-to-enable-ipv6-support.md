---
title: 'Procedura: Modificare il file di configurazione del computer per abilitare il supporto IPv6'
description: Informazioni su come modificare il file di configurazione del computer, Machine. config, per abilitare il supporto IPv6 nel .NET Framework.
ms.date: 03/30/2017
ms.assetid: 5611b677-b9cc-43b8-a434-60e18d89aada
ms.openlocfilehash: eb7b3665c0dbcf0edefa8c48a9e69297d7259067
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502522"
---
# <a name="how-to-modify-the-computer-configuration-file-to-enable-ipv6-support"></a><span data-ttu-id="011f4-103">Procedura: Modificare il file di configurazione del computer per abilitare il supporto IPv6</span><span class="sxs-lookup"><span data-stu-id="011f4-103">How to: Modify the Computer Configuration File to Enable IPv6 Support</span></span>
<span data-ttu-id="011f4-104">L'esempio di codice seguente mostra come modificare il file di configurazione del computer, *machine.config*, per abilitare il supporto di IPv6.</span><span class="sxs-lookup"><span data-stu-id="011f4-104">The following code example shows how to modify the computer configuration file, *machine.config*, to enable IPv6 support.</span></span> <span data-ttu-id="011f4-105">Il file *machine.config* è archiviato nella cartella *%Windir%\Microsoft.NET\Framework* nella directory in cui è installato Windows.</span><span class="sxs-lookup"><span data-stu-id="011f4-105">The *machine.config* file is stored in the *%Windir%\Microsoft.NET\Framework* folder in the directory where Windows was installed.</span></span> <span data-ttu-id="011f4-106">Esiste un file *machine.config* separato nelle cartelle *%Windir%\Microsoft.NET\Framework* per ogni versione di .NET Framework installata nel computer, ad esempio *C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\machine.config*.</span><span class="sxs-lookup"><span data-stu-id="011f4-106">There is a separate *machine.config* file in the folders under *%Windir%\Microsoft.NET\Framework* for each version of the .NET Framework installed on the computer (for example, *C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\machine.config*).</span></span>  
  
 <span data-ttu-id="011f4-107">Queste impostazioni possono essere effettuate anche nel file di configurazione dell'applicazione, che ha la precedenza sul file di configurazione del computer.</span><span class="sxs-lookup"><span data-stu-id="011f4-107">These settings can also be made in the configuration file for the application, which has precedence over the computer configuration file.</span></span>  
  
 <span data-ttu-id="011f4-108">Per .NET Framework versione 1.1 e versioni precedenti, il valore dell'opzione di configurazione **ipv6 enabled** specifica se i membri della classe <xref:System.Net.Dns?displayProperty=nameWithType> restituiscono indirizzi IPv6.</span><span class="sxs-lookup"><span data-stu-id="011f4-108">For .NET Framework version 1.1 and earlier, the value of the **ipv6 enabled** configuration switch specifies whether members of the <xref:System.Net.Dns?displayProperty=nameWithType> class return IPv6 addresses.</span></span>  
  
 <span data-ttu-id="011f4-109">Per .NET Framework versione 2.0 e versioni successive, se Windows supporta IPv6, tutti i membri della classe <xref:System.Net.Dns?displayProperty=nameWithType> (ad esempio, il metodo <xref:System.Net.Dns.GetHostEntry%2A?displayProperty=nameWithType>) restituiscono indirizzi IPv6 con una limitazione.</span><span class="sxs-lookup"><span data-stu-id="011f4-109">For .NET Framework version 2.0 and later, if Windows supports IPv6, then all members of the <xref:System.Net.Dns?displayProperty=nameWithType> class (for example, the <xref:System.Net.Dns.GetHostEntry%2A?displayProperty=nameWithType> method), will return IPv6 addresses with one limitation.</span></span> <span data-ttu-id="011f4-110">I membri obsoleti della classe <xref:System.Net.Dns?displayProperty=nameWithType> (ad esempio, il metodo <xref:System.Net.Dns.Resolve%2A?displayProperty=nameWithType>) leggeranno e riconosceranno il valore nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="011f4-110">Obsolete members of the <xref:System.Net.Dns?displayProperty=nameWithType> class (for example, the <xref:System.Net.Dns.Resolve%2A?displayProperty=nameWithType> method) will read and recognize the value in the configuration file.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="011f4-111">Per .NET Framework versione 2.0 e versioni successive, IPv6 è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="011f4-111">For .NET Framework version 2.0 and later, IPv6 is enabled by default.</span></span> <span data-ttu-id="011f4-112">Per .NET Framework versione 1.1 e versioni precedenti, IPv6 è disabilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="011f4-112">For .NET Framework version 1.1 and earlier, IPv6 is disabled by default.</span></span>  
  
## <a name="example"></a><span data-ttu-id="011f4-113">Esempio</span><span class="sxs-lookup"><span data-stu-id="011f4-113">Example</span></span>  
  
```xml  
<system.net>  
    …………  
    <settings>  
        …………  
        <ipv6 enabled="true"/>
    ……………  
    </settings>  
    ………………  
</system.net>  
```  
  
## <a name="see-also"></a><span data-ttu-id="011f4-114">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="011f4-114">See also</span></span>

- [<span data-ttu-id="011f4-115">Indirizzamento IPv6</span><span class="sxs-lookup"><span data-stu-id="011f4-115">IPv6 Addressing</span></span>](ipv6-addressing.md)
- [<span data-ttu-id="011f4-116">Schema delle impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="011f4-116">Network Settings Schema</span></span>](../configure-apps/file-schema/network/index.md)
- [<span data-ttu-id="011f4-117">\<ipv6>Elemento (impostazioni di rete)</span><span class="sxs-lookup"><span data-stu-id="011f4-117">\<ipv6> Element (Network Settings)</span></span>](../configure-apps/file-schema/network/ipv6-element-network-settings.md)

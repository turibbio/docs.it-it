---
title: <cryptographySettings> Elemento
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#cryptographySettings
helpviewer_keywords:
- cryptographySettings element
- <cryptographySettings> element
ms.assetid: 6201b7da-bcb7-49f7-b9f5-ba1fe05573b9
ms.openlocfilehash: fe6de09213c6f980e8eb205a318aae50033b2a84
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "79155232"
---
# <a name="cryptographysettings-element"></a><span data-ttu-id="901f2-102">\<cryptographySettings> Elemento</span><span class="sxs-lookup"><span data-stu-id="901f2-102">\<cryptographySettings> Element</span></span>
<span data-ttu-id="901f2-103">Contiene le impostazioni di crittografia.</span><span class="sxs-lookup"><span data-stu-id="901f2-103">Contains cryptography settings.</span></span>  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<mscorlib>**](mscorlib-element-for-cryptography-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<cryptographySettings>**

## <a name="syntax"></a><span data-ttu-id="901f2-104">Sintassi</span><span class="sxs-lookup"><span data-stu-id="901f2-104">Syntax</span></span>  
  
```xml  
      <cryptographySettings>
</cryptographySettings>  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="901f2-105">Attributi ed elementi</span><span class="sxs-lookup"><span data-stu-id="901f2-105">Attributes and Elements</span></span>  
 <span data-ttu-id="901f2-106">Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.</span><span class="sxs-lookup"><span data-stu-id="901f2-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="901f2-107">Attributi</span><span class="sxs-lookup"><span data-stu-id="901f2-107">Attributes</span></span>  
 <span data-ttu-id="901f2-108">No.</span><span class="sxs-lookup"><span data-stu-id="901f2-108">None.</span></span>  
  
### <a name="child-elements"></a><span data-ttu-id="901f2-109">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="901f2-109">Child Elements</span></span>  
  
|<span data-ttu-id="901f2-110">Elemento</span><span class="sxs-lookup"><span data-stu-id="901f2-110">Element</span></span>|<span data-ttu-id="901f2-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="901f2-111">Description</span></span>|  
|-------------|-----------------|  
|[\<cryptoNameMapping>](cryptonamemapping-element.md)|<span data-ttu-id="901f2-112">Contiene i mapping di classi e nomi descrittivi.</span><span class="sxs-lookup"><span data-stu-id="901f2-112">Contains mappings of classes to friendly names.</span></span>|  
|[\<oidMap>](oidmap-element.md)|<span data-ttu-id="901f2-113">Contiene i mapping degli identificatori di oggetto (OID) ASN. 1 alle classi.</span><span class="sxs-lookup"><span data-stu-id="901f2-113">Contains ASN.1 object identifier (OID) mappings to classes.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="901f2-114">Elementi padre</span><span class="sxs-lookup"><span data-stu-id="901f2-114">Parent Elements</span></span>  
  
|<span data-ttu-id="901f2-115">Elemento</span><span class="sxs-lookup"><span data-stu-id="901f2-115">Element</span></span>|<span data-ttu-id="901f2-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="901f2-116">Description</span></span>|  
|-------------|-----------------|  
|`configuration`|<span data-ttu-id="901f2-117">Elemento radice in ciascun file di configurazione usato in Common Language Runtime e nelle applicazioni .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="901f2-117">The root element in every configuration file used by the common language runtime and .NET Framework applications.</span></span>|  
|`mscorlib`|<span data-ttu-id="901f2-118">Contiene l' `cryptographySettings` elemento.</span><span class="sxs-lookup"><span data-stu-id="901f2-118">Contains the `cryptographySettings` element.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="901f2-119">Esempio</span><span class="sxs-lookup"><span data-stu-id="901f2-119">Example</span></span>  
 <span data-ttu-id="901f2-120">Nell'esempio seguente viene illustrato come utilizzare l' **\<cryptographySettings>** elemento per contenere mapping dei nomi di crittografia e mapping OID.</span><span class="sxs-lookup"><span data-stu-id="901f2-120">The following example shows how use the **\<cryptographySettings>** element to contain cryptography name mappings and OID mappings.</span></span> <span data-ttu-id="901f2-121">Questo esempio configura il runtime in modo che <xref:System.Security.Cryptography.HashAlgorithm.Create%2A?displayProperty=nameWithType> restituisca un `MyHashClass` oggetto e la `MyCryptoClass` classe venga mappata all'identificatore di oggetto 1.3.36.2.1.</span><span class="sxs-lookup"><span data-stu-id="901f2-121">This example configures the runtime so that <xref:System.Security.Cryptography.HashAlgorithm.Create%2A?displayProperty=nameWithType> returns a `MyHashClass` object and the `MyCryptoClass` class maps to the object identifier 1.3.36.2.1.</span></span>  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyHash="MyHashClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
               <cryptoClass   MyCrypto="MyCryptoClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="System.Security.Cryptography.HashAlgorithm"  
                       class="MyHash"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.36.3.2.1"   name="MyCryptoClass"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="901f2-122">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="901f2-122">See also</span></span>

- [<span data-ttu-id="901f2-123">Schema del file di configurazione</span><span class="sxs-lookup"><span data-stu-id="901f2-123">Configuration File Schema</span></span>](../index.md)
- [<span data-ttu-id="901f2-124">Schema delle impostazioni di crittografia</span><span class="sxs-lookup"><span data-stu-id="901f2-124">Cryptography Settings Schema</span></span>](index.md)
- [<span data-ttu-id="901f2-125">Servizi di crittografia</span><span class="sxs-lookup"><span data-stu-id="901f2-125">Cryptographic Services</span></span>](../../../../standard/security/cryptographic-services.md)

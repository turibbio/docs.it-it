---
title: Sicurezza e Registro di sistema
ms.date: 07/20/2015
helpviewer_keywords:
- security [Visual Basic], registry
- registry [Visual Basic], security issues
ms.assetid: 9980aff7-2f69-492b-8f66-29a9a76d3df5
ms.openlocfilehash: 2eba9d177769b22de3f931bc7af4905a80e316b5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359968"
---
# <a name="security-and-the-registry-visual-basic"></a><span data-ttu-id="b3235-102">Sicurezza e Registro di sistema (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b3235-102">Security and the Registry (Visual Basic)</span></span>

<span data-ttu-id="b3235-103">In questo argomento vengono illustrate le implicazioni in termini di sicurezza della memorizzazione dei dati nel Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="b3235-103">This page discusses the security implications of storing data in the registry.</span></span>  
  
## <a name="permissions"></a><span data-ttu-id="b3235-104">Autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="b3235-104">Permissions</span></span>  

 <span data-ttu-id="b3235-105">Archiviare come testo nel Registro di sistema informazioni riservate, quali le password, può presentare dei rischi, anche se la chiave del Registro di sistema è protetta da elenchi di controllo di accesso (ACL, Access Control List).</span><span class="sxs-lookup"><span data-stu-id="b3235-105">It is not secure to store secrets, such as passwords, in the registry as plain text, even if the registry key is protected by ACLs (access control lists).</span></span>  
  
 <span data-ttu-id="b3235-106">L'uso del Registro di sistema può compromettere la sicurezza poiché consente l'accesso inappropriato alle risorse di sistema o alle informazioni protette.</span><span class="sxs-lookup"><span data-stu-id="b3235-106">Working with the registry may compromise security by allowing inappropriate access to system resources or protected information.</span></span> <span data-ttu-id="b3235-107">Per usare tali proprietà, è necessario avere autorizzazioni di lettura e scrittura derivanti dall'enumerazione <xref:System.Security.Permissions.RegistryPermissionAccess> che controlla l'accesso alle variabili del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="b3235-107">To use these properties, you must have read and write permissions from the <xref:System.Security.Permissions.RegistryPermissionAccess> enumeration, which controls access to registry variables.</span></span> <span data-ttu-id="b3235-108">Qualsiasi codice eseguito con attendibilità completa, che in base ai criteri di sicurezza predefiniti corrisponde al codice installato nel disco rigido locale dell'utente, ha le autorizzazioni necessarie per accedere al Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="b3235-108">Any code running with full trust (under the default security policy, this is any code installed on the user's local hard disk) has the necessary permissions to access the registry.</span></span> <span data-ttu-id="b3235-109">Per ulteriori informazioni, vedere la classe <xref:System.Security.Permissions.RegistryPermission>.</span><span class="sxs-lookup"><span data-stu-id="b3235-109">For more information, see <xref:System.Security.Permissions.RegistryPermission> class.</span></span>  
  
 <span data-ttu-id="b3235-110">Le variabili del Registro di sistema non devono essere memorizzate in posizioni di memoria accessibili da codice senza <xref:System.Security.Permissions.RegistryPermission>.</span><span class="sxs-lookup"><span data-stu-id="b3235-110">Registry variables should not be stored in memory locations where code without <xref:System.Security.Permissions.RegistryPermission> can access them.</span></span> <span data-ttu-id="b3235-111">Analogamente, concedere i privilegi minimi necessari a eseguire il lavoro.</span><span class="sxs-lookup"><span data-stu-id="b3235-111">Similarly, when granting permissions, grant the minimum privileges necessary to get the job done.</span></span>  
  
 <span data-ttu-id="b3235-112">I valori di accesso alle autorizzazioni per il Registro di sistema sono definiti dall'enumerazione <xref:System.Security.Permissions.RegistryPermissionAccess>.</span><span class="sxs-lookup"><span data-stu-id="b3235-112">Registry permission access values are defined by the <xref:System.Security.Permissions.RegistryPermissionAccess> enumeration.</span></span> <span data-ttu-id="b3235-113">Nella tabella riportata di seguito sono illustrati i dettagli dei membri.</span><span class="sxs-lookup"><span data-stu-id="b3235-113">The following table details its members.</span></span>  
  
|<span data-ttu-id="b3235-114">valore</span><span class="sxs-lookup"><span data-stu-id="b3235-114">Value</span></span>|<span data-ttu-id="b3235-115">Accesso alle variabili del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="b3235-115">Access to Registry Variables</span></span>|  
|-----------|----------------------------------|  
|`AllAccess`|<span data-ttu-id="b3235-116">Creazione, lettura e scrittura</span><span class="sxs-lookup"><span data-stu-id="b3235-116">Create, read, and write</span></span>|  
|`Create`|<span data-ttu-id="b3235-117">Create</span><span class="sxs-lookup"><span data-stu-id="b3235-117">Create</span></span>|  
|`NoAccess`|<span data-ttu-id="b3235-118">Nessun accesso</span><span class="sxs-lookup"><span data-stu-id="b3235-118">No access</span></span>|  
|`Read`|<span data-ttu-id="b3235-119">Lettura</span><span class="sxs-lookup"><span data-stu-id="b3235-119">Read</span></span>|  
|`Write`|<span data-ttu-id="b3235-120">Scrittura</span><span class="sxs-lookup"><span data-stu-id="b3235-120">Write</span></span>|  
  
## <a name="checking-values-in-registry-keys"></a><span data-ttu-id="b3235-121">Verifica dei valori nelle chiavi del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="b3235-121">Checking Values in Registry Keys</span></span>  

 <span data-ttu-id="b3235-122">Quando si crea un valore del Registro di sistema, è necessario decidere come procedere nel caso in cui tale valore esista già.</span><span class="sxs-lookup"><span data-stu-id="b3235-122">When you create a registry value, you need to decide what to do if that value already exists.</span></span> <span data-ttu-id="b3235-123">È possibile che un altro processo, forse dannoso, abbia già creato il valore e possa accedervi.</span><span class="sxs-lookup"><span data-stu-id="b3235-123">Another process, perhaps a malicious one, may have already created the value and have access to it.</span></span> <span data-ttu-id="b3235-124">I dati inseriti nel valore del Registro di sistema sono disponibili per altri processi.</span><span class="sxs-lookup"><span data-stu-id="b3235-124">When you put data in the registry value, the data is available to the other process.</span></span> <span data-ttu-id="b3235-125">Per evitare che ciò accada, usare il metodo `GetValue`.</span><span class="sxs-lookup"><span data-stu-id="b3235-125">To prevent this, use the `GetValue` method.</span></span> <span data-ttu-id="b3235-126">Restituisce `Nothing` se la chiave non esiste.</span><span class="sxs-lookup"><span data-stu-id="b3235-126">It returns `Nothing` if the key does not already exist.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="b3235-127">Durante la lettura del Registro di sistema da un'applicazione Web, l'identità dell'utente corrente dipende dall'autenticazione e dalla rappresentazione implementate nell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="b3235-127">When reading the registry from a Web application, the identity of current user depends on the authentication and impersonation implemented in the Web application.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b3235-128">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b3235-128">See also</span></span>

- <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>
- [<span data-ttu-id="b3235-129">Lettura e scrittura nel Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="b3235-129">Reading from and Writing to the Registry</span></span>](reading-from-and-writing-to-the-registry.md)

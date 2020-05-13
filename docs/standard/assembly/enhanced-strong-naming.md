---
title: Denominazione sicura avanzata
description: Le firme con nome sicuro convenzionali per gli assembly in .NET Framework presentano limitazioni. Informazioni sui nomi sicuri avanzati.
ms.date: 08/20/2019
helpviewer_keywords:
- strong-named assemblies
- strong naming [.NET Framework], enhanced
ms.assetid: 6cf17a82-62a1-4f6d-8d5a-d7d06dec2bb5
ms.openlocfilehash: 720eda86ef0555127da422b2f44a414e8bbfb1b7
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378958"
---
# <a name="enhanced-strong-naming"></a><span data-ttu-id="8c37e-104">Denominazione sicura avanzata</span><span class="sxs-lookup"><span data-stu-id="8c37e-104">Enhanced strong naming</span></span>
<span data-ttu-id="8c37e-105">Una firma con nome sicuro è un meccanismo di identità in .NET Framework per l'identificazione degli assembly.</span><span class="sxs-lookup"><span data-stu-id="8c37e-105">A strong name signature is an identity mechanism in the .NET Framework for identifying assemblies.</span></span> <span data-ttu-id="8c37e-106">È una firma digitale a chiave pubblica che in genere si usa per verificare l'integrità dei dati passati da un autore (firmatario) a un destinatario (verificatore).</span><span class="sxs-lookup"><span data-stu-id="8c37e-106">It is a public-key digital signature that is typically used to verify the integrity of data being passed from an originator (signer) to a recipient (verifier).</span></span> <span data-ttu-id="8c37e-107">Questa firma viene usata come identità univoca per un assembly e garantisce che i riferimenti all'assembly non siano ambigui.</span><span class="sxs-lookup"><span data-stu-id="8c37e-107">This signature is used as a unique identity for an assembly and ensures that references to the assembly are not ambiguous.</span></span> <span data-ttu-id="8c37e-108">L'assembly è firmato come parte del processo di compilazione e quindi verificato quando viene caricato.</span><span class="sxs-lookup"><span data-stu-id="8c37e-108">The assembly is signed as part of the build process and then verified when it is loaded.</span></span>  
  
 <span data-ttu-id="8c37e-109">Le firme con nome sicuro consentono di evitare che utenti malintenzionati possano manomettere un assembly e firmarlo nuovamente con la chiave del firmatario originale.</span><span class="sxs-lookup"><span data-stu-id="8c37e-109">Strong name signatures help prevent malicious parties from tampering with an assembly and then re-signing the assembly with the original signer’s key.</span></span> <span data-ttu-id="8c37e-110">Tuttavia, le chiavi con nome sicuro non contengono informazioni affidabili sul server di pubblicazione e non contengono una gerarchia di certificati.</span><span class="sxs-lookup"><span data-stu-id="8c37e-110">However, strong name keys don’t contain any reliable information about the publisher, nor do they contain a certificate hierarchy.</span></span> <span data-ttu-id="8c37e-111">Una firma con nome sicuro non garantisce l'affidabilità della persona che ha firmato l'assembly né indica se la persona è un legittimo proprietario della chiave, indica solo che il proprietario della chiave ha firmato l'assembly.</span><span class="sxs-lookup"><span data-stu-id="8c37e-111">A strong name signature does not guarantee the trustworthiness of the person who signed the assembly or indicate whether that person was a legitimate owner of the key; it indicates only that the owner of the key signed the assembly.</span></span> <span data-ttu-id="8c37e-112">Di conseguenza, non è consigliabile usare una firma con nome sicuro come validator di sicurezza per concedere l'attendibilità a codice di terze parti.</span><span class="sxs-lookup"><span data-stu-id="8c37e-112">Therefore, we do not recommend using a strong name signature as a security validator for trusting third-party code.</span></span> <span data-ttu-id="8c37e-113">Microsoft Authenticode è lo strumento consigliato per l'autenticazione di codice.</span><span class="sxs-lookup"><span data-stu-id="8c37e-113">Microsoft Authenticode is the recommended way to authenticate code.</span></span>  
  
## <a name="limitations-of-conventional-strong-names"></a><span data-ttu-id="8c37e-114">Limitazioni dei nomi sicuri convenzionali</span><span class="sxs-lookup"><span data-stu-id="8c37e-114">Limitations of conventional strong names</span></span>  
 <span data-ttu-id="8c37e-115">La tecnologia di denominazione sicura usata nelle versioni precedenti a .NET Framework 4.5 presenta queste limitazioni:</span><span class="sxs-lookup"><span data-stu-id="8c37e-115">The strong naming technology used in versions before the .NET Framework 4.5 has the following shortcomings:</span></span>  
  
- <span data-ttu-id="8c37e-116">Le chiavi sono costantemente sotto attacco e grazie all'uso di tecniche e hardware più evoluti è più semplice dedurre una chiave privata da una chiave pubblica.</span><span class="sxs-lookup"><span data-stu-id="8c37e-116">Keys are constantly under attack, and improved techniques and hardware make it easier to infer a private key from a public key.</span></span> <span data-ttu-id="8c37e-117">Per proteggersi dagli attacchi, sono necessarie chiavi di dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="8c37e-117">To guard against attacks, larger keys are necessary.</span></span> <span data-ttu-id="8c37e-118">Le versioni di .NET Framework precedenti a .NET Framework 4.5 offrono la possibilità di accedere con chiavi di qualsiasi dimensione (quella predefinita è 1024 bit), ma firmare un assembly con una nuova chiave interrompe tutti i file binari che fanno riferimento all'identità precedente dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="8c37e-118">.NET Framework versions before the .NET Framework 4.5 provide the ability to sign with any size key (the default size is 1024 bits), but signing an assembly with a new key breaks all binaries that reference the older identity of the assembly.</span></span> <span data-ttu-id="8c37e-119">È quindi estremamente difficile aggiornare la dimensione di una chiave di firma se si vuole mantenere la compatibilità.</span><span class="sxs-lookup"><span data-stu-id="8c37e-119">Therefore, it is extremely difficult to upgrade the size of a signing key if you want to maintain compatibility.</span></span>  
  
- <span data-ttu-id="8c37e-120">La firma con nome sicuro supporta solo l'algoritmo SHA-1.</span><span class="sxs-lookup"><span data-stu-id="8c37e-120">Strong name signing supports only the SHA-1 algorithm.</span></span> <span data-ttu-id="8c37e-121">Si è scoperto di recente che SHA-1 non è adeguato per le applicazioni che usano l'algoritmo SHA.</span><span class="sxs-lookup"><span data-stu-id="8c37e-121">SHA-1 has recently been found to be inadequate for secure hashing applications.</span></span> <span data-ttu-id="8c37e-122">È quindi necessario un algoritmo più robusto, ad esempio SHA-256 o superiore.</span><span class="sxs-lookup"><span data-stu-id="8c37e-122">Therefore, a stronger algorithm (SHA-256 or greater) is necessary.</span></span> <span data-ttu-id="8c37e-123">È possibile che in futuro SHA-1 non sia più conforme agli standard FIPS e questo può causare problemi agli utenti che scelgono di usare solo software e algoritmi conformi agli standard FIPS.</span><span class="sxs-lookup"><span data-stu-id="8c37e-123">It is possible that SHA-1 will lose its FIPS-compliant standing, which would present problems for those who choose to use only FIPS-compliant software and algorithms.</span></span>  
  
## <a name="advantages-of-enhanced-strong-names"></a><span data-ttu-id="8c37e-124">Vantaggi dei nomi sicuri avanzati</span><span class="sxs-lookup"><span data-stu-id="8c37e-124">Advantages of enhanced strong names</span></span>  
 <span data-ttu-id="8c37e-125">I vantaggi principali offerti dai nomi sicuri avanzati sono la compatibilità con nomi sicuri preesistenti e la possibilità di richiedere che un'identità sia equivalente a un'altra:</span><span class="sxs-lookup"><span data-stu-id="8c37e-125">The main advantages of enhanced strong names are compatibility with pre-existing strong names and the ability to claim that one identity is equivalent to another:</span></span>  
  
- <span data-ttu-id="8c37e-126">Gli sviluppatori che usano assembly firmati preesistenti possono eseguire la migrazione delle proprie identità agli algoritmi SHA-2 conservando la compatibilità con gli assembly che fanno riferimento alle identità precedenti.</span><span class="sxs-lookup"><span data-stu-id="8c37e-126">Developers who have pre-existing signed assemblies can migrate their identities to the SHA-2 algorithms while maintaining compatibility with assemblies that reference the old identities.</span></span>  
  
- <span data-ttu-id="8c37e-127">Gli sviluppatori che creano nuovi assembly e non ritengono rilevanti le firme con nome sicuro preesistenti possono usare gli algoritmi SHA-2, più sicuri, e firmare gli assembly come in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8c37e-127">Developers who create new assemblies and are not concerned with pre-existing strong name signatures can use the more secure SHA-2 algorithms and sign the assemblies as they always have.</span></span>  
  
## <a name="use-enhanced-strong-names"></a><span data-ttu-id="8c37e-128">Usa nomi sicuri avanzati</span><span class="sxs-lookup"><span data-stu-id="8c37e-128">Use enhanced strong names</span></span>  
 <span data-ttu-id="8c37e-129">Le chiavi con nome sicuro sono costituite da una chiave di firma e una chiave di identità.</span><span class="sxs-lookup"><span data-stu-id="8c37e-129">Strong name keys consist of a signature key and an identity key.</span></span> <span data-ttu-id="8c37e-130">L'assembly è firmato con la chiave di firma e identificato dalla chiave di identità.</span><span class="sxs-lookup"><span data-stu-id="8c37e-130">The assembly is signed with the signature key and is identified by the identity key.</span></span> <span data-ttu-id="8c37e-131">Nelle versioni precedenti a .NET Framework 4.5 queste due chiavi erano identiche.</span><span class="sxs-lookup"><span data-stu-id="8c37e-131">Prior to the .NET Framework 4.5, these two keys were identical.</span></span> <span data-ttu-id="8c37e-132">A partire da .NET Framework 4.5, la chiave di identità rimane la stessa delle versioni precedenti di .NET Framework, ma la chiave di firma è stata migliorata con un algoritmo hash più avanzato.</span><span class="sxs-lookup"><span data-stu-id="8c37e-132">Starting with the .NET Framework 4.5, the identity key remains the same as in earlier .NET Framework versions, but the signature key is enhanced with a stronger hash algorithm.</span></span> <span data-ttu-id="8c37e-133">Inoltre, la chiave di firma viene firmata con la chiave di identità per creare una controfirma.</span><span class="sxs-lookup"><span data-stu-id="8c37e-133">In addition, the signature key is signed with the identity key to create a counter-signature.</span></span>  
  
 <span data-ttu-id="8c37e-134">L'attributo <xref:System.Reflection.AssemblySignatureKeyAttribute> consente ai metadati dell'assembly di usare la chiave pubblica preesistente per l'identità dell'assembly e quindi i vecchi riferimenti all'assembly continuano a funzionare.</span><span class="sxs-lookup"><span data-stu-id="8c37e-134">The <xref:System.Reflection.AssemblySignatureKeyAttribute> attribute enables the assembly metadata to use the pre-existing public key for assembly identity, which allows old assembly references to continue to work.</span></span>  <span data-ttu-id="8c37e-135">L'attributo <xref:System.Reflection.AssemblySignatureKeyAttribute> usa la controfirma per verificare che il proprietario della nuova chiave di firma sia anche il proprietario della chiave di identità precedente.</span><span class="sxs-lookup"><span data-stu-id="8c37e-135">The <xref:System.Reflection.AssemblySignatureKeyAttribute> attribute uses the counter-signature to ensure that the owner of the new signature key is also the owner of the old identity key.</span></span>  
  
### <a name="sign-with-sha-2-without-key-migration"></a><span data-ttu-id="8c37e-136">Firma con SHA-2, senza migrazione della chiave</span><span class="sxs-lookup"><span data-stu-id="8c37e-136">Sign with SHA-2, without key migration</span></span>  
 <span data-ttu-id="8c37e-137">Eseguire i comandi seguenti da un prompt dei comandi per firmare un assembly senza eseguire la migrazione di una firma con nome sicuro:</span><span class="sxs-lookup"><span data-stu-id="8c37e-137">Run the following commands from a command prompt to sign an assembly without migrating a strong name signature:</span></span>  
  
1. <span data-ttu-id="8c37e-138">Generare la nuova chiave di identità, se necessario.</span><span class="sxs-lookup"><span data-stu-id="8c37e-138">Generate the new identity key (if necessary).</span></span>  
  
    ```console  
    sn -k IdentityKey.snk  
    ```  
  
2. <span data-ttu-id="8c37e-139">Estrarre la chiave pubblica di identità e specificare che deve essere usato un algoritmo SHA-2 per la firma con questa chiave.</span><span class="sxs-lookup"><span data-stu-id="8c37e-139">Extract the identity public key, and specify that a SHA-2 algorithm should be used when signing with this key.</span></span>  
  
    ```console  
    sn -p IdentityKey.snk IdentityPubKey.snk sha256  
    ```  
  
3. <span data-ttu-id="8c37e-140">Ritardare la firma dell'assembly con il file della chiave pubblica di identità.</span><span class="sxs-lookup"><span data-stu-id="8c37e-140">Delay-sign the assembly with the identity public key file.</span></span>  
  
    ```console  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
    ```  
  
4. <span data-ttu-id="8c37e-141">Firmare di nuovo l'assembly con la coppia di chiavi di identità completa.</span><span class="sxs-lookup"><span data-stu-id="8c37e-141">Re-sign the assembly with the full identity key pair.</span></span>  
  
    ```console  
    sn -Ra MyAssembly.exe IdentityKey.snk  
    ```  
  
### <a name="sign-with-sha-2-with-key-migration"></a><span data-ttu-id="8c37e-142">Firma con SHA-2, con migrazione della chiave</span><span class="sxs-lookup"><span data-stu-id="8c37e-142">Sign with SHA-2, with key migration</span></span>  
 <span data-ttu-id="8c37e-143">Eseguire i comandi seguenti da un prompt dei comandi per firmare un assembly con una firma con nome sicuro migrata.</span><span class="sxs-lookup"><span data-stu-id="8c37e-143">Run the following commands from a command prompt to sign an assembly with a migrated strong name signature.</span></span>  
  
1. <span data-ttu-id="8c37e-144">Generare una coppia di chiavi di identità e firma, se necessario.</span><span class="sxs-lookup"><span data-stu-id="8c37e-144">Generate an identity and signature key pair (if necessary).</span></span>  
  
    ```console  
    sn -k IdentityKey.snk  
    sn -k SignatureKey.snk  
    ```  
  
2. <span data-ttu-id="8c37e-145">Estrarre la chiave pubblica di firma e specificare che deve essere usato un algoritmo SHA-2 per la firma con questa chiave.</span><span class="sxs-lookup"><span data-stu-id="8c37e-145">Extract the signature public key, and specify that a SHA-2 algorithm should be used when signing with this key.</span></span>  
  
    ```console  
    sn -p SignatureKey.snk SignaturePubKey.snk sha256  
    ```  
  
3. <span data-ttu-id="8c37e-146">Estrarre la chiave pubblica di identità, che determina l'algoritmo hash che genera una controfirma.</span><span class="sxs-lookup"><span data-stu-id="8c37e-146">Extract the identity public key, which determines the hash algorithm that generates a counter-signature.</span></span>  
  
    ```console  
    sn -p IdentityKey.snk IdentityPubKey.snk  
    ```  
  
4. <span data-ttu-id="8c37e-147">Generare i parametri per un attributo <xref:System.Reflection.AssemblySignatureKeyAttribute> e allegare l'attributo all'assembly.</span><span class="sxs-lookup"><span data-stu-id="8c37e-147">Generate the parameters for a <xref:System.Reflection.AssemblySignatureKeyAttribute> attribute, and attach the attribute to the assembly.</span></span>  
  
    ```console  
    sn -a IdentityPubKey.snk IdentityKey.snk SignaturePubKey.snk  
    ```  

    <span data-ttu-id="8c37e-148">Si genera un output simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="8c37e-148">This produces output similar to the following.</span></span>

    ```output
    Information for key migration attribute.
    (System.Reflection.AssemblySignatureKeyAttribute):
    publicKey=
    002400000c80000094000000060200000024000052534131000400000100010005a3a81ac0a519
    d96244a9c589fc147c7d403e40ccf184fc290bdd06c7339389a76b738e255a2bce1d56c3e7e936
    e4fc87d45adc82ca94c716b50a65d39d373eea033919a613e4341c66863cb2dc622bcb541762b4
    3893434d219d1c43f07e9c83fada2aed400b9f6e44ff05e3ecde6c2827830b8f43f7ac8e3270a3
    4d153cdd

    counterSignature=
    e3cf7c211678c4d1a7b8fb20276c894ab74c29f0b5a34de4d61e63d4a997222f78cdcbfe4c91eb
    e1ddf9f3505a32edcb2a76f34df0450c4f61e376b70fa3cdeb7374b1b8e2078b121e2ee6e8c6a8
    ed661cc35621b4af53ac29c9e41738f199a81240e8fd478c887d1a30729d34e954a97cddce66e3
    ae5fec2c682e57b7442738
    ```

    <span data-ttu-id="8c37e-149">Questo output può poi essere convertito in AssemblySignatureKeyAttribute.</span><span class="sxs-lookup"><span data-stu-id="8c37e-149">This output can then be transformed into an AssemblySignatureKeyAttribute.</span></span>

    ```
    [assembly:System.Reflection.AssemblySignatureKeyAttribute(
    "002400000c80000094000000060200000024000052534131000400000100010005a3a81ac0a519d96244a9c589fc147c7d403e40ccf184fc290bdd06c7339389a76b738e255a2bce1d56c3e7e936e4fc87d45adc82ca94c716b50a65d39d373eea033919a613e4341c66863cb2dc622bcb541762b43893434d219d1c43f07e9c83fada2aed400b9f6e44ff05e3ecde6c2827830b8f43f7ac8e3270a34d153cdd",
    "e3cf7c211678c4d1a7b8fb20276c894ab74c29f0b5a34de4d61e63d4a997222f78cdcbfe4c91ebe1ddf9f3505a32edcb2a76f34df0450c4f61e376b70fa3cdeb7374b1b8e2078b121e2ee6e8c6a8ed661cc35621b4af53ac29c9e41738f199a81240e8fd478c887d1a30729d34e954a97cddce66e3ae5fec2c682e57b7442738"
    )]
    ```
  
5. <span data-ttu-id="8c37e-150">Ritardare la firma dell'assembly con la chiave pubblica di identità.</span><span class="sxs-lookup"><span data-stu-id="8c37e-150">Delay-sign the assembly with the identity public key.</span></span>  
  
    ```console  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
    ```  
  
6. <span data-ttu-id="8c37e-151">Firmare completamente l'assembly con la coppia di chiavi di firma.</span><span class="sxs-lookup"><span data-stu-id="8c37e-151">Fully sign the assembly with the signature key pair.</span></span>  
  
    ```console  
    sn -Ra MyAssembly.exe SignatureKey.snk  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="8c37e-152">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8c37e-152">See also</span></span>

- [<span data-ttu-id="8c37e-153">Creare e usare gli assembly con nome sicuro</span><span class="sxs-lookup"><span data-stu-id="8c37e-153">Create and use strong-named assemblies</span></span>](create-use-strong-named.md)

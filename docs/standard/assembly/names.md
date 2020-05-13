---
title: Nomi degli assembly
description: Informazioni sui nomi degli assembly .NET e sul relativo effetto sull'ambito dell'assembly e sull'utilizzo da parte di un'applicazione e informazioni sulla proprietà FullName.
ms.date: 08/19/2019
helpviewer_keywords:
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
ms.assetid: 8f8c2c90-f15d-400e-87e7-a757e4f04d0e
ms.openlocfilehash: 5a499f4f04c84de8d6542d7107d7a707b808e47f
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379879"
---
# <a name="assembly-names"></a>Nomi degli assembly
Il nome di un assembly viene archiviato nei metadati e ha un effetto significativo sull'ambito dell'assembly e sull'uso dell'assembly da parte di un'applicazione. Un assembly con un nome sicuro dispone di un nome completo costituito da nome, impostazioni cultura, chiave pubblica e numero di versione dell'assembly. Questo nome è spesso detto nome visualizzato. Nel caso degli assembly caricati è possibile ottenere tale nome con la proprietà <xref:System.Reflection.Assembly.FullName%2A>.

 Il runtime usa queste informazioni per individuare l'assembly e distinguerlo da altri assembly con lo stesso nome. Ad esempio un assembly con il nome sicuro `myTypes` può avere il seguente nome completo:

```
myTypes, Version=1.0.1234.0, Culture=en-US, PublicKeyToken=b77a5c561934e089c, ProcessorArchitecture=msil
```

> [!NOTE]
> In .NET Framework versione 2.0 all'identità dell'assembly viene aggiunta l'architettura del processore, per il supporto di versioni di assembly specifiche per un determinato processore. È possibile creare versioni di un assembly la cui identità differisce solo per l'architettura del processore, ad esempio versioni specifiche per processori a 32 bit o a 64 bit. L'architettura del processore non è obbligatoria per i nomi sicuri. Per altre informazioni, vedere <xref:System.Reflection.AssemblyName.ProcessorArchitecture%2A?displayProperty=nameWithType>.

 In questo esempio il nome completo indica che l'assembly `myTypes` ha un nome sicuro con un token di chiave pubblica, il valore di impostazioni cultura corrispondente a Inglese (Stati Uniti) e il numero di versione 1.0.1234.0. L'architettura del processore è "msil". Ciò significa che l'assembly sarà compilato con modalità JIT (Just-In-Time) in codice a 32 bit o a 64 bit a seconda del sistema operativo e del processore.

 Il codice che richiede i tipi in un assembly deve usare un nome dell'assembly completo. Questa caratteristica è detta associazione completa. L'associazione parziale che specifica solo il nome di un assembly non è consentita per il riferimento ad assembly in .NET Framework.

 Tutti i riferimenti ad assembly che costituiscono il .NET Framework devono contenere anche il nome completo dell'assembly. Ad esempio, un riferimento all'assembly System. Data .NET Framework per la versione 1,0 include:

```
System.data, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
```

 Si noti che la versione corrisponde al numero di versione di tutti gli assembly .NET Framework forniti con .NET Framework versione 1.0. Per gli assembly .NET Framework il valore delle impostazioni cultura è sempre neutro e la chiave pubblica è uguale a quella visualizzata nell'esempio precedente.

 Ad esempio per aggiungere un riferimento assembly a un file di configurazione per configurare un listener di traccia è necessario includere il nome dell'assembly completo per l'assembly .NET Framework di sistema:

```xml
<add name="myListener" type="System.Diagnostics.TextWriterTraceListener, System, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />
```

> [!NOTE]
> Il runtime non distingue tra maiuscole e minuscole durante l'associazione a un assembly, ma conserva le maiuscole o le maiuscole usate nel nome dell'assembly. Vari strumenti di Windows SDK rilevano la differenza tra maiuscole e minuscole nei nomi degli assembly. Per risultati ottimali è consigliabile gestire i nomi degli assembly includendo la distinzione tra maiuscole e minuscole.

## <a name="name-application-components"></a>Assegnare un nome ai componenti dell'applicazione
 Quando determina l'identità di un assembly il runtime non considera il nome file. L'identità dell'assembly, costituita da nome, versione, impostazioni cultura e nome sicuro dell'assembly, deve risultare chiara per il runtime.

 Se, ad esempio, si dispone di un assembly denominato MyAssembly *. exe* che fa riferimento a un assembly denominato MyAssembly *. dll*, l'associazione viene eseguita correttamente se si esegue *myAssembly. exe*. Tuttavia, se un'altra applicazione esegue *myAssembly. exe* usando il metodo <xref:System.AppDomain.ExecuteAssembly%2A?displayProperty=nameWithType> , il runtime determina che `myAssembly` è già caricato quando *myAssembly. exe* richiede l'associazione a `myAssembly` . In questo caso, *myAssembly. dll* non viene mai caricato. Poiché *myAssembly. exe* non contiene il tipo richiesto, <xref:System.TypeLoadException> si verifica un errore.

 Per evitare questo problema assicurarsi che gli assembly che costituiscono l'applicazione non abbiano lo stesso nome oppure posizionare gli assembly con lo stesso nome in directory diverse.

> [!NOTE]
> Nel .NET Framework, se si inserisce un assembly con nome sicuro nel Global Assembly Cache, il nome file dell'assembly deve corrispondere al nome dell'assembly, escluso l'estensione del nome file, ad esempio *. exe* o *. dll*. Se, ad esempio, il nome file di un assembly è *myAssembly. dll*, il nome dell'assembly deve essere `myAssembly` . Gli assembly privati distribuiti solo nella directory radice dell'applicazione possono avere un nome dell'assembly diverso dal nome file.

## <a name="see-also"></a>Vedere anche

- [Procedura: determinare il nome completo di un assembly](find-fully-qualified-name.md)
- [Creare assembly](create.md)
- [Assembly con nomi sicuri](strong-named.md)
- [Assembly Cache globale](../../framework/app-domains/gac.md)
- [Come il runtime individua gli assembly](../../framework/deployment/how-the-runtime-locates-assemblies.md)

---
title: Strumenti di .NET Framework
ms.date: 03/30/2017
helpviewer_keywords:
- command line, .NET Framework tools
- .NET Framework, tools
- tools [.NET Framework]
- running .NET Framework tools
ms.assetid: a2ca532d-91f7-426a-9303-417c2ee1247c
ms.openlocfilehash: 60a9cb241f289cacc7437174f112114e843aca47
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/20/2020
ms.locfileid: "81645556"
---
# <a name="net-framework-tools"></a>Strumenti di .NET Framework

Gli strumenti di .NET Framework facilitano la creazione, la distribuzione e la gestione di applicazioni e componenti destinati a .NET Framework.

La maggior parte degli strumenti di .NET Framework descritti in questa sezione vengono installati automaticamente con Visual Studio. Per scaricare Visual Studio, visitare la pagina [Download di Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019).

È possibile eseguire tutti gli strumenti dalla riga di comando, ad eccezione del Visualizzatore cache assembly (*Shfusion.dll*). È necessario accedere a *Shfusion.dll* da Esplora file.
  
Il modo migliore per eseguire gli strumenti da riga di comando è tramite il prompt dei comandi per gli sviluppatori per Visual Studio. Queste utilità consentono di eseguire gli strumenti facilmente, senza dover passare alla cartella di installazione. Per altre informazioni, vedere [Prompt dei comandi](developer-command-prompt-for-vs.md).

> [!NOTE]
> Alcuni strumenti sono specifici per computer a 32 bit o computer a 64 bit. Assicurarsi di eseguire la versione dello strumento appropriata per il computer.

## <a name="in-this-section"></a>Contenuto della sezione

- [Al.exe (Assembly Linker)](al-exe-assembly-linker.md)  
Genera un file che dispone di un manifesto dell'assembly ricavato da moduli o file di risorse.

- [Aximp.exe (utilità di importazione di controlli ActiveX di Windows Form)](aximp-exe-windows-forms-activex-control-importer.md)  
Consente di convertire le definizioni dei tipi in una libreria di tipi COM per un controllo ActiveX in un controllo Windows Form.

- [Caspol.exe (strumento criteri di sicurezza dall'accesso di codice)](caspol-exe-code-access-security-policy-tool.md)  
Consente di visualizzare e configurare i criteri di sicurezza stabiliti a livello di computer, di utente o dell'intera azienda. In .NET Framework 4 e versioni successive, questo strumento non influisce sui criteri di sicurezza `true`dall'accesso di codice, a meno che l'elemento [ \<> legacyCasPolicy](../configure-apps/file-schema/runtime/netfx40-legacysecuritypolicy-element.md) non sia impostato su . Per altre informazioni, vedere [Modifiche della sicurezza](https://docs.microsoft.com/previous-versions/dotnet/framework/security/security-changes).

- [Cert2spc.exe (Strumento di test certificati di L'autore del software)](cert2spc-exe-software-publisher-certificate-test-tool.md)  
Crea un certificato dell'editore del software (SPC, Software Publisher's Certificate) da uno o più certificati X.509. Questo strumento è finalizzato unicamente ai test.

- [Certmgr.exe (strumento Gestione certificati)](certmgr-exe-certificate-manager-tool.md)  
Consente di gestire certificati, elenchi di certificati attendibili (CTL, Certificate Trust List) ed elenchi di certificati revocati (CRL, Certificate Revocation List).

- [Clrver.exe (CLR Version Tool)](clrver-exe-clr-version-tool.md)  
Segnala tutte le versioni installate di Common Language Runtime (CLR) nel computer.

- [Prompt dei comandi](developer-command-prompt-for-vs.md)  
Consente di utilizzare gli strumenti di .NET Framework più facilmente. Questo prompt dei comandi imposta automaticamente variabili di ambiente specifiche.

- [CorFlags.exe (strumento di conversione CorFlags)](corflags-exe-corflags-conversion-tool.md)  
Consente di configurare la sezione CorFlags dell'intestazione di un'immagine PE.

- [Fuslogvw.exe (Visualizzatore registro associazione assembly)](fuslogvw-exe-assembly-binding-log-viewer.md)  
Visualizza informazioni sulle associazioni di assembly per consentire di diagnosticare per quale motivo non sia possibile individuare un assembly in fase di esecuzione.

- [Gacutil.exe (strumento Global Assembly Cache)](gacutil-exe-gac-tool.md)  
Consente di visualizzare e modificare il contenuto della Global Assembly Cache e della Download Cache.

- [Ilasm.exe (Assembler IL)](ilasm-exe-il-assembler.md)  
Genera un file eseguibile di tipo PE dal linguaggio intermedio (IL). È possibile eseguire il file eseguibile così ottenuto per determinare se il codice IL funziona come previsto.

- [Ildasm.exe (Disassembler IL)](ildasm-exe-il-disassembler.md)  
Accetta un file eseguibile di tipo PE contenente codice del linguaggio intermedio (IL) e crea un file di testo utilizzabile come input per l'assembler IL (Ilasm.exe).

- [Installutil.exe (strumento di installazione)](installutil-exe-installer-tool.md)  
Consente di installare e disinstallare le risorse del server eseguendo i componenti del programma di installazione di un assembly specificato. Funziona con le classi dello spazio dei nomi <xref:System.Configuration.Install>.

- [Lc.exe (compilatore di licenze)](lc-exe-license-compiler.md)  
Legge i file di testo che contengono informazioni sulle licenze e produce un file *con estensione licenses* che può essere incorporato in un eseguibile di Common Language Runtime come risorsa.

- [Mage.exe (Manifest Generation and Editing Tool)](mage-exe-manifest-generation-and-editing-tool.md)  
Consente di creare, modificare e firmare manifesti dell'applicazione e di distribuzione. Come strumento della riga di comando, *Mage.exe* può essere eseguito da script batch e altre applicazioni basate su Windows, incluse le applicazioni ASP.NET.

- [MageUI.exe (strumento di generazione e modifica di manifesti, client grafico)](mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)  
Supporta le stesse funzionalità dello strumento della riga di comando Mage.exe, ma usa un'interfaccia utente basata su Windows. Supporta la stessa funzionalità dello strumento della riga di comando *Mage.exe*, ma utilizza un'interfaccia utente basata su Windows.

- [MDbg.exe (debugger della riga di comando di .NET Framework)](mdbg-exe.md)  
Consente ai fornitori di strumenti e agli sviluppatori di applicazioni di individuare e correggere i bug dei programmi basati sul Common Language Runtime di .NET Framework. Questo strumento usa l'API di debug del runtime per offrire servizi di debug.

- [Mgmtclassgen.exe (Generatore di classi fortemente tipizzate di gestione)](mgmtclassgen-exe.md)  
Consente di generare una classe gestita con associazione anticipata per una classe Windows Management Instrumentation (WMI) specificata.

- [Mpgo.exe (strumento di ottimizzazione PGO gestiti)](mpgo-exe-managed-profile-guided-optimization-tool.md)  
Consente di ottimizzare gli assembly di immagini native usando scenari comuni dell'utente finale. Mpgo.exe consente la generazione e l'utilizzo di dati di profilatura per gli assembly di applicazioni di immagini native (non gli assembly .NET Framework) usando scenari di training selezionati dallo sviluppatore di applicazioni.

- [Ngen.exe (generatore di immagini native)](ngen-exe-native-image-generator.md)  
Migliora le prestazioni delle applicazioni gestite tramite l'utilizzo di immagini native, ovvero file che contengono codice macchina compilato specifico del processore. Il runtime può usare le immagini native della cache anziché il compilatore Just-In-Time (JIT) per compilare l'assembly originale.

- [Peverify.exe (strumento PEVerify)](peverify-exe-peverify-tool.md)  
Consente di verificare se il codice Microsoft Intermediate Language (MSIL) e i metadati associati soddisfano i requisiti di indipendenza dai tipi.

- [Regasm.exe (strumento di registrazione degli assembly)](regasm-exe-assembly-registration-tool.md)  
Legge i metadati in un assembly e aggiunge le voci necessarie nel Registro di sistema. In questo modo i client COM vengono visualizzati come classi .NET Framework.

- [Regsvcs.exe (strumento di installazione dei servizi .NET)](regsvcs-exe-net-services-installation-tool.md)  
Carica e registra un assembly, genera e installa una libreria dei tipi in un'applicazione specificata della versione 1.0 di COM+ e configura i servizi aggiunti a livello di codice a una classe.

- [Resgen.exe (generatore di file di risorse)](resgen-exe-resource-file-generator.md)  
Converte i file di testo (*txt* o *restext*) e i file in formato di risorsa basato su XML (*resx*) in file binari di Common Language Runtime (*.resources*) che possono essere incorporati in un eseguibile binario di runtime o compilati in assembly satellite.

- [SecAnnotate.exe (strumento di annotatore per la sicurezza .NET)](secannotate-exe-net-security-annotator-tool.md)  
Identifica le parti `SecurityCritical` e `SecuritySafeCritical` di un assembly.

- [SignTool.exe (strumento di firma)](signtool-exe.md)  
Consente di apporre una firma digitale ai file, di verificare le firme nei file e di apporre un timestamp ai file.

- [Sn.exe (strumento Nome sicuro)](sn-exe-strong-name-tool.md)  
Consente di creare assembly con nomi sicuri. In questo strumento sono disponibili opzioni per la gestione delle chiavi nonché per la generazione e la verifica delle firme.

- [SOS.dll (estensione per il debug SOS)](sos-dll-sos-debugging-extension.md)  
Facilita l'esecuzione del debug di programmi gestiti nel debugger WinDbg.exe e in Visual Studio fornendo informazioni sull'ambiente Common Language Runtime interno.

- [SqlMetal.exe (Code Generation Tool)](sqlmetal-exe-code-generation-tool.md)  
Genera codice e attributi di mapping per il componente LINQ to SQL di .NET Framework.

- [Storeadm.exe (strumento di archiviazione isolata)](storeadm-exe-isolated-storage-tool.md)  
Gestisce lo spazio di memorizzazione isolato, fornisce opzioni per elencare ed eliminare le archiviazioni dell'utente.

- [Tlbexp.exe (utilità di esportazione della libreria dei tipi)](tlbexp-exe-type-library-exporter.md)  
Genera una libreria dei tipi che descrive i tipi definiti in un assembly di Common Language Runtime.

- [Tlbimp.exe (utilità di importazione della libreria dei tipi)](tlbimp-exe-type-library-importer.md)  
Converte le definizioni dei tipi presenti in una libreria dei tipi COM nelle definizioni equivalenti di un assembly di Common Language Runtime.

- [Winmdexp.exe (strumento di esportazione dei metadati di Windows Runtime)](winmdexp-exe-windows-runtime-metadata-export-tool.md)  
Esporta un assembly .NET Framework compilato come file *con estensione winmdobj* in un componente di Windows Runtime, incluso nel pacchetto come file *con estensione winmd* contenente sia i metadati di Windows Runtime che le informazioni di implementazione.

- [Winres.exe (Editor risorse di Windows Form)](winres-exe-windows-forms-resource-editor.md)  
Consente di localizzare le risorse dell'interfaccia utente (file*con estensione resx* o *resources)* utilizzate da Windows Form. È possibile tradurre stringhe e quindi ridimensionare, spostare e nascondere i controlli per adattarli alle stringhe localizzate.

## <a name="related-sections"></a>Sezioni correlate

- [strumenti WPF](https://docs.microsoft.com/previous-versions/ms742404(v=vs.110))  
Include strumenti quali lo strumento di conformità isXPS (isXPS.exe) e gli strumenti di profilatura delle prestazioni.

- [Windows Communication Foundation Tools](../wcf/tools.md)  
Include strumenti che semplificano la creazione, la distribuzione e la gestione di applicazioni Windows Communication Foundation (WCF).

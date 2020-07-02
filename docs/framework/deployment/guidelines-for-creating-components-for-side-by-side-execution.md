---
title: Linee guida per la creazione di componenti per l'esecuzione affiancata di più versioni
description: Esaminare le linee guida per la creazione di componenti per l'esecuzione side-by-side. Ad esempio, associare l'identità del tipo a una determinata versione di file o usare l'archiviazione con supporto della versione.
ms.date: 03/30/2017
helpviewer_keywords:
- side-by-side execution, multiple application versions
- side-by-side execution, multiple component versions
ms.assetid: 5c540161-6e40-42e9-be92-6175aee2c46a
ms.openlocfilehash: f0d25984f2444d29d9fc0edb3add23b6adc04c62
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622640"
---
# <a name="guidelines-for-creating-components-for-side-by-side-execution"></a>Linee guida per la creazione di componenti per l'esecuzione affiancata di più versioni
Per creare applicazioni o componenti gestiti progettati per l'esecuzione affiancata, seguire le indicazioni generali riportate di seguito.  
  
- Associare l'identità del tipo a una determinata versione di un file.  
  
     In Common Language Runtime, l'identità del tipo viene associata a una determinata versione di file con assembly con nome sicuro. Per creare un'applicazione o un componente per l'esecuzione affiancata, è necessario assegnare a tutti gli assembly un nome sicuro. In questo modo, viene creata una precisa identità del tipo e viene garantito che qualsiasi risoluzione del tipo verrà reindirizzata al file corretto. Un assembly con nome sicuro contiene informazioni sulla versione, sulle impostazioni cultura e sull'editore che vengono usate dal runtime per trovare il file corretto in risposta a una richiesta di binding.  
  
- Usare l'archiviazione con supporto della versione.  
  
     Per fornire l'archiviazione con supporto della versione, nel runtime viene usata la Global Assembly Cache, che rappresenta una struttura di directory con supporto della versione che viene installata su qualsiasi computer in cui viene usato .NET Framework. Gli assembly installati nella Global Assembly Cache non vengono sovrascritti in caso di installazione di una nuova versione dell'assembly.  
  
- Creare un'applicazione o un componente che viene eseguito in modalità isolata.  
  
     Un'applicazione o un componente eseguito in modalità isolata deve riuscire a gestire le risorse in modo da evitare conflitti quando due istanze dell'applicazione o del componente vengono eseguite contemporaneamente. L'applicazione o il componente deve usare anche una struttura di file specifica della versione.  
  
## <a name="application-and-component-isolation"></a>Isolamento di applicazioni e componenti  
 L'isolamento costituisce un fattore determinante per la corretta progettazione di un'applicazione o di un componente per l'esecuzione affiancata. L'applicazione o il componente deve riuscire a gestire tutte le risorse, in particolare l'I/O di file, in modo isolato. Per assicurarsi che l'applicazione o il componente venga eseguito in modalità isolata, seguire le indicazioni riportate di seguito.  
  
- Scrivere i valori nel Registro di sistema in base alla versione. Archiviare i valori in hive o chiavi in cui viene indicata la versione e non condividere le informazioni o lo stato tra più versioni di un componente. Viene così impedita la sovrascrittura di informazioni da parte di due applicazioni eseguite contemporaneamente.  
  
- Impostare gli oggetti denominati del kernel in base alla versione, affinché non si verifichi una race condition. Una race condition si verifica ad esempio quando due semafori di due versioni della stessa applicazione si trovano in stato di reciproca attesa.  
  
- Usare nomi di file e directory che tengono conto delle informazioni sulla versione. Le strutture di file devono essere basate sulle informazioni relative alla versione.  
  
- Creare account utente e gruppi in base alla versione. Gli account utente e i gruppi creati da un'applicazione devono essere identificati in base alla versione. Non condividere account utente e gruppi tra versioni diverse di un'applicazione.  
  
## <a name="installing-and-uninstalling-versions"></a>Installazione o disinstallazione delle versioni  
 In occasione della progettazione di un'applicazione per l'esecuzione affiancata, seguire le indicazioni relative all'installazione e alla disinstallazione delle versioni:  
  
- Non eliminare dal Registro di sistema informazioni che potrebbero essere necessarie per altre applicazioni eseguite con una diversa versione di .NET Framework.  
  
- Non sostituire informazioni del Registro di sistema che potrebbero essere necessarie per altre applicazioni eseguite con una diversa versione di .NET Framework.  
  
- Non annullare la registrazione di componenti COM che potrebbero essere necessari per altre applicazioni eseguite con una diversa versione di .NET Framework.  
  
- Non modificare **InprocServer32** o altre voci del Registro di sistema per un server COM già registrato.  
  
- Non eliminare account utente o gruppi che potrebbero essere necessari per altre applicazioni eseguite con una diversa versione di .NET Framework.  
  
- Non aggiungere nel Registro di sistema informazioni contenenti un percorso che non tenga conto della versione.  
  
## <a name="file-version-number-and-assembly-version-number"></a>Numero di versione di file e assembly  
 La versione dei file costituisce una risorsa di versione Win32 non usata dal runtime. In generale, la versione dei file viene aggiornata anche per un aggiornamento sul posto. Due file identici possono disporre di informazioni sulla versione del file diverse e due file diversi possono disporre delle stesse informazioni sulla versione del file.  
  
 La versione degli assembly viene usata dal runtime per il binding di assembly. Due assembly identici con numeri di versione diversi vengono gestiti dal runtime come due assembly diversi.  
  
 Lo [strumento Global Assembly Cache (Gacutil.exe)](../tools/gacutil-exe-gac-tool.md) consente di sostituire un assembly solo quando il numero di versione del file è più recente. Windows Installer in genere non esegue l'installazione su un assembly a meno che il numero di versione dell'assembly non sia superiore.  
  
## <a name="see-also"></a>Vedere anche

- [Esecuzione side-by-side](side-by-side-execution.md)
- [Procedura: Abilitare e disabilitare il reindirizzamento di associazione automatico](../configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)

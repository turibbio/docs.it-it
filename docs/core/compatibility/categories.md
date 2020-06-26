---
title: Compatibilità
description: Informazioni sui modi in cui le modifiche al codice possono influenzare la compatibilità in .NET.
ms.date: 06/10/2019
ms.openlocfilehash: 1cf14b7ff4143367653bd1c305cc1dda6711f980
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85415693"
---
# <a name="how-code-changes-can-affect-compatibility"></a>Come possono influenzare la compatibilità con le modifiche al codice

Per *compatibilità* si intende la possibilità di compilare o eseguire codice in una versione di un'implementazione di .NET diversa da quella con cui il codice è stato sviluppato originariamente. Una [particolare modifica](index.md) può influire sulla compatibilità in sei modi diversi:

- [Modifiche funzionali](#behavioral-change)
- [Compatibilità binaria](#binary-compatibility)
- [Compatibilità con l'origine](#source-compatibility)
- [Compatibilità della fase di progettazione](#design-time-compatibility)
- [Compatibilità con le versioni precedenti](#backwards-compatibility)
- [Compatibilità](#forward-compatibility) con le edizioni (non obiettivo di .NET Core)

## <a name="behavioral-change"></a>Modifiche funzionali

Una modifica funzionale rappresenta una modifica del comportamento di un membro. La modifica può essere visibile esternamente (ad esempio, un metodo può generare un'eccezione diversa) oppure può rappresentare un'implementazione modificata (ad esempio, una modifica nel modo in cui viene calcolato un valore restituito, l'aggiunta o la rimozione di chiamate di metodo interne o anche un miglioramento significativo delle prestazioni).

Quando le modifiche funzionali sono visibili esternamente e modificano il contratto pubblico di un tipo, risultano facili da valutare poiché influiscono sulla compatibilità binaria. Le modifiche all'implementazione sono molto più difficili da valutare. A seconda della natura della modifica e della frequenza e dei modelli d'uso dell'API, l'impatto di una modifica può variare da grave a innocuo.

## <a name="binary-compatibility"></a>Compatibilità binaria

La compatibilità binaria si riferisce alla capacità di un consumer di un'API di usare l'API in una versione più recente senza ricompilarla. Le modifiche come l'aggiunta di metodi o l'aggiunta di una nuova implementazione di interfaccia a un tipo non influiscono sulla compatibilità binaria. Tuttavia, la rimozione o la modifica delle firme pubbliche di un assembly a causa della quale i consumer non possono più accedere alla stessa interfaccia esposta dall'assembly influiscono sulla compatibilità binaria. Una modifica di questo tipo viene definita *modifica senza compatibilità binaria*.

## <a name="source-compatibility"></a>Compatibilità con l'origine

La compatibilità con l'origine si riferisce alla capacità dei consumer esistenti di un'API di eseguire la ricompilazione per una versione più recente senza apportare alcuna modifica all'origine. Una *modifica incompatibile con l'origine* si verifica quando un consumer deve modificare il codice sorgente per poterlo compilare correttamente per una versione più recente di un'API.

## <a name="design-time-compatibility"></a>Compatibilità della fase di progettazione

La compatibilità della fase di progettazione si riferisce al mantenimento dell'esperienza in fase di progettazione in versioni diverse di Visual Studio e in altri ambienti di progettazione. Sebbene ciò possa interessare il comportamento o l'interfaccia utente degli strumenti di progettazione, l'aspetto più importante della compatibilità della fase di progettazione riguarda la compatibilità del progetto. Un progetto o una soluzione deve poter essere aperto e usato in una versione più recente dell'ambiente di progettazione.

## <a name="backwards-compatibility"></a>Compatibilità con le versioni precedenti

La compatibilità con le versioni precedenti si riferisce alla capacità di un consumer esistente di un'API di supportare l'esecuzione su una nuova versione mantenendo invariato il comportamento. Sia le modifiche funzionali che quelle alla compatibilità binaria influiscono sulla compatibilità con le versioni precedenti. Se un consumer non supporta l'esecuzione o funziona in modo diverso quando viene eseguito con la versione più recente dell'API, l'API è *incompatibile con le versioni precedenti*.

Le modifiche che interessano la compatibilità con le versioni precedenti sono sconsigliate, poiché gli sviluppatori si aspettano la compatibilità con le versioni precedenti di un'API.

## <a name="forward-compatibility"></a>Compatibilità con le versioni successive

La compatibilità con le versioni successive si riferisce alla capacità di un consumer esistente di un'API di supportare l'esecuzione su una versione precedente offrendo lo stesso comportamento. Se un consumer non supporta l'esecuzione o funziona in modo diverso quando viene eseguito in una versione precedente dell'API, l'API è *incompatibile con le versioni successive*.

Il mantenimento della compatibilità con le versioni successive impedisce virtualmente modifiche o aggiunte da una versione all'altra, perché tali modifiche impediscono l'esecuzione in una versione precedente a un consumer destinato a una versione successiva. Gli sviluppatori si aspettano che un consumer che si basa su un'API più recente potrebbe non funzionare correttamente con l'API precedente.

Mantenere la compatibilità con le edizioni successive non è un obiettivo di .NET Core.

## <a name="see-also"></a>Vedi anche

- [Valutare le modifiche che causano un'interruzione in .NET Core](index.md)

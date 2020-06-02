---
title: Convenzioni di denominazione generali
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- names [.NET Framework], conflicts
- type names, conflicts
- language-specific type names
- names [.NET Framework], about naming guidelines
- names [.NET Framework], abbreviations
- abbreviation naming guidelines
- acronym naming guidelines
- Hungarian notation
- names [.NET Framework], type names
- names [.NET Framework], acronyms
ms.assetid: d3a77ea1-75d2-4969-a8c3-3e1e3e1aaedc
ms.openlocfilehash: c90987fd28d5157cfb7f7eea4680b5ab4be1a200
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290954"
---
# <a name="general-naming-conventions"></a>Convenzioni di denominazione generali

In questa sezione vengono descritte le convenzioni di denominazione generali che riguardano la scelta di Word, le linee guida sull'utilizzo delle abbreviazioni e degli acronimi e consigli su come evitare l'utilizzo di nomi specifici della lingua.

## <a name="word-choice"></a>Scelta di Word
 ✔️ scegliere nomi di identificatori facilmente leggibili.

 Ad esempio, una proprietà denominata `HorizontalAlignment` è più leggibile in inglese rispetto a `AlignmentHorizontal` .

 ✔️ prediligono la leggibilità per brevità.

 Il nome della proprietà `CanScrollHorizontally` è migliore di `ScrollableX` (un riferimento oscuro all'asse X).

 ❌Non usare caratteri di sottolineatura, trattini o altri caratteri non alfanumerici.

 ❌Non usare la notazione ungherese.

 ❌EVITARE l'utilizzo di identificatori in conflitto con parole chiave di linguaggi di programmazione ampiamente utilizzati.

 In base alla regola 4 della Common Language Specification (CLS), tutti i linguaggi conformi devono fornire un meccanismo che consenta l'accesso agli elementi denominati che usano una parola chiave di tale lingua come identificatore. In C#, ad esempio, in questo caso viene utilizzato il segno @ come meccanismo di escape. Tuttavia, è comunque consigliabile evitare le parole chiave comuni perché è molto più difficile usare un metodo con la sequenza di escape rispetto a una senza di essa.

## <a name="using-abbreviations-and-acronyms"></a>Uso delle abbreviazioni e degli acronimi
 ❌Non usare abbreviazioni o contrazioni come parte dei nomi degli identificatori.

 Ad esempio, usare `GetWindow` anziché `GetWin` .

 ❌Non usare alcun acronimo che non sia ampiamente accettato e anche se sono, solo quando necessario.

## <a name="avoiding-language-specific-names"></a>Evitare nomi specifici della lingua
 ✔️ utilizzare nomi semanticamente interessanti anziché parole chiave specifiche della lingua per i nomi dei tipi.

 Ad esempio, `GetLength` è un nome migliore rispetto a `GetInt` .

 ✔️ utilizzano un nome di tipo CLR generico, anziché un nome specifico della lingua, nei rari casi in cui un identificatore non ha un significato semantico oltre il relativo tipo.

 Ad esempio, un metodo che converte in <xref:System.Int64> deve essere denominato `ToInt64` , non `ToLong` (perché <xref:System.Int64> è un nome CLR per l'alias specifico di C# `long` ). Nella tabella seguente vengono illustrati diversi tipi di dati di base utilizzando i nomi dei tipi CLR (nonché i nomi dei tipi corrispondenti per C#, Visual Basic e C++).

|C#|Visual Basic|C++|CLR|
|---------|------------------|-----------|---------|
|**sbyte**|**SByte**|**char**|**SByte**|
|**byte**|**Byte**|**unsigned char**|**Byte**|
|**short**|**Breve**|**short**|**Int16**|
|**ushort**|**UInt16**|**unsigned short**|**UInt16**|
|**int**|**Intero**|**int**|**Int32**|
|**uint**|**UInt32**|**int senza segno**|**UInt32**|
|**long**|**Long**|**__int64**|**Int64**|
|**ULONG**|**UInt64**|**unsigned __int64**|**UInt64**|
|**float**|**Singolo**|**float**|**Singolo**|
|**double**|**Doppio**|**double**|**Doppio**|
|**bool**|**Boolean**|**bool**|**Boolean**|
|**char**|**Char**|**wchar_t**|**Char**|
|**string**|**Stringa**|**Stringa**|**Stringa**|
|**object**|**Object**|**Object**|**Object**|

 ✔️ usano un nome comune, ad esempio `value` o `item` , anziché ripetere il nome del tipo, nei rari casi in cui un identificatore non ha un significato semantico e il tipo del parametro non è importante.

## <a name="naming-new-versions-of-existing-apis"></a>Assegnazione di un nome alle nuove versioni delle API esistenti
 ✔️ usare un nome simile a quello dell'API precedente durante la creazione di nuove versioni di un'API esistente.

 Ciò consente di evidenziare la relazione tra le API.

 ✔️ preferiscono aggiungere un suffisso anziché un prefisso per indicare una nuova versione di un'API esistente.

 Questa operazione aiuterà l'individuazione durante l'esplorazione della documentazione o l'uso di IntelliSense. La versione precedente dell'API verrà organizzata vicino alle nuove API, perché la maggior parte dei browser e di IntelliSense mostrano gli identificatori in ordine alfabetico.

 ✔️ CONSIGLIABILE usare un identificatore nuovo, ma significativo, anziché aggiungere un suffisso o un prefisso.

 ✔️ usare un suffisso numerico per indicare una nuova versione di un'API esistente, in particolare se il nome esistente dell'API è l'unico nome che ha senso (ad esempio, se è uno standard di settore) e se l'aggiunta di un suffisso significativo (o la modifica del nome) non è un'opzione appropriata.

 ❌Non usare il suffisso "ex" (o simile) per un identificatore per distinguerlo da una versione precedente della stessa API.

 ✔️ usare il suffisso "64" quando si introducono versioni di API che operano su un intero a 64 bit (un valore Long Integer) invece che su un intero a 32 bit. È necessario adottare questo approccio solo quando esiste l'API a 32 bit esistente. non eseguire questa operazione per le API nuovissime con una versione a 64 bit.

 *Parti &copy; 2005, 2009 Microsoft Corporation. Tutti i diritti riservati.*

 *Ristampato con l'autorizzazione di Pearson Education, Inc. da [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2a edizione](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) di Krzysztof Cwalina and Brad Abrams, pubblicato il 22 ottobre 2008 da Addison-Wesley Professional nella collana Microsoft Windows Development Series.*

## <a name="see-also"></a>Vedere anche

- [Linee guida per la progettazione di framework](index.md)
- [Convenzioni di denominazione](naming-guidelines.md)
- [.NET naming conventions for EditorConfig](/visualstudio/ide/editorconfig-naming-conventions) (Convenzioni di denominazione .NET per EditorConfig)

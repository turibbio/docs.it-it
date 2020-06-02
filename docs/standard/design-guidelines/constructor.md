---
title: Progettazione di costruttori
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines, constructors
- constructors, design guidelines
- instance constructors
- type constructors
- virtual members
- constructors, types
- parameterless constructors
- static constructors
ms.assetid: b4496afe-5fa7-4bb0-85ca-70b0ef21e6fc
ms.openlocfilehash: a258bebac57258cc1e8fbe2d6b5ccce88cb28872
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84280348"
---
# <a name="constructor-design"></a>Progettazione di costruttori

Esistono due tipi di costruttori: costruttori di tipi e costruttori di istanze.

I costruttori di tipi sono statici e vengono eseguiti da CLR prima di utilizzare il tipo. I costruttori di istanza vengono eseguiti quando viene creata un'istanza di un tipo.

I costruttori di tipi non possono assumere parametri. I costruttori di istanze possono. I costruttori di istanze che non accettano parametri sono spesso denominati costruttori senza parametri.

I costruttori rappresentano il modo più naturale per creare istanze di un tipo. La maggior parte degli sviluppatori cercherà e tenterà di usare un costruttore prima di prendere in considerazione modi alternativi per creare istanze, ad esempio i metodi factory.

✔️ CONSIGLIABILE fornire costruttori semplici e idealmente predefiniti.

Un costruttore semplice ha un numero molto ridotto di parametri e tutti i parametri sono primitivi o enumerazioni. Tali costruttori semplici aumentano l'usabilità del Framework.

✔️ VALUTARE l'uso di un metodo factory statico anziché di un costruttore se la semantica dell'operazione desiderata non viene mappata direttamente alla costruzione di una nuova istanza o se segue le linee guida di progettazione del costruttore si ritengono non naturale.

✔️ usare i parametri del costruttore come collegamenti per l'impostazione delle proprietà principali.

Non deve esserci alcuna differenza nella semantica tra l'uso del costruttore vuoto seguito da alcuni set di proprietà e l'uso di un costruttore con più argomenti.

✔️ utilizzare lo stesso nome per i parametri del costruttore e una proprietà se i parametri del costruttore vengono utilizzati per impostare semplicemente la proprietà.

L'unica differenza tra tali parametri e le proprietà dovrebbe essere la combinazione di maiuscole e minuscole.

✔️ ESEGUIRE operazioni minime nel costruttore.

I costruttori non devono eseguire molto lavoro oltre a acquisire i parametri del costruttore. Il costo di qualsiasi altra elaborazione deve essere posticipato fino a quando richiesto.

✔️ generano eccezioni dai costruttori di istanza, se appropriato.

✔️ dichiarare in modo esplicito il costruttore pubblico senza parametri nelle classi, se tale costruttore è obbligatorio.

Se non si dichiara in modo esplicito alcun costruttore in un tipo, molti linguaggi (ad esempio C#) aggiungeranno automaticamente un costruttore pubblico senza parametri. (Le classi astratte ottengono un costruttore protetto).

L'aggiunta di un costruttore con parametri a una classe impedisce al compilatore di aggiungere il costruttore senza parametri. Questo causa spesso modifiche di rilievo accidentali.

❌EVITARE di definire in modo esplicito costruttori senza parametri per gli struct.

In questo modo la creazione di matrici risulta più veloce, perché se il costruttore senza parametri non è definito, non è necessario eseguirlo in ogni slot della matrice. Si noti che molti compilatori, incluso C#, non consentono agli struct di avere costruttori senza parametri per questo motivo.

❌EVITARE di chiamare membri virtuali su un oggetto all'interno del relativo costruttore.

La chiamata a un membro virtuale provocherà la chiamata dell'override più derivato, anche se il costruttore del tipo più derivato non è ancora stato completamente eseguito.

## <a name="type-constructor-guidelines"></a>Linee guida sui costruttori di tipi

✔️ rendere privati i costruttori statici.

Un costruttore statico, detto anche costruttore di classe, viene usato per inizializzare un tipo. CLR chiama il costruttore statico prima che venga creata la prima istanza del tipo o venga chiamato qualsiasi membro statico del tipo. L'utente non ha alcun controllo sul momento in cui viene chiamato il costruttore statico. Se un costruttore statico non è privato, può essere chiamato da codice diverso da CLR. A seconda delle operazioni eseguite nel costruttore, questo può causare un comportamento imprevisto. Il compilatore C# forza i costruttori statici come privati.

❌Non generare eccezioni dai costruttori statici.

Se un'eccezione viene generata da un costruttore di tipo, il tipo non è utilizzabile nel dominio applicazione corrente.

✔️ PROVARE a inizializzare i campi statici inline invece di usare in modo esplicito i costruttori statici, perché il runtime è in grado di ottimizzare le prestazioni dei tipi che non hanno un costruttore statico definito in modo esplicito.

*Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti riservati.*

*Ristampato con l'autorizzazione di Pearson Education, Inc. da [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2a edizione](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) di Krzysztof Cwalina and Brad Abrams, pubblicato il 22 ottobre 2008 da Addison-Wesley Professional nella collana Microsoft Windows Development Series.*

## <a name="see-also"></a>Vedere anche

- [Linee guida per la progettazione di membri](member.md)
- [Linee guida per la progettazione di Framework](index.md)
